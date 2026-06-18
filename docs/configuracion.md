# Configuración Inicial y Conceptos Base

Antes de escribir comandos, es fundamental entender dónde ocurren las cosas y cómo se comunica nuestro entorno.

## 1. CLI vs. GUI: ¿Cómo interactuamos con Git?

* **CLI (Command Line Interface / Interfaz de Línea de Comandos):** Es la terminal. Escribimos comandos de texto directamente. Es el estándar profesional porque es más veloz, consume menos recursos y funciona en cualquier servidor del mundo.
* **GUI (Graphical User Interface / Interfaz Gráfica de Usuario):** Son programas visuales como GitKraken, GitHub Desktop o el panel integrado de VSCode. Son excelentes para ver gráficos de ramas complejas, pero a veces ocultan errores técnicos que solo se solucionan en la terminal.

**Regla de aprendizaje:** Aprende primero la CLI. Si dominas los comandos, podrás usar cualquier herramienta visual; si solo aprendes la herramienta visual, quedarás desarmado cuando falle.

---

## 2. Diferencia entre Local y Remoto

* **Local:** Es tu computadora física. Tu código, tus archivos y todo el historial de cambios viven dentro de una carpeta oculta llamada `.git` en tu disco duro. No necesitas internet para usar Git de forma local.
* **Remoto:** Es un servidor seguro en la nube (como GitHub, GitLab o Bitbucket). Sirve como respaldo de tu proyecto y como punto de encuentro para que otros programadores descarguen tu código y colaboren.

---

## 3. Configuración Global Obligatoria

Cuando te instalas Git por primera vez, debes decirle quién eres. Cada commit (guardado) lleva tu firma para que el equipo sepa quién programó cada línea.

Ejecuta estos comandos en tu terminal una sola vez:

```bash
# Configura tu nombre completo
git config --global user.name "Tu Nombre y Apellido"

# Configura el correo asociado a tu cuenta de GitHub
git config --global user.email "tu@email.com"

# IMPORTANTE: Configura 'main' como rama por defecto en tu PC
git config --global init.defaultBranch main
```

> **Nota sobre la rama por defecto:** Históricamente Git creaba una rama llamada "master". Hoy en día, GitHub y la industria utilizan "main". Configurar esto evita conflictos de nombres al subir tu código por primera vez.

---

## 4. ¿Cómo conectar tu proyecto? (Dos caminos diferentes)

### Camino A: Crear un repositorio local desde cero y subirlo a GitHub
Usa este método si empezaste a programar en tu PC y recién ahora quieres crear el repositorio en GitHub.

1. Inicializa Git en tu carpeta local (se hace una sola vez por proyecto):
   ```bash
   git init
   ```
2. Agrega y confirma tus primeros archivos locales (`git add .` y `git commit`).
3. Ve a GitHub, crea un repositorio vacío y copia su URL.
4. Vincula tu carpeta local con ese servidor remoto (lo llamamos "origin"):
   ```bash
   git remote add origin https://github.com/tu-usuario/tu-repositorio.git
   ```
5. Sube tus cambios y define la rama de destino por defecto (`-u`):
   ```bash
   git push -u origin main
   ```

### Camino B: Clonar un repositorio que ya existe en GitHub
Usa este método si el proyecto ya fue creado en GitHub (por ti o por tu equipo) y quieres descargarlo para empezar a trabajar.

```bash
git clone  https://github.com/tu-usuario/tu-repositorio.git
```
Al clonar, Git automáticamente descarga el código, crea la carpeta oculta `.git` e indexa el vínculo remoto ("origin"). No necesitas hacer `git init` ni `git remote add`.

---

## 5. Protocolos de Conexión: HTTPS vs. SSH

Cuando descargas o subes código a GitHub, necesitas demostrar que tienes permisos. Hay dos formas de hacerlo:

* **HTTPS:** Utiliza la URL clásica del navegador. Es muy fácil de usar al principio, pero por seguridad, GitHub ya no acepta tu contraseña normal en la terminal; te pedirá configurar un Token de Acceso Personal (PAT), el cual expira y debes renovar.
* **SSH (Secure Shell):** Utiliza un sistema de llaves criptográficas (una llave privada que se queda en tu PC y una pública que subes a GitHub). Configurarlo requiere un par de pasos extra, pero una vez hecho, nunca más te pedirá contraseñas ni tokens para trabajar. Es la opción recomendada para el trabajo diario.