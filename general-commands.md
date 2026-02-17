# Linux/Mac Commands

### Update Server

# informacion del sistema
fastfetch
# Lista actualizaciones
sudo apt update
# Actualiza
sudo apt upgrade
# Installa o Actualiza
apt install <packname pname2 ...>
# Si el folder existe el reinicio es requerido
ls /var/run/reboot-required

# WIFI on macs
sudo apt install broadcom-sta-common broadcom-sta-dkms


### Disk Usage

# Encuentra archivos de 1GB
find ~ -type f -size +1G -exec ls -lh {} \;
# Lista el uso del disco
df -h
# Lista el uso de los discos especificados
df -h /media/belial/BACKUP "/media/belial/WEDDING L&A"
# Lista los directorios root dependiente por GBs
sudo du -h / --max-depth=1 | sort -hr | head -n 20
# Lista directorios específicos dependiente
sudo du -h /<folder>/<subfolder> --max-depth=1 | sort -hr | head -n 20
# Encuentra archivos mayores de 100 MB
sudo find / -type f -size +100M -exec ls -lh {} \; | sort -k 5 -hr | head -n 20




### Disk Copy / Backup (USB → SSD)

# Copia archivos sin borrar contenido existente
rsync -aHAX --progress "/media/belial/WEDDING L&A/" /media/belial/BACKUP/
# Espejo exacto (borra extras en destino)
rsync -aHAX --delete --progress "/media/belial/WEDDING L&A/" /media/belial/BACKUP/
# Simula copia (size + mtime)
rsync -aHAX --dry-run "/media/belial/WEDDING L&A/" /media/belial/BACKUP/
# Verificación byte-por-byte sin copiar
rsync -aHAX --dry-run --checksum "/media/belial/WEDDING L&A/" /media/belial/BACKUP/
# Verificación con progreso global
rsync -aHAX --dry-run --checksum --info=progress2 "/media/belial/WEDDING L&A/" /media/belial/BACKUP/
# Reanuda copias interrumpidas
rsync -aHAX --partial --append-verify --progress "/media/belial/WEDDING L&A/" /media/belial/BACKUP/
# Hash para verificar un archivo específico
sha256sum "/media/belial/WEDDING L&A/2. Videos/Documental Leslie y Aarón.mp4"




### Usuario Ubuntu

# Agrega usuario
sudo adduser <username>
# Agrega a sudo
sudo usermod -aG sudo <username>

