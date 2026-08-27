# 08. Usar Source Control en Visual Studio Code

En esta sección aprenderás a realizar tareas básicas de Git mediante el panel **Source Control** de Visual Studio Code. Cada acción gráfica se relacionará con el comando que ya conoces para que comprendas qué ocurre.

Los nombres, iconos o posiciones de algunos botones pueden variar ligeramente según la versión, el idioma, el tamaño de la ventana y la configuración de Visual Studio Code.

---

## 1. ¿Qué es Source Control?

Visual Studio Code incorpora una interfaz gráfica de **control de código fuente**. Su integración con Git permite revisar archivos modificados, preparar cambios, crear commits e intercambiar commits con un repositorio remoto sin salir del editor.

La interfaz no reemplaza Git. Cuando seleccionas un botón, Visual Studio Code solicita a Git que realice la operación correspondiente. Por eso, los cambios hechos desde Source Control también aparecen en la terminal y viceversa.

Comprender los comandos continúa siendo importante: permite interpretar mejor el estado del repositorio, trabajar en otros entornos y diagnosticar problemas.

---

## 2. ¿Dónde está Source Control?

El icono de **Source Control** se encuentra normalmente en la **Activity Bar**, la barra vertical del lado izquierdo. Suele representar una bifurcación con círculos conectados.

Puedes abrir la vista de estas formas:

- Selecciona el icono **Source Control** en la Activity Bar.
- Abre **View → Source Control** desde el menú.
- En Windows/Linux, utiliza `Ctrl + Shift + G`.
- En macOS, utiliza `Control + Shift + G`.

Cuando hay cambios, el icono puede mostrar una insignia numérica. Ese número ayuda a identificar cuántos recursos modificados detecta la vista, pero no significa que ya exista un commit.

---

## 3. Abrir un repositorio Git

Para que Source Control funcione correctamente, abre la carpeta raíz del repositorio mediante:

**File → Open Folder**

Después abre la terminal integrada y comprueba:

```bash
git status
```

Git debe mostrar la rama y el estado de los archivos. Si aparece `fatal: not a git repository`, revisa que hayas abierto la carpeta correcta.

Cuando una carpeta todavía no es un repositorio, Source Control puede mostrar **Initialize Repository**. Esa opción se explicará más adelante; no la selecciones si el proyecto ya contiene un repositorio Git o si no estás seguro de la carpeta abierta.

---

## 4. Qué muestra el panel Source Control

Según el estado del proyecto, el panel puede incluir:

- **Changes:** archivos nuevos, modificados o eliminados que todavía no están preparados.
- **Staged Changes:** cambios preparados que formarán parte del próximo commit.
- **Insignia o cantidad de cambios:** número de archivos detectados.
- **Cuadro del mensaje:** espacio donde se escribe la descripción del commit.
- **Botón Commit:** crea el commit con los cambios preparados.
- **More Actions (`...`):** menú con operaciones como Pull, Push, Fetch y otras acciones Git.
- **Indicadores de sincronización:** muestran commits entrantes o salientes cuando existe un remoto.

También pueden aparecer letras como `M` para un archivo modificado, `U` para uno sin seguimiento y `D` para uno eliminado.

La interfaz puede variar ligeramente entre versiones. Si no ves una acción, revisa el menú `...`, el menú contextual del archivo o la Command Palette.

---

## 5. Modificar un archivo y observar el cambio

Realiza un ejemplo sencillo:

1. Abre `README.md` desde el panel Explorer.
2. Agrega o corrige una línea de texto.
3. Guarda con `Ctrl + S` en Windows/Linux o `Command + S` en macOS.
4. Abre Source Control.

`README.md` debería aparecer automáticamente bajo **Changes** con el indicador de archivo modificado.

Esta información corresponde a lo que muestra la terminal al ejecutar:

```bash
git status
```

Guardar el archivo permite que Git lea el cambio desde el disco. Todavía no lo prepara ni crea un commit.

---

## 6. Ver las diferencias de un archivo

Selecciona `README.md` en la lista **Changes**. Visual Studio Code abrirá un editor de diferencias o *diff*.

Según el ancho y la configuración, la comparación puede aparecer lado a lado o en una sola vista. Allí podrás reconocer:

- **Líneas agregadas:** contenido nuevo, normalmente marcado en verde y con `+`.
- **Líneas eliminadas:** contenido retirado, normalmente marcado en rojo y con `-`.
- **Versión anterior:** contenido registrado en el último commit.
- **Versión actual:** contenido guardado actualmente en el computador.

Revisar el *diff* antes de preparar cambios ayuda a detectar errores, texto accidental, archivos equivocados y datos privados. No hagas commit únicamente porque un archivo aparece en la lista; comprueba primero qué cambió.

---

## 7. Preparar un archivo desde Source Control

Para preparar solamente un archivo:

1. Coloca el cursor sobre el archivo bajo **Changes**.
2. Selecciona el símbolo `+`, llamado **Stage Changes**.
3. Comprueba que el archivo pase a **Staged Changes**.

Esta acción equivale a ejecutar:

```bash
git add nombre-archivo
```

Para el ejemplo de esta sección sería:

```bash
git add README.md
```

Preparar un archivo significa seleccionarlo para el próximo commit. No lo publica en GitHub.

---

## 8. Preparar todos los cambios

Para preparar todos los archivos, coloca el cursor sobre el encabezado **Changes** y selecciona el símbolo `+`. Según la versión, también puedes abrir el menú `...` y elegir **Stage All Changes**.

La acción se relaciona con:

```bash
git add .
```

El punto representa la carpeta actual. Antes de preparar todo, revisa cada archivo y confirma que `.gitignore` excluya dependencias, archivos temporales y configuraciones privadas.

Nunca prepares contraseñas, tokens, claves API, claves privadas ni archivos `.env` que contengan secretos.

---

## 9. Quitar un archivo del área de preparación

Si preparaste un archivo por equivocación:

1. Busca el archivo bajo **Staged Changes**.
2. Coloca el cursor sobre él.
3. Selecciona el símbolo `−`, llamado **Unstage Changes**.

El archivo regresará a **Changes**. Esta acción realiza la operación Git inversa a *stage*: retira el cambio del área de preparación, pero mantiene la modificación en tu archivo de trabajo.

No confundas **Unstage Changes** con opciones que descartan cambios. Quitar del área de preparación no debe borrar tu edición.

---

## 10. Crear un commit desde VS Code

Cuando **Staged Changes** contenga solamente los cambios correctos:

1. Escribe un mensaje claro en el cuadro situado en la parte superior de Source Control.
2. Describe qué cambió, por ejemplo: `Actualizar instrucciones de instalación`.
3. Selecciona **Commit**.

La acción equivale a:

```bash
git commit -m "Actualizar instrucciones de instalación"
```

Si el commit se crea correctamente, los archivos preparados desaparecerán de **Staged Changes**. Esto no significa necesariamente que se publicaron en GitHub: el commit primero queda en el historial local.

Puedes comprobarlo desde la terminal:

```bash
git status
git log --oneline -5
```

---

## 11. Sincronizar o hacer `push`

Después del commit, Visual Studio Code puede mostrar distintas acciones:

- **Push:** envía los commits locales pendientes al remoto vinculado. Equivale a `git push`.
- **Sync Changes:** primero recibe cambios remotos y después envía los commits locales.
- **Publish Branch:** publica una rama local que todavía no tiene una rama remota vinculada.

Para ejecutar Push de manera individual, abre **More Actions (`...`)** en Source Control y selecciona **Push**. La operación equivale a:

```bash
git push
```

Si no aparece Push, revisa el menú `...`, la conexión remota y si realmente existen commits locales pendientes.

---

## 12. Hacer `pull` desde VS Code

Antes de recibir cambios, revisa que el proyecto esté en un estado seguro. Puedes comprobarlo en Source Control y mediante:

```bash
git status
```

Después abre **More Actions (`...`)** y selecciona **Pull**. Según la versión, la acción también puede aparecer en la Command Palette o en menús relacionados con Git.

La operación equivale a:

```bash
git pull
```

Pull descarga los commits remotos e intenta integrarlos en la rama local. Si tienes modificaciones locales incompatibles, Git puede detener la operación o producir un conflicto. Lee los mensajes antes de continuar.

---

## 13. Sincronizar cambios

**Sync Changes** combina dos direcciones de trabajo: normalmente realiza primero Pull para recibir cambios remotos y luego Push para enviar commits locales.

Puede resultar cómodo, pero oculta dos operaciones distintas. Antes de depender de este botón, comprende bien:

- `git pull`: GitHub → computador.
- `git push`: computador → GitHub.

En un proyecto compartido, revisa el estado, los commits entrantes y los salientes antes de sincronizar. Si VS Code solicita confirmación, lee el mensaje completo.

---

## 14. Inicializar un repositorio desde Source Control

Cuando la carpeta abierta todavía no contiene Git, Source Control puede mostrar **Initialize Repository**.

Seleccionar esa opción equivale a:

```bash
git init
```

Visual Studio Code solicita a Git que cree el repositorio local y su carpeta oculta `.git`. Después, los archivos existentes aparecerán como cambios sin seguimiento.

Utiliza esta opción solamente si confirmaste que la carpeta correcta aún no es un repositorio. Si `git status` ya muestra una rama, no necesitas inicializarlo otra vez.

---

## 15. Publicar un repositorio en GitHub desde VS Code

Cuando tienes un repositorio local sin remoto, Source Control puede ofrecer **Publish to GitHub**.

De forma general, esta opción permite:

1. Iniciar sesión en GitHub si es necesario.
2. Elegir si el nuevo repositorio será público o privado.
3. Seleccionar los archivos iniciales.
4. Crear el repositorio en GitHub.
5. Configurar la conexión remota y enviar los commits.

Es una alternativa gráfica al proceso manual estudiado en las secciones anteriores. No reemplaza lo aprendido: conviene comprender `git init`, `git add`, `git commit`, `git remote` y `git push` antes de automatizar el proceso.

Los textos exactos y las preguntas pueden variar. Revisa siempre el nombre, la visibilidad y los archivos antes de confirmar la publicación.

---

## 16. Iniciar sesión en GitHub desde VS Code

Clonar repositorios privados, publicar, hacer Push y utilizar otras funciones de GitHub puede requerir autenticación.

Visual Studio Code puede abrir el navegador o mostrar una notificación para iniciar sesión y autorizar el acceso. Verifica que la solicitud pertenezca realmente a Visual Studio Code y GitHub, y sigue el mecanismo oficial presentado.

Nunca compartas contraseñas, tokens, códigos de autenticación o claves. Tampoco los escribas en archivos del proyecto, mensajes de commit o capturas de pantalla. Esta guía no utiliza credenciales reales.

Tener acceso de lectura permite clonar algunos repositorios, pero Push requiere permisos de escritura.

---

## 17. Relación entre interfaz y comandos

| Acción en VS Code | Comando equivalente | Resultado principal |
| --- | --- | --- |
| **Stage Changes** en un archivo | `git add archivo` | Prepara un archivo para el próximo commit. |
| **Stage All Changes** | `git add .` | Prepara los cambios revisados de la carpeta actual. |
| **Commit** | `git commit -m "mensaje"` | Registra los cambios preparados en el historial local. |
| **Push** | `git push` | Envía commits locales al remoto. |
| **Pull** | `git pull` | Descarga e integra commits remotos. |
| **Initialize Repository** | `git init` | Inicializa Git en la carpeta abierta. |

La interfaz y la terminal operan sobre el mismo repositorio. Puedes preparar un archivo desde Source Control y comprobar el resultado con `git status`.

---

## 18. Flujo visual usando Source Control

```text
Modificar archivo
        ↓
Guardar
        ↓
Abrir Source Control
        ↓
Revisar cambios
        ↓
Stage
        ↓
Commit
        ↓
Push
        ↓
Verificar en GitHub
```

El flujo gráfico conserva las mismas etapas del trabajo por terminal: modificar, revisar, preparar, confirmar y publicar.

---

## 19. ¿Terminal o interfaz gráfica?

### Terminal

- Ayuda a comprender con precisión qué operación se ejecuta.
- Es más universal y funciona en distintos editores y entornos.
- Permite leer claramente comandos, resultados y errores.
- Facilita seguir documentación técnica y solicitar ayuda.

### Source Control

- Presenta el estado de manera visual.
- Facilita revisar diferencias entre versiones.
- Permite preparar archivos mediante botones.
- Puede resultar cómodo para tareas rutinarias.

Ambas formas son válidas y complementarias. Una buena práctica para aprender es ejecutar una acción gráfica y comprobar después su efecto con `git status` o `git log`.

---

## 20. Errores y situaciones frecuentes

### Source Control no muestra archivos modificados

- **Causa probable:** el archivo no se guardó, abriste otra carpeta, está ignorado o Source Control todavía no actualizó la vista.
- **Solución básica:** guarda el archivo, confirma la carpeta abierta y ejecuta `git status`. Comprueba también `.gitignore`.

### No aparece el botón Push

- **Causa probable:** no existen commits pendientes, la acción está dentro de `...` o no hay un remoto configurado.
- **Solución básica:** revisa `git status`, abre **More Actions (`...`)** y comprueba `git remote -v`. No agregues otro remoto sin entender la configuración actual.

### Aparece Publish Branch

- **Causa probable:** la rama actual existe solamente en tu computador y aún no tiene una rama remota vinculada.
- **Solución básica:** confirma el nombre de la rama y el repositorio remoto. Si deseas publicarla y tienes permisos, utiliza **Publish Branch**.

### Se muestra Sync Changes

- **Causa probable:** la rama está vinculada con un remoto y puede tener commits entrantes, salientes o ambos.
- **Solución básica:** revisa los indicadores y comprende que Sync normalmente realiza Pull y Push. Si prefieres controlar cada paso, utiliza las acciones individuales desde `...`.

### No hay repositorio Git abierto

- **Causa probable:** abriste una carpeta que no contiene `.git` o abriste solamente un archivo.
- **Solución básica:** usa **File → Open Folder** para abrir la raíz correcta y confirma con `git status`. Inicializa solo si realmente se trata de un proyecto nuevo sin Git.

### VS Code pide iniciar sesión en GitHub

- **Causa probable:** intentas publicar, acceder a un repositorio privado o realizar una operación que necesita autorización.
- **Solución básica:** verifica la solicitud e inicia sesión mediante el proceso oficial. Confirma que tu cuenta tenga permisos y nunca compartas credenciales.

---

## 21. Buenas prácticas

- Revisa el *diff* antes de preparar cualquier archivo.
- Prepara solamente cambios relacionados con el propósito del commit.
- Escribe mensajes claros y específicos.
- Comprueba que no estás agregando archivos innecesarios.
- Mantén `.gitignore` adecuado al proyecto.
- Nunca publiques contraseñas, tokens, claves API o claves privadas.
- Comprueba GitHub después de Push.
- Revisa `git status` cuando la interfaz no sea clara.
- Comprende qué hace cada acción antes de depender de botones automáticos como Sync Changes.
- Lee todas las advertencias y mensajes antes de confirmar una operación.

---

## 22. Tabla rápida de consulta

| Quiero... | Dónde hacerlo en Source Control... | Comando equivalente... |
| --- | --- | --- |
| Ver archivos modificados | Lista **Changes** | `git status` |
| Revisar una diferencia | Seleccionar el archivo en **Changes** | No es un único comando básico; corresponde a revisar el *diff*. |
| Preparar un archivo | Botón `+` junto al archivo | `git add archivo` |
| Preparar todos los cambios | Botón `+` junto a **Changes** | `git add .` |
| Quitar un archivo preparado | Botón `−` en **Staged Changes** | Operación Git de *unstage*. |
| Crear un commit | Escribir mensaje y seleccionar **Commit** | `git commit -m "mensaje"` |
| Subir commits | `...` → **Push** | `git push` |
| Recibir e integrar commits | `...` → **Pull** | `git pull` |
| Intercambiar cambios | **Sync Changes** | Pull seguido de Push. |
| Inicializar la carpeta | **Initialize Repository** | `git init` |

---

## 23. Comprobación final

Confirma que puedes completar cada tarea:

- [ ] Identifico el icono y la vista Source Control.
- [ ] Reconozco la diferencia entre **Changes** y **Staged Changes**.
- [ ] Abro y reviso las diferencias de un archivo.
- [ ] Preparo archivos individuales o todos los cambios revisados.
- [ ] Creo commits con mensajes claros desde Visual Studio Code.
- [ ] Realizo Push de los commits locales.
- [ ] Realizo Pull después de revisar el estado del proyecto.
- [ ] Relaciono los botones principales con sus comandos Git equivalentes.
- [ ] Distingo el historial local de los commits publicados en el remoto.

Si completaste la lista, ya puedes combinar la terminal y Source Control para realizar el flujo básico de Git desde Visual Studio Code.
