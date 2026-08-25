# 02. Preparar Visual Studio Code para trabajar con Git y GitHub

En esta sección prepararás Visual Studio Code para trabajar con un proyecto controlado mediante Git. Aprenderás a abrir la carpeta correcta, utilizar la terminal integrada e identificar las herramientas de Git disponibles en el editor.

No modificarás todavía el historial del proyecto ni publicarás archivos en GitHub. El objetivo es reconocer el entorno de trabajo y comprobar que todo está listo.

---

## 1. Abrir Visual Studio Code

Inicia **Visual Studio Code** desde el menú de aplicaciones de tu sistema operativo.

Durante esta sección utilizarás tres partes principales del programa:

- El **Explorador**, para ver los archivos y las carpetas del proyecto.
- La **terminal integrada**, para ejecutar comandos.
- El panel **Source Control**, para consultar los cambios detectados por Git.

---

## 2. Abrir correctamente una carpeta de proyecto

En la barra de menú de Visual Studio Code, selecciona:

**File → Open Folder**

Busca la carpeta de tu proyecto, selecciónala y confirma la apertura. Si Visual Studio Code pregunta si confías en quienes crearon los archivos, responde afirmativamente solo si conoces el origen del proyecto.

Es importante abrir la **carpeta raíz del proyecto**, es decir, la carpeta principal que contiene todos sus archivos y subcarpetas. Por ejemplo, si tu proyecto se llama `mi-proyecto`, debes abrir la carpeta `mi-proyecto` completa.

No abras únicamente un archivo suelto. Si abres solo un archivo, Visual Studio Code no tendrá el contexto completo del proyecto y algunas funciones de Git, búsqueda y navegación podrían no estar disponibles correctamente.

Puedes confirmar el nombre de la carpeta abierta observando la parte superior del Explorador.

---

## 3. Identificar el Explorador de archivos

El panel **Explorer** suele estar en el lado izquierdo de Visual Studio Code. Su icono representa dos archivos y normalmente es el primero de la barra vertical llamada **Activity Bar**.

Si el panel no está visible, puedes abrirlo desde **View → Explorer**. También puedes utilizar estos atajos:

- Windows/Linux: `Ctrl + Shift + E`
- macOS: `Command + Shift + E`

El Explorador muestra la estructura completa del proyecto. Desde allí puedes abrir, crear, renombrar y organizar archivos y carpetas. Antes de trabajar, verifica que muestre la carpeta raíz que seleccionaste en el paso anterior.

---

## 4. Abrir la terminal integrada

En la barra de menú, selecciona:

**Terminal → New Terminal**

La terminal se abrirá normalmente en la parte inferior de Visual Studio Code. También puedes utilizar el atajo:

- Windows/Linux: <kbd>Ctrl</kbd> + <kbd>`</kbd>
- macOS: <kbd>Control</kbd> + <kbd>`</kbd>

La tecla `` ` `` se conoce como **acento grave** o *backtick*. Su ubicación depende de la distribución del teclado.

La terminal integrada permite ejecutar comandos sin salir de Visual Studio Code. Cada vez que abras un proyecto, conviene comprobar que la terminal está ubicada en la carpeta correcta.

---

## 5. Verificar en qué carpeta está ubicada la terminal

La terminal trabaja siempre desde una ubicación concreta del sistema de archivos. Esa ubicación se denomina **directorio de trabajo actual**.

### Linux y macOS

Ejecuta el siguiente comando:

```bash
pwd
```

`pwd` muestra la ruta completa de la carpeta actual. Un resultado correcto podría ser:

```text
/home/estudiante/Documentos/mi-proyecto
```

### Windows

En una terminal de **Símbolo del sistema (Command Prompt)**, ejecuta:

```powershell
cd
```

Un resultado correcto podría ser:

```text
C:\Users\Estudiante\Documents\mi-proyecto
```

Si utilizas PowerShell y `cd` no muestra la ruta, puedes consultarla con:

```powershell
Get-Location
```

En todos los casos, la parte final de la ruta debe coincidir con el nombre de la carpeta raíz del proyecto. Comprobarla evita ejecutar comandos en otro proyecto o modificar archivos por equivocación.

Si la ruta no corresponde al proyecto abierto, cierra esa terminal con el icono de papelera y crea una nueva después de abrir correctamente la carpeta mediante **File → Open Folder**.

---

## 6. Verificar que Git funciona desde VS Code

En la terminal integrada, ejecuta:

```bash
git --version
```

Si Git está instalado y Visual Studio Code puede encontrarlo, aparecerá un resultado similar a este:

```text
git version 2.43.0
```

El número de versión puede ser diferente. Lo importante es que la respuesta comience con `git version` y no muestre un mensaje de comando desconocido.

Si Git no se reconoce, revisa la sección [01. Instalación y configuración de Git](../01-instalacion-y-configuracion/README.md).

---

## 7. Verificar si la carpeta ya es un repositorio Git

Una vez confirmada la ruta, ejecuta:

```bash
git status
```

Este comando consulta el estado del repositorio y no modifica ningún archivo. Pueden ocurrir dos situaciones principales.

### La carpeta ya es un repositorio Git

Git mostrará información sobre la rama actual y los archivos del proyecto. Por ejemplo:

```text
On branch main
nothing to commit, working tree clean
```

Este resultado indica que estás en la rama `main` y que no hay cambios pendientes. Si existen archivos modificados o nuevos, Git los mostrará también; eso es normal.

### La carpeta todavía no es un repositorio Git

Puedes ver un mensaje similar a este:

```text
fatal: not a git repository (or any of the parent directories): .git
```

Este error **no significa que Git esté mal instalado**. Indica que la carpeta actual todavía no se ha inicializado como repositorio Git. La inicialización se explicará en la sección siguiente de la guía.

---

## 8. Identificar el panel Source Control

El icono de **Source Control** o **Control de código fuente** se encuentra en la barra vertical izquierda de Visual Studio Code. Generalmente tiene la forma de una bifurcación con varios círculos conectados.

Puedes abrir el panel seleccionando ese icono o mediante el atajo:

- Windows/Linux: `Ctrl + Shift + G`
- macOS: `Control + Shift + G`

Cuando la carpeta es un repositorio Git, este panel permite:

- Ver los archivos nuevos o modificados.
- Revisar las diferencias entre versiones.
- Preparar cambios para incluirlos en un commit.
- Escribir el mensaje y realizar un commit.

En esta guía trabajarás primero con comandos para comprender qué hace Git en cada paso. Más adelante relacionarás esos mismos comandos con los botones y opciones de la interfaz gráfica de Visual Studio Code.

---

## 9. Verificar extensiones útiles

Para abrir el panel **Extensions**, selecciona el icono de bloques ubicado en la barra lateral izquierda o utiliza:

- Windows/Linux: `Ctrl + Shift + X`
- macOS: `Command + Shift + X`

Visual Studio Code ya incluye integración con Git. Por lo tanto, **no es obligatorio instalar una extensión adicional** para consultar cambios, preparar archivos o realizar commits con las funciones básicas.

Una extensión opcional es **GitHub Pull Requests and Issues**, publicada por GitHub. Permite revisar solicitudes de cambio (*pull requests*) e incidencias (*issues*) desde Visual Studio Code. No es indispensable para seguir esta guía y puedes instalarla más adelante si la necesitas.

Antes de instalar una extensión, comprueba su nombre y quién la publica para evitar instalar imitaciones.

---

## 10. Comprobación final

Confirma cada punto antes de continuar:

- [ ] Tengo Visual Studio Code abierto.
- [ ] Abrí la carpeta raíz de mi proyecto mediante **File → Open Folder**.
- [ ] Puedo abrir la terminal integrada.
- [ ] Sé verificar la ruta actual con `pwd`, `cd` o `Get-Location`, según mi sistema y terminal.
- [ ] Puedo ejecutar `git --version` y ver la versión instalada.
- [ ] Sé ejecutar `git status` e interpretar sus resultados básicos.
- [ ] Identifico el panel **Source Control**.

Si completaste la lista, Visual Studio Code está preparado para comenzar a trabajar con Git.

---

## 11. Tabla resumen

| Comando o acción | Sistema o ubicación | Función |
| --- | --- | --- |
| **File → Open Folder** | Menú de Visual Studio Code | Abre la carpeta raíz de un proyecto. |
| **View → Explorer** | Menú de Visual Studio Code | Muestra el Explorador de archivos. |
| **Terminal → New Terminal** | Menú de Visual Studio Code | Abre una terminal integrada. |
| `pwd` | Linux/macOS | Muestra la ruta del directorio de trabajo actual. |
| `cd` | Símbolo del sistema de Windows | Muestra la ruta del directorio de trabajo actual. |
| `Get-Location` | PowerShell | Muestra la ubicación actual en PowerShell. |
| `git --version` | Todos los sistemas | Comprueba que Git funciona y muestra su versión. |
| `git status` | Todos los sistemas | Muestra el estado del repositorio actual. |
| Icono **Source Control** | Barra lateral de Visual Studio Code | Abre las herramientas gráficas integradas de Git. |
| Icono **Extensions** | Barra lateral de Visual Studio Code | Permite buscar y administrar extensiones. |

Cuando termines esta preparación, podrás continuar con la creación o inicialización de tu primer repositorio Git.
