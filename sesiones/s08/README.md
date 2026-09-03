# Sesión 08 · Su RAG puede buscar mejor: hybrid search, reranking y query transformation

**Módulo 3 · Recuperación Aumentada (RAG) y patrones agentic** · Semana 8 · 3 h · Clase grabada

## De qué se trata

La semana pasada montaron el RAG ingenuo y anotaron dónde falla su búsqueda. Hoy se diagnostica cada fallo y se le asigna su técnica: términos exactos que el denso difumina → hybrid search; ruido en el top-k → reranking; la pregunta es el problema → query transformation. Ninguna entra al sistema por moda: cada una se gana su lugar con el delta medido en el harness. La sesión abre con un recap que resuelve las dudas del formulario de salida y reubica a los equipos en el mapa del semestre.

## Al terminar la sesión pueden

- Explicar BM25 y por qué complementa (no reemplaza) a la búsqueda densa: fallos no correlacionados.
- Fusionar rankings con Reciprocal Rank Fusion, RRF = Σ 1/(k + puesto), y explicar por qué fusiona puestos y no puntajes.
- Distinguir bi-encoder de cross-encoder y aplicar el patrón embudo: retrieve top-30 barato → rerank → top-5 al prompt.
- Elegir la transformación de consulta adecuada: multi-query (coloquial), HyDE (estilo pregunta ≠ estilo corpus), step-back (hiperespecífica), decomposition (compuesta).
- Reportar un experimento controlado A / B / C con tabla de deltas y latencia por consulta.

## Agenda

| Bloque | Tema | Tiempo |
|---|---|---|
| 1 | Recap: dudas del formulario de salida · el harness · el mapa del semestre | 25 min |
| 2 | Los problemas del RAG ingenuo: síntoma → técnica | 15 min |
| 3 | Hybrid search: BM25 + denso, fusión con RRF | 35 min |
| 4 | Reranking con cross-encoders: el embudo | 30 min |
| 5 | Query transformation: multi-query, HyDE, step-back, decomposition | 35 min |
| 6 | Lab: ingenuo vs. híbrido vs. híbrido + reranker, medir el delta | 35 min |
| 7 | Lectura de la tabla de deltas · costo/latencia · hacia S09 | 15 min |

## Contenido de esta carpeta

- Presentación `SI4006_S08_Semana8_Sesion8` (`.pptx` / `.pdf`).
- Notebook `S08_Lab_RAG_avanzado.ipynb`: BM25 (`rank_bm25`) + RRF, cross-encoder `mmarco-mMiniLMv2`, multi-query opcional, harness × 3 y tabla de deltas.
- Guion de la clase grabada (`.md`).
- Infografías de apoyo: métricas y embeddings, benchmarks, los dos mundos del RAG, las perillas del RAG, qué es el harness, mapa del semestre, denso vs. BM25, RRF con dos jurados.

## Antes de la sesión

- Tener el RAG ingenuo de S07 corriendo y su scorecard con el harness de M2.
- Traer las consultas fallidas anotadas en S07: se prueban contra el sistema C al final del lab.
- Correr la celda de instalación del notebook desde el inicio (descarga del cross-encoder).

## Para S09

1. **Parcial** (15%, individual, 45 min, sin computador): cubre M1, M2 y RAG inicial. Hacer el taller de la carpeta `nivelacion/` a conciencia.
2. **Checkpoint público** (5 min por equipo): scorecard del baseline, delta del RAG con las técnicas de hoy y el problema más duro que tienen abierto.
3. Subir al repo la **tabla de deltas** del lab: insumo directo de la entrega M3 (S10).

## Lo que viene

S09: parcial y checkpoint. S10: tool use y patrones agentic, evaluación con RAGAS y entrega M3 (15%), que exige al menos dos técnicas avanzadas justificadas con su delta.

## Referencias

- Cormack, Clarke & Buettcher, *Reciprocal Rank Fusion outperforms Condorcet and individual rank learning methods* (2009)
- Gao et al., *Precise Zero-Shot Dense Retrieval without Relevance Labels (HyDE)* (2022) — arxiv.org/abs/2212.10496
- Zheng et al., *Take a Step Back* (2023) — arxiv.org/abs/2310.06117
- `bge-reranker` — huggingface.co/BAAI · `rank_bm25` — github.com/dorianbrown/rank_bm25
