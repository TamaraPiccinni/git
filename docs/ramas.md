# Gestión de Ramas (Branching) y Fusión de Cambios

Las ramas constituyen una de las herramientas más robustas de Git. Te permiten bifurcar el desarrollo del proyecto en líneas de tiempo paralelas para experimentar, estructurar nuevas funcionalidades o corregir fallos técnicos sin alterar el código centralizado que ya se encuentra operativo.

---

## 1. Estrategia de Ramificación Profesional

Trabajar de manera exclusiva sobre la rama raíz deteriora la organización del software en entornos compartidos. Estructurar el repositorio en niveles de estabilidad protege el código final de producción:



* **Rama `main` (Producción):** Es la línea de tiempo definitiva y estable del proyecto. Alberga únicamente el código que ha sido testeado, aprobado y se encuentra listo para su despliegue final o publicación. Queda estrictamente desaconsejado realizar commits directos sobre ella.
* **Rama `dev` (Desarrollo):** Funciona como la rama integradora común del equipo. Aquí se fusionan las tareas particulares completadas por cada integrante con el fin de realizar pruebas generales antes de actualizar la rama `main`.
* **Ramas `feature/` (Funcionalidades):** Líneas de tiempo auxiliares e independientes que nacen a partir de `dev` para resolver una tarea muy concreta (por ejemplo: `feature/interfaz-registro`). Al completarse la funcionalidad, se integran de regreso a la rama `dev` y se eliminan del entorno local.

---

## 2. Comandos Esenciales para la Gestión de Ramas

Aprende a desplazarte con exactitud entre tus líneas de desarrollo:

* **Listar las ramas disponibles en tu entorno local:**
  ```bash
  git branch
  ```
  Desplegará las ramas de tu equipo. Aquella que presente un asterisco y un color distintivo señala la rama en la cual te encuentras posicionado actualmente.

* **Crear una rama nueva:**
  ```bash
  git branch dev
  ```
  Genera la rama `dev`, tomando como base inicial el estado exacto del último commit de la rama donde estás situado en ese momento.

* **Cambiar de línea de tiempo:**
  ```bash
  git switch dev
  ```
  Traslada tus herramientas de trabajo a la rama seleccionada. Los archivos dentro de tu editor de código se actualizarán automáticamente para mostrar el contenido correspondiente a esa rama.

* **Comando combinado (Crear y cambiar de rama simultáneamente):**
  ```bash
  git switch -c feature/nueva-interfaz
  ```
  La bandera `-c` (create) ejecuta la creación de la rama y te posiciona en ella en un solo paso. Es la instrucción más habitual en las rutinas de programación.

---

## 3. ¿Cómo fusionar el trabajo al finalizar el proyecto? (git merge)



El proceso de fusión toma las modificaciones registradas en una rama de desarrollo y las incorpora cronológicamente en otra. Para efectuar la fusión de manera adecuada, debes situarte siempre sobre la rama **destino** (aquella que recibirá los nuevos datos).

### Ejemplo práctico: Integrar la rama `dev` consolidada dentro de la rama estable `main`

Supongamos que tu equipo ha concluido el desarrollo del software en la rama `dev`, realizaron todas las pruebas de control necesarias y desean publicar la actualización definitiva en `main`. Debes ejecutar la siguiente secuencia en tu terminal:

1. Asegúrate de que no conservas archivos sueltos modificados sin confirmar. Ejecuta `git status` para verificar que tu espacio de trabajo se encuentre limpio.
2. Desplázate hacia la rama destino que asimilará las mejoras (en este caso, `main`):
   ```bash
   git switch main
   ```
3. Ejecuta la fusión llamando al nombre de la rama origen que contiene las novedades:
   ```bash
   git merge dev
   ```
4. Git evaluará las dos líneas históricas. Si las modificaciones no se superponen en las mismas líneas de código, se unificarán automáticamente mediante la creación de un commit especial denominado "Merge Commit". La rama `main` quedará al día.

---

## 4. Eliminación de Ramas Secundarias

Una vez concluida la integración de una funcionalidad con éxito, su rama de soporte deja de cumplir un propósito técnico en el repositorio. Eliminar las ramas obsoletas optimiza la lectura general de la cronología del software.

* **Eliminar una rama de forma segura en tu entorno local:**
  ```bash
  git branch -d feature/nueva-interfaz
  ```
  Git validará la operación y solo te permitirá borrarla si sus datos ya fueron fusionados con otra rama del proyecto.

* **Forzar la eliminación de una rama local:**
  ```bash
  git branch -D feature/experimento-fallido
  ```
  Útil para descartar pruebas de código que no planeas integrar en ninguna parte del proyecto; borra la rama sin verificar remanentes.

---

## 5. ¿Qué es un conflicto de fusión (Merge Conflict)?

Si dos desarrolladores editan **la misma línea del mismo archivo** en ramas diferentes con soluciones distintas, Git no podrá determinar cuál de las dos alternativas debe prevalecer y detendrá la automatización del proceso de fusión de manera inmediata.

La consola arrojará un aviso de alerta y los archivos afectados se reescribirán temporalmente mostrando etiquetas visuales en tu editor que deberás inspeccionar manualmente:

```text
<<<<<<< HEAD
Código original presente en tu rama de destino actual (main)
=======
Código entrante de la rama que intentas incorporar (dev)
>>>>>>> dev
```

### Pasos para solucionar un conflicto:
1. Abre el archivo en conflicto con tu editor de código (como VSCode).
2. Borra las delimitaciones técnicas del texto (`<<<<<<<`, `=======`, `>>>>>>>`).
3. Evalúa con tu equipo de trabajo cuál de los dos bloques de código debe conservarse, o genera una solución integrada que unifique ambas partes. Limpia el archivo dejando solo el código final deseado.
4. Guarda el archivo, añádelo al área de preparación con `git add nombre-del-archivo` y culmina formalmente el merge registrando un commit regular:
   ```bash
   git commit -m "fix: resolucion de conflictos en archivo principal"
   ```