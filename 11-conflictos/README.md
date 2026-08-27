# 11. Resolver conflictos en Git

En esta sección aprenderás a reconocer y resolver conflictos de Git desde Visual Studio Code. El objetivo es conservar el trabajo válido de todas las personas y completar la integración de forma consciente.

---

## 1. ¿Qué es un conflicto?

Git puede integrar automáticamente muchos cambios. Sin embargo, algunas veces dos versiones modifican de manera incompatible la misma parte de un archivo y Git no sabe cuál debe quedar en el resultado.

En ese momento Git detiene la integración y solicita que una persona revise las versiones y decida qué contenido conservar o combinar.

Un conflicto **no significa que el proyecto esté perdido**. Git mantiene información de ambas versiones para que puedas compararlas. La resolución forma parte normal del trabajo con ramas y equipos.

---

## 2. Situación típica de conflicto

Imagina este caso:

1. Ana y Carlos parten de la misma versión de `README.md`.
2. Ambos modifican la misma línea en sus copias locales.
3. Ana crea un commit y hace `push` primero.
4. Carlos también tiene su modificación confirmada localmente.
5. Carlos ejecuta `git pull` para recibir el cambio de Ana.

Git encuentra dos contenidos diferentes para la misma línea: el commit local de Carlos y el commit remoto de Ana. No puede conocer la intención del equipo ni elegir cuál texto es correcto, por lo que marca el conflicto para que Carlos lo resuelva.

---

## 3. ¿Cuándo pueden aparecer conflictos?

Los conflictos pueden aparecer durante operaciones que intentan combinar historiales o aplicar cambios, por ejemplo:

- Al ejecutar `git pull` y recibir commits incompatibles con los commits locales.
- Al ejecutar `git merge` para integrar una rama.
- Durante el trabajo colaborativo, cuando varias personas cambian el mismo contenido.
- Al integrar ramas de funcionalidades diferentes en una rama principal.

No todos los `pull` o merges producen conflictos. Git solo pide intervención cuando no puede construir con seguridad un resultado automático.

---

## 4. Cómo reconocer un conflicto

La terminal puede mostrar mensajes similares a:

```text
CONFLICT (content): Merge conflict in README.md
Automatic merge failed; fix conflicts and then commit the result.
```

Las expresiones principales indican:

- **`CONFLICT (content)`:** existe contenido incompatible en un archivo.
- **`Automatic merge failed`:** Git no pudo completar automáticamente la integración.
- **`fix conflicts and then commit the result`:** debes resolver los archivos y después confirmar el resultado.

Los textos exactos pueden variar según la operación y la versión de Git. Ante cualquier duda, lee toda la salida y ejecuta `git status`.

---

## 5. Primer paso: no entrar en pánico ni borrar archivos

Cuando aparezca un conflicto:

1. Detén la secuencia de comandos que estabas ejecutando.
2. No borres archivos ni carpetas.
3. No intentes reemplazar el historial.
4. Lee el mensaje completo.
5. Consulta el estado:

```bash
git status
```

Git conserva las versiones necesarias para resolver. Tu primera tarea es identificar qué archivos requieren atención, no hacer desaparecer rápidamente el mensaje.

---

## 6. Usar `git status` durante un conflicto

Ejecuta:

```bash
git status
```

El resultado puede incluir:

```text
Unmerged paths:
  both modified:   README.md
```

- **`Unmerged paths`:** existen archivos cuya integración no está terminada.
- **`both modified`:** las dos versiones modificaron el archivo y Git necesita una resolución.

`git status` también suele indicar que estás realizando un merge y sugiere resolver los archivos y usar `git add`. Puedes ejecutarlo tantas veces como sea necesario; no modifica el proyecto.

---

## 7. Marcas de conflicto dentro del archivo

Cuando abres un archivo en conflicto, puedes encontrar tres marcas:

```text
<<<<<<< HEAD
Contenido de la versión actual
=======
Contenido de la versión entrante
>>>>>>> origin/main
```

- `<<<<<<< HEAD` inicia normalmente la zona de la versión actual.
- `=======` separa las dos versiones.
- `>>>>>>> origin/main` termina la zona entrante e indica su origen cuando está disponible.

Las etiquetas pueden contener nombres diferentes, como el de otra rama o un identificador. Estas marcas son ayudas temporales y no deben permanecer en el archivo final.

---

## 8. Ejemplo completo de conflicto

La versión local contiene:

```html
<h1>Bienvenidos al curso</h1>
```

La versión entrante contiene:

```html
<h1>Bienvenidos al proyecto</h1>
```

Git puede representar el conflicto así:

```text
<<<<<<< HEAD
<h1>Bienvenidos al curso</h1>
=======
<h1>Bienvenidos al proyecto</h1>
>>>>>>> origin/main
```

Una resolución posible, después de consultar el objetivo del equipo, sería combinar la intención en una sola línea:

```html
<h1>Bienvenidos al proyecto del curso</h1>
```

El resultado final ya no contiene las marcas ni las dos alternativas incompatibles.

---

## 9. Current Change

En Visual Studio Code, **Current Change** representa generalmente el contenido de la rama que estaba activa cuando comenzó la integración.

En un `git pull`, suele corresponder a la versión local actual. En otros tipos de integración, el contexto puede variar; revisa los nombres de las ramas y el contenido antes de decidir.

---

## 10. Incoming Change

**Incoming Change** representa normalmente el cambio que intenta incorporarse desde la otra rama o versión.

Durante un `pull`, suele provenir de la rama remota. Durante un merge local, proviene de la rama indicada en `git merge nombre-rama`.

“Incoming” no significa automáticamente “más correcto” ni “más reciente para todos los propósitos”. Debes leer ambas alternativas.

---

## 11. Accept Current Change

**Accept Current Change** conserva la versión actual del bloque y retira la alternativa entrante de ese bloque.

Selecciona esta opción solamente después de comprobar que el contenido actual cumple el objetivo y que no elimina una contribución necesaria. Si no conoces la intención del cambio entrante, consulta a quien lo creó.

---

## 12. Accept Incoming Change

**Accept Incoming Change** conserva la versión que se está integrando y retira la actual para ese bloque.

Antes de utilizarla, verifica que la versión entrante realmente deba sustituir a la local y que no se pierda parte útil de tu trabajo.

---

## 13. Accept Both Changes

**Accept Both Changes** conserva normalmente ambos bloques, uno después del otro.

Esta opción no garantiza una resolución correcta. Puede producir texto repetido, dos funciones con el mismo nombre, etiquetas HTML duplicadas o instrucciones contradictorias. Después de aceptarla, edita manualmente el resultado y comprueba que tenga sentido.

---

## 14. Comparar cambios antes de decidir

Visual Studio Code resalta los bloques y puede ofrecer una comparación en línea o un **Merge Editor** con varias vistas.

Antes de elegir:

- Lee el bloque completo, no solo la línea marcada.
- Revisa el archivo alrededor del conflicto.
- Comprueba qué tarea pretendía resolver cada versión.
- Consulta el historial o habla con el equipo si falta contexto.
- Observa el resultado que quedaría después de la elección.

Nunca selecciones una opción únicamente para hacer desaparecer el conflicto. El objetivo es construir el contenido correcto.

---

## 15. Resolver manualmente

También puedes editar directamente el archivo. Para cada bloque en conflicto:

1. Conserva la parte correcta de la versión actual.
2. Conserva la parte correcta de la versión entrante.
3. Combina o reescribe el contenido si ninguna alternativa funciona por sí sola.
4. Elimina `<<<<<<<`, `=======` y `>>>>>>>`.
5. Guarda el archivo.

La resolución manual suele ser necesaria cuando ambas versiones aportan información útil o cuando deben adaptarse para funcionar juntas.

---

## 16. Verificar que no queden marcas

Antes de preparar el archivo, busca estas marcas en Visual Studio Code:

```text
<<<<<<<
=======
>>>>>>>
```

Puedes utilizar la búsqueda del proyecto con `Ctrl + Shift + F` en Windows/Linux o `Command + Shift + F` en macOS.

Revisa los resultados con cuidado: una línea de signos igual podría formar parte legítima de otro archivo, pero las secuencias `<<<<<<<` y `>>>>>>>` son señales especialmente importantes.

---

## 17. Preparar el archivo resuelto

Después de editar, guardar y revisar el archivo, indícale a Git que atendiste su conflicto:

```bash
git add nombre-archivo
```

Por ejemplo:

```bash
git add README.md
```

Durante una resolución, `git add` no solo prepara el contenido: también informa a Git que consideras resuelto ese archivo. Por eso debes ejecutarlo únicamente después de comprobar el resultado.

---

## 18. Revisar nuevamente

Ejecuta:

```bash
git status
```

El archivo resuelto ya no debe aparecer bajo **Unmerged paths**. Puede mostrarse como preparado para el commit.

Si existen otros archivos sin resolver, repite el proceso para cada uno. No completes la integración hasta que `git status` deje de mostrar rutas sin fusionar.

---

## 19. Finalizar el proceso

Dependiendo de la operación y la configuración de Git, puede ser necesario crear un commit que complete la integración:

```bash
git commit -m "Resolver conflicto en README"
```

Después comprueba:

```bash
git status
```

Cuando el repositorio esté en un estado coherente, el proyecto haya sido probado y corresponda publicar el resultado, ejecuta:

```bash
git push
```

El `push` debe realizarse al final, no mientras existan conflictos sin resolver.

---

## 20. Flujo completo de resolución

```text
Conflicto
    ↓
git status
    ↓
Abrir archivo
    ↓
Comparar cambios
    ↓
Decidir qué conservar
    ↓
Eliminar marcas
    ↓
Guardar y probar
    ↓
git add archivo
    ↓
git status
    ↓
git commit
    ↓
git push
```

Lee el resultado de cada paso. Si todavía aparecen archivos sin fusionar, no avances al commit.

---

## 21. Conflictos producidos por `git pull`

`git pull` descarga commits remotos e intenta integrarlos en la rama local. Puede aparecer un conflicto cuando tus commits locales y los remotos cambiaron de manera incompatible el mismo contenido.

Git descarga la información, inicia la integración y se detiene en los bloques que no puede resolver. Debes atenderlos, prepararlos y completar el commit antes de continuar.

Si solo tienes cambios locales sin confirmar que serían sobrescritos, Git puede cancelar el `pull` antes de iniciar el merge. En ambos casos, comienza con `git status` y protege tu trabajo local.

---

## 22. Conflictos producidos por merge

Al integrar una rama con:

```bash
git merge nombre-rama
```

Git compara los historiales de la rama activa y `nombre-rama`. Si ambas modificaron de forma incompatible la misma parte, detiene el merge y marca los conflictos.

Recuerda que el merge integra **en la rama activa**. Antes de ejecutarlo, confirma la rama con `git branch` y actualiza el estado según el flujo del equipo.

---

## 23. Qué NO hacer

- No borres archivos sin revisar las dos versiones.
- No elimines las marcas sin decidir qué contenido quedará.
- No utilices `force push` para intentar arreglar el conflicto.
- No utilices `reset --hard` como solución automática.
- No sobrescribas el trabajo de otra persona sin comprender su propósito.
- No hagas commit hasta revisar todos los archivos resueltos.
- No hagas `push` mientras `git status` muestre rutas sin fusionar.
- No elijas Current, Incoming o Both automáticamente.

Estas acciones pueden perder trabajo o publicar un resultado incorrecto.

---

## 24. Cómo reducir la aparición de conflictos

- Ejecuta `git pull` antes de comenzar una sesión colaborativa, con el trabajo local protegido.
- Divide las tareas por funcionalidades o zonas claras.
- Trabaja con ramas para aislar cambios.
- Crea commits pequeños y coherentes.
- Comunica qué archivos y comportamientos estás modificando.
- Evita editar simultáneamente las mismas líneas.
- Integra cambios con una frecuencia razonable para no acumular grandes diferencias.
- Revisa el estado antes y después de cada integración.

Estas prácticas reducen los conflictos, pero no los eliminan por completo.

---

## 25. Conflictos en archivos diferentes

Si dos personas modifican archivos diferentes, normalmente Git puede integrar los cambios automáticamente porque no compiten por el mismo contenido.

Aun así, los archivos pueden depender entre sí. Una integración sin conflicto textual puede producir un error funcional, por lo que siempre debes probar el proyecto.

---

## 26. Conflictos en el mismo archivo pero líneas diferentes

Git muchas veces puede integrar automáticamente cambios situados en zonas diferentes del mismo archivo.

Por ejemplo, una persona modifica el título al inicio de `README.md` y otra agrega una sección al final. Si las modificaciones no se superponen, Git suele combinarlas sin intervención.

El resultado automático debe revisarse igualmente para confirmar que el documento conserve una estructura lógica.

---

## 27. Conflictos en las mismas líneas

Uno de los casos más comunes ocurre cuando dos versiones cambian las mismas líneas o agregan contenido diferente en el mismo lugar.

Git no puede deducir cuál intención debe prevalecer. Por eso muestra las marcas y exige una decisión humana. La resolución puede conservar Current, Incoming, ambas o una versión nueva construida a partir de las dos.

---

## 28. Herramientas visuales de VS Code

Visual Studio Code puede mostrar acciones dentro del archivo o una interfaz llamada **Merge Editor**.

El Merge Editor suele incluir:

- **Incoming:** la versión que se intenta integrar.
- **Current:** la versión de la rama actualmente activa.
- **Result:** el contenido final que se guardará.

Puedes aceptar alternativas, combinarlas o editar directamente **Result**. La disposición y los nombres exactos pueden variar según la versión de Visual Studio Code.

Cuando todos los conflictos estén resueltos, revisa el resultado completo. Algunas versiones pueden ofrecer **Complete Merge**, pero continúa comprobando el estado con `git status` para entender qué hizo la interfaz.

---

## 29. Verificar el proyecto después de resolver

Eliminar las marcas no garantiza que el proyecto funcione. Antes del commit:

- Lee el archivo completo.
- Comprueba que no haya contenido repetido o ausente.
- Ejecuta o prueba el proyecto.
- Ejecuta las pruebas automatizadas disponibles.
- Revisa las diferencias desde Source Control.
- Ejecuta `git status`.

La resolución correcta debe ser válida tanto para Git como para la lógica del proyecto.

---

## 30. Ejercicio guiado

Practica este análisis en un repositorio de ejercicio, no durante una entrega importante.

### Situación simulada

Supón que un `git pull` produjo en `README.md`:

```text
<<<<<<< HEAD
## Instalación para estudiantes
=======
## Configuración inicial
>>>>>>> origin/main
```

### Resolución

1. Ejecuta `git status` e identifica `README.md` como archivo sin fusionar.
2. Ábrelo en Visual Studio Code.
3. Interpreta **Current** como `## Instalación para estudiantes` e **Incoming** como `## Configuración inicial`.
4. Decide que ambas ideas son necesarias, pero que deben formar un único título.
5. Reemplaza todo el bloque por:

```text
## Instalación y configuración inicial para estudiantes
```

6. Guarda el archivo.
7. Busca `<<<<<<<`, `=======` y `>>>>>>>` para confirmar que no queden marcas.
8. Revisa el documento completo y su vista previa Markdown.
9. Prepara y verifica la resolución:

```bash
git add README.md
git status
```

10. Si no quedan conflictos y el contenido es correcto, completa el proceso:

```bash
git commit -m "Resolver conflicto en README"
git status
git push
```

Este ejercicio no elige ciegamente una versión: combina las dos intenciones en un resultado revisado.

---

## 31. Errores y situaciones frecuentes

### `CONFLICT (content)`

- **Qué significa:** Git encontró contenido incompatible en el archivo indicado.
- **Acción segura:** ejecuta `git status`, abre el archivo y compara Current e Incoming antes de editar.

### `Automatic merge failed`

- **Qué significa:** Git no pudo completar automáticamente la integración.
- **Acción segura:** resuelve todos los archivos señalados, guárdalos, pruébalos y prepáralos. No ejecutes `push` todavía.

### `You have unmerged paths`

- **Qué significa:** todavía existen archivos con conflictos sin resolver o sin marcar como resueltos.
- **Acción segura:** revisa la lista de `git status`. Atiende cada archivo y usa `git add archivo` solo después de resolverlo.

### `All conflicts fixed but you are still merging`

- **Qué significa:** todos los archivos parecen resueltos y preparados, pero falta finalizar el merge.
- **Acción segura:** revisa y prueba el resultado una vez más; después crea el commit solicitado por Git para completar la integración.

---

## 32. Tabla rápida

| Quiero... | Comando | Función |
| --- | --- | --- |
| Ver conflictos | `git status` | Muestra archivos sin fusionar y el estado de la operación. |
| Marcar un archivo como resuelto | `git add archivo` | Prepara el resultado elegido para ese archivo. |
| Finalizar la resolución | `git commit -m "mensaje"` | Completa la integración cuando Git solicita un commit. |
| Subir el resultado | `git push` | Publica los commits después de resolver y verificar. |

---

## 33. Regla práctica

> Cuando aparezca un conflicto, sigue este orden:

1. **Leer** el mensaje completo.
2. **Comparar** las dos versiones.
3. **Decidir** qué resultado necesita el proyecto.
4. **Editar** el contenido con cuidado.
5. **Guardar** y probar el archivo.
6. Ejecutar **`git add archivo`**.
7. Revisar nuevamente con **`git status`**.
8. Crear el **commit** que complete la integración.
9. Hacer **`git push`** solo después de verificar todo.

---

## 34. Comprobación final

Confirma que puedes realizar cada tarea:

- [ ] Explico qué es un conflicto y sé que no implica pérdida automática del proyecto.
- [ ] Reconozco mensajes típicos de conflicto.
- [ ] Interpreto las marcas `<<<<<<<`, `=======` y `>>>>>>>`.
- [ ] Distingo **Current** de **Incoming** según el contexto.
- [ ] Utilizo las herramientas visuales de Visual Studio Code sin decidir a ciegas.
- [ ] Resuelvo manualmente un archivo y retiro todas las marcas.
- [ ] Marco el archivo resuelto mediante `git add archivo`.
- [ ] Finalizo la integración mediante un commit cuando corresponde.
- [ ] Reviso y pruebo el proyecto antes de subirlo.
- [ ] Evito `force push`, `reset --hard` y otras operaciones destructivas.

Si completaste la lista, ya puedes resolver conflictos básicos protegiendo el trabajo local y las contribuciones del equipo.
