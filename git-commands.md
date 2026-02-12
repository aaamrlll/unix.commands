# Linux/Mac Commands

### Git – Web Development & Collaboration
```
# Inicializa un repositorio
git init
# Clona un repositorio remoto
git clone <repo-url>
# Estado del working tree
git status
# Configura nombre (local)
git config user.name "Your Name"
# Configura email (local)
git config user.email "you@email.com"
```

---

### Staging & Commits
```
# Agrega todos los cambios
git add .
# Agrega archivo específico
git add <file>
# Commit
git commit -m "message"
# Modifica el último commit
git commit --amend
# Saca archivo del staging
git reset <file>
# Descarta cambios locales
git restore <file>
# Quita archivo del staging
git restore --staged <file>
```

---

### Branching
```
# Lista ramas
git branch
# Crea rama
git branch <branch-name>
# Cambia de rama
git checkout <branch-name>
# Crea y cambia a nueva rama
git checkout -b <branch-name>
# Cambia de rama (moderno)
git switch <branch-name>
# Crea y cambia de rama
git switch -c <branch-name>
# Borra rama local
git branch -d <branch-name>
```

---

### Merging & Rebase
```
# Merge de rama
git merge <branch-name>
# Rebase sobre otra rama
git rebase <branch-name>
# Rebase interactivo
git rebase -i HEAD~n
# Aplica commit específico
git cherry-pick <commit>
```

---

### Remote / Collaboration
```
# Lista remotos
git remote -v
# Agrega remoto
git remote add origin <url>
# Trae cambios sin aplicar
git fetch
# Fetch + merge
git pull
# Pull usando rebase
git pull --rebase
# Push a remoto
git push
# Set upstream
git push -u origin <branch>
# Borra rama remota
git push origin --delete <branch>
```

---

### History & Diff
```
# Historial completo
git log
# Historial visual
git log --oneline --graph --decorate
# Muestra commit
git show <commit>
# Cambios no stageados
git diff
# Cambios en staging
git diff --staged
# Quién cambió cada línea
git blame <file>
```

---

### Stash (muy común en web dev)
```
# Guarda cambios temporales
git stash
# Lista stashes
git stash list
# Restaura último stash
git stash pop
# Aplica stash sin borrarlo
git stash apply
```

---

### Tags & Releases
```
# Lista tags
git tag
# Crea tag
git tag v1.0.0
# Publica tag
git push origin v1.0.0
# Publica todos los tags
git push origin --tags
```

---

### Cleanup / Recovery
```
# Borra archivos no trackeados
git clean -fd
# Descarta TODO cambio local
git reset --hard HEAD
# Historial de referencias (rescates)
git reflog
```

---