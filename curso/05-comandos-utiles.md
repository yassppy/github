## 🔍 Comandos útiles en Git

---

### `git status` — Estado del área de trabajo

Muestra qué archivos están en el working directory, cuáles están en el staging
area y cuáles aún no tienen seguimiento.

```bash
git status        # Vista completa
git status -s     # Vista reducida (short)
```

La salida completa tiene tres secciones:

```
Changes to be committed:        ← están en staging, listos para commit
  new file: index.html

Changes not staged for commit:  ← modificados pero fuera del staging
  modified: main.js

Untracked files:                ← Git no les hace seguimiento todavía
  src/
```

En la vista reducida `-s` cada archivo tiene una letra de prefijo:

| Prefijo | Significado |
|---------|-------------|
| `A` | Archivo nuevo añadido al staging |
| `M` | Archivo modificado |
| `??` | Archivo sin seguimiento (untracked) |

#### Personalizar colores de `git status`

Puedes cambiar el color con el que se muestran los archivos en cada estado.
El valor del color puede ser un nombre (`red`, `blue`, `magenta`) o un número
de la paleta xterm-256.

```bash
git config color.status.branch magenta       # color del nombre de la rama
git config color.status.added blue           # color de archivos en staging
git config color.status.untracked "141 bold" # color con número xterm (entre comillas)
```

> 💡 Si tu terminal no reconoce el color, busca `xterm 256` para ver la tabla
> de colores compatibles con tu emulador de terminal.

---

### `git log` — Historial de commits

Muestra la información completa de cada commit: hash SHA-1, autor, fecha
y mensaje.

```bash
git log                        # Historial completo
git log --oneline              # Solo hash corto + título del commit
git log -n 2                   # Solo los últimos N commits
git log --format=short         # Formato reducido (short / medium / full)
```

Ejemplo de salida de `git log`:

```
commit 06a3ab9a7694cd5db282ffa0ac2f55e82c7c5cbe (HEAD -> main, develop)
Author: manuCastrillonM <manu.cm43@gmail.com>
Date:   Sun Apr 2 03:26:51 2023 +0200

    agrego saludo desde rama develop
```

Ejemplo de `git log --oneline`:

```
06a3ab9 (HEAD -> main, develop) agrego saludo desde rama develop
a760f1b (origin/main) Update main.js
efbc9bc agrego saludo
6a3f139 Agrego saludo a mis amigos
```

| Opción | Qué muestra |
|--------|------------|
| `--oneline` | Hash corto + título del commit |
| `-n <número>` | Limita a los últimos N commits |
| `--format=short` | Hash + autor + título |
| `--format=medium` | Por defecto: hash + autor + fecha + título |
| `--format=full` | Hash + autor + committer + título |

---

### `git diff` — Ver diferencias

Muestra línea por línea qué cambió entre dos versiones de un archivo,
dos commits o dos ramas.

```bash
git diff                       # Cambios en working directory vs staging
git diff --staged              # Cambios en staging vs último commit
git diff <rama-a> <rama-b>     # Diferencias entre dos ramas
git diff <hash-a> <hash-b>     # Diferencias entre dos commits
```

Cómo leer la salida:

```diff
--- a/index.html    ← versión anterior (del repositorio)
+++ b/index.html    ← versión nueva (con tus cambios)
@@ -8,5 +8,6 @@    ← antes había 5 líneas desde la 8; ahora hay 6
    </head>
    <body>
      <h1>Hello world</h1>
+     <h2>Welcome to my page</h2>   ← línea añadida
    </body>
  </html>
```

| Símbolo | Significado |
|---------|-------------|
| `---` | Versión anterior del archivo |
| `+++` | Versión nueva del archivo |
| `@@` | Resumen de líneas afectadas |
| `+` | Línea añadida |
| `-` | Línea eliminada |

---

### `git stash` — Guardar cambios temporalmente

Funciona como una **cuarta área** fuera del historial de versiones. Guarda los
cambios del working directory y el staging area, y deja el proyecto limpio en
el último commit.

> 🍪 **Analogía:** ya empezaste a preparar la masa de galletas pero necesitas
> salir a comprar ingredientes. En lugar de tirar la masa, la guardas en el
> refrigerador. `git stash` hace exactamente eso con tu código.

**Caso de uso típico:** estás trabajando en una feature, el código aún no está
listo para un commit, y de repente hay un error en producción que debes
solucionar ya. Guardas tus cambios con `git stash`, arreglas el bug, y luego
los recuperas.

```
Área de stash  ←──  Área de trabajo  ──→  Staging  ──→  Repositorio
  cambio 3
  cambio 2
  cambio 1
```

```bash
git stash                          # Guarda cambios y limpia el working tree
git stash save "nombre descriptivo"# Guarda con nombre personalizado
git stash list                     # Lista todos los stashes guardados
git stash pop                      # Restaura el último stash (lo elimina de la lista)
git stash pop stash@{1}            # Restaura un stash específico por índice
git stash --include-untracked      # Incluye archivos nuevos (untracked)
```

Ejemplo de `git stash list`:

```
stash@{0}: WIP on main: 01f11fa add console log to test git rebase
stash@{1}: On main: test stash
```

> ⚠️ El stash funciona como una **pila (LIFO)**: el último en entrar es el
> primero en salir con `git stash pop`.

> ⚠️ Por defecto `git stash` **no incluye archivos recién creados**
> (untracked). Debes usar `git stash --include-untracked` para guardarlos.

---

### `git show` — Detalle de un commit

Muestra la información completa de un commit específico: metadatos y todos
los cambios de código que introdujo, en formato diff.

```bash
git show                   # Muestra el commit más reciente (HEAD)
git show <hash>            # Muestra un commit específico por su hash
```

Ejemplo de salida:

```
commit 06a3ab9a7694cd5db282ffa0ac2f55e82c7c5cbe (develop)
Author: manuCastrillonM <manu.cm43@gmail.com>
Date:   Sun Apr 2 03:26:51 2023 +0200

    agrego saludo desde rama develop

diff --git a/main.js b/main.js
--- a/main.js
+++ b/main.js
@@ -1,2 +1,3 @@
 console.log("hello world from main.js");
 console.log("hola desde el repositorio remoto");
+console.log("hola desde la rama develop");
```

> 💡 `git show` es útil cuando colaboras en equipo y quieres entender
> exactamente qué cambió en un commit puntual sin revisar todo el historial.
