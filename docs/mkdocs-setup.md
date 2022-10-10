# MkDocs

## Introduction
MkDocs is static site generator.

The content can be writen and edited in any text editor in markdown language. When changes are pushed to repository, building action is automaticly triggered and the static website generated.

<!-- TODO add git hooks, autobuild etc -->
``` mermaid
flowchart LR
A(content in markdown) --> B(MkDocs) --> C(static website)
```

Every time there is a push to master branch it triggers the build flow
``` mermaid
gitGraph
       commit
       commit
       branch develop
       checkout develop
       commit
       commit
       checkout main
       merge develop
       commit
       commit
```
the built documentation can ba also previed loccaly with
```bash
mkdocs serve
```

## Building from scratch

Create a new repository at github where we deploy the documentation, recommended setup: 
- gitignore for python
- MIT licence
- add README.md

Once created, clone localy on your machine.

create requirments.txt (not esential but good practise) with one line mkdocs-material
```bash
"mkdocs-material" > requirments.txt
```
create enviroment (list of comannds below can be put into one script)
```bash
export _VERSION_=3.8
conda create --prefix ./env python=${_VERSION_} -y
source activate ./env
pip install -r requirements.txt
```
After the installation you can create the site:
```bash
mkdocs new .
```
the nactivate the enviroment:
```bash
conda activate ./env
```

More info how to getting started at [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/getting-started/)


## Commands

* `mkdocs new [dir-name]` - Create a new project.
* `mkdocs serve` - Start the live-reloading docs server.
* `mkdocs build` - Build the documentation site.
* `mkdocs -h` - Print help message and exit.
