## ⏳ Manipulando la historia de Git

> ⚠️ **Importante:** estos comandos reescriben el historial. Úsalos **solo en
> ramas en las que trabajas tú solo**. Nunca en ramas compartidas (`main`,
> `develop`) porque afecta el historial de los demás colaboradores.

---

### `git rebase` — Reubicar commits sobre otra base

Rebase toma los commits de tu rama y los **reaplica encima de otra rama**,
como si los hubieras creado desde ahí desde el principio. Sirve para dos cosas
principales: mantener tu rama actualizada con `main`, y limpiar el historial
comprimiendo varios commits en uno.

#### Uso 1 — Actualizar una rama con los cambios de `main`

```
Antes:                           Después:
main:    A → B → C               main:    A → B → C
                ↓                                  ↓
mi-rama:        D → E            mi-rama:          D' → E'
```

```bash
git switch mi-rama
git rebase main         # reaplica los commits de mi-rama sobre main
```

#### Uso 2 — Comprimir varios commits en uno (squash interactivo)

Útil para limpiar el historial antes de hacer merge: varios commits de trabajo
se convierten en uno solo bien descrito.

```bash
git rebase -i HEAD~3    # abre el editor con los últimos 3 commits
```

En el editor que se abre, cambia `pick` por `squash` (o `s`) en los commits
que quieres comprimir:

```
pick  a1b2c3 add login form
squash d4e5f6 fix typo in form
squash g7h8i9 fix validation bug
```

Después de guardar, Git te pedirá escribir el mensaje final del commit unificado.

| Opción | Acción |
|--------|--------|
| `pick` | Mantener el commit tal cual |
| `squash` / `s` | Comprimir con el commit anterior |
| `reword` / `r` | Mantener el commit pero editar el mensaje |
| `drop` / `d` | Eliminar el commit completamente |

---

### `git commit --amend` — Modificar el último commit

Permite corregir el **último commit** sin crear uno nuevo. Se usa cuando
olvidaste agregar un archivo, hay un error en el mensaje, o quieres incluir
un cambio pequeño que debería haber ido en ese commit.

#### Caso 1 — Solo corregir el mensaje

```bash
git commit --amend
# Se abre el editor con el mensaje actual — lo editas, guardas y cierras
# En Vim: editar → Esc → :wq → Enter
```

#### Caso 2 — Agregar archivos olvidados al último commit

```bash
# Tienes cambios en index.css que olvidaste incluir
git add index.css
git commit --amend
# El editor se abre con el mensaje anterior — lo puedes dejar igual o editar
```

El resultado es un único commit actualizado que incluye los cambios nuevos.
El hash SHA-1 cambia porque el contenido cambió.

> ⚠️ No uses `--amend` si ya hiciste `git push` de ese commit. Reescribir
> un commit ya publicado causa conflictos para los demás colaboradores.

---

### `git cherry-pick` — Traer un commit específico de otra rama

Copia un commit de cualquier rama y lo aplica en la rama actual, **sin
necesidad de hacer merge de toda la rama**. El commit se integra al historial
de tu rama con un nuevo hash.

```
Antes:                           Después:
otra-rama:  A → B → ◆            otra-rama:  A → B → ◆
main:       C → D                main:       C → D
mi-rama:    E → F                mi-rama:    E → F → ◆'
```

```bash
# 1. Obtener el hash del commit que quieres copiar
git log --oneline otra-rama

# 2. Posicionarte en la rama destino
git switch mi-rama

# 3. Aplicar el commit
git cherry-pick <hash-del-commit>
```

**Ejemplo real:**

```bash
git switch develop
git cherry-pick b0c0183     # copia el commit "change color title" a develop
```

El commit queda integrado en el historial de `develop` como si hubiera sido
creado ahí, y conserva el mensaje y los cambios originales.

> 💡 Útil cuando un fix crítico hecho en una rama feature también se necesita
> urgentemente en `main` o `develop`, sin esperar el merge completo.

---

### Resumen comparativo

| Comando | Para qué sirve | Reescribe historial |
|---------|---------------|---------------------|
| `git rebase <rama>` | Actualizar tu rama con los cambios de otra | ✅ Sí |
| `git rebase -i HEAD~N` | Limpiar / comprimir los últimos N commits | ✅ Sí |
| `git commit --amend` | Corregir el último commit (mensaje o archivos) | ✅ Sí |
| `git cherry-pick <hash>` | Copiar un commit específico a la rama actual | ❌ No |
