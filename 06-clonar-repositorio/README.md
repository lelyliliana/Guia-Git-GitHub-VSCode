# 06. Clonar un repositorio desde GitHub

En esta sección aprenderás a obtener una copia local de un repositorio de GitHub y a abrirla correctamente en Visual Studio Code. Primero utilizarás la terminal integrada para comprender el proceso y después conocerás la alternativa gráfica.

---

## 1. ¿Qué significa clonar un repositorio?

**Clonar** significa crear en tu computador una copia local completa de un repositorio remoto.

La copia incluye:

- Los archivos y las carpetas del proyecto.
- El historial de commits disponible.
- Las ramas enviadas al repositorio remoto.
- La configuración que conecta la copia local con el repositorio original.

Al clonar desde GitHub, Git normalmente asigna el nombre `origin` a esa conexión remota. Gracias a ella podrás recibir cambios con `git pull` y, si tienes permisos, enviar commits con `git push`.

Clonar **no es lo mismo que descargar un archivo ZIP**. Un ZIP contiene una copia de los archivos, pero no incluye el historial ni deja configurada la conexión con GitHub.

---

## 2. ¿Cuándo necesito clonar un repositorio?

Puedes necesitar este procedimiento cuando:

- La profesora comparte un repositorio con ejemplos o actividades.
- Quieres trabajar con tu repositorio desde otro computador.
- Vas a participar en un proyecto que ya existe.
- Necesitas continuar trabajando con un repositorio publicado previamente en GitHub.
- Quieres obtener una copia local completa para estudiar su código e historial.

Antes de clonar, confirma que conoces el repositorio correcto y que tienes autorización para acceder a él si es privado.

---

## 3. Copiar la URL del repositorio en GitHub

Desde el navegador:

1. Entra en [GitHub](https://github.com/) e inicia sesión si es necesario.
2. Abre la página principal del repositorio.
3. Pulsa el botón **Code**.
4. Selecciona la opción **HTTPS**.
5. Copia la URL mediante el botón ubicado junto a ella.

La URL tendrá una estructura similar a:

```text
https://github.com/usuario/nombre-repositorio.git
```

En el ejemplo, `usuario` representa a la persona u organización propietaria y `nombre-repositorio` es el nombre del proyecto. Utiliza siempre la URL real mostrada por GitHub.

---

## 4. Elegir dónde guardar el repositorio

Antes de clonar, elige una carpeta **general** donde almacenes tus proyectos. Por ejemplo:

```text
Documentos/
```

Ubica la terminal dentro de esa carpeta general. No crees previamente una carpeta llamada `nombre-repositorio`: `git clone` la creará automáticamente y colocará allí el proyecto.

La estructura final será parecida a:

```text
Documentos/
└── nombre-repositorio/
    ├── README.md
    └── ...
```

Si deseas usar un nombre local diferente, Git permite indicarlo, pero para este primer ejercicio se conservará el nombre original.

---

## 5. Abrir una terminal desde Visual Studio Code

Abre Visual Studio Code y selecciona:

**Terminal → New Terminal**

La terminal aparecerá normalmente en la parte inferior. Debes ubicarla en la carpeta general donde quieres guardar el repositorio, por ejemplo `Documentos`, y no dentro de otro proyecto.

Puedes cambiar de ubicación con `cd` seguido de una ruta. Por ejemplo, si `Documentos` está dentro de tu carpeta personal:

### Linux y macOS

```bash
cd ~/Documentos
```

### Windows PowerShell

```powershell
cd $HOME\Documents
```

El nombre real de la carpeta puede ser `Documents`, `Documentos` u otro, según el sistema y su idioma. Escribe la ruta que exista en tu computador.

---

## 6. Verificar la ubicación

Antes de clonar, comprueba la ruta actual.

### Linux y macOS

```bash
pwd
```

### Windows PowerShell

```powershell
Get-Location
```

Un resultado posible en Linux sería:

```text
/home/estudiante/Documentos
```

En Windows podría ser:

```text
C:\Users\Estudiante\Documents
```

Confirma que la ruta corresponde a la carpeta general elegida. El repositorio se creará dentro de ella como una nueva subcarpeta.

---

## 7. Clonar el repositorio

La forma general del comando es:

```bash
git clone URL_DEL_REPOSITORIO
```

Reemplaza `URL_DEL_REPOSITORIO` por la dirección HTTPS copiada desde GitHub. Por ejemplo:

```bash
git clone https://github.com/usuario/nombre-repositorio.git
```

`git clone` realiza varias tareas:

1. Se conecta con el repositorio remoto.
2. Crea una carpeta con el nombre del repositorio.
3. Descarga sus archivos y su historial Git.
4. Prepara la rama de trabajo inicial.
5. Configura automáticamente el remoto `origin`.

Durante el proceso puedes ver mensajes como `Cloning into...`, `Receiving objects` y `Resolving deltas`. Al finalizar sin errores, volverá a aparecer el indicador de la terminal.

---

## 8. Entrar a la carpeta clonada

Después de clonar, la terminal continúa ubicada en la carpeta general. Entra al repositorio con:

```bash
cd nombre-repositorio
```

`cd` significa **cambiar de directorio**. Sustituye `nombre-repositorio` por el nombre real de la carpeta creada por Git.

Puedes verificar la nueva ubicación con `pwd` en Linux/macOS o `Get-Location` en PowerShell. La ruta debe terminar ahora con el nombre del repositorio.

---

## 9. Abrir el proyecto en Visual Studio Code

Si el comando de Visual Studio Code está disponible en la terminal, ejecuta:

```bash
code .
```

`code` abre Visual Studio Code y el punto `.` representa la carpeta actual. El proyecto puede abrirse en una ventana nueva o en la ventana existente, según tu configuración.

Si la terminal indica que `code` no se reconoce o no se encuentra, utiliza la interfaz:

1. Selecciona **File → Open Folder**.
2. Busca la carpeta clonada.
3. Selecciónala y confirma la apertura.

En ambos casos, comprueba en el panel **Explorer** que Visual Studio Code muestre la raíz completa del repositorio.

---

## 10. Verificar que el repositorio fue clonado correctamente

Abre una terminal integrada dentro del proyecto y ejecuta:

```bash
git status
```

Si acabas de clonar y no cambiaste archivos, el resultado será similar a:

```text
On branch main
Your branch is up to date with 'origin/main'.
nothing to commit, working tree clean
```

El nombre de la rama puede ser diferente. Lo importante es que Git reconozca el repositorio y no muestre `fatal: not a git repository`.

Comprueba también la conexión remota:

```bash
git remote -v
```

Normalmente aparecerá `origin` automáticamente:

```text
origin  https://github.com/usuario/nombre-repositorio.git (fetch)
origin  https://github.com/usuario/nombre-repositorio.git (push)
```

`fetch` indica desde dónde se reciben cambios y `push` hacia dónde se intentan enviar. No necesitas ejecutar `git remote add origin` después de un clon correcto.

---

## 11. Verificar la rama actual

Ejecuta:

```bash
git branch
```

Git mostrará las ramas locales y colocará un asterisco `*` junto a la rama activa. Por ejemplo:

```text
* main
```

La rama activa es aquella donde se registrarán los próximos commits. Algunos repositorios utilizan un nombre diferente de `main`; respeta la organización del proyecto.

---

## 12. Diferencia entre `git clone` y descargar ZIP

| Característica | `git clone` | **Download ZIP** |
| --- | --- | --- |
| Descarga los archivos | Sí | Sí |
| Conserva el historial Git | Sí | No |
| Configura `origin` | Sí | No |
| Mantiene el proyecto como repositorio Git | Sí | No |
| Permite usar `git pull` inmediatamente | Sí | No |
| Permite usar `git push` si tienes permisos | Sí | No |
| Requiere extraer un archivo comprimido | No | Sí |

Utiliza **Download ZIP** cuando solo necesites consultar una copia puntual de los archivos y no vayas a trabajar con el historial.

Utiliza `git clone` cuando quieras desarrollar, actualizar, consultar commits o colaborar. Para el trabajo habitual con Git y GitHub, esta es la opción adecuada.

---

## 13. ¿Qué pasa si el repositorio es privado?

GitHub solicitará autenticación al intentar clonar un repositorio privado. Además de iniciar sesión, tu cuenta debe tener permisos para acceder al proyecto.

Dependiendo de la configuración, Visual Studio Code o Git puede abrir el navegador para autorizar la operación o utilizar un administrador seguro de credenciales. Sigue las instrucciones oficiales que aparezcan en pantalla.

Nunca escribas contraseñas, tokens o claves en archivos del proyecto, mensajes de commit, capturas de pantalla o conversaciones. Tampoco compartas códigos de autenticación. Los ejemplos de esta guía no contienen credenciales reales.

Si no tienes acceso a un repositorio privado, solicita permiso a la persona u organización propietaria; no intentes evitar sus controles de acceso.

---

## 14. Clonar desde la interfaz gráfica de Visual Studio Code

También puedes clonar sin escribir `git clone` manualmente:

1. Abre Visual Studio Code.
2. Abre la **Command Palette** mediante **View → Command Palette**.
3. Escribe y selecciona **Git: Clone**.
4. Pega la URL HTTPS del repositorio y presiona `Enter`.
5. Elige la carpeta general donde quieres guardar el proyecto.
6. Espera a que termine la descarga.
7. Cuando Visual Studio Code pregunte, selecciona **Open** para abrir el repositorio.

También puedes abrir la Command Palette con `Ctrl + Shift + P` en Windows/Linux o `Command + Shift + P` en macOS.

La interfaz ejecuta el mismo concepto de clonación. Esta guía comienza con la terminal para que puedas ver la ubicación, el comando y las verificaciones que intervienen en el proceso.

---

## 15. ¿Qué pasa después de clonar?

Antes de empezar una nueva sesión de trabajo, normalmente debes recibir los cambios recientes. Un flujo básico será:

```bash
git pull
# Trabajar y guardar archivos en Visual Studio Code
git status
git add .
git commit -m "Descripción clara del cambio"
git push
```

- `git pull` recibe e integra los cambios disponibles en la rama remota vinculada.
- `git status` muestra tus cambios locales.
- `git add .` prepara los cambios revisados.
- `git commit` registra un punto en el historial local.
- `git push` envía los commits a GitHub.

`git push` solo funcionará si tu cuenta tiene permisos de escritura sobre el repositorio y si el envío puede integrarse de forma segura con el historial remoto. Poder clonar un repositorio público no implica tener permiso para modificarlo en GitHub.

---

## 16. Errores frecuentes

### `fatal: destination path '...' already exists and is not an empty directory`

- **Qué significa:** Git no puede crear la carpeta de destino porque ya existe y contiene archivos.
- **Causa probable:** Creaste previamente una carpeta con el nombre del repositorio o ya existe otra copia.
- **Solución básica y segura:** No borres la carpeta sin revisar su contenido. Elige otra carpeta general, clona con un nombre local diferente o abre la carpeta existente y comprueba si ya es el repositorio que necesitas.

### `repository not found`

- **Qué significa:** GitHub no encuentra un repositorio accesible en la URL indicada.
- **Causa probable:** La URL está incompleta o tiene un error, el repositorio cambió de nombre, es privado o tu cuenta no tiene acceso.
- **Solución básica y segura:** Abre el repositorio en el navegador, confirma que puedes verlo y vuelve a copiar su URL desde **Code → HTTPS**. Si es privado, solicita acceso.

### `Permission denied`

- **Qué significa:** El sistema o el servicio rechazó el acceso solicitado.
- **Causa probable:** No tienes permisos para escribir en la carpeta local, la cuenta no tiene acceso al repositorio o intentaste usar una conexión SSH sin una clave autorizada.
- **Solución básica y segura:** Lee la línea completa del error. Para HTTPS, vuelve a copiar la URL HTTPS; para la carpeta local, selecciona una ubicación personal como `Documentos`. Si el repositorio es privado, confirma tus permisos con la persona propietaria.

### `Authentication failed`

- **Qué significa:** GitHub no pudo verificar tu identidad.
- **Causa probable:** La sesión expiró, se eligió una cuenta incorrecta o las credenciales almacenadas dejaron de ser válidas.
- **Solución básica y segura:** Cancela cualquier solicitud sospechosa, confirma que la URL pertenece a GitHub e inicia sesión nuevamente mediante el navegador o el mecanismo oficial mostrado por Git o Visual Studio Code. No compartas credenciales ni pegues tokens en el repositorio.

### `fatal: unable to access`

- **Qué significa:** Git no pudo conectarse con la URL remota.
- **Causa probable:** No hay conexión a Internet, la URL es incorrecta, GitHub no está disponible o una red institucional, proxy o certificado está bloqueando la conexión.
- **Solución básica y segura:** Comprueba Internet y abre la URL en el navegador. Vuelve a copiar la dirección HTTPS. Si estás en una red institucional, consulta al soporte técnico; no desactives controles de seguridad ni la verificación de certificados.

---

## 17. Flujo resumido

```text
Copiar URL en GitHub
        ↓
Elegir carpeta
        ↓
git clone URL
        ↓
cd nombre-repositorio
        ↓
code .
        ↓
git status
        ↓
git remote -v
```

Al terminar, el repositorio debe estar abierto desde su carpeta raíz en Visual Studio Code y conectado con `origin`.

---

## 18. Tabla resumen de comandos

| Comando | Sistema | Función |
| --- | --- | --- |
| `pwd` | Linux/macOS | Muestra la ruta de la carpeta actual. |
| `Get-Location` | Windows PowerShell | Muestra la ruta de la carpeta actual. |
| `git clone URL` | Todos | Crea una copia local completa del repositorio remoto. |
| `cd nombre-repositorio` | Todos | Entra en la carpeta clonada. |
| `code .` | Todos, si el comando está disponible | Abre la carpeta actual en Visual Studio Code. |
| `git status` | Todos | Muestra la rama y el estado del repositorio local. |
| `git remote -v` | Todos | Muestra las URL asociadas al remoto, normalmente `origin`. |
| `git branch` | Todos | Muestra las ramas locales e identifica la activa con `*`. |

---

## 19. Comprobación final

Confirma que puedes completar cada tarea:

- [ ] Sé copiar la URL HTTPS desde **Code** en GitHub.
- [ ] Elegí correctamente la carpeta general donde guardar el repositorio.
- [ ] Ejecuté `git clone` con la URL correcta.
- [ ] Entré en la carpeta clonada con `cd`.
- [ ] Abrí la carpeta raíz del proyecto en Visual Studio Code.
- [ ] Verifiqué el repositorio con `git status`.
- [ ] Confirmé con `git remote -v` que existe `origin` y que su URL es correcta.
- [ ] Sé diferenciar `git clone` de **Download ZIP**.

Si completaste la lista, ya puedes clonar repositorios de GitHub y prepararlos correctamente para trabajar desde Visual Studio Code.
