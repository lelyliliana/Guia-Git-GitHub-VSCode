# 05. Flujo de trabajo diario con Git y GitHub

Esta sección presenta una rutina práctica para guardar correctamente los cambios de un proyecto y publicarlos en GitHub desde la terminal integrada de Visual Studio Code.

El procedimiento supone que el repositorio ya fue creado, tiene al menos un commit y está conectado con GitHub. Si todavía no lo está, consulta [03. Crear el primer repositorio con Git y GitHub](../03-primer-repositorio/README.md) o [04. Subir un proyecto existente a GitHub](../04-subir-proyecto-existente/README.md).

---

## 1. ¿Para qué sirve esta sección?

Esta será una de las rutinas que utilizarás con mayor frecuencia después de crear y conectar el repositorio.

Una situación habitual es la siguiente: abres el proyecto, modificas archivos, agregas una funcionalidad o corriges un error. Después necesitas registrar esos cambios en Git y subir los commits a GitHub para conservarlos y compartirlos.

El ciclo básico consiste en revisar, preparar, confirmar y subir:

1. Revisar qué cambió.
2. Elegir los cambios que formarán parte del commit.
3. Crear un commit con un mensaje claro.
4. Enviar el commit a GitHub.

---

## 2. Antes de comenzar

Realiza estas comprobaciones antes de modificar el repositorio:

1. Abre Visual Studio Code.
2. Selecciona **File → Open Folder** y abre la carpeta raíz correcta.
3. Selecciona **Terminal → New Terminal**.
4. Comprueba que la terminal esté ubicada dentro del proyecto.

### Linux y macOS

```bash
pwd
```

### Windows PowerShell

```powershell
Get-Location
```

La ruta mostrada debe terminar con el nombre de la carpeta del proyecto. Esta verificación evita ejecutar comandos en otro repositorio por equivocación.

---

## 3. Revisar el estado del proyecto

Ejecuta:

```bash
git status
```

Conviene convertir `git status` en una rutina. Es un comando seguro: muestra información y no modifica archivos ni commits.

Su resultado puede incluir:

- **Archivos modificados (*modified*):** archivos conocidos por Git cuyo contenido cambió.
- **Archivos nuevos o sin seguimiento (*untracked*):** archivos que Git todavía no controla.
- **Archivos eliminados (*deleted*):** archivos conocidos por Git que ya no están en la carpeta.
- **Cambios preparados (*staged*):** cambios incluidos en el área de preparación y listos para el próximo commit.
- **Cambios no preparados (*unstaged*):** cambios detectados que todavía no se agregaron al área de preparación.
- **Repositorio limpio (*working tree clean*):** no existen cambios nuevos respecto del último commit.

Lee la salida completa antes de decidir qué hacer.

---

## 4. Hacer los cambios en el proyecto

Trabaja normalmente desde el editor de Visual Studio Code. Puedes:

- Modificar código existente.
- Crear archivos o carpetas.
- Eliminar elementos que ya no se necesitan.
- Actualizar la documentación.
- Corregir errores.
- Agregar una funcionalidad.

Guarda los archivos después de editarlos. En Windows/Linux utiliza `Ctrl + S`; en macOS, `Command + S`.

Git detectará las diferencias entre los archivos guardados y el último commit. Detectar un cambio no significa que Git lo haya incluido automáticamente en un commit.

---

## 5. Revisar nuevamente el estado

Después de guardar tus cambios, ejecuta otra vez:

```bash
git status
```

Revisar antes de agregar archivos permite comprobar que:

- Los cambios esperados aparecen en la lista.
- No modificaste o eliminaste un archivo por accidente.
- No vas a incluir archivos temporales, dependencias o información privada.
- `.gitignore` está excluyendo lo que no debe publicarse.

Si aparece algo inesperado, detente y revísalo antes de continuar.

---

## 6. Agregar los cambios al área de preparación

Para preparar todos los cambios permitidos de la carpeta actual, ejecuta:

```bash
git add .
```

El punto `.` representa la carpeta actual. Git prepara sus archivos nuevos, modificados y eliminados, excepto los archivos nuevos excluidos mediante reglas como `.gitignore`.

También puedes preparar un solo archivo:

```bash
git add nombre-archivo
```

Por ejemplo:

```bash
git add README.md
```

Agregar archivos individualmente es preferible cuando realizaste varios cambios que no pertenecen al mismo propósito. Así puedes crear commits separados y fáciles de entender, por ejemplo uno para corregir un error y otro para actualizar la documentación.

`git add` no crea el commit ni sube archivos a GitHub. Solamente selecciona el contenido del próximo commit.

---

## 7. Verificar qué quedó preparado

Ejecuta:

```bash
git status
```

Los elementos preparados deben aparecer bajo **Changes to be committed** o **Cambios a ser confirmados**. Los que aún no están preparados aparecerán en otra sección.

Revisa la lista completa. El commit incluirá solamente la versión preparada de cada archivo. Si modificas un archivo nuevamente después de ejecutar `git add`, tendrás que volver a agregarlo si quieres incluir esa última modificación.

No continúes si ves contraseñas, tokens, claves privadas, archivos `.env` con secretos o elementos que no deberían publicarse.

---

## 8. Crear un commit

Cuando el área de preparación sea correcta, crea el commit:

```bash
git commit -m "Descripción clara del cambio"
```

Un commit es un punto de guardado en el historial local del repositorio. Un buen mensaje indica qué cambió y permite comprender el historial sin abrir todos los archivos.

Ejemplos de mensajes claros:

```bash
git commit -m "Corregir validación del formulario"
git commit -m "Agregar estilos responsivos"
git commit -m "Actualizar documentación del proyecto"
```

Evita mensajes demasiado generales:

```bash
git commit -m "cambios"
git commit -m "cosas"
git commit -m "actualización"
```

Estos mensajes no explican qué se hizo y dificultan localizar una modificación más adelante. Procura completar mentalmente la frase: “Este commit permite…”. Por ejemplo: “Este commit permite **corregir la validación del formulario**”.

---

## 9. Subir los cambios a GitHub

Después de crear el commit, ejecuta:

```bash
git push
```

`git push` envía a GitHub los commits locales que todavía no existen en el repositorio remoto.

Si anteriormente se vinculó la rama local `main` con `origin/main`, normalmente no es necesario volver a escribir:

```bash
git push -u origin main
```

La opción `-u` se utiliza habitualmente en el primer envío para establecer esa relación. Los envíos posteriores pueden realizarse con `git push`.

---

## 10. Verificar el resultado

Después de que `git push` termine correctamente:

1. Abre el repositorio en GitHub.
2. Actualiza la página del navegador.
3. Comprueba que aparece el mensaje del commit reciente.
4. Abre los archivos modificados y verifica su contenido.

Esta comprobación confirma que no solo creaste el commit local, sino que también lo publicaste en el repositorio correcto.

---

## 11. El ciclo de trabajo diario

```text
Abrir proyecto
      ↓
Modificar archivos
      ↓
git status
      ↓
git add .
      ↓
git status
      ↓
git commit -m "..."
      ↓
git push
      ↓
Verificar en GitHub
```

Esta secuencia puede repetirse muchas veces durante el desarrollo. No es necesario esperar hasta terminar todo el proyecto: cada cambio completo y coherente puede registrarse en su propio commit.

---

## 12. ¿Cada cuánto hacer commits?

No existe un número exacto de minutos o archivos. Para comenzar, crea un commit cuando completes un cambio que tenga sentido por sí mismo.

Momentos adecuados pueden ser:

- Después de corregir un error específico.
- Después de terminar una función pequeña.
- Después de agregar y comprobar una nueva página.
- Después de actualizar una sección completa de la documentación.
- Antes de comenzar una tarea diferente.
- Al terminar una sesión de trabajo con el proyecto funcionando.

Evita acumular en un solo commit muchas modificaciones sin relación, porque será difícil entenderlas o revisarlas. Tampoco necesitas crear un commit por cada tecla o ajuste mínimo. El objetivo es producir commits pequeños, pero significativos.

No esperes hasta finalizar todo el proyecto: hacerlo elimina gran parte de la utilidad del historial de Git.

---

## 13. ¿Qué pasa si `git status` dice que no hay cambios?

Puedes encontrar este mensaje:

```text
nothing to commit, working tree clean
```

**No es un error.** Significa que todos los cambios guardados ya están registrados en commits o que no existen modificaciones nuevas.

Si esperabas ver un cambio, comprueba que guardaste el archivo en Visual Studio Code y que la terminal corresponde al proyecto correcto. También revisa si `.gitignore` está excluyendo un archivo nuevo.

---

## 14. ¿Qué pasa si olvidé hacer `git add`?

Si ejecutas `git commit` sin preparar cambios, Git puede indicar que existen modificaciones no preparadas. Los archivos modificados no entrarán automáticamente en el commit.

Revisa y sigue el flujo correcto:

```bash
git status
git add .
git commit -m "Descripción clara del cambio"
git push
```

No ejecutes los comandos de forma mecánica: lee `git status` antes de `git add .` y verifica que todos los archivos correspondan al mismo cambio.

---

## 15. ¿Cómo saber si tengo commits que todavía no he subido?

Después de crear un commit, `git status` puede mostrar:

```text
Your branch is ahead of 'origin/main' by 1 commit.
```

Significa que existe un commit en la rama local `main` que todavía no está en GitHub. El trabajo sí está guardado en el historial local, pero falta publicarlo.

Ejecuta:

```bash
git push
```

Después del envío, `git status` debería indicar que la rama está actualizada con `origin/main`, siempre que no existan otros cambios locales.

---

## 16. Diferencia entre guardar en VS Code, `commit` y `push`

Estos tres pasos guardan información en lugares distintos y **no son equivalentes**.

| Acción | Dónde guarda | Qué consigue |
| --- | --- | --- |
| `Ctrl + S` o `Command + S` | En el archivo del computador | Conserva la edición actual en el disco. |
| `git commit` | En el historial Git local | Registra un punto del historial con los cambios preparados. |
| `git push` | En el repositorio remoto de GitHub | Envía los commits locales para publicarlos y respaldarlos remotamente. |

Una comparación sencilla:

- **Guardar** es escribir la versión actual en tu cuaderno local.
- **Commit** es colocar una etiqueta fechada en un conjunto de páginas para poder encontrar ese estado después.
- **Push** es enviar una copia de esas páginas etiquetadas al repositorio compartido en GitHub.

Por lo tanto:

- Guardar un archivo no crea un commit.
- Crear un commit no lo envía automáticamente a GitHub.
- `git push` solo puede enviar commits que ya existen localmente.

---

## 17. Consultar el historial

Para ver los commits de forma resumida, ejecuta:

```bash
git log --oneline
```

Cada línea muestra un identificador abreviado y el mensaje de un commit. Los commits más recientes aparecen primero.

Para mostrar solamente los últimos cinco commits, utiliza:

```bash
git log --oneline -5
```

Un resultado podría ser:

```text
4a8c102 Actualizar documentación del proyecto
d093f61 Corregir validación del formulario
7be21aa Agregar formulario de contacto
```

Los identificadores serán diferentes en cada repositorio. Si la vista ocupa toda la terminal, presiona `q` para salir.

---

## 18. Buenas prácticas del trabajo diario

- Ejecuta `git status` con frecuencia y especialmente antes de `git add`, `commit` y `push`.
- Lee los mensajes completos de Git; suelen explicar el estado y sugerir el paso siguiente.
- Crea commits pequeños, coherentes y con un propósito reconocible.
- Escribe mensajes claros que indiquen qué cambió.
- Revisa qué archivos se prepararon antes de confirmar el commit.
- Mantén `.gitignore` adecuado a la tecnología del proyecto.
- Nunca prepares ni publiques contraseñas, tokens, claves API, claves privadas o archivos `.env` con secretos.
- Haz `push` después de completar una sesión importante para conservar los commits en GitHub.
- Verifica el resultado en GitHub, especialmente si trabajas con otras personas.

Si un secreto llegó a un commit, no basta con borrarlo en otro commit: reemplaza o revoca la credencial en el servicio que la generó y solicita ayuda para revisar el historial.

---

## 19. Errores y situaciones frecuentes

### `nothing to commit, working tree clean`

- **Qué significa:** no existen cambios nuevos respecto del último commit.
- **Tipo:** mensaje informativo, no es un error.
- **Qué hacer:** no hagas otro commit. Si esperabas cambios, guarda los archivos y revisa la carpeta y `.gitignore`.

### `Your branch is ahead of 'origin/main'`

- **Qué significa:** tienes uno o más commits locales que todavía no están en GitHub.
- **Tipo:** mensaje informativo.
- **Qué hacer:** revisa que estás en el repositorio correcto y ejecuta `git push` cuando quieras publicarlos.

### `Everything up-to-date`

- **Qué significa:** GitHub ya contiene todos los commits locales de la rama que intentaste subir.
- **Tipo:** mensaje informativo, no es un error.
- **Qué hacer:** no se requiere ninguna acción. Si esperabas subir cambios, comprueba que guardaste, preparaste y confirmaste esos cambios.

### `Changes not staged for commit`

- **Qué significa:** existen modificaciones conocidas por Git, pero no están en el área de preparación.
- **Tipo:** descripción del estado, no es un fallo de Git.
- **Qué hacer:** revisa los archivos y agrega solo los que deban formar parte del commit con `git add archivo` o `git add .`.

### `Untracked files`

- **Qué significa:** existen archivos nuevos que Git todavía no controla.
- **Tipo:** descripción del estado.
- **Qué hacer:** revísalos. Agrega los que pertenezcan al proyecto y coloca en `.gitignore` los que no deban controlarse. Nunca agregues secretos.

---

## 20. Tabla rápida de consulta

| Quiero... | Comando |
| --- | --- |
| Ver el estado del proyecto | `git status` |
| Agregar todos los cambios de la carpeta actual | `git add .` |
| Agregar un archivo específico | `git add archivo` |
| Agregar `README.md` | `git add README.md` |
| Crear un commit | `git commit -m "mensaje"` |
| Subir los commits a GitHub | `git push` |
| Ver el historial resumido | `git log --oneline` |
| Ver los últimos cinco commits | `git log --oneline -5` |

---

## 21. Rutina recomendada

> **Cada vez que termines un cambio importante**, guarda los archivos y sigue esta rutina después de revisar que no contengan información privada:

```bash
git status
git add .
git status
git commit -m "Descripción del cambio"
git push
```

Cada línea cumple una función:

1. El primer `git status` muestra qué cambió.
2. `git add .` prepara los cambios de la carpeta actual que formarán parte del commit.
3. El segundo `git status` permite verificar exactamente qué quedó preparado.
4. `git commit` registra esos cambios en el historial local con un mensaje claro.
5. `git push` envía los commits pendientes a GitHub.

La revisión entre pasos es parte de la rutina. No conviene copiar y ejecutar todos los comandos sin leer sus resultados.

---

## 22. Comprobación final

Confirma que puedes realizar cada tarea:

- [ ] Identifico los archivos modificados, nuevos y eliminados mediante `git status`.
- [ ] Agrego todos los cambios o archivos individuales al área de preparación.
- [ ] Verifico el área de preparación antes de crear un commit.
- [ ] Creo commits con los cambios seleccionados.
- [ ] Escribo mensajes de commit claros y específicos.
- [ ] Utilizo `git push` para publicar los commits en GitHub.
- [ ] Distingo entre guardar un archivo, crear un commit y hacer push.
- [ ] Interpreto los mensajes más comunes de `git status`.
- [ ] Consulto el historial con `git log --oneline`.

Si completaste la lista, ya puedes utilizar el flujo diario básico de Git y GitHub desde Visual Studio Code.
