# Cómo contribuir

Este repositorio es **material de un curso**, no un proyecto de software que se
desarrolle de forma colaborativa. La forma más útil de contribuir es ayudar a
mantener el material correcto: reportar erratas, enlaces rotos o notebooks que
no corren.

## Reportar un error en el material

1. Revisa los [issues abiertos](../../issues) por si alguien ya lo reportó.
2. Abre un issue con la plantilla **Error en el material**.
3. Indica la sesión, el archivo y —si aplica— la celda y el mensaje de error.

## Proponer una corrección

Si quieres corregir tú mismo una errata o un enlace:

1. Haz un fork del repositorio.
2. Crea una rama descriptiva (`fix/enlace-s03`, `fix/errata-readme`).
3. Haz el cambio y, si tocaste código o notebooks, corre `pre-commit run --all-files`.
4. Abre un pull request explicando qué corriges y por qué.

Cambios de contenido académico (objetivos, temario, evaluación) los define la
docente; propón la idea en un issue antes de abrir un PR.

## Qué NO subir

- **Datos personales** —tuyos o de terceros— en notebooks, issues o PRs.
- **Credenciales o tokens** (Hugging Face, W&B, APIs). Si expones uno por error,
  revócalo de inmediato.
- **Datasets con licencia restrictiva** o que no puedas redistribuir.
- **Pesos de modelos** u otros archivos grandes: el límite del repo es 5 MB por
  archivo (ver `.pre-commit-config.yaml`).

## Estilo

- Código Python: `ruff` (lint + format), configurado en pre-commit.
- Notebooks: se limpian los outputs con `nbstripout` en cada commit.
