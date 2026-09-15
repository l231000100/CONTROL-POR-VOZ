# Terminal — Subir la práctica a GitHub 💻

Guía rápida de los comandos que se usan en la terminal para subir la carpeta `Practicas` a GitHub.

**Autores:** Iván Luna, Daniel Bustamante

---

## 1. Verifica que tengas Git instalado

```bash
git --version
```

Si no aparece un número de versión, descarga Git desde [git-scm.com](https://git-scm.com) e instálalo primero.

---

## 2. Configura tu identidad (solo la primera vez)

```bash
git config --global user.name "Tu Nombre"
git config --global user.email "tu_correo@ejemplo.com"
```

---

## 3. Ve a la carpeta de tu proyecto

```bash
cd ruta/a/tu/carpeta/Practicas
```

---

## 4. Convierte la carpeta en un repositorio Git

```bash
git init
```

---

## 5. Agrega y guarda tus archivos (commit)

```bash
git add .
git commit -m "Practica: control de robot por voz"
```

---

## 6. Crea el repositorio en GitHub

1. Entra a [github.com](https://github.com) y da clic en **New repository**.
2. Ponle nombre (ej. `control-por-voz`).
3. Déjalo **público** si quieres compartir el link después.
4. NO marques "Add a README" (ya tienes uno) — copia la URL que te da GitHub, algo como:
   `https://github.com/tu-usuario/control-por-voz.git`

---

## 7. Conecta tu carpeta local con GitHub y sube los archivos

```bash
git remote add origin https://github.com/tu-usuario/control-por-voz.git
git branch -M main
git push -u origin main
```

Te va a pedir tu usuario y contraseña (o un token de acceso personal si GitHub ya no acepta contraseña directa).

---

## 8. Para subir cambios futuros

Cada vez que modifiques algo, solo repite:

```bash
git add .
git commit -m "Descripción breve del cambio"
git push
```

---

## 🐞 Problemas comunes

| Error | Solución |
|---|---|
| `git: command not found` | Instala Git desde git-scm.com |
| Pide usuario/contraseña y falla | GitHub ya no acepta contraseña normal; genera un **Personal Access Token** en Settings > Developer settings > Personal access tokens, y úsalo como contraseña |
| `fatal: remote origin already exists` | Usa `git remote set-url origin <URL>` en vez de `git remote add` |
| `rejected... fetch first` | Corre `git pull origin main --allow-unrelated-histories` antes de volver a hacer push |
