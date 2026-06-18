# Configuración Inicial y Conceptos Base

Antes de escribir comandos, es fundamental entender dónde ocurren las cosas y cómo se comunica nuestro entorno de desarrollo.

## 1. CLI vs. GUI: ¿Cómo interactuamos con Git?

* **CLI (Command Line Interface / Interfaz de Línea de Comandos):** Es la terminal o consola (como Git Bash). Controlamos el sistema escribiendo comandos de texto directamente. Es el estándar profesional en la industria porque es más veloz, consume menos recursos y funciona de la misma forma en cualquier servidor del mundo.
* **GUI (Graphical User Interface / Interfaz Gráfica de Usuario):** Son aplicaciones visuales con botones y menús (como GitHub Desktop o el panel de Git de VSCode). Son útiles para visualizar flujos complejos, pero suelen ocultar los procesos técnicos internos, complicando la resolución de errores estructurales.

Regla de aprendizaje: Domina primero la CLI. Si entiendes los comandos por texto, podrás usar cualquier herramienta visual sin problemas; si solo dependes de la interfaz gráfica, quedarás desarmado ante fallos del sistema.

---

## 2. Diferencia entre Local y Remoto

* **Local:** Hace referencia a tu computadora física. Tu código, tus archivos de trabajo y todo el historial de cambios viven dentro de una carpeta oculta llamada `.git` en tu disco duro. No requieres conexión a internet para gestionar tus versiones localmente.
* **Remoto:** Es un servidor seguro en la nube (como GitHub, GitLab o Bitbucket). Funciona como respaldo centralizado de tu proyecto y como espacio de sincronización para que otros desarrolladores colaboren.

---

## 3. Configuración Global Obligatoria

Al instalar Git por primera vez, debes identificarte. Cada guardado (commit) lleva tu firma digital para que el equipo de trabajo sepa con precisión quién programó cada línea de código.

Ejecuta estos comandos en tu terminal una sola vez:

```bash
# Configura tu nombre completo de usuario
git config --global user.name "Tu Nombre y Apellido"

# Configura el correo electrónico asociado a tu cuenta de GitHub
git config --global user.email "tu@email.com"

# Configura 'main' como la rama inicial por defecto en tu computadora
git config --global init.defaultBranch main
```

Nota sobre la rama por defecto: Históricamente Git creaba una rama raíz llamada "master". En la actualidad, GitHub y los estándares profesionales de la industria emplean "main". Definir esto de forma global previene conflictos de nombres al subir código por primera vez.

---

## 4. ¿Cómo corregir errores o duplicados en la configuración global?

Si escribes mal una palabra al configurar las variables globales (por ejemplo, `init.defaulBranch` omitiendo la "t"), Git no te mostrará un aviso de error; asumirá que deseas inventar una configuración nueva con ese nombre específico y la guardará de todas formas, provocando duplicados al listar los valores con `git config --global --list`.

Para solucionar esto, dispones de dos opciones:

### Método A: Eliminar el valor incorrecto desde la terminal (--unset)
Si identificas con precisión la línea errónea, solicita a Git que la remueva usando el parámetro `--unset`:
```bash
git config --global --unset init.defaulBranch
```
Si el error se repite en varias líneas idénticas y necesitas limpiar el registro por completo para reescribirlo adecuadamente, emplea `--unset-all`:
```bash
git config --global --unset-all init.defaultBranch
```

### Método B: Editar el archivo de configuración manualmente (--edit)
Todas tus configuraciones globales se almacenan en un archivo de texto plano oculto en tu sistema operativo llamado `.gitconfig`. Puedes abrir este documento directamente para corregirlo visualmente:
```bash
git config --global -e
```
Esto desplegará el archivo en tu editor predeterminado. Verás un texto estructurado de la siguiente forma:
```text
[user]
    name = Tu Nombre
    email = tu@email.com
[init]
    defaulBranch = main
    defaultBranch = main
```
Simplemente borra con tu teclado las líneas duplicadas o mal escritas, guarda los cambios del archivo y ciérralo. Tu registro quedará limpio.

---

## 5. ¿Cómo vincular tu proyecto con la nube?

### Camino A: Iniciar un repositorio local y subirlo a GitHub
Utiliza este flujo si ya comenzaste a desarrollar el código en tu computadora y deseas guardarlo en un repositorio nuevo en internet.

1. Inicializa el sistema de control de versiones en tu carpeta de proyecto (una vez por proyecto):
   ```bash
   git init
   ```
2. Añade y confirma tus archivos iniciales empleando `git add .` y `git commit`.
3. Crea un repositorio vacío en la plataforma web de GitHub y copia su dirección URL.
4. Vincula tu carpeta local con esa dirección remota del servidor (asociándole el nombre por defecto `origin`):
   ```bash
   git remote add origin https://github.com/tu-usuario/tu-repositorio.git
   ```
5. Sube tu historial local por primera vez y establece la sincronización de ramas con la bandera `-u`:
   ```bash
   git push -u origin main
   ```

### Camino B: Clonar un repositorio existente desde GitHub
Utiliza este flujo si el proyecto ya fue creado en la nube (por ti o por tu equipo) y necesitas descargarlo para comenzar a trabajar en él.

```bash
git clone  https://github.com/tu-usuario/tu-repositorio.git
```
El comando `clone` descarga el código completo, genera la carpeta interna oculta `.git` y configura automáticamente el enlace hacia el servidor remoto (`origin`). No debes ejecutar `git init` ni `git remote add` en este escenario.

---

## 6. Protocolos de Transferencia: HTTPS vs. SSH

Al clonar o subir información a GitHub, el servidor requiere verificar tu identidad y permisos de acceso:

* **HTTPS:** Emplea la URL convencional del navegador. Es simple de implementar al inicio, pero GitHub no admite contraseñas de usuario tradicionales a través de la terminal por motivos de seguridad; requiere que generes un Token de Acceso Personal (PAT) en la web, el cual expira periódicamente y debe renovarse.
* **SSH (Secure Shell):** Utiliza un mecanismo de llaves criptográficas (una llave privada que permanece resguardada en tu computadora y una llave pública que registras en tu cuenta de GitHub). Aunque requiere pasos adicionales para su generación inicial, una vez establecido no volverá a solicitar credenciales ni tokens en tus operaciones diarias. Es el estándar recomendado para el desarrollo profesional.