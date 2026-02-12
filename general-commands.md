# Linux/Mac Commands

### Update Server
```
fastfetch                           # informacion del sistema
sudo apt update                     # Lista actualizaciones
sudo apt upgrade                    # Actualiza
apt install <packname pname2 ...>   # Installa o Actualiza
ls /var/run/reboot-required         # Si el folder existe el reinicio es requerido
```

---

### Disk Usage
```
find ~ -type f -size +1G -exec ls -lh {} \;                                         # Encuentra archivos de 1GB
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

### Usuario Ubuntu
```
sudo adduser <username>           # Agrega usuario
sudo usermod -aG sudo <username>  # Agrega a sudo
```

---

### SSH Ubuntu
```
cd ~/.ssh                       # Ruta a folder ssh
chmod 700 ~/.ssh                # Solo owner tiene acceso
chmod 600 id_ed25519            # Solo owner tiene acceso
chmod 644 id_ed25519.pub        # Non sensitive
chmod 600 id_ed25519_ent        # Solo owner tiene acceso
chmod 644 id_ed25519_ent.pub    # Non sensitive

```
