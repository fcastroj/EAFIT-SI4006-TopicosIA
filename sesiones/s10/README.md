# Sesión 10 · RAG agéntico y evaluación con RAGAS

**Módulo:** M3 — RAG, agentes, tool use, RAGAS · **Duración:** 3 h · **Fecha:** jue 17 SEP · Cierra el módulo con la **entrega M3 (15%, dom 27 SEP)**

## Contenido

Ya tenemos un RAG que recupera bien (S08). Hoy hacemos dos cosas encima: le damos herramientas para actuar cuando la pregunta lo pide, y aprendemos a evaluarlo por dentro, mirando el contexto recuperado y no solo la respuesta.

| Bloque | Tema | Lab |
|---|---|---|
| 1 | Recap: dónde estamos en el semestre y el bucle agentic (percibir → razonar → actuar) | — |
| 2 | Tool use y function calling: esquema de una herramienta, el modelo propone y nosotros ejecutamos, validar el JSON | Lab A |
| 3 | ReAct: pensamiento → acción → observación; el retrieval como herramienta; cuándo un agente ayuda y cuándo estorba | Lab B |
| 4 | RAGAS: faithfulness, context precision, context recall, answer relevancy; por qué complementa al harness | Lab C |
| 5 | Guardar corridas con Weights & Biases (opcional) | Extra |
| 6 | Cierre del módulo: el sistema completo y la entrega M3 | — |
| 7 | Profundización: memoria conversacional · optimización de prompts con DSPy | Extra |

Al terminar la sesión pueden:

- Describir una herramienta con un esquema y montar el bucle propone → ejecuta → observa → responde.
- Implementar un mini-agente ReAct y decidir, con el harness, si el agente se justifica frente al RAG de una pasada.
- Calcular e interpretar las cuatro métricas de RAGAS y usarlas como diagnóstico: retrieval (precision/recall) vs. generación (faithfulness/relevancy).

## Material

- Diapositivas: `SI4006_S10_Semana10_Sesion10.pptx` (32 slides + mapa del semestre después de la slide 4).
- Guion de la clase grabada: `SI4006_S10_Guion_Clase_Grabada.md`.
- Imagen: `mapa_semestre_s10.png` (dónde estamos, qué falta).

## Notebook

- **Lab principal:** `S10_Lab_Agentic_RAG_RAGAS.ipynb` — Labs A (function calling), B (ReAct) y C (RAGAS a mano). TODO A: despachador de herramientas · TODO B: un paso ReAct · TODO C: faithfulness.
  [![Abrir en Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/<ORG>/<REPO>/blob/main/sesiones/s10/S10_Lab_Agentic_RAG_RAGAS.ipynb)
- Versión resuelta: `S10_Lab_Agentic_RAG_RAGAS_RESUELTO.ipynb`.
- Extras (opcionales): `S10_Extra_WandB.ipynb` (seguimiento de corridas, offline) · `S10_Extra_DSPy.ipynb` (optimización de prompts con modelo local vía Ollama).

Modelos: `Qwen/Qwen2.5-1.5B-Instruct` (generador y juez), `paraphrase-multilingual-MiniLM-L12-v2` (embeddings), Chroma. Corre en Colab con T4; en CPU va lento porque el generador se llama muchas veces.

## Antes de la sesión

- Traer el sistema de la S08 (retriever avanzado) y su `eval_set`: el notebook levanta un RAG compacto para correr solo, pero donde diga pueden pegar el suyo.
- Tener el harness de M2 corriendo: la entrega pide el scorecard propio junto a RAGAS.
- Correr la celda de instalación del notebook desde el inicio (descarga del generador).

## Entrega M3 (15%, por equipo · cierra dom 27 SEP 23:59)

1. Sistema RAG completo con al menos dos técnicas avanzadas (S08) y al menos una herramienta (tool).
2. Reporte de evaluación: scorecard del harness propio + las cuatro métricas de RAGAS.
3. Lectura honesta: qué técnica movió qué, qué costó en latencia y qué falla queda pendiente.

## Referencias

- Yao et al., *ReAct: Synergizing Reasoning and Acting in Language Models* (ICLR 2023) — arxiv.org/abs/2210.03629
- Es et al., *RAGAS: Automated Evaluation of Retrieval Augmented Generation* (EACL 2024) — arxiv.org/abs/2309.15217
- Schick et al., *Toolformer: Language Models Can Teach Themselves to Use Tools* (2023) — arxiv.org/abs/2302.04761
- Khattab et al., *DSPy: Compiling Declarative Language Model Calls into Self-Improving Pipelines* (2023) — arxiv.org/abs/2310.03714
- Documentación: `ragas` (docs.ragas.io) · Weights & Biases (docs.wandb.ai) · DSPy (dspy.ai)
