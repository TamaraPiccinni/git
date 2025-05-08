# Curso práctico de Git y GitHub

## Índice

- [Navegación básica en la terminal](#navegaci%C3%B3n-b%C3%A1sica-en-la-terminal)
- [Manejo de archivos y carpetas](#manejo-de-archivos-y-carpetas)
- [Inicializar un repositorio Git](#inicializar-un-repositorio-git)
- [Flujo básico de trabajo con Git](#flujo-b%C3%A1sico-de-trabajo-con-git)
- [Modificar y deshacer cambios](#modificar-y-deshacer-cambios)
- [Volver a versiones anteriores](#volver-a-versiones-anteriores)
- [Ramas y flujo de trabajo](#ramas-y-flujo-de-trabajo)
- [Trabajo con repositorios remotos](#trabajo-con-repositorios-remotos)
- [Resolución de conflictos](#resoluci%C3%B3n-de-conflictos)
- [Configuración de llaves SSH](#configuraci%C3%B3n-de-llaves-ssh)
- [Recursos útiles](#recursos-%C3%BAtiles)

---

## Navegación básica en la terminal

```bash
pwd             # Ruta actual
cd carpeta      # Entrar a una carpeta
cd ..           # Subir un nivel
cd ~            # Ir al home
ls              # Ver archivos y carpetas
ls -a           # Incluir ocultos
clear           # Limpiar la pantalla
```

---

## Manejo de archivos y carpetas

```bash
mkdir nombre             # Crear carpeta
touch archivo.txt        # Crear archivo vacío
cat archivo.txt          # Ver contenido
rm archivo.txt           # Borrar archivo
rm -r carpeta/           # Borrar carpeta completa
code .                   # Abrir carpeta en VSCode
```

---

## Inicializar un repositorio Git

```bash
git init                                 # Crear repositorio
git config --global user.name "Tu Nombre"
git config --global user.email "tu@email.com"
```

---

## Flujo básico de trabajo con Git

```bash
git status                 # Ver estado actual
git add archivo.txt        # Agregar archivo al staging
git add .                  # Agregar todos los cambios
git commit -m "Mensaje"    # Crear commit
git log                    # Historial de commits
```

---

## Modificar y deshacer cambios

```bash
git rm --cached archivo.txt   # Quitar archivo del staging
git diff                      # Ver diferencias
git commit -am "Mensaje"      # Add + Commit en archivos ya trackeados
```

---

## Volver a versiones anteriores

```bash
git log                          # Ver historial
git reset --soft <hash>         # Volver atrás, mantener cambios en staging
git reset --mixed <hash>        # Volver atrás, mantener cambios sin staging
git reset --hard <hash>         # Volver y borrar todo

# Recuperar un archivo específico
git checkout <hash> archivo     # Recuperar archivo de commit anterior
git checkout main archivo       # Recuperar desde rama principal
```

---

## Ramas y flujo de trabajo

```bash
git branch nombre-rama         # Crear rama
git checkout nombre-rama       # Cambiar de rama
git merge nombre-rama          # Fusionar con rama actual
git branch -d nombre-rama      # Borrar rama local
```

> Convenciones comunes: `feature/`, `hotfix/`, `release/`

---

## Trabajo con repositorios remotos

```bash
git clone url_repo             # Clonar repositorio

git remote add origin url      # Enlazar repo local con GitHub
git push -u origin main        # Subir por primera vez
git push                       # Subir cambios
git fetch                      # Obtener cambios remotos sin mezclar
git merge                      # Unir cambios remotos con los locales
git pull                       # Traer y unir en un paso (fetch + merge)
```

---

## Resolución de conflictos

1. Git marca las diferencias en conflicto con:

```text
<<<<<<< HEAD
código en rama actual
=======
código en rama a fusionar
>>>>>>> rama
```

2. Editar y decidir qué conservar.
3. Borrar las marcas (`<<<<<<<`, `=======`, `>>>>>>>`).
4. Guardar y confirmar:

```bash
git add archivo
git commit -m "Conflicto resuelto"
```

> Si querés cancelar el merge:

```bash
git merge --abort
```

---

## Configuración de llaves SSH

Las llaves SSH permiten autenticación segura con GitHub sin ingresar contraseña.

```bash
ssh-keygen -t rsa -b 4096 -C "tu@email.com"
eval $(ssh-agent -s)
ssh-add ~/.ssh/id_rsa
cat ~/.ssh/id_rsa.pub         # Copiar y pegar en GitHub (Settings > SSH keys)
```
---

## Recursos útiles

- [Git - Documentación oficial](https://git-scm.com/doc)
- [Guía Markdown](https://www.markdownguide.org/basic-syntax/)
- [GitHub SSH Keys](https://docs.github.com/es/authentication/connecting-to-github-with-ssh)
- [Git Branching Model (GitFlow)](https://nvie.com/posts/a-successful-git-branching-model/)

---

## Comandos adicionales útiles

```bash
history                     # Ver historial de comandos
!número                     # Ejecutar comando del historial

git log --oneline           # Ver resumen de commits
git log --graph --decorate --all --oneline   # Visualizar ramas

git shortlog                # Resumen por autor
git log -p                  # Ver los parches (diffs)
git log --stat              # Ver cambios por archivo
git log --author="Nombre"
git log --after="2023-01-01"
git log --grep="Texto"
```

---



