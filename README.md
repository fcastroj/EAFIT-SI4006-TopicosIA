<div align="center">

# SI4006 · Tópicos Especiales y Aplicaciones en IA

Curso electivo de la Universidad EAFIT: 16 sesiones construyendo, en equipo, un sistema de IA generativa desplegado.

![Curso](https://img.shields.io/badge/Curso-SI4006-1f4e79?style=flat-square)
![Universidad EAFIT](https://img.shields.io/badge/Universidad-EAFIT-1f4e79?style=flat-square)
![Python](https://img.shields.io/badge/Python-3.10%2B-1f4e79?style=flat-square&logo=python&logoColor=white)
[![Abrir en Colab](https://img.shields.io/badge/Abrir%20en-Colab-1f4e79?style=flat-square&logo=googlecolab&logoColor=white)](https://colab.research.google.com/github/manularrea/EAFIT-SI4006/blob/main/sesiones/s01/S01_Demo_Capacidades.ipynb)
[![CI](https://img.shields.io/github/actions/workflow/status/manularrea/EAFIT-SI4006/ci.yml?branch=main&style=flat-square&label=CI)](https://github.com/manularrea/EAFIT-SI4006/actions/workflows/ci.yml)

**[Cómo usar](#cómo-usar-este-repositorio) · [Mapa del semestre](#mapa-del-semestre) · [Sesiones](#sesiones) · [Evaluación](#evaluación) · [Proyecto](#proyecto-integrador) · [Setup](#entorno-y-setup) · [Contacto](#contacto)**

</div>

---

## Qué es este curso

Electiva de séptimo semestre (3 créditos) sobre IA generativa aplicada. A lo
largo de 16 sesiones de 3 horas, cada equipo lleva un proyecto desde la
definición del problema hasta una demo pública desplegada, pasando por
fine-tuning, evaluación rigurosa, RAG, multimodalidad y serving eficiente. No
hay examen final: el cierre es la demo.

## Cómo usar este repositorio

La ruta del estudiante, en tres pasos:

1. **Abre la sesión** en [`sesiones/`](sesiones/) y lee su `README`.
2. **Haz clic en el badge de Colab** del notebook de la sesión.
3. **Activa la GPU** en Colab (`Entorno de ejecución` → `Cambiar tipo` → GPU T4)
   y corre primero la celda de instalación.

Detalle completo en [recursos/setup-colab.md](recursos/setup-colab.md).

## Mapa del semestre

Los cinco módulos no son temas sueltos: cada uno apila una capa sobre el mismo
proyecto, que converge en una demo desplegada.

```mermaid
flowchart TD
    S01([S01 · Encuadre — se define el proyecto])

    S01 --> M1
    M1["M1 · S02–S04 · Fine-tuning con Hugging Face<br/>+ modelo ajustado al dominio"]
    M2["M2 · S05–S06 · Evaluación generativa<br/>+ harness de evaluación"]
    M3["M3 · S07–S08 · S10 · RAG · tool use · RAGAS<br/>+ sistema RAG con tool use"]
    M4["M4 · S11–S13 · ViT · CLIP · difusión<br/>+ componente visual"]
    M5["M5 · S14–S15 · Serving y MLOps<br/>+ despliegue y eficiencia"]

    M1 --> M2 --> M3 --> M4 --> M5
    M5 --> FINAL([S16 · Demo pública desplegada])

    S09{{S09 · Parcial individual — módulos 1 y 2}}
    M2 -.evalúa.-> S09
```

## Sesiones

| # | Módulo | Tema | Material | Colab |
|:--:|:--:|------|:--:|:--:|
| 01 | Encuadre | Encuadre y demo de capacidades | [Ver](sesiones/s01/) | [![Colab](https://img.shields.io/badge/Abrir-Colab-1f4e79?style=flat-square&logo=googlecolab&logoColor=white)](https://colab.research.google.com/github/manularrea/EAFIT-SI4006/blob/main/sesiones/s01/S01_Demo_Capacidades.ipynb) |
| 02 | M1 | Transformers y fine-tuning con Hugging Face | [Ver](sesiones/s02/) | — |
| 03 | M1 | Transformers y fine-tuning con Hugging Face | [Ver](sesiones/s03/) | — |
| 04 | M1 | Transformers y fine-tuning con Hugging Face | [Ver](sesiones/s04/) | — |
| 05 | M2 | Evaluación de sistemas generativos | [Ver](sesiones/s05/) | — |
| 06 | M2 | Evaluación de sistemas generativos | [Ver](sesiones/s06/) | — |
| 07 | M3 | RAG, agentes, tool use, RAGAS | [Ver](sesiones/s07/) | — |
| 08 | M3 | RAG, agentes, tool use, RAGAS | [Ver](sesiones/s08/) | — |
| 09 | Parcial | Parcial individual (módulos 1 y 2) | [Ver](sesiones/s09/) | — |
| 10 | M3 | RAG, agentes, tool use, RAGAS | [Ver](sesiones/s10/) | — |
| 11 | M4 | ViT, CLIP, multimodales, difusión | [Ver](sesiones/s11/) | — |
| 12 | M4 | ViT, CLIP, multimodales, difusión | [Ver](sesiones/s12/) | — |
| 13 | M4 | ViT, CLIP, multimodales, difusión | [Ver](sesiones/s13/) | — |
| 14 | M5 | Destilación, quantization, serving, MLOps | [Ver](sesiones/s14/) | — |
| 15 | M5 | Destilación, quantization, serving, MLOps | [Ver](sesiones/s15/) | — |
| 16 | Cierre | Demos finales | [Ver](sesiones/s16/) | — |

Índice también en [sesiones/README.md](sesiones/README.md). El guion (—) en Colab
indica que el notebook de esa sesión aún no está publicado.

## Evaluación

Sin examen final. La nota se reparte entre los entregables del proyecto y un
parcial individual.

| Ítem | Sesión | Peso |
|------|:--:|:--:|
| M1 — Fine-tuning baseline + dataset | S04 | 10% |
| M2 — Harness de evaluación + scorecard | S06 | 10% |
| Parcial individual (módulos 1 y 2) | S09 | 15% |
| M3 — Sistema RAG + evaluación RAGAS | S10 | 15% |
| M4 — Pipeline multimodal + casos de prueba | S13 | 10% |
| Proyecto final — demo desplegada + presentación + reporte | S16 | 40% |
| **Total** | | **100%** |

## Proyecto integrador

Hilo conductor del curso: un proyecto en equipos de 3–4 personas que crece
módulo a módulo hasta una demo pública desplegada. Arranca en la Sesión 1 con la
definición del problema y el usuario.

Empieza por la [plantilla de definición](proyecto/plantilla-definicion.md).

## Entorno y setup

<details>
<summary>Colab (ruta principal) y setup local</summary>

<br>

**Colab** es la ruta principal: no necesitas instalar nada. Cada notebook abre
en Colab desde su badge y corre en la GPU gratuita T4. Ver
[recursos/setup-colab.md](recursos/setup-colab.md).

**Local** (secundario) — si prefieres tu máquina:

```bash
python -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
```

Las versiones de [`requirements.txt`](requirements.txt) están fijadas a
propósito: `transformers==4.49.0` es el piso para Qwen2.5 y SmolVLM con el
pipeline `image-text-to-text`. No las cambies.

**Stack:** Python · PyTorch · Hugging Face (transformers, sentence-transformers)
· Google Colab (T4) · Chroma · RAGAS · Weights & Biases · Gradio/Streamlit ·
Hugging Face Spaces.

</details>

## Política de uso de IA

<!-- TODO: la docente redacta la política de uso de IA del curso. -->

## Contacto

- **Docente:** Manuela Larrea Gómez — [mlarreag@eafit.edu.co](mailto:mlarreag@eafit.edu.co)
- **Canal oficial del curso:** Microsoft Teams

Para erratas o notebooks que no corren, abre un [issue](https://github.com/manularrea/EAFIT-SI4006/issues); para dudas
administrativas y de entregas, usa Teams.

## Licencia

Licencia dual: el **código** se distribuye bajo [MIT](LICENSE) —reutilízalo
libremente—; el **material docente** (diapositivas, guiones, enunciados) bajo
[CC BY-NC-SA 4.0](LICENSE-CONTENIDO.md) —se comparte con atribución, pero no se
comercializa.
