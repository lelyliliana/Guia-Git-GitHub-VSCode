# Comandos rápidos de Git y GitHub

Este documento es una “chuleta” para consultar rápidamente qué comando utilizar según una necesidad concreta. Ejecuta los comandos desde la terminal integrada de Visual Studio Code y lee siempre el resultado antes de continuar.

---

## 1. Diagnóstico básico

| Quiero... | Comando |
| --- | --- |
| Ver el estado del repositorio | `git status` |
| Ver la rama actual | `git branch` |
| Ver el repositorio remoto | `git remote -v` |
| Ver los últimos cinco commits | `git log --oneline -5` |
| Ver cambios no preparados | `git diff` |

Estos comandos consultan información y son un buen punto de partida cuando algo no funciona como esperabas.

---

## 2. Configuración inicial

Comprueba la instalación:

```bash
git --version
```

Configura el nombre y el correo que aparecerán en tus commits:

```bash
git config --global user.name "Nombre Apellido"
git config --global user.email "correo@ejemplo.com"
```

Es preferible utilizar el correo asociado a GitHub. Después configura `main` como rama inicial y revisa el resultado:

```bash
git config --global init.defaultBranch main
git config --list
```

---

## 3. Crear un repositorio

Inicializa Git dentro de la carpeta actual:

```bash
git init
```

Si es necesario, establece `main` como nombre de la rama y consulta el estado:

```bash
git branch -m main
git status
```

Verifica siempre que la terminal esté en la carpeta raíz correcta antes de `git init`.

---

## 4. Preparar y guardar cambios

Prepara un archivo específico:

```bash
git add nombre-archivo
```

Prepara todos los cambios revisados de la carpeta actual:

```bash
git add .
```

Comprueba qué quedó preparado y crea el commit:

```bash
git status
git commit -m "Descripción del cambio"
```

- `git add` selecciona y prepara cambios para el próximo commit.
- `git commit` crea un punto en el historial local con los cambios preparados.

---

## 5. Conectar con GitHub

Agrega el repositorio remoto y verifica su URL:

```bash
git remote add origin URL
git remote -v
```

Realiza el primer envío de `main` y establece el vínculo remoto:

```bash
git push -u origin main
```

Después, normalmente bastará con:

```bash
git push
```

Sustituye `URL` por la dirección HTTPS real del repositorio.

---

## 6. Clonar un repositorio

```bash
git clone URL
cd nombre-repositorio
code .
```

`git clone` crea una copia local completa, `cd` entra en ella y `code .` abre la carpeta actual en Visual Studio Code.

El comando `code .` puede no estar disponible en todos los equipos. En ese caso, utiliza **File → Open Folder**.

---

## 7. Actualizar el proyecto

Descarga e integra los cambios remotos:

```bash
git pull
```

Descarga información remota sin integrarla inmediatamente:

```bash
git fetch
```

`git fetch` actualiza las referencias remotas para consultarlas; `git pull` descarga e intenta integrar los cambios en la rama local actual.

---

## 8. Trabajo diario

> Después de completar y revisar un cambio:

```bash
git status
git add .
git commit -m "Descripción del cambio"
git push
```

Revisa la salida de `git status` antes de preparar archivos y confirma que no incluyas información privada.

---

## 9. Trabajo colaborativo

```bash
git pull
git status
git add .
git commit -m "Descripción del cambio"
git pull
git push
```

El primer `pull` actualiza el proyecto antes de trabajar. El segundo permite detectar e integrar cambios que otras personas pudieron publicar mientras realizabas tu tarea, antes de intentar el `push`.

Si aparece un conflicto, detente y resuélvelo antes de continuar.

---

## 10. Ramas

```bash
git branch
git switch -c nombre-rama
git switch nombre-rama
git branch -r
git branch -a
git merge nombre-rama
git branch -d nombre-rama
git push -u origin nombre-rama
```

| Comando | Función |
| --- | --- |
| `git branch` | Muestra las ramas locales. |
| `git switch -c nombre-rama` | Crea una rama y cambia a ella. |
| `git switch nombre-rama` | Cambia a una rama existente. |
| `git branch -r` | Muestra referencias de ramas remotas. |
| `git branch -a` | Muestra ramas locales y remotas. |
| `git merge nombre-rama` | Integra esa rama en la rama activa. |
| `git branch -d nombre-rama` | Elimina de forma segura una rama local integrada. |
| `git push -u origin nombre-rama` | Publica una rama y establece su vínculo remoto. |

---

## 11. Resolver conflictos

Utiliza únicamente el flujo seguro de revisión, resolución y confirmación:

```bash
git status
git add archivo-resuelto
git commit -m "Resolver conflicto"
git push
```

Antes de `git add`, abre el archivo en Visual Studio Code, compara ambas versiones, elimina las marcas, guarda y prueba el resultado.

---

## 12. Sacar un archivo del *staging* sin borrarlo

Cuando el repositorio ya tiene un commit anterior, utiliza:

```bash
git restore --staged nombre-archivo
```

Este comando retira el archivo del área de preparación, pero **no borra el archivo ni sus modificaciones del computador**. Comprueba el resultado con `git status`.

---

## 13. Consultar por qué un archivo está ignorado

```bash
git check-ignore -v nombre-archivo
```

El comando solo consulta qué regla de ignorado coincide con el archivo. No modifica el archivo ni `.gitignore`.

---

## 14. Mensajes que NO son errores

| Mensaje | Qué significa |
| --- | --- |
| `nothing to commit, working tree clean` | No existen cambios nuevos pendientes de commit. |
| `Everything up-to-date` | No hay commits locales pendientes de subir. |
| `Already up to date.` | No existen commits nuevos para integrar mediante `pull` o merge. |
| `Your branch is up to date with 'origin/main'` | La rama local y la referencia remota conocida están sincronizadas. |

Si esperabas otro resultado, ejecuta `git status` y verifica la carpeta, la rama y el remoto.

---

## 15. Antes de pedir ayuda

Recopila la salida de:

```bash
git status
git branch
git remote -v
git log --oneline -5
```

Copia también el mensaje completo del error y anota el comando que ejecutaste justo antes.

Antes de compartir resultados o capturas, comprueba que no aparezcan contraseñas, tokens, claves privadas, códigos de autenticación ni otros datos sensibles.

---

## 16. Comandos peligrosos para principiantes

No ejecutes estos comandos solo porque aparecen en una respuesta de Internet:

```text
git push --force
git reset --hard
git clean -fd
```

Pueden sobrescribir historial o eliminar trabajo local. No deben utilizarse sin comprender exactamente sus consecuencias, confirmar el repositorio afectado y proteger previamente la información necesaria.

---

## 17. Tabla principal: “Quiero hacer…”

| Quiero hacer... | Comando |
| --- | --- |
| Ver qué cambió | `git status` |
| Preparar todos los cambios | `git add .` |
| Guardar en el historial | `git commit -m "mensaje"` |
| Subir a GitHub | `git push` |
| Actualizar desde GitHub | `git pull` |
| Descargar un repositorio | `git clone URL` |
| Crear una rama | `git switch -c nombre` |
| Cambiar de rama | `git switch nombre` |
| Ver ramas | `git branch` |
| Revisar el origen | `git remote -v` |

Para explicaciones y diagnóstico detallado, consulta [Errores frecuentes](../12-errores-frecuentes/).

---

Material elaborado por **Leli Liliana** como recurso académico de apoyo.
