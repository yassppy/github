## ↩️ Deshaciendo cambios

---

### `git checkout` — Descartar cambios del working directory

Restaura un archivo a su última versión confirmada (el último commit).
Los cambios que no fueron al staging **se pierden de forma permanente**.

```bash
git checkout <archivo>    # descarta cambios de un archivo específico
git checkout .            # descarta todos los cambios del proyecto
```

> ⚠️ No hay forma de recuperar los cambios descartados con `checkout`.
> Úsalo solo cuando estés seguro de que no necesitas esos cambios.

---

### `git revert` — Deshacer un commit de forma segura ✅

Es la opción más recomendada para ramas compartidas. En lugar de
modificar el historial, **crea un nuevo commit** que invierte exactamente
los cambios del commit que quieres deshacer. El commit original sigue
existiendo en el historial.

```bash
git log --oneline              # identifica el hash del commit a revertir
git revert <hash-del-commit>   # Git abre el editor con el mensaje pre-rellenado
                               # Guardar y cerrar (:wq en Vim) para confirmar
```

```
Historial antes:    A → B → C (change color)
Historial después:  A → B → C (change color) → D (Revert "change color")
```

| Ventaja | Por qué importa |
|---------|----------------|
| No modifica el historial | No causa conflictos al hacer push |
| El commit original queda | Puedes ver qué pasó y cuándo |
| Seguro en ramas compartidas | Otros colaboradores no se ven afectados |

---

### `git reset` — Retroceder el historial

Mueve el puntero `HEAD` a un commit anterior, deshaciendo los commits
que quedaron por encima. Tiene tres modos según qué hace con los cambios
de esos commits.

> ⚠️ Úsalo solo en **ramas en las que trabajas tú solo**. En ramas
> compartidas causa conflictos al hacer push porque reescribe el historial.

#### Modos de `git reset`

```bash
git reset --soft HEAD~1    # deshace el commit, conserva cambios en staging
git reset HEAD~1           # deshace el commit, conserva cambios en working directory (por defecto: --mixed)
git reset --hard HEAD~1    # deshace el commit y BORRA los cambios permanentemente
```

| Modo | Deshace el commit | ¿Dónde quedan los cambios? |
|------|:-----------------:|---------------------------|
| `--soft` | ✅ | En el **staging area** (listos para volver a confirmar) |
| `--mixed` | ✅ | En el **working directory** (modificados pero sin staging) |
| `--hard` | ✅ | **Se eliminan** — no hay forma de recuperarlos |

**Ejemplos:**

```bash
# Retroceder 1 commit pero conservar los cambios en staging
git reset --soft HEAD~1

# Retroceder al commit con hash 73d9573 (modo mixed por defecto)
git reset 73d9573

# Retroceder 1 commit y eliminar todos los cambios (peligroso)
git reset --hard HEAD~1
```

> 💡 `HEAD~1` significa "un commit antes del actual". `HEAD~3` serían
> tres commits atrás. También puedes usar directamente el hash de un commit.

---

### Comparativa general: ¿cuándo usar cada uno?

| Comando | Modifica historial | Seguro en ramas compartidas | Cuándo usarlo |
|---------|:-----------------:|:---------------------------:|---------------|
| `git checkout <archivo>` | ❌ | ✅ | Descartar cambios no guardados de un archivo |
| `git revert <hash>` | ❌ | ✅ | Deshacer un commit ya publicado |
| `git reset --soft` | ✅ | ❌ | Rehacer el último commit con más cambios |
| `git reset --mixed` | ✅ | ❌ | Volver a editar los cambios antes de commitear |
| `git reset --hard` | ✅ | ❌ | Descartar todo y volver a un estado anterior |
