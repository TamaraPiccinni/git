# El Archivo .gitignore (Ignorar Archivos)

Cuando trabajas en un proyecto de software, tu editor de código, el sistema operativo y los gestores de paquetes crean archivos temporales, carpetas de dependencias o configuraciones personales que no forman parte del código fuente del proyecto. 

Subir estos archivos a GitHub satura el servidor, ralentiza las descargas y puede exponer información confidencial. Para evitar esto de forma automática, utilizamos el archivo `.gitignore`.

---

## 1. ¿Qué es .gitignore?

Es un archivo de texto plano que se coloca en la raíz del repositorio local. Su nombre debe empezar estrictamente por un punto y escribirse todo en minúsculas: `.gitignore`. 

Dentro de este archivo, escribes los nombres de las carpetas, archivos o extensiones que Git debe omitir por completo. Una vez registrados ahí, Git los ignorará, lo que significa que nunca aparecerán en el comando `git status` ni se incluirán al ejecutar `git add .`.



---

## 2. ¿Qué tipos de archivos debemos ignorar?

Por regla general, hay tres categorías de archivos que nunca deben subirse al repositorio central:

* **Dependencias de software:** Carpetas generadas automáticamente por los gestores de paquetes que contienen miles de archivos de librerías externas necesarias para que el proyecto corra localmente (por ejemplo, `node_modules` en proyectos de Node.js o `venv` en entornos virtuales de Python). Estas carpetas se pueden volver a generar en cualquier computadora ejecutando un comando de instalación, por lo que subirlas es redundante y pesado.
* **Archivos del Sistema Operativo o del Editor:** Archivos ocultos que crea tu computadora para recordar la disposición de las ventanas o configuraciones de tu editor de código (como la carpeta `.vscode` de Visual Studio Code o los archivos `.DS_Store` en sistemas Mac).
* **Variables de Entorno y Credenciales:** Archivos que contienen contraseñas de bases de datos, claves de APIs privadas o tokens de acceso (habitualmente archivos `.env`). Si subes estos archivos a un repositorio público, cualquier persona en internet podría acceder a tus servicios privados.

---

## 3. Sintaxis básica para escribir un .gitignore

La escritura dentro del archivo es línea por línea y utiliza reglas sencillas:

```text
# Los textos que empiezan con numeral son comentarios y Git no los lee

# Ignorar un archivo específico con su nombre y extensión
config.json

# Ignorar una carpeta completa y todo su contenido (se usa la barra diagonal)
node_modules/
venv/

# Ignorar todos los archivos que tengan una extensión específica (se usa el asterisco)
*.log
*.env
```

---

## 4. Cómo crear e implementar el archivo paso a paso

El mejor momento para configurar el `.gitignore` es inmediatamente después de ejecutar `git init`, antes de hacer el primer commit del proyecto.

1. En la raíz de tu proyecto, crea un nuevo archivo y nómbralo `.gitignore`.
2. Abre el archivo en tu editor de código y añade las líneas necesarias según la tecnología que estés usando.
3. Guarda el archivo.
4. Ejecuta `git status` en la terminal. Notarás que las carpetas y archivos pesados que listaste en el archivo ya no aparecen como elementos pendientes de seguimiento. Git ahora solo ve el propio archivo `.gitignore`.
5. Registra el archivo en tu historial:
   ```bash
   git add .gitignore
   ```
   ```bash
   git commit -m "chore: agregar archivo gitignore"
   ```

---

## 5. Qué hacer si Git ya está siguiendo un archivo que querías ignorar

Un error técnico muy habitual sucede cuando creas el archivo `.gitignore` tarde, cuando Git ya había guardado previamente una carpeta pesada (como `node_modules`) en un commit anterior. 

Si simplemente escribes el nombre de la carpeta en el `.gitignore` después de haberla guardado, Git continuará registrando sus cambios porque el archivo ya está bajo el control del repositorio.

Para obligar a Git a dejar de seguir un archivo o carpeta sin borrarlo de tu computadora física, debes removerlo explícitamente de la memoria de Git (el caché):

* **Para dejar de seguir una carpeta completa:**
  ```bash
  git rm -r --cached node_modules/
  ```

* **Para dejar de seguir un archivo individual:**
  ```bash
  git rm --cached archivo_secreto.txt
  ```

Tras ejecutar este comando, la carpeta o archivo saldrá del control de versiones. El paso final es realizar un commit para asentar este cambio en el historial local:
```bash
git commit -m "chore: remover archivos innecesarios del control de versiones"
```