# Ubuntu Home Server via Cloudflare Tunnel + Nginx + .NET API + SSH

## Overview

This setup provides:

-   Static website: home.suffragium.net
-   SSH access: ssh.suffragium.net
-   Optional API: api.suffragium.net or path-based routing
-   No router port forwarding
-   No public IP exposure
-   SSH key-only authentication
-   Firewall default-deny inbound

------------------------------------------------------------------------

# 1) Install Cloudflared (Server)

cd /tmp curl -L -o cloudflared.deb
https://github.com/cloudflare/cloudflared/releases/latest/download/cloudflared-linux-amd64.deb
sudo dpkg -i cloudflared.deb sudo apt -f install -y cloudflared
--version

------------------------------------------------------------------------

# 2) Authenticate Server with Cloudflare

cloudflared tunnel login ls \~/.cloudflared

Confirm: - cert.pem exists

------------------------------------------------------------------------

# 3) Create Tunnel

cloudflared tunnel create home-server cloudflared tunnel list ls
\~/.cloudflared/\*.json

Confirm: - Tunnel ID is listed - Credentials JSON file exists

------------------------------------------------------------------------

# 4) Create DNS Routes

cloudflared tunnel route dns home-server home.suffragium.net cloudflared
tunnel route dns home-server ssh.suffragium.net cloudflared tunnel route
dns home-server api.suffragium.net

Verify DNS: dig home.suffragium.net +short dig ssh.suffragium.net +short

Should return \*.cfargotunnel.com

------------------------------------------------------------------------

# 5) Install and Configure Nginx

sudo apt update sudo apt install -y nginx sudo systemctl enable --now
nginx sudo ss -ltnp \| grep ':80'

Confirm: - Port 80 is listening

------------------------------------------------------------------------

# 6) Deploy Website

sudo mkdir -p /var/www/home sudo rsync -av --delete /path/to/your/site/
/var/www/home/ sudo chown -R www-data:www-data /var/www/home sudo find
/var/www/home -type d -exec chmod 755 {} ; sudo find /var/www/home -type
f -exec chmod 644 {} ;

Test locally: curl -I http://127.0.0.1/

------------------------------------------------------------------------

# 7) Nginx Site Config

sudo nano /etc/nginx/sites-available/home.suffragium.net

server { listen 80; server_name home.suffragium.net;

    root /var/www/home;
    index index.html;

    location / {
        try_files $uri $uri/ /index.html;
    }

}

sudo ln -sf /etc/nginx/sites-available/home.suffragium.net
/etc/nginx/sites-enabled/ sudo rm -f /etc/nginx/sites-enabled/default
sudo nginx -t sudo systemctl reload nginx

------------------------------------------------------------------------

# 8) Cloudflare Tunnel Config

sudo mkdir -p /etc/cloudflared sudo nano /etc/cloudflared/config.yml

tunnel: `<TUNNEL_ID>`{=html} credentials-file:
/home/belial/.cloudflared/`<TUNNEL_ID>`{=html}.json

ingress: - hostname: home.suffragium.net service: http://127.0.0.1:80

-   hostname: ssh.suffragium.net service: ssh://127.0.0.1:22

-   hostname: api.suffragium.net service: http://127.0.0.1:8080

-   service: http_status:404

Test: sudo cloudflared tunnel run home-server

Confirm externally: https://home.suffragium.net

------------------------------------------------------------------------

# 9) Make Tunnel Persistent

sudo cloudflared service install sudo systemctl enable --now cloudflared
sudo systemctl status cloudflared --no-pager

------------------------------------------------------------------------

# 10) .NET API Setup

Publish: sudo mkdir -p /opt/myapi sudo dotnet publish -c Release -o
/opt/myapi

Create service user: sudo useradd --system --no-create-home --shell
/usr/sbin/nologin myapi \|\| true sudo chown -R myapi:myapi /opt/myapi

Create service: sudo nano /etc/systemd/system/myapi.service

\[Unit\] Description=My ASP.NET Core API After=network-online.target

\[Service\] Type=simple User=myapi WorkingDirectory=/opt/myapi
Environment=ASPNETCORE_URLS=http://127.0.0.1:5000
ExecStart=/usr/bin/dotnet /opt/myapi/YourApi.dll Restart=always

\[Install\] WantedBy=multi-user.target

Enable: sudo systemctl daemon-reload sudo systemctl enable --now myapi
sudo systemctl status myapi --no-pager

------------------------------------------------------------------------

# 11) SSH Hardening

sudo nano /etc/ssh/sshd_config

PasswordAuthentication no PubkeyAuthentication yes PermitRootLogin no
ChallengeResponseAuthentication no UsePAM yes

sudo systemctl restart ssh sudo systemctl status ssh --no-pager

------------------------------------------------------------------------

# 12) Firewall (UFW)

sudo ufw --force reset sudo ufw default deny incoming sudo ufw default
allow outgoing sudo ufw enable sudo ufw status verbose

------------------------------------------------------------------------

# Final State Verification Checklist

-   cloudflared tunnel list shows tunnel
-   systemctl status cloudflared shows active (running)
-   curl http://127.0.0.1 works locally
-   https://home.suffragium.net works externally
-   ssh suffragiumhome connects via tunnel
-   sudo ufw status shows default deny incoming