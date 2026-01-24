# Linux/Mac Commands

### Git – Web Development & Collaboration
```
git init                                      # Inicializa un repositorio
git clone <repo-url>                          # Clona un repositorio remoto
git status                                    # Estado del working tree
git config user.name "Your Name"              # Configura nombre (local)
git config user.email "you@email.com"         # Configura email (local)
```

---

### Staging & Commits
```
git add .                                     # Agrega todos los cambios
git add <file>                                # Agrega archivo específico
git commit -m "message"                       # Commit
git commit --amend                            # Modifica el último commit
git reset <file>                              # Saca archivo del staging
git restore <file>                            # Descarta cambios locales
git restore --staged <file>                   # Quita archivo del staging
```

---

### Branching
```
git branch                                    # Lista ramas
git branch <branch-name>                      # Crea rama
git checkout <branch-name>                   # Cambia de rama
git checkout -b <branch-name>                # Crea y cambia a nueva rama
git switch <branch-name>                     # Cambia de rama (moderno)
git switch -c <branch-name>                  # Crea y cambia de rama
git branch -d <branch-name>                  # Borra rama local
```

---

### Merging & Rebase
```
git merge <branch-name>                      # Merge de rama
git rebase <branch-name>                     # Rebase sobre otra rama
git rebase -i HEAD~n                         # Rebase interactivo
git cherry-pick <commit>                     # Aplica commit específico
```

---

### Remote / Collaboration
```
git remote -v                                # Lista remotos
git remote add origin <url>                  # Agrega remoto
git fetch                                    # Trae cambios sin aplicar
git pull                                     # Fetch + merge
git pull --rebase                            # Pull usando rebase
git push                                     # Push a remoto
git push -u origin <branch>                  # Set upstream
git push origin --delete <branch>            # Borra rama remota
```

---

### History & Diff
```
git log                                      # Historial completo
git log --oneline --graph --decorate         # Historial visual
git show <commit>                            # Muestra commit
git diff                                     # Cambios no stageados
git diff --staged                            # Cambios en staging
git blame <file>                             # Quién cambió cada línea
```

---

### Stash (muy común en web dev)
```
git stash                                    # Guarda cambios temporales
git stash list                               # Lista stashes
git stash pop                                # Restaura último stash
git stash apply                              # Aplica stash sin borrarlo
```

---

### Tags & Releases
```
git tag                                      # Lista tags
git tag v1.0.0                               # Crea tag
git push origin v1.0.0                       # Publica tag
git push origin --tags                       # Publica todos los tags
```

---

### Cleanup / Recovery
```
git clean -fd                                # Borra archivos no trackeados
git reset --hard HEAD                       # Descarta TODO cambio local
git reflog                                   # Historial de referencias (rescates)
```

---