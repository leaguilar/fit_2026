# Hands-On AI · FIT 2026

Taller práctico de 3.5 horas: del gradient descent a las propiedades
emergentes de los modelos de lenguaje.

Dr. Leonel Aguilar · ETH Zürich

Todo se ejecuta en **Google Colab**. No hace falta instalar nada ni saber
programar. Solo un navegador y una cuenta de Google.

---

## Los notebooks

Abre cada uno con su botón. Se ejecutan en orden.

| | Notebook | Qué construimos | Duración |
|---|---|---|---|
| 0 | [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/leaguilar/fit_2026/blob/main/notebooks/0_fundamentos_gradient_descent.ipynb) [`0_fundamentos_gradient_descent`](notebooks/0_fundamentos_gradient_descent.ipynb) | Gradient descent, el mapa de niveles y el *learning rate* | 30 min |
| 1 | [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/leaguilar/fit_2026/blob/main/notebooks/1_redes_neuronales_backpropagation.ipynb) [`1_redes_neuronales_backpropagation`](notebooks/1_redes_neuronales_backpropagation.ipynb) | Backpropagation en 25 líneas de numpy, y la red como interpolador | 35 min |
| 2 | [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/leaguilar/fit_2026/blob/main/notebooks/2_reinforcement_learning_q_learning.ipynb) [`2_reinforcement_learning_q_learning`](notebooks/2_reinforcement_learning_q_learning.ipynb) | Q-table a mano, Q-learning, y deep Q-learning cuando la tabla se rompe | 45 min |
| 3 | [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/leaguilar/fit_2026/blob/main/notebooks/3_modelos_de_lenguaje.ipynb) [`3_modelos_de_lenguaje`](notebooks/3_modelos_de_lenguaje.ipynb) | Eliza, bigramas, una red de lenguaje entrenada en vivo, y un LLM real | 40 min |
| 4 | [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/leaguilar/fit_2026/blob/main/notebooks/4_propiedades_emergentes_cot_rag.ipynb) [`4_propiedades_emergentes_cot_rag`](notebooks/4_propiedades_emergentes_cot_rag.ipynb) | Few-shot, chain-of-thought medido, y RAG | 30 min |

**Hoja de trabajo:** [`handout/hoja_de_trabajo.pdf`](handout/hoja_de_trabajo.pdf).
Dos páginas (una hoja a doble cara), para llenar con lápiz. Se usa en los
notebooks 2 y 3. Las figuras las genera `slides/figuras/construir_figuras.py`.

---

## La idea del taller

Hacemos el mismo recorrido tres veces:

| | Primero una tabla | Después una red |
|---|---|---|
| **Decidir** | Q-table de 5×3 | deep Q-learning |
| **Escribir** | tabla de bigramas | red de lenguaje |
| **Siempre** | se rompe al crecer | interpola y generaliza |

Y debajo de todo, siempre lo mismo: medir el error y bajar la colina (gradient descent).

Cada bloque sigue el mismo patrón: un poco de teoría, un ejercicio **a mano**,
y después el mismo ejercicio en código.

Hay tres celdas marcadas `TODO` en todo el taller. Son de dos o tres líneas,
y cada una tiene su solución justo debajo.

---

## Antes de empezar

1. Abre el notebook 0 con el botón de arriba.
2. Ejecuta la primera celda. Si imprime `Listo`, ya está todo.
3. Para los notebooks 3 y 4 conviene activar la GPU:
   *Entorno de ejecución → Cambiar tipo de entorno → T4 GPU*.
   Sin GPU también funcionan, solo tardan más.

En el notebook 3, **ejecuta la primera celda en cuanto lo abras**: empieza a
descargar el modelo en segundo plano mientras trabajas en las otras partes.

---

## Fuera de Colab

```bash
git clone https://github.com/leaguilar/fit_2026.git
cd fit_2026
pip install -r requirements.txt
jupyter lab notebooks/
```

Los notebooks buscan `datos/quijote_fragmento.txt` en el repositorio. Si no lo
encuentran, lo descargan.

**Modelos.** El notebook 3 y el 4 usan `Qwen/Qwen3-0.6B` por defecto (unos
1.5 GB). En la celda de setup hay dos líneas comentadas para cambiarlo por uno
más pequeño (`Qwen2.5-0.5B-Instruct`) o más grande (`Qwen3-1.7B`, necesita GPU).

---

## Qué hay en cada carpeta

```
notebooks/   los cinco notebooks del taller
datos/       el fragmento del Quijote que entrena el modelo de lenguaje
handout/     la hoja de trabajo (LaTeX y PDF)
requirements.txt
```

---

## Licencia y créditos

El fragmento del Quijote viene de [Project Gutenberg](https://www.gutenberg.org/ebooks/2000)
y es de dominio público.

Artículos originales de lo que se ve en el taller:

- Bellman (1957), *A Markovian decision process*
- Mnih et al. (2015), *Human-level control through deep reinforcement learning*, Nature 518
- Wei et al. (2022), *Chain-of-thought prompting elicits reasoning in large language models*, arXiv:2201.11903
- Lewis et al. (2020), *Retrieval-augmented generation for knowledge-intensive NLP tasks*, arXiv:2005.11401
