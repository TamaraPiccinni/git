# Guía de Instalación y Terminal para Linux y macOS

A diferencia de Windows, donde es necesario instalar Git Bash para emular un entorno de comandos compatible, los sistemas operativos basados en Unix (como Linux y macOS) ya cuentan con terminales nativas preparadas para ejecutar Git de forma directa y eficiente.

---

## 1. Guía para usuarios de Linux

En Linux, Git suele venir preinstalado en muchas distribuciones, o bien se encuentra disponible de forma directa en los repositorios oficiales de software.

### Instalación según la distribución
Abre la terminal nativa de tu sistema (usualmente accesible con el atajo de teclado Ctrl + Alt + T) y ejecuta el comando correspondiente a tu distribución:

* **En Debian, Ubuntu, Linux Mint y derivados:**
  ```bash
  sudo apt update
  sudo apt install git
  ```

* **En Fedora, Red Hat y CentOS:**
  ```bash
  sudo dnf install git
  ```

* **En Arch Linux y derivados (como Manjaro):**
  ```bash
  sudo pacman -S git
  ```

### Verificación de la instalación
Para comprobar que el sistema reconoce el programa correctamente, ejecuta:
```bash
git --version
```

---

## 2. Guía para usuarios de macOS (Mac)

En las computadoras Mac, la terminal nativa utiliza actualmente un entorno llamado Zsh (Z Shell) por defecto, el cual es completamente compatible con todos los comandos estándar de Git.

### Métodos de instalación

* **Opción A: A través de las herramientas de línea de comandos de Xcode (Recomendado y más simple)**
  1. Abre la aplicación Terminal (puedes buscarla en el Launchpad o con Spotlight presionando Cmd + Espacio).
  2. Escribe el siguiente comando y presiona Enter:
     ```bash
     git --version
     ```
  3. Si no está instalado, el propio sistema operativo abrirá una ventana emergente preguntando si deseas instalar las "Herramientas de línea de comandos de Xcode". Haz clic en "Instalar" y acepta los términos. No es necesario descargar la aplicación completa de Xcode (que es muy pesada).

* **Opción B: A través del gestor de paquetes Homebrew (Para usuarios avanzados)**
  Si ya utilizas Homebrew en tu Mac, puedes instalarlo y mantenerlo actualizado ejecutando:
  ```bash
  brew install git
  ```

---

## 3. Particularidades importantes entre Sistemas Operativos

Es altamente recomendable que expliques estas diferencias a tu equipo de trabajo para prevenir errores misteriosos durante el desarrollo del proyecto:

### A. Sensibilidad a las mayúsculas y minúsculas (Case Sensitivity)
Este es uno de los problemas más invisibles y complejos para los principiantes cuando colaboran en equipo:
* **Linux es estrictamente sensible:** Para Linux, un archivo llamado `index.html` y otro llamado `Index.html` son dos archivos completamente diferentes y pueden convivir en la misma carpeta.
* **Windows y macOS no son sensibles por defecto:** Si cambias la primera letra de un archivo de minúscula a mayúscula, tu computadora asumirá que es el mismo archivo modificado.

**El problema:** Si un alumno en Mac renombra un archivo de `estilos.css` a `Estilos.css`, su computadora no registrará un cambio de archivo. Pero al subirlo a GitHub y ser descargado por un compañero que usa Linux, el proyecto podría romperse porque Linux buscará el archivo con la combinación exacta de letras. 

**Solución:** Mantener la buena práctica de escribir siempre todos los nombres de archivos y carpetas estrictamente en minúsculas y separados por guiones medios.

### B. Los saltos de línea (CRLF vs. LF)
La forma en que los sistemas operativos guardan el carácter invisible de "Intro" o "Salto de línea" al final de cada frase es distinta:
* Windows utiliza el formato CRLF (Carriage Return Line Feed).
* Linux y Mac utilizan el formato LF (Line Feed).

Si un usuario de Windows y uno de Mac editan el mismo archivo de texto, Git podría alertar que se ha modificado el archivo completo (línea por línea) solo porque cambiaron los caracteres invisibles de salto de línea, dificultando la lectura del comando `git diff`.

**Solución:** Configurar Git para que gestione esto de forma automática según el sistema operativo.

* **Comando para usuarios de Windows:**
  ```bash
  git config --global core.autocrlf true
  ```

* **Comando para usuarios de Linux y Mac:**
  ```bash
  git config --global core.autocrlf input
  ```