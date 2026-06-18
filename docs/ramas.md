# Trabajo con Ramas (Branching) y Estrategia

Las ramas son la característica más poderosa de Git. Te permiten crear líneas de tiempo paralelas para experimentar, programar nuevas funciones o corregir errores sin alterar el código que ya funciona.

## 1. La Regla de Oro: ¡No trabajes en Main!

La rama `main` (o antigua `master`) representa el código sagrado de tu aplicación: el código que está en producción, funcionando y sin errores. 

Si programas directamente en `main` y cometes un error intermedio, romperás la versión estable del proyecto. En entornos profesionales y educativos, trabajar directo en `main` está estrictamente desaconsejado.

### El Flujo Ideal para Principiantes

1. **Main:** Línea estable de producción.
2. **Dev (Desarrollo):** Una rama paralela a `main` donde se unifican las tareas de todo el equipo antes de subirlas definitivamente a producción.
3. **Features (Características):** Ramas independientes creadas a partir de `dev` para realizar una sola tarea específica (ej: estructurar el formulario de contacto).

---

## 2. Comandos Esenciales para Ramas

```bash
# Ver las ramas locales que existen (la que tiene un asterisco es la actual)
git branch

# Crear una nueva rama basada en la que estás parado actualmente
git branch dev

# Cambiar de rama (Forma moderna)
git switch dev

# Atajo: Crear una rama nueva y cambiarte a ella inmediatamente
git switch -c feature/login-form

# Borrar una rama local (solo si ya fusionaste sus cambios con otra)
git branch -d feature/login-form

# Forzar el borrado de una rama (aunque pierdas los cambios no fusionados)
git branch -D feature/experimento-fallido
```

---

## 3. ¿Cómo fusionar el trabajo al finalizar el proyecto? (git merge)

Cuando el equipo ha trabajado en diferentes características dentro de la rama de desarrollo (`dev`) y el proyecto está listo, estable y probado, es momento de llevar todos esos cambios a la rama principal (`main`) para publicarlos.

Para fusionar la rama `dev` dentro de `main`, debes seguir estos pasos en orden estricto:

1. Asegúrate de haber guardado y confirmado todos los cambios pendientes en tu rama actual con `git add .` y `git commit`.

2. Cámbiate a la rama que va a recibir los cambios (la rama destino, que en este caso es `main`):
   ```bash
   git switch main
   ```

3. Trae los cambios de la rama de desarrollo hacia tu rama actual:
   ```bash
   git merge dev
   ```

4. Si todo el código es compatible, Git unirá las dos líneas de tiempo de forma automática. Ahora la rama `main` estará completamente actualizada con el último trabajo del equipo.