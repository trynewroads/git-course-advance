---
marp: true
theme: default
title: Git Avanzado
paginate: true
size: 16:9
backgroundColor: #2E2052;
color: #ffffff;
footer: Git Avanzado
header: |
  <div class="logo-start">
    <img src="../../img/git-logo-white.png" alt="Logo Git"  class="logo"/>
  </div>
  <div class="logo-end">
    <img src="../../img/logo_white.png" alt="Logo TNR" class="logo" />
  </div>

style: |
  section {
    display:flex;
  }

  section > h2, h3, h4, h5{
    border-bottom: 2px solid #2D6BFA;
    padding-bottom: .3rem;
  }

  section::after, header, footer {
    font-weight: 700;
    color: white;
  }

  section > header {
    display: flex;
    top: 0;
    width: calc(100% - 60px);
    background: radial-gradient(30% 100% at 50% 0%, #2D6BFA 0%, rgba(46, 32, 82, 0.00) 100%);
  }

  .logo-start{
    flex:1;
  }

  .logo-end{
    flex:1;
    text-align:end;
    width: auto;
    height: 30px;
  }

  .logo {
    width: auto;
    height: 30px;
  }

  .front {
    display: flex;
    flex-direction: column;
  }

  .title{
    font-size:2.5em;
    margin-bottom:0;
    padding-bottom:0;
    
  }

  .line{
    width:100%;
    background-color: #2D6BFA
  }

  .author{
    font-size:1.3em;
    font-weight: 700;
    margin-bottom: 0;
  }

  .company{
    font-size:.9em;
    margin-top: .1em;
  }

  blockquote{
    color:white;
    font-size: 16px;
    border-color:#2D6BFA;
    bottom: 70px;
    left: 30px;
    position: absolute;
  }

  a{
    background-color: rgb(45 107 250 / 30%);
    color: white;
    font-weight: bold;
    text-decoration: none;
  }

  a > code {
    background-color: rgb(45 107 250 / 30%);
  }


  code {
    background-color: rgb(255 255 255 / 30%);
  }


  .container-column  {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: .5rem;
  }

  .small {
    font-size: 16px;
  }

  figure{
    display: block;    
  }

  figcaption{
    padding: 2px;
    text-align: center;
    font-size: 18px;
    font-bold: bold;
  }

  figure img {
    width: 100%;
    object-fit: contain;
  }


  table, td, th, tr{
    background: transparent!important;
  }

  th {
   font-size: 26px;
  }

  td {
    font-size: 20px;
  }
---

  <!-- _paginate: skip -->

  <div class="front">
    <h1 class="title"> Git Avanzado </h1>
    <hr class="line"/>
    <p class="author">Arturo Silvelo</p>
    <p class="company">Try New Roads</p>
  </div>

---

# Configuración avanzada de Git

---

## Configuración avanzada de Git

Git no solo guarda tu código, también registra información sobre **quién hizo qué cambios y cómo se gestionan los repositorios**.

- Tu identidad (nombre y correo para los commits)
- Alias para comandos frecuentes
- Comportamiento de fusión y merges
- Optimización y limpieza de repositorios
- Reglas de seguridad y políticas de la organización

---

**Por qué es importante:**

- Evita errores de identificación de commits.
- Mejora la productividad con comandos abreviados.
- Facilita la colaboración en equipos grandes.
- Mantiene los repositorios eficientes y limpios.

---

## Niveles de configuración en Git

Git tiene **tres niveles** de configuración:

1. **System (sistema)**

   - Aplica a **todos los usuarios y repositorios** en el equipo.
   - Ubicación: `/etc/gitconfig` o `C:\ProgramData\Git\config`.
   - Ideal para establecer reglas globales de la organización.

---

| Configuración            | Comando                                             | Explicación                                                             |
| ------------------------ | --------------------------------------------------- | ----------------------------------------------------------------------- |
| Editor por defecto       | `git config --system core.editor "nano"`            | Todos los usuarios usarán `nano` al abrir editores de commits o merges. |
| Colores de la terminal   | `git config --system color.ui auto`                 | Activa colores por defecto para todos los usuarios y repositorios.      |
| Política de line endings | `git config --system core.autocrlf true`            | Evita problemas de saltos de línea en equipos Windows/Linux.            |
| Path de hooks globales   | `git config --system core.hooksPath /opt/git/hooks` | Define hooks que se aplican a todos los repositorios del equipo.        |

---

2. **Global (usuario)**

   - Aplica a todos los repositorios de un usuario.
   - Ubicación: `~/.gitconfig`.
   - Se configura identidad, aliases y preferencias personales.

---

| Configuración                | Comando                                               | Explicación                                                             |
| ---------------------------- | ----------------------------------------------------- | ----------------------------------------------------------------------- |
| Nombre de usuario            | `git config --global user.name "Arturo Silvelo"`      | Se usa en todos los commits del usuario.                                |
| Correo de usuario            | `git config --global user.email "arturo@example.com"` | Asociado a todos los commits del usuario.                               |
| Alias de comandos            | `git config --global alias.co checkout`               | Facilita comandos frecuentes.                                           |
| Fusión automática con rebase | `git config --global pull.rebase true`                | El usuario siempre hará rebase al hacer pull, para un historial lineal. |
| Editor personalizado         | `git config --global core.editor "code --wait"`       | Configura el editor que prefiera el usuario, sin afectar a otros.       |

---

3. **Local (repositorio)**
   - Aplica solo al repositorio actual.
   - Ubicación: `.git/config`.
   - Útil para proyectos específicos o clientes distintos.

---

| Configuración               | Comando                                                  | Explicación                                                           |
| --------------------------- | -------------------------------------------------------- | --------------------------------------------------------------------- |
| Nombre de equipo o proyecto | `git config --local user.name "Equipo ProyectoX"`        | Sobrescribe la identidad global solo para este proyecto.              |
| Ignorar reglas específicas  | `git config --local core.excludesFile .gitignore_global` | Define reglas de exclusión solo para este repositorio.                |
| Branch principal            | `git config --local init.defaultBranch main`             | Configura la rama por defecto para este repositorio.                  |
| Hooks específicos           | `git config --local core.hooksPath .githooks`            | Usa hooks que solo se aplican a este repositorio.                     |
| Estrategia de merges        | `git config --local merge.ff false`                      | Fuerza merges con commit, sin fast-forward, solo en este repositorio. |

---

**Prioridad de configuración:** Local > Global > System

- **System**: políticas de la organización y todos los usuarios
- **Global**: preferencias y identidad del usuario
- **Local**: reglas específicas de un proyecto

---

# Gestión de credencial y seguridad

---

En Git y GitHub, la **autenticación y las credenciales** son esenciales para controlar quién puede leer o modificar un repositorio.

Una mala configuración puede provocar:

- Push sin permisos
- Exposición de datos sensibles
- Confusión entre identidades si se usan varias cuentas

---

## Métodos de autenticación en GitHub

1. **SSH Keys (recomendado para desarrolladores)**

   - Clave pública y privada.
   - Conexión segura sin pedir contraseña en cada push/pull.

---

### Configuración de SSH

- **Generar clave SSH:**

  ```bash
  ssh-keygen -t ed25519 -C "tu_email@example.com"
  ```

- Copiar contenido de ~/.ssh/id_ed25519.pub

- Añadirlo en Settings → SSH and GPG keys.

---

2. **Personal Access Tokens (PAT)**

   - Se usan en lugar de la contraseña para HTTPS.
   - Se pueden configurar con permisos específicos (repo, workflow, packages, etc.).

---

### Configuración de Personal Access Token (PAT)

1. Crear token en Settings → Developer settings → Personal access tokens → Tokens (classic).

2. Elegir permisos mínimos necesarios: repo para repositorios privados, workflow para GitHub Actions, etc.

---

## Manejo de múltiples cuentas

- Problema: un mismo equipo puede necesitar acceso a repositorios de cuentas distintas.

- Solución: usar configuración SSH con archivos de config:

---

```
# ~/.ssh/config
Host github-personal
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_ed25519_personal

Host github-work
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_ed25519_work

```

- Clonar usando el alias definido

```
git clone git@github-personal:usuario/repositorio.git
git clone git@github-work:empresa/repositorio.git
```

---

## Protección de secretos

Evitar subir información sensible al repositorio y proteger credenciales.

- Subir secretos (contraseñas, claves, tokens) puede comprometer proyectos y cuentas.
- Los errores son fáciles de cometer: accidentalmente un `.env` o un `credentials.json`.
- Mantener un repositorio seguro evita fugas de datos y problemas legales o empresariales.

---

## Estrategias de protección

```bash
git config --global core.excludesFile ~/.gitignore_global
```

```md
# .gitignore_global

_.env
_.key
_.pem
_.crt
credentials.json
```

---

# Internals de Git

---

## Internals de Git

- Git es un sistema **basado en snapshots**, no en diferencias entre archivos.
- Cada commit es un **objeto que apunta a un árbol de archivos**, que a su vez apunta a blobs (contenido de archivos).
- Git forma un **DAG (Directed Acyclic Graph)** de commits, lo que permite:
  - Historial lineal o ramificado
  - Fusión de ramas eficiente
  - Recuperación de cambios incluso eliminados

---

## Estructura interna de Git

- Cada repositorio Git tiene un directorio oculto .git en la raíz.
- Contiene toda la información necesaria para versionar el proyecto: commits, ramas, configuraciones, hooks, etc.
- Si borras .git, pierdes el historial, pero los archivos de trabajo permanecen.

---

| Elemento   | Función                                                                |
| ---------- | ---------------------------------------------------------------------- |
| `HEAD`     | Apunta al commit actual o a la rama activa                             |
| `config`   | Configuración local del repositorio                                    |
| `hooks/`   | Scripts que se ejecutan en eventos de Git (pre-commit, pre-push, etc.) |
| `objects/` | Contiene todos los **objetos de Git** (blobs, trees, commits, tags)    |
| `refs/`    | Contiene referencias a ramas (`heads`) y tags (`tags`)                 |
| `logs/`    | Reflog: historial de movimientos de HEAD y ramas                       |
| `info/`    | Archivos de configuración interna, como `.exclude`                     |

---

### Objects

- Cada commit es un objeto en .git/objects con un SHA único.
- Los almacena de manera comprimida y codificada
- Contiene:
  - Referencia al árbol
  - Commit padre
  - Autor y fecha
  - Mensaje

---

#### Tipos de Objetos

- Blob → contenido de archivo
- Tree → lista de archivos y subdirectorios, apunta a blobs y otros trees
- Commit → apunta a un tree y a sus padres

---

- Contenido de un commit

  ```bash
  $git cat-file -p 2e06f2b8448649f16a3e82660cb57616a457cedd
  tree 181cb51532a71991e1154b40b56e3b575b8d8e18
  author Arturo Silvelo <asilvelo@trynewroads.com> 1760527440 +0200
  committer Arturo Silvelo <asilvelo@trynewroads.com> 1760527440 +0200

  Commit A: archivo1.txt
  ```

- Contenido de un tree

  ```bash
  $git cat-file -p 181cb51532a71991e1154b40b56e3b575b8d8e18
  100644 blob 0152d71fe5e5653f52e8772031fb073a2aa113ac	archivo1.txt
  ```

- Contenido de un blob

  ```bash
  $git cat-file -p 0152d71fe5e5653f52e8772031fb073a2aa113ac
  Hola Git
  ```

---

### Ramas y referencias

Las ramas son simplemente archivos de texto en .git/refs/heads/ que contienen el SHA del último commit de esa rama.

```bash
$ls .git/refs/heads/
feature  main
```

```bash
$cat .git/refs/heads/feature
f88435db6de38b34a264c7fc25a771ae54e934ee
```

Tags funcionan de manera similar en .git/refs/tags/

---

### Logs

La carpeta .git/logs/ contiene los registros de movimientos de las referencias en tu repositorio, principalmente el reflog.

Historial completo de todos los movimientos de HEAD

```bash
$cat .git/logs/HEAD
# ó
$git reflog
ce455ac (HEAD -> main, tag: v0.1) HEAD@{0}: merge feature: Merge made by the 'ort' strategy.
a57fb6f HEAD@{1}: commit: Commit D: cambio en main
73fb1ea HEAD@{2}: checkout: moving from feature to main
f88435d (feature) HEAD@{3}: commit: Commit C: feature.txt
73fb1ea HEAD@{4}: checkout: moving from main to feature
73fb1ea HEAD@{5}: commit: Commit B: archivo2.txt
2e06f2b HEAD@{6}: commit (initial): Commit A: archivo1.txt
```

---

### index

staging area, donde Git guarda la información de los archivos que se van a commitear.

```bash
git ls-files --stage
```

---

### config

Configuración local del repositorio

```bash
git config --local user.name Teacher
```

```bash
cat .git/config
[user]
	name = Teacher
```

---

# Conventional Commits

---

# Commitlint y Husky

---

```

```
