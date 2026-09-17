# Sesión 04 · Fine-tuning eficiente con Hugging Face y LoRA

**Módulo 1 · Arquitectura transformer y fine-tuning eficiente** · Semana 4 · 3 h · Cierra con la **entrega M1 (10%)**

## De qué se trata

Última sesión del Módulo 1. Ya conocen la arquitectura y las familias de modelos; hoy adaptan un modelo base a su dominio. Se recorre el ecosistema Hugging Face, el fine-tuning supervisado con la Trainer API y la adaptación de bajo rango (LoRA / QLoRA), y en el lab cada equipo entrena su baseline sobre el dataset del proyecto.

## Al terminar la sesión pueden

- Ubicar y usar las piezas del ecosistema Hugging Face: `transformers`, `datasets`, `accelerate`, `peft`, `evaluate` y el Hub.
- Ejecutar un fine-tuning supervisado con `Trainer`, con evaluación durante el entrenamiento y seguimiento en TensorBoard o W&B.
- Explicar qué hace LoRA (ΔW = B·A, con rango r ≪ d), qué controlan `r`, `alpha` y `target_modules`, y cuándo conviene QLoRA.
- Reportar un baseline fine-tuneado con métricas comparadas contra el modelo sin adaptar.

## Agenda

| Bloque | Tema | Tiempo |
|---|---|---|
| 1 | Tour del ecosistema Hugging Face | 30 min |
| 2 | Fine-tuning supervisado con Trainer API, evaluación y tracking | 40 min |
| 3 | LoRA y QLoRA: intuición, hiperparámetros, cuándo usar cada uno | 30 min |
| 4 | Lab: fine-tuning del modelo base sobre el dataset del proyecto (Colab) | 60 min |
| 5 | Cierre y entrega M1 | 20 min |

## Contenido de esta carpeta

- Presentación de la sesión (`.pptx` / `.pdf`).
- Notebook del lab de fine-tuning con LoRA (Colab, GPU T4).
- Plantilla de reporte de la entrega M1.

## Antes de la sesión

- Tener el dataset del proyecto en formato `datasets` (train / validation) y el modelo base candidato decidido en S03.
- Cuenta en Hugging Face y token de acceso configurado en Colab.
- Correr la celda de instalación del notebook antes de empezar: la descarga del modelo base tarda.

## Entrega M1 (10%, por equipo)

1. Modelo fine-tuneado con LoRA sobre el dataset del dominio (adaptador publicado en el Hub o guardado en el repo).
2. Descripción del dataset: origen, tamaño, splits, ejemplo representativo.
3. Métricas del baseline con comparación contra el modelo sin fine-tuning, y la curva de training loss.

## Lo que viene

S05 abre el Módulo 2 con una pregunta incómoda: la curva bajó, ¿pero el modelo es bueno? Tarea previa: ninguna aparte de la entrega.

## Referencias

- Hu et al., *LoRA: Low-Rank Adaptation of Large Language Models* (2022) — arxiv.org/abs/2106.09685
- Dettmers et al., *QLoRA: Efficient Finetuning of Quantized LLMs* (2023) — arxiv.org/abs/2305.14314
- Hugging Face NLP Course, capítulo de fine-tuning — huggingface.co/learn/nlp-course
- Documentación de `peft` — huggingface.co/docs/peft
