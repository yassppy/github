## 🌲 Ramas (Branches)

Una rama es como escribir ideas alternativas de un libro: puedes desarrollar
contenido en paralelo y luego fusionarlo con el texto principal cuando esté listo.

Cada rama es un flujo de trabajo independiente que parte desde la rama actual
y hereda todos sus commits.

---

### ¿Por qué usar ramas?

- Trabajar de forma segura y organizada
- Aislar los cambios por funcionalidad
- Experimentar sin comprometer el código principal
- Trabajar en diferentes funcionalidades simultáneamente
- Facilitar el trabajo en equipo

> 💡 Crea una rama nueva **cada vez que vayas a realizar un cambio**: agregar,
> arreglar, eliminar o modificar algo en el proyecto.

---

### Nombramiento de ramas

El nombre debe ser **descriptivo**, permitir identificar el ticket o tarea
asociada y seguir el estándar definido por tu equipo.

| ✅ Correcto | ❌ Incorrecto |
|------------|--------------|
| `feat45-add-navbar` | `addNew-feature` |
| `fix-contact-cta` | `fix-button` |
| `test-color-rebrand` | `myBranch` |
| `56-update-user-db-model` | `other-branch` |

**Patrón recomendado:** `<tipo>-<descripción-corta>` o `<número-ticket>-<descripción>`

---

### Comandos de ramas

```bash
git branch                    # Lista todas las ramas del repositorio
git branch <nombre-rama>      # Crea una nueva rama desde la rama actual
git branch -d <nombre-rama>   # Elimina una rama (debes estar en otra rama)
git branch -D <nombre-rama>   # Elimina una rama forzosamente (sin merge previo)
```

---

### Navegar entre ramas

`git switch` cambia tu área de trabajo a la rama indicada.
Desde Git 2.23 reemplaza al antiguo `git checkout` para cambiar ramas.

```bash
git switch <nombre-rama>      # Cambia a una rama existente
git switch -c <nombre-rama>   # Crea una nueva rama y cambia a ella a la vez
```

| Acción | Versión antigua | Versión nueva (Git 2.23+) |
|--------|----------------|--------------------------|
| Cambiar de rama | `git checkout <rama>` | `git switch <rama>` |
| Crear y cambiar | `git checkout -b <rama>` | `git switch -c <rama>` |

---

### Unir ramas — `git merge`

Una vez terminados los cambios en una rama, se integran a la rama destino
(normalmente `main`) mediante un merge.

**Pasos:**

```bash
# 1. Posicionarse en la rama que va a RECIBIR los cambios
git switch main

# 2. Fusionar la rama con los nuevos cambios
git merge <nombre-rama>
```

> ⚠️ Siempre debes estar en la rama **destino** antes de ejecutar `git merge`,
> no en la rama que quieres fusionar.

---

### Estrategias de merge

Git elige la estrategia automáticamente según el historial, pero conviene
entender qué hace cada una.

#### 1. Fast-forward merge

Ocurre cuando la rama destino **no tiene commits nuevos** desde que se creó
la rama. Git simplemente mueve el puntero hacia adelante, sin crear un commit
extra. El historial queda lineal.

```
Antes:                          Después:
main:    A → B → C              main:    A → B → C → D → E
                ↓
develop:        D → E
```

#### 2. Merge commit

Ocurre cuando **ambas ramas tienen commits nuevos** desde que se bifurcaron.
Git crea un commit de fusión que une los dos historiales. Conserva la trazabilidad
completa de cada rama.

```
Antes:                          Después:
main:    A → B → C              main:    A → B → C ──────→ M
                ↓                                           ↑
develop:        D → E           develop:         D → E ───/
```

`M` es el merge commit que une ambas líneas.

#### 3. Squash merge

Comprime **todos los commits de la rama** en uno solo antes de fusionar.
El historial de `main` queda limpio y lineal. Los commits individuales de la
rama desaparecen del historial principal.

```
Antes:                          Después:
main:    A → B → C → D          main:    A → B → C → D → [D+E comprimidos]
                    ↓
develop:            E1 → E2
```

| Estrategia | Historial | Cuándo usarla |
|------------|-----------|---------------|
| Fast-forward | Lineal, sin commit extra | Ramas simples sin divergencia |
| Merge commit | Conserva ambas ramas | Trabajo en equipo, trazabilidad |
| Squash merge | Limpio, un solo commit | Features con muchos commits de trabajo |

> 💡 La estrategia depende del flujo de trabajo de tu equipo. No hay una
> universalmente correcta.
```
