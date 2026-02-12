# Linux/Mac Commands

### SSH Server
```
sudo nano /etc/ssh/sshd_config      # SSH server config file
sudo sshd -t                        # Valida la configuracion
sudo systemctl daemon-reload.       # Reload cuando cambia la configuracion
sudo systemctl restart ssh.socket   # En caso de que el server use socket unit en la configuracion
sudo systemctl restart ssh          # En caso de que se ocupe hacer un restart para aplicar configuracion
```

---

### SSH Client
```
cd ~/.ssh                           # Ruta a folder ssh
chmod 700 ~/.ssh                    # Solo owner tiene acceso
chmod 600 id_ed25519                # Solo owner tiene acceso
chmod 644 id_ed25519.pub            # Non sensitive
chmod 600 id_ed25519_ent            # Solo owner tiene acceso
chmod 644 id_ed25519_ent.pub        # Non sensitive
```

---

### SSH File transfers
```
rsync -avz proyectoAngular123/ user@serverIp:/var/www/app/      # Pasar el contenido de la carpeta al server
rsync -a user@serverIp:/var/www/app/angularDeploy/ .            # Descarga el contenido de la carpeta al cliente
rsync -a backup.sql user@serverIp:/home/belial/                 # Pasar un archivo al server
rsync -a user@serverIp:/etc/nginx/nginx.conf .                  # Descargar un archivo al cliente
parametro --delete                                              # Mantiene sincronización exacta
parametro -a                                                    # Modo archivo (recursivo + preserva permisos y timestamps)
parametro -v                                                    # Muestra qué archivos se transfieren
parametro -z                                                    # Compresión durante la transferencia
parametro --dry-run                                             # Hace solo simulacion
parametro --progress                                            # Muestra el progreso
parametro carpetaEjemplo/                                       # Copia solo el contenido
parametro carpetaEjemplo                                        # Copia la carpeta y su contenido

```

---