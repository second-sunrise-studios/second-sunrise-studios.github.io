# Second Sunrise Studios — Landing

Esta es la web de Second Sunrise Studios. Es una sola página HTML que vive en GitHub
y se publica automáticamente cuando se le hace `push`.

**URL en vivo:** https://tomaspeirotti.github.io/second-sunrise-studios/

---

## Cómo pedir cambios

1. Abrí tu agente de IA (Antigravity, Claude Code, Cursor, etc.) en esta carpeta.
2. Decile en lenguaje natural qué querés cambiar. Ejemplos:
   - _"Cambiá el precio del plan anual a $59"_
   - _"Agregá un nuevo curso llamado 'Animación 2D' después de Level Design"_
   - _"En la sección Por qué nosotros, cambiá el texto del cuarto bloque"_
3. El agente edita `index.html`, hace `commit` y `push`. En ~30 segundos los cambios
   salen en la URL en vivo.

> Si algo se rompe, pedile al agente: _"revertí el último cambio"_ — vuelve al estado
> anterior al instante.

---

## Setup inicial (solo se hace una vez en cada computadora)

Necesitás **dos cosas**: GitHub CLI (para que el agente publique los cambios) y un editor con agente de IA.

### 1. Instalar GitHub CLI (`gh`)

GitHub CLI es una herramienta de línea de comandos que el agente usa para subir cambios a GitHub.

**En Mac (más común)**:

```sh
# Si no tenés Homebrew, instalalo primero desde https://brew.sh
brew install gh
```

**En Windows**:

Descargá el instalador de [cli.github.com](https://cli.github.com/) y seguí los pasos.
Alternativa con winget:

```sh
winget install --id GitHub.cli
```

**En Linux** (Debian/Ubuntu):

```sh
sudo apt install gh
```

Para otros sistemas: [instrucciones oficiales](https://github.com/cli/cli#installation).

### 2. Iniciar sesión en GitHub

Una vez instalado, en la terminal corré:

```sh
gh auth login
```

Te va a hacer una serie de preguntas. **Respondé así**:

| Pregunta | Respuesta |
|---|---|
| Where do you use GitHub? | **GitHub.com** |
| Preferred protocol for Git operations? | **SSH** (recomendado) o **HTTPS** si SSH te pide cosas raras |
| Generate a new SSH key? | **Yes** (si elegiste SSH) |
| How would you like to authenticate? | **Login with a web browser** |

Vas a ver un código de 8 caracteres tipo `XXXX-XXXX`. Copialo, apretá Enter, se va a abrir
el navegador, pegás el código, hacés "Authorize" y listo.

Para verificar que funcionó:

```sh
gh auth status
```

Debería decir: `✓ Logged in to github.com account <tu-usuario>`.

### 3. Clonar este repositorio

```sh
gh repo clone tomaspeirotti/second-sunrise-studios
cd second-sunrise-studios
```

Eso te baja una copia de la web en tu computadora.

### 4. Abrir el proyecto con tu agente de IA

- **Antigravity / Cursor / VS Code**: abrí la carpeta `second-sunrise-studios` desde
  el menú `File → Open Folder`.
- **Claude Code**: abrí una terminal en la carpeta y corré `claude`.

El agente automáticamente lee el archivo `AGENTS.md` y entiende cómo modificar y
publicar la web. Ya podés pedirle cambios.

---

## Cómo ver la web localmente (antes de publicar)

Si querés previsualizar los cambios antes de que salgan en vivo, abrí
`index.html` directamente con doble click — debería abrirse en el navegador.

Si necesitás un servidor local (por temas de carga de fuentes/imágenes):

```sh
python3 -m http.server 8000
```

Y abrís `http://localhost:8000` en el navegador.

---

## Estructura del proyecto

```
.
├── index.html        # Toda la web está acá
├── assets/           # Imágenes y fuentes que usa la web
├── reference/        # Material de origen (no se publica)
├── AGENTS.md         # Instrucciones para los agentes de IA
├── README.md         # Este archivo
└── .gitignore
```

La carpeta `reference/` contiene archivos pesados (prototipos, logos en alta resolución,
fuentes vectoriales). Vive solo localmente — **no se sube a GitHub** ni se publica.
Si cambiás de computadora, asegurate de hacer un respaldo aparte (Drive, Dropbox, etc.).

---

## Comandos útiles del día a día

```sh
# Ver el estado actual del repo
git status

# Ver los últimos cambios
git log --oneline -10

# Revertir el último commit (deshace los últimos cambios publicados)
git revert HEAD
git push

# Abrir la web en vivo desde la terminal
gh browse

# Ver el repo en github.com
gh repo view --web
```

---

## Hosting & deploy

- **Hosting**: GitHub Pages (gratis, incluido con GitHub).
- **Deploy**: automático en cada `push` a `main`. Tarda ~30 segundos.
- **SSL**: GitHub lo provee automáticamente.
- **Sin staging/preview**: cada `push` va directo a producción. Si algo se rompe,
  `git revert HEAD && git push` lo arregla en segundos.
