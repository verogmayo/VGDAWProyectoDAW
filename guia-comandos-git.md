# Guía Completa de Comandos Git

## Índice

1. [Comandos Básicos](#comandos-básicos)
2. [Gestión de Ramas](#gestión-de-ramas)
3. [Integración de Cambios](#integración-de-cambios)
4. [Comandos de Historial](#comandos-de-historial)
5. [Comandos de Sincronización](#comandos-de-sincronización)
6. [Comandos Avanzados](#comandos-avanzados)
7. [GitHub vs Git](#github-vs-git)
8. [Flujos de Trabajo Comunes](#flujos-de-trabajo-comunes)

---

## 

### 









### `git log`

Muestra el historial de commits del repositorio.

**Sintaxis básica:**
```bash
git log
```

**Opciones útiles:**
```bash
# Formato compacto (una línea por commit)
git log --oneline

# Mostrar los últimos N commits
git log -n 5

# Ver historial con gráfico de ramas
git log --graph --oneline --all

# Ver cambios de cada commit
git log -p

# Ver estadísticas de cada commit
git log --stat

# Filtrar por autor
git log --author="Juan"

# Filtrar por fecha
git log --since="2 weeks ago"
git log --after="2024-01-01" --before="2024-12-31"

# Buscar en mensajes de commit
git log --grep="bug fix"

# Ver commits que afectaron un archivo específico
git log -- ruta/archivo.js
```

**Ejemplo de salida:**
```bash
commit a1b2c3d4e5f6g7h8i9j0 (HEAD -> main, origin/main)
Author: Juan Pérez <juan@email.com>
Date:   Mon Feb 10 14:30:00 2025 +0100

    Fix: Corregir error en login

commit b2c3d4e5f6g7h8i9j0k1
Author: María García <maria@email.com>
Date:   Sun Feb 09 10:15:00 2025 +0100

    Feature: Añadir página de contacto
```

**Formato personalizado:**
```bash
# Formato bonito y detallado
git log --pretty=format:"%h - %an, %ar : %s" --graph

# Explicación del formato:
# %h  = hash corto del commit
# %an = nombre del autor
# %ar = fecha relativa
# %s  = mensaje del commit
```

---

## Gestión de Ramas

### Conceptos Básicos de Ramas

Una **rama** es una línea independiente de desarrollo. Te permite trabajar en nuevas características sin afectar el código principal.

```
main     A---B---C---F---G
              \         /
feature        D---E---
```

### Crear y cambiar de rama

```bash
# Crear nueva rama
git branch nombre-rama

# Cambiar a una rama
git checkout nombre-rama

# Crear y cambiar en un solo comando (recomendado)
git checkout -b nombre-rama

# Forma moderna (Git 2.23+)
git switch nombre-rama
git switch -c nombre-rama  # crear y cambiar
```

### Ver ramas

```bash
# Listar ramas locales
git branch

# Listar todas las ramas (locales y remotas)
git branch -a

# Ver última commit de cada rama
git branch -v

# Ver ramas fusionadas/no fusionadas
git branch --merged
git branch --no-merged
```

### Eliminar ramas

```bash
# Eliminar rama local (solo si está fusionada)
git branch -d nombre-rama

# Forzar eliminación (aunque no esté fusionada)
git branch -D nombre-rama

# Eliminar rama remota
git push origin --delete nombre-rama
```

---

## Integración de Cambios

### `git merge`

Fusiona cambios de una rama en otra, creando un **commit de merge**.

**Cómo funciona:**
```
Antes:
main     A---B---C
              \
feature        D---E

Después de: git merge feature (estando en main)
main     A---B---C-------F (merge commit)
              \         /
feature        D---E---
```

**Sintaxis:**
```bash
# Estar en la rama destino
git checkout main

# Fusionar otra rama
git merge feature

# Merge sin fast-forward (siempre crea commit de merge)
git merge --no-ff feature

# Merge solo si puede hacer fast-forward
git merge --ff-only feature
```

**Tipos de merge:**

1. **Fast-forward**: Cuando no hay commits divergentes
```
main     A---B
              \
feature        C---D

Después:
main     A---B---C---D
```

2. **Three-way merge**: Cuando hay commits en ambas ramas
```
main     A---B---C
              \
feature        D---E

Después (crea commit de merge):
main     A---B---C-------F
              \         /
feature        D---E---
```

**Resolver conflictos:**
```bash
# Si hay conflictos, Git te lo indicará
git merge feature
# Auto-merging archivo.js
# CONFLICT (content): Merge conflict in archivo.js

# Editar archivos con conflictos (verás marcadores como <<<<<<, ======, >>>>>>)
# Después de resolver:
git add archivo.js
git commit  # finaliza el merge
```

**Cuándo usar:**
- Para integrar features completadas
- Cuando quieres preservar el historial completo
- En flujos de trabajo tipo GitHub Flow

---

### `git rebase`

Reescribe el historial moviendo commits a una nueva base. Crea un historial **lineal**.

**Cómo funciona:**
```
Antes:
main     A---B---C
              \
feature        D---E

Después de: git rebase main (estando en feature)
main     A---B---C
                  \
feature            D'---E'
```

**Sintaxis:**
```bash
# Estar en la rama que quieres mover
git checkout feature

# Rebase sobre otra rama
git rebase main

# Rebase interactivo (para editar commits)
git rebase -i HEAD~3  # últimos 3 commits

# Continuar después de resolver conflictos
git rebase --continue

# Abortar rebase
git rebase --abort

# Saltar commit conflictivo
git rebase --skip
```

**Rebase Interactivo:**
```bash
git rebase -i HEAD~3

# Se abre un editor con:
pick a1b2c3d Commit 1
pick b2c3d4e Commit 2
pick c3d4e5f Commit 3

# Opciones disponibles:
# pick   = usar commit
# reword = usar commit pero editar mensaje
# edit   = usar commit pero pausar para modificar
# squash = fusionar con commit anterior
# fixup  = como squash pero descartar mensaje
# drop   = eliminar commit
```

**Cuándo usar:**
- Para mantener un historial limpio y lineal
- Antes de hacer merge de tu feature
- Para limpiar commits locales antes de push

**⚠️ NUNCA hagas rebase de commits públicos** (ya pusheados y compartidos)

**Merge vs Rebase:**

| Aspecto | Merge | Rebase |
|---------|-------|--------|
| Historial | Preserva todo | Reescribe |
| Conflictos | Una sola vez | Posible por commit |
| Claridad | Muestra bifurcaciones | Lineal y limpio |
| Seguridad | Más seguro | Peligroso si es público |
| Uso | Features públicas | Limpieza local |

---

### `git cherry-pick`

Aplica cambios de commits específicos a la rama actual.

**Cómo funciona:**
```
main     A---B---C
              \
feature        D---E---F

# Quiero solo el commit E en main
git checkout main
git cherry-pick <hash-de-E>

main     A---B---C---E'
              \
feature        D---E---F
```

**Sintaxis:**
```bash
# Aplicar un commit específico
git cherry-pick a1b2c3d

# Aplicar múltiples commits
git cherry-pick a1b2c3d b2c3d4e c3d4e5f

# Aplicar rango de commits
git cherry-pick main~3..main~1

# Cherry-pick sin hacer commit automáticamente
git cherry-pick -n a1b2c3d

# Continuar después de resolver conflictos
git cherry-pick --continue

# Abortar
git cherry-pick --abort
```

**Cuándo usar:**
- Aplicar un hotfix a múltiples ramas
- Recuperar un commit de una rama eliminada
- Copiar commits específicos sin todo el historial

**Ejemplo práctico:**
```bash
# Tienes un bugfix en develop que necesitas en main
git log develop --oneline
# a1b2c3d Fix: Corregir error crítico

git checkout main
git cherry-pick a1b2c3d
```

---

## Comandos de Historial

### `git revert`

Crea un **nuevo commit** que deshace los cambios de un commit anterior, **sin reescribir historial**.

**Cómo funciona:**
```
Antes:
A---B---C (main)
        ↑
     mal commit

Después de: git revert C
A---B---C---C' (main)
            ↑
        deshace C
```

**Sintaxis:**
```bash
# Revertir último commit
git revert HEAD

# Revertir commit específico
git revert a1b2c3d

# Revertir múltiples commits
git revert HEAD~3..HEAD

# Revertir sin hacer commit inmediato
git revert -n a1b2c3d

# Revertir un merge commit
git revert -m 1 a1b2c3d  # -m 1 indica que quieres mantener la rama principal
```

**Cuándo usar:**
- Para deshacer cambios en historial público
- Cuando necesitas registro de la reversión
- Es la forma **segura** de deshacer en ramas compartidas

---

### `git reset`

Mueve el puntero HEAD y opcionalmente modifica staging area y working directory.

**⚠️ Peligroso**: Puede perder cambios permanentemente.

**Tres modos:**

#### 1. **Soft**: Solo mueve HEAD
```bash
git reset --soft HEAD~1

# Efecto:
# - Commits deshechos
# - Cambios quedan en staging
# - Working directory sin cambios
```

#### 2. **Mixed** (por defecto): Mueve HEAD y unstage
```bash
git reset HEAD~1
# o
git reset --mixed HEAD~1

# Efecto:
# - Commits deshechos
# - Cambios quedan en working directory (sin staging)
# - Archivos modificados pero no staged
```

#### 3. **Hard**: Elimina todo
```bash
git reset --hard HEAD~1

# ⚠️ Efecto:
# - Commits deshechos
# - Staging limpio
# - Working directory restaurado
# - ¡CAMBIOS PERDIDOS!
```

**Diagrama comparativo:**
```
Estado inicial:
A---B---C (HEAD, main)

git reset --soft HEAD~1:
A---B (HEAD, main)
Cambios de C en staging

git reset --mixed HEAD~1:
A---B (HEAD, main)
Cambios de C sin staging

git reset --hard HEAD~1:
A---B (HEAD, main)
Cambios de C eliminados
```

**Casos de uso:**

```bash
# Deshacer último commit pero mantener cambios
git reset --soft HEAD~1

# Unstage archivos (quitar de staging)
git reset archivo.js
# o todos:
git reset

# Deshacer cambios locales (¡PELIGROSO!)
git reset --hard HEAD

# Volver a un commit específico
git reset --hard a1b2c3d

# Deshacer un push accidental (si nadie ha pulleado)
git reset --hard HEAD~1
git push --force  # ⚠️ Cuidado con esto
```

**Recuperar después de reset hard:**
```bash
# Git guarda referencias por ~30 días
git reflog

# Verás algo como:
# a1b2c3d HEAD@{0}: reset: moving to HEAD~1
# b2c3d4e HEAD@{1}: commit: Mi commit perdido

# Recuperar:
git reset --hard b2c3d4e
```

---

### `git tag`

Marca puntos específicos en el historial como importantes (releases, versiones).

**Tipos de tags:**

#### 1. **Lightweight tag** (simple referencia)
```bash
git tag v1.0.0
```

#### 2. **Annotated tag** (recomendado, con metadata)
```bash
git tag -a v1.0.0 -m "Versión 1.0.0 - Release inicial"
```

**Comandos comunes:**

```bash
# Listar tags
git tag
git tag -l "v1.*"  # filtrar

# Ver información de un tag
git show v1.0.0

# Crear tag en commit específico
git tag -a v1.0.0 a1b2c3d -m "Mensaje"

# Eliminar tag local
git tag -d v1.0.0

# Eliminar tag remoto
git push origin --delete v1.0.0

# Pushear tags al remoto
git push origin v1.0.0       # un tag específico
git push origin --tags       # todos los tags

# Checkout a un tag
git checkout v1.0.0  # entra en "detached HEAD state"
```

**Convención de nombres (Semantic Versioning):**
```
v1.2.3
│ │ │
│ │ └─ PATCH: Bug fixes
│ └─── MINOR: Nuevas features (compatible)
└───── MAJOR: Cambios incompatibles
```

**Cuándo usar:**
- Marcar releases (v1.0.0, v2.1.5)
- Puntos importantes del desarrollo
- Para poder volver a versiones específicas

**Ejemplo práctico:**
```bash
# Acabas de terminar la versión 1.0.0
git tag -a v1.0.0 -m "Release 1.0.0 - Primera versión estable"
git push origin v1.0.0

# Luego puedes hacer:
git checkout v1.0.0  # volver a esa versión
```

---

## Comandos de Sincronización

### `git push`

Envía commits locales al repositorio remoto.

**Sintaxis básica:**
```bash
# Push a la rama actual
git push

# Push especificando remoto y rama
git push origin main

# Primera vez que pusheas una rama
git push -u origin feature-nueva
# -u establece tracking (luego solo necesitas: git push)
```

**Opciones importantes:**

```bash
# Forzar push (⚠️ PELIGROSO - reescribe historial remoto)
git push --force
# o más seguro:
git push --force-with-lease  # solo fuerza si nadie más ha pusheado

# Pushear todos los tags
git push --tags

# Pushear y establecer upstream
git push -u origin main

# Eliminar rama remota
git push origin --delete nombre-rama

# Push de todas las ramas
git push --all
```

**Situaciones comunes:**

```bash
# Error: Updates were rejected
# Causa: El remoto tiene commits que tú no tienes
# Solución:
git pull --rebase  # o git pull
git push

# Error: No tienes permisos
# Solución: Verifica tus credenciales o token

# Primera vez en nuevo repo
git remote add origin https://github.com/usuario/repo.git
git push -u origin main
```

---

### `git fetch`

Descarga cambios del remoto **sin fusionarlos** (más seguro que pull).

**Sintaxis:**
```bash
# Fetch de todos los remotos
git fetch

# Fetch de un remoto específico
git fetch origin

# Fetch de una rama específica
git fetch origin main

# Fetch y eliminar referencias a ramas remotas eliminadas
git fetch --prune
```

**Qué hace:**
```
Remoto:  A---B---C---D (origin/main)
Local:   A---B---C (main)

Después de: git fetch
Remoto:  A---B---C---D (origin/main)
Local:   A---B---C (main)
         origin/main apunta a D (actualizado)
```

**Cuándo usar:**
- Para ver qué hay nuevo sin afectar tu trabajo
- Antes de hacer merge manual
- Para revisar cambios antes de integrarlos

**Workflow recomendado:**
```bash
# 1. Ver qué hay nuevo
git fetch origin

# 2. Comparar con tu rama
git log main..origin/main  # ver commits que no tienes
git diff main origin/main  # ver diferencias

# 3. Decidir qué hacer
git merge origin/main   # fusionar
# o
git rebase origin/main  # rebase
```

---

### `git pull`

Descarga cambios del remoto **y los fusiona** (fetch + merge).

**Sintaxis:**
```bash
# Pull con merge (por defecto)
git pull

# Pull con rebase (recomendado para historial limpio)
git pull --rebase

# Pull de remoto y rama específicos
git pull origin main
```

**Qué hace:**
```bash
git pull
# equivale a:
git fetch
git merge origin/main

git pull --rebase
# equivale a:
git fetch
git rebase origin/main
```

**Configurar pull por defecto:**
```bash
# Configurar para siempre usar rebase
git config --global pull.rebase true

# O solo para este repositorio
git config pull.rebase true
```

**Resolver conflictos en pull:**
```bash
git pull origin main
# CONFLICT (content): Merge conflict in archivo.js

# Editar archivos, resolver conflictos
git add archivo.js

# Si fue pull normal:
git commit

# Si fue pull --rebase:
git rebase --continue
```

---

### `git clone`

Copia un repositorio completo a tu máquina local.

**Sintaxis:**
```bash
# Clonar repositorio
git clone https://github.com/usuario/repositorio.git

# Clonar en carpeta específica
git clone https://github.com/usuario/repo.git mi-carpeta

# Clonar solo una rama específica
git clone -b develop https://github.com/usuario/repo.git

# Clonar con profundidad limitada (más rápido)
git clone --depth 1 https://github.com/usuario/repo.git
```

**Qué incluye:**
- Todo el historial de commits
- Todas las ramas (como referencias remotas)
- La rama principal checked out
- Configuración de remoto (origin)

---

### `git remote`

Gestiona repositorios remotos.

**Comandos comunes:**
```bash
# Ver remotos configurados
git remote
git remote -v  # con URLs

# Añadir remoto
git remote add origin https://github.com/usuario/repo.git

# Cambiar URL de remoto
git remote set-url origin https://github.com/usuario/nuevo-repo.git

# Eliminar remoto
git remote remove origin

# Renombrar remoto
git remote rename origin upstream

# Ver información de remoto
git remote show origin
```

**Múltiples remotos:**
```bash
# Típico en forks
git remote add origin https://github.com/tu-usuario/repo.git
git remote add upstream https://github.com/usuario-original/repo.git

# Fetch de upstream
git fetch upstream

# Merge de upstream a tu main
git checkout main
git merge upstream/main
```

---

## Comandos Avanzados

### `git stash`

Guarda cambios temporalmente sin hacer commit.

**Sintaxis:**
```bash
# Guardar cambios actuales
git stash

# Guardar con mensaje descriptivo
git stash save "WIP: trabajando en login"

# Incluir archivos untracked
git stash -u

# Incluir archivos ignorados también
git stash -a

# Listar stashes
git stash list
# stash@{0}: WIP on main: a1b2c3d mensaje
# stash@{1}: WIP on feature: b2c3d4e otro mensaje

# Aplicar último stash
git stash apply

# Aplicar y eliminar último stash
git stash pop

# Aplicar stash específico
git stash apply stash@{1}

# Eliminar stash
git stash drop stash@{0}

# Limpiar todos los stashes
git stash clear

# Ver contenido de un stash
git stash show -p stash@{0}
```

**Caso de uso:**
```bash
# Estás trabajando en una feature
# Te piden un hotfix urgente

git stash  # guardar trabajo actual
git checkout main
git checkout -b hotfix
# ... hacer el fix ...
git checkout feature
git stash pop  # recuperar trabajo
```

---

### `git diff`

Muestra diferencias entre commits, branches, archivos.

**Sintaxis:**
```bash
# Ver cambios no staged
git diff

# Ver cambios staged (listos para commit)
git diff --staged
# o
git diff --cached

# Comparar con un commit específico
git diff a1b2c3d

# Comparar dos commits
git diff a1b2c3d b2c3d4e

# Comparar ramas
git diff main feature

# Diferencias de un archivo específico
git diff archivo.js

# Mostrar solo nombres de archivos cambiados
git diff --name-only

# Estadísticas de cambios
git diff --stat
```

---

### `git reflog`

Historial de **todos** los movimientos de HEAD (útil para recuperar trabajo perdido).

**Sintaxis:**
```bash
# Ver reflog
git reflog

# Reflog con fechas
git reflog --relative-date

# Reflog de una rama específica
git reflog show main
```

**Recuperar trabajo perdido:**
```bash
# Hiciste git reset --hard accidentalmente
git reflog
# a1b2c3d HEAD@{0}: reset: moving to HEAD~1
# b2c3d4e HEAD@{1}: commit: Mi trabajo importante ← aquí está!

# Recuperar:
git reset --hard b2c3d4e
```

---

### `git blame`

Muestra quién modificó cada línea de un archivo y cuándo.

**Sintaxis:**
```bash
# Ver blame de un archivo
git blame archivo.js

# Mostrar email del autor
git blame -e archivo.js

# Ver solo líneas específicas
git blame -L 10,20 archivo.js

# Formato más legible
git blame -c archivo.js
```

**Ejemplo de salida:**
```
a1b2c3d (Juan Pérez  2025-01-15 10:30:00 +0100  1) function login() {
b2c3d4e (María López 2025-02-01 14:20:00 +0100  2)   return auth.verify();
c3d4e5f (Juan Pérez  2025-02-05 09:15:00 +0100  3) }
```

---

### `git bisect`

Búsqueda binaria para encontrar qué commit introdujo un bug.

**Proceso:**
```bash
# Iniciar bisect
git bisect start

# Marcar commit actual como malo
git bisect bad

# Marcar último commit bueno conocido
git bisect good a1b2c3d

# Git hace checkout a commit intermedio
# Pruebas si funciona...

# Si funciona:
git bisect good
# Si no funciona:
git bisect bad

# Repetir hasta encontrar el commit culpable

# Terminar bisect
git bisect reset
```

**Automatizado:**
```bash
git bisect start HEAD v1.0.0
git bisect run npm test  # ejecuta tests automáticamente
```

---

## GitHub vs Git

### ¿Qué es Git?

**Git** es el **sistema de control de versiones** (software) que se ejecuta en tu máquina local.

- Creado por Linus Torvalds en 2005
- Es de código abierto y gratuito
- Funciona completamente offline
- Se instala en tu ordenador

### ¿Qué es GitHub?

**GitHub** es un **servicio de hosting** para repositorios Git en la nube (como Dropbox pero para código).

- Plataforma web propiedad de Microsoft
- Aloja repositorios Git remotos
- Añade funcionalidades extra: Issues, Pull Requests, Actions, etc.
- Requiere conexión a internet

### Diferencias clave

| Aspecto | Git | GitHub |
|---------|-----|--------|
| Tipo | Software/herramienta | Servicio web |
| Ubicación | Tu ordenador | Servidores de GitHub |
| Funcionamiento | Offline | Online |
| Costo | Gratis | Freemium |
| Funcionalidad | Control de versiones | Hosting + colaboración |

### Alternativas a GitHub

- **GitLab** - Similar a GitHub, con CI/CD integrado
- **Bitbucket** - De Atlassian, integración con Jira
- **Gitea** - Auto-hosted, open source
- **SourceForge** - Uno de los más antiguos
- **Azure DevOps** - De Microsoft, para empresas

**Todos usan Git** como sistema de control de versiones.

### Flujo de trabajo Git + GitHub

```bash
# 1. LOCAL (Git)
git init
git add .
git commit -m "Initial commit"

# 2. CONECTAR CON GITHUB
git remote add origin https://github.com/usuario/repo.git

# 3. SINCRONIZAR (Git + GitHub)
git push -u origin main    # subir a GitHub
git pull origin main       # bajar de GitHub
```

### Características exclusivas de GitHub

- **Pull Requests**: Proponer cambios y revisión de código
- **Issues**: Sistema de tickets/bugs
- **Actions**: CI/CD automatizado
- **Projects**: Gestión de proyectos estilo Kanban
- **Discussions**: Foros de comunidad
- **Releases**: Publicar versiones
- **GitHub Pages**: Hosting de sitios estáticos gratis
- **Colaboración**: Forks, Code review, etc.

---

## Flujos de Trabajo Comunes

### Flujo Básico Diario

```bash
# 1. Actualizar tu repo
git pull origin main

# 2. Crear rama para nueva feature
git checkout -b feature/nueva-funcionalidad

# 3. Hacer cambios y commits
git add .
git commit -m "feat: añadir nueva funcionalidad"

# 4. Pushear tu rama
git push -u origin feature/nueva-funcionalidad

# 5. Crear Pull Request en GitHub
# (desde la interfaz web)

# 6. Después de aprobación, fusionar
git checkout main
git pull origin main
git branch -d feature/nueva-funcionalidad
```

### GitHub Flow (Recomendado para equipos)

```
main
  │
  ├── feature/login ──┐
  │                   │ (Pull Request)
  │                   │ (Code Review)
  │◄──────────────────┘ (Merge)
  │
  ├── feature/payment ─┐
  │                    │
  │◄───────────────────┘
  │
```

**Reglas:**
1. `main` siempre está lista para producción
2. Cada feature en su propia rama
3. Pull Requests para todo
4. Deploy después de merge a main

### Git Flow (Para proyectos grandes)

```
main          ●────────●────────●
              ↑        ↑        ↑
develop  ─────●────●───●────●───●
              ↑    ↑        ↑
feature/x     ●────●
feature/y          ●────────●
hotfix             ●─────────────→●
```

**Ramas:**
- `main`: Producción
- `develop`: Desarrollo principal
- `feature/*`: Nuevas funcionalidades
- `release/*`: Preparación de releases
- `hotfix/*`: Correcciones urgentes

### Conventional Commits

Formato estándar para mensajes de commit:

```
<tipo>[ámbito opcional]: <descripción>

[cuerpo opcional]

[footer opcional]
```

**Tipos:**
- `feat`: Nueva funcionalidad
- `fix`: Corrección de bug
- `docs`: Documentación
- `style`: Formato (no afecta código)
- `refactor`: Refactorización
- `test`: Tests
- `chore`: Mantenimiento

**Ejemplos:**
```bash
git commit -m "feat(auth): añadir login con Google"
git commit -m "fix(api): corregir error 500 en /users"
git commit -m "docs: actualizar README con instrucciones"
git commit -m "refactor(utils): simplificar función de validación"
```

---

## Resolución de Problemas Comunes

### "Detached HEAD state"

**Problema:** Hiciste checkout a un commit específico.

```bash
# Salir sin cambios
git checkout main

# Guardar cambios en nueva rama
git checkout -b nueva-rama
```

### Conflictos de merge

**Solución:**
```bash
# Git marca los conflictos en archivos:
<<<<<<< HEAD
tu código
=======
código del otro
>>>>>>> rama-otra

# 1. Editar archivos manualmente
# 2. Quitar marcadores <<<<, ====, >>>>
# 3. Guardar la versión correcta

git add archivo-resuelto.js
git commit  # o git merge --continue
```

### Deshice algo por error

```bash
# Ver historial completo
git reflog

# Volver a estado anterior
git reset --hard HEAD@{2}
```

### Necesito cambiar el último commit

```bash
# Cambiar mensaje
git commit --amend -m "Nuevo mensaje"

# Añadir archivos olvidados
git add archivo-olvidado.js
git commit --amend --no-edit
```

### Commit en rama equivocada

```bash
# Estás en main pero el commit debía ir a feature
git log  # copiar hash del commit erróneo

git checkout feature
git cherry-pick <hash>

git checkout main
git reset --hard HEAD~1  # eliminar de main
```

---

## Configuración Útil

### Configuración Global

```bash
# Identidad
git config --global user.name "Tu Nombre"
git config --global user.email "tu@email.com"

# Editor por defecto
git config --global core.editor "code --wait"  # VSCode
git config --global core.editor "vim"          # Vim

# Colores
git config --global color.ui auto

# Alias útiles
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.cm commit
git config --global alias.lg "log --oneline --graph --all"

# Pull por defecto con rebase
git config --global pull.rebase true

# Auto-setup de tracking en push
git config --global push.autoSetupRemote true
```

### Archivo .gitignore

```bash
# Archivos de Node.js
node_modules/
npm-debug.log

# Variables de entorno
.env
.env.local

# IDEs
.vscode/
.idea/
*.swp

# Sistema operativo
.DS_Store
Thumbs.db

# Build
dist/
build/
*.log
```

---

