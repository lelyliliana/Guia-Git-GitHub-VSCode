# 10. Trabajar con ramas en Git

En esta sección aprenderás a crear, cambiar, publicar e integrar ramas desde la terminal de Visual Studio Code. También relacionarás estas operaciones con la interfaz gráfica del editor.

Los ejemplos suponen que trabajas en un repositorio existente, con al menos un commit y una rama principal llamada `main`.

---

## 1. ¿Qué es una rama?

Una **rama** es una línea de trabajo separada dentro del mismo repositorio. Permite crear commits sin modificar inmediatamente la línea principal del proyecto.

Imagina que `main` es el texto definitivo de un informe. Para preparar una sección nueva, haces una copia de trabajo: allí puedes escribir, corregir y revisar. Cuando la nueva sección está lista, integras su resultado en el informe principal.

En Git no se duplica manualmente toda la carpeta. La rama mantiene una referencia a una línea de commits y Git administra las diferencias.

La rama principal se llama normalmente:

```text
main
```

Un proyecto puede utilizar otro nombre, por lo que siempre debes verificarlo.

---

## 2. ¿Para qué sirven las ramas?

Las ramas permiten:

- Desarrollar una nueva funcionalidad sin modificar inmediatamente `main`.
- Corregir un error de manera aislada.
- Experimentar sin afectar la versión principal.
- Dividir tareas entre integrantes del equipo.
- Preparar y revisar cambios antes de integrarlos.
- Mantener separadas tareas que tienen propósitos diferentes.

Una rama no reemplaza los commits ni la comunicación. Debes guardar cambios coherentes y acordar con el equipo cómo se integrarán.

---

## 3. Visualizar las ramas existentes

En la terminal integrada, ejecuta:

```bash
git branch
```

Git muestra las ramas locales que contienen commits. Un asterisco identifica la rama activa:

```text
* main
```

En este ejemplo estás trabajando en `main`. Los próximos commits pertenecerán a esa rama hasta que cambies a otra.

---

## 4. Crear una nueva rama

La forma general es:

```bash
git branch nombre-rama
```

Por ejemplo:

```bash
git branch formulario-contacto
```

Este comando crea `formulario-contacto` a partir del commit actual. **Crear la rama no significa cambiarse automáticamente a ella**.

Si ejecutas `git branch` después, verás ambas ramas, pero el asterisco continuará junto a `main`.

---

## 5. Crear una rama y cambiarse inmediatamente

Una forma práctica de hacer ambos pasos es:

```bash
git switch -c nombre-rama
```

Por ejemplo:

```bash
git switch -c formulario-contacto
```

`switch` cambia la rama activa y la opción `-c` indica que Git debe **crear** primero una rama nueva. El resultado habitual será:

```text
Switched to a new branch 'formulario-contacto'
```

Utiliza este comando cuando la rama todavía no exista. Si ya existe, cambia a ella sin `-c`.

---

## 6. Cambiar entre ramas

Para regresar a la rama principal:

```bash
git switch main
```

Para volver a la rama de trabajo:

```bash
git switch formulario-contacto
```

Al cambiar de rama, Git actualiza los archivos de la carpeta para representar el commit correspondiente. Por eso es importante guardar y conservar adecuadamente cualquier cambio pendiente antes de cambiar.

Verifica siempre la rama activa: un commit creado en la rama equivocada queda registrado en una línea de trabajo distinta de la prevista.

---

## 7. Verificar la rama activa

Ejecuta:

```bash
git branch
```

Busca el asterisco junto al nombre activo. También puedes usar:

```bash
git status
```

La primera parte del resultado suele indicar algo como:

```text
On branch formulario-contacto
```

Conviene comprobarlo antes de editar archivos, crear commits, hacer `pull`, integrar o publicar una rama.

---

## 8. Realizar cambios dentro de una rama

Supón que crearás una página nueva:

```bash
git switch -c nueva-pagina
```

Modifica o crea los archivos en Visual Studio Code y guárdalos. Después revisa:

```bash
git status
```

Prepara los cambios revisados y crea el commit:

```bash
git add .
git commit -m "Agregar nueva página"
```

Ese commit pertenece a `nueva-pagina`, porque era la rama activa. No aparecerá automáticamente en `main`.

---

## 9. Comparar lo que ocurre en `main` y en otra rama

Cuando creas `nueva-pagina`, ambas ramas parten inicialmente del mismo commit. Al confirmar cambios en la rama nueva, su historial avanza mientras `main` permanece en el punto anterior.

```text
main:          A
                \
nueva-pagina:   B
```

El commit `B` existe en `nueva-pagina`, pero todavía no forma parte de `main`. Esto permite mantener estable la rama principal mientras se desarrolla y revisa la tarea.

Al cambiar entre ramas, algunos archivos pueden mostrar contenidos diferentes. Es el comportamiento esperado: Visual Studio Code refleja la versión de la rama activa.

---

## 10. Subir una rama a GitHub

La primera vez que publiques una rama, ejecuta:

```bash
git push -u origin nombre-rama
```

Por ejemplo:

```bash
git push -u origin nueva-pagina
```

- `push` envía los commits.
- `origin` identifica el repositorio remoto.
- `nueva-pagina` es la rama que se publicará.
- `-u` vincula la rama local con su rama remota para futuros envíos.

Después de establecer ese vínculo, normalmente bastará con:

```bash
git push
```

Publicar una rama no integra sus cambios en `main`; crea o actualiza una rama separada en GitHub.

---

## 11. Ver ramas remotas

Para ver las referencias de ramas remotas conocidas, ejecuta:

```bash
git branch -r
```

Puedes encontrar:

```text
origin/main
origin/nueva-pagina
```

`origin/main` representa la rama `main` conocida en el remoto `origin`, y `origin/nueva-pagina` representa la rama publicada. Son referencias remotas, no ramas locales donde editas directamente.

---

## 12. Ver todas las ramas

Ejecuta:

```bash
git branch -a
```

Este comando combina:

- **Ramas locales:** líneas de trabajo disponibles directamente en tu copia.
- **Referencias remotas:** estado conocido de las ramas publicadas en remotos como `origin`.

Las referencias remotas suelen aparecer con un prefijo como `remotes/origin/`. Si otra persona acaba de publicar una rama y no aparece, puede ser necesario actualizar primero la información remota mediante `git fetch`.

---

## 13. Flujo básico con una rama

```text
main
  ↓
Crear nueva rama
  ↓
git switch -c nueva-funcionalidad
  ↓
Trabajar y guardar archivos
  ↓
git status
  ↓
git add .
  ↓
git commit -m "Descripción del cambio"
  ↓
git push -u origin nueva-funcionalidad
```

La rama queda disponible localmente y en GitHub, pero sus commits continúan separados de `main` hasta que se integren.

---

## 14. Integrar una rama en `main`

**Merge** es la operación que integra en la rama actual los commits de otra rama.

Primero asegúrate de haber confirmado el trabajo de la rama y de que el directorio esté limpio. Después cambia a `main`:

```bash
git switch main
```

Actualiza `main` desde GitHub:

```bash
git pull
```

Ahora integra la rama:

```bash
git merge nombre-rama
```

Por ejemplo:

```bash
git merge nueva-pagina
```

Git incorpora en la rama activa —en este caso `main`— los commits alcanzables desde `nueva-pagina`. Puede avanzar directamente, crear un commit de merge o detenerse si existen conflictos.

Antes de integrar en un repositorio de equipo, confirma que el procedimiento coincide con las reglas acordadas; algunos proyectos integran ramas mediante *pull requests* en GitHub.

---

## 15. Verificar después del merge

Consulta el estado:

```bash
git status
```

Si la integración terminó correctamente, no deben quedar conflictos sin resolver. Después consulta el historial:

```bash
git log --oneline
```

Busca el mensaje `Agregar nueva página` o el commit correspondiente. También puedes abrir y probar los archivos desde Visual Studio Code para comprobar que el resultado combinado funciona.

La verificación funcional es importante: Git puede integrar texto sin detectar errores de comportamiento.

---

## 16. Subir `main` después del merge

El merge realizado por terminal modifica primero la rama `main` local. Para publicar el resultado en GitHub, ejecuta:

```bash
git push
```

Después actualiza la página del repositorio y comprueba que `main` contiene los commits integrados.

No confundas publicar la rama de trabajo con publicar `main`: son envíos de ramas diferentes.

---

## 17. Diferencia entre `branch`, `switch` y `merge`

| Comando | Función principal | Ejemplo |
| --- | --- | --- |
| `git branch` | Ver ramas o crear una rama sin cambiarte a ella. | `git branch nueva-pagina` |
| `git switch` | Cambiar la rama activa; con `-c`, crearla y cambiar. | `git switch nueva-pagina` |
| `git merge` | Integrar otra rama en la rama activa. | `git merge nueva-pagina` |

Antes de `merge`, confirma con `git branch` cuál es la rama activa. La dirección importa: estando en `main`, `git merge nueva-pagina` integra `nueva-pagina` dentro de `main`.

---

## 18. Nombres recomendados para ramas

En equipos que utilizan categorías, algunos nombres posibles son:

```text
feature/formulario
feature/login
fix/error-validacion
docs/actualizar-readme
```

Para comenzar también puedes usar nombres simples:

```text
formulario-contacto
corregir-menu
actualizar-readme
```

El nombre debe describir una tarea concreta. Utiliza minúsculas, separa palabras con guiones y evita espacios. Respeta siempre la convención acordada por el equipo.

---

## 19. Qué NO hacer al trabajar con ramas

- No olvides verificar la rama activa antes de modificar o confirmar archivos.
- No trabajes directamente en `main` si el equipo acordó usar ramas para las tareas.
- No elimines una rama sin comprobar que sus cambios estén integrados o que ya no sean necesarios.
- No utilices `force push`; puede reemplazar historial compartido.
- No mezcles tareas completamente diferentes en una sola rama.
- No cambies de rama ignorando modificaciones locales pendientes.
- No integres código sin revisar y probar el resultado.

---

## 20. Conflictos al hacer merge

Puede producirse un conflicto si `main` y la otra rama modificaron de forma incompatible las mismas líneas o estructuras.

Git detendrá la integración y marcará los archivos afectados. Empieza por:

```bash
git status
```

Abre cada archivo en Visual Studio Code, revisa las versiones Current e Incoming y construye el resultado correcto. No hagas `push` hasta resolver todos los conflictos y completar el commit del merge.

Los conflictos fueron introducidos en [09. Trabajo colaborativo con GitHub](../09-trabajo-colaborativo/README.md) y se tratarán con mayor detalle en la siguiente sección.

---

## 21. Eliminar una rama local después de integrarla

Cuando confirmes que la rama fue integrada y publicada correctamente, puedes eliminar la referencia local:

```bash
git branch -d nombre-rama
```

Por ejemplo:

```bash
git branch -d nueva-pagina
```

La opción `-d` solicita una eliminación segura: Git normalmente se niega si detecta commits de la rama que no están integrados en la rama actual.

Debes estar en otra rama, por ejemplo `main`, antes de eliminarla. No es obligatorio borrar inmediatamente las ramas para continuar con esta guía; verifica primero con el equipo.

---

## 22. Eliminar una rama remota

Cuando el equipo esté completamente seguro de que la rama publicada ya no es necesaria, puede eliminarse del remoto:

```bash
git push origin --delete nombre-rama
```

Este comando modifica el repositorio compartido y afecta a los demás integrantes. Antes de ejecutarlo:

1. Comprueba que los cambios estén integrados en `main`.
2. Verifica que `main` se haya publicado correctamente.
3. Confirma que nadie continúe trabajando en esa rama.
4. Acuerda la eliminación con el equipo.

No elimines una rama remota únicamente para ordenar la lista si no conoces el estado de su trabajo.

---

## 23. Ramas desde Visual Studio Code

Visual Studio Code muestra normalmente la rama activa en la barra de estado inferior. Seleccionar su nombre abre opciones relacionadas con ramas.

También puedes utilizar la Command Palette:

- **Git: Create Branch** se relaciona con crear una rama, como `git branch nombre` o `git switch -c nombre`.
- **Git: Checkout to** o la opción equivalente permite elegir otra rama, como `git switch nombre`.
- Las opciones de publicación se relacionan con `git push -u origin nombre`.

Source Control y el gráfico del repositorio también pueden mostrar ramas y su historial. Los nombres exactos pueden variar según la versión de Visual Studio Code.

Después de una acción gráfica, verifica el resultado en la terminal:

```bash
git branch
git status
```

---

## 24. Ejemplo completo

### Situación

Debes agregar una sección de contacto a un proyecto sin modificar directamente `main`.

### Preparar la rama

Confirma que el trabajo actual esté guardado. Después ejecuta cada comando por separado:

```bash
git switch main
git pull
git switch -c formulario-contacto
```

Ahora modifica los archivos necesarios en Visual Studio Code, guarda y prueba el formulario.

### Guardar y publicar la tarea

```bash
git status
git add .
git status
git commit -m "Agregar formulario de contacto"
git push -u origin formulario-contacto
```

Comprueba en GitHub que la rama `formulario-contacto` y su commit estén publicados.

### Integrar posteriormente en `main`

Cuando la tarea haya sido revisada y el equipo autorice la integración:

```bash
git switch main
git pull
git merge formulario-contacto
git status
git push
```

Si el merge produce conflictos, detente, resuélvelos y completa el commit antes de `git push`. Finalmente, verifica en GitHub que `main` contenga el formulario.

---

## 25. Errores y situaciones frecuentes

### `fatal: a branch named '...' already exists`

- **Qué significa:** intentaste crear una rama con un nombre local que ya existe.
- **Causa probable:** ejecutaste nuevamente `git switch -c nombre` o `git branch nombre`.
- **Solución segura:** revisa `git branch`. Si es la rama correcta, cambia a ella con `git switch nombre`; no vuelvas a crearla.

### `error: pathspec '...' did not match any file(s) known to git`

- **Qué significa:** Git no encuentra el nombre solicitado para cambiar de rama.
- **Causa probable:** hay un error de escritura o la rama no existe localmente.
- **Solución segura:** ejecuta `git branch -a`, revisa el nombre exacto y confirma con el equipo qué rama necesitas. No crees otra rama con un nombre parecido sin comprobarlo.

### `Your branch is ahead of...`

- **Qué significa:** la rama local contiene commits que todavía no están en su rama remota vinculada.
- **Causa probable:** hiciste commit después del último envío.
- **Solución segura:** revisa `git status` y, si los commits son correctos y tienes permisos, ejecuta `git push`.

### `merge conflict`

- **Qué significa:** Git no pudo integrar automáticamente cambios incompatibles.
- **Causa probable:** ambas ramas modificaron las mismas líneas o estructuras relacionadas.
- **Solución segura:** revisa `git status`, resuelve cada archivo en Visual Studio Code, prueba el resultado y completa el commit. No borres ni fuerces cambios.

### `Already up to date.`

- **Qué significa:** la rama que intentas integrar no aporta commits nuevos a la rama activa, o el `pull` no encontró cambios remotos nuevos.
- **Causa probable:** los cambios ya estaban integrados o no había novedades.
- **Solución segura:** ninguna; es informativo. Confirma la rama activa y el historial si esperabas otro resultado.

---

## 26. Tabla rápida de comandos

| Quiero... | Comando |
| --- | --- |
| Ver ramas locales | `git branch` |
| Crear una rama | `git branch nombre` |
| Crear una rama y cambiar inmediatamente | `git switch -c nombre` |
| Cambiar de rama | `git switch nombre` |
| Ver ramas remotas | `git branch -r` |
| Ver ramas locales y remotas | `git branch -a` |
| Subir una rama por primera vez | `git push -u origin nombre` |
| Integrar una rama en la rama activa | `git merge nombre` |
| Eliminar de forma segura una rama local integrada | `git branch -d nombre` |

---

## 27. Buenas prácticas

- Crea una rama por funcionalidad, corrección o tarea coherente.
- Utiliza nombres descriptivos y acordados con el equipo.
- Haz commits pequeños con mensajes claros.
- Actualiza `main` antes de crear una rama y antes de integrarla.
- Ejecuta `git status` con frecuencia.
- Verifica la rama activa antes de modificar archivos y hacer commits.
- Revisa y prueba el resultado de cada merge.
- Resuelve conflictos leyendo todas las versiones.
- Publica la rama para respaldar y compartir sus commits cuando corresponda.
- Evita comandos destructivos y nunca utilices `force push` sin una política explícita y conocimiento avanzado.

---

## 28. Comprobación final

Confirma que puedes realizar cada tarea:

- [ ] Explico qué es una rama y por qué separa líneas de trabajo.
- [ ] Identifico la rama activa con `git branch` o `git status`.
- [ ] Creo ramas nuevas.
- [ ] Cambio entre ramas mediante `git switch`.
- [ ] Creo commits dentro de una rama de trabajo.
- [ ] Publico una rama en GitHub y establezco su vínculo remoto.
- [ ] Distingo ramas locales de referencias remotas.
- [ ] Integro una rama en `main` mediante merge y verifico el resultado.
- [ ] Elimino una rama local integrada con la opción segura `-d`.
- [ ] Creo y cambio ramas también desde la interfaz de Visual Studio Code.

Si completaste la lista, ya puedes utilizar ramas para organizar tareas y proteger la estabilidad de `main`.
