# 01. Instalación y configuración de Git

En esta sección aprenderás a instalar Git y a realizar su configuración inicial desde Visual Studio Code. No necesitas tener conocimientos previos.

---

## 1. ¿Qué es Git?

Git es un **sistema de control de versiones**. Es una herramienta que registra los cambios realizados en los archivos de un proyecto y conserva un historial de esos cambios.

Con Git puedes:

- Saber qué archivos cambiaron y quién realizó cada cambio.
- Guardar distintas versiones de un proyecto.
- Recuperar una versión anterior si algo sale mal.
- Trabajar de manera ordenada con otras personas.

Git funciona en tu computador y puede utilizarse incluso sin conexión a Internet.

---

## 2. ¿Qué es GitHub?

GitHub es una plataforma en Internet que permite almacenar, compartir y colaborar en proyectos que utilizan Git. Un proyecto administrado con Git se denomina **repositorio**.

Aunque se complementan, **Git y GitHub no son lo mismo**:

- **Git** es la herramienta de control de versiones que se instala y ejecuta en tu computador.
- **GitHub** es un servicio en línea donde puedes publicar repositorios Git y colaborar con otras personas.

Puedes usar Git sin GitHub. Sin embargo, GitHub facilita guardar una copia remota del proyecto, compartirla y trabajar en equipo.

---

## 3. Verificar si Git está instalado

Abre **Visual Studio Code** y, en la barra de menú, selecciona:

**Terminal → New Terminal**

Se abrirá una terminal integrada en la parte inferior de la ventana. Escribe el siguiente comando y presiona `Enter`:

```bash
git --version
```

Este comando consulta la versión de Git instalada. Si Git está disponible, verás un resultado similar a este:

```text
git version 2.43.0
```

El número de versión puede variar y eso es normal. Si la terminal indica que `git` no se reconoce, no se encuentra o no existe, continúa con la instalación de la sección siguiente.

---

## 4. Instalar Git si no está instalado

Sigue únicamente las instrucciones correspondientes a tu sistema operativo. Al terminar, cierra y vuelve a abrir Visual Studio Code; después ejecuta nuevamente `git --version`.

### Windows

1. Entra al sitio oficial de Git: [https://git-scm.com/](https://git-scm.com/).
2. Descarga el instalador para Windows.
3. Ejecuta el archivo descargado.
4. Completa el asistente de instalación. Para una instalación inicial puedes conservar las opciones predeterminadas.
5. Reinicia Visual Studio Code y verifica la instalación con `git --version`.

### Ubuntu/Debian Linux

Primero actualiza la información de los paquetes disponibles:

```bash
sudo apt update
```

Después instala Git:

```bash
sudo apt install git
```

El sistema puede solicitar tu contraseña y una confirmación. Mientras escribes la contraseña, es normal que no aparezcan caracteres en la terminal.

### macOS

Si ya tienes [Homebrew](https://brew.sh/) instalado, abre la terminal integrada de Visual Studio Code y ejecuta:

```bash
brew install git
```

Homebrew descargará e instalará Git. Al finalizar, reinicia Visual Studio Code y comprueba la instalación con `git --version`.

---

## 5. Configurar el nombre del usuario

Git guarda el nombre de la persona que realiza cada cambio. Configúralo con el siguiente comando, sustituyendo el texto entre comillas por tu nombre:

```bash
git config --global user.name "Nombre Apellido"
```

Por ejemplo:

```bash
git config --global user.name "Ana Pérez"
```

La opción `--global` aplica esta configuración a todos los repositorios que utilices con tu cuenta de usuario en ese computador.

---

## 6. Configurar el correo electrónico

Git también asocia un correo electrónico a cada cambio. Sustituye el correo del ejemplo por el tuyo:

```bash
git config --global user.email "correo@ejemplo.com"
```

Es preferible utilizar el correo asociado a tu cuenta de GitHub. De esa manera, GitHub podrá relacionar correctamente tus contribuciones con tu perfil.

---

## 7. Verificar la configuración

Para consultar la configuración actual de Git, ejecuta:

```bash
git config --list
```

En el resultado, localiza líneas similares a estas:

```text
user.name=Ana Pérez
user.email=correo@ejemplo.com
```

Comprueba que `user.name` y `user.email` contengan tus datos correctos. La lista puede mostrar otras opciones adicionales; esto es normal.

---

## 8. Configurar `main` como rama inicial

Ejecuta el siguiente comando:

```bash
git config --global init.defaultBranch main
```

Este comando indica que los repositorios nuevos creados con Git deben usar `main` como nombre de su rama inicial. Conviene configurarlo porque `main` es el nombre utilizado habitualmente en GitHub y así se evitan diferencias de nombres al publicar un repositorio.

Esta opción se aplicará a los repositorios que crees después de configurarla; no cambia el nombre de las ramas de repositorios existentes.

---

## 9. Tabla resumen de comandos

| Comando | Función |
| --- | --- |
| `git --version` | Comprueba si Git está instalado y muestra su versión. |
| `sudo apt update` | Actualiza la información de paquetes en Ubuntu/Debian. |
| `sudo apt install git` | Instala Git en Ubuntu/Debian. |
| `brew install git` | Instala Git en macOS mediante Homebrew. |
| `git config --global user.name "Nombre Apellido"` | Configura el nombre que Git asociará a los cambios. |
| `git config --global user.email "correo@ejemplo.com"` | Configura el correo que Git asociará a los cambios. |
| `git config --list` | Muestra la configuración actual de Git. |
| `git config --global init.defaultBranch main` | Define `main` como rama inicial para repositorios nuevos. |

---

## 10. Comprobación final

Antes de continuar con el siguiente capítulo, confirma cada punto:

- [ ] Git está instalado en mi computador.
- [ ] El comando `git --version` muestra una versión.
- [ ] Mi nombre aparece correctamente en `user.name`.
- [ ] Mi correo aparece correctamente en `user.email`.
- [ ] La rama inicial está configurada como `main`.

Si completaste toda la lista, Git está listo para comenzar a trabajar con repositorios desde Visual Studio Code.
