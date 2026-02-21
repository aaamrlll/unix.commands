# Linux/Mac Commands

### Open / Run Files

# Muestra contenido corto
cat file
# Visualiza archivo largo
less file
# Edita archivo con nano
nano file
# Edita archivo con vi
vi file
# Abre archivo con app por defecto
xdg-open file
# Ejecuta script local
./script.sh
# Ejecuta script con bash
bash script.sh
# Ejecuta script con sh
sh script.sh




### File Moves

# Muestra el directorio actual
pwd
# Lista archivos con permisos y tamaños
ls -lah
# Crea un directorio
mkdir <folder>
# Crea directorios anidados
mkdir -p a/b/c
# Crea archivo vacío o actualiza timestamp
touch <file>
# Copia archivo
cp file1 file2
# Copia directorios recursivamente
cp -r dir1 dir2
# Renombra archivo o directorio
mv oldname newname
# Mueve archivo
mv file /path/dest/
# Borra archivo
rm file
# Borra directorio y contenido
rm -r folder
# Borra forzado (peligroso)
rm -rf folder
# Detalles completos del archivo
stat file
# Detecta tipo de archivo
file file




### File Permissions

# Permisos rw-r--r--
chmod u=rw,g=r,o=r file
# Hace un archivo ejecutable
chmod u+x script.sh
# Permisos recursivos rwx-rx-rx
chmod -R u=rwx,g=rx,o=rx folder
# Cambia dueño y grupo
chown user:group file
# Cambia dueño recursivamente
chown -R user:group folder



### Mount usb or drives

# crear una carpeta para montar -p para crear si no existe
sudo mkdir -p /mnt/usb1
# monta el drive -t para especifical el file system
sudo mount -t exfat /dev/sdc4 /mnt/usb1
# lista archivos del drive
ls -la /mnt/usb
# copiar archivos
cp /mnt/usb/file.ext ~/
# desmonstar la carpeta se puede reutilizar
sudo umount /mnt/usb1

