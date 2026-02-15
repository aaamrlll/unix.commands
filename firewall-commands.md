# Linux/Mac Commands

### Firewall

# Reset Firewall rules
sudo ufw --force reset
# Default lockdown
sudo ufw default deny incoming
# Default outgoing
sudo ufw default allow outgoing
# Enable specific port
sudo ufw allow <portNumber>/tcp
# Enable specific por LAN only
sudo ufw allow from 192.168.1.0/24 to any port <portNumber> proto tcp
# Review current rules indexes
sudo ufw status numbered
# Remove by index
sudo ufw delete <index>
# Enable firewall
sudo ufw enable
