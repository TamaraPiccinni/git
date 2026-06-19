# Trabajo Colaborativo y Repositorios Remotos

Cuando trabajas de manera individual, eres la única persona que altera la línea de tiempo del proyecto. Sin embargo, en el ámbito laboral o académico, múltiples integrantes envían código a un mismo repositorio central de forma simultánea. Git establece directrices rigurosas para asegurar que el progreso de un desarrollador no destruya o sobrescriba de manera accidental el trabajo de otro.

---

## 1. Sincronización Obligatoria: Pull antes de Push

Considera el siguiente flujo de acontecimientos:
1. Al comenzar la jornada (10:00 AM), descargas la versión más reciente del proyecto a tu computadora.
2. Al mediodía (11:00 AM), una compañera de equipo concluye su sección de código y la sube al repositorio central en GitHub.
3. Por la tarde (12:00 PM), tú terminas tus desarrollos e intentas subirlos directamente mediante el comando `git push`.

**Resultado:** GitHub rechazará tu envío y bloqueará la transacción mediante un error que indica que el repositorio remoto contiene trabajo que no posees localmente ("Updates were rejected because the remote contains work that you do not have locally").

**Explicación técnica:** El servidor remoto contiene commits nuevos que no existen todavía en tu base de datos local. Si GitHub procesara tu envío a ciegas, el trabajo previo de tu compañera quedaría anulado y sobrescrito.

### El protocolo correcto de envío diario:

Para evitar este inconveniente, la rutina segura al trabajar en una rama compartida debe seguir este orden estricto:

1. **Confirma tus progresos locales:**
   ```bash
   git add .
   ```
   ```bash
   git commit -m "feat: implementar validacion de datos"
   ```

2. **Descarga e integra las novedades del servidor (Actualiza tu PC):**
   ```bash
   git pull origin dev
   ```
   *Nota: Si tú y tu compañera modificaron exactamente las mismas líneas en el mismo archivo, la terminal detendrá el proceso de descarga indicando un conflicto de fusión, el cual deberás resolver manualmente en tu editor antes de avanzar.*

3. **Ejecuta el envío definitivo:**
   ```bash
   git push origin dev
   ```
   Ahora la plataforma en la nube validará tu operación sin inconvenientes, dado que tu envío incorpora de manera armónica el historial de tus compañeros y tus propias novedades.

---

## 2. Diferencia Operativa entre Fetch y Pull

A veces quieres revisar qué ha hecho el equipo en el servidor, pero sin que ese código se mezcle inmediatamente con los archivos que estás editando en ese instante para evitar alteraciones inesperadas.

* **`git fetch` (Consultar el servidor):** Descarga a tu base de datos interna la información de todo lo nuevo que ha sucedido en GitHub (nuevas ramas creadas, commits del equipo), pero **no altera** tus archivos de trabajo vigentes ni modifica tu editor. Te permite analizar el panorama técnico antes de tomar una decisión.
* **`git pull` (Descargar e integrar):** Es una operación compuesta. Ejecuta de manera secuencial interna un `git fetch` para traer los datos del servidor y, de inmediato, realiza un `git merge` para acoplar dichos datos con la rama en la que estás trabajando en ese momento.

---

## 3. Clonar vs. Conectar Repositorios

Dependiendo de cómo empiece el proyecto en tu rutina de trabajo, usarás comandos distintos para establecer la conexión con los servidores remotos.

* **Si el proyecto ya existe en GitHub y eres nuevo en el equipo:**
  Utilizas el comando clonar. Solo se ejecuta la primera vez para descargar la estructura completa del proyecto a tu computadora.
  ```bash
  git clone https://github.com/tu-usuario/tu-repositorio.git
  ```
  Al clonar, Git configura de forma automática el enlace hacia el servidor remoto bajo el nombre por defecto `origin`.

* **Si el proyecto lo empezaste en tu PC y ahora quieres subirlo a GitHub:**
  Primero creas un repositorio vacío en la plataforma web de GitHub. Luego, le indicas a tu computadora la dirección de ese nuevo servidor remoto asociándole el nombre `origin`:
  ```bash
  git remote add origin https://github.com/tu-usuario/tu-repositorio.git
  ```

### ¿Qué significa la bandera "-u" en el primer Push?

La primera vez que subes una rama nueva a GitHub, debes indicarle a Git que vincule tu rama local con la rama remota correspondiente:
```bash
git push -u origin nombre-de-la-rama
```
El parámetro `-u` (upstream) crea este vínculo de seguimiento permanente. Gracias a esto, las próximas veces que quieras sincronizar código en esa misma rama, solo tendrás que escribir `git push` o `git pull`, y Git sabrá exactamente a qué servidor y rama dirigirse sin necesidad de especificar los nombres de nuevo.

---

## 4. Permisos en Repositorios Públicos: ¿Cualquiera puede modificar mi código?

Este punto genera dudas recurrentes al comenzar a utilizar GitHub. La respuesta es taxativa: **No, ninguna persona externa puede realizar cambios en tu código a menos que tú lo autorices explícitamente.**

Por defecto, los repositorios clasificados como públicos en GitHub operan bajo la premisa técnica de **Lectura universal y Escritura restringida**.

### Derechos de acceso públicos (Lectura)
Cualquier usuario conectado a internet posee la facultad de:
- Examinar la estructura de tu código fuente a través del portal web de GitHub.
- Clonar el repositorio completo en su estación local de trabajo (`git clone`).
- Inspeccionar la bitácora histórica de tus commits.

### Restricciones del repositorio (Escritura)
Si un usuario ajeno al proyecto descarga tu código, efectúa cambios locales en su computadora e intenta subirlos ejecutando `git push` hacia tu enlace, GitHub detendrá la conexión de inmediato mostrando un error de autenticación y acceso denegado. Tu código de origen permanece siempre resguardado.

### Mecanismos de Cooperación Autorizada

Si deseas trabajar conjuntamente con alumnos o colegas en el mismo repositorio, dispones de dos metodologías de gestión de accesos:

* **Colaboradores Directos (Para equipos de confianza):**
  Puedes otorgar permisos de escritura directos desde el menú web de GitHub ingresando a la ruta: **Settings > Collaborators > Add people**. Digita el nombre de usuario o correo de tu compañero. Una vez que este acepte la solicitud formal de invitación, compartirá contigo el derecho de utilizar el comando `git push` de forma directa en el repositorio.

* **Bifurcaciones y Solicitudes (Fork & Pull Request - Para contribuciones externas):**
  Si un programador ajeno a tu equipo encuentra tu proyecto y desea enmendar un error o plantear una optimización, el protocolo seguro es el siguiente:
  1. El usuario presiona el botón **Fork** en la interfaz de GitHub, lo cual genera una réplica exacta de tu proyecto guardada bajo el control de su propia cuenta de usuario.
  2. En su réplica personal, él sí goza de plenos derechos de escritura, por lo que realiza sus ediciones y ejecuta un `git push` hacia su propio perfil de GitHub.
  3. Finalmente, el usuario emite una solicitud de revisión denominada **Pull Request (PR)** hacia tu repositorio de origen.
  4. Recibirás una notificación técnica en tu tablero web donde podrás inspeccionar minuciosamente, línea por línea, los cambios sugeridos. Si consideras que la propuesta es idónea y segura, puedes aprobar la solicitud para que Git ensamble los códigos automáticamente; si la consideras errónea, la rechazas sin comprometer tus archivos.

### Protección de Ramas Principales

Incluso en entornos compartidos donde has configurado colaboradores aprobados, existe la posibilidad de que un miembro del equipo incurra en una distracción y envíe código incompleto o roto directamente a la rama raíz de producción. Para mitigar este riesgo, puedes establecer reglas de restricción en la plataforma de GitHub ingresando en **Settings > Branches**:
- Al activar una regla de protección sobre la rama `main`, puedes inhabilitar por completo los comandos de push directos sobre ella.
- Esto obligará a todos los desarrolladores (incluido el administrador del proyecto) a crear obligatoriamente una rama auxiliar (como `dev`), subirla por separado al servidor y abrir una solicitud de Pull Request para que la fusión del código sea evaluada antes de ser integrada formalmente en la línea de tiempo estable del software.

## 5. Cómo descargar todas las ramas y cambios del servidor (git fetch --all)

Un error frecuente es pensar que `git pull` traerá y actualizará todas las ramas del repositorio en tu computadora. En realidad, `git pull` solo descarga e integra los cambios en la rama activa en la que te encuentres posicionado en ese instante.

Si lo que necesitas es actualizar la base de datos de tu computadora con absolutamente todas las ramas, cambios y commits que existen en GitHub (sin fusionar nada ni alterar tus archivos actuales), debes usar el comando de consulta completa.

### El comando de descarga masiva
```bash
git fetch --all
```

### ¿Qué sucede cuando ejecutas este comando?
1. Git se conecta a GitHub y revisa si tus compañeros crearon ramas nuevas o subieron commits en ramas que tú no tenías registradas.
2. Descarga el historial completo de todas esas ramas hacia tu repositorio local (la carpeta oculta `.git`).
3. No toca ni modifica ninguno de los archivos de texto en los que estés trabajando en tu editor de código. Es una operación completamente segura que no genera conflictos.

### Cómo ver y usar las ramas descargadas
Una vez que ejecutaste el fetch, puedes listar todas las ramas (tanto las que ya tienes activas en tu computadora como las que están guardadas en el servidor remoto) con el siguiente comando:
```bash
git branch -a
```
Las ramas que están en la nube pero aún no has abierto en tu computadora aparecerán listadas de un color diferente y con el prefijo `remotes/origin/`.

Si quieres empezar a trabajar en una de esas ramas nuevas que creó un compañero y que acabas de descargar con el fetch, simplemente ejecutas el comando de cambio convencional:
```bash
git switch nombre-de-la-rama-remota
```
Git detectará automáticamente que esa línea de tiempo ya fue descargada desde el servidor, creará una copia local idéntica en tu computadora y te posicionará en ella para que puedas comenzar a colaborar.