# Sesión 15 · Una URL que funciona: cuantizar, servir, desplegar y observar

**Módulo:** M5 — Eficiencia, despliegue y compresión · **Duración:** 3 h · **Fecha:** jue 29 OCT · Clase grabada · Última sesión de contenido

## Contenido

Cierra el Módulo 5 y el contenido del curso. El sistema sale del notebook: se cuantiza (los mismos pesos con menos bits, sin reentrenar), se sirve (cargar una vez, atender muchas), se despliega en Hugging Face Spaces con una URL pública, y se instrumenta con health check, logging estructurado y observabilidad en W&B. Todo lo que la rúbrica llama "producción verificable". Termina con una despedida construida con los datos del propio formulario de salida del semestre.

| Bloque | Tema | Lab |
|---|---|---|
| 0 | Recap: dudas del formulario (por qué ChatGPT responde tan rápido · cómo se usa e integra un modelo en una empresa · la temperatura y tres dudas sobre el profesor · costos, reglas de M5 y buenas prácticas DevOps/Cloud) | — |
| 1 | Cuantizar: fp32 → fp16 → int8 → int4; bitsandbytes, GPTQ/AWQ, GGUF; el trade-off y cómo se combina con destilar; demo en vivo fp16 vs. int4 | — |
| 2 | Servir: Gradio, FastAPI, vLLM, llama.cpp; p50/p95 y tokens por segundo | — |
| 3 | Desplegar: app.py → requirements → Space → health check + logging JSON | Lab |
| 4 | Observar: W&B en producción, las cuatro gráficas, drift · lo que falta para el demo day · profundización (speculative decoding, canary, guardrails) · el curso en una frase por parada · despedida | — |

Al terminar la sesión pueden:

- Cuantizar un generador a int4 con una línea y medir memoria, latencia p50/p95 y calidad con temperatura 0 y semilla fija.
- Explicar por qué un modelo servido responde en segundos (carga única, batching, KV cache, streaming, réplicas).
- Escribir un `app.py` con Gradio sobre su sistema, con pestaña de estado y una línea JSON de log por petición.
- Desplegarlo en un Space de HF con secretos fuera del código, conectar W&B y abrir la URL desde otro dispositivo.

## Material

- Diapositivas: `SI4006_S15_Semana15_Sesion15.pptx` (24 slides; versión con guion en notas: `..._MLG_con_guion.pptx`).
- Infografías incluidas en el deck (también sueltas): por qué ChatGPT responde tan rápido · cómo se usa un modelo en una empresa · temperatura y el profesor · costos, reglas de M5 y DevOps · cuantizar · el despliegue instrumentado · la despedida (nube de palabras del QR).

## Notebook

- **Lab principal:** `S15_Lab_Despliegue.ipynb` — Parte A: cuantizar a int4 y tabla antes/después. Parte B: `app.py` con Gradio, health y logging JSON, prueba con `share=True`. Parte C: Space de HF + `requirements.txt` + W&B. TODO 1: casos y harness · 2: conectar `sistema_multimodal` · 3: p50/p95 desde los logs · 4: requirements con versiones.
  [![Abrir en Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/manularrea/EAFIT-SI4006/blob/main/sesiones/s15/S15_Lab_Despliegue.ipynb)
- Versión resuelta: `S15_Lab_Despliegue_RESUELTO.ipynb`.

Modelos: `Qwen/Qwen2.5-1.5B-Instruct` como ejemplo (o el suyo). Herramientas: bitsandbytes, Gradio, Hugging Face Spaces, Weights & Biases. GPU T4 para la parte A.

## Antes de la sesión

- Su `sistema_multimodal` (o `responder_m3`) importable, y 10 casos del eval set.
- Cuenta en Hugging Face con un Space creado (vacío) y cuenta en W&B.
- El estudiante de S14 con su tabla, si destilaron.

## Entrega final · Demo day · S16 · jue 5 NOV · 15 min por equipo · 30 % · nota individual

M5 en el repo: URL pública con el sistema completo (M1–M4) · una técnica de eficiencia medida (destilado o cuantizado, con contrato y tabla antes/después) · health check, logging estructurado y dashboard de W&B · reporte final (problema y usuario, decisiones, scorecard vs. baselines, ablation, errores, límites y ética) · README reproducible. La infografía del demo day (qué decir minuto a minuto, cómo visibilizar un resultado, rúbrica de 30 puntos) está en Teams.

## Referencias

- Dettmers et al., *LLM.int8()* (2022) — arxiv.org/abs/2208.07339 · Dettmers et al., *QLoRA* (2023) — arxiv.org/abs/2305.14314
- Frantar et al., *GPTQ* (2022) — arxiv.org/abs/2210.17323 · Lin et al., *AWQ* (2023) — arxiv.org/abs/2306.00978
- Kwon et al., *Efficient Memory Management for LLM Serving with PagedAttention* (vLLM, 2023) — arxiv.org/abs/2309.06180
- Hugging Face Spaces docs — huggingface.co/docs/hub/spaces · Gradio docs — gradio.app/docs · W&B docs — docs.wandb.ai
- Profundización: Leviathan et al., *Speculative Decoding* (2023) — arxiv.org/abs/2211.17192 · NIST AI RMF 1.0 (2023)
