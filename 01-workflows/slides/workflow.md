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
---

  <!-- _paginate: skip -->

  <div class="front">
    <h1 class="title"> Git Avanzado </h1>
    <hr class="line"/>
    <p class="author">Arturo Silvelo</p>
    <p class="company">Try New Roads</p>
  </div>

---

# Flujos de trabajo en Git

---

## Trunk Based Development

Todos los desarrolladores trabajan sobre una única rama principal (trunk, main o master).
Las ramas de trabajo son muy cortas y se fusionan rápidamente.
Favorece la integración continua y despliegues frecuentes.

**Ventajas:**

- Simplicidad y rapidez.
- Menos conflictos de integración.

**Desventajas:**

- Requiere alta disciplina y automatización.

---

## Feature Branch Workflow

Cada nueva funcionalidad o corrección se desarrolla en una rama independiente.
Las ramas se fusionan a la rama principal mediante Pull Requests.
Facilita la revisión y el control de cambios.

**Ventajas:**

- Permite trabajo paralelo y seguro.
- Facilita la revisión de código.

**Desventajas:**

- Puede generar ramas huérfanas si no se gestionan bien.

---

## Forking Workflow

Cada colaborador crea un fork (copia) del repositorio principal.
Los cambios se proponen mediante Pull Requests desde el fork al repositorio original.
Común en proyectos open source.

**Ventajas:**

- Permite contribuciones externas sin acceso directo al repositorio.
- Ideal para comunidades grandes.

**Desventajas:**

- El proceso de revisión puede ser más lento.

---

## Git Flow

Define ramas específicas para desarrollo (develop), producción (main/master), funcionalidades (feature), correcciones (hotfix) y lanzamientos (release).
Muy útil para proyectos con ciclos de lanzamiento definidos.

**Ventajas:**

- Organización clara del ciclo de vida del software.
- Facilita la gestión de versiones y correcciones.

**Desventajas:**

- Puede ser complejo para proyectos pequeños.

---

## GitHub Flow

Basado en ramas de funcionalidades y Pull Requests.
Simplicidad y rapidez, ideal para despliegues continuos.
Solo dos ramas principales: producción y ramas de trabajo.

**Ventajas:**

- Fácil de entender y aplicar.
- Favorece la entrega continua.

**Desventajas:**

- No contempla ciclos de lanzamiento complejos.

---

# Protección de ramas

---

## ¿Qué es la protección de ramas?

La protección de ramas es una funcionalidad que permite establecer reglas para evitar cambios no deseados en ramas críticas del repositorio (por ejemplo, `main` o `develop`).  
Su objetivo es asegurar la calidad del código y evitar errores accidentales.

---

## ¿Para qué sirve la protección de ramas?

- Evitar cambios directos en ramas importantes.
- Obligar a que los cambios pasen por revisiones y Pull Requests.
- Garantizar que el código fusionado cumple con los estándares del equipo.
- Proteger el historial y la integridad del proyecto.

---

## ¿Qué opciones existen?

- **Pull Request obligatorio:** Solo se puede fusionar código mediante Pull Request.
- **Revisiones obligatorias:** Uno o varios revisores deben aprobar los cambios antes del merge.
- **Checks automáticos:** Exigir que pasen tests, linters o builds antes de permitir el merge.
- **Restricción de pushes:** Limitar quién puede hacer push o aprobar cambios.
- **Bloqueo de force-push y borrado:** Impedir el force-push y el borrado de ramas protegidas.
- **Requerir actualizaciones:** Obligar a que la rama esté actualizada con la principal antes de fusionar.

---
