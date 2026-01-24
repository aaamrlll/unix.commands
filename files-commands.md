# Linux/Mac Commands

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

### File Moves
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

### File Permissions
```
chmod u=rw,g=r,o=r file               # Permisos rw-r--r--
chmod u+x script.sh                   # Hace un archivo ejecutable
chmod -R u=rwx,g=rx,o=rx folder       # Permisos recursivos rwx-rx-rx
chown user:group file                 # Cambia dueño y grupo
chown -R user:group folder            # Cambia dueño recursivamente
```

---