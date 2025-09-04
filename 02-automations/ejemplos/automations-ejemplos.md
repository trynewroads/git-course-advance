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

  .col-container{
    display:flex;
    gap: 2rem;
  }

  .col-container > .col {
    flex: 1
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

<div class="col-container">
  <div class="col">

```
// bad.js
const fs = require("fs");
function readFile(path) {
const data = fs.readFileSync(path, "utf8");
console.log(data);
return data;
}
readFile("./file.txt");
```

  </div>
  <div class="col">

```js
// good.js
const fs = require("fs");
function readFile(path) {
  let data = fs.readFileSync(path, "utf8");
  console.log(data);
  return data;
}
readFile("./file.txt");
```

  </div>
</div>

---

<div class="col-container">
  <div class="col">

```python
# bad.py
import os,sys
def read_file(path, encoding='utf8'):
  data = open(path, 'r', encoding=encoding).read()
  print(data)
  return data
def count_lines(path):
    with open(path,'r') as f:
       return len(f.readlines())
print(read_file('./file.txt')) ; print(count_lines('./file.txt'))
```

  </div>
  <div class="col">

```python
# good.py
import sys
from pathlib import Path


def read_file(path: str, encoding: str = "utf8") -> str:
    data = Path(path).read_text(encoding=encoding)
    print(data)
    return data


def count_lines(path: str) -> int:
    with open(path, "r", encoding="utf8") as f:
        return len(f.readlines())


if __name__ == "__main__":
    print(read_file("./file.txt"))
    print(count_lines("./file.txt"))
```

  </div>
</div>

---

```
feat(fw): añadir función read_file con manejo de encoding
- Añade read_file() usando pathlib y typing.
- Mejora la lectura de ficheros y la tipificación.
```

```
fix(io): corregir lectura de ficheros con encoding
- Evita errores al abrir archivos sin especificar encoding.
- Usa Path.read_text() y cierra correctamente ficheros.
```

```
docs: documentar convención de commits en CONTRIBUTING.md
- Añade ejemplos de Conventional Commits y cómo usar commitlint.
- Incluye sección sobre reescribir commits (amend/rebase).
```

---

```
feat(api): añadir endpoint /users

Añade paginación y validaciones de entrada.

Closes #42
```

```
feat(auth): cambiar token handling

Se modifica el formato del token para mejorar seguridad.

BREAKING CHANGE: el token ahora incluye timestamp, requiere migración.
```
