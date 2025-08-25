# Template LaTeX — Manual (Overleaf-friendly)

Este repositorio es una plantilla modular LaTeX para un manual (documentclass `report`). Está pensada para poder usarse en Overleaf sin cambios, pero también admite activar `minted` localmente.

## Estructura

- `main.tex` — archivo principal. Carga `preamble.tex`, `titlepage.tex` y los capítulos en `chapters/`.
- `preamble.tex` — preámbulo con paquetes y macros de plantilla. Tiene una opción para usar `minted` o un fallback con `listings` (más abajo explico cómo cambiarlo).
- `titlepage.tex` — portada que usa macros de plantilla (`\docTitle`, `\docVersion`, `\docAuthor`).
- `chapters/` — capítulos modulares.

## Uso en Overleaf (recomendado)

Overleaf normalmente no permite `-shell-escape` por defecto, por lo que el paquete `minted` (que requiere ejecución de Pygments via shell) no funcionará a menos que actives explícitamente esa opción en un proyecto privado con soporte. Para facilitar usar la plantilla en Overleaf, `minted` está desactivado por defecto y la plantilla usa un fallback basado en `listings`.

Pasos para abrir en Overleaf:
1. Sube todo el contenido del repositorio a un nuevo proyecto en Overleaf.
2. Compila normalmente (Overleaf selecciona `pdflatex`/`xelatex` automáticamente según tu configuración). Debería compilar sin requerir `-shell-escape`.

Si quieres usar `minted` en Overleaf (no siempre disponible):
- Overleaf Teams/Private projects pueden permitir `-shell-escape` en algunas configuraciones; revisa la documentación de Overleaf y la configuración del proyecto.

## Uso local (Windows, cmd.exe)

Recomendación básica para compilar localmente con `minted` desactivado (funciona siempre):

```bat
REM Compilar con pdfLaTeX (sin minted)
pdflatex -interaction=nonstopmode main.tex
bibtex main  REM si usas bibliografía
pdflatex -interaction=nonstopmode main.tex
pdflatex -interaction=nonstopmode main.tex
```

Si quieres usar `minted` localmente, asegúrate de tener Python y Pygments instalados y compila con `-shell-escape`:

```bat
REM Compilar con minted (requiere Python + Pygments y que TeX permita shell-escape)
pdflatex -shell-escape -interaction=nonstopmode main.tex
bibtex main
pdflatex -shell-escape -interaction=nonstopmode main.tex
pdflatex -shell-escape -interaction=nonstopmode main.tex
```

También puedes usar `latexmk` si lo tienes instalado:

```bat
latexmk -pdf -pdflatex="pdflatex -shell-escape -interaction=nonstopmode" main.tex
```

## Activar minted en el proyecto (opcional)

- En `preamble.tex` hay una bandera al principio del bloque de código:

```tex
\newif\ifuseminted
\usemintedfalse % cambiar a \usemintedtrue si se desea usar minted (requiere -shell-escape)
```

Cámbiala a `\usemintedtrue` para activar `minted`. Recuerda que en Overleaf eso puede no estar permitido.

## Logo opcional

Coloca un archivo `logo.pdf` o `logo.jpg` en la raíz del proyecto para que aparezca en la portada.

## Notas finales

- Esta rama sólo ha normalizado la plantilla y añadido instrucciones para Overleaf; no se ha verificado exhaustivamente la compilación en todos los entornos.
- Si quieres, puedo:
  - Forzar `
  - Añadir un archivo `.latexmkrc` para facilitar compilación local.
  - Generar un ejemplo mínimo de capítulo con encabezados y etiquetas.

---

Si quieres que active `minted` por defecto o que añada un `.latexmkrc` o `README` en español más detallado, dime cuál prefieres y lo agrego.
