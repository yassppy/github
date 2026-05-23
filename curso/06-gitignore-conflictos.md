````markdown
## ⚔️ Conflictos en Git

Un conflicto ocurre cuando Git intenta fusionar dos ramas y **no puede decidir
automáticamente** qué versión del código conservar. Esto pasa cuando dos o más
personas modificaron las mismas líneas del mismo archivo en ramas distintas.

> Git fusiona automáticamente cuando los cambios están en líneas diferentes.
> El conflicto solo aparece cuando hay **colisión en la misma línea**.

**Ejemplo:**

```
main:    <h1>Hello Dog</h1>    ← cambio en main
develop: <h1>Hello Cat</h1>    ← cambio en develop
                    ↓
             💥 Conflicto: ¿cuál se queda?
```

---

### Cómo se ve un conflicto en el archivo

Al ejecutar `git merge <rama>` con conflicto, Git modifica el archivo
afectado e inserta marcadores para señalar las dos versiones:

```html
<<<<<<< HEAD (Current Change)
  <h1>Hello family</h1>       ← versión de la rama actual (main)
=======
  <h1>Hello friends</h1>      ← versión de la rama entrante (develop)
>>>>>>> conflict-test (Incoming Change)
```

| Marcador | Significado |
|----------|-------------|
| `<<<<<<< HEAD` | Inicio de los cambios de la rama actual |
| `=======` | Separador entre las dos versiones |
| `>>>>>>> <rama>` | Fin de los cambios de la rama entrante |

---

### Estrategias para resolver un conflicto

#### Estrategia 1 — Edición manual

La más flexible. Abres el archivo, eliminas los marcadores de Git y dejas
exactamente el código que quieres conservar (puede ser uno, el otro, o una
combinación de ambos).

```bash
# 1. Editar el archivo y eliminar los marcadores <<<, ===, >>>
# 2. Guardar el archivo
# 3. Marcar como resuelto y confirmar

git add index.html
git commit           # Git abre el editor con el mensaje de merge pre-rellenado
                     # Guardar y cerrar con :wq en Vim, o cerrar la pestaña en VS Code
```

> El commit de merge se genera automáticamente con la última versión de la
> rama destino como base.

---

#### Estrategia 2 — `--ours` / `--theirs`

Cuando quieres quedarte completamente con una de las dos versiones sin
mezclar, sin editar el archivo manualmente.

```bash
# Conservar la versión de la rama actual (main)
git checkout --ours index.html

# Conservar la versión de la rama entrante (develop / conflict-test)
git checkout --theirs index.html

# Después de elegir, agregar y hacer commit
git add index.html
git commit
```

| Opción | Versión que conserva |
|--------|---------------------|
| `--ours` | La rama **destino** (en la que estás parado) |
| `--theirs` | La rama **entrante** (la que estás fusionando) |

---

#### Estrategia 3 — Editor de texto (VS Code)

VS Code detecta los conflictos automáticamente y muestra botones encima
de cada bloque para resolverlos sin editar manualmente los marcadores.

| Opción en VS Code | Qué hace |
|-------------------|----------|
| `Accept Current Change` | Se queda con la versión de `HEAD` (rama actual) |
| `Accept Incoming Change` | Se queda con la versión de la rama entrante |
| `Accept Both Changes` | Mantiene ambas versiones una debajo de la otra |
| `Compare Changes` | Abre una vista diff lado a lado |

Después de resolver en el editor:

```bash
git add index.html
git commit
```

---

### Flujo completo de resolución

```
1. git merge <rama>           ← Git detecta el conflicto y pausa el merge
2. Abrir el archivo afectado
3. Elegir una estrategia y resolver
4. git add <archivo>          ← marcar como resuelto
5. git commit                 ← finalizar el merge commit
```

---

### ✅ Buenas prácticas para evitar conflictos

- Realiza commits **pequeños y frecuentes**
- Escribe mensajes de commit **descriptivos**
- Actualiza constantemente tu repositorio local con `git pull`
- Trabaja siempre en **ramas propias**, nunca directamente en `main`

---

## 🙈 .gitignore

El archivo `.gitignore` lista todos los archivos y carpetas que Git debe
**ignorar completamente**: no los rastreará, no aparecerán en `git status`
y no se subirán al repositorio remoto.

### ¿Por qué ignorar archivos?

- Archivos `.env` con credenciales, claves API y datos sensibles
- Carpetas de librerías instaladas (`node_modules/`, `venv/`)
- Archivos compilados o generados automáticamente (`dist/`, `build/`)
- Logs y archivos temporales

### Sintaxis del `.gitignore`

```gitignore
# Comentario — esta línea se ignora

# Archivos específicos
.env
npm-debug.log
yarn-error.log

# Carpetas completas (con la barra al final)
node_modules/
dist/
build/

# Todos los archivos de una extensión
*.zip
*.log

# Todos los archivos de un tipo dentro de una carpeta
carpetasecreta/*.js

# Excepciones — NO ignorar este archivo aunque coincida con una regla
!importante.log
```

### Ejemplo real para un proyecto Node.js / Next.js

```gitignore
# Dependencias
node_modules/

# Build
dist/
.next/
out/

# Variables de entorno
.env
.env.local
.env.production

# Logs
npm-debug.log
yarn-error.log

# Sistema operativo
.DS_Store
Thumbs.db

# Editor
.vscode/
.idea/
```

> 💡 Puedes generar un `.gitignore` completo para tu stack en
> [gitignore.io](https://www.toptal.com/developers/gitignore)

> ⚠️ Si ya subiste un archivo al repositorio antes de agregarlo al
> `.gitignore`, Git seguirá rastreándolo. Para dejar de hacerlo:
> ```bash
> git rm --cached <archivo>   # elimina del tracking sin borrar el archivo local
> git commit -m "chore: remove tracked file now in .gitignore"
> ```
````
