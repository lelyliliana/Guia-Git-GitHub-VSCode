# 12. Errores frecuentes en Git y GitHub

Esta sección es una referencia rápida para diagnosticar problemas comunes desde Visual Studio Code. Busca una parte reconocible del mensaje, lee su explicación y realiza primero las comprobaciones seguras.

---

## 1. Cómo usar esta guía

Ante un error o resultado inesperado:

1. Lee el mensaje completo, incluidas las líneas anteriores.
2. No ejecutes comandos al azar ni copies soluciones sin comprenderlas.
3. Confirma en qué carpeta está la terminal.
4. Ejecuta `git status`.
5. Comprueba la rama activa.
6. Revisa el remoto configurado.
7. Protege tus archivos y commits antes de cambiar algo.
8. Evita comandos destructivos.

Comandos iniciales de diagnóstico:

```bash
git status
git branch
git remote -v
```

Los mensajes de Git pueden variar según el sistema, idioma, versión y situación. Distingue entre un **error**, que impide una operación, y un **mensaje informativo**, que solamente describe el estado.

---

## 2. `fatal: not a git repository`

**Tipo:** error de ubicación o inicialización.

**Qué significa:** Git no encuentra un repositorio en la carpeta actual ni en sus carpetas superiores.

**Causas probables:** abriste la terminal fuera del proyecto, abriste una subcarpeta equivocada o el proyecto todavía no fue inicializado.

Verifica la ruta.

### Linux y macOS

```bash
pwd
```

### Windows PowerShell

```powershell
Get-Location
```

Entra en la carpeta correcta con `cd ruta-del-proyecto` y comprueba:

```bash
git status
```

Utiliza `git init` únicamente si confirmaste que estás en la raíz de un proyecto nuevo que todavía no debe tener historial. No lo ejecutes para corregir una ruta equivocada. Consulta [03. Crear el primer repositorio](../03-primer-repositorio/README.md).

---

## 3. `remote origin already exists`

**Tipo:** error de configuración duplicada.

**Qué significa:** el repositorio ya tiene un remoto llamado `origin`.

Revisa la configuración existente:

```bash
git remote -v
```

Comprueba el propietario y el nombre del repositorio en las URL de `fetch` y `push`. Si son correctas, no agregues `origin` otra vez.

Si la URL es incorrecta, no elimines conexiones a ciegas. Confirma primero cuál debe ser el repositorio remoto y consulta el procedimiento de conexión en [04. Subir un proyecto existente](../04-subir-proyecto-existente/README.md).

---

## 4. `repository not found`

**Tipo:** error de acceso o URL.

**Qué significa:** GitHub no encuentra un repositorio accesible para la cuenta y la dirección utilizadas.

**Causas posibles:**

- La URL es incorrecta.
- El repositorio es privado.
- Tu cuenta no tiene permisos.
- El repositorio fue eliminado o cambió de nombre.
- Iniciaste sesión con otro usuario.

Comprueba el remoto:

```bash
git remote -v
```

Abre el repositorio en el navegador. Si puedes acceder, copia nuevamente la URL desde **Code → HTTPS**. Si es privado, solicita acceso a la persona propietaria.

---

## 5. `Permission denied`

**Tipo:** error de permisos o autenticación.

**Qué significa:** el sistema operativo, GitHub o el método de conexión rechazó el acceso.

Lee la línea completa. Puede referirse a una carpeta local sin permiso de escritura, a una conexión SSH no configurada o a una cuenta sin acceso al repositorio.

Utiliza una carpeta personal para los proyectos, verifica la URL con `git remote -v` y confirma que tu cuenta haya sido invitada. Nunca compartas contraseñas, tokens, códigos de autenticación ni claves SSH privadas.

---

## 6. `Authentication failed`

**Tipo:** error de autenticación.

**Qué significa:** GitHub no pudo verificar tu identidad para la operación solicitada.

La autenticación Git por HTTPS no acepta la contraseña normal de la cuenta de GitHub en muchos flujos. Visual Studio Code o el administrador de credenciales puede abrir un navegador o utilizar un mecanismo autorizado.

Comprueba:

- Que iniciaste sesión con la cuenta correcta.
- Que la sesión o credencial guardada sigue siendo válida.
- Que la URL corresponde realmente a GitHub.
- Que tu cuenta tiene permisos sobre el repositorio.

Sigue únicamente el proceso oficial mostrado por GitHub, Git o Visual Studio Code. No pegues credenciales reales en archivos, comandos compartidos o capturas.

---

## 7. `failed to push some refs`

**Tipo:** error de envío.

**Qué significa:** Git no pudo publicar una o más referencias. Frecuentemente el remoto contiene commits que todavía no existen localmente.

Empieza por:

```bash
git status
git pull
```

Lee el resultado de `git pull`. Si aparecen conflictos, resuélvelos y completa el commit antes de intentar:

```bash
git push
```

No utilices `force push`; podría sobrescribir trabajo remoto. Consulta [07. Actualizar un repositorio](../07-actualizar-repositorio/README.md).

---

## 8. `rejected`

**Tipo:** error de envío o protección.

**Qué significa:** el remoto rechazó el `push`. Una causa frecuente es que la rama de GitHub cambió desde tu última actualización.

Protege primero el trabajo local y revisa:

```bash
git status
git pull
```

También puede existir una regla del repositorio que impida el envío directo. Lee el resto del mensaje: explica si faltan cambios remotos, permisos o verificaciones.

---

## 9. `src refspec main does not match any`

**Tipo:** error de rama o historial.

**Qué significa:** Git no encuentra una referencia local `main` adecuada para enviar.

**Causas típicas:** todavía no existe ningún commit o la rama tiene otro nombre.

Revisa:

```bash
git status
git branch
git log --oneline -5
```

Confirma que exista al menos un commit y observa el nombre real de la rama. No renombres una rama compartida sin comprobar la convención del proyecto.

---

## 10. `nothing to commit, working tree clean`

> **Tipo: mensaje informativo. NO es un error.**

Significa que no existen cambios nuevos pendientes de commit: los archivos guardados coinciden con el último commit.

Si esperabas cambios, guarda el archivo, confirma la carpeta y revisa `.gitignore`. Si no esperabas cambios, no debes hacer nada.

---

## 11. `Everything up-to-date`

> **Tipo: mensaje informativo. NO es un error.**

Significa que no existen commits locales pendientes de subir a la rama remota seleccionada.

Si editaste archivos, recuerda que `git push` solo envía commits. Revisa si guardaste, preparaste y confirmaste los cambios.

---

## 12. `Already up to date.`

> **Tipo: mensaje informativo. NO es un error.**

Significa que `git pull` o una integración no encontró commits nuevos que aplicar a la rama actual.

Si esperabas una actualización, comprueba el remoto y la rama activa.

---

## 13. `Untracked files`

**Tipo:** estado informativo.

Son archivos nuevos que Git todavía no controla. Revísalos con:

```bash
git status
```

Para preparar uno específico:

```bash
git add nombre-archivo
```

Para preparar todos los cambios revisados de la carpeta actual:

```bash
git add .
```

Agrega a `.gitignore` dependencias, archivos temporales o configuraciones privadas que no deban controlarse. Nunca prepares secretos.

---

## 14. `Changes not staged for commit`

**Tipo:** estado informativo.

Existen archivos conocidos por Git que cambiaron, pero todavía no están preparados para el próximo commit.

Después de revisar las diferencias, puedes preparar los cambios:

```bash
git add .
git status
```

El segundo comando permite confirmar qué pasó a **Changes to be committed**.

---

## 15. `Changes to be committed`

**Tipo:** estado normal.

Los cambios ya están en el área de preparación y formarán parte del próximo commit. Revisa la lista y, si es correcta, ejecuta:

```bash
git commit -m "Mensaje claro del cambio"
```

Este estado no significa que los cambios ya estén en GitHub.

---

## 16. `Your branch is ahead of 'origin/main'`

**Tipo:** mensaje informativo.

La rama local contiene uno o más commits que todavía no están en `origin/main`.

Después de verificar que la rama y los commits son correctos, la acción habitual es:

```bash
git push
```

---

## 17. `Your branch is behind 'origin/main'`

**Tipo:** mensaje informativo que requiere actualización.

`origin/main` contiene commits que faltan en tu rama local. Con el trabajo local protegido, la acción habitual es:

```bash
git pull
```

Lee el resultado porque la integración puede requerir resolver conflictos.

---

## 18. `Your branch is up to date with 'origin/main'`

**Tipo:** mensaje informativo.

La rama local y la referencia remota conocida están sincronizadas en ese momento. Ten presente que `git fetch` o `git pull` actualiza la información recibida desde el remoto.

No se requiere ninguna acción si no esperabas cambios nuevos.

---

## 19. `divergent branches`

**Tipo:** situación de historiales diferentes.

La rama local y la remota avanzaron por caminos distintos: cada una contiene commits que la otra no tiene. Git puede solicitar que elijas una estrategia de integración.

Diagnostica primero:

```bash
git status
git log --oneline -5
git fetch
```

Revisa qué trabajo existe en cada lado y consulta la estrategia acordada por el equipo. Si no comprendes la situación, pide orientación. No uses comandos destructivos ni envío forzado.

---

## 20. `local changes would be overwritten by merge`

**Tipo:** error de protección.

Git cancela la integración porque podría sobrescribir modificaciones locales. Está protegiendo tu trabajo.

Ejecuta:

```bash
git status
```

Abre los archivos indicados y decide cómo conservarlos. Si forman un cambio completo, revísalos y crea un commit. Si no sabes de dónde provienen, detente y solicita ayuda. No borres ni fuerces la operación.

---

## 21. `Your local changes would be overwritten`

**Tipo:** error de protección.

El mismo principio puede aparecer durante `pull`, merge o cambio de rama: la operación solicitada reemplazaría cambios locales.

Revisa `git status`, guarda los archivos en Visual Studio Code y conserva adecuadamente el trabajo. No elimines contenido ni elijas una opción de fuerza para ocultar el problema.

---

## 22. `merge conflict`

**Tipo:** conflicto que necesita intervención humana.

Dos cambios no pudieron integrarse automáticamente. Flujo básico:

```bash
git status
# Resolver y guardar el archivo en Visual Studio Code
git add nombre-archivo
git status
git commit -m "Resolver conflicto"
```

Compara Current e Incoming, elimina las marcas y prueba el resultado. Consulta la guía completa [11. Resolver conflictos en Git](../11-conflictos/README.md).

---

## 23. `CONFLICT (content)`

**Tipo:** conflicto de contenido.

Git detectó versiones incompatibles dentro del archivo indicado. Ábrelo en Visual Studio Code, lee ambos bloques y construye el contenido final correcto.

No selecciones **Accept Current**, **Accept Incoming** o **Accept Both** sin revisar el resultado.

---

## 24. `You have unmerged paths`

**Tipo:** estado de conflicto pendiente.

Todavía existen archivos sin resolver o sin marcar como resueltos. Consulta la lista:

```bash
git status
```

Resuelve cada archivo, guárdalo y usa `git add archivo` solamente después de revisarlo. No hagas `push` mientras existan rutas sin fusionar.

---

## 25. `fatal: destination path '...' already exists and is not an empty directory`

**Tipo:** error al clonar.

`git clone` intenta crear una carpeta, pero ya existe una carpeta no vacía con el mismo nombre.

No la borres automáticamente. Revisa si contiene trabajo o si ya es una copia del repositorio. Puedes elegir otra carpeta general o clonar con un nombre local distinto. Consulta [06. Clonar un repositorio](../06-clonar-repositorio/README.md).

---

## 26. `pathspec '...' did not match any file(s) known to git`

**Tipo:** error de nombre o referencia.

Git no encuentra la rama, archivo o referencia escrita. Puede existir un error ortográfico, un nombre de archivo incorrecto o una rama inexistente.

Para ramas, revisa:

```bash
git branch
git branch -a
```

Para archivos, confirma el nombre exacto en Explorer, incluidas mayúsculas, minúsculas y extensión.

---

## 27. `branch already exists`

**Tipo:** error al crear una rama duplicada.

La rama ya existe localmente. Compruébalo:

```bash
git branch
```

Si esa es la rama deseada, cambia a ella sin intentar crearla otra vez:

```bash
git switch nombre-rama
```

Consulta [10. Trabajar con ramas](../10-ramas/README.md).

---

## 28. No aparece nada al ejecutar `git branch`

**Tipo:** estado posible en un repositorio nuevo.

En un repositorio recién inicializado y sin commits, la rama todavía puede no aparecer de forma útil en `git branch`.

Ejecuta `git status`, crea o revisa el primer archivo, prepáralo y realiza el primer commit siguiendo [03. Crear el primer repositorio](../03-primer-repositorio/README.md). Después, `git branch` podrá mostrar la rama asociada al historial.

---

## 29. Git no reconoce el comando `git`

**Tipo:** error de instalación o PATH.

En Linux/macOS puede aparecer:

```text
git: command not found
```

En Windows puede indicarse que `git` no se reconoce como comando. Git puede no estar instalado o su ejecutable no estar disponible en `PATH` para la terminal actual.

Cierra y abre Visual Studio Code si acabas de instalarlo. Después consulta [01. Instalación y configuración de Git](../01-instalacion-y-configuracion/README.md).

---

## 30. `code: command not found`

**Tipo:** error del comando de apertura de Visual Studio Code.

El comando:

```bash
code .
```

no está disponible en el `PATH`. Esto no impide trabajar con Git.

Abre Visual Studio Code manualmente y utiliza:

**File → Open Folder**

Selecciona la carpeta raíz del proyecto. La configuración del comando `code` puede realizarse después según el sistema.

---

## 31. VS Code no muestra cambios en Source Control

**Tipo:** problema de vista, carpeta o estado.

**Causas posibles:**

- El archivo no se guardó.
- Abriste otra carpeta.
- El proyecto no está inicializado con Git.
- `.gitignore` excluye el archivo nuevo.
- Source Control necesita actualizar la vista.

Guarda el archivo y comprueba en la terminal:

```bash
git status
```

Si Git muestra el cambio pero Source Control no, actualiza la vista o vuelve a abrir la carpeta. Consulta [08. Usar Source Control](../08-source-control-vscode/README.md).

---

## 32. Un archivo no aparece en `git status`

**Tipo:** posible regla de exclusión.

El archivo puede coincidir con `.gitignore` u otra regla de ignorado. Diagnostica un archivo concreto con:

```bash
git check-ignore -v nombre-archivo
```

Este comando solo consulta qué regla ignora el archivo; no lo modifica. Si muestra una ruta, número de línea y patrón, revisa esa regla antes de cambiar `.gitignore`.

Un archivo ya controlado se comporta de forma diferente: `.gitignore` está pensado principalmente para archivos que aún no tienen seguimiento.

---

## 33. Subí un archivo que no quería subir

No entres en pánico. Primero determina en qué etapa está.

Si está preparado pero todavía no existe el commit, y el repositorio ya tiene un commit anterior, retíralo del área de preparación:

```bash
git restore --staged nombre-archivo
```

El comando conserva el archivo en el computador; solamente lo retira del *staging area*. También puedes usar **Unstage Changes** desde Source Control. Después revisa `.gitignore` y `git status`.

Si el repositorio aún no tiene ningún commit y el comando no puede usar una versión anterior como referencia, utiliza **Unstage Changes** en Source Control y comprueba el resultado.

Si el archivo ya llegó a GitHub y contiene contraseñas, tokens o secretos, borrarlo en un commit posterior no es suficiente. Revoca o reemplaza inmediatamente las credenciales desde el servicio que las emitió y solicita ayuda para revisar el historial.

---

## 34. Agregué demasiados archivos con `git add .`

Antes de crear el commit, revisa:

```bash
git status
```

Para retirar un archivo preparado, cuando ya existe un commit anterior:

```bash
git restore --staged nombre-archivo
```

Esto no borra el archivo del computador. También puedes seleccionar **Unstage Changes** en Source Control. Agrega reglas correctas a `.gitignore` cuando se trate de archivos nuevos que no deben controlarse y vuelve a revisar.

---

## 35. Me equivoqué en el mensaje del commit

**Tipo:** error descriptivo, normalmente no funcional.

Si el commit ya existe y el mensaje no afecta el funcionamiento, para principiantes suele ser más seguro dejarlo así y escribir mensajes mejores en los próximos commits.

Modificar commits puede reescribir historial, especialmente si ya fueron publicados. No lo hagas como solución automática en un repositorio compartido.

---

## 36. Hice cambios pero `git push` dice `Everything up-to-date`

`git push` envía commits, no archivos editados directamente. Es probable que los cambios no se guardaran, prepararan o confirmaran.

Sigue el flujo y lee cada resultado:

```bash
git status
git add .
git status
git commit -m "Descripción clara del cambio"
git push
```

Antes de `git add .`, comprueba que no haya archivos innecesarios o secretos.

---

## 37. Hice commit pero no aparece en GitHub

El commit se guarda primero en el repositorio local. Revisa:

```bash
git status
git branch
```

Si `git status` dice que la rama está **ahead** de su rama remota, ejecuta:

```bash
git push
```

Después confirma en GitHub que estás viendo el repositorio y la rama correctos.

---

## 38. Hice `push` pero estoy mirando otra rama en GitHub

GitHub puede mostrar `main` mientras tú publicaste otra rama. Comprueba la rama local activa:

```bash
git branch
```

En GitHub, utiliza el selector de ramas situado sobre la lista de archivos y elige la rama publicada. Subir una rama de trabajo no integra automáticamente sus commits en `main`.

---

## 39. No puedo hacer `push` porque no tengo permisos

**Tipo:** error de autorización.

Clonar un repositorio público significa que puedes leerlo, no que puedas modificarlo directamente en GitHub.

La persona propietaria puede agregarte como colaborador. En otros proyectos se utiliza un flujo con *fork* y *pull request*, pero ese procedimiento no se desarrolla todavía en esta guía.

Confirma tu cuenta, la invitación y `git remote -v`. Nunca uses credenciales de otra persona.

---

## 40. Tabla de diagnóstico rápido

| Mensaje o problema | Qué significa | Primer comando que debes ejecutar |
| --- | --- | --- |
| `not a git repository` | La terminal no está dentro de un repositorio reconocido. | `git status` después de verificar la ruta |
| `origin already exists` | Ya hay un remoto llamado `origin`. | `git remote -v` |
| `repository not found` | URL incorrecta o falta de acceso. | `git remote -v` |
| `failed to push some refs` / `rejected` | El envío no pudo integrarse o fue protegido. | `git status` |
| `src refspec main does not match any` | No existe una rama `main` enviable o falta el primer commit. | `git status` |
| `nothing to commit` | No hay cambios nuevos para confirmar. | `git status` |
| `Everything up-to-date` | No hay commits locales pendientes de subir. | `git status` |
| Rama **ahead** | Hay commits locales pendientes de publicar. | `git status` |
| Rama **behind** | Hay commits remotos pendientes de integrar. | `git status` |
| `divergent branches` | Local y remoto tienen commits diferentes. | `git status` |
| `local changes would be overwritten` | Git protege modificaciones locales. | `git status` |
| `merge conflict` / `unmerged paths` | Hay archivos que requieren resolución. | `git status` |
| Source Control no muestra cambios | Posible archivo sin guardar, carpeta incorrecta o regla de ignorado. | `git status` |

`git status` aparece repetidamente porque ofrece contexto sin modificar el proyecto.

---

## 41. Los cinco comandos de diagnóstico más útiles

### Estado general

```bash
git status
```

Muestra la rama, cambios preparados, no preparados, archivos nuevos y conflictos.

### Rama activa

```bash
git branch
```

Lista ramas locales e identifica la activa mediante `*`.

### Conexión remota

```bash
git remote -v
```

Muestra los nombres y las URL de los remotos configurados.

### Historial reciente

```bash
git log --oneline -5
```

Muestra los cinco commits más recientes de forma resumida.

### Diferencias no preparadas

```bash
git diff
```

Muestra cambios en archivos controlados que todavía no están preparados. Es una consulta y no modifica los archivos.

---

## 42. Antes de pedir ayuda

Recopila:

- El mensaje completo del error.
- La salida de `git status`.
- La salida de `git branch`.
- La salida de `git remote -v`.
- El comando que ejecutaste justo antes.
- Qué resultado esperabas.
- Una captura de pantalla, si ayuda a mostrar la interfaz.

> **Antes de compartir texto o capturas**, comprueba que no aparezcan contraseñas, tokens, claves privadas, códigos de autenticación, correos privados, rutas sensibles u otros datos personales. Oculta esa información y nunca publiques credenciales para pedir ayuda.

---

## 43. Comandos que NO debes ejecutar solo porque los encontraste en Internet

Ten especial cuidado con:

```text
git push --force
git reset --hard
git clean -fd
```

Estos comandos pueden sobrescribir historial remoto o eliminar cambios y archivos locales. Que un comando elimine el mensaje de error no significa que haya conservado el trabajo correcto.

No los uses como soluciones rutinarias. Antes de cualquier operación destructiva debes comprender exactamente qué datos afecta, confirmar la rama y el repositorio, conservar copias necesarias y recibir orientación adecuada.

---

## 44. Regla principal para resolver problemas

> 1. **Lee** el mensaje completo.
> 2. Ejecuta **`git status`**.
> 3. **Verifica la carpeta** abierta y la ruta de la terminal.
> 4. **Verifica la rama** con `git branch`.
> 5. **Verifica `origin`** con `git remote -v`.
> 6. **No fuerces nada** para ocultar el problema.
> 7. **Protege tu trabajo** antes de realizar cambios.

---

## 45. Comprobación final

Confirma que puedes realizar cada tarea:

- [ ] Distingo mensajes informativos de errores.
- [ ] Utilizo `git status` como primer diagnóstico.
- [ ] Reviso la rama activa.
- [ ] Reviso `origin` y su URL.
- [ ] Reconozco problemas básicos de `pull` y `push`.
- [ ] Reconozco problemas de autenticación y permisos sin compartir credenciales.
- [ ] Reconozco conflictos y rutas sin fusionar.
- [ ] Retiro un archivo del área de preparación sin borrarlo.
- [ ] Recopilo información útil y segura antes de pedir ayuda.
- [ ] Evito comandos destructivos y soluciones al azar.

Si completaste la lista, puedes diagnosticar los problemas más frecuentes de Git, GitHub y Visual Studio Code de forma segura y ordenada.
