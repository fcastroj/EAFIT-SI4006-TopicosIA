# 🎯 Taller de nivelación — Preparate para S09
### SI4006 · Tópicos Especiales y Aplicaciones en IA · Módulos 1 y 2 + RAG inicial

> **Promesa del taller:** quien lo resuelva **a conciencia** — escribiendo sus respuestas ANTES de mirar las soluciones — llega al parcial dominando todos los temas que entran. No hay preguntas del parcial aquí; hay algo mejor: los mismos conceptos, ejercitados más duro de lo que el parcial los pregunta. MEJOR AUN: Lo que te preguntan en una vacante laboral como AI Engineer. 

---

## 📖 Cómo usar este taller (léelo, en serio)

Este taller usa tres principios con evidencia sólida en ciencias del aprendizaje:

1. **Práctica de recuperación (testing effect):** recordar algo desde cero fortalece la memoria mucho más que releerlo. Por eso cada ejercicio te pide **escribir tu respuesta antes de abrir la solución**. Si abres la solución primero, el taller no sirve — te sentirás "familiarizado" con el tema, que es exactamente lo que se siente saber sin saber.
2. **Calibración:** antes de verificar cada respuesta, márcala con 🟢 (seguro), 🟡 (dudoso) o 🔴 (ni idea). Al final, tu lista de 🟡 y 🔴 es tu plan de estudio personalizado — no pierdas tiempo repasando lo que ya está 🟢.
3. **Práctica espaciada:** NO hagas el taller de una sentada la noche anterior. Hazlo en **tres sesiones de ~45 min** en días distintos (por ejemplo: Estaciones 1–2, luego Estación 3, luego Estación 4 + cierre). El olvido entre sesiones es parte del entrenamiento, no un fallo.

**Materiales:** papel y lápiz (sí, físico: el parcial es sin computador) y las slides de S02–S07 SOLO para la fase de verificación.

**Cada solución está plegada** en un bloque `▸ Ver solución`. GitHub los muestra cerrados por defecto — el sistema de honor es contigo mismo.

---

## ⚡ Diagnóstico de entrada (5 min)

Sin mirar nada, responde mentalmente sí/no: ¿podrías ahora mismo...?

| # | ¿Podrías...? | 🟢/🟡/🔴 |
|---|---|---|
| D1 | Dibujar de memoria las dos torres del transformer con sus capas |  |
| D2 | Explicar qué hace la capa Feed Forward y de qué está hecha |  |
| D3 | Decidir encoder-only vs decoder-only para una tarea dada |  |
| D4 | Explicar qué congela y qué entrena LoRA (y escribir su fórmula) |  |
| D5 | Explicar por qué 92% de accuracy puede no significar nada |  |
| D6 | Decir qué mide BLEU y cuándo se equivoca |  |
| D7 | Explicar perplexity en una frase sin decir "perplejidad" |  |
| D8 | Nombrar los 3 sesgos del LLM-as-a-judge y una mitigación |  |
| D9 | Decidir RAG vs fine-tuning para un caso y justificarlo |  |
| D10 | Ordenar las 7 etapas del pipeline RAG |  |

Guarda esta tabla. Al terminar el taller vas a volver a llenarla — la diferencia entre las dos es lo que el taller te dio.

---

# 🏗 Estación 1 · El transformer por dentro
*(cubre: arquitectura, Feed Forward, atención — S02–S03)*

### Ejercicio 1.1 — Dibuja de memoria ✏️

Cierra todo. En papel, **dibuja la arquitectura del transformer** del paper *Attention Is All You Need*: las dos torres, sus capas en orden, y las flechas. Usa los nombres **en inglés** (Input Embedding, Positional Encoding, Multi-Head Attention, Feed Forward, Masked Multi-Head Attention, Add & Norm, Linear, Softmax).

No tiene que ser bonito. Tiene que estar **completo y en orden**.

Cuando termines — y solo cuando termines — compara con la figura 1 del paper (o la slide de S02) y marca con rojo TODO lo que te faltó o pusiste en otro lugar.

<details><summary>▸ Ver lista de verificación</summary>

Tu dibujo debe tener, de abajo hacia arriba:

**Torre izquierda (encoder):** Inputs → **Input Embedding** → ⊕ **Positional Encoding** → [ **Multi-Head Attention** → Add & Norm → **Feed Forward** → Add & Norm ] ×N

**Torre derecha (decoder):** Outputs (shifted right) → **Output Embedding** → ⊕ **Positional Encoding** → [ **Masked Multi-Head Attention** → Add & Norm → **Multi-Head Attention** (cruzada: recibe la salida del encoder) → Add & Norm → **Feed Forward** → Add & Norm ] ×N → **Linear** → **Softmax** → Output Probabilities

**Los tres errores más comunes:** (1) olvidar el Positional Encoding; (2) olvidar que la atención del medio del decoder es la que MIRA al encoder (cruzada); (3) olvidar la máscara en la primera atención del decoder — sin ella, el decoder vería el futuro y generar sería trampa.

**Si te faltaron 3 o más elementos:** repite el dibujo mañana desde cero. El segundo intento siempre sale mejor, y ese es el que se queda.
</details>

### Ejercicio 1.2 — Explícaselo a tu compañero de equipo 🗣

Escribe (3–4 frases, lenguaje sencillo) la respuesta a: **"¿qué es la capa Feed Forward y qué tiene que ver con un perceptrón?"** Imagina que se lo explicas a un compañero que faltó a esa clase.

<details><summary>▸ Ver solución</summary>

Idea esperada: la capa Feed Forward es una **pequeña red de perceptrones** dentro de cada bloque del transformer. Cada perceptrón (neurona) hace tres cosas: multiplica sus entradas por **pesos**, las **suma** (junto con un sesgo), y pasa el resultado por una **función de activación**. Mientras la atención decide *a qué tokens mirar*, la Feed Forward *procesa* lo que se recogió, token por token.

Auto-chequeo: si tu explicación no menciona pesos, suma y activación, quedó incompleta. Si dijiste que la Feed Forward "compara tokens entre sí", confundiste Feed Forward con atención — repasa la slide de S02 y vuelve a escribirla.
</details>

### Ejercicio 1.3 — Caza el error 🕵️

Cada afirmación tiene UN error. Encuéntralo y corrígelo (una línea cada una):

- a) "En self-attention, cada token produce dos vectores: query y value."
- b) "La atención enmascarada del decoder impide que el modelo vea los tokens anteriores."
- c) "El Positional Encoding le dice al modelo qué significa cada palabra."
- d) "La capa Softmax final convierte el texto en tokens."

<details><summary>▸ Ver solución</summary>

- a) Son **tres** vectores: query, **key** y value. (Query = lo que busco; key = la etiqueta con la que me encuentran; value = la información que entrego.)
- b) Al revés: impide ver los tokens **siguientes** (el futuro). Los anteriores son exactamente lo que sí puede ver.
- c) El significado viene del **embedding**; el Positional Encoding aporta la **posición** (el orden) — sin él, "perro muerde hombre" y "hombre muerde perro" serían lo mismo.
- d) Softmax no tokeniza: convierte los puntajes de la capa Linear en una **distribución de probabilidad** sobre el vocabulario para elegir el siguiente token.
</details>

---

# 🧬 Estación 2 · Familias y fine-tuning
*(cubre: encoder/decoder/enc-dec, MLM vs CLM, LoRA — S03–S04)*

### Ejercicio 2.1 — Ronda de clasificación rápida ⚡

Para cada sistema, escribe la familia (**encoder-only / decoder-only / encoder-decoder**) y UNA razón de máximo 10 palabras. Hazlo en menos de 6 minutos — en el parcial el tiempo vuela:

1. Detectar si un tweet sobre una vacuna es desinformación (sí/no).
2. Un tutor que explica fracciones conversando con un niño.
3. Traducir sentencias del español jurídico a lenguaje ciudadano.
4. Extraer el nombre del demandante de una demanda.
5. Redactar descripciones de producto a partir de la ficha técnica.
6. Clasificar reseñas de hoteles en positiva/negativa/neutra.
7. Resumir historias clínicas veterinarias.
8. Un chatbot de recomendaciones agrícolas.

<details><summary>▸ Ver solución</summary>

| # | Familia | Razón |
|---|---|---|
| 1 | encoder-only | entender texto → etiqueta (clasificar) |
| 2 | decoder-only | genera y conversa |
| 3 | encoder-decoder | transformar texto→texto |
| 4 | encoder-only | extraer un span, no generar |
| 5 | encoder-decoder (o decoder-only) | transformar ficha→texto; un LLM con prompt también sirve |
| 6 | encoder-only | clasificación pura |
| 7 | encoder-decoder (o decoder-only) | resumen = transformación |
| 8 | decoder-only | conversación abierta |

**El patrón que debes llevarte:** ¿la salida es una **etiqueta**? → encoder. ¿La salida es **texto libre**? → decoder. ¿La salida es **otro texto derivado del primero**? → encoder-decoder (aunque los LLM decoder-only modernos también lo hacen bien vía prompting — si escribiste eso como matiz, vas MUY bien).

7–8 correctas: tema dominado. 5–6: repasa la tabla de S03 y repite mañana. <5: vuelve a la slide "La métrica depende de qué hace su modelo" de S05, que conecta familias con tareas, y repite la ronda completa.
</details>

### Ejercicio 2.2 — LoRA: el ejemplo resuelto y el tuyo 🔢

**Ejemplo resuelto (léelo con calma):** una capa del modelo tiene una matriz W de 4096×4096 ≈ **16.7 millones** de parámetros. Con full fine-tuning, entrenas los 16.7M. Con LoRA de rango r=8: congelas W y entrenas B (4096×8) y A (8×4096) → 32.768 + 32.768 = **65.536 parámetros ≈ el 0.4%**. La actualización efectiva es W′ = W + B·A.

**Ahora tú, sin calculadora ni computador (aproxima):**

- a) Con r=16 en esa misma capa, ¿cuántos parámetros entrenas, aproximadamente? ¿Sigue siendo un ahorro enorme?
- b) ¿Por qué el producto B·A tiene el mismo tamaño que W, si B y A son pequeñas?
- c) Tu compañero dice: "entonces LoRA pierde mucha calidad, porque entrena el 0.4% del modelo". ¿Qué le responderías? (2 líneas)

<details><summary>▸ Ver solución</summary>

- a) 2 × (4096×16) = **131.072 ≈ el 0.8%**. Duplicar el rango duplica lo entrenable — y sigue siendo despreciable frente a 16.7M.
- b) B es 4096×**r** y A es **r**×4096: su producto es 4096×4096 — mismo tamaño que W. El rango r solo limita la "riqueza" de esa actualización, no su forma.
- c) La adaptación a un dominio suele necesitar cambios de **bajo rango** — no hay que reescribir todo el conocimiento del modelo, solo orientarlo. Empíricamente LoRA logra calidad comparable al full fine-tuning en adaptación de dominio; además evita dañar lo que el base ya sabe.
</details>

### Ejercicio 2.3 — MLM vs CLM en una tabla 📋

Completa de memoria (después verifica con S03):

| | ¿Qué predice? | ¿Qué contexto ve? | ¿Familia que lo usa? | ¿Sirve para generar? |
|---|---|---|---|---|
| **MLM** | | | | |
| **CLM** | | | | |

<details><summary>▸ Ver solución</summary>

| | ¿Qué predice? | ¿Qué contexto ve? | ¿Familia? | ¿Genera? |
|---|---|---|---|---|
| **MLM** | tokens ocultos dentro de la frase | ambos lados (bidireccional) | BERT (encoder-only) | no está entrenado para continuar secuencias |
| **CLM** | el siguiente token | solo lo anterior (izquierda→derecha) | GPT / LLaMA (decoder-only) | sí: generar ES predecir el siguiente token repetidamente |
</details>

---

# 📏 Estación 3 · Evaluación de sistemas generativos
*(cubre: accuracy y baselines, BLEU/embeddings, perplexity, benchmarks, LLM-judge, kappa — S05–S06)*

### Ejercicio 3.1 — El ejemplo resuelto del accuracy engañoso 🔍

**Léelo y luego responde las variantes.** Un dataset tiene 200 correos: 180 normales, 20 fraudulentos. Un "modelo" que responde SIEMPRE "normal" logra accuracy = 180/200 = **90%** sin detectar ni un solo fraude. Su recall de la clase "fraude" es 0/20 = **0%**. Moraleja: con clases desbalanceadas, el accuracy queda dominado por la clase mayoritaria; hay que mirar la clase que importa.

**Variantes (escribe tus respuestas):**

- a) Un modelo real logra 93% de accuracy en ese dataset. ¿Cuántos puntos aporta sobre "no hacer nada inteligente"?
- b) De los 20 fraudes, ese modelo detecta 8. Calcula el recall de "fraude" y di, en una frase, por qué ese número importa más que el 93%.
- c) Tu equipo del proyecto: ¿cuál es la clase (o el tipo de caso) minoritaria-pero-crítica de SU dominio? Escríbela — es la que su harness debe vigilar.

<details><summary>▸ Ver solución</summary>

- a) 93 − 90 = **3 puntos** sobre el baseline de clase mayoritaria. El "93%" impresiona; el "+3" cuenta la verdad.
- b) Recall = 8/20 = **40%**: deja pasar 6 de cada 10 fraudes. El costo del negocio está en los falsos negativos, y el accuracy global es ciego a eso.
- c) Ejemplos: brotes reales (salud pública), plazos procesales (legal), alertas de helada (agro), urgencias veterinarias, reclamos de garantía (e-commerce), señales de frustración del estudiante (educación). Si escribiste la de tu dominio, acabas de escribir un renglón de tu informe de M2.
</details>

### Ejercicio 3.2 — Tres candidatos, dos métricas 🎭

Referencia: **"El medicamento debe suspenderse si aparece fiebre."**

- Candidato A: "El medicamento debe continuarse si aparece fiebre."
- Candidato B: "Ante un episodio febril, interrumpa el tratamiento."
- Candidato C: "El medicamento debe suspenderse si aparece fiebre alta y sostenida por más de tres días."

Para cada candidato predice: ¿BLEU alto o bajo? ¿similitud por embeddings alta o baja? ¿es correcto o incorrecto frente a la referencia? Organízalo en una tabla de 3×3 y escribe UNA conclusión.

<details><summary>▸ Ver solución</summary>

| | BLEU | Embeddings | ¿Correcto? |
|---|---|---|---|
| A (niega) | **alto** (casi toda la superficie coincide) | **alto** (mismo tema — la negación apenas mueve el vector) | ❌ dice lo contrario |
| B (paráfrasis) | **bajo** (cero palabras en común) | **alto** | ✔ |
| C (agrega condiciones) | alto-medio | alto | ⚠ cambia la instrucción: añade condiciones que la referencia no pone |

Conclusión esperada: BLEU premia superficie (falla con A y con B por razones opuestas); los embeddings rescatan la paráfrasis pero **también** premian al candidato A y al C — ninguna métrica automática detecta sola la corrección factual. Por eso el harness tiene 3 dimensiones y un juez con rúbrica.

El candidato C es el más sutil — y el más parecido a los errores reales de un LLM: no contradice, **agrega**. Si lo cazaste, estás leyendo como evaluador.
</details>

### Ejercicio 3.3 — Perplexity: el detector de mitos 🧯

Marca V/F y corrige las falsas en una línea:

- a) La perplexity necesita respuestas de referencia para calcularse.
- b) PPL = 1 significa que el modelo predice cada token con certeza total.
- c) Comparar la PPL de dos modelos con tokenizadores distintos es válido si el texto es el mismo.
- d) Un modelo con PPL bajísima en foros de internet repetirá con fluidez los mitos frecuentes de esos foros.
- e) La perplexity es la exponencial de la cross-entropy — el training loss que vieron bajar en M1.

<details><summary>▸ Ver solución</summary>

a) **F** — es intrínseca: solo necesita el modelo y el texto. b) **V**. c) **F** — la PPL se promedia por token y cada tokenizador parte distinto: escalas no comparables. d) **V** — baja sorpresa premia lo frecuente, no lo cierto. e) **V** — cuando el loss bajó de 3.0 a 2.0, la PPL bajó de ~20 a ~7.4.

4–5 correctas: listo. Menos: relee la slide "Cuándo perplexity engaña" de S05 — son exactamente estas tres letras pequeñas.
</details>

### Ejercicio 3.4 — El juez y sus vicios ⚖️

Sin mirar las slides:

- a) Nombra los **tres sesgos** del LLM-as-a-judge y da un ejemplo de una línea para cada uno.
- b) Tu equipo compara la versión con-RAG contra la sin-RAG usando el juez en modo pairwise. Describe el **protocolo exacto** (paso a paso) para que el sesgo de posición no contamine la conclusión.
- c) Pregunta de conexión: ¿por qué medir el acuerdo entre DOS PERSONAS (Cohen's kappa) es un paso previo a confiar en el juez máquina? (2–3 líneas)

<details><summary>▸ Ver solución</summary>

- a) **Posición** (prefiere la primera que ve: al invertir el orden cambia de favorita) · **Longitud** (mejor nota a la más larga, aunque no sea mejor) · **Auto-preferencia** (prefiere respuestas de su propia familia de modelos).
- b) Para cada pregunta del eval set: (1) presentar el par en orden A-B y registrar el veredicto; (2) presentar B-A y registrar; (3) declarar ganadora SOLO si ambos veredictos coinciden; si cambia con el orden → empate; (4) agregar sobre todo el eval set. (Bonus si añadiste: rúbrica con anclas y pedir solo la letra como salida.)
- c) Si dos humanos con la misma rúbrica no concuerdan (kappa bajo), la rúbrica es ambigua — y calibrar un juez contra una rúbrica ambigua es calibrarlo contra ruido. Primero se depura la rúbrica hasta que los humanos concuerden; luego ese juicio humano es la vara contra la que se valida el juez.
</details>

### Ejercicio 3.5 — El leaderboard sospechoso 🏆

Un vendedor te dice: "nuestro modelo es #1 en MMLU, así que es el mejor para su chatbot de e-commerce en Colombia". Escribe las **tres réplicas** distintas que le harías (una línea cada una) y qué evaluación exigirías antes de firmar.

<details><summary>▸ Ver solución</summary>

Réplicas esperadas (tres mecanismos distintos): (1) **contaminación** — MMLU es público hace años; el puntaje puede ser memoria, no capacidad; (2) **desalineación** — MMLU es opción múltiple académica en inglés; su caso es generación en español sobre SU catálogo; (3) **sobreajuste al benchmark** — prompt-tuning para ese examen no transfiere a su tarea. Evaluación a exigir: correr los modelos candidatos sobre **su eval set propio** (gold + adversariales) con **su harness** — el leaderboard preselecciona, el eval propio decide.
</details>

---

# 🔎 Estación 4 · RAG inicial
*(cubre: motivación, pipeline, chunking, RAG vs fine-tuning — S07)*

### Ejercicio 4.1 — El pipeline, de memoria y al revés 🔄

- a) Escribe las **7 etapas** del pipeline RAG en orden, y sepáralas en sus dos fases (indexación / consulta).
- b) Ahora el reto inverso: para cada síntoma, di **qué etapa** probablemente falló:
  1. El sistema responde con un pasaje del documento correcto, pero cortado a la mitad de la idea.
  2. La búsqueda devuelve chunks del tema equivocado.
  3. El chunk correcto está en el prompt, pero el modelo responde de memoria otra cosa.
  4. El sistema no encuentra nada sobre un decreto de la semana pasada.

<details><summary>▸ Ver solución</summary>

- a) **Indexación (offline):** ingest → chunk → embed → store. **Consulta (online):** retrieve → augment → generate.
- b) 1 → **chunk** (el corte partió la idea; revisar tamaño/overlap). 2 → **retrieve/embed** (la búsqueda semántica no está matcheando; a veces también chunking). 3 → **generate** (el modelo ignora el contexto; revisar el prompt y su válvula de escape). 4 → **ingest** (el documento nunca entró al corpus — ninguna búsqueda encuentra lo que no se indexó).

Este mapeo síntoma→etapa es EXACTAMENTE el diagnóstico que harán en M3. Si lo dominas, la entrega M3 te va a fluir.
</details>

### Ejercicio 4.2 — ¿RAG, fine-tuning o ambos? Decide como ingeniero 🧭

Para cada necesidad, escribe **RAG / fine-tuning / ambos** + una razón de una línea:

1. Que el asistente legal cite el artículo exacto y vigente de la norma.
2. Que el bot de la tienda responda siempre con el tono de la marca.
3. Que el tutor resuelva con el método de enseñanza propio del colegio Y use los ejercicios del libro del período actual.
4. Que el sistema veterinario conozca el brote de moquillo reportado este mes.
5. Que el modelo aprenda el formato de reporte agroclimático de la federación.

<details><summary>▸ Ver solución</summary>

1. **RAG** — conocimiento cambiante + trazabilidad (citar la fuente). 2. **Fine-tuning** — el tono es un patrón estable de comportamiento (forma). 3. **Ambos** — el método es forma (FT), los ejercicios del período son contenido cambiante (RAG). 4. **RAG** — conocimiento reciente: re-indexar, no reentrenar. 5. **Fine-tuning** — formato/estilo estable.

**La regla para el parcial y para la vida:** ¿el problema es de **habilidad/forma estable**? → fine-tuning. ¿Es de **conocimiento cambiante, privado o citable**? → RAG. ¿Tiene de las dos? → ambos, y no es contradicción: es la arquitectura de su proyecto.
</details>

### Ejercicio 4.3 — Explica el chunk con TU corpus 📚

En 3 líneas, usando **un documento real de tu proyecto** (una norma, una ficha de producto, un protocolo): ¿qué es un chunk, por qué ese documento no se indexa entero, y qué pasaría con una pregunta concreta si el chunk fuera demasiado grande?

<details><summary>▸ Ver solución</summary>

Estructura esperada (con TU documento): un chunk es un **pedazo del documento y la unidad de recuperación**. Entero no se indexa porque su embedding promediaría todos sus temas y no quedaría cerca de ninguna pregunta concreta (además de inflar el prompt). Con chunks demasiado grandes, la pregunta puntual matchearía un pedazo lleno de ruido, y el modelo respondería diluido — o con la parte equivocada del documento.

Si tu respuesta funciona con tu documento real, ya tienes escrito el párrafo de "decisiones de chunking" del informe de M3.
</details>

---

## 🏁 Cierre metacognitivo (15 min — no te lo saltes)

1. **Vuelve al diagnóstico de entrada** y llénalo de nuevo. Compara.
2. Todo lo que siga en 🟡/🔴 tiene su ruta corta:

| Si sigue difícil... | Repasa... | Y repite... |
|---|---|---|
| Arquitectura / dibujo | figura 1 del paper + slides S02 | Ejercicio 1.1 mañana |
| Familias | tabla de S03 | Ejercicio 2.1 (cronómetro: 5 min) |
| LoRA | slides S04 | Ejercicio 2.2 con r=4 |
| Accuracy/baselines | "la pregunta trampa" de S05 | Ejercicio 3.1 con otros números |
| BLEU/embeddings | Lab A de S05 | Ejercicio 3.2 inventando un candidato D |
| Perplexity | "cuándo perplexity engaña" S05 | Ejercicio 3.3 |
| Juez y sesgos | slides S06 + Lab B | Ejercicio 3.4b escrito de memoria |
| RAG | pipeline S07 + su propio Lab | Ejercicios 4.1 y 4.2 |

3. **La prueba final del taller:** explícale el curso a alguien que no es del curso, en 5 frases: qué es un transformer, qué le hicieron en M1, cómo saben si quedó bueno (M2), y qué le agregaron en S07 y por qué. Si las 5 frases salen solas, estás listo. Si alguna se traba, esa es tu última sesión de repaso.

> **Nota honesta sobre el parcial:** el parcial no pregunta definiciones de memoria — pregunta si sabes **usar** estos conceptos en casos nuevos. Este taller te entrenó exactamente en eso. Si lo hiciste a conciencia (escribiendo antes de abrir, en tres sesiones, con la tabla de calibración llena), el parcial va a sentirse como una ronda más del taller. Nos vemos en S09. 💪
