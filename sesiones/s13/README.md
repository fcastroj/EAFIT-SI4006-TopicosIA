# Sesión 13 · Integrar la visión al proyecto: patrones, laboratorio guiado y entrega M4

**Módulo:** M4 — ViT, CLIP, multimodales, difusión · **Duración:** 3 h · **Fecha:** jue 15 OCT · Taller con entrega

## Contenido

Cierra la Unidad 4. No hay modelo nuevo: cada equipo integra **un** componente visual (input, tool u output) al sistema de M3, lo mide con su harness (≥5 casos con imagen) y llena la tabla de delta contra M3. La sesión es un taller en dos partes con mini-presentaciones al final; lo que sale del notebook es el núcleo de la **entrega M4**.

| Bloque | Tema | Lab |
|---|---|---|
| 0 | Recap: dudas del formulario (las flechitas y los schedulers DDPM/DDIM/Euler/DPM-Solver · las piezas de Stable Diffusion y ControlNet · "¿solo analizar, sin generar?" · los diez años: de carísimo a un Colab gratis) + mapa del semestre | — |
| 1 | Integrar: los tres patrones (decisión final), la receta de cinco pasos, cada patrón por dentro (input / tool / output) | Parte 1 |
| 2 | Medir: el eval set con imagen, criterios que saben mirar (exacto, campos, válvula, juez VLM, checklist, CLIP score, latencia), la tabla de delta contra M3 | Parte 2 |
| 3 | Mini-presentaciones: 4 min por equipo (pregunta · patrón · un caso en vivo · tabla de delta · el fallo) | — |
| 4 | Entrega M4: rúbrica, qué va en `m4/`, ética del contenido visual · profundización (SAM, DINOv2, ColPali) · hacia S14 (eficiencia) | — |

Al terminar la sesión pueden:

- Construir una función `ver()` con el modelo que corresponde a su patrón (VLM, CLIP/ViT o difusión) y probarla sola, con latencia.
- Enchufarla al sistema de M3 sin reescribirlo: antes del RAG, en la lista de tools o después del LLM.
- Escribir casos de prueba con imagen (incluido uno adversarial) y calificarlos con criterios nuevos dentro del mismo harness de M2.
- Llenar y leer la tabla de delta contra M3: ¿mejoró lo nuevo? ¿no empeoró lo viejo? ¿cuánto cuesta?

## Material

- Diapositivas: `SI4006_S13_Semana13_Sesion13.pptx` (32 slides; versión con guion en notas: `..._MLG_con_guion.pptx`).
- Infografías incluidas en el deck (también sueltas): las flechitas y los schedulers · las piezas de SD y ControlNet · ¿solo analizar, sin generar? · la línea de tiempo 2012–2024 · mapa del semestre S13.

## Notebook

- **Lab principal:** `S13_Lab_Integracion_Visual.ipynb` — Parte 1 (elegir patrón, `ver()` con VLM / CLIP / SD, probarla, enchufarla con `sistema_multimodal`) y Parte 2 (casos con imagen, harness con criterios nuevos, tabla de delta, `scorecard_m4.csv`). TODO 1: patrón y pregunta · 2: instrucción / clases / plantilla del dominio · 3: conectar `responder_m3` · 4: ≥5 casos · 5: `nota_campos` · 6: números de M3.
  [![Abrir en Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/manularrea/EAFIT-SI4006/blob/main/sesiones/s13/S13_Lab_Integracion_Visual.ipynb)
- Versión resuelta: `S13_Lab_Integracion_Visual_RESUELTO.ipynb`.

Modelos según patrón: `Qwen/Qwen2-VL-2B-Instruct` (input), `openai/clip-vit-base-patch32` (tool, corre en CPU), `stable-diffusion-v1-5/stable-diffusion-v1-5` (output, GPU). Opcional: `facebook/sam-vit-base`. GPU T4 en Colab.

## Antes de la sesión

- Traer 3–6 imágenes del dominio (anonimizadas), el `responder_m3` de su repo (o la URL) y el scorecard de M3.
- Tener decidido el patrón (input / tool / output) y la pregunta del usuario que lo justifica: el plan visual declarado en S11.
- Correr la celda de instalación desde el inicio; si el patrón es output, instalar `diffusers`.

## Entrega M4 · dom 25 OCT · 23:59 · 10 %

Carpeta `m4/` en el repo del equipo:

1. `pipeline` — el notebook terminado o un módulo importable: `ver()`, `sistema_multimodal()` y la conexión con el sistema de M3. Debe correr desde cero en Colab.
2. `eval_set` — CSV con ≥5 casos con imagen (uno adversarial, criterio declarado por caso) y la carpeta de imágenes referenciadas, sin datos personales.
3. `scorecard_m4.csv` y la tabla de delta M3 vs. M4 (con latencia).
4. `README.md` de una página: la pregunta, el patrón, el modelo, dónde se enchufó, la tabla de delta, el peor caso y los límites.

Rúbrica: pipeline funcionando (3.0) · justificación del patrón (1.5) · eval set con imagen (2.0) · harness, scorecard y delta (2.5) · límites y ética (1.0). Lo que va más allá de lo visto en clase se valora. Entrega tardía: −2 % por día, máximo 7 días.

Clase grabada: en lugar de la mini-presentación en el aula, video de 4 min en Teams con la misma estructura y el mismo plazo.

## Referencias

- Liu et al., *Visual Instruction Tuning* (LLaVA, 2023) — arxiv.org/abs/2304.08485 · Wang et al., *Qwen2-VL* (2024) — arxiv.org/abs/2409.12191
- Radford et al., *CLIP* (2021) — arxiv.org/abs/2103.00020 · Rombach et al., *High-Resolution Image Synthesis with Latent Diffusion Models* (2022) — arxiv.org/abs/2112.10752
- Zhang et al., *Adding Conditional Control to Text-to-Image Diffusion Models* (ControlNet, 2023) — arxiv.org/abs/2302.05543
- Lu et al., *DPM-Solver* (2022) — arxiv.org/abs/2206.00927 · Song et al., *DDIM* (2021) — arxiv.org/abs/2010.02502
- Profundización: SAM (arxiv.org/abs/2304.02643) · DINOv2 (arxiv.org/abs/2304.07193) · ColPali (arxiv.org/abs/2407.01449)
