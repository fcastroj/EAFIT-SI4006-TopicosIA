# Setup en Google Colab

Colab es la ruta principal del curso: no necesitas instalar nada en tu máquina.
Cada notebook trae un badge **Abrir en Colab** que lo abre listo para correr.

## Los tres pasos

1. **Abre el notebook** desde el badge de la sesión (o desde la tabla del
   [README](../README.md)).
2. **Activa la GPU:** menú `Entorno de ejecución` → `Cambiar tipo de entorno de
   ejecución` → acelerador por hardware **GPU (T4)** → `Guardar`.
3. **Corre la celda de instalación primero** (la del bloque *Setup*) y una sola
   vez. Si Colab muestra el botón **RESTART RUNTIME**, haz clic y vuelve a
   ejecutar desde esa celda hacia abajo.

## Verifica que la GPU está activa

La primera celda de código de los notebooks imprime el dispositivo. Debe decir
`Device: cuda` y el nombre de la GPU (`Tesla T4`). Si dice `cpu`, no activaste
la GPU en el paso 2.

## Notas

- La GPU gratuita de Colab (T4) es suficiente para todo el material del curso.
- Las versiones de las dependencias están fijadas a propósito (ver
  [`requirements.txt`](../requirements.txt)). No instales `transformers` en otra
  celda ni cambies su versión: rompe el resto del notebook.
- Colab desconecta las sesiones inactivas. Si vuelves después de un rato, corre
  de nuevo desde la celda de instalación.

## Cuentas que vas a necesitar

- **Google** — para usar Colab.
- **Hugging Face** — para descargar modelos y, más adelante, publicar tu demo en
  Spaces. Créala en <https://huggingface.co/join>.
