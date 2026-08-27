# 09. Trabajo colaborativo con GitHub

En esta sección aprenderás un flujo básico para colaborar en un mismo repositorio desde Visual Studio Code. También conocerás cómo prevenir, reconocer y resolver de forma introductoria un conflicto.

El ejemplo supone que el equipo tiene permiso para escribir directamente en el repositorio compartido. En proyectos más grandes suelen utilizarse ramas y *pull requests*, que se estudiarán posteriormente.

---

## 1. ¿Qué significa trabajar colaborativamente con Git y GitHub?

Trabajar colaborativamente significa que varias personas participan en un mismo proyecto. Cada integrante puede desarrollar funcionalidades, corregir errores o actualizar documentos.

Git registra los commits de cada persona y permite combinar las distintas contribuciones. GitHub proporciona el repositorio remoto donde el equipo comparte esos commits.

Los comandos no bastan por sí solos. Un equipo también necesita:

- Repartir responsabilidades.
- Comunicar qué se está modificando.
- Mantener actualizadas las copias locales.
- Revisar los cambios antes de publicarlos.
- Resolver conjuntamente las diferencias cuando sea necesario.

Git conserva el historial, pero no puede decidir los objetivos del equipo ni sustituir la comunicación.

---

## 2. Ejemplo de un equipo de trabajo

Imagina un equipo de tres estudiantes:

- **Ana** crea el repositorio en GitHub y organiza el trabajo inicial.
- **Carlos** desarrolla parte de la presentación visual.
- **Luis** agrega comportamiento con JavaScript.

Ana, como propietaria, invita a Carlos y Luis como colaboradores. Cuando ellos aceptan, cada integrante clona el mismo repositorio en su propio computador.

Aunque todos comparten el repositorio remoto, cada persona trabaja en una copia local independiente. Los cambios de una copia solo llegan al equipo después de crear commits y hacer `push`.

---

## 3. Agregar colaboradores en GitHub

La persona propietaria del repositorio puede seguir este procedimiento general:

1. Abre la página principal del repositorio en GitHub.
2. Entra en **Settings**.
3. Busca la sección **Access** y la opción **Collaborators** o una opción equivalente de acceso.
4. Selecciona **Add people** o la acción para agregar una persona.
5. Busca el nombre de usuario o correo de GitHub del integrante.
6. Confirma la invitación.
7. Espera a que la persona invitada la acepte.

Los nombres y la ubicación de las opciones pueden cambiar ligeramente según la interfaz, el idioma y si el repositorio pertenece a una cuenta personal o a una organización.

Invita únicamente a personas que deban participar y verifica cuidadosamente el nombre de usuario antes de conceder acceso.

---

## 4. Aceptar una invitación

La persona invitada recibirá una notificación en GitHub y, según su configuración, un correo electrónico.

Debe abrir la invitación, comprobar el repositorio y la persona propietaria, y seleccionar la opción para aceptarla. Hasta aceptar, es posible que pueda ver un repositorio público, pero no tendrá el acceso de colaborador necesario para hacer `push` directamente.

En un repositorio privado, la invitación aceptada también permite acceder al contenido según los permisos concedidos.

---

## 5. Clonar el repositorio

Cada integrante necesita su propia copia local. Desde GitHub, copia la URL HTTPS mediante **Code → HTTPS**. Luego, desde una carpeta general en la terminal integrada de Visual Studio Code, ejecuta:

```bash
git clone URL_DEL_REPOSITORIO
```

Por ejemplo:

```bash
git clone https://github.com/usuario/proyecto-equipo.git
```

Entra en la carpeta creada:

```bash
cd proyecto-equipo
```

Si el comando `code` está disponible, puedes abrir la carpeta actual con:

```bash
code .
```

Si no está disponible, selecciona **File → Open Folder** y abre la carpeta clonada. Cada integrante debe trabajar dentro de su propia copia; no es necesario compartir una misma carpeta del sistema.

---

## 6. Verificar `origin`

Dentro de la carpeta clonada, ejecuta:

```bash
git remote -v
```

El resultado debe mostrar que `origin` apunta al repositorio compartido:

```text
origin  https://github.com/usuario/proyecto-equipo.git (fetch)
origin  https://github.com/usuario/proyecto-equipo.git (push)
```

Comprueba el propietario y el nombre del repositorio. `origin` es el nombre local convencional de esa conexión remota; no identifica a un integrante ni a una rama.

---

## 7. Regla principal antes de empezar a trabajar

> **Antes de comenzar una tarea en un repositorio compartido, revisa el estado y actualiza tu rama.**

```bash
git status
git pull
```

`git pull` descarga e integra los commits nuevos del remoto. Esto reduce la posibilidad de empezar a trabajar sobre una versión desactualizada.

El directorio de trabajo debería estar limpio antes de actualizar. Si `git status` muestra cambios locales pendientes, revísalos y consérvalos adecuadamente antes de hacer `pull`.

---

## 8. Repartir tareas

Antes de modificar archivos, el equipo debe definir responsabilidades. Por ejemplo:

- Ana trabaja en `index.html`.
- Carlos trabaja en `style.css`.
- Luis trabaja en `script.js`.

Otra opción es repartir funcionalidades completas: autenticación, formulario, menú o documentación.

Separar archivos o funcionalidades reduce la probabilidad de que dos personas cambien simultáneamente el mismo contenido. Sin embargo, todos deben conocer las relaciones entre sus tareas: un cambio en HTML puede requerir ajustes en CSS o JavaScript.

---

## 9. Evitar modificar simultáneamente la misma parte

Si dos personas cambian las mismas líneas de un archivo, Git puede no saber cómo combinar las versiones y producir un conflicto.

Antes de editar una zona compartida, informa al equipo. Si otra persona ya trabaja allí, coordinen quién hará el cambio o dividan la tarea de otra forma.

Git detecta diferencias, pero no sabe cuál implementación cumple mejor los requisitos. La comunicación previene trabajo duplicado y decisiones contradictorias.

---

## 10. Flujo de trabajo de cada integrante

```text
git pull
    ↓
Trabajar y guardar archivos
    ↓
git status
    ↓
git add .
    ↓
git commit -m "..."
    ↓
git pull
    ↓
git push
```

El primer `git pull` actualiza el proyecto antes de la tarea. El segundo comprueba e integra commits que otra persona pudo publicar mientras trabajabas.

Como tu trabajo ya está guardado en un commit antes del segundo `pull`, Git puede comparar ambos historiales. Si aparece un conflicto, debes resolverlo antes de hacer `push`. Ejecuta cada comando por separado y lee su resultado.

---

## 11. Crear commits claros

Utiliza mensajes que describan el propósito del cambio:

```bash
git commit -m "Agregar validación del formulario"
git commit -m "Crear menú de navegación"
git commit -m "Corregir estilos de la página principal"
```

La información de autoría del commit permite identificar quién lo creó y el mensaje explica qué hizo. En conjunto ayudan al equipo a entender quién modificó qué y con qué propósito.

Evita mensajes como `cambios`, `cosas` o `listo`, porque no permiten comprender el historial.

---

## 12. Qué pasa si otra persona hizo cambios

Cuando ejecutas:

```bash
git pull
```

Git descarga los commits remotos y trata de integrarlos en tu rama local.

Si los cambios afectan archivos o líneas diferentes, normalmente Git puede combinarlos automáticamente. Después debes revisar el resultado, ejecutar `git status` y comprobar que el proyecto continúe funcionando.

Una integración automática no sustituye las pruebas. Dos cambios técnicamente combinables aún pueden producir un comportamiento incorrecto al usarse juntos.

---

## 13. Introducción a los conflictos

Un **conflicto de merge** ocurre cuando Git encuentra cambios incompatibles y necesita que una persona decida el resultado final.

Ejemplo:

1. Ana y Carlos parten de la misma versión de `README.md`.
2. Ambos modifican la misma línea y crean un commit.
3. Ana hace `push` primero.
4. Carlos intenta actualizar o subir después.
5. Carlos ejecuta `git pull` para recibir el commit de Ana.
6. Git encuentra dos versiones distintas para la misma línea.

Git detiene la integración porque no puede saber si debe conservar la versión de Ana, la de Carlos o una combinación. Carlos y el equipo deben revisar la intención de ambos cambios.

---

## 14. Cómo reconocer un conflicto

La terminal puede mostrar mensajes como:

```text
CONFLICT (content): Merge conflict in README.md
Automatic merge failed; fix conflicts and then commit the result.
```

`git status` también indicará archivos sin fusionar. En Visual Studio Code, Source Control puede agruparlos bajo **Merge Changes**.

Dentro de un archivo pueden aparecer estas marcas:

```text
<<<<<<< HEAD
Contenido de la versión actual
=======
Contenido de la versión entrante
>>>>>>> origin/main
```

`<<<<<<<`, `=======` y `>>>>>>>` delimitan las dos versiones. Son marcas temporales de Git y **no deben quedar en el archivo final**.

---

## 15. Resolver un conflicto desde Visual Studio Code

Realiza el proceso con calma:

1. Ejecuta `git status` e identifica todos los archivos en conflicto.
2. Abre uno de ellos desde Source Control.
3. Lee la versión actual y la entrante.
4. Consulta al integrante correspondiente si la intención no está clara.
5. Decide si debes conservar una versión, la otra o combinar ambas.
6. Edita el resultado y elimina todas las marcas de conflicto.
7. Guarda el archivo.
8. Revisa que el código tenga sentido y, cuando sea posible, pruébalo.
9. Prepara el archivo resuelto y completa el commit.

Flujo básico para un archivo:

```bash
git status
git add README.md
git commit -m "Resolver conflicto en README"
git push
```

Sustituye `README.md` por el archivo real. No agregues ni confirmes el resultado hasta revisar todos los conflictos. Nunca borres el trabajo de otra persona sin comprenderlo.

---

## 16. Herramientas visuales de VS Code para conflictos

Visual Studio Code puede ofrecer acciones en línea o un editor de combinación de tres vistas. Entre las opciones habituales están:

- **Accept Current Change**.
- **Accept Incoming Change**.
- **Accept Both Changes**.
- **Compare Changes** o una opción para abrir el **Merge Editor**.

En el Merge Editor pueden aparecer paneles llamados **Incoming**, **Current** y **Result**. La ubicación y el nombre exacto de los botones pueden variar según la versión y la vista utilizada.

Estas herramientas ayudan a construir el resultado, pero la decisión sigue siendo humana. Revisa siempre el panel **Result** o el archivo final antes de completar la integración.

---

## 17. Qué significa Current Change

**Current Change** representa normalmente el cambio que ya existe en la rama local actual durante la resolución.

Seleccionar **Accept Current Change** conserva esa versión para el bloque y descarta la versión entrante de ese mismo bloque. No la elijas solo porque dice “Current”: primero confirma que contiene el resultado correcto para el equipo.

---

## 18. Qué significa Incoming Change

**Incoming Change** representa normalmente el cambio que llega desde la rama o versión que se está integrando.

Seleccionar **Accept Incoming Change** conserva la versión entrante para ese bloque y descarta la actual. Revisa quién hizo el cambio, cuál era su objetivo y cómo afecta al resto del proyecto.

---

## 19. Qué significa Both Changes

**Both Changes** permite conservar las dos versiones, normalmente una después de la otra.

Esto no garantiza que el resultado sea correcto. Puede duplicar una línea, una función, una propiedad CSS o una etiqueta HTML. Después de aceptar ambas, edita manualmente el resultado, elimina duplicaciones y comprueba que el orden tenga sentido.

---

## 20. No resolver conflictos a ciegas

> **No selecciones automáticamente Current, Incoming o Both sin leer el código.**

Una elección apresurada puede borrar una corrección, duplicar una función o dejar el proyecto en un estado inválido. El equipo debe decidir qué versión cumple los requisitos y, cuando corresponda, crear una combinación nueva.

Después de resolver, busca cualquier marca restante, guarda, revisa las diferencias y prueba el proyecto antes del commit.

---

## 21. Trabajo con archivos distintos

Cuando cada integrante modifica archivos distintos, es menos probable que Git encuentre cambios incompatibles en las mismas líneas.

Sin embargo, el riesgo no desaparece por completo. Dos archivos diferentes pueden depender entre sí: Carlos podría cambiar un nombre de clase en CSS mientras Ana cambia el HTML que utiliza esa clase.

Por eso, además de dividir tareas, el equipo debe comunicar cambios que afecten contratos, nombres, estructuras y comportamiento compartido.

---

## 22. Importancia de `git status`

Utiliza con frecuencia:

```bash
git status
```

Ejecútalo antes y después de operaciones importantes:

- Antes y después de `git pull`, para conocer el estado local y el resultado de la integración.
- Antes y después de `git add`, para revisar qué se preparará y qué quedó preparado.
- Antes y después de `git commit`, para confirmar el contenido y el estado posterior.
- Antes de `git push`, para detectar conflictos, cambios pendientes o commits sin publicar.

`git status` no modifica el proyecto. Es una de las herramientas más seguras para comprender qué ocurre.

---

## 23. Qué hacer antes de subir cambios

Sigue esta lista de forma consciente:

```bash
git status
git pull
# Resolver conflictos si aparecen
git status
git push
```

1. El primer `git status` confirma que tu trabajo está guardado y el repositorio es el correcto.
2. `git pull` recibe los commits publicados por otras personas.
3. Si aparecen conflictos, revísalos, resuélvelos, pruébalos y completa el commit.
4. El segundo `git status` comprueba que no quedan conflictos ni cambios inesperados.
5. `git push` publica tus commits.

No hagas `push` mientras existan conflictos sin resolver.

---

## 24. ¿Qué pasa si el `push` es rechazado?

Puedes ver mensajes que incluyen:

```text
rejected
failed to push some refs
```

Normalmente significa que el repositorio remoto contiene commits que aún no existen en tu rama local. Git rechaza el envío para evitar sobrescribir ese trabajo.

Revisa primero:

```bash
git status
git pull
```

Si el `pull` integra los cambios automáticamente, revisa y prueba el resultado antes de intentar `git push` otra vez. Si produce conflictos o informa ramas divergentes, detente y resuelve la situación con el equipo.

No utilices `force push`; puede sobrescribir commits de otras personas.

---

## 25. Regla de oro para equipos

> **Antes de trabajar:** actualiza una copia local limpia.

```bash
git status
git pull
```

> **Después de terminar una tarea:** revisa, prepara, confirma, vuelve a actualizar y publica.

```bash
git status
git add .
git status
git commit -m "Descripción clara de la tarea"
git pull
git status
git push
```

Lee el resultado de cada comando. Si un paso falla o produce un conflicto, no continúes automáticamente con el siguiente.

---

## 26. Comunicación del equipo

Es conveniente informar:

- Qué archivo o zona se está modificando.
- Qué funcionalidad se está desarrollando.
- Qué dependencias o estructuras compartidas cambiarán.
- Cuándo se hizo `push` y qué commit se publicó.
- Cuándo apareció o se resolvió un conflicto.
- Si el proyecto requiere una decisión antes de integrar.

El equipo puede usar una reunión breve, una herramienta de tareas o el medio acordado. Lo importante es que la información esté disponible antes de que dos personas realicen trabajo incompatible.

---

## 27. Commits frecuentes pero con sentido

Los commits pequeños y coherentes facilitan:

- Revisar exactamente qué cambió.
- Identificar cuándo se introdujo un error.
- Entender quién modificó qué y con qué propósito.
- Integrar el trabajo de distintas personas.
- Resolver conflictos sobre unidades más pequeñas.

No hagas un commit por cada tecla ni agrupes toda una semana de trabajo en un único commit. Crea uno cuando completes un cambio funcional y reconocible.

---

## 28. No compartir credenciales

Cada integrante debe usar su propia cuenta de GitHub. Esto mantiene una autoría correcta y permite retirar el acceso de una persona sin afectar a las demás.

Nunca compartas:

- Contraseñas.
- Tokens de acceso.
- Claves SSH privadas.
- Códigos de autenticación.
- Credenciales de bases de datos u otros servicios.

Tampoco guardes esos datos en archivos, mensajes de commit, capturas o conversaciones del proyecto. Si una credencial se publica, debe considerarse expuesta y reemplazarse desde el servicio que la emitió.

---

## 29. Flujo visual colaborativo

```text
Integrante A
     ↓
 git pull
     ↓
  Trabaja
     ↓
  Commit
     ↓
 git pull
     ↓
 git push
     ↓
   GitHub
     ↑
 git pull
     ↑
Integrante B
```

GitHub funciona como punto compartido, pero cada integrante conserva su propia copia local. Ambos deben recibir cambios recientes antes de comenzar y antes de publicar cuando el equipo trabaja activamente.

---

## 30. Errores y situaciones frecuentes

### `rejected` o `failed to push some refs`

- **Qué significa:** Git no pudo enviar los commits.
- **Causa probable:** el remoto avanzó y contiene commits que faltan localmente.
- **Acción segura:** ejecuta `git status` y `git pull`; integra o resuelve conflictos antes de volver a subir. No fuerces el envío.

### `merge conflict`

- **Qué significa:** Git no pudo combinar automáticamente cambios incompatibles.
- **Causa probable:** dos versiones modificaron las mismas líneas o realizaron cambios estructuralmente incompatibles.
- **Acción segura:** abre cada archivo en conflicto, compara ambas intenciones, coordina con el equipo, edita el resultado y confirma la resolución.

### `Your branch is behind 'origin/main'`

- **Qué significa:** GitHub contiene commits que faltan en tu rama local.
- **Causa probable:** otra persona publicó cambios o tu copia no se actualizó recientemente.
- **Acción segura:** con el trabajo local protegido, ejecuta `git pull` y revisa el resultado.

### `Already up to date.`

- **Qué significa:** no hay commits remotos nuevos para integrar.
- **Causa probable:** tu rama ya contiene la información remota más reciente conocida por el `pull`.
- **Acción segura:** ninguna; es un mensaje informativo, no un error.

### `Permission denied`

- **Qué significa:** el acceso u operación fue rechazado.
- **Causa probable:** la invitación no fue aceptada, la cuenta no tiene permiso de escritura o la autenticación no corresponde.
- **Acción segura:** confirma la cuenta activa, acepta la invitación y solicita a la persona propietaria que revise el acceso. No compartas credenciales.

### `Repository not found`

- **Qué significa:** GitHub no encuentra un repositorio accesible en la URL indicada.
- **Causa probable:** la URL es incorrecta, el repositorio cambió de nombre, es privado o tu cuenta no tiene acceso.
- **Acción segura:** abre el repositorio en el navegador, verifica tus permisos y copia nuevamente la URL desde **Code → HTTPS**.

---

## 31. Tabla rápida de consulta

| Quiero... | Comando | Qué debo revisar |
| --- | --- | --- |
| Actualizar antes de trabajar | `git pull` | Que el trabajo local esté protegido. |
| Ver cambios y estado | `git status` | Archivos modificados, preparados y conflictos. |
| Preparar los cambios revisados | `git add .` | Que no haya archivos innecesarios o secretos. |
| Guardar una versión local | `git commit -m "mensaje"` | Que el mensaje describa la tarea. |
| Actualizar antes de subir | `git pull` | Si llegaron commits o aparecieron conflictos. |
| Subir commits | `git push` | Que no existan conflictos sin resolver. |
| Ver el origen compartido | `git remote -v` | Que `origin` apunte al repositorio correcto. |

---

## 32. Buenas prácticas para equipos

- Haz `git pull` antes de empezar a trabajar.
- Divide tareas con límites y objetivos claros.
- Comunica qué estás modificando y cuándo publicas.
- Evita modificar innecesariamente las mismas líneas o archivos.
- Crea commits pequeños, coherentes y con mensajes claros.
- No utilices `force push` en el repositorio compartido.
- Resuelve los conflictos leyendo y probando el código.
- Revisa `git status` entre cada etapa importante.
- No publiques credenciales ni información privada.
- Verifica GitHub después del `push` y comunica el resultado al equipo.

---

## 33. Comprobación final

Confirma que puedes realizar cada tarea:

- [ ] Acepto una invitación como colaborador desde mi propia cuenta.
- [ ] Clono el repositorio compartido y verifico `origin`.
- [ ] Hago `git pull` antes de trabajar.
- [ ] Creo commits claros y coherentes.
- [ ] Hago `git push` después de actualizar y revisar el estado.
- [ ] Reconozco un conflicto y sus marcas básicas.
- [ ] Resuelvo de forma básica un conflicto desde Visual Studio Code sin borrar trabajo a ciegas.
- [ ] Comprendo **Current Change**, **Incoming Change** y **Both Changes**.
- [ ] Trabajo sin utilizar `force push` ni comandos destructivos.
- [ ] Coordino tareas, cambios y publicaciones con los demás integrantes.

Si completaste la lista, ya conoces un flujo inicial y seguro para colaborar en GitHub desde Visual Studio Code.
