# Curso Práctico de Git y GitHub

Bienvenido a este curso diseñado desde cero. Para evitar la saturación de información en una sola página, este repositorio está estructurado en módulos conceptuales y prácticos. Sigue el mapa de contenido para avanzar paso a paso.

## Mapa del Curso

* [Instalación según Sistema Operativo](docs/instalacion-os.md): Guía de instalación y particularidades de la terminal nativa para usuarios de Linux y macOS.
* [Manual de Configuración Inicial](docs/configuracion.md): Qué es la terminal, la diferencia entre Git local y GitHub remoto, cómo configurar tu entorno y cómo solucionar errores de duplicados.
* [Uso de Gitignore](docs/gitignore.md): Qué es y cómo evitar subir archivos basura, carpetas pesadas (como dependencias) o contraseñas al servidor.
* [El Historial y Viajes en el Tiempo](docs/historial.md): Cómo monitorear tus archivos y moverte entre versiones anteriores de tu código de forma segura.
* [Trabajo con Ramas y Estrategias](docs/ramas.md): Por qué evitar la rama main, cómo utilizar la rama dev y cómo fusionar tus cambios correctamente.
* [Trabajo Colaborativo en Equipo](docs/colaborativo.md): El flujo correcto de pull y push, resolución de sincronización y control de permisos en repositorios públicos.
* [Glosario para Principiantes](docs/glosario.md): Un diccionario con analogías sencillas para entender toda la terminología técnica de Git.

---

## Guía de Inicio Rápido (Flujo Diario)

Si ya instalaste y configuraste tu entorno y solo necesitas recordar el orden técnico de los comandos que debes seguir en tu día a día, utiliza este esquema:

1. Ver el estado actual de tus archivos y en qué rama estás parado:
```bash
   git status
   ```

2. Preparar los archivos modificados que vas a guardar:
```bash
   git add .
   ```

3. Registrar la instantánea o "foto" de tu código en el historial local:
```bash
   git commit -m "feat(scope): mensaje descriptivo"
   ```

4. Descargar las actualizaciones de tus compañeros antes de subir las tuyas:
```bash
   git pull origin nombre-de-tu-rama
   ```

5. Subir tus cambios confirmados al servidor en la nube (GitHub):
```bash
   git push origin nombre-de-tu-rama
   ```

---

## Recursos Útiles

* [Documentación Oficial de Git](https://git-scm.com/doc)
* [Guía de Markdown](https://www.markdownguide.org/basic-syntax/)
* [Conventional Commits](https://www.conventionalcommits.org/es/v1.0.0/)