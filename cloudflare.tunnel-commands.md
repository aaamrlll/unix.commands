# Steps linux server via cloudflare tunnerl and Nginx

### Configure server

# Install cloudflared
cd /tmp
curl -L -o cloudflared.deb \
https://github.com/cloudflare/cloudflared/releases/latest/download/cloudflared-linux-amd64.deb
sudo dpkg -i cloudflared.deb
sudo apt -f install -y
# Login into cloudflare and chose a zone to grant permissions to (Create a special DNS record like
_xxxx.suffragium.net)
cloudflared tunnel login
# After login and zone verify .pem file was created
ls ~/.cloudflared
# Create a tunnel and name
cloudflared tunnel create home-server
# Verify it created a credentials file for that tunnel
cloudflared tunnel list
# Create a host name (can create for ssh too)
cloudflared tunnel route dns home-server home.suffragium.net
cloudflared tunnel route dns home-server ssh.suffragium.net
# Create the tunnel configuration file
sudo mkdir -p /etc/cloudflared
# Edit config file
sudo nano /etc/cloudflared/config.yml

# Example
tunnel: 7311b664-0b90-413f-a74a-07c3f758dee6
credentials-file: /home/belial/.cloudflared/7311b664-0b90-413f-a74a-07c3f758dee6.json

ingress:
  - hostname: home.suffragium.net
    service: http://localhost:80

  - hostname: ssh.suffragium.net
    service: ssh://localhost:22

  - service: http_status:404

# Start the tunnel server to test
sudo cloudflared tunnel run home-server
# Verify port 80 is listening
sudo ss -ltnp | grep ':80' || true

### NGINX

# Install nginx 
sudo apt install -y nginx
# Enable Nginx
sudo systemctl enable --now nginx
# Confirm it
sudo ss -ltnp | grep ':80'
# Test tunnel is working
curl -I https://home.suffragium.net
# Make a home page dir and copy the page files there
sudo mkdir -p /var/www/home
# Set permissions
sudo chown -R www-data:www-data /var/www/home
sudo find /var/www/home -type d -exec chmod 755 {} \;
sudo find /var/www/home -type f -exec chmod 644 {} \;
# Configure Nginx
sudo nano /etc/nginx/sites-available/home.suffragium.net

# Example
server {
    listen 80;
    server_name home.suffragium.net;

    # Static site
    root /var/www/home;
    index index.html;

    location / {
        try_files $uri $uri/ /index.html;
    }

    # API
    location /siempre-nota/api/ {
        proxy_pass http://127.0.0.1:5000/;
        proxy_http_version 1.1;

        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;

        proxy_read_timeout 60s;
        proxy_send_timeout 60s;
    }
}

# Optional instead configurea new tunnel host
# Edit config file
sudo nano /etc/cloudflared/config.yml
# Add an other host name and port
  - hostname: api.suffragium.net
    service: http://localhost:8080
# Create the hostname and restart
cloudflared tunnel route dns home-server api.suffragium.net
sudo systemctl restart cloudflared
# Create an ew Nginx site
sudo nano /etc/nginx/sites-available/api.suffragium.net

# Example
server {
    listen 8080;
    server_name api.suffragium.net;

    location / {
        proxy_pass http://127.0.0.1:5000;
        proxy_http_version 1.1;

        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
        
        proxy_read_timeout 60s;
        proxy_send_timeout 60s;
    }
}

# Remove default nginx site and enable new sites
sudo ln -sf /etc/nginx/sites-available/home.suffragium.net /etc/nginx/sites-enabled/home.suffragium.net
sudo rm -f /etc/nginx/sites-enabled/default
# Optional in case of multiple sites
sudo ln -sf /etc/nginx/sites-available/api.suffragium.net /etc/nginx/sites-enabled/


# Verify config
sudo nginx -t
# Reload Nginx service
sudo systemctl reload nginx

# If needed start .net api dll
ASPNETCORE_URLS=http://127.0.0.1:5000 dotnet YourApi.dll

### Make tunnel persistent

# Install cloudflared service
sudo cloudflared service install
# Enable the service
sudo systemctl enable --now cloudflared
# Confirm
sudo systemctl status cloudflared --no-pager

### Configure client for ssh

# Install cloudflared Mac
brew install cloudflared
# Install Linux
cd /tmp
curl -L -o cloudflared.deb \
https://github.com/cloudflare/cloudflared/releases/latest/download/cloudflared-linux-amd64.deb
sudo dpkg -i cloudflared.deb
sudo apt -f install -y
# Configure client ssh hosts Mac
nano ~/.ssh/config

# Example
Host home.suffragium
    HostName ssh.suffragium.net
    ProxyCommand cloudflared access ssh --hostname %h
    User belial
    IdentityFile ~/.ssh/id_ed25519

Host suffragium
    HostName <IpAddress>
    User aaron
    IdentityFile ~/.ssh/id_ed25519

# Configure client ssh hosts Ubuntu add IdentitiesOnly and IdentityAgent if ubuntu blocks it
nano ~/.ssh/config

# Example
Host suffragium
    HostName <IpAddress>
    User aaron
    IdentityFile ~/.ssh/id_ed25519
    IdentitiesOnly yes
    IdentityAgent none


# Generate ssh keys
ssh-keygen -t ed25519 -C "aaron.alanis@suffragium.net"
# On server create an ssh folder if needed
mkdir -p ~/.ssh
# Copy SSH keys to Server
nano ~/.ssh/authorized_keys
# Set permissions
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys
# Lockdown ssh server
sudo nano /etc/ssh/sshd_config

# Example
PasswordAuthentication no
PubkeyAuthentication yes
PermitRootLogin no
ChallengeResponseAuthentication no
UsePAM yes
X11Forwarding no

# Restart SSH server
sudo systemctl daemon-reload
sudo systemctl restart ssh.socket
sudo systemctl restart ssh
# Configure servers firewall
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw enable

