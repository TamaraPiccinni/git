# El Historial y Viajes en el Tiempo

Git funciona como una cámara fotográfica de alta fidelidad para tu código. Cada "foto" es un commit que guarda el estado exacto de tus archivos en ese instante.

## 1. Comandos de Inspección Básica

Antes de moverte en el tiempo, necesitas saber dónde estás parado y qué fotos has tomado:

* `git status`: Te dice el estado actual de tu directorio de trabajo. Te muestra qué archivos modificaste, cuáles no estás siguiendo todavía y en qué rama estás. Úsalo constantemente.
* `git log`: Te muestra la lista completa de commits realizados, el autor, la fecha y el mensaje descriptivo.
* `git log --oneline`: Una versión compacta y ultra legible. Te muestra cada commit en una sola línea junto a su "Hash" (el ID único de 7 caracteres).

---

## 2. Viajar en el Tiempo: Explorar vs. Modificar

Para viajar al pasado, necesitas el Hash del commit al que deseas ir (lo obtienes con `git log --oneline`).

### Modo Explorador (git checkout)
Si solo quieres ver cómo lucía tu proyecto hace tres días para revisar una función o recordar cómo hiciste algo, pero no quieres borrar nada de lo que hiciste después:

```bash
git checkout 1a2b3c4
```
Esto te coloca en un estado llamado "detached HEAD" (cabecera desprendida). Puedes leer el código antiguo tranquilamente. 

Para regresar al presente de forma segura sin alterar nada:
```bash
git switch main
```

### Modo Modificador / Destructivo (git reset)
Si cometiste un error grave y necesitas borrar commits para regresar firmemente al pasado. Existen tres niveles de intensidad:

1. **Reset Suave (`--soft`):** Borra los commits del historial, pero conserva todos los cambios de tus archivos intactos dentro del Staging Area (listos para volver a hacer commit). Nada de código se pierde.
   ```bash
   git reset --soft 1a2b3c4
   ```

2. **Reset Mezclado (`--mixed` / Opción por defecto):** Borra los commits del historial y saca los cambios del Staging Area, pero conserva tus archivos modificados en tu carpeta. El código sigue ahí, listo para que lo revises y decidas qué añadir de nuevo.
   ```bash
   git reset --mixed 1a2b3c4
   ```

3. **Reset Duro (`--hard`):** Peligro. Borra los commits, borra el Staging Area y elimina por completo cualquier modificación en tus archivos físicos. Tu proyecto regresa exactamente a como estaba en ese commit antiguo. Lo que no se guardó en un commit previo se pierde para siempre.
   ```bash
   git reset --hard 1a2b3c4
   ```