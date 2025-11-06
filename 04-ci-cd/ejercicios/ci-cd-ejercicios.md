---
marp: true
theme: default
title: CI/CD
paginate: true
size: 16:9
backgroundColor: #2E2052;
color: #ffffff;
footer: CI/CD
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
    max-height: 75%;
    height: auto;
    display: flex;
    flex: 1 0 auto;
    max-width: 100%;
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

  table {
    margin: auto;
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
    <h1 class="title"> CI/CD </h1>
    <hr class="line"/>
    <p class="author">Arturo Silvelo</p>
    <p class="company">Try New Roads</p>
  </div>

---




## Ejercicio: Configurar hooks locales en un repositorio Python


En este ejercicio, vamos a configurar dos hooks locales en un repositorio de Python para automatizar tareas comunes:

1. **Hook `pre-commit`**: Validará los archivos Python staged utilizando un linter (`flake8`) antes de permitir un commit.

2. **Hook `commit-msg`**: Ejecutará los tests del proyecto utilizando `pytest` antes de permitir un push.


---

#### Pasos a seguir:

1. **Preparar el entorno**:
   - Utiliza uno existente.
    
      ```
      unzip ci-hook.zip
      ```

   - Asegúrate de tener `black`, `flake8` y `pytest` instalados en tu entorno:


     ```bash
     python3 -m venv venv
     source venv/bin/activate
     pip install flake8 black pytest
     ```
  
    - Fichero `.flake8`

      ```
      [flake8]
        max-line-length = 88
        extend-ignore = E203, W503
      ```

---

2. **Configurar el hook `pre-commit`**:
   - Crea el archivo `.git/hooks/pre-commit`ó usar `pre-commit`
   - Escribe un script que valide los archivos Python staged con `black`  y `flake8`.
   - Haz el hook ejecutable:

     ```bash
     chmod +x .git/hooks/pre-commit
     ```
---

  - `pre-commit`:
    - Instalar dependencia
    
      ```
      pip install pre-commit
      ```
    - Configurar `.pre-commit-config.yaml`
      - https://github.com/psf/black
      - https://github.com/pycqa/flake8
---

3. **Configurar el hook `pre-push`**:
   - Crea el archivo `.git/hooks/commit-msg`.
   - Escribe un script que ejecute los tests del proyecto con `pytest`.
   - Haz el hook ejecutable:

     ```bash
     chmod +x .git/hooks/commit-msg
     ```

---

4. **Probar los hooks**:
   - Modifica un archivo Python con errores de estilo y prueba el hook `pre-commit`.
   - Intenta hacer un push con tests que fallen y verifica que el hook `commit-msg` lo bloquee.


---

## Ejercicio: Configurar GitHub Actions para un repositorio Python


Crear un workflow de CI con GitHub Actions que ejecute formateo/lint y tests automáticamente en cada push y pull request.

---

1. Archivo de workflow en `.github/workflows/ci.yml` que:
   - Se dispare en `push` y `pull_request` sobre ramas `main`.
   - Use `actions/checkout@v4` y `actions/setup-python@v4`.
   - Instale dependencias (`requirements.txt`) y herramientas `black`, `flake8`, `pytest`.
   - Ejecute: `black --check .`, `flake8 .` y `pytest`.

---

Pasos sugeridos para realizarlo  

1. Crear `.github/workflows/ci.yml` con los jobs y steps necesarios.  

2. Comprobar en una rama feature: push → abrir PR → verificar ejecución en Actions.  

3. Corregir un error intencionado (p. ej. mala formatación o test roto) y comprobar que el workflow falla.

