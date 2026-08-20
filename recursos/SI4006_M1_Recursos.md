# SI4006 · Recursos para M1 — datos y medición

Guía de lectura para reforzar dos cosas de su entrega M1: **cómo armar buenos ejemplos de fine-tuning** y **cómo medir el baseline vs. el modelo ya entrenado con Weights & Biases**. No tienen que leerlo todo — elijan según lo que su equipo necesite reforzar.

---

## 1 · Armar buenos ejemplos de fine-tuning

La calidad de sus 20 ejemplos importa más que la cantidad. Un ejemplo excelente enseña más que diez mediocres.

**Empiecen por aquí — Hugging Face, guía oficial de datasets**
https://huggingface.co/docs/transformers/en/tasks/summarization
La documentación oficial, con el formato exacto que espera el modelo. Es la fuente que usamos en el laboratorio, así que lo que vean aquí calza con su notebook.

**Meta AI — cómo curar un buen dataset de fine-tuning**
https://ai.meta.com/blog/how-to-fine-tune-llms-peft-dataset-curation/
De los ingenieros de Llama. Explica las reglas de oro con datos reales: los modelos pequeños bien afinados superan a los grandes en tareas específicas, y las tareas de generación/resumen necesitan más datos que las de clasificación. Directo y sin humo.

**DigitalOcean — cómo crear datos para fine-tuning**
https://www.digitalocean.com/community/tutorials/how-to-create-llm-finetuning-dataset
El más didáctico para empezar. Explica el formato JSONL (una línea = un ejemplo), cuántos ejemplos hacen falta según la técnica, y de dónde sacar datos de dominio: documentación, FAQs, tickets de soporte, guías internas.

**La idea que más les va a servir (de una guía de práctica 2026):**
El mejor dataset no es el más grande — es el que **coincide con lo que el sistema verá en producción**. Si su chatbot va a atender quejas de clientes en un e-commerce, no lo afinen con resúmenes de Wikipedia. Los ejemplos deben parecerse a las preguntas reales que recibirá su sistema. Un modelo afinado con datos que no reflejan su uso real "suena bien" pero falla cuando importa.

### Checklist rápido para sus 20 ejemplos
- [ ] Cada ejemplo es un par claro: **entrada → salida deseada**.
- [ ] Las entradas se parecen a lo que un usuario real escribiría (no versiones idealizadas).
- [ ] Las salidas son el tipo de respuesta que ustedes quieren que el modelo dé.
- [ ] Cubren la variedad de casos de su dominio, no solo el caso fácil.
- [ ] Están limpios: sin errores de tipeo, sin contradicciones entre ejemplos.
- [ ] Documentaron de dónde salieron y por qué son representativos (esto va en M1).

---

## 2 · Medir baseline vs. modelo fine-tuneado con W&B

El baseline es el corazón de M1: sin medir *antes* y *después*, no pueden demostrar que el fine-tuning sirvió. W&B es la herramienta para verlo y dejarlo registrado.

**Empiecen por aquí — W&B, documentación oficial de experiment tracking**
https://docs.wandb.ai/models/track
Cómo registrar métricas con pocas líneas de código y ver el dashboard que compara varias corridas. Es la base: aquí aprenden a que cada entrenamiento quede guardado y comparable.

**W&B para fine-tuning de LLMs (página oficial)**
https://wandb.ai/site/solutions/llm-fine-tuning/
Muestra cómo se conecta W&B con la Trainer API de Hugging Face — que es justo lo que usan en el notebook. La clave: con `report_to="wandb"` en el `TrainingArguments`, la curva de pérdida se registra sola, sin código extra.

**Guía práctica de setup (Markaicode)**
https://markaicode.com/wandb-llm-experiment-tracking-guide/
Paso a paso desde cero: crear la cuenta, conseguir la API key (en https://wandb.ai/authorize), y las primeras métricas. Ideal si nunca han tocado W&B.

### Cómo medir el baseline vs. el resultado (el patrón de M1)
La lógica que ya está en su notebook, explicada:

1. **Antes de entrenar (baseline):** le hacen a su modelo base una pregunta de su dominio y guardan la respuesta. Ese es el punto de partida.
2. **Entrenan con LoRA (o QLoRA):** durante el entrenamiento, W&B dibuja la pérdida en tiempo real. Debe **bajar** — esa curva es la señal de que aprende.
3. **Después de entrenar:** le hacen la **misma** pregunta al modelo ya afinado y comparan con el baseline.

Cómo leer la curva de pérdida en W&B:
- **Baja de forma sostenida** → el modelo está aprendiendo. 
- **Se estanca (se aplana)** → ya aprendió lo que podía; más épocas no ayudan.
- **Sube o oscila mucho** → algo anda mal: learning rate muy alto, o datos ruidosos.(OJO)

### Lo que W&B les deja para M1
- La **curva de pérdida** como evidencia visual de que el entrenamiento funcionó.
- Un registro **comparable** entre corridas: si prueban dos configuraciones de LoRA, las ven lado a lado.
- Un enlace al dashboard que pueden incluir en su entrega — observabilidad verificable, que es lo que pide el proyecto.

---

## Cómo usar esto para M1

No necesitan volverse expertos. Con esto basta:
1. Del bloque 1, lean el checklist y revisen sus 20 ejemplos contra él.
2. Del bloque 2, activen W&B en su notebook (`report_to="wandb"`) y guarden el enlace de su corrida.
3. En el informe, incluyan: los ejemplos documentados, la curva de pérdida de W&B, y la comparación baseline vs. resultado con su lectura de por qué mejoró (o por qué no).

Recuerden lo que dijimos en clase: **lo que más pesa no es que el número mejore mucho, es que ustedes entiendan y puedan explicar qué pasó.**

Cualquier duda, al canal. M1 cierra el domingo 16 de agosto.
