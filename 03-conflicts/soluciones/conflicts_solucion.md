---
marp: true
theme: default
title: Resolución de conflictos
paginate: true
size: 16:9
backgroundColor: #2E2052;
color: #ffffff;
footer: Resolución de conflictos
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
    <h1 class="title"> Resolución de conflictos  </h1>
    <hr class="line"/>
    <p class="author">Arturo Silvelo</p>
    <p class="company">Try New Roads</p>
  </div>

---

- Consultar los logs para obtener los `commit id`

  ```
  git log --online
  ```


- Iniciar el proceso de `bisect`

  ```
  git bisect start
  git bisect bad HEAD # último commit del repositorio
  git bisect good 6ba9e0f # primer commit del repositorio
  ```

  ```
  Bisecting: 19 revisions left to test after this (roughly 4 steps)
  ```

---

- Comprobar en cada paso (roughly 4 steps) si la aplicación funciona

  ```
  pytest -v
  ```

- Avanzar al siguiente paso

  ```
  git bisect good
  # ó
  git bisect bad
  ```

---

- Repetir proceso hasta el último paso

  ```
  git bisect bad
  ea2bdab147f7c871ee239e813fb8eb19dbdef168 is the first bad commit
  commit ea2bdab147f7c871ee239e813fb8eb19dbdef168
  Author: Carol <carol@example.com>
  Date:   Wed Nov 5 10:58:01 2025 +0100

      Commit 6: Format file

  operaciones/suma.py          | 2 +-
  tests/test_multiplicacion.py | 4 +---
  2 files changed, 2 insertions(+), 4 deletions(-)
  ```

  ```
  git blame operaciones/suma.py
  ccfdf5b9 (Alice 2025-11-05 10:45:24 +0100 1) def suma(a, b):
  ccfdf5b9 (Alice 2025-11-05 10:45:24 +0100 2)     """Suma a y b"""
  ea2bdab1 (Carol 2025-11-05 10:58:01 +0100 3)     return a - b
  ```

---

## Opción A — Arreglar en main (hotfix rápido)

Útil si necesitas una solución urgente y la práctica del repo lo permite.


Comandos:
```bash
git switch main
git pull

# editar operaciones/suma.py y restaurar:
# def suma(a, b):
#     return a + b

git add operaciones/suma.py
git commit -m "Commit 11: fix suma - restore correct addition behavior"
python3 -m pytest     # o el comando de tests del repositorio
git push origin main
```

---

## Opción B — Crear rama de corrección y merge (recomendado)

Flujo seguro para equipos: crea rama, corrige, PR/merge.

Comandos:

```bash
git switch main
git pull

git switch -c fix/suma/main

# editar operaciones/suma.py para corregir la función
git add operaciones/suma.py
git commit -m "Commit 11: fix suma - restore correct addition behavior"

```
---

```
pytest -v

# integrar vía merge (o abrir PR)
git switch main
git merge --no-ff fix/suma/main -m "Merge: fix/suma/main -> main"
git branch -d fix/suma/main
git push origin main
```


---

## Opción C — Rebase interactivo y enmendar (solo si NO está publicado o con acuerdo del equipo)



Reescribe la historia para corregir el commit culpable (mantiene historial "limpio").


1) Iniciar rebase interactivo desde el padre del commit objetivo. El sufijo `^` indica "el padre del commit":

    ```
    git rebase -i ea2bdab147f7c871ee239e813fb8eb19dbdef168^
    ```

(Equivalente: `git rebase -i ea2bdab147f7c871ee239e813fb8eb19dbdef168~1`)

---

2) En el editor que abra, cambia `pick` por `edit` en la línea del commit identificado (`Commit 6: Format file`), guarda y cierra.

    ```
    edit ea2bdab147f7c871ee239e813fb8eb19dbdef168 Commit 6: Format file
    ```

    ```
    def suma(a, b):
        """Suma a y b"""
        return a + b
    ```

3) Cuando el rebase pare en ese commit, arregla el código y prueba localmente:

    ```bash
    # editar operaciones/suma.py -> restore return a + b
    python3 -m pytest

    git add operaciones/suma.py
    git commit --amend -m "Commit 6: Format file (fix suma bug)"
    git rebase --continue
    ```