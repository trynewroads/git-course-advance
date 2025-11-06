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
   - Crea un repositorio nuevo o utiliza uno existente.
   - Asegúrate de tener `flake8` y `pytest` instalados en tu entorno:

     ```bash
     python3 -m venv venv
     source venv/bin/activate
     pip install flake8 black pytest
     ```

---

2. **Configurar el hook `pre-commit`**:
   - Crea el archivo `.git/hooks/pre-commit`.
   - Escribe un script que valide los archivos Python staged con `flake8`.
   - Haz el hook ejecutable:

     ```bash
     chmod +x .git/hooks/pre-commit
     ```


---


```
#!/bin/bash
# filepath: .git/hooks/pre-commit
# Hook pre-commit para ejecutar Flake8 en archivos staged

set -e

# Obtener archivos staged que terminan en .py
FILES=$(git diff --cached --name-only --diff-filter=ACM | grep '\.py$')

if [ -z "$FILES" ]; then
  echo "No Python files to lint."
  exit 0
fi

# Ejecutar Flake8 en los archivos staged
echo "Running Flake8..."
echo "$FILES" | xargs flake8

if [ $? -ne 0 ]; then
  echo "Flake8 found issues. Commit aborted."
  exit 1
fi

echo "Flake8 passed. Proceeding with commit."
exit 0
```

---

3. **Configurar el hook `pre-push`**:
   - Crea el archivo `.git/hooks/commit-msg`.
   - Escribe un script que ejecute los tests del proyecto con `pytest`.
   - Haz el hook ejecutable:

     ```bash
     chmod +x .git/hooks/commit-msg
     ```
---

```
#!/bin/bash
# filepath: .git/hooks/pre-push
# Hook pre-push para ejecutar tests con pytest

set -e

echo "Running tests with pytest..."
pytest

if [ $? -ne 0 ]; then
  echo "Tests failed. Push aborted."
  exit 1
fi

echo "All tests passed. Proceeding with push."
exit 0

```

---

4. **Probar los hooks**:
   - Modifica un archivo Python con errores de estilo y prueba el hook `pre-commit`.
   - Intenta hacer un push con tests que fallen y verifica que el hook `commit-msg` lo bloquee.



---



#### Pasos a seguir:

1. **Preparar el entorno**:
   - Crea un repositorio nuevo o utiliza uno existente.
   - Asegúrate de tener `pre-commit`, `flake8` y `pytest` instalados en tu entorno:

     ```bash
     python3 -m venv venv
     source venv/bin/activate
     pip install pre-commit flake8 pytest
     ```

---

2. **Configurar pre-commit**:
   - Crea un archivo `.pre-commit-config.yaml` en la raíz del repositorio con el siguiente contenido:

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

---


```yaml
repos:
  - repo: https://github.com/psf/black
    rev: 23.3.0
    hooks:
      - id: black
        language_version: python3
  - repo: https://github.com/pycqa/flake8
    rev: 6.1.0
    hooks:
      - id: flake8
        name: Revisar estilo con flake8
        language_version: python3
  - repo: local
    hooks:
      - id: pytest
        name: pytest
        entry: pytest
        language: system
        pass_filenames: false
        stages: [commit-msg]
```
---

   - Este archivo configura dos hooks:
     - `black`, `flake8` para validar los archivos staged en el hook `pre-commit`.
     - `pytest` para ejecutar los tests en el hook `commit-msg`.

---

3. **Instalar los hooks**:
   - Ejecuta el siguiente comando para instalar los hooks en el repositorio:
     ```bash
     pre-commit install
     pre-commit install --hook-type commit-msg
     ```

---

4. **Probar los hooks**:
   - Modifica un archivo Python con errores de estilo y prueba el hook `pre-commit`:
     ```bash
     git add <archivo>
     git commit -m "Test pre-commit hook"
     ```
   - Introduce un test que falle y prueba el hook `commit-msg`:
     ```bash
     git commit
     ```


---

```yaml
     name: CI - lint & test

on:
  push:
    branches: [ main, develop ]
  pull_request:
    branches: [ main, develop ]
```
---

```yaml
jobs:
  lint-and-test:
    runs-on: ubuntu-latest
    strategy:
      matrix:
        python-version: [3.11]
    steps:
      - name: Checkout repository
        uses: actions/checkout@v4
        with:
          fetch-depth: 0

      - name: Set up Python ${{ matrix.python-version }}
        uses: actions/setup-python@v4
        with:
          python-version: ${{ matrix.python-version }}
      - name: Cache pip
        uses: actions/cache@v4
        with:
          path: ~/.cache/pip
          key: pip-${{ runner.os }}-py${{ matrix.python-version }}-${{ hashFiles('**/requirements.txt') }}
          restore-keys: |
            pip-${{ runner.os }}-py${{ matrix.python-version }}-

```

---

```yaml

      - name: Install dependencies
        run: |
          python -m pip install --upgrade pip
          if [ -f requirements.txt ]; then pip install -r requirements.txt; fi
          pip install black flake8 pytest

      - name: Run Black (check)
        run: |
          black --check .

      - name: Run Flake8
        run: |
          flake8 .

      - name: Run tests
        run: |
          pytest -q

```