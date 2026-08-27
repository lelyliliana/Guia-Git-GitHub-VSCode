# Glosario de Git, GitHub y Visual Studio Code

Este glosario reúne los términos principales de la guía en orden alfabético y con definiciones breves para estudiantes principiantes.

---

## `.git`

Carpeta oculta donde Git almacena el historial y la configuración local de un repositorio. Se crea normalmente con `git init` o al clonar.

No debe borrarse ni modificarse manualmente.

## `.gitignore`

Archivo de texto que contiene reglas para indicar qué archivos nuevos no debe controlar Git, como dependencias, cachés o configuraciones privadas.

No elimina del historial archivos que Git ya controlaba.

## Branch

Una *branch* o rama es una línea de trabajo separada dentro del repositorio. Permite desarrollar una tarea sin modificar inmediatamente la rama principal.

Se consulta con `git branch`.

## Clone

Es una copia local completa de un repositorio remoto, incluidos sus archivos, historial y conexión `origin`.

Se crea con `git clone URL` y no equivale a descargar un ZIP.

## Commit

Es un registro de cambios guardado en el historial local de Git. Puede entenderse como un “punto de guardado” del proyecto.

```bash
git commit -m "Agregar formulario"
```

## Conflict

Un conflicto ocurre cuando Git no puede combinar automáticamente dos cambios incompatibles. Una persona debe comparar las versiones y decidir el resultado final.

No significa que el proyecto se haya perdido.

## Current Change

En una resolución de conflictos, representa normalmente el contenido de la rama actualmente activa.

Debe compararse con **Incoming Change** antes de elegir qué conservar.

## Fetch

Operación que descarga información y commits remotos sin integrarlos inmediatamente en la rama local actual.

Se ejecuta con `git fetch`.

## Git

Sistema de control de versiones que registra cambios e historial en un repositorio. Funciona localmente en el computador y puede utilizarse sin GitHub.

## GitHub

Plataforma en línea para almacenar, compartir y colaborar en repositorios Git. GitHub utiliza Git, pero no son la misma herramienta.

## Incoming Change

En una resolución de conflictos, representa normalmente el contenido que llega desde la rama o versión que se intenta integrar.

No debe aceptarse automáticamente sin revisar la versión actual.

## Local

Describe archivos, ramas, commits o repositorios que están en tu computador.

Un commit local no aparece en GitHub hasta que se publica mediante `git push`.

## Main

Nombre utilizado habitualmente para la rama principal del proyecto. Contiene normalmente la versión estable o integrada.

El nombre puede variar según el repositorio.

## Merge

Operación que integra los commits de una rama en la rama activa. Puede completarse automáticamente o producir conflictos.

```bash
git merge nombre-rama
```

## Origin

Nombre que Git utiliza normalmente para identificar el repositorio remoto principal.

Puede verificarse con:

```bash
git remote -v
```

## Pull

Operación que descarga cambios remotos e intenta integrarlos en la rama local actual.

Se ejecuta con `git pull` y mueve información desde GitHub hacia el computador.

## Push

Operación que envía commits locales a un repositorio remoto como GitHub.

Se ejecuta con `git push`; no envía cambios que todavía no formen parte de un commit.

## Remote

Referencia local a un repositorio ubicado en otro lugar, normalmente en GitHub. Cada remoto tiene un nombre y una URL.

`origin` suele ser el remoto principal.

## Repository

Carpeta de proyecto administrada por Git, con archivos de trabajo y un historial de cambios. Puede existir localmente y tener una copia remota.

También se utiliza la palabra **repositorio**.

## Source Control

Panel de Visual Studio Code que presenta una interfaz gráfica para Git. Permite revisar cambios, preparar archivos, crear commits y acceder a operaciones como Pull y Push.

La interfaz y la terminal trabajan sobre el mismo repositorio.

## Stage

Acción de preparar un cambio para incluirlo en el próximo commit.

```bash
git add nombre-archivo
```

## Staged Changes

Sección de Source Control que muestra los cambios ya preparados para el próximo commit.

Todavía son locales y no se han publicado necesariamente en GitHub.

## Staging Area

Área temporal donde Git mantiene la versión de los cambios seleccionados para el próximo commit.

`git add` incorpora cambios al *staging area* y `git commit` registra lo preparado.

## Status

Estado actual del repositorio: rama activa, cambios preparados, no preparados, archivos nuevos y posibles conflictos.

Se consulta de forma segura con `git status`.

## Switch

Operación para cambiar la rama activa. Con la opción `-c`, también puede crear una rama nueva.

```bash
git switch nombre-rama
```

## Terminal

Interfaz de texto donde se escriben comandos. Visual Studio Code incluye una terminal integrada accesible desde **Terminal → New Terminal**.

## Tracked file

Archivo con seguimiento: Git ya lo conoce porque se agregó previamente al repositorio.

Sus modificaciones aparecen normalmente en `git status`.

## Untracked file

Archivo sin seguimiento: existe en la carpeta, pero Git todavía no lo controla.

Puede prepararse con `git add archivo` o ignorarse mediante una regla adecuada.

## Visual Studio Code

Editor de código que incluye terminal integrada y herramientas visuales de Source Control. Permite trabajar con Git mediante comandos y botones.

## Working Directory

Carpeta desde la cual se ejecutan los comandos en la terminal. También se llama directorio de trabajo actual.

Su ruta puede consultarse con `pwd` en Linux/macOS o `Get-Location` en PowerShell.

## Working Tree

Conjunto de archivos visibles del proyecto en su estado actual. Puede contener modificaciones respecto del último commit.

El mensaje `working tree clean` indica que no existen cambios locales pendientes respecto del commit actual.

---

## Términos que suelen confundirse

### Git vs. GitHub

- **Git:** herramienta local de control de versiones.
- **GitHub:** plataforma en línea que aloja y comparte repositorios Git.

### Guardar vs. Commit vs. Push

- **Guardar:** escribe el archivo en el computador.
- **Commit:** registra cambios preparados en el historial local.
- **Push:** envía commits locales al remoto.

### Pull vs. Push

- **Pull:** trae e integra cambios desde el remoto hacia el computador.
- **Push:** envía commits desde el computador hacia el remoto.

### Clone vs. Download ZIP

- **Clone:** incluye archivos, historial Git y conexión remota.
- **Download ZIP:** descarga solamente una copia de los archivos.

### Local vs. Remote

- **Local:** existe en tu computador.
- **Remote:** está referenciado en otro lugar, como GitHub.

### Branch vs. Main

- **Branch:** cualquier línea de trabajo del repositorio.
- **Main:** nombre habitual de la rama principal; también es una branch.

### Stage vs. Commit

- **Stage:** selecciona los cambios que se incluirán.
- **Commit:** registra en el historial los cambios preparados.

---

Material elaborado por **Leli Liliana** como recurso académico de apoyo.
