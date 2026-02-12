# Linux/Mac Commands

### Memory check
```
# Estado de memoria
free -h
# Reinicia servicios
sudo systemctl restart NetworkManager
# Procesos en tiempo real
top
# Mejor versión (si está instalada)
htop
# Procesos que más memoria usan
ps aux --sort=-%mem | head
```

---

### Clean apt y snap
```
# Elimina dependencias no usadas
sudo apt autoremove --purge
# Limpia paquetes .deb antiguos
sudo apt autoclean
# Borra todo el cache de apt
sudo apt clean
# Lista versiones instaladas
snap list --all
# Borra versiones viejas
sudo snap remove <snap> --revision <id>
```

---

### Cache and logs
```
# Revisa cache del sistema
sudo du -sh /var/cache/*
# Limpia temporales (runtime-safe)
sudo rm -rf /tmp/*
# Uso de logs del sistema
sudo journalctl --disk-usage
# Borra logs > 7 días
sudo journalctl --vacuum-time=7d
```

---

### Remove NVM
```
rm -rf ~/.nvm
# For bash
nano ~/.zshrc
nano ~/.bash_profile
# Also check nano ~/.profile
nano ~/.bashrc
brew uninstall nvm
sudo rm -rf /usr/local/nvm
unset NVM_DIR
unset NVM_CD_FLAGS
unset NVM_BIN
command -v nvm
nvm --version
```

---

### Remove Node (Global)
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