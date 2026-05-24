# Laboratorio 1 — Comandos Básicos de Linux

🔗 [Linux basic commands](https://kodekloud.com/studio/labs/linux/) · Duración máxima: 1 hora

---

## Navegación y archivos básicos

| Comando | Descripción |
|---|---|
| `pwd` / `echo $HOME` | Muestra el directorio actual |
| `ls` | Lista archivos y directorios en el directorio actual |
| `mkdir <nombre>` | Crea un nuevo directorio |
| `touch <nombre>` | Crea un archivo vacío con el nombre indicado |
| `rm <archivo>` | Elimina un archivo |

> **Nota:** `git` representa un ejecutable; en algunos contextos también se le llama *file*.

---

## Directorios: crear y eliminar

| Comando | Descripción |
|---|---|
| `mkdir -p <ruta>` | Crea directorios de forma recursiva (crea padres si no existen) |
| `rm -r <directorio>` | Elimina un directorio y todo su contenido |

**Ejemplo — crear varios directorios a la vez:**

```bash
mkdir -p ~/mammals/{elephant,monkey}
```

Crea los directorios `elephant` y `monkey` dentro de `~/mammals`. Si `mammals` no existe, también lo crea.

---

## Mover archivos

```bash
mv ~/reptile/frog ~/amphibian/
```

Mueve el archivo `frog` desde `~/reptile/` hacia `~/amphibian/`.

---

## Renombrar archivos

```bash
mv <nombre_actual> <nombre_nuevo>
```

`mv` también sirve para renombrar: si el destino es un nombre de archivo (no un directorio existente), el archivo queda renombrado.

**Ejemplo:**

```bash
mv ~/documents/reporte_v1.txt ~/documents/reporte_final.txt
```
