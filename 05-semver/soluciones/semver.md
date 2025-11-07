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
    <h1 class="title"> SermVer </h1>
    <hr class="line"/>
    <p class="author">Arturo Silvelo</p>
    <p class="company">Try New Roads</p>
  </div>

---


## Ejercicio: Release automático con GitHub Actions 


- Implementar un workflow en GitHub Actions que genere releases automáticas (tag + GitHub Release + changelog) cuando se hagan push contra la rama `main`.  

- Trabajarás sobre el repositorio proporcionado en el fichero `semver.zip`.


Crear el fichero `.github/workflows/release.yml` en el repositorio (workflow que se activa al hacer push en `main`).  

--- 

Pasos:

  1. `actions/checkout@v5` (checkout del repositorio).  

  2. `commitizen-tools/commitizen-action@master` (usar commitizen para generar/versionar/changelog según commits).

  3. `softprops/action-gh-release@v1` (crear la GitHub Release y subir assets si procede).

  4. Hacer varios push para comprobar que los versionados se generan.
--- 


## Notas

Configurar `pyproject.toml`

```
[tool.commitizen]
name = "cz_conventional_commits"
version = "0.1.0"
tag_format = "v$version"
changelog_file = "CHANGELOG.md"
update_changelog_on_bump = true
```

Para GITHUB activar el uso de GITHUB_TOKEN en:
`Settings -> Actions -> Workflow permissions -> 
Read and write permissions`


---

```yaml
name: Release

on:
  push:
    branches:
      - main

jobs:
  bump-version:
    runs-on: ubuntu-latest
    name: "Bump version and create changelog with commitizen"
    steps:
      - name: Check out
        uses: actions/checkout@v5
        with:
          fetch-depth: 0
          token: "${{ secrets.GITHUB_TOKEN }}"
      - name: Create bump and changelog
        uses: commitizen-tools/commitizen-action@master
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          changelog_increment_filename: body.md
      - name: Release
        uses: softprops/action-gh-release@v1
        with:
          body_path: "body.md"
          tag_name: ${{ env.REVISION }}
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```