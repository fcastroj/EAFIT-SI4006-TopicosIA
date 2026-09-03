# Sesión 07 · El modelo no lo sabe todo: RAG ingenuo

**Módulo 3 · Recuperación Aumentada (RAG) y patrones agentic** · Semana 7 · 3 h · Clase grabada

## De qué se trata

El modelo de M1 responde de memoria, y la memoria falla: tiene fecha de corte, no conoce sus datos privados y cuando no sabe, completa con lo más probable (alucina). La solución no es más entrenamiento sino darle una biblioteca: buscar primero, responder después. Se construye el pipeline RAG completo, se practican sus dos oficios técnicos —partir documentos y buscar por significado— y cada equipo monta su primer RAG ingenuo sobre el corpus del proyecto.

## Al terminar la sesión pueden

- Explicar cuándo RAG le gana al fine-tuning (conocimiento nuevo, privado, cambiante, con trazabilidad) y cuándo no.
- Describir las siete etapas del pipeline: ingest → chunk → embed → store · retrieve → augment → generate.
- Elegir y justificar una estrategia de chunking (fixed-size, recursive, semantic, hierarchical) y el tamaño/overlap inicial.
- Usar embeddings y similitud de coseno como motor de búsqueda sobre una base vectorial (Chroma).
- Armar el prompt aumentado en cuatro partes: instrucción, contexto con fuente, válvula de escape, pregunta.

## Agenda

| Bloque | Tema | Tiempo |
|---|---|---|
| 1 | Motivación: knowledge cutoff, datos privados, costos, trazabilidad | 20 min |
| 2 | Pipeline RAG completo | 30 min |
| 3 | Chunking: cuatro estrategias · Lab A | 30 min |
| 4 | Embeddings como buscador y bases vectoriales (Chroma, FAISS, Qdrant) | 40 min |
| 5 | Lab B: primer RAG ingenuo sobre el corpus del proyecto | 50 min |
| 6 | Cierre y tarea: aplicar el harness de M2 al RAG ingenuo | 10 min |

## Contenido de esta carpeta

- Presentación `SI4006_S07_Semana7_Sesion7` (`.pptx` / `.pdf`).
- Notebook `S07_Lab_RAG_ingenuo.ipynb` (Labs A y B: chunking, embeddings + Chroma, prompt aumentado, generación con Qwen2.5-1.5B-Instruct).
- Guía pedagógica slide por slide (`.md`).
- Imágenes de apoyo: mapa cutoff → alucinación, chunking con las cuatro estrategias sobre el mismo texto.

## Antes de la sesión

- Traer el corpus del proyecto: entre 5 y 20 documentos del dominio (PDF, HTML o texto).
- Tener el harness de M2 corriendo: es la tarea de esta semana.
- Correr la celda de instalación del notebook desde el inicio (descarga del generador y del modelo de embeddings).

## Tarea para S08

1. Pasar el RAG ingenuo por el harness de M2 y comparar con el scorecard del baseline.
2. Anotar las **consultas fallidas**: preguntas del eval set donde el retrieval no trajo el chunk correcto. Son el insumo de la sesión 8.

## Lo que viene

S08: los problemas del RAG ingenuo y las técnicas para arreglarlos (hybrid search, reranking, query transformation), cada una justificada con el delta en el harness.

## Referencias

- Lewis et al., *Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks* (2020) — arxiv.org/abs/2005.11401
- Documentación de Chroma — docs.trychroma.com
- Sentence-Transformers — sbert.net
