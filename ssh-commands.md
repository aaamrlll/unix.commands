# Linux/Mac Commands

### SSH Server

# SSH server config file
sudo nano /etc/ssh/sshd_config
# Valida la configuracion
sudo sshd -t
# Reload cuando cambia la configuracion
sudo systemctl daemon-reload.
# En caso de que el server use socket unit en la configuracion
sudo systemctl restart ssh.socket
# En caso de que se ocupe hacer un restart para aplicar configuracion
sudo systemctl restart ssh




### SSH Client

# Ruta a folder ssh
cd ~/.ssh
# Solo owner tiene acceso
chmod 700 ~/.ssh
# Solo owner tiene acceso
chmod 600 id_ed25519
# Non sensitive
chmod 644 id_ed25519.pub
# Solo owner tiene acceso
chmod 600 id_ed25519_ent
# Non sensitive
chmod 644 id_ed25519_ent.pub




### SSH File transfers

# Pasar el contenido de la carpeta al server
rsync -avz proyectoAngular123/ user@serverIp:/var/www/app/
# Descarga el contenido de la carpeta al cliente
rsync -a user@serverIp:/var/www/app/angularDeploy/ .
# Pasar un archivo al server
rsync -a backup.sql user@serverIp:/home/belial/
# Descargar un archivo al cliente
rsync -a user@serverIp:/etc/nginx/nginx.conf .
# Mantiene sincronización exacta
parametro --delete
# Modo archivo (recursivo + preserva permisos y timestamps)
parametro -a
# Muestra qué archivos se transfieren
parametro -v
# Compresión durante la transferencia
parametro -z
# Hace solo simulacion
parametro --dry-run
# Muestra el progreso
parametro --progress
# Copia solo el contenido
parametro carpetaEjemplo/
# Copia la carpeta y su contenido
parametro carpetaEjemplo



