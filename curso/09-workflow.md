## 🔄 Git Workflow

Un Git Workflow es un **estándar de trabajo en equipo** que define cómo
se usan las ramas, los commits y los merges en un proyecto. El objetivo
es mejorar la productividad, mantener la calidad del código y responder
a incidencias de forma eficiente.

### ¿Qué define un workflow?

- Nombramiento de ramas y commits
- Cuándo y cómo crear ramas
- Cómo y cuándo hacer merge
- Cómo responder ante errores en producción

---

## 1. Feature Based

Cada desarrollador crea una **rama nueva por cada cambio o tarea**.
Al terminar, abre una **Pull Request (PR)** para que el equipo revise
el código antes de hacer merge a la rama principal.

```
main:     ──────────────────────────→
              ↑                  ↑
feature:      └── commit → commit ┘  (PR → code review → merge)
```

### Flujo de trabajo

```bash
git switch -c feat45-add-navbar     # crear rama para la tarea
# ... trabajar, hacer commits ...
git push origin feat45-add-navbar   # subir al remoto
# abrir Pull Request en GitHub → code review → merge
```

### ¿Qué es un code review?

Es la revisión del código por parte de los compañeros del equipo
**antes de integrarlo** a la rama principal. Permite detectar errores,
compartir conocimiento y mantener la calidad del código.

### Beneficios

- Mejora la calidad del código
- Fomenta la colaboración en equipo
- Aumenta el conocimiento compartido del proyecto
- Ahorra tiempo al detectar errores antes del merge

---

## 2. GitFlow

Diseñado para proyectos **grandes y complejos** con ciclos de release
definidos. Es el más usado en empresas con múltiples versiones en
producción simultáneamente.

### Ramas principales

| Rama | Propósito |
|------|-----------|
| `main` | Código en producción — siempre estable |
| `develop` | Integración continua — base de todo el desarrollo |
| `feature/*` | Nuevas funcionalidades — parten de `develop` |
| `release/*` | Preparación de una versión para producción |
| `hotfix/*` | Correcciones urgentes directamente en `main` |

### Diagrama de ramas

```
main:      ●────────────────────────●────────●
           ↑                        ↑        ↑
develop:   ●──●──●──●──●──●──●──●──●        |
                  ↑        ↓                 |
feature:          ●──●──●──┘                 |
                              ↑              |
release:                      ●──●───────────┘
                                    ↓
hotfix:                       (error en producción)
                              main → hotfix → main + develop
```

### Cuándo usar cada rama

```bash
# Nueva funcionalidad
git switch -c feature/add-login develop

# Preparar release
git switch -c release/1.2.0 develop

# Error urgente en producción
git switch -c hotfix/fix-payment-crash main
```

### Ventajas e inconvenientes

| ✅ Ventajas | ⚠️ Inconvenientes |
|------------|------------------|
| Muy estructurado | Muchas ramas = complejidad alta |
| Ideal para versiones múltiples | Llegar a `main` es lento |
| Separa bien producción y desarrollo | No apto para CI/CD ágil |

---

## 3. Trunk Based Development

El flujo en auge gracias a la **entrega continua (CI/CD)**. Todos los
desarrolladores trabajan sobre una única rama principal (`main` o `trunk`)
con ramas de **muy corta vida** (horas o días, no semanas).

Los cambios se integran frecuentemente y solo pasan a `main` si superan
los **tests automatizados**.

```
main:   ●──●──────────●──────────●──●──→
            ↑        ↓    ↑     ↓
short:      ●──●──●──┘    ●──●──┘
           (rama de 1-2 días máximo)
```

### Flujo de trabajo

```bash
git switch -c short-lived-feature   # rama corta
# ... pocos commits, cambio pequeño ...
git push origin short-lived-feature
# tests automáticos → merge rápido a main → despliegue
```

### Ventajas e inconvenientes

| ✅ Ventajas | ⚠️ Inconvenientes |
|------------|------------------|
| Simplicidad — pocas ramas | Mayor riesgo de introducir fallas |
| Entrega rápida y continua | Requiere tests automatizados sólidos |
| Menor complejidad de merges | No apto para equipos sin disciplina de testing |
| Mayor visibilidad del estado del proyecto | Difícil gestionar múltiples versiones |

---

## Comparativa de los tres workflows

| | Feature Based | GitFlow | Trunk Based |
|---|:---:|:---:|:---:|
| **Tamaño de equipo** | Cualquiera | Grande | Pequeño / mediano |
| **Complejidad** | Media | Alta | Baja |
| **Velocidad de entrega** | Media | Lenta | Rápida |
| **CI/CD compatible** | Parcial | ❌ Difícil | ✅ Ideal |
| **Code review** | ✅ Sí | ✅ Sí | Opcional |
| **Gestión de versiones** | Básica | ✅ Avanzada | Limitada |
| **Ideal para** | La mayoría de proyectos | Apps con releases formales | Startups, proyectos ágiles |
