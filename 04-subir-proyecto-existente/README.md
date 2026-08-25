# 04. Subir un proyecto existente a GitHub

En esta sección aprenderás a publicar en GitHub un proyecto que ya está guardado en tu computador. Todo el trabajo local se realizará desde Visual Studio Code y su terminal integrada.

Antes de comenzar, asegúrate de tener Git configurado y una cuenta de GitHub. Si necesitas repasar algún concepto, consulta las secciones [01. Instalación y configuración de Git](../01-instalacion-y-configuracion/README.md), [02. Preparar Visual Studio Code para trabajar con Git y GitHub](../02-preparar-vscode/README.md) y [03. Crear el primer repositorio con Git y GitHub](../03-primer-repositorio/README.md).

---

## 1. ¿Cuándo necesito este procedimiento?

Este procedimiento se utiliza cuando el proyecto ya existe en tu computador y ahora quieres publicarlo en GitHub. Puede ser, por ejemplo:

- Una página web con HTML, CSS y JavaScript.
- Un proyecto Java o Maven.
- Una aplicación Python.
- Un proyecto React o Node.js.
- Cualquier otra carpeta con archivos de trabajo.

La situación es diferente de comenzar con una carpeta vacía: aquí debes revisar cuidadosamente un proyecto que ya contiene archivos, dependencias y posiblemente configuraciones privadas antes de incorporarlo a Git.

El objetivo será conservar el proyecto local, crear su primer commit si todavía no tiene historial y enviarlo a un repositorio remoto vacío en GitHub.

---

## 2. Abrir correctamente el proyecto en Visual Studio Code

Abre Visual Studio Code y selecciona:

**File → Open Folder**

Busca y abre la **carpeta raíz** del proyecto. Es la carpeta principal que contiene el código y los elementos que identifican el proyecto, como `README.md`, `package.json`, `pom.xml`, `requirements.txt` o sus subcarpetas principales.

Para comprobar que elegiste la carpeta correcta:

1. Observa el nombre mostrado en la parte superior del panel **Explorer**.
2. Revisa que el Explorador muestre todos los archivos y subcarpetas esperados.
3. Confirma que no abriste una carpeta superior con varios proyectos ni una subcarpeta que contenga solo una parte del proyecto.

No abras únicamente un archivo suelto, porque Git debe trabajar con la carpeta completa.

---

## 3. Abrir la terminal integrada

En la barra de menú selecciona:

**Terminal → New Terminal**

La terminal aparecerá normalmente en la parte inferior de Visual Studio Code. Debe quedar ubicada dentro de la carpeta raíz que acabas de abrir.

No ejecutes todavía comandos que cambien el proyecto. Primero verifica la ruta y si Git ya está inicializado.

---

## 4. Verificar la ubicación actual

### Linux y macOS

Ejecuta:

```bash
pwd
```

### Windows PowerShell

Ejecuta:

```powershell
Get-Location
```

Ambos comandos muestran la ruta de la carpeta actual. Un resultado podría ser:

```text
/home/estudiante/Documentos/mi-proyecto
```

o, en Windows:

```text
C:\Users\Estudiante\Documents\mi-proyecto
```

La parte final de la ruta debe coincidir con la carpeta raíz del proyecto. Esta comprobación evita inicializar Git o preparar archivos en una ubicación equivocada.

---

## 5. Verificar si el proyecto ya tiene Git

Ejecuta el siguiente comando, que solo consulta el estado:

```bash
git status
```

Pueden presentarse dos escenarios.

### A. Git ya está inicializado

Si aparece información sobre una rama, archivos modificados o el estado del directorio de trabajo, la carpeta ya es un repositorio Git. Por ejemplo:

```text
On branch main
nothing to commit, working tree clean
```

En este caso, **no es necesario ejecutar `git init` otra vez**. Continúa revisando la rama, los archivos y los remotos existentes.

### B. Git todavía no está inicializado

Si aparece un mensaje similar a este:

```text
fatal: not a git repository (or any of the parent directories): .git
```

Git funciona, pero no encuentra un repositorio en la carpeta actual. Después de confirmar que la ruta es correcta, deberás inicializarlo en el paso siguiente.

No ejecutes `git init` innecesariamente cuando el proyecto ya sea un repositorio. El estado existente podría pertenecer a un flujo de trabajo o a una conexión remota que debes revisar y conservar.

---

## 6. Inicializar Git si es necesario

Realiza este paso solamente si `git status` confirmó que la carpeta no es un repositorio.

```bash
git init
```

`git init` crea dentro del proyecto una carpeta oculta llamada `.git`, donde Git almacenará el historial y la configuración local. No elimina ni reemplaza los archivos del proyecto.

Comprueba el resultado:

```bash
git status
```

Ahora Git debe mostrar la rama actual y una lista de archivos sin seguimiento. No elimines ni modifiques manualmente la carpeta `.git`.

---

## 7. Verificar o configurar la rama principal

Consulta las ramas locales con:

```bash
git branch
```

El asterisco `*` identifica la rama actual. Sin embargo, si el repositorio todavía no tiene ningún commit, es posible que este comando no muestre información útil.

También puedes consultar directamente el nombre previsto para la rama actual:

```bash
git branch --show-current
```

Si necesitas llamar `main` a la rama principal, ejecuta:

```bash
git branch -m main
```

La opción `-m` cambia el nombre de la rama actual. Si el proyecto ya tenía commits y utiliza otra rama de forma intencional, revisa su organización antes de renombrarla.

---

## 8. Revisar los archivos antes de agregarlos

Antes de preparar un commit, revisa qué archivos detecta Git:

```bash
git status
```

Git puede agruparlos de distintas maneras:

- **Archivos sin seguimiento (*untracked*):** existen en el proyecto, pero Git todavía no los controla.
- **Archivos modificados (*modified*):** Git ya los conoce, pero su contenido cambió desde el último commit.
- **Archivos ignorados (*ignored*):** coinciden con reglas de exclusión y normalmente no aparecen en la salida habitual de `git status`.

Si necesitas comprobar los archivos ignorados, puedes usar temporalmente:

```bash
git status --ignored
```

Revisa los nombres antes de ejecutar `git add .`. No todo lo que funciona en tu computador debe almacenarse en GitHub: las dependencias descargadas, archivos temporales, entornos locales y credenciales suelen quedar fuera del repositorio.

---

## 9. Introducción a `.gitignore`

`.gitignore` es un archivo de texto que indica a Git qué archivos o carpetas sin seguimiento debe ignorar. Conviene crearlo o revisarlo **antes** de agregar los archivos al área de preparación.

Las reglas de `.gitignore` se aplican principalmente a archivos que Git todavía no sigue. Si un archivo ya estaba incluido en commits anteriores, agregarlo a `.gitignore` no hace que Git deje de controlarlo.

Algunos ejemplos habituales son:

### Node.js

```gitignore
node_modules/
.env
```

`node_modules/` contiene dependencias que normalmente pueden volver a instalarse. Un archivo `.env` suele contener configuraciones locales o secretos.

### Java y Maven

```gitignore
target/
```

`target/` suele contener archivos generados durante la compilación.

### Python

```gitignore
__pycache__/
.venv/
venv/
```

Estas carpetas contienen caché o entornos virtuales que normalmente no deben compartirse como parte del código fuente.

### Visual Studio Code

```gitignore
.vscode/
```

No siempre es necesario ignorar `.vscode/`: algunas configuraciones del proyecto pueden ser útiles para el equipo. Para principiantes, conviene revisar su contenido antes de publicarlo y excluirlo si contiene ajustes personales, rutas locales o información que no debe compartirse.

> **Advertencia de seguridad:** nunca publiques contraseñas, tokens, claves API, claves privadas ni archivos `.env` que contengan secretos. `.gitignore` ayuda a prevenir su inclusión, pero debes revisar igualmente los archivos preparados. Si un secreto ya fue incluido en un commit, agregarlo después a `.gitignore` no lo elimina del historial; considera ese secreto expuesto y reemplázalo desde el servicio que lo emitió.

---

## 10. Crear un archivo `.gitignore`

Desde el panel **Explorer** de Visual Studio Code:

1. Selecciona **New File** en la carpeta raíz.
2. Escribe exactamente `.gitignore` y presiona `Enter`.
3. Agrega únicamente las reglas adecuadas para tu proyecto.
4. Guarda el archivo.

Por ejemplo, un proyecto de Node.js podría comenzar con:

```gitignore
# Dependencias instaladas
node_modules/

# Variables locales y secretos
.env

# Archivos de registro
*.log
```

Cada línea representa un patrón que Git debe ignorar y las líneas que comienzan con `#` son comentarios. El contenido correcto depende de la tecnología, las herramientas y las necesidades del proyecto; no copies reglas sin entender qué excluyen.

Después de guardarlo, ejecuta `git status` y confirma que los elementos ignorados no estén en la lista de archivos que se agregarán.

---

## 11. Agregar los archivos al área de preparación

Cuando hayas revisado el proyecto y `.gitignore`, prepara los cambios con:

```bash
git add .
```

El punto `.` representa la carpeta actual. En este comando, Git agrega al área de preparación los cambios del proyecto. Los archivos nuevos que coincidan con `.gitignore` se omiten, pero los archivos que Git ya seguía pueden prepararse aunque después se agregue una regla para ignorarlos.

Este paso no crea un commit ni sube información a GitHub. Revisa exactamente qué quedó preparado:

```bash
git status
```

Los archivos que formarán parte del commit deben aparecer bajo **Changes to be committed** o **Cambios a ser confirmados**. Lee la lista completa y confirma que no incluya dependencias, archivos temporales o información privada.

Si detectas un archivo que no debe incluirse, no continúes con el commit. Abre el panel **Source Control**, ubica el archivo bajo **Staged Changes** y selecciona **Unstage Changes** mediante el botón `−` o el menú contextual. Esta acción lo retira del área de preparación sin borrar el archivo del computador.

Si era un archivo nuevo, agrega después la regla apropiada a `.gitignore` y revisa otra vez con `git status`. Si Git ya lo seguía desde un commit anterior, solicita orientación antes de publicarlo: ignorarlo requiere un paso adicional y, si contenía secretos, también debes reemplazar esas credenciales.

---

## 12. Crear el primer commit del proyecto

Cuando la lista preparada sea correcta, crea un commit:

```bash
git commit -m "Agregar proyecto inicial"
```

Un commit es un punto de guardado dentro del historial de Git. El mensaje debe describir claramente el estado o los cambios guardados. En este caso, `Agregar proyecto inicial` indica que se registra la versión existente del proyecto.

Git mostrará un resumen de los archivos incluidos. Si indica que falta configurar el nombre o el correo, completa la configuración de la sección 01 antes de intentarlo nuevamente.

---

## 13. Crear el repositorio remoto en GitHub

Entra en [GitHub](https://github.com/), inicia sesión y sigue estos pasos:

1. Selecciona **New repository**.
2. Usa preferiblemente el mismo nombre de la carpeta del proyecto.
3. Elige **Public** si cualquiera puede ver el contenido o **Private** si el acceso debe estar restringido.
4. No actives **Add a README file** si el proyecto local ya tiene contenido.
5. No agregues un `.gitignore` desde GitHub si ya lo creaste localmente.
6. No agregues una licencia en este momento, salvo que sepas cuál necesita el proyecto.
7. Selecciona **Create repository**.

El repositorio remoto debe quedar vacío. Esto evita comenzar con un commit diferente al historial que ya creaste localmente.

---

## 14. Conectar el proyecto local con GitHub

En la página del repositorio vacío, selecciona la opción **HTTPS** y copia la URL. Luego ejecuta en la terminal integrada, reemplazando el ejemplo por tu URL:

```bash
git remote add origin https://github.com/usuario/nombre-repositorio.git
```

Un **remote** es una referencia a un repositorio externo. `origin` es el nombre corto utilizado por convención para identificar el repositorio remoto principal; no es el nombre de una rama ni una carpeta.

El comando configura la conexión, pero todavía no sube los archivos.

---

## 15. Verificar el *remote*

Comprueba la configuración con:

```bash
git remote -v
```

El resultado debe incluir dos líneas parecidas a estas:

```text
origin  https://github.com/usuario/nombre-repositorio.git (fetch)
origin  https://github.com/usuario/nombre-repositorio.git (push)
```

Verifica cuidadosamente el usuario, el nombre del repositorio y la URL. `fetch` señala desde dónde se reciben cambios y `push` hacia dónde se envían.

---

## 16. Subir el proyecto

Asegúrate de que la rama se llame `main` y realiza el primer envío:

```bash
git push -u origin main
```

Cada parte cumple una función:

- `push` envía los commits locales al repositorio remoto.
- `-u` vincula la rama local con la rama remota para simplificar los envíos posteriores.
- `origin` identifica el repositorio remoto configurado.
- `main` es la rama que se enviará.

GitHub puede solicitar que inicies sesión o autorices la operación en el navegador. Sigue las indicaciones mostradas y no compartas credenciales ni códigos de acceso.

Después de este primer envío, normalmente podrás utilizar:

```bash
git push
```

Git recordará el remoto y la rama vinculados por medio de `-u`.

---

## 17. Verificar el resultado en GitHub

Actualiza la página del repositorio en el navegador y confirma que:

- Aparecen las carpetas esperadas.
- Aparecen los archivos de código y configuración que sí deben compartirse.
- Aparece `README.md`, si el proyecto lo contiene.
- No aparecen las carpetas ni los archivos excluidos mediante `.gitignore`.
- No aparecen contraseñas, tokens, claves API, archivos `.env` con secretos ni otras credenciales.

Abre algunos archivos desde GitHub para comprobar su contenido. Si descubres un secreto publicado, no basta con borrar el archivo en un commit posterior: reemplaza o revoca inmediatamente la credencial en el servicio correspondiente y solicita ayuda para limpiar el historial de forma segura.

---

## 18. ¿Qué pasa si el repositorio remoto no está vacío?

Si al crear el repositorio en GitHub agregaste un README, `.gitignore` o licencia, GitHub habrá creado un commit remoto. Como ese commit no forma parte del historial local, el primer `push` puede ser rechazado para evitar que se sobrescriba trabajo.

La forma más sencilla de prevenir este escenario es crear el repositorio remoto vacío cuando el proyecto y su historial ya existen localmente.

Si el remoto ya contiene archivos importantes, detente y revisa ambos historiales antes de continuar. La integración correcta depende de si necesitas conservar el contenido local, el remoto o ambos. No elimines archivos ni reemplaces el historial para intentar resolverlo rápidamente.

> **Advertencia:** no utilices `push --force` ni otras variantes de envío forzado sin comprender completamente sus consecuencias. Pueden sobrescribir commits remotos y provocar pérdida de trabajo.

---

## 19. Errores frecuentes

### `fatal: not a git repository`

**Qué significa:** Git no encuentra un repositorio en la carpeta actual ni en sus carpetas superiores.

**Causa probable:** La terminal está fuera del proyecto o la carpeta todavía no fue inicializada.

**Solución básica y segura:** Verifica la ruta con `pwd` o `Get-Location`. Entra en la carpeta raíz correcta y ejecuta `git status`. Utiliza `git init` solo si confirmaste que el proyecto aún no es un repositorio.

### `remote origin already exists`

**Qué significa:** El repositorio local ya tiene un remoto llamado `origin`.

**Causa probable:** La conexión se configuró antes o el proyecto ya estaba vinculado con otro repositorio.

**Solución básica y segura:** No agregues otro remoto con el mismo nombre. Inspecciona primero la URL:

```bash
git remote -v
```

Si confirmas que es incorrecta, reemplázala por la URL correcta:

```bash
git remote set-url origin https://github.com/usuario/nombre-repositorio.git
```

### `nothing to commit, working tree clean`

**Qué significa:** Git no detecta cambios nuevos para guardar.

**Causa probable:** Los archivos ya están incluidos en el último commit, no se guardaron cambios nuevos o todo lo nuevo está correctamente ignorado.

**Solución básica y segura:** Si esperabas cambios, guarda los archivos en Visual Studio Code y revisa `git status` y `.gitignore`. Si no esperabas cambios, no hay ningún problema: el repositorio está limpio.

### `rejected` o `failed to push some refs`

**Qué significa:** GitHub rechazó el envío para proteger el historial remoto.

**Causa probable:** El repositorio remoto contiene commits que no están en el repositorio local, por ejemplo un README creado desde GitHub.

**Solución básica y segura:** No fuerces el envío. Revisa la página de GitHub, confirma qué archivos y commits existen en ambos lados y conserva una copia de tu trabajo. Si necesitas ambos historiales, solicita orientación para integrarlos correctamente antes de volver a ejecutar `push`.

### `src refspec main does not match any`

**Qué significa:** Git no encuentra una rama local `main` con commits para enviar.

**Causa probable:** Todavía no existe el primer commit o la rama actual tiene otro nombre.

**Solución básica y segura:** Consulta el estado y la rama:

```bash
git status
git branch --show-current
```

Si no existe un commit, revisa los archivos, ejecuta `git add .` y crea el commit. Si la rama debe llamarse `main`, renómbrala con `git branch -m main` y vuelve a comprobarla antes del `push`.

---

## 20. Flujo resumido

```text
Proyecto ya creado
        ↓
Abrir carpeta en VS Code
        ↓
git status
        ↓
git init (solo si hace falta)
        ↓
Crear o revisar .gitignore
        ↓
git add .
        ↓
git commit
        ↓
Crear repositorio vacío en GitHub
        ↓
git remote add origin
        ↓
git push -u origin main
```

La revisión de archivos y secretos debe realizarse antes de `git add .`, nuevamente antes del commit y después de publicar el proyecto.

---

## 21. Tabla resumen de comandos

| Comando | Sistema | Función |
| --- | --- | --- |
| `pwd` | Linux/macOS | Muestra la ruta de la carpeta actual. |
| `Get-Location` | Windows PowerShell | Muestra la ruta de la carpeta actual. |
| `git status` | Todos | Muestra la rama y el estado de los archivos. |
| `git init` | Todos | Inicializa Git en la carpeta actual, si es necesario. |
| `git branch` | Todos | Muestra las ramas locales con commits. |
| `git branch -m main` | Todos | Renombra la rama actual como `main`. |
| `git add .` | Todos | Prepara los cambios no ignorados de la carpeta actual. |
| `git commit -m "Agregar proyecto inicial"` | Todos | Crea un commit con los cambios preparados. |
| `git remote add origin URL` | Todos | Agrega la conexión con el repositorio remoto. |
| `git remote -v` | Todos | Muestra los remotos y sus URL. |
| `git push -u origin main` | Todos | Envía `main` por primera vez y establece su vínculo remoto. |
| `git push` | Todos | Envía commits posteriores al remoto vinculado. |

---

## 22. Comprobación final

Antes de terminar, confirma cada punto:

- [ ] Abrí la carpeta raíz correcta en Visual Studio Code.
- [ ] Verifiqué si Git ya estaba inicializado antes de usar `git init`.
- [ ] Revisé o creé `.gitignore` según la tecnología del proyecto.
- [ ] Confirmé que no estoy publicando contraseñas, tokens, claves ni otros secretos.
- [ ] Agregué al área de preparación solamente los archivos correctos.
- [ ] Creé el commit inicial del proyecto.
- [ ] Creé un repositorio remoto vacío en GitHub.
- [ ] Conecté correctamente el remoto `origin`.
- [ ] Realicé el primer `push` de la rama `main`.
- [ ] Verifiqué los archivos y su contenido en GitHub.

Si completaste la lista, tu proyecto existente ya está almacenado en un repositorio Git y publicado de forma segura en GitHub.
