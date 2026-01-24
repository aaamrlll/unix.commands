# Linux/Mac Commands

### Remove NVM
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