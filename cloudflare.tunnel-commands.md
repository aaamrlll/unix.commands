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

    root /var/www/home;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }
}

# Remove default nginx site
sudo ln -sf /etc/nginx/sites-available/home.suffragium.net /etc/nginx/sites-enabled/home.suffragium.net
sudo rm -f /etc/nginx/sites-enabled/default
# Verify config
sudo nginx -t
# Reload Nginx service
sudo systemctl reload nginx

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

# Configure client ssh hosts Ubuntu
nano ~/.ssh/config

# Example
Host home.suffragium
    HostName ssh.suffragium.net
    ProxyCommand cloudflared access ssh --hostname %h
    User belial
    IdentityFile ~/.ssh/id_ed25519


# Generate ssh keys
ssh-keygen -t ed25519 -C "aaron.alanis@suffragium.net"
# Copy SSH keys to Server
nano ~/.ssh/authorized_keys
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

