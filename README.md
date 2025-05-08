# Curso práctico de Git y GitHub

## Índice

* [Terminal: navegación y manejo de archivos](#terminal-navegación-y-manejo-de-archivos)
* [Configuración inicial de Git](#configuración-inicial-de-git)
* [Flujo de trabajo básico](#flujo-de-trabajo-básico)
* [Modificar y deshacer cambios](#modificar-y-deshacer-cambios)
* [Volver a versiones anteriores](#volver-a-versiones-anteriores)
* [Trabajo con ramas](#trabajo-con-ramas)
* [Repositorios remotos](#repositorios-remotos)
* [Resolución de conflictos](#resolución-de-conflictos)
* [Llaves SSH](#llaves-ssh)
* [Buenas prácticas](#buenas-prácticas)
* [Commits convencionales](#commits-convencionales)
* [Commitlint y Husky](#commitlint-y-husky)
* [Recursos útiles](#recursos-útiles)

---

## Terminal: navegación y manejo de archivos

```bash
pwd                  # Ruta actual
cd carpeta           # Entrar a una carpeta
cd ..                # Subir un nivel
cd ~                 # Ir al home
ls                   # Ver archivos y carpetas
ls -a                # Incluir ocultos
clear                # Limpiar pantalla

mkdir nombre         # Crear carpeta
touch archivo.txt    # Crear archivo vacío
cat archivo.txt      # Ver contenido
rm archivo.txt       # Borrar archivo
rm -r carpeta/       # Borrar carpeta completa
code .               # Abrir carpeta en VSCode
```

---

## Configuración inicial de Git

```bash
git init                                  # Inicializar repositorio
git config --global user.name "Tu Nombre"
git config --global user.email "tu@email.com"
```

---

## Flujo de trabajo básico

```bash
git status                 # Ver estado
git add archivo.txt        # Agregar archivo al staging
git add .                  # Agregar todos los cambios
git commit -m "Mensaje"    # Crear commit
git log                    # Ver historial
git commit -am "Mensaje"   # Add + Commit archivos ya trackeados
```

---

## Modificar y deshacer cambios

```bash
git rm --cached archivo.txt  # Quitar del staging
git diff                     # Ver diferencias
```

---

## Volver a versiones anteriores

```bash
git reset --soft <hash>     # Mantiene cambios en staging
git reset --mixed <hash>    # Mantiene cambios sin staging
git reset --hard <hash>     # Borra todo

# Recuperar archivo específico
git checkout <hash> archivo
git checkout main archivo
```

---

## Trabajo con ramas

```bash
git branch nombre-rama         # Crear rama
git checkout nombre-rama       # Cambiar de rama
git switch nombre-rama         # Alternativa moderna
git checkout -b nueva-rama     # Crear y cambiar
git merge nombre-rama          # Fusionar con la actual
git branch -d nombre-rama      # Borrar rama (si fue mergeada)
git branch -D nombre-rama      # Forzar borrado
```

### Convenciones de ramas

| Tipo     | Descripción                  | Ejemplo              |
| -------- | ---------------------------- | -------------------- |
| feature/ | Nueva funcionalidad          | feature/login-form   |
| fix/     | Corrección de error          | fix/navbar-overlap   |
| hotfix/  | Urgente en producción        | hotfix/api-timeout   |
| release/ | Preparación de versión final | release/v1.2.0       |
| test/    | Pruebas o validaciones       | test/form-validation |

### Buenas prácticas con ramas

* Nombres descriptivos, minúscula y con guiones
* Trabajar en ramas pequeñas y específicas
* Evitar trabajar en `main`
* Sincronizar frecuentemente (git pull)
* Usar Pull Requests para revisión colaborativa

---

## Repositorios remotos

```bash
git clone url_repo             # Clonar

git remote add origin url      # Enlazar local con remoto
git push -u origin main        # Subir por primera vez
git push                       # Subir cambios
git fetch                      # Traer sin fusionar
git merge                      # Fusionar cambios remotos
git pull                       # fetch + merge
```

> Hacer `git pull` antes de `git push` para evitar conflictos.

---

## Resolución de conflictos

```text
<<<<<<< HEAD
código actual
=======
código entrante
>>>>>>> rama
```

### Pasos:

1. Editar y elegir qué conservar
2. Eliminar marcas
3. Guardar y confirmar:

```bash
git add archivo
git commit -m "Conflicto resuelto"
```

> Cancelar merge:

```bash
git merge --abort
```

---

## Llaves SSH

1. Generar llave:

```bash
ssh-keygen -t rsa -b 4096 -C "tu@email.com"
```

2. Agregar al agente:

```bash
eval $(ssh-agent -s)
ssh-add ~/.ssh/id_rsa
```

3. Copiar clave pública:

```bash
cat ~/.ssh/id_rsa.pub
```

4. Agregarla en GitHub: Settings > SSH keys

> Permite clonar y hacer push sin ingresar contraseña.

---

## Buenas prácticas

* Hacelo atómico: un cambio por commit
* Mensajes claros y descriptivos
* Evitá `git add .` sin revisar
* Usá `.gitignore` desde el inicio
* Hacé commits frecuentes
* Siempre revisar con `git status` y `git log`

---

## Commits convencionales

```
tipo(alcance opcional): mensaje breve
```

### Tipos comunes:

* feat: funcionalidad nueva
* fix: corrección de bug
* docs: documentación
* style: formato (espacios, indentación)
* refactor: mejora sin cambiar funcionalidad
* test: tests agregados o corregidos
* chore: tareas menores

### Ejemplos:

```bash
git commit -m "feat(nav): agregar menú"
git commit -m "fix(login): error en validación"
git commit -m "docs: actualizar README"
```

---

## Commitlint y Husky

### ¿Qué es `commitlint`?

Una herramienta que valida que los mensajes de commit respeten el formato de los [Commits Convencionales](#commits-convencionales).

### ¿Qué es `husky`?

Permite ejecutar scripts automáticos en *ganchos de Git* como `pre-commit` o `commit-msg`. Se usa para activar `commitlint` antes de confirmar.

### Instalación rápida:

```bash
npm install --save-dev husky @commitlint/{config-conventional,cli}
npx husky install
npx husky add .husky/commit-msg "npx --no -- commitlint --edit $1"
```

### Configuración mínima:

Agregar en `package.json`:

```json
"commitlint": {
  "extends": ["@commitlint/config-conventional"]
}
```

> Así evitás commits con mensajes poco claros o que rompen el estándar del equipo.

---

## Recursos útiles

* [Git oficial](https://git-scm.com/doc)
* [Guía Markdown](https://www.markdownguide.org/basic-syntax/)
* [GitHub SSH Keys](https://docs.github.com/es/authentication/connecting-to-github-with-ssh)
* [GitFlow](https://nvie.com/posts/a-successful-git-branching-model/)
* [Conventional Commits](https://www.conventionalcommits.org/es/v1.0.0/)
* [Commitlint](https://commitlint.js.org/)
* [Husky](https://github.com/typicode/husky)


