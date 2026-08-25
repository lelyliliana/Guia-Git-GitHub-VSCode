# 03. Crear el primer repositorio con Git y GitHub

En esta sección crearás un repositorio local desde Visual Studio Code, guardarás su primera versión con Git y publicarás el proyecto en GitHub.

Antes de comenzar, comprueba que Git esté instalado y configurado, y que tengas una cuenta de GitHub. Si necesitas ayuda, consulta las secciones [01. Instalación y configuración de Git](../01-instalacion-y-configuracion/README.md) y [02. Preparar Visual Studio Code para trabajar con Git y GitHub](../02-preparar-vscode/README.md).

---

## 1. ¿Qué vamos a hacer?

El proceso tendrá cinco objetivos principales:

1. Crear una carpeta para el proyecto y abrirla en Visual Studio Code.
2. Inicializar un repositorio Git dentro de esa carpeta.
3. Crear un archivo `README.md` y guardar el primer commit.
4. Crear un repositorio vacío en GitHub.
5. Conectar el repositorio local con GitHub y subir los archivos.

El **repositorio local** estará en tu computador. El **repositorio remoto** estará en GitHub. Al final, ambos contendrán el mismo primer commit.

---

## 2. Crear una carpeta para el proyecto

Puedes crear una carpeta llamada `mi-primer-repositorio` desde el explorador de archivos de tu sistema operativo o mediante la terminal.

### Linux y macOS

Abre una terminal en la ubicación donde quieras guardar el proyecto y ejecuta:

```bash
mkdir mi-primer-repositorio
cd mi-primer-repositorio
```

### Windows PowerShell

En PowerShell puedes utilizar los mismos comandos:

```powershell
mkdir mi-primer-repositorio
cd mi-primer-repositorio
```

`mkdir` crea la carpeta y `cd` entra en ella. Los comandos no muestran necesariamente un mensaje cuando funcionan correctamente.

Después, abre Visual Studio Code y selecciona:

**File → Open Folder**

Elige la carpeta `mi-primer-repositorio`. Asegúrate de abrir la carpeta completa y no solamente un archivo suelto.

---

## 3. Crear un archivo `README.md`

Un archivo `README.md` presenta el proyecto. Normalmente explica su propósito, sus requisitos y la forma de utilizarlo. La extensión `.md` indica que utiliza Markdown, un formato de texto sencillo.

La forma más directa de crearlo en Visual Studio Code es:

1. Abre el panel **Explorer**.
2. Selecciona el botón **New File**.
3. Escribe `README.md` y presiona `Enter`.
4. Agrega un título, por ejemplo:

```text
# Mi primer repositorio
```

5. Guarda el archivo con `Ctrl + S` en Windows/Linux o `Command + S` en macOS.

También puedes crear el archivo vacío desde la terminal.

### Linux y macOS

```bash
touch README.md
```

### Windows PowerShell

```powershell
New-Item README.md
```

Después de utilizar la terminal, abre `README.md` desde el Explorador, agrega el título y guarda el archivo.

---

## 4. Inicializar Git

En la terminal integrada de Visual Studio Code, verifica que estés dentro de `mi-primer-repositorio` y ejecuta:

```bash
git init
```

`git init` convierte la carpeta actual en un repositorio Git. El resultado será similar a:

```text
Initialized empty Git repository in .../mi-primer-repositorio/.git/
```

Git crea una carpeta oculta llamada `.git`. Allí guarda el historial, la configuración local y otros datos internos del repositorio. **No elimines ni modifiques manualmente esa carpeta**, porque hacerlo puede dañar o eliminar el historial local.

Tus archivos de trabajo continúan visibles normalmente; Git todavía no ha creado ningún commit.

---

## 5. Verificar el estado

Ejecuta:

```bash
git status
```

Este comando informa qué está ocurriendo en el repositorio sin modificar nada. Si creaste `README.md`, el resultado incluirá una sección similar a:

```text
Untracked files:
  README.md
```

Un archivo **sin seguimiento** (*untracked*) existe en la carpeta, pero Git todavía no lo ha incorporado al control de versiones. Debes decidir explícitamente si quieres incluirlo en el próximo commit.

---

## 6. Configurar la rama `main`

La rama principal del proyecto se llamará `main`. Si `git status` muestra otro nombre de rama, cámbialo con:

```bash
git branch -m main
```

La opción `-m` cambia el nombre de la rama actual a `main`.

Si anteriormente ejecutaste este comando global:

```bash
git config --global init.defaultBranch main
```

es probable que el repositorio ya se haya creado con la rama `main` y no necesites renombrarla. Puedes consultar el nombre actual con:

```bash
git branch --show-current
```

---

## 7. Preparar el archivo para el commit

Agrega `README.md` al área de preparación:

```bash
git add README.md
```

El **área de preparación** o *staging area* es una lista temporal de los cambios que formarán parte del próximo commit. `git add` no publica el archivo en GitHub ni crea todavía un commit.

Comprueba nuevamente el estado:

```bash
git status
```

Ahora `README.md` debe aparecer bajo un mensaje como **Changes to be committed** o **Cambios a ser confirmados**. Esto significa que el archivo está preparado.

---

## 8. Crear el primer commit

Guarda la primera versión del proyecto en el historial:

```bash
git commit -m "Primer commit"
```

Un **commit** es un registro permanente de los cambios preparados en un momento específico. Puede entenderse como un punto de guardado dentro del historial del proyecto.

La opción `-m` permite escribir el mensaje del commit en el mismo comando. El mensaje `Primer commit` describe brevemente este primer registro.

Git mostrará un resumen con el identificador del commit y la cantidad de archivos modificados. Si solicita tu nombre o correo, completa primero la configuración explicada en la sección 01 y vuelve a ejecutar el commit.

---

## 9. Verificar el historial

Para ver una versión resumida del historial, ejecuta:

```bash
git log --oneline
```

El resultado será parecido a:

```text
a1b2c3d (HEAD -> main) Primer commit
```

Los primeros caracteres identifican el commit. `HEAD -> main` indica que estás ubicado en la rama `main`, y al final aparece el mensaje `Primer commit`. El identificador real será diferente en tu computador.

Para salir de la vista del historial si ocupa toda la terminal, presiona la tecla `q`.

---

## 10. Crear el repositorio en GitHub

Ahora crea el repositorio remoto desde la interfaz web:

1. Entra en [GitHub](https://github.com/) e inicia sesión.
2. Pulsa el botón **New repository**. También puedes abrir el menú **+** de la parte superior y elegir **New repository**.
3. En **Repository name**, escribe `mi-primer-repositorio`.
4. Agrega una descripción si lo deseas.
5. Elige la visibilidad:
   - **Public**: cualquier persona puede ver el repositorio.
   - **Private**: solamente tú y las personas autorizadas pueden verlo.
6. **No actives** la opción **Add a README file**.
7. **No agregues** un archivo `.gitignore` todavía.
8. **No elijas** una licencia todavía.
9. Pulsa **Create repository**.

Conviene dejar el repositorio remoto vacío porque el repositorio local ya contiene un README y un commit. Si GitHub crea archivos adicionales, los historiales local y remoto comenzarán de forma diferente y será necesario integrarlos antes de hacer el primer `push`.

---

## 11. Conectar el repositorio local con GitHub

En la página del repositorio vacío, selecciona **HTTPS** y copia la URL. Tendrá una estructura similar a:

```text
https://github.com/usuario/mi-primer-repositorio.git
```

Regresa a la terminal integrada de Visual Studio Code y ejecuta el siguiente comando, reemplazando la URL del ejemplo por la que copiaste:

```bash
git remote add origin https://github.com/usuario/mi-primer-repositorio.git
```

Cada parte tiene una función:

- `remote` administra conexiones con repositorios externos.
- `add` agrega una conexión nueva.
- `origin` es el nombre corto y convencional que se asigna al repositorio remoto principal.
- La URL remota indica la ubicación exacta del repositorio en GitHub.

Este comando configura la conexión; todavía no sube ningún archivo.

---

## 12. Verificar la conexión

Ejecuta:

```bash
git remote -v
```

Debes ver dos líneas similares a estas:

```text
origin  https://github.com/usuario/mi-primer-repositorio.git (fetch)
origin  https://github.com/usuario/mi-primer-repositorio.git (push)
```

`fetch` identifica la dirección desde la que Git puede descargar cambios y `push` la dirección a la que puede subirlos. Comprueba que el nombre de usuario y del repositorio sean correctos.

---

## 13. Subir el proyecto por primera vez

Para enviar la rama `main` y su historial a GitHub, ejecuta:

```bash
git push -u origin main
```

El comando significa lo siguiente:

- `push` envía commits del repositorio local al repositorio remoto.
- `origin` señala el remoto configurado en el paso anterior.
- `main` es la rama que se enviará.
- `-u` vincula la rama local `main` con la rama remota correspondiente para futuros envíos.

GitHub puede pedirte iniciar sesión o autorizar Visual Studio Code en el navegador. Sigue las instrucciones mostradas y nunca compartas tus credenciales o códigos de acceso.

Después de completar correctamente este primer envío, normalmente bastará con ejecutar:

```bash
git push
```

Este comando utilizará la conexión establecida mediante `-u`.

---

## 14. Verificar en GitHub

Regresa al navegador y actualiza la página del repositorio. Debes comprobar que:

- Aparece el archivo `README.md`.
- La página muestra el título escrito dentro del README.
- La rama seleccionada es `main`.
- El historial contiene el mensaje `Primer commit`.

Si los archivos aparecen, el repositorio local se conectó y se publicó correctamente en GitHub.

---

## 15. Flujo completo resumido

```text
Crear carpeta
      ↓
Abrir en VS Code
      ↓
git init
      ↓
git status
      ↓
git add
      ↓
git commit
      ↓
Crear repositorio en GitHub
      ↓
git remote add origin
      ↓
git push
```

Este flujo parte de una carpeta local nueva y termina con una copia del repositorio publicada en GitHub.

---

## 16. Errores frecuentes

### `fatal: not a git repository`

**Qué significa:** Git no encuentra un repositorio en la carpeta actual ni en sus carpetas superiores.

**Causa probable:** La terminal está ubicada fuera del proyecto o todavía no se ejecutó `git init`.

**Solución básica:** Comprueba la ruta actual, entra en la carpeta correcta y ejecuta `git status`. Si es un proyecto nuevo que aún no se ha inicializado, ejecuta allí `git init`.

### `remote origin already exists`

**Qué significa:** Ya existe una conexión remota llamada `origin`.

**Causa probable:** El comando `git remote add origin ...` ya se ejecutó anteriormente.

**Solución básica:** Revisa la conexión existente con:

```bash
git remote -v
```

Si la URL es incorrecta, actualízala con la URL correcta de tu repositorio:

```bash
git remote set-url origin https://github.com/usuario/mi-primer-repositorio.git
```

### `src refspec main does not match any`

**Qué significa:** Git no encuentra una rama local `main` con commits para enviar.

**Causa probable:** Todavía no se creó el primer commit o la rama tiene otro nombre.

**Solución básica:** Ejecuta `git status` y `git log --oneline`. Si falta el commit, prepara los archivos y créalo. Después comprueba la rama con `git branch --show-current` y, si es necesario, renómbrala:

```bash
git branch -m main
```

Vuelve a intentar `git push -u origin main` cuando exista al menos un commit en `main`.

### `nothing to commit, working tree clean`

**Qué significa:** No hay cambios nuevos para guardar; el directorio de trabajo coincide con el último commit.

**Causa probable:** Los cambios ya fueron incluidos en un commit o no se guardó ninguna modificación nueva en los archivos.

**Solución básica:** Si esperabas cambios, guarda el archivo en Visual Studio Code y ejecuta nuevamente `git status`. Si no esperabas cambios, no necesitas hacer nada: el mensaje describe un estado correcto y limpio.

---

## 17. Tabla resumen de comandos

| Comando | Función |
| --- | --- |
| `git init` | Inicializa un repositorio Git en la carpeta actual. |
| `git status` | Muestra la rama y el estado de los archivos. |
| `git branch -m main` | Renombra la rama actual como `main`. |
| `git add README.md` | Agrega `README.md` al área de preparación. |
| `git commit -m "Primer commit"` | Crea un commit con los cambios preparados. |
| `git log --oneline` | Muestra el historial de commits de forma resumida. |
| `git remote add origin URL` | Agrega un repositorio remoto llamado `origin`. |
| `git remote -v` | Muestra los remotos configurados y sus URL. |
| `git push -u origin main` | Realiza el primer envío de `main` y establece su vínculo remoto. |
| `git push` | Envía los commits posteriores al remoto vinculado. |

---

## 18. Comprobación final

Antes de continuar con la guía, confirma cada punto:

- [ ] Creé la carpeta `mi-primer-repositorio`.
- [ ] Abrí la carpeta completa en Visual Studio Code.
- [ ] Inicialicé Git con `git init`.
- [ ] Creé y guardé el archivo `README.md`.
- [ ] Preparé el archivo e hice el primer commit.
- [ ] Creé un repositorio remoto vacío en GitHub.
- [ ] Conecté el remoto con el nombre `origin`.
- [ ] Realicé el primer `push` de la rama `main`.
- [ ] Puedo ver `README.md` y el commit en GitHub.

Si completaste toda la lista, ya creaste tu primer repositorio Git y lo conectaste correctamente con GitHub.
