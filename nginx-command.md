# Linux/Mac Commands

### Service Control (Systemd)

# Verifica el estado del servicio
sudo systemctl status nginx
# Inicia el servicio
sudo systemctl start nginx
# Detiene el servicio
sudo systemctl stop nginx
# Reinicia el servicio (corte completo)
sudo systemctl restart nginx
# Recarga configuración (sin caída de sesiones)
sudo systemctl reload nginx
# Habilita inicio automático al arrancar
sudo systemctl enable nginx
# Deshabilita inicio automático
sudo systemctl disable nginx

### Configuration & Validation

# Prueba la sintaxis de los archivos de config
sudo nginx -t
# Muestra la versión instalada
nginx -v
# Muestra configuración completa activa
nginx -T
# Edita la configuración principal
sudo nano /etc/nginx/nginx.conf
# Edita sitio específico
sudo nano /etc/nginx/sites-available/default

### Permissions & Ownership (The "Belial" Setup)

# Cambia dueño al usuario y su grupo personal llamado igual(Recursivo)
sudo chown -R <USER1>:<USER1> /var/www/home
# Cambia dueño al grupo web (www-data)
sudo chown -R www-data:www-data /var/www/home
# Permisos estándar (775: Dueño/Grupo todo, Otros lectura)
sudo chmod -R 775 /var/www/home
# Forzar herencia de grupo (SetGID bit) alo nuevos archivos copiados
sudo chmod g+s /var/www/home
# Agrega tu usuario al grupo de nginx y relogeas
sudo usermod -aG www-data <USER>

### Deployment & File Transfer (rsync)

# Sincroniza archivos (Local -> Server)
rsync -avz /local/path/ user@host:/var/www/home/
# Sincroniza y borra archivos obsoletos en destino
rsync -avz --delete /local/path/ user@host:/var/www/home/
# Sincroniza ignorando permisos de origen
rsync -avz --no-perms --no-owner --no-group /local/path/ user@host:/var/www/home/

### Logs & Troubleshooting

# Ver errores en tiempo real (Nginx Error Log)
sudo tail -f /var/log/nginx/error.log
# Ver accesos en tiempo real (Access Log)
sudo tail -f /var/log/nginx/access.log
# Ver logs de sistema del servicio nginx
sudo journalctl -u nginx -f
# Buscar errores específicos en el log
grep "error" /var/log/nginx/error.log

### Ports & Networking

# Lista puertos en escucha (ver si el 80/443 están activos)
sudo ss -tulpn | grep LISTEN
# Verifica si el firewall permite HTTP/HTTPS
sudo ufw status
# Permite tráfico Nginx en el firewall
sudo ufw allow 'Nginx Full'
# Recarga el firewall
sudo ufw reload

### Symbolic Links (Atomic Deploys)

# Crea link simbólico de disponible a habilitado
sudo ln -s /etc/nginx/sites-available/myapp /etc/nginx/sites-enabled/
# Borra el link (deshabilita el sitio)
sudo rm /etc/nginx/sites-enabled/myapp
# Crea link de carpeta de versión a carpeta 'current'
ln -sfn /var/www/releases/v1 /var/www/home