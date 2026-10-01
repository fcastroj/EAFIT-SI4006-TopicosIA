# Sesión 11 · El transformer aprende a ver: ViT, CLIP y modelos multimodales

**Módulo:** M4 — ViT, CLIP, multimodales, difusión · **Duración:** 3 h · **Fecha:** jue 24 SEP · Clase grabada

## Contenido

Cerramos el RAG (M3 cierra dom 27 SEP) y abrimos la Unidad 4. El mismo transformer de S03 entra a las imágenes: parches en vez de palabras (ViT), texto e imagen en un solo espacio vectorial (CLIP) y un LLM que mira (LLaVA y familia). La sesión termina con la pregunta del proyecto: qué componente visual, con qué patrón y cómo se mide.

| Bloque | Tema | Lab |
|---|---|---|
| 1 | Recap: dudas del formulario (RAGAS y faithfulness · RAG vs. tools vs. agente · DSPy y MCP · el tweet del cierre) + mapa del semestre | — |
| 2 | Vision Transformer: parches como tokens, el encoder no cambia, ViT vs. CNN | — |
| 3 | CLIP: contrastive learning, zero-shot con prompts, búsqueda de imágenes con texto | Lab A |
| 4 | Modelos multimodales: la receta encoder visual → proyector → LLM; cómo preguntarle; dónde alucina | Lab B |
| 5 | Patrones de integración visual (input / tool / output), ideas por dominio, cómo se mide con el harness | — |
| 6 | Declaración del plan visual (tarea) · hacia S12 (difusión) y M4 (S13) | — |

Al terminar la sesión pueden:

- Explicar qué cambia y qué no entre BERT y ViT (tokenizador, embedding, posición; encoder igual).
- Clasificar imágenes sin entrenar con CLIP escribiendo las clases como texto, y medir el efecto del prompt.
- Usar un modelo multimodal pequeño para describir, responder y extraer JSON de una imagen, con válvula de escape y caso trampa.
- Elegir y justificar un patrón de integración visual para su proyecto y decir cómo entra al harness.

## Material

- Diapositivas: `SI4006_S11_Semana11_Sesion11.pptx` (31 slides).
- Infografías incluidas en el deck (también sueltas): RAGAS en una imagen · RAG/tools/agente · DSPy y MCP · el tweet del cierre anotado con lo aprendido y lo que viene · mapa del semestre S11 · ViT · CLIP · receta multimodal.

## Notebook

- **Lab principal:** `S11_Lab_Vision.ipynb` — Lab A (CLIP zero-shot, prompt como hiperparámetro, búsqueda imagen-texto) y Lab B (visual QA con Qwen2-VL-2B; LLaVA-1.5-7B en 4 bits como celda opcional). TODO A1: matriz de cosenos · A2: comparar formulaciones de prompt · B3: parsear JSON · B4: pregunta trampa.
  [![Abrir en Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/manularrea/EAFIT-SI4006/blob/main/sesiones/s11/S11_Lab_Vision.ipynb)
- Versión resuelta: `S11_Lab_Vision_RESUELTO.ipynb`.

Modelos: `openai/clip-vit-base-patch32`, `Qwen/Qwen2-VL-2B-Instruct` (opcional `llava-hf/llava-1.5-7b-hf` en 4 bits). GPU T4 en Colab; en CPU el Lab B es lento.

## Antes de la sesión

- Traer 3–6 imágenes del dominio del proyecto (fotos de producto, hojas, documentos escaneados, mascotas…). El notebook trae imágenes de ejemplo, pero el lab vale más con las suyas.
- Tener presente el eval set de M2: los casos con imagen de M4 se agregan ahí.
- Correr la celda de instalación desde el inicio (descarga del modelo multimodal).

## Tarea para S12 · declaración del plan visual

1. La pregunta de su usuario que necesita ver una imagen (o la justificación de que no hay ninguna).
2. Patrón (input / tool / output) y modelo (CLIP, ViT fine-tuneado, VLM o difusión).
3. Al menos 5 casos con imagen para el eval set y qué dimensión del harness los califica.

Es el borrador de la **entrega M4** (S13 · 15 OCT · cierra dom 25 OCT · 10%): pipeline multimodal + casos de prueba.

## Referencias

- Dosovitskiy et al., *An Image is Worth 16×16 Words: Transformers for Image Recognition at Scale* (ICLR 2021) — arxiv.org/abs/2010.11929
- Radford et al., *Learning Transferable Visual Models from Natural Language Supervision* (CLIP, ICML 2021) — arxiv.org/abs/2103.00020
- Liu et al., *Visual Instruction Tuning* (LLaVA, NeurIPS 2023) — arxiv.org/abs/2304.08485
- Li et al., *BLIP-2* (2023) — arxiv.org/abs/2301.12597 · Wang et al., *Qwen2-VL* (2024) — arxiv.org/abs/2409.12191
- Profundización: SAM (arxiv.org/abs/2304.02643) · DINOv2 (arxiv.org/abs/2304.07193) · ColPali (arxiv.org/abs/2407.01449)
