# Conventional Commits — Guía práctica

> Referencia oficial: https://www.conventionalcommits.org/es/v1.0.0/

---

## ¿Por qué Conventional Commits?

- Historial de git legible y semántico
- Generación automática de CHANGELOG
- Dispara releases semánticos (semver) de forma automática
- Facilita la revisión de PRs y el trabajo en equipo

---

## Estructura del mensaje

```
<type>(<scope>): <descripción corta en inglés>

[cuerpo opcional — explica el QUÉ y el POR QUÉ]

[footer opcional — Breaking Changes, Refs, Closes #issue]
```

### Reglas básicas

- La descripción va en **inglés**, en **imperativo** y en **minúsculas**
- Sin punto al final de la descripción corta
- Máximo ~72 caracteres en la primera línea
- El `scope` es opcional pero muy recomendado

---

## Tipos de commit

| Tipo | Cuándo usarlo |
|------|--------------|
| `feat` | Nueva funcionalidad visible para el usuario |
| `fix` | Corrección de bug |
| `docs` | Solo cambios en documentación |
| `style` | Formato, espaciado, puntos y comas — sin cambio de lógica |
| `refactor` | Reestructuración de código sin cambio de comportamiento |
| `test` | Añadir o corregir tests |
| `chore` | Tareas de mantenimiento, dependencias, build, CI |
| `perf` | Mejora de rendimiento |
| `ci` | Cambios en pipelines de CI/CD |
| `revert` | Revierte un commit anterior |
| `spike` | Investigación o prototipo desechable |
| `data` | Migraciones, seeds, esquemas de base de datos |
| `model` | Definición/cambio de modelos ML, arquitectura de red |
| `exp` | Experimento reproducible (ML/LangChain) |

---

## Scopes comunes por dominio

| Scope | Dominio | Cuándo usarlo |
|-------|---------|---------------|
| `(home)` | Web | Página principal |
| `(auth)` | Web / API | Login, registro, sesión, tokens |
| `(navbar)` | Web | Barra de navegación |
| `(api)` | Backend | Endpoints REST |
| `(ui)` | Web | Componentes genéricos reutilizables |
| `(deps)` | Cualquiera | Actualización de dependencias |
| `(db)` | Backend / DB | Migraciones, esquemas, seeds |
| `(schema)` | Backend / DB | Cambios en el modelo de datos |
| `(graph)` | LangGraph | Nodos, edges, estado del grafo |
| `(chain)` | LangChain | Cadenas, prompts, retrievers |
| `(agent)` | LangGraph / ML | Agentes y herramientas |
| `(pipeline)` | ML | Preprocessing, training, evaluación |
| `(model)` | ML | Arquitectura, pesos, configuración |
| `(config)` | Cualquiera | Archivos de configuración |
| `(readme)` | Docs | README y guías de inicio |
| `(notebook)` | ML / Docs | Jupyter notebooks |
| `(ci)` | DevOps | GitHub Actions, pipelines |
| `(docker)` | DevOps | Dockerfile, compose |

---

## 🚀 Setup inicial del proyecto

```bash
# Un solo commit para el init mínimo
chore: initial project setup

# O desglosado si hay mucha configuración
chore: init project with Next.js and Tailwind CSS
chore: set up folder structure (components, pages, hooks)
chore: add ESLint and Prettier config
chore: configure absolute imports with tsconfig paths
chore: add .env.example with required variables
```

---

## 🌐 Desarrollo Web — Next.js / React

```bash
# Features
feat(home): add hero section with CTA button
feat(home): add scroll animations to hero section
feat(auth): implement login form with validation
feat(auth): add Google OAuth provider
feat(navbar): add responsive mobile menu
feat(ui): create reusable Button component with variants

# Fixes
fix(home): correct hero image overflow on mobile screens
fix(navbar): broken link to contact section
fix(auth): form not submitting when email has uppercase letters
fix(ui): Button component missing disabled state styles

# Styles
style(home): adjust hero font size and line height for desktop
style: format all files with Prettier

# Refactor
refactor(home): extract HeroSection into its own component
refactor(auth): simplify token refresh logic
refactor(ui): consolidate modal components into single abstraction
```

---

## 🔌 REST API — Backend

```bash
# Features
feat(api): add POST /users endpoint with email validation
feat(api): implement JWT authentication middleware
feat(auth): add refresh token rotation
feat(api): add pagination to GET /products endpoint
feat(api): add rate limiting to public endpoints

# Fixes
fix(api): return 404 instead of 500 on missing resource
fix(auth): token not invalidated on logout
fix(api): incorrect HTTP status on validation errors

# Refactor
refactor(api): extract error handler to shared middleware
refactor(api): move business logic from controllers to services

# Tests
test(api): add integration tests for login endpoint
test(api): add unit tests for JWT middleware
test(api): add e2e tests for user registration flow
```

---

## 🗄️ Base de datos

```bash
# Migraciones
data(db): add users table with email and password fields
data(db): add index on users.email for faster lookups
data(db): add created_at and updated_at to orders table

# Cambios de esquema
refactor(schema): rename user_id to author_id in posts table
feat(schema): add soft delete support with deleted_at column

# Seeds
chore(db): add seed data for development environment
chore(db): add fixtures for integration tests
```

---

## 🦜 LangChain / LangGraph

```bash
# Grafo y agentes
feat(graph): add supervisor node for multi-agent routing
feat(graph): define initial state schema with TypedDict
feat(agent): add web search tool with Tavily integration
feat(agent): implement ReAct loop for task decomposition
feat(chain): add RAG chain with FAISS retriever

# Prompts
feat(chain): add system prompt template for customer support agent
refactor(chain): move prompts to dedicated prompt registry module
fix(chain): correct prompt template variable interpolation

# Estado y memoria
feat(graph): add persistent memory with MemorySaver checkpointer
feat(graph): implement human-in-the-loop interrupt on approval node
refactor(graph): simplify conditional edge routing logic

# Experimentos / Spikes
spike: evaluate LangSmith tracing for production observability
exp(graph): test streaming tokens with async generator pattern
```

---

## 🤖 Machine Learning

```bash
# Pipeline
feat(pipeline): add data preprocessing with standardization
feat(pipeline): add train/val/test split with stratification
feat(pipeline): add feature engineering for categorical variables
refactor(pipeline): extract preprocessing into sklearn Pipeline object

# Modelos
feat(model): implement LSTM for time series forecasting
feat(model): add dropout layers to reduce overfitting
perf(model): optimize batch size and learning rate schedule
fix(model): correct label encoding causing data leakage

# Experimentos
exp(model): test XGBoost vs Random Forest on validation set
exp(pipeline): evaluate SMOTE for class imbalance handling
chore(notebook): clean and document EDA notebook

# Evaluación
feat(pipeline): add classification report and confusion matrix logging
feat(pipeline): add MLflow experiment tracking
```

---

## 📝 Documentación

```bash
docs: update README with local setup instructions
docs(api): document authentication endpoints with OpenAPI
docs(home): add JSDoc comments to HeroSection component
docs(graph): add architecture diagram for multi-agent system
docs(model): document hyperparameter tuning decisions
docs(readme): add badges for CI status and coverage
docs(notebook): add markdown explanations to EDA notebook
```

---

## ⚙️ Configuración y CI/CD

```bash
chore: add ESLint config for the project
chore: update Tailwind CSS to v4
chore(deps): bump axios from 1.6.0 to 1.7.2
chore(docker): add Dockerfile for production build
chore(docker): add docker-compose for local dev with PostgreSQL
ci: add GitHub Actions workflow for linting and tests
ci: add deployment workflow to Vercel on main branch merge
ci: add coverage report upload to Codecov
```

---

## 🐛 Corrección de bugs

```bash
fix(home): correct hero image overflow on mobile screens
fix(api): unhandled promise rejection in async route handler
fix(graph): agent stuck in infinite loop on ambiguous input
fix(model): NaN loss caused by missing value imputation order
fix(db): migration rollback not reverting index creation
```

---

## ♻️ Refactor

```bash
refactor(home): extract HeroSection into its own component
refactor(home): simplify banner animation logic
refactor(api): move validation schemas to dedicated validators module
refactor(graph): rename nodes for clarity (router → supervisor)
refactor(pipeline): replace manual loops with vectorized operations
```

---

## 🧪 Tests

```bash
test(home): add unit tests for HeroSection render
test(api): add integration tests for login endpoint
test(graph): add unit tests for supervisor routing logic
test(model): add regression tests for preprocessing output shape
test(api): add snapshot tests for error response format
```

---

## 💥 Breaking Change

Un breaking change se marca con `!` después del tipo/scope, y se documenta en el footer con `BREAKING CHANGE:`.

```bash
feat(auth)!: replace JWT with session-based authentication

BREAKING CHANGE: clients must now use cookies instead of the
Authorization header. Remove the `Authorization: Bearer <token>`
header from all API requests and enable credentials on fetch/axios.

Closes #142
```

```bash
refactor(api)!: rename /users/:id to /users/:userId

BREAKING CHANGE: all routes using :id param for users must be
updated to :userId. Update any client-side API calls accordingly.
```

---

## 🔁 Revert

```bash
revert: feat(home): add hero section with CTA button

Refs: a3f5c21
Reason: caused layout regression on Safari 16, reverted until fixed
```

---

## 📚 Apuntes y notas personales

```bash
docs(notes): add notes on React Server Components patterns
docs(notes): add summary of LangGraph multi-agent architecture
docs(notes): add cheatsheet for PostgreSQL window functions
chore(notebook): add exploratory notebook for transformer fine-tuning
spike: research vector database options (Pinecone vs Chroma vs Weaviate)
```

---

## 💡 Consejos de uso con IA

Cuando uses una IA para sugerir commits, incluye este prompt:

```
You are a conventional commits assistant. Given the following git diff or
description of changes, suggest one or more commits following the
Conventional Commits specification (https://www.conventionalcommits.org).

Rules:
- Use English for the commit message
- Use imperative mood ("add", "fix", "update" — not "added" or "fixes")
- Lowercase type and description
- No period at the end
- Include a scope when relevant (e.g., feat(auth), fix(api))
- Group related changes into a single commit when appropriate
- Split into multiple commits when changes are logically independent
- Use BREAKING CHANGE footer when needed
- Available types: feat, fix, docs, style, refactor, test, chore, perf, ci, revert, spike, data, model, exp

Context about this project: [describe your project here]

Changes to commit:
[paste your diff or describe your changes]
```

---

## Agrupación vs. commits individuales

| Situación | Recomendación |
|-----------|--------------|
| Varios archivos del mismo componente | Un solo commit con scope |
| Feature + sus tests | Se puede agrupar: `feat(auth): add login with tests` |
| Feature + documentación | Separar: `feat` luego `docs` |
| Refactor + fix en el mismo módulo | Separar siempre — distintos tipos |
| Múltiples dependencias actualizadas | Un solo `chore(deps): bump X, Y, Z` |
| Migración + seed relacionados | Se puede agrupar bajo `data(db)` |
| Cambios de estilo + lógica | **Siempre separar** — `style` no debe tocar lógica |
