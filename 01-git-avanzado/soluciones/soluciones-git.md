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
    <h1 class="title"> Ejercicios prácticos — Git Avanzado </h1>
    <hr class="line"/>
    <p class="author">Arturo Silvelo</p>
    <p class="company">Try New Roads</p>
  </div>

---

# Ejercicios prácticos — Git Avanzado

Repositorio de trabajo: `01-git-avanzado/ejercicios/git-labs-repo` (crea con el script `setup-labs-repo.sh`).

---

## Lab 1 — Recuperar una rama borrada (reflog)

Objetivo: recuperar commits de una rama eliminada usando `git reflog`.

---

Pasos:

1. Preparar el repo:

```bash
cd git-labs-repo
``` 

2. Ver el reflog para identificar el commit perdido:

```bash
git reflog
```

3. Recuperar la rama a partir del reflog:

```bash
git checkout -b rama-recuperada 644763a
git log --oneline --decorate
```

Resultado esperado: tendrás una rama `rama-recuperada` con los commits etiquetados (p. ej. "Commit B: ...", "Commit C: ...").

---

## Lab 2 — Stash avanzado y mover WIP entre ramas

Objetivo: usar `git stash` para guardar trabajo en progreso y aplicarlo en otra rama.

---

Pasos:

1. Crear un nuevo cambio no commiteado:

```bash
git switch -c practica-stash
echo "cambios temporales" > temp2.txt
git add temp2.txt
git stash push -m "Commit G: WIP practica-stash"
```
---
3. Aplicar el stash en otra rama (sin eliminarlo):

```bash
git switch main
git stash apply stash@{0}
```

4. Alternativa: crear una rama a partir del stash:


```bash
git stash branch desde-stash stash@{0}
```

5. Limpiar stashes

```bash
git stash drop stash@{0}
git stash clear
```


