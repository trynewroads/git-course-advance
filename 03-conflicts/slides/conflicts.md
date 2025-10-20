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

## Conflictos

---

### Conflictos

Un **conflicto** ocurre cuando Git no puede fusionar automáticamente los cambios realizados en diferentes ramas o commits, porque afectan a las mismas líneas de un archivo o a archivos eliminados/modificados en paralelo.

---

### Situaciones comunes que generan conflictos

- **Edición concurrente:**  
  Dos o más personas modifican las mismas líneas de un archivo en ramas diferentes.

- **Eliminación y modificación:**  
  Un archivo se elimina en una rama y se modifica en otra.

- **Renombrado de archivos:**  
  Un archivo se renombra en una rama y se edita en otra.

---

- **Rebase o cherry-pick:**  
  Al reescribir el historial, pueden surgir conflictos si los cambios ya existen en otra rama.

- **Fusión de ramas antiguas:**  
  Cuanto más tiempo pasa sin fusionar ramas, mayor es la probabilidad de conflictos.

---

### Cómo prevenir conflictos en Git

- **Comunicación constante:**  
  Habla con tu equipo sobre los archivos en los que estás trabajando para evitar solapamientos.

- **Fusiones frecuentes:**  
  Integra los cambios de la rama principal (`main` o `develop`) en tu rama de trabajo de forma regular para minimizar diferencias.

- **Pequeños commits y ramas cortas:**  
  Trabaja en ramas de vida corta y realiza commits pequeños y frecuentes para facilitar la integración.

---

- **Evita cambios masivos:**  
  No hagas refactors grandes o cambios estructurales sin avisar al equipo.

- **Herramientas de bloqueo:**  
  Usa mecanismos de bloqueo o advertencia en archivos críticos (por ejemplo, archivos binarios o de configuración global).

---

### ¿Cómo se identifica un conflicto en Git?

- Al intentar hacer un `merge`, `rebase` o `cherry-pick`, Git detiene la operación y muestra un mensaje de conflicto.
- Los archivos afectados aparecen como “Unmerged” en `git status`.

<figure>
  <img src="../../img/git_status_unmerge.png" height="320px" alt="Status Unmerge">
</figure>

---

- Git inserta marcas especiales en los archivos conflictivos para señalar las diferencias

<figure>
  <img src="../../img/conflict_file.png" height="225px" alt="Conflict File">
</figure>

- Debes editar manualmente los archivos para resolver el conflicto, eliminar las marcas y decidir qué cambios conservar.
