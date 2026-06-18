# Curso Práctico de Git y GitHub

Bienvenido a este curso diseñado desde cero. Para evitar la saturación de información en una sola página, este repositorio está estructurado en módulos conceptuales y prácticos. Sigue el mapa de contenido para avanzar paso a paso.

## Mapa del Curso

* [Manual de Configuración Inicial](docs/configuracion.md): Qué es la terminal, la diferencia entre Git local y GitHub remoto, cómo configurar tu entorno (HTTPS vs. SSH) y cómo solucionar errores de duplicados.
* [El Historial y Viajes en el Tiempo](docs/historial.md): Cómo monitorear tus archivos y moverte entre versiones anteriores sin romper nada.
* [Trabajo con Ramas y Estrategias](docs/ramas.md): Por qué nunca debes trabajar en la rama main, cómo usar la rama dev y cómo fusionar tus cambios de forma segura.
* [Trabajo Colaborativo en Equipo](docs/colaborativo.md): El flujo correcto de pull y push, control de permisos en repositorios públicos y protección de ramas.
* [Glosario para Principiantes](docs/glosario.md): Un diccionario con analogías sencillas para entender los términos técnicos de Git.

---

## Guía de Inicio Rápido (Flujo Diario Diario)

Si ya configuraste tu entorno y necesitas recordar el orden técnico que debes seguir en tu día a día, utiliza este esquema:

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