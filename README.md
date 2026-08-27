# Guía de Git y GitHub con Visual Studio Code

Guía práctica diseñada para estudiantes que necesitan aprender a utilizar **Git** y **GitHub** desde **Visual Studio Code** mediante procedimientos claros y progresivos.

Puede utilizarse:

- Como curso progresivo, siguiendo las secciones en orden.
- Como guía de consulta para recordar un procedimiento.
- Como material de apoyo durante proyectos académicos.
- Como referencia para diagnosticar y solucionar errores frecuentes.

---

## Objetivo de la guía

El objetivo es que el estudiante pueda gestionar proyectos con Git y GitHub desde Visual Studio Code de manera **autónoma, segura y organizada**: registrar cambios, mantener un historial, publicar repositorios, colaborar con otras personas y resolver problemas comunes sin poner en riesgo su trabajo.

---

## ¿A quién está dirigida?

Está pensada especialmente para:

- Estudiantes que nunca han utilizado Git.
- Estudiantes que han utilizado GitHub, pero todavía se confunden con los comandos.
- Estudiantes que trabajan en proyectos individuales.
- Estudiantes que participan en proyectos colaborativos.
- Personas que necesitan una referencia rápida de comandos y errores comunes.

---

## ¿Qué necesitas?

- **Visual Studio Code**.
- **Git** instalado.
- Una cuenta de **GitHub**.
- Conexión a Internet para trabajar con GitHub.
- Conocimientos básicos sobre archivos y carpetas.

No necesitas conocimientos previos de Git. Las primeras secciones explican la instalación y los conceptos fundamentales desde el principio.

---

## Ruta de aprendizaje recomendada

```text
Inicio
  ↓
01. Instalación y configuración
  ↓
02. Preparar Visual Studio Code
  ↓
03. Crear el primer repositorio
  ↓
04. Subir un proyecto existente
  ↓
05. Flujo de trabajo diario
  ↓
06. Clonar repositorios
  ↓
07. Actualizar repositorios
  ↓
08. Source Control en VS Code
  ↓
09. Trabajo colaborativo
  ↓
10. Ramas
  ↓
11. Conflictos
  ↓
12. Errores frecuentes
```

La ruta comienza con la preparación del entorno, continúa con el trabajo individual y termina con colaboración, ramas, conflictos y diagnóstico.

---

## Contenido de la guía

| Sección | Tema | ¿Qué aprenderás? |
| --- | --- | --- |
| 01 | [Instalación y configuración](./01-instalacion-y-configuracion/) | Instalar Git, configurar nombre y correo, y definir `main` como rama inicial. |
| 02 | [Preparar Visual Studio Code](./02-preparar-vscode/) | Abrir correctamente un proyecto, usar la terminal e identificar Source Control. |
| 03 | [Crear el primer repositorio](./03-primer-repositorio/) | Inicializar Git, crear el primer commit y conectar un repositorio con GitHub. |
| 04 | [Subir un proyecto existente](./04-subir-proyecto-existente/) | Revisar, preparar y publicar en GitHub un proyecto que ya existe. |
| 05 | [Flujo de trabajo diario](./05-flujo-trabajo-diario/) | Guardar, preparar, confirmar y subir cambios durante el trabajo habitual. |
| 06 | [Clonar un repositorio](./06-clonar-repositorio/) | Obtener una copia local completa de un repositorio de GitHub. |
| 07 | [Actualizar con `git pull`](./07-actualizar-repositorio/) | Recibir cambios remotos y mantener actualizada la copia local. |
| 08 | [Source Control en VS Code](./08-source-control-vscode/) | Relacionar la interfaz gráfica de Visual Studio Code con comandos Git. |
| 09 | [Trabajo colaborativo](./09-trabajo-colaborativo/) | Coordinar cambios, mantener el proyecto actualizado y colaborar de forma segura. |
| 10 | [Ramas](./10-ramas/) | Crear, publicar e integrar líneas de trabajo separadas. |
| 11 | [Resolver conflictos](./11-conflictos/) | Reconocer conflictos, comparar versiones y completar una resolución. |
| 12 | [Errores frecuentes](./12-errores-frecuentes/) | Diagnosticar mensajes comunes y aplicar soluciones básicas y seguras. |

---

## Si es tu primera vez usando Git

Sigue las secciones desde la **01** y respeta el orden propuesto. Cada capítulo utiliza conceptos explicados anteriormente.

Las primeras cinco secciones contienen los fundamentos necesarios para comenzar:

1. Preparar Git.
2. Preparar Visual Studio Code.
3. Crear y publicar un repositorio.
4. Incorporar un proyecto existente.
5. Repetir correctamente el flujo de trabajo diario.

Practica cada comando en un proyecto de ejemplo y completa la lista de comprobación final de cada sección antes de continuar.

---

## Si ya sabes algo de Git

Utiliza la tabla de contenido para ir directamente al tema que necesites. Cada capítulo funciona también como material autónomo de consulta y contiene explicaciones, comandos, resultados esperados y comprobaciones.

---

## Consulta rápida

> Accesos directos a las tareas más habituales:

- [Flujo de trabajo diario](./05-flujo-trabajo-diario/)
- [Clonar un repositorio](./06-clonar-repositorio/)
- [Actualizar con `git pull`](./07-actualizar-repositorio/)
- [Trabajo colaborativo](./09-trabajo-colaborativo/)
- [Trabajar con ramas](./10-ramas/)
- [Resolver conflictos](./11-conflictos/)
- [Consultar errores frecuentes](./12-errores-frecuentes/)

---

## Los comandos que más utilizarás

| Comando | Función |
| --- | --- |
| `git status` | Muestra la rama y el estado de los archivos. |
| `git add .` | Prepara los cambios revisados de la carpeta actual. |
| `git commit -m "mensaje"` | Registra los cambios preparados en el historial local. |
| `git pull` | Descarga e integra cambios del repositorio remoto. |
| `git push` | Envía los commits locales a GitHub. |
| `git branch` | Muestra las ramas locales. |
| `git switch nombre-rama` | Cambia la rama activa. |
| `git clone URL` | Crea una copia local completa de un repositorio remoto. |

No ejecutes una secuencia de comandos de forma mecánica. Lee siempre el resultado de cada paso.

---

## El ciclo básico de Git

```text
Modificar archivos
       ↓
git status
       ↓
git add .
       ↓
git commit
       ↓
git push
       ↓
GitHub
```

En un proyecto colaborativo, normalmente debes ejecutar `git status` y `git pull` antes de comenzar, con el trabajo local en un estado seguro. Así reduces la posibilidad de trabajar sobre una versión desactualizada.

---

## Tres conceptos que no debes confundir

> **Guardar, confirmar y publicar son acciones diferentes.**

| Acción | Qué hace | Dónde queda la información |
| --- | --- | --- |
| **Guardar con `Ctrl + S`** (`Command + S` en macOS) | Guarda la edición actual del archivo. | En el computador. |
| **`git commit`** | Registra los cambios preparados como un punto del historial. | En el repositorio Git local. |
| **`git push`** | Envía a GitHub los commits locales pendientes. | En el repositorio remoto. |

Guardar un archivo no crea un commit. Crear un commit no lo publica automáticamente. `git push` solo puede enviar commits que ya existen localmente.

---

## Git y GitHub no son lo mismo

- **Git** es una herramienta de control de versiones que funciona localmente y registra el historial del proyecto.
- **GitHub** es una plataforma en línea donde pueden almacenarse, compartirse y revisarse repositorios Git.

Puedes utilizar Git sin GitHub. GitHub añade almacenamiento remoto y herramientas de colaboración.

---

## Terminal e interfaz gráfica

La guía enseña primero los comandos desde la **terminal integrada de Visual Studio Code**. Después relaciona esos comandos con el panel **Source Control**.

Ambas formas trabajan sobre el mismo repositorio. Comprender los comandos permite interpretar mejor los mensajes, saber qué acción ejecuta cada botón y diagnosticar errores cuando la interfaz no ofrece suficiente contexto.

---

## Reglas importantes

- Ejecuta `git status` con frecuencia.
- Lee los mensajes de Git antes de ejecutar otro comando.
- Crea commits pequeños y utiliza mensajes claros.
- Haz `git pull` antes de trabajar en proyectos colaborativos, después de proteger cualquier cambio local.
- Revisa qué archivos estás agregando al área de preparación.
- Utiliza `.gitignore` de acuerdo con la tecnología del proyecto.
- Nunca publiques contraseñas, tokens, claves API ni claves privadas.
- Evita comandos destructivos cuyo efecto no comprendas.
- Verifica el repositorio y la rama en GitHub después de `git push`.

---

## ¿Tienes un error?

> Consulta primero: **[12. Errores frecuentes en Git y GitHub](./12-errores-frecuentes/)**.

Antes de pedir ayuda, ejecuta:

```bash
git status
git branch
git remote -v
```

Conserva el mensaje completo del error y anota qué comando ejecutaste justo antes. Antes de compartir texto o capturas, oculta contraseñas, tokens, claves, correos privados y cualquier otro dato sensible.

---

## Metodología

Cada sección contiene:

- Explicaciones en lenguaje sencillo.
- Comandos y descripción de su función.
- Ejemplos realistas.
- Resultados esperados.
- Errores o situaciones frecuentes.
- Una comprobación final de aprendizaje.

---

## Forma de utilizar la guía en clase

1. Lee el tema completo antes de comenzar.
2. Ejecuta cada procedimiento desde Visual Studio Code.
3. Lee los resultados y verifica que coincidan con lo esperado.
4. Completa la comprobación final del capítulo.
5. Regresa a la guía cuando surjan dudas durante tus proyectos.

Utiliza proyectos de práctica para experimentar y evita probar procedimientos nuevos directamente sobre una entrega importante sin conservar una copia segura.

---

## Tecnologías utilizadas

- Git
- GitHub
- Visual Studio Code

---

## Estado de la guía

Esta es una guía en evolución. Puede actualizarse con nuevos ejemplos, errores frecuentes, mejoras de claridad y procedimientos relacionados con el trabajo académico y colaborativo.

---

## Autoría

Material académico de apoyo para procesos de enseñanza y aprendizaje en programación y desarrollo de software.
