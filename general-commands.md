# Linux/Mac Commands

## Update Server
```
sudo apt update                     # Lista actualizaciones
sudo apt upgrade                    # Actualiza
apt install <packname pname2 ...>   # Installa o Actualiza
ls /var/run/reboot-required         # Si el folder existe el reinicio es requerido
```

## Disk Usage
```
df -h                                                                               # Lista el uso del disco
df -h /media/belial/BACKUP "/media/belial/WEDDING L&A"                              # Lista el uso de los discos especificados
sudo du -h / --max-depth=1 | sort -hr | head -n 20                                  # Lista los directorios root dependiente por GBs
sudo du -h /<folder>/<subfolder> --max-depth=1 | sort -hr | head -n 20              # Lista directorios específicos dependiente
sudo find / -type f -size +100M -exec ls -lh {} \; | sort -k 5 -hr | head -n 20     # Encuentra archivos mayores de 100 MB
```

---
### Disk Copy / Backup (USB → SSD)
```
rsync -aHAX --progress "/media/belial/WEDDING L&A/" /media/belial/BACKUP/                             # Copia archivos sin borrar contenido existente
rsync -aHAX --delete --progress "/media/belial/WEDDING L&A/" /media/belial/BACKUP/                    # Espejo exacto (borra extras en destino)
rsync -aHAX --dry-run "/media/belial/WEDDING L&A/" /media/belial/BACKUP/                              # Simula copia (size + mtime)
rsync -aHAX --dry-run --checksum "/media/belial/WEDDING L&A/" /media/belial/BACKUP/                   # Verificación byte-por-byte sin copiar
rsync -aHAX --dry-run --checksum --info=progress2 "/media/belial/WEDDING L&A/" /media/belial/BACKUP/  # Verificación con progreso global
rsync -aHAX --partial --append-verify --progress "/media/belial/WEDDING L&A/" /media/belial/BACKUP/   # Reanuda copias interrumpidas
sha256sum "/media/belial/WEDDING L&A/2. Videos/Documental Leslie y Aarón.mp4"                         # Hash para verificar un archivo específico
```

---

### File Moves & Permissions
```
pwd                                   # Muestra el directorio actual
ls -lah                               # Lista archivos con permisos y tamaños
mkdir <folder>                        # Crea un directorio
mkdir -p a/b/c                        # Crea directorios anidados
touch <file>                          # Crea archivo vacío o actualiza timestamp
cp file1 file2                        # Copia archivo
cp -r dir1 dir2                       # Copia directorios recursivamente
mv oldname newname                    # Renombra archivo o directorio
mv file /path/dest/                   # Mueve archivo
rm file                               # Borra archivo
rm -r folder                          # Borra directorio y contenido
rm -rf folder                         # Borra forzado (peligroso)
chmod u=rw,g=r,o=r file               # Permisos rw-r--r--
chmod u+x script.sh                   # Hace un archivo ejecutable
chmod -R u=rwx,g=rx,o=rx folder       # Permisos recursivos rwx-rx-rx
chown user:group file                 # Cambia dueño y grupo
chown -R user:group folder            # Cambia dueño recursivamente
stat file                             # Detalles completos del archivo
file file                             # Detecta tipo de archivo
```

---

### Open / Run Files
```
cat file            # Muestra contenido corto
less file           # Visualiza archivo largo
nano file           # Edita archivo con nano
vi file             # Edita archivo con vi
xdg-open file       # Abre archivo con app por defecto
./script.sh         # Ejecuta script local
bash script.sh      # Ejecuta script con bash
sh script.sh        # Ejecuta script con sh
```

---

## Docker Clean Unsafe
```
docker system df                  # Uso de disco de docker para antes y después
docker container prune            # Borra contenedores detenidos
docker image prune                # Borra imágenes sin uso
docker volume prune               # Borra volumen sin uso
docker system prune               # Borra todo lo sin uso
docker system prune --volumes     # Borra volúmenes (peligroso)
```

## Docker
```
docker compose up -d              # Para iniciar un contenedor
docker compose down               # Para detener un contenedor
```

---

## Usuario Ubuntu
```
sudo adduser <username>           # Agrega usuario
sudo usermod -aG sudo <username>  # Agrega a sudo
```

---

## Remove NVM
```
rm -rf ~/.nvm
nano ~/.zshrc                     # For bash
nano ~/.bash_profile
nano ~/.bashrc                    # Also check nano ~/.profile
brew uninstall nvm
sudo rm -rf /usr/local/nvm
unset NVM_DIR
unset NVM_CD_FLAGS
unset NVM_BIN
command -v nvm
nvm --version
```

---

## Remove Node (Global)
```
sudo rm -rf /usr/local/lib/node_modules
sudo rm -rf /usr/local/include/node
sudo rm -rf /usr/local/lib/node
sudo rm -rf /usr/local/include/node_modules
sudo rm /usr/local/bin/node
sudo rm /usr/local/bin/npm
sudo rm /usr/local/bin/npx
rm -rf ~/.npm
rm -rf ~/.npmrc
rm -rf ~/.node_repl_history
rm -rf ~/.node-gyp
sudo rm -rf /usr/local/share/man/man1/node*
sudo rm -rf /usr/local/share/man/man1/npm*
sudo rm -rf /opt/node
sudo rm -rf /opt/npm
brew uninstall node
brew uninstall npm
brew cleanup
```
