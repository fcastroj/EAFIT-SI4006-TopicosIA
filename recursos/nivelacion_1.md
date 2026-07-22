# Nivelación · Módulo 1 (Sesiones 2 a 4)

> **Para quién es esto.** Las sesiones 2, 3 y 4 son las más técnicas del semestre y arrancan rápido. Si en algún laboratorio sientes que todos entienden el código menos tú, no es que estés atrasado en el tema del día: casi siempre es que falta uno de los tres cimientos de abajo. Esta guía los cubre. No entra en evaluación y no hay que entregarla — es una red de seguridad para que los laboratorios se disfruten en vez de sufrirse.
>
> **Cómo usarla.** No la leas entera de corrido. Haz el autodiagnóstico, y baja solo al bloque que te falle.

---

## Autodiagnóstico (5 minutos)

Abre un Colab en blanco y trata de escribir, sin buscar en internet, lo siguiente. Si puedes con los cuatro, estás nivelada para el Módulo 1 y no necesitas nada más de este documento.

1. Crear un tensor de PyTorch de forma `(2, 3)` con números al azar, e imprimir su `.shape`.
2. Multiplicar dos matrices con `@` y explicar por qué `(2,3) @ (3,4)` funciona pero `(2,3) @ (2,3)` no.
3. Cargar cualquier modelo desde Hugging Face con `AutoModel.from_pretrained(...)` y su tokenizador.
4. Decir qué hace `softmax` a un vector de números, en una frase.

¿Te trabaste en alguno? Ese número te dice a qué bloque ir: 1 y 2 → **Bloque A**, 3 → **Bloque B**, 4 → **Bloque C**.

---

## Bloque A · Tensores y operaciones matriciales

**Por qué importa.** Un transformer es, por dentro, una secuencia de multiplicaciones de matrices. En el Lab de la Sesión 2 vas a escribir `Q @ K.transpose(-2, -1)` con tus manos. Si los tensores te son cómodos, esa línea es transparente; si no, es un muro.

**Qué necesitas dominar, en orden:**

Lo primero es la idea de **forma** (`shape`). Un tensor es una caja de números con dimensiones, y casi todos los errores de PyTorch que vas a ver este semestre dicen lo mismo con distintas palabras: "las formas no encajan". Aprender a leer un `shape` y a predecir el `shape` del resultado de una operación es, con diferencia, la habilidad que más te va a ahorrar tiempo.

Después, la **multiplicación de matrices**: por qué `(a, b) @ (b, c)` da `(a, c)`, y por qué la dimensión del medio tiene que coincidir. No necesitas la matemática formal — necesitas la intuición de las formas y saber que `@` es el operador.

Por último, dos operaciones que aparecen todo el tiempo: `transpose` (intercambiar dos ejes) y `softmax` (convertir números en una distribución que suma 1). Las dos salen en el Lab B.

**Recursos concretos:**
- *Deep Learning with PyTorch: A 60 Minute Blitz*, sección "Tensors" — la documentación oficial, es corta y práctica: [pytorch.org/tutorials/beginner/blitz](https://pytorch.org/tutorials/beginner/deep_learning_60min_blitz.html)
- Para la intuición visual de qué es multiplicar matrices, el video de 3Blue1Brown "But what is a matrix multiplication?" sobre transformaciones lineales. No necesitas el álgebra completa, solo la primera mitad.

**Ejercicio de comprobación.** Si puedes correr esto y predecir el `shape` de cada línea *antes* de ejecutarla, estás listo:
```python
import torch
X = torch.randn(1, 4, 8)       # ¿shape?
W = torch.randn(8, 8)          # ¿shape?
Y = X @ W                      # ¿shape?
Z = Y.transpose(-2, -1)        # ¿shape?
P = torch.softmax(Z, dim=-1)   # ¿suma 1 sobre qué eje?
```

---

## Bloque B · El ecosistema de Hugging Face

**Por qué importa.** A partir de la Sesión 2 todo sale de Hugging Face: los tokenizadores, los modelos, y en S04 también los datasets. Casi nadie entrena desde cero — el trabajo real es *cargar bien* algo que alguien ya entrenó. Si el patrón `from_pretrained` te resulta natural, las tres sesiones fluyen.

**Qué necesitas dominar:**

El patrón central es siempre el mismo, y se repite todo el semestre: se elige un identificador de modelo (por ejemplo `"Qwen/Qwen2.5-3B-Instruct"`), y con él se cargan **dos** cosas emparejadas — el tokenizador y el modelo. Van juntos siempre: cada modelo espera el tokenizador con el que fue entrenado, y mezclarlos produce resultados sin sentido de forma silenciosa. Entender que son un par inseparable te evita el bug más común de principiante en esto.

Lo segundo es saber navegar el **Hub** (huggingface.co): buscar un modelo, leer su tarjeta, y distinguir un modelo `base` de uno `Instruct` — porque en S03 vas a tener que elegir uno para tu proyecto, y esa distinción cambia todo.

**Recursos concretos:**
- El curso oficial de Hugging Face, capítulos 1 y 2 — gratis, en español, y es exactamente esto: [huggingface.co/learn/nlp-course](https://huggingface.co/learn/nlp-course)
- Crear la cuenta de Hugging Face (si no la tienes de la tarea de S01) y dar una vuelta por el Hub con intención: busca un modelo de tu dominio y lee su tarjeta.

**Ejercicio de comprobación.** Cargar un tokenizador y ver, con tus ojos, en qué convierte una frase:
```python
from transformers import AutoTokenizer
tok = AutoTokenizer.from_pretrained("gpt2")
print(tok.tokenize("Nivelación para el Módulo 1"))
```
Si entiendes por qué la salida son fragmentos y no palabras completas, ya llegaste a donde empieza el Lab A.

---

## Bloque C · Las tres ideas de machine learning que se dan por sabidas

**Por qué importa.** El curso asume Fundamentos de Aprendizaje Automático y Redes Neuronales como prerrequisito. Si vienes con esos frescos, salta este bloque. Si hace rato no los tocas, estos son los tres conceptos que van a aparecer sin aviso.

**Los tres, en una frase cada uno:**

**Softmax** — toma una lista de números cualesquiera y los convierte en una lista que suma 1, resaltando el más grande. Es cómo un modelo pasa de "puntajes crudos" a algo que se puede leer como pesos o probabilidades. Aparece en el corazón de la atención (S02) y en la salida de casi todo modelo.

**Gradiente y entrenamiento** — entrenar es ajustar los números del modelo poco a poco para que se equivoque menos, midiendo en qué dirección moverlos. No necesitas derivar nada a mano; necesitas la intuición de que "entrenar = corregir en la dirección que reduce el error, muchas veces". Es lo que va a estar pasando por dentro en S04.

**Embedding** — representar algo (una palabra, un token) como un vector de números, de modo que cosas parecidas queden cerca en el espacio. Ya lo viste en Redes Neuronales con word2vec; en S02 vas a ver cómo la atención lo lleva un paso más allá.

**Recurso concreto:**
- Si quieres una sola fuente que cubra los tres con intuición y cero álgebra pesada, los primeros capítulos de *The Illustrated Word2vec* y *The Illustrated Transformer* de Jay Alammar — están en la bibliografía del curso y son la mejor puerta de entrada visual: [jalammar.github.io](https://jalammar.github.io)

---

## Si sigues perdida después de esto

No es fracaso, es el punto de partida — y lo dijimos el primer día: el salón no es homogéneo y está bien. Dos caminos:

- Trae la duda concreta al canal **Atascos y hallazgos** de Teams. "No entiendo por qué este tensor tiene esta forma" es exactamente el tipo de pregunta para la que existe ese canal.
- La barrera de herramientas se supera en semanas; el criterio toma el semestre. Ponerte al día en esto ahora es la mejor inversión de tiempo del curso, porque todo lo demás se apoya aquí.

---

## Stack y herramientas del curso

Para el uso concreto de las herramientas (Colab con GPU, cuenta de Hugging Face, configuración del entorno), ver [`setup-colab.md`](setup-colab.md).

---

*Material de nivelación (propuesta docente). No corresponde a contenido evaluable del microcurrículo; es apoyo para emparejar puntos de partida en el Módulo 1.*
