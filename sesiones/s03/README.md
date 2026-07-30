 Sesión 03 · El bloque y las familias

**Módulo:** M1 — Transformers y fine-tuning con Hugging Face · **Duración:** 3 h

Qué hay dentro de un transformer, por qué está armado así, y qué familia de modelos —encoder, decoder o encoder-decoder— le sirve a cada proyecto. Al final de la sesión cada equipo sale con su modelo base candidato elegido y con la razón por la que lo eligió.

## Contenido

- **El bloque completo** — más allá de la atención: conexión residual, layer normalization y red feed-forward. Por qué cada pieza está ahí y qué se rompería sin ella.
- **Por qué el residual importa** — el `x +` que hace posible entrenar en profundidad. Se mide en el Lab A: la norma del gradiente con y sin residual.
- **Las tres familias** — mismo bloque, distinto cableado. Encoder-only (BERT), decoder-only (GPT, Qwen), encoder-decoder (T5). La diferencia es una máscara.
- **Objetivos de pre-entrenamiento** — MLM, CLM y span corruption. Por qué el objetivo con que se entrena un modelo define para qué sirve.
- **Escalado** — leyes empíricas (Chinchilla), por qué más grande no es mejor, y qué tamaño de modelo tiene sentido en Colab.

## Material

- Diapositivas: `SI4006_S03_Semana3_Sesion3.pptx` (en esta carpeta)

## Notebook

Laboratorio de la sesión — tres partes: el bloque armado y roto (residual), las tres familias sobre una misma frase, y cada objetivo de pre-entrenamiento hecho código.

[![Abrir en Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/manularrea/EAFIT-SI4006/blob/main/sesiones/s03/S03_Lab_El_bloque_y_las_familias.ipynb)

## Antes de la sesión

- Haber leído la **sección 3** de *Attention Is All You Need* (tarea de S02).
- Tener a mano el candidato a modelo base que cada equipo trajo de la sesión anterior.
- No se necesita GPU para este laboratorio: corre en CPU.

## Después de la sesión

- Abrir la **tarjeta del modelo base** elegido en el Hub y leerla completa: licencia, idiomas, con qué datos se entrenó y sus limitaciones conocidas. Se cita en la entrega M1.
- Cada equipo llega a la **Sesión 4** con **20 ejemplos reales de su dominio** (pares entrada→salida). En S04 empieza el fine-tuning y sin datos no hay nada que entrenar.

## Referencias

- Vaswani et al. (2017), *Attention Is All You Need* — [arxiv.org/abs/1706.03762](https://arxiv.org/abs/1706.03762)
- Hoffmann et al. (2022), *Training Compute-Optimal Large Language Models* (Chinchilla) — [arxiv.org/abs/2203.15556](https://arxiv.org/abs/2203.15556)
- Devlin et al. (2018), *BERT: Pre-training of Deep Bidirectional Transformers* — [arxiv.org/abs/1810.04805](https://arxiv.org/abs/1810.04805)
- Raffel et al. (2019), *Exploring the Limits of Transfer Learning with a Unified Text-to-Text Transformer* (T5) — [arxiv.org/abs/1910.10683](https://arxiv.org/abs/1910.10683)
- Hugging Face — *The Model Hub* — [huggingface.co/models](https://huggingface.co/models)
