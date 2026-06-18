# Curso Práctico de Git y GitHub

Bienvenido a este curso diseñado desde cero. Para evitar que te abrumes con tanta información en una sola página, este repositorio está dividido en módulos conceptuales y prácticos. Sigue el mapa de contenido para avanzar paso a paso.

## Mapa del Curso

* [Manual de Configuración Inicial](docs/configuracion.md): Aprende qué es la terminal, la diferencia entre Git local y GitHub remoto, y cómo configurar tu entorno (HTTPS vs. SSH).
* [El Historial y Viajes en el Tiempo](docs/historial.md): Aprende a monitorear tus archivos y a moverte entre versiones anteriores sin romper nada.
* [Trabajo con Ramas y Estrategias](docs/ramas.md): Descubre por qué nunca debes trabajar en la rama main, cómo usar la rama dev y cómo fusionar tus cambios.
* [Glosario para Principiantes](docs/glosario.md): Un diccionario con analogías sencillas para entender los términos técnicos de Git.

---

## Guía de Inicio Rápido (Los 5 Mandamientos)

Si ya configuraste tu entorno y necesitas recordar el flujo diario, este es el orden técnico que debes seguir:

1. Ver dónde estás parado y qué cambió:
   ```bash
   git status
   ```

2. Preparar los archivos que vas a guardar:
   ```bash
   git add .
   ```

3. Tomar la "foto" o registro de tu código:
   ```bash
   git commit -m "feat(scope): mensaje descriptivo"
   ```

4. Traer cambios de tus compañeros antes de subir los tuyos:
   ```bash
   git pull origin nombre-de-tu-rama
   ```

5. Subir tus cambios a la nube (GitHub):
   ```bash
   git push origin nombre-de-tu-rama
   ```

---

## Recursos Útiles

* [Documentación Oficial de Git](https://git-scm.com/doc)
* [Guía de Markdown](https://www.markdownguide.org/basic-syntax/)
* [Conventional Commits](https://www.conventionalcommits.org/es/v1.0.0/)