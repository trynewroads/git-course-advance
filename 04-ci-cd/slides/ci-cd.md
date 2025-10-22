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

## Introducción a CI/CD

---

### ¿Qué es CI y CD?

- CI (Continuous Integration): automatiza la integración de cambios (build + tests) en cada push/PR para detectar errores pronto.
- CD (Continuous Delivery / Deployment): automatiza la entrega o despliegue de artefactos a entornos (staging/production).
  - Delivery: artefactos preparados para desplegar manualmente.
  - Deployment: despliegue automático a producción.

---

## Conventional Commits

---

### Conventional Commits

Conventional Commits es una convención simple para mensajes de commit que aporta estructura al historial: facilita changelogs automáticos, versionado semántico y automatizaciones en CI/CD.

---

### Formato general

```
<type>(<scope>): <subject>
<BLANK LINE>
<body>
<BLANK LINE>
<footer>
```

---

### Type

- feat — nueva funcionalidad
- fix — corrección de bug
- docs — documentación
- style — formato (sin cambios de lógica)
- refactor — refactorización (sin cambios funcionales)
- perf — mejoras de rendimiento
- test — tests añadidos/modificados
- chore — tareas de mantenimiento
- ci — cambios en CI/CD

---

## Scope, subject y reglas básicas

- scope: opcional, indica área afectada (kebab-case): `feat(api)`, `fix(ui-button)`
- subject: breve, en minúsculas, modo imperativo, sin punto final: `fix(login): validate token`
- body: explica el “por qué” si hace falta
- footer: notas de breaking change o referencias a issues, ej. `BREAKING CHANGE: cambia X` o `Closes #123`

---

## Breaking changes

Se documentan en el footer:

```
feat(api): change response format

BREAKING CHANGE: response now includes 'meta' field instead of top-level 'count'
Closes #456
```

Los breaking changes suelen disparar incremento mayor en versionado semántico (major).

---

### Hooks

---

### Herramientas

#### Commitizen

---

### Github Actions

---

### Workflows

---

## Análisis Automático

---

### Circle CI

### SonnarQubne

### Snyk
