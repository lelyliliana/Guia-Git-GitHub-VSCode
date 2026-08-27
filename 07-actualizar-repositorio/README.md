# 07. Actualizar un repositorio con `git pull`

En esta sección aprenderás a traer a tu computador los cambios nuevos de un repositorio de GitHub. El objetivo principal es actualizar el proyecto sin poner en riesgo el trabajo local.

El procedimiento supone que el repositorio ya fue clonado o conectado con GitHub. Si todavía no tienes una copia local, consulta [06. Clonar un repositorio desde GitHub](../06-clonar-repositorio/README.md).

---

## 1. ¿Cuándo necesito actualizar un repositorio?

Debes actualizar tu copia local cuando GitHub contiene commits que todavía no existen en tu computador. Esto puede ocurrir cuando:

- La profesora actualizó un repositorio de ejemplo o de apoyo.
- Otro integrante del equipo realizó cambios y los subió a GitHub.
- Trabajas desde varios computadores y publicaste cambios desde otro equipo.
- Alguien integró una contribución nueva en el repositorio remoto.

Actualizar antes de comenzar reduce la posibilidad de trabajar sobre una versión antigua y encontrar diferencias inesperadas al intentar subir tus cambios.

---

## 2. Abrir el proyecto correcto en Visual Studio Code

Abre Visual Studio Code y selecciona:

**File → Open Folder**

Elige la carpeta raíz del repositorio. Debe ser la carpeta principal que contiene todos los archivos del proyecto y la carpeta oculta `.git`.

Comprueba en el panel **Explorer** que aparecen el nombre y la estructura esperados. No abras solamente un archivo ni una subcarpeta aislada.

---

## 3. Abrir la terminal integrada

En la barra de menú selecciona:

**Terminal → New Terminal**

La terminal aparecerá normalmente en la parte inferior de Visual Studio Code y debería quedar ubicada en la carpeta raíz abierta. Antes de actualizar, verifica el repositorio y su estado.

---

## 4. Verificar que se está dentro del repositorio correcto

Ejecuta:

```bash
git status
```

Git debe reconocer la rama actual y mostrar el estado de los archivos. Por ejemplo:

```text
On branch main
Your branch is up to date with 'origin/main'.
nothing to commit, working tree clean
```

El nombre de la rama puede ser diferente. Si aparece este mensaje:

```text
fatal: not a git repository (or any of the parent directories): .git
```

la terminal no está dentro de un repositorio Git. Revisa la carpeta abierta y la ruta antes de continuar. No ejecutes `git pull` desde una ubicación que no reconoces.

---

## 5. Verificar la conexión con GitHub

Consulta los repositorios remotos configurados:

```bash
git remote -v
```

En un repositorio clonado normalmente verás algo similar a:

```text
origin  https://github.com/usuario/nombre-repositorio.git (fetch)
origin  https://github.com/usuario/nombre-repositorio.git (push)
```

`origin` es el nombre corto del remoto principal. La URL indica el repositorio de GitHub desde el cual se recibirán cambios y hacia el cual se intentarán enviar commits.

Comprueba el usuario u organización y el nombre del repositorio. Si la URL no corresponde al proyecto esperado, detente y revisa la configuración antes de descargar o subir información.

---

## 6. Revisar si existen cambios locales antes de actualizar

Ejecuta nuevamente:

```bash
git status
```

Esta revisión protege tu trabajo local antes de ejecutar `git pull`. Puedes encontrar:

- **`working tree clean`:** no hay cambios locales sin confirmar.
- **Archivos modificados:** su contenido cambió desde el último commit.
- **Archivos sin seguimiento (*untracked*):** Git todavía no controla esos archivos nuevos.
- **Cambios preparados (*staged*):** ya se agregaron al área de preparación, pero todavía no forman parte de un commit.

El escenario más sencillo para actualizar es un directorio de trabajo limpio. Si hay cambios locales, un cambio remoto sobre los mismos archivos puede impedir la actualización o producir conflictos.

No ignores la salida de `git status`. Primero entiende y guarda adecuadamente tu trabajo cuando corresponda.

---

## 7. Obtener y aplicar los cambios remotos

Si confirmaste que estás en el repositorio y la rama correctos, ejecuta:

```bash
git pull
```

En lenguaje sencillo, `git pull` realiza dos tareas relacionadas:

1. Descarga información y commits nuevos desde el repositorio remoto configurado.
2. Intenta integrar esos commits en la rama local actual.

Git utilizará normalmente la rama remota vinculada, por ejemplo `origin/main`. Lee el resultado completo antes de modificar archivos o ejecutar otro comando.

---

## 8. Resultado cuando no hay cambios nuevos

Si la rama local ya contiene los mismos commits que la rama remota, Git puede mostrar:

```text
Already up to date.
```

**No es un error.** Significa que no había commits nuevos para descargar e integrar y que el proyecto local ya estaba actualizado respecto de esa rama remota.

---

## 9. Resultado cuando sí existen cambios

Si GitHub contiene commits nuevos, Git mostrará información sobre la descarga y la integración. Un resultado sencillo puede incluir:

```text
Updating a1b2c3d..d4e5f6a
Fast-forward
 README.md | 4 +++-
 1 file changed, 3 insertions(+), 1 deletion(-)
```

Los identificadores, archivos y cantidades serán diferentes. `Fast-forward` indica que Git pudo avanzar la rama local hasta el estado remoto sin crear un commit de integración adicional.

Después del `pull`, los archivos visibles en Visual Studio Code pueden cambiar: podrían aparecer líneas nuevas, correcciones, archivos creados o archivos eliminados por los commits recibidos. Revisa el proyecto antes de continuar trabajando.

---

## 10. Verificar después del `pull`

Consulta de nuevo el estado:

```bash
git status
```

Si la integración terminó y no tenías otros cambios, normalmente verás que la rama está actualizada y el directorio de trabajo está limpio.

Consulta los cinco commits más recientes:

```bash
git log --oneline -5
```

Los commits descargados deberían aparecer en las primeras líneas. Cada línea contiene un identificador abreviado y el mensaje del commit. Si la vista ocupa la terminal, presiona `q` para salir.

---

## 11. Diferencia entre `git pull` y `git push`

Los comandos mueven commits en direcciones opuestas:

| Comando | Dirección | Función |
| --- | --- | --- |
| `git pull` | GitHub → computador | Descarga e integra cambios remotos en la rama local. |
| `git push` | Computador → GitHub | Envía los commits locales al repositorio remoto. |

Una forma breve de recordarlo:

- **Pull**: traer hacia tu computador.
- **Push**: enviar hacia GitHub.

Los estudiantes suelen confundirlos, pero no son intercambiables. `git pull` no publica tu trabajo y `git push` no actualiza primero tus archivos con los cambios de otras personas.

---

## 12. ¿Cuándo hacer `git pull`?

Es una buena práctica ejecutar `git pull`:

- Antes de comenzar una sesión en un proyecto colaborativo.
- Cuando sabes que otra persona actualizó el repositorio.
- Antes de subir cambios propios en un proyecto compartido, después de guardar coherentemente el trabajo local.
- Cuando la profesora informa que actualizó un repositorio de apoyo.
- Al cambiar de computador para continuar con un repositorio que utilizas en varios equipos.

Antes de cada `pull`, utiliza `git status`. Actualizar con un directorio de trabajo limpio suele ser más sencillo y seguro.

---

## 13. Flujo recomendado al comenzar a trabajar

```text
Abrir proyecto
      ↓
git status
      ↓
git pull
      ↓
Trabajar en archivos
      ↓
git status
      ↓
git add .
      ↓
git commit
      ↓
git push
```

Este flujo es especialmente útil en proyectos colaborativos, porque parte de la versión remota más reciente antes de crear nuevos cambios locales.

Cada paso requiere revisar el resultado del anterior. Si `git status` muestra trabajo local pendiente o `git pull` informa un conflicto, detente y resuelve esa situación antes de continuar.

---

## 14. ¿Qué pasa si tengo cambios locales?

Git compara los cambios locales con los remotos. Si ambos afectan archivos o líneas relacionadas, puede impedir el `pull` o solicitar que resuelvas un conflicto.

Empieza siempre por:

```bash
git status
```

Lee qué archivos están modificados, preparados o sin seguimiento. Si completaste un cambio coherente, revisa los archivos, agrégalos y crea un commit con un mensaje claro antes de actualizar. De esa manera, el trabajo queda registrado en el historial local.

Si el trabajo todavía no está listo para un commit o no sabes de dónde provienen los cambios, no borres archivos ni fuerces la operación. Conserva una copia segura si es necesario y solicita orientación para elegir cómo guardar temporalmente o integrar el trabajo.

---

## 15. ¿Qué es un conflicto?

Un **conflicto** ocurre cuando Git no puede integrar automáticamente dos versiones de un cambio.

Por ejemplo, tú modificaste una línea de `README.md` en tu computador y otra persona modificó la misma línea y la publicó en GitHub. Git no puede decidir por sí solo cuál versión debe conservarse.

Cuando sucede, Git detiene la integración y marca los archivos que requieren una decisión humana. No significa necesariamente que el trabajo se perdió. Debes revisar las dos versiones, elegir o combinar el contenido correcto y completar el proceso con cuidado.

Los conflictos se estudiarán paso a paso en una sección posterior de esta guía.

---

## 16. Error: `local changes would be overwritten by merge`

El mensaje puede verse de forma similar a:

```text
error: Your local changes to the following files would be overwritten by merge:
    nombre-archivo
Please commit your changes or stash them before you merge.
Aborting
```

**Qué significa:** la actualización reemplazaría cambios locales que todavía no están protegidos en el historial, por lo que Git cancela la integración.

**Por qué ocurre:** el repositorio remoto y tu directorio de trabajo modifican archivos relacionados.

**Acción segura:** ejecuta `git status`, abre los archivos indicados y determina qué trabajo local necesitas conservar. Si ese cambio está completo, prepáralo y crea un commit antes de intentar actualizar otra vez. Si no comprendes el origen de los cambios, detente y solicita ayuda.

Git está protegiendo tu trabajo. No borres archivos ni fuerces la integración para eliminar el mensaje.

---

## 17. Error: `Your local changes would be overwritten`

Esta frase puede aparecer en mensajes relacionados con una integración, cambio de rama u otra operación.

**Qué significa:** Git detectó que la operación solicitada podría sobrescribir modificaciones locales.

**Causa probable:** existen archivos modificados o preparados que entran en contacto con los cambios que Git intentaría aplicar.

**Acción segura:** revisa primero:

```bash
git status
```

Guarda los archivos en Visual Studio Code, revisa las diferencias y crea un commit cuando los cambios formen una unidad coherente. Si todavía no deben confirmarse, no continúes hasta decidir cómo conservarlos. La cancelación protege el contenido local.

---

## 18. Error: `failed to pull` o ramas divergentes

Git puede informar que las ramas son **divergentes** cuando el historial local y el remoto avanzaron de manera diferente: existen commits locales que GitHub no tiene y commits remotos que tu computador no tiene.

En versiones actuales de Git también puede aparecer un mensaje que solicita elegir una estrategia para reconciliar ramas divergentes.

Este escenario no se resuelve correctamente escogiendo comandos al azar. Primero debes revisar:

- Qué commits existen localmente.
- Qué commits llegaron al remoto.
- Si ambos grupos de cambios deben conservarse.
- Qué estrategia de integración utiliza el proyecto o el equipo.

No utilices envío forzado, `reset --hard` ni operaciones que reemplacen el historial. Solicita orientación antes de elegir entre una integración mediante *merge* o *rebase*; ambos conceptos se tratarán más adelante.

---

## 19. Diferencia entre `git fetch` y `git pull`

| Comando | Qué hace | ¿Cambia inmediatamente los archivos de la rama actual? |
| --- | --- | --- |
| `git fetch` | Descarga información, ramas y commits remotos para actualizar las referencias remotas. | No. |
| `git pull` | Descarga los cambios remotos e intenta integrarlos en la rama local actual. | Sí, si hay cambios que integrar. |

`git fetch` permite consultar de forma segura que el remoto avanzó sin integrar inmediatamente esos cambios en tu rama de trabajo.

Para el flujo básico del curso se utilizará principalmente `git pull`. `git fetch` se presenta para que comprendas que descargar información e integrarla pueden ser pasos separados.

---

## 20. Ver cambios remotos de forma segura

Para actualizar la información conocida sobre el remoto sin integrar cambios, ejecuta:

```bash
git fetch
```

Después consulta:

```bash
git status
```

Si la rama remota tiene commits nuevos y existe un vínculo de seguimiento, Git puede mostrar algo similar a:

```text
Your branch is behind 'origin/main' by 2 commits, and can be fast-forwarded.
```

Esto informa que `origin/main` avanzó dos commits y que todavía no los has integrado en `main`. `git fetch` no reemplazó tus archivos de trabajo.

Cuando el directorio de trabajo esté en un estado seguro y comprendas el resultado, podrás utilizar `git pull` para integrar esos cambios.

---

## 21. Trabajo colaborativo: regla práctica

> **Antes de empezar a trabajar en un repositorio compartido:** revisa `git status` y, si el estado local permite actualizar con seguridad, ejecuta `git pull`.

```bash
git status
git pull
```

> **Antes de subir tu trabajo:** ejecuta `git status` y verifica que el proyecto esté en un estado coherente, que los commits sean los correctos y que no estés publicando secretos.

```bash
git status
git push
```

Esta regla no sustituye la lectura de los mensajes de Git. Si existen cambios locales, conflictos o ramas divergentes, resuelve la situación antes de continuar.

---

## 22. Errores y mensajes frecuentes

### `Already up to date.`

- **Significado:** no existen commits remotos nuevos para integrar.
- **Tipo:** mensaje informativo; no es un error.
- **Acción:** ninguna. Puedes comenzar a trabajar.

### `Your branch is behind 'origin/main'`

- **Significado:** la rama remota contiene commits que todavía no están en la rama local.
- **Tipo:** mensaje informativo sobre una diferencia.
- **Acción:** revisa `git status`; si el trabajo local está en un estado seguro, utiliza `git pull` para actualizar.

### `Your branch is up to date with 'origin/main'`

- **Significado:** la rama local y su rama remota vinculada contienen los mismos commits conocidos.
- **Tipo:** mensaje informativo.
- **Acción:** no necesitas actualizar por ese motivo. Ten presente que `git fetch` o `git pull` es lo que consulta información nueva del remoto.

### `local changes would be overwritten`

- **Significado:** la operación podría reemplazar modificaciones locales.
- **Tipo:** error de protección; Git cancela la operación.
- **Acción:** ejecuta `git status`, revisa los archivos y guarda el trabajo mediante un commit cuando corresponda. No fuerces ni borres cambios.

### `divergent branches`

- **Significado:** hay commits diferentes tanto en la rama local como en la remota.
- **Tipo:** situación que requiere una decisión de integración.
- **Acción:** revisa ambos lados y consulta la estrategia del equipo. No uses comandos destructivos o envío forzado.

### `fatal: not a git repository`

- **Significado:** la terminal no está dentro de una carpeta reconocida como repositorio Git.
- **Tipo:** error de ubicación o de inicialización.
- **Acción:** abre la carpeta raíz correcta en Visual Studio Code. Si esperabas un repositorio clonado, verifica que la carpeta contenga su directorio `.git`.

---

## 23. Tabla rápida de consulta

| Quiero... | Comando |
| --- | --- |
| Ver el estado local y la relación con la rama remota | `git status` |
| Ver el repositorio remoto configurado | `git remote -v` |
| Actualizar el proyecto descargando e integrando cambios | `git pull` |
| Consultar y descargar información remota sin integrarla | `git fetch` |
| Ver los cinco commits más recientes | `git log --oneline -5` |
| Subir commits locales | `git push` |

---

## 24. Flujo visual: `pull` frente a `push`

```text
             GitHub
               │
      git pull ↓ ↑ git push
               │
           Computador
```

`git pull` trae e integra cambios desde GitHub hacia el computador. `git push` envía commits desde el computador hacia GitHub.

---

## 25. Comprobación final

Confirma que puedes realizar cada tarea:

- [ ] Identifico cuándo necesito actualizar un repositorio local.
- [ ] Verifico el estado y la carpeta antes de actualizar.
- [ ] Ejecuto `git pull` y leo su resultado.
- [ ] Interpreto `Already up to date.` como un mensaje informativo.
- [ ] Distingo la dirección y el propósito de `git pull` y `git push`.
- [ ] Comprendo que `git fetch` descarga información sin integrarla inmediatamente.
- [ ] Identifico de forma básica cuándo puede existir un conflicto.
- [ ] Sé que no debo forzar una operación sin comprender el problema y proteger primero el trabajo local.

Si completaste la lista, ya puedes actualizar de forma consciente y segura un repositorio local desde la terminal integrada de Visual Studio Code.
