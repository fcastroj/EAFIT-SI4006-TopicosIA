# Sesión 06 · ¿Quién juzga al juez? LLM-as-a-judge, evaluación humana y el harness

**Módulo 2 · Evaluación rigurosa de sistemas generativos** · Semana 6 · 3 h · Clase grabada · Cierra con la **entrega M2 (10%)**

## De qué se trata

La sesión pasada mostró que ninguna métrica sola alcanza. Hoy se suman dos jueces que sí evalúan calidad —un LLM con rúbrica y la mirada humana—, se estudian los sesgos del juez automático y cómo mitigarlos, y se fabrican casos adversariales. Con esas piezas cada equipo arma el **harness de tres dimensiones** que evaluará su sistema el resto del semestre y produce el scorecard del baseline.

## Al terminar la sesión pueden

- Montar un LLM-as-a-judge con rúbrica explícita (pointwise, pairwise o con referencia) y escala definida.
- Identificar y mitigar los sesgos conocidos del juez: posición, longitud/verbosidad y auto-preferencia.
- Diseñar una evaluación humana con rúbrica y medir acuerdo entre anotadores (Cohen's kappa).
- Generar ejemplos adversariales y de borde para su dominio (red-teaming).
- Ejecutar `harness(eval_set, sistema)` → scorecard con tres dimensiones: métrica clásica, LLM-juez y acierto de dominio.

## Agenda

| Bloque | Tema | Tiempo |
|---|---|---|
| 1 | Recap: medir no basta, hay que juzgar | 10 min |
| 2 | LLM-as-a-judge: rúbricas y setup · Lab A | 40 min |
| 3 | Sesgos del juez y mitigaciones · Lab B (provocar un sesgo) | 35 min |
| 4 | Evaluación humana: rúbricas, anotadores múltiples, inter-rater agreement | 25 min |
| 5 | Datasets sintéticos y adversariales, red-teaming | 25 min |
| 6 | Lab C: armar el harness y el scorecard del baseline | 30 min |
| 7 | Cierre y entrega M2 | 15 min |

## Contenido de esta carpeta

- Presentación de la sesión (`.pptx` / `.pdf`).
- Notebook `S06 · Lab Harness de evaluación` (Labs A, B y C). Al final guarda `scorecard_baseline.csv` y `eval_set.json`.
- Guion de la clase grabada (`.md`).

## Antes de la sesión

- Traer los 10 ejemplos gold de la tarea de S05.
- Tener corriendo el modelo de M1 (o aceptar el generador placeholder del notebook y documentarlo como tal).
- Correr la primera celda del notebook desde el inicio: la descarga del modelo juez tarda varios minutos.

## Entrega M2 (10%, por equipo)

1. **Harness ejecutable**: las tres dimensiones corriendo sobre un eval set de mínimo 10 gold y mínimo 2 adversariales.
2. **Scorecard del baseline** más un párrafo de lectura honesta: dónde falla y por qué. Un baseline honesto vale más que uno inflado.
3. `eval_set.json` y `scorecard_baseline.csv` en el repo del equipo.

## Lo que viene

S07 abre el Módulo 3: el modelo no lo sabe todo. RAG ingenuo sobre el corpus del proyecto, y la tarea será pasarlo por este harness.

## Referencias

- Zheng et al., *Judging LLM-as-a-Judge with MT-Bench and Chatbot Arena* (2023) — arxiv.org/abs/2306.05685
- Liang et al., *HELM* (2022) — crfm.stanford.edu/helm
- `promptfoo` — promptfoo.dev · `garak` — github.com/leondz/garak
