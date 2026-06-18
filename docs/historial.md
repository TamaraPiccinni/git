# Gestión de Ramas y Trabajo en Equipo (Guía Completa)

Las ramas (branches) son el núcleo del desarrollo colaborativo y profesional. Permiten que múltiples programadores trabajen de forma paralela en el mismo proyecto sin interferir con el código de los demás ni romper la versión que ya funciona.

---

## 1. Estrategia de Ramificación Profesional (GitFlow Simplificado)

Un error común al iniciar es realizar todas las modificaciones sobre la rama principal. En proyectos reales, el trabajo se divide en niveles de estabilidad para proteger el código final:



* **Rama `main` (Producción):** Es la rama sagrada. Contiene el código que ya está publicado, probado y funcionando sin errores. Nunca se programa directamente aquí.
* **Rama `dev` (Desarrollo):** Es la rama de integración. Aquí se unen las tareas terminadas de todos los miembros del equipo. Es una zona de pruebas antes de pasar a `main`.
* **Ramas `feature/` (Características):** Son ramas temporales creadas para desarrollar una tarea específica (ej: `feature/boton-pago`, `feature/formulario-contacto`). Nacen de `dev` y, al terminar la tarea, se fusionan de vuelta a `dev` y se eliminan.

---

## 2. Comandos para crear y navegar entre ramas

Para trabajar con este flujo, necesitas moverte con precisión entre las líneas de tiempo locales:

* **Listar ramas existentes:**
  ```bash
  git branch
  ```
  Muestra las ramas de tu computadora. La rama que tenga un asterisco al lado y cambie de color es la rama en la que estás parado actualmente.

* **Crear una rama nueva:**
  ```bash
  git branch dev
  ```
  Crea la rama `dev`, tomando como punto de partida exacto el commit de la rama donde te encuentres en ese instante.

* **Cambiar de rama:**
  ```bash
  git switch dev
  ```
  Mueve tus herramientas de trabajo a la rama `dev`. Los archivos de tu editor de código cambiarán automáticamente para reflejar el estado de esa rama.

* **Atajo definitivo (Crear y cambiar en un solo paso):**
  ```bash
  git switch -c feature/nueva-interfaz
  ```
  El parámetro `-c` significa "create". Crea la rama interna y te mueve a ella inmediatamente. Es el comando más utilizado en el día a día.

---

## 3. Integración de Código: Cómo hacer un Merge paso a paso



El proceso de fusión (`git merge`) consiste en tomar los cambios de una rama secundaria e integrarlos cronológicamente en una rama principal o de integración. 

Para realizar una fusión de forma correcta, debes situarte siempre en la rama **destino** (la rama que va a recibir el código nuevo).

### Caso de uso real: Llevar el trabajo terminado de `dev` a la rama estable `main`

Imagina que tu equipo trabajó en la rama `dev`, probaron la aplicación y todo funciona de maravilla. Ahora quieren publicar esa nueva versión en `main`. Sigue este orden estricto de comandos en tu terminal:

1. Asegúrate de que no tienes archivos sueltos sin guardar. Ejecuta `git status` y confirma que tu directorio de trabajo está limpio.
2. Cámbiate a la rama destino que recibirá las actualizaciones (en este caso, `main`):
   ```bash
   git switch main
   ```
3. Ejecuta la fusión indicando el nombre de la rama origen (la que contiene las novedades):
   ```bash
   git merge dev
   ```
4. Git analizará la historia de ambas ramas. Si no hay líneas de código que entren en conflicto, unirá los cambios de forma automática creando un "Commit de fusión" (Merge Commit).

---

## 4. Gestión y limpieza de ramas remotes

Una vez que una característica ha sido fusionada con éxito y su código ya forma parte de la línea principal, la rama secundaria deja de ser útil. Mantener decenas de ramas viejas dificulta la lectura del repositorio.

* **Borrar la rama local de forma segura:**
  ```bash
  git branch -d feature/nueva-interfaz
  ```
  Git solo te permitirá borrarla si sus cambios ya fueron fusionados con otra rama.

* **Forzar el borrado local (en caso de experimentos fallidos):**
  ```bash
  git branch -D feature/experimento-roto
  ```
  Borra la rama sin importar si perdiste código que no se integró en ningún lado.

---

## 5. ¿Qué es un conflicto de fusión (Merge Conflict)?

Cuando intentas hacer un `git merge`, Git intenta fusionar el código automáticamente línea por línea. Sin embargo, si dos programadores modificaron **la misma línea del mismo archivo** en ramas diferentes con textos distintos, Git no sabrá cuál versión es la correcta y detendrá el proceso de fusión.

Aparecerá una alerta en la terminal avisando que hay un conflicto. El archivo afectado mostrará unas marcas visuales que debes resolver manualmente en tu editor de código antes de poder continuar:

```text
<<<<<<< HEAD
Código que estaba en tu rama actual (main)
=======
Código nuevo que viene de la rama que quieres fusionar (dev)
>>>>>>> dev
```

### Cómo solucionarlo:
1. Abre el archivo en tu editor de código (como VSCode).
2. Borra las marcas (`<<<<<<<`, `=======`, `>>>>>>>`).
3. Habla con tu equipo o analiza cuál de las dos opciones de código debe conservarse (o si debes combinar ambas). Dejas solo el código definitivo.
4. Guarda el archivo, prepáralo con `git add <archivo>` y finaliza el proceso registrando un commit normal mediante `git commit -m "Fix: resolución de conflictos"`.