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
    <h1 class="title"> Automatización, calidad de código y hooks </h1>
    <hr class="line"/>
    <p class="author">Arturo Silvelo</p>
    <p class="company">Try New Roads</p>
  </div>

---

### ¿Qué es la automatización en Git y para qué sirve?

La automatización en Git permite ejecutar tareas repetitivas y controles de calidad de forma automática, mejorando la eficiencia y reduciendo errores humanos.

**Ventajas:**

- Asegura que el código cumple con los estándares del equipo.
- Detecta errores antes de integrar cambios.
- Facilita la integración y entrega continua (CI/CD).
- Mejora la colaboración y la calidad del proyecto.

---

# Calidad de código

---

#### Linters

Los linters analizan el código fuente para detectar errores de sintaxis, estilos y posibles problemas.

**Herramientas:**

- ESLint (JavaScript/TypeScript)
- Prettier (formateo automático)
- Flake8 (Python)
- Checkstyle (Java)

---

#### Convetional Commits

Seguir una convención en los mensajes de commit ayuda a mantener un historial claro y facilita la automatización de procesos como generación de changelogs y versionado semántico.

**Herramientas:**

- Conventional Commits
- Commitlint

---

#### Hooks de Git

Los hooks son scripts que se ejecutan automáticamente en determinados momentos del flujo de trabajo de Git.

- **Pre-commit:** Se ejecuta antes de crear un commit. Útil para lanzar linters y tests automáticos.
- **Pre-push:** Se ejecuta antes de hacer push. Permite ejecutar pruebas adicionales.
- **Husky:** Herramienta que facilita la gestión de hooks en proyectos modernos.

La integración de linters y tests automáticos en los hooks ayuda a garantizar que solo código de calidad llegue al repositorio.

---

# Automatización con CI/CD

---

#### ¿Qué es CI/CD?

CI/CD (Integración Continua y Entrega/Despliegue Continua) es una práctica que permite integrar, probar y desplegar cambios de forma automática y frecuente.

---

#### ¿Cómo funciona?

- Cada vez que se realiza un cambio en el repositorio, se ejecutan pipelines automáticos que validan, prueban y despliegan el código.
- Se pueden configurar flujos para ejecutar linters, tests, builds y despliegues en diferentes entornos.

---

#### ¿Cómo se configura?

- **GitHub Actions:** Plataforma integrada en GitHub para definir flujos de trabajo automáticos mediante archivos YAML.
- Permite ejecutar tareas en cada push, pull request o evento relevante.

**Ejemplo de configuración:**

- Ejecutar linters y tests en cada push.
- Desplegar automáticamente en producción tras aprobar un Pull Request.

---

## Casos de uso CI/CD

En los pipelines CI/CD se pueden automatizar muchas tareas que mejoran la calidad y aceleran la entrega de software. A continuación, casos de uso comunes que conviene conocer:

- Generación automática de release
- Despliegues
- Tests automatizados
- Calidad y seguridad
- Publicación de artefactos
