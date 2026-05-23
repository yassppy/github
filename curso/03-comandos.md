### 🔰 Inicialización

```bash
git init                      # Inicializa un nuevo repositorio .git con configuración e historial
git clone <repo-url>          # Clona un repositorio desde una URL
```

### 🛠️ Desarrollo diario

```bash
git status                    # Muestra el estado de los cambios
git add <archivo.html>        # Añade un archivo específico al área de preparación
git add *.html                # Añade todos los archivos con una extensión específica
git add src/component-*       # Añade archivos que sigan un patrón
git add .                     # Añade todos los archivos del directorio actual
git add -A                    # Añade todos los archivos con cambios en el proyecto
git add -u                    # Añade solo archivos modificados o eliminados (no nuevos)
git commit -m "mensaje"       # Confirma los cambios: mueve el staging al repositorio
```

> 💡 **¿Cada cuánto debo hacer un commit?**  
> Cuando completes una feature o una unidad lógica de trabajo. Con IA puedes agrupar varios cambios relacionados en un solo commit bien descrito.  
> Revisar: [Conventional Commits — Guía práctica](assets-git/conventional_commits.png)

### 🌲 Gestión de ramas

```bash
git branch                    # Lista las ramas
git branch <nombre-rama>      # Crea una nueva rama
git switch <nombre-rama>      # Cambia a una rama
git branch -d <nombre-rama>   # Elimina una rama (solo si ya fue fusionada)
```

### 🤝 Integración y colaboración

```bash
git merge <rama>              # Fusiona los cambios de una rama en la actual
git remote add <nombre> <url> # Añade un repositorio remoto
git push <remoto> <rama>      # Envía los commits locales al repositorio remoto
git pull <remoto> <rama>      # Descarga y fusiona cambios desde el remoto
```

### ⏪ Recuperación y limpieza

```bash
git fetch                     # Descarga cambios remotos sin fusionarlos
git reset --hard HEAD         # Descarta todos los cambios locales sin guardar
git revert <hash-commit>      # Crea un commit que deshace los cambios de otro
```

### ✨ Avanzado y utilidades

```bash
git diff <a> <b>              # Compara dos commits, ramas o archivos
git show <hash>               # Muestra los detalles y cambios de un commit
git stash                     # Guarda cambios temporales y limpia el working tree
git stash pop                 # Restaura los últimos cambios guardados en el stash
git cherry-pick <hash>        # Aplica un commit específico en la rama actual
git rebase <base>             # Reaplica commits sobre otra rama base
```
