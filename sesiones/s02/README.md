# Sesión 02 · Abrir la caja

**Módulo:** M1 — Transformers y fine-tuning con Hugging Face · **Duración:** 3 h

Tokenización, self-attention y codificación posicional, construidos a mano. Al final de la sesión cada estudiante ha escrito, línea por línea, el mecanismo que hace funcionar a los modelos que usamos en la Sesión 1.

## Contenido

- **Tokenización** — subpalabra, BPE, WordPiece y SentencePiece. Por qué un mismo texto cuesta distinto según el tokenizador, y qué significa eso para un proyecto en español.
- **Self-attention** — embeddings estáticos frente a contextuales; los papeles Q, K, V; y la ecuación `softmax(Q·Kᵀ/√d)·V` paso a paso.
- **Codificación posicional** — por qué la atención pura no distingue el orden de las palabras, y cómo se le inyecta la posición: sinusoidal, aprendida y RoPE.
- **Multi-head attention** — varias atenciones en paralelo y qué aporta cada cabeza.

## Material

- Diapositivas: `SI4006_S02_Semana2_Sesion2.pptx` (en esta carpeta)

## Notebook

Laboratorio de la sesión — tres partes: forense de tokenizadores, attention a mano y la atención no sabe de orden.

[![Abrir en Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/manularrea/EAFIT-SI4006/blob/main/sesiones/s02/S02_Lab_Abrir_la_caja.ipynb)

> La versión resuelta (`S02_Lab_Abrir_la_caja_SOLUCION.ipynb`) se publica **después** de la sesión, e incluye material adicional de profundización marcado con 🔬.

## Antes de la sesión

- Tener cuenta de Hugging Face (gratuita) y haber verificado el acceso a Google Colab.
- No se necesita GPU para este laboratorio: todo corre en CPU.

## Después de la sesión

- Leer la **sección 3** de *Attention Is All You Need* — [arxiv.org/abs/1706.03762](https://arxiv.org/abs/1706.03762). Ya escribieron la ecuación en clase; ahora la van a reconocer en el paper.
- Cada equipo llega a la Sesión 3 con un **candidato a modelo base** para M1, evaluando cómo tokeniza su dominio.

## Referencias

- Vaswani et al. (2017), *Attention Is All You Need* — [arxiv.org/abs/1706.03762](https://arxiv.org/abs/1706.03762)
- Su et al. (2021), *RoFormer: Enhanced Transformer with Rotary Position Embedding* — [arxiv.org/abs/2104.09864](https://arxiv.org/abs/2104.09864)
- Alammar, J., *The Illustrated Transformer* — [jalammar.github.io/illustrated-transformer](https://jalammar.github.io/illustrated-transformer/)
