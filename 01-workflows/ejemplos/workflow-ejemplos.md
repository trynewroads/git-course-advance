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

  .col-container {
    gap: 2rem;
    display: flex
  }

  .col {
    flex: 1
  }

  .col-container > div {
    place-content: center;
  }

  .col-container > div > img {
    max-width: 250px;
    height: auto;
    max-height: 420px;
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

<div class="col-container">
    <div>
        <img src="../../img/workflow-trunk.png" alt="Trunk Based Development"/>
    </div>
  <div class="col">
    <a href="https://learngitbranching.js.org/?NODEMO=&command=git%20switch%20-c%20f%2Fsearch%3Bgit%20commit%3Bgit%20commit%3Bgit%20switch%20-c%20f%2Flogin%3Bgit%20commit%3Bgit%20commit%3Bgit%20switch%20main%3Bgit%20merge%20f%2Fsearch%3Bgit%20switch%20f%2Flogin%3Bgit%20commit%3Bgit%20commit%3Bgit%20switch%20main%3Bgit%20merge%20f%2Flogin&locale=es_ES">Ver diagrama en LearnGitBranching</a>
    <br><br>
    <p> En este diagrama se observa cómo varios desarrolladores crean ramas de características (<code>feature1</code>, <code>feature2</code>, <code>feature3</code>) desde la rama principal (<code>main</code>).         Cada rama contiene varios commits y se desarrollan en paralelo. Cuando las funcionalidades están listas, se fusionan rápidamente a <code>main</code>, manteniendo el código siempre actualizado y listo para producción.
    
  </div>
</div>

---

<div class="col-container">
    <div class="col">    
        <pre><code>
        git switch -c feature1
        git commit
        git commit
        git switch main
        git switch -c feature2
        git commit
        git commit
        git commit
        git switch main
        git merge feature1
        git switch -c feature3
        </code></pre>
    </div>
    <div class="col">    
        <pre><code>
        git commit
        git commit
        git switch feature2
        git commit
        git switch main
        git merge feature2
        git switch feature3
        git merge feature3
        git commit
        git switch main
        git merge feature3
        </code></pre>
    </div>
</div>
    
---

## Feature Branch Workflow

<div class="col-container">
    <div>
        <img src="../../img/workflow-branch.png" alt="Feature Branch Workflow" />
    </div>
    <div class="col">
        <a href="https://learngitbranching.js.org/?NODEMO=&command=git%20switch%20-c%20f%2Flogin%3Bgit%20commit%3Bgit%20commit%3Bgit%20switch%20main%3Bgit%20merge%20f%2Flogin&locale=es_ES">Ver diagrama en LearnGitBranching</a>
        <br><br>
        <p>
        En este diagrama se muestra cómo cada nueva funcionalidad se desarrolla en una rama independiente (<code>login</code>) creada desde la rama principal (<code>main</code>).  
        Los desarrolladores realizan varios commits en la rama de la funcionalidad.  
        Cuando la funcionalidad está lista, se fusiona a <code>main</code> mediante un merge (normalmente a través de un Pull Request), permitiendo revisiones y control de calidad antes de integrar los cambios.
        </p>
    </div>
</div>

---

```
git switch -c f/login
git commit
git commit
git switch main
git merge f/login
```

---

## Forking Workflow

<div class="col-container">
    <div>
        <img src="../../img/workflow-fork.png" alt="Forking Workflow" />
    </div>
    <div class="col">
        <a href="https://learngitbranching.js.org/?NODEMO=&command=git%20clone%3Bgit%20switch%20-c%20feat%3Bgit%20commit%3Bgit%20commit%3Bgit%20commit%3Bgit%20push%3Bgit%20fakeTeamwork%3Bgit%20mergeMR%20feat%20main&locale==es_ES">Ver diagrama en LearnGitBranching</a>
        <br><br>
        <p>
        En este diagrama se observa cómo un colaborador realiza un <strong>fork</strong> (copia) del repositorio principal.  
        El desarrollo se realiza en el fork, normalmente en una rama de característica (<code>feat</code>).  
        Cuando los cambios están listos, se propone una integración al repositorio original mediante un Pull Request, permitiendo revisiones y control antes de fusionar los cambios.
        </p>
    </div>
</div>

---

## Git Flow Workflow

<div class="col-container">
    <div>
        <img src="../../img/workflow-gitflow.png" alt="Git Flow Workflow" />
    </div>
    <div class="col">
        <a href="https://learngitbranching.js.org/?NODEMO=&command=git%20switch%20-c%20develop%3Bgit%20switch%20-c%20f%2Flogin%3Bgit%20commit%3Bgit%20switch%20develop%3Bgit%20switch%20-c%20f%2Fsearch%3Bgit%20commit%3Bgit%20commit%3Bgit%20switch%20f%2Flogin%3Bgit%20commit%3Bgit%20commit%3Bgit%20switch%20develop%3Bgit%20merge%20f%2Flogin%3Bgit%20switch%20-c%20r%2F1.0%3Bgit%20commit%3Bgit%20switch%20main%3Bgit%20merge%20r%2F1.0%3Bgit%20switch%20-c%20h%2Furgent%3Bgit%20commit%3Bgit%20commit%3Bgit%20switch%20main%3Bgit%20merge%20h%2Furgent%3Bgit%20switch%20develop%3Bgit%20merge%20h%2Furgent&locale=es_ES">Ver diagrama en LearnGitBranching</a>
        <br><br>
        <p>
        En este diagrama se observa el flujo clásico de <strong>Git Flow</strong>:  
        Se crea una rama <code>develop</code> para integrar nuevas funcionalidades.  
        Las ramas de características (<code>f/login</code>, <code>f/search</code>) se desarrollan desde <code>develop</code> y se fusionan de vuelta.  
        Cuando se prepara un lanzamiento, se crea una rama <code>r/1.0</code> desde <code>develop</code> y se fusiona a <code>main</code>.  
        Las correcciones urgentes (<code>h/urgent</code>) se desarrollan desde <code>main</code> y se fusionan tanto a <code>main</code> como a <code>develop</code>.
        </p>
    </div>

---

## GitHub Flow

<div class="col-container">
    <div>
        <img src="../../img/workflow-github-flow.png" alt="GitHub Flow" />
    </div>
    <div class="col">
        <a href="https://learngitbranching.js.org/?NODEMO=&command=git%20branch%20f%2Flogin%3Bgit%20switch%20-c%20f%2Fsearch%3Bgit%20commit%3Bgit%20commit%3Bgit%20switch%20f%2Flogin%3Bgit%20commit%3Bgit%20commit%3Bgit%20commit%3Bgit%20switch%20main%3Bgit%20merge%20f%2Fsearch%3Bgit%20switch%20f%2Flogin%3Bgit%20commit%3Bgit%20commit%3Bgit%20switch%20main%3Bgit%20merge%20f%2Flogin&locale=es_ES">Ver diagrama en LearnGitBranching</a>
        <br><br>
        <p>
        En este diagrama se muestra el flujo <strong>GitHub Flow</strong>:  
        Cada nueva funcionalidad o corrección se desarrolla en una rama corta (<code>f/search</code>, <code>f/login</code>) creada desde <code>main</code>.  
        Cuando los cambios están listos, se integran a <code>main</code> mediante un Pull Request, permitiendo revisiones y despliegues frecuentes.  
        Este workflow es ideal para integración y entrega continua.
        </p>
    </div>
