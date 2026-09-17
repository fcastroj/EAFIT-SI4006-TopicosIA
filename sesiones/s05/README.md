# Sesión 05 · Métricas, perplexity y benchmarks: por qué evaluar LLMs es difícil

**Módulo 2 · Evaluación rigurosa de sistemas generativos** · Semana 5 · 3 h

## De qué se trata

En M1 la curva de training loss bajó. Eso responde "¿entrenó?", no "¿es bueno?". Esta sesión desarma las herramientas con las que se suele responder esa pregunta —métricas de n-gramas, embeddings, perplexity y benchmarks públicos— y muestra dónde falla cada una. La conclusión es la motivación de S06: ninguna medida sola alcanza; hay que combinar miradas con fallos no correlacionados.

## Al terminar la sesión pueden

- Calcular e interpretar BLEU (precisión), ROUGE (recall), METEOR (sinónimos y raíces) y BERTScore (significado), y decir qué modo de fallo tiene cada una.
- Explicar perplexity como exp(cross-entropy), su relación con el training loss de M1 y por qué mide fluidez y no verdad.
- Leer un número de benchmark (MMLU, GSM8K, MT-Bench, HELM, BIG-bench) con tres preguntas: qué hay dentro, qué regla lo puntúa y si mide su problema.
- Reconocer contaminación de benchmarks y leer un leaderboard con criterio.
- Escribir un ejemplo gold de su dominio: input, respuesta esperada y criterio.

## Agenda

| Bloque | Tema | Tiempo |
|---|---|---|
| 1 | Recap y motivación: por qué evaluar LLMs es difícil | 20 min |
| 2 | Métricas clásicas: BLEU, ROUGE, METEOR, BERTScore y dónde fallan (Lab A) | 40 min |
| 3 | Perplexity y cross-entropy como métricas intrínsecas | 25 min |
| 4 | Benchmarks modernos: qué miden y qué no | 45 min |
| 5 | Contaminación y lectura crítica de leaderboards | 20 min |
| 6 | Hacia su harness: tres dimensiones · tarea | 30 min |

## Contenido de esta carpeta

- Presentación de la sesión (`.pptx` / `.pdf`).
- Notebook del lab de métricas (BLEU/ROUGE/BERTScore/perplexity sobre ejemplos del dominio).
- Guía teórica y pedagógica slide por slide (`.md`).

## Antes de la sesión

- Tener a mano el scorecard informal de M1: qué respuestas del modelo les parecieron buenas y cuáles no.
- Correr la celda de instalación del notebook (descarga del modelo de embeddings).

## Tarea para S06

Recopilar **10 ejemplos gold** del dominio del proyecto, cada uno con input, respuesta esperada y criterio de "buena respuesta". Son la semilla del eval set y la vara fija del semestre: con estos mismos ejemplos se evaluará el baseline (M2), el RAG (M3), la visión (M4) y la producción (M5).

## Lo que viene

S06: LLM-as-a-judge, sus sesgos, evaluación humana, casos adversariales y la construcción del harness. Cierra con la entrega M2.

## Referencias

- Liang et al., *Holistic Evaluation of Language Models (HELM)* (2022) — crfm.stanford.edu/helm
- Chang et al., *A Survey on Evaluation of Large Language Models* (2024) — arxiv.org/abs/2307.03109
- Papineni et al., *BLEU* (2002) · Lin, *ROUGE* (2004) · Zhang et al., *BERTScore* (2019) — arxiv.org/abs/1904.09675
- `lm-evaluation-harness` — github.com/EleutherAI/lm-evaluation-harness
