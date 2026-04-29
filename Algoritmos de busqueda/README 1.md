# Inteligencia_Artificial

# Problema 1 — Matriz de Confusión + Métricas

## Descripción del problema
Se tiene el siguiente resultado de un clasificador binario: TP = 50, FP = 10, FN = 5, TN = 35.

Preguntas:

Construir la matriz de confusión.
Calcular Accuracy, Precision, Recall y F1-score.
Discusión: ¿Qué métrica es más importante si es detección de enfermedad?

Construcción y análisis de métricas de evaluación para un clasificador binario usando una matriz de confusión.

Objetivo: comprender cómo interpretar Accuracy, Precision, Recall y F1-score dentro de un contexto de clasificación.

---

# 1. Matriz de Confusión + Métricas

## Ejercicio 1: Construcción básica

Se tiene el siguiente resultado de un clasificador binario:

* TP = 50
* FP = 10
* FN = 5
* TN = 35

### Preguntas

1. Construir la matriz de confusión.
2. Calcular Accuracy, Precision, Recall y F1-score.
3. Discusión: ¿Qué métrica es más importante si es detección de enfermedad?

### Matriz de confusión

| Clase real / Predicción | Predicción positiva (+) | Predicción negativa (−) |
| ----------------------- | ----------------------- | ----------------------- |
| Clase real positiva     | TP = 50                 | FN = 5                  |
| Clase real negativa     | FP = 10                 | TN = 35                 |

### Cálculo de métricas

#### Accuracy (Exactitud)

```text
Accuracy = (TP + TN) / (TP + TN + FP + FN)
Accuracy = (50 + 35) / 100
Accuracy = 0.85 = 85%
```

#### Precisión

```text
Precisión = TP / (TP + FP)
Precisión = 50 / (50 + 10)
Precisión = 50 / 60 = 0.833 ≈ 83.3%
```

#### Recall (Sensibilidad)

```text
Recall = TP / (TP + FN)
Recall = 50 / (50 + 5)
Recall = 50 / 55 = 0.9091 ≈ 90.9%
```

#### F1-Score

```text
F1 = 2·(Precisión × Recall) / (Precisión + Recall)
F1 = 2·(0.833)(0.909) / (0.833 + 0.909)
F1 = 0.869 ≈ 86.9%
```

### Discusión

¿Qué métrica es más importante en detección de enfermedad?

En un contexto médico la métrica más importante suele ser el Recall (Sensibilidad). Un Falso Negativo (FN) significa decirle a una persona enferma que está sana. Esto es crítico porque el paciente no recibiría tratamiento, poniendo en riesgo su vida.

Preferimos tener algunos Falsos Positivos (que se envíen a pruebas confirmatorias adicionales) que dejar pasar un solo caso positivo real.

Aunque el Recall es prioritario para no perder enfermos, siempre se debe vigilar que la Precisión no sea excesivamente baja.

---

# Problema 2 — Métricas con Desbalance de Clases

## Descripción del problema
Se tiene el siguiente dataset médico desbalanceado (solo 5 % de casos positivos).

Preguntas:

¿Accuracy es una buena métrica aquí?
Calcula Recall y Precisión.
¿Qué métrica priorizarías y por qué?
¿Es un buen modelo?

Análisis de un dataset médico desbalanceado donde la clase positiva representa un porcentaje pequeño del total.

Objetivo: evaluar por qué Accuracy puede ser engañosa y determinar qué métricas son más relevantes.

---

# 2. Métricas con Desbalance de Clases

## Ejercicio 2: Dataset médico – detección de enfermedad (solo 5 % positivos)

Se tiene el siguiente dataset médico desbalanceado (solo 5 % de casos positivos).

### Preguntas

1. ¿Accuracy es una buena métrica aquí?
2. Calcula Recall y Precisión.
3. ¿Qué métrica priorizarías y por qué?
4. ¿Es un buen modelo?

---

# Página 2

### Matriz del dataset

| Clase real / Predicción | Predicción: Sí | Predicción: No |
| ----------------------- | -------------- | -------------- |
| Real: Sí                | 8              | 2              |
| Real: No                | 90             | 900            |

### ¿El Accuracy es una buena métrica aquí?

No. En datasets desbalanceados el Accuracy es engañoso.

```text
Accuracy = (8 + 900) / 1000
Accuracy = 0.908 = 90.8%
```

A primera vista parece excelente; sin embargo, un modelo que siempre prediga “No está enfermo” tendría un Accuracy cercano al 99 % en este dataset.

El 90.8 % es peor que simplemente seguir la clase mayoritaria.

### Cálculo de Recall y Precisión

```text
TP = 8
FN = 2
FP = 90
TN = 900
```

#### Recall

```text
Recall = TP / (TP + FN)
Recall = 8 / (8 + 2)
Recall = 8 / 10 = 0.80 = 80%
```

#### Precisión

```text
Precisión = TP / (TP + FP)
Precisión = 8 / (8 + 90)
Precisión = 8 / 98 = 0.081 = 8.1%
```

### ¿Qué métrica priorizarías y por qué?

En medicina sigue siendo importante priorizar Recall.

Con Recall = 80 %, se pierde al 20 % de los enfermos reales.

Sin embargo, con una Precisión de 8.1 %, la mayoría de los positivos detectados serían falsos positivos.

Esto podría causar:

* Angustia innecesaria
* Saturación hospitalaria
* Costos diagnósticos elevados

### ¿Es un buen modelo?

No.

Razones:

1. Baja precisión.
2. Recall insuficiente.
3. Demasiados falsos positivos.
4. Coste operativo elevado.

Un modelo útil debería aspirar a Recall del 95–99 % sin destruir la Precisión.

---

# Problema 3 — Error en Regresión (MSE vs MAE)

## Descripción del problema
Se tienen las siguientes predicciones de precios:

Real = 100 / Pred = 90
Real = 200 / Pred = 210
Real = 300 / Pred = 1000
Calcular:

MAE.
MSE.
¿Cuál penaliza más errores grandes?

Comparación entre métricas de error utilizadas en regresión para evaluar predicciones numéricas.

Objetivo: analizar cómo MAE y MSE reaccionan frente a errores extremos.

---

# 3. Error en Regresión (MSE vs MAE)

## Ejercicio 3: Predicciones de precios

Se tienen las siguientes predicciones:

* Real = 100 / Pred = 90
* Real = 200 / Pred = 210
* Real = 300 / Pred = 1000

### Tabla de errores

| Valor real | Predicción | Error absoluto     | Error cuadrático |
| ---------- | ---------- | ------------------ | ---------------- |
| 100        | 90         | |100 − 90| = 10    | 10² = 100        |
| 200        | 210        | |200 − 210| = 10   | 10² = 100        |
| 300        | 1000       | |300 − 1000| = 700 | 700² = 490000    |

### MAE (Mean Absolute Error)

```text
MAE = (10 + 10 + 700) / 3
MAE = 720 / 3
MAE = 240
```

### MSE (Mean Squared Error)

```text
MSE = (100 + 100 + 490000) / 3
MSE = 490200 / 3
MSE = 163400
```

### ¿Cuál penaliza más los errores grandes?

El MSE penaliza mucho más los errores grandes porque eleva los errores al cuadrado.

Esto provoca que un error extremo tenga un impacto desproporcionadamente alto en el promedio.

---


## Ejercicio 4: Interpretación de coeficientes

**Enunciado completo:**

Dado el modelo de regresión lineal:

```text
y = 5 + 2·x₁ − 3·x₂
```

Preguntas:

1. Interpretar cada coeficiente.
2. ¿Qué pasa si x₂ aumenta?

---
# Interpretación del Modelo de Regresión

## 1. Interpretación de cada coeficiente

* **Intersección ($b_0 = 5$):** Es el valor esperado de $y$ cuando tanto $x_1$ como $x_2$ son iguales a $0$. Representa el punto de partida o el nivel base del modelo.

* **Coeficiente $x_1$ ($w_1 = 2$):** Indica una **relación positiva**. La variable objetivo $y$ aumentará en $2$ unidades por cada unidad que aumente $x_1$, siempre que $x_2$ se mantenga constante.

* **Coeficiente $x_2$ ($w_2 = -3$):** Indica una **relación negativa**. La variable objetivo $y$ disminuirá en $3$ unidades por cada unidad que aumente $x_2$, siempre que $x_1$ se mantenga constante.

---

## 2. Dinámica de Cambio

### ¿Qué pasa si $x_2$ aumenta?
Si $x_2$ aumenta, el valor de $y$ **disminuye**. En este modelo, $x_2$ tiene un impacto o "fuerza" mayor que $x_1$ en el resultado final (magnitud de 3 frente a 2), pero actúa en sentido opuesto. El signo negativo funciona como un penalizador.

### Analogía en un escenario real
Si la variable **$y$** representara la **Satisfacción del Cliente**:
* **$x_1$** podría ser la **Calidad del Producto** (impacto positivo).
* **$x_2$** podría ser el **Tiempo de Espera** (impacto negativo).

## Ejercicio 5: Modelo sigmoide

**Enunciado completo:**

Dado el modelo de regresión logística:

```text
P(y=1|x) = 1 / (1 + e^(-(2x-4)))
```

Preguntas:

1. ¿Qué pasa cuando x = 2?
2. ¿Cuál es el umbral de decisión?
3. ¿Qué significa el coeficiente 2?

---

# Análisis de la Función Sigmoide y Umbral de Decisión

## 1. ¿Qué pasa cuando $x = 2$?

Al sustituir el valor de $x = 2$ en la función, observamos lo siguiente:

* **Cálculo del exponente:** $2(2) - 4 = 4 - 4 = 0$.
* **Cálculo de la probabilidad:**
    $$P = rac{1}{1 + e^0} = rac{1}{1 + 1} = rac{1}{2} = 0.5 = 50\%$$

**Conclusión:** Cuando $x = 2$, la probabilidad de que la clase sea positiva es exactamente del **50%**. Este es el punto de indiferencia o frontera del modelo.

---

## 2. ¿Cuál es el umbral de decisión?

El umbral de decisión estándar es **0.5**. En este modelo específico, el umbral en términos de la variable de entrada $x$ se sitúa en $x = 2$:

* **Si $x > 2$:** La probabilidad será mayor a $0.5 
ightarrow$ el modelo predice la **Clase 1**.
* **Si $x < 2$:** La probabilidad será menor a $0.5 
ightarrow$ el modelo predice la **Clase 0**.

---

## 3. Interpretación de los Parámetros

### El Coeficiente ($w = 2$)
El peso que acompaña a la variable determina la pendiente de la curva:
* **Relación:** Al ser un valor positivo, indica que a medida que $x$ aumenta, la probabilidad de que $y = 1$ también aumenta.
* **Velocidad de cambio:** Su magnitud nos dice qué tan rápido el modelo "cambia de opinión". Entre más grande sea este número, más radical será el salto en la curva sigmoide, haciendo la transición entre clases más abrupta.

### El Bias o Sesgo ($b = -4$)
Este término desplaza la curva horizontalmente:
* En este caso, desplaza la curva hacia la **derecha**.
* Si el bias fuera $0$, el punto de indecisión ($0.5$) estaría exactamente en $x = 0$.

## Ejercicio 6: Margen máximo

**Enunciado completo:**

Dado un plano con puntos separables:

* Clase +1: (2,2) y (3,3)
* Clase –1: (0,0) y (1,1)

Preguntas:

1. Dibujar los puntos.
2. Proponer una recta separadora.
3. Identificar los vectores de soporte (intuitivo).

---
# Análisis de Separabilidad y SVM (Máquinas de Vector de Soporte)

## 1. Gráfica de Puntos y Distribución

En este conjunto de datos, todos los puntos yacen sobre la diagonal $y = x$. Se distribuyen de la siguiente manera:

* **Clase -1:** Se encuentra en los puntos $(0,0)$ y $(1,1)$.
* **Clase +1:** Se encuentra en los puntos $(2,2)$ y $(3,3)$.

**Observación:** Los datos son perfectamente separables por una recta perpendicular a la diagonal que pase por el espacio entre $(1,1)$ y $(2,2)$.

---

## 2. Recta Separadora

Una recta que separa intuitivamente estas clases es **$x + y = 3$**.

### Comprobación del modelo:
| Punto $(x, y)$ | Sustitución ($x + y$) | Resultado | Clasificación |
| :--- | :--- | :--- | :--- |
| $(0,0)$ | $0 + 0 = 0$ | $0 < 3$ | Lado $-1$ (Correcto) |
| $(1,1)$ | $1 + 1 = 2$ | $2 < 3$ | Lado $-1$ (Correcto) |
| $(2,2)$ | $2 + 2 = 4$ | $4 > 3$ | Lado $+1$ (Correcto) |
| $(3,3)$ | $3 + 3 = 6$ | $6 > 3$ | Lado $+1$ (Correcto) |

### Cálculo de la bisectriz exacta:
El punto medio entre los puntos más cercanos de ambas clases $(1,1)$ y $(2,2)$ es $(1.5, 1.5)$. La recta con pendiente $-1$ (perpendicular a la diagonal) que pasa por dicho punto es:
$$y - 1.5 = -(x - 1.5) \implies y = -x + 3 \implies x + y = 3$$

---

## 3. Vectores de Soporte

En un modelo SVM, los **vectores de soporte** son los puntos críticos que definen el margen máximo:

* **Vectores de soporte detectados:** $(1,1)$ y $(2,2)$.
* **Razón:** Son los puntos más cercanos entre las dos clases opuestas.
* **Puntos descartados:** $(0,0)$ y $(3,3)$ no son vectores de soporte porque, al estar más alejados de la frontera $x + y = 3$, no influyen en la definición del margen ni en la posición de la recta separadora.


## Ejercicio 8: Clasificación manual

**Enunciado completo:**

Puntos:

* Clase A: (1,1), (2,2)
* Clase B: (4,4), (5,5)
* Nuevo punto: (3,3)

Preguntas:

1. Clasificar con k = 1.
2. Clasificar con k = 3.
3. ¿Qué cambia?

---

# Análisis de Clasificación K-Nearest Neighbors (k-NN)

## 1. Clasificación con $k = 1$

Para clasificar el punto $(3,3)$, calculamos la distancia euclídea hacia los puntos conocidos más cercanos. Dado que todos los puntos están sobre la diagonal $y = x$, las distancias se calculan de la siguiente forma:

* **Distancia a $(2,2)$ (Clase A):** $\sqrt{(3-2)^2 + (3-2)^2} = \sqrt{1^2 + 1^2} = \sqrt{2} \approx 1.41$
* **Distancia a $(4,4)$ (Clase B):** $\sqrt{(3-4)^2 + (3-4)^2} = \sqrt{(-1)^2 + (-1)^2} = \sqrt{2} \approx 1.41$

**Resultado:** Existe un **empate**. El punto $(3,3)$ se encuentra a la misma distancia mínima de ambas clases. En estos casos, el algoritmo suele decidir al azar o basándose en el orden de aparición de los datos en el dataset.

---

## 2. Clasificación con $k = 3$

Buscamos los tres vecinos más cercanos al punto $(3,3)$:

1.  **$(2,2)$ (Clase A):** Distancia $\approx 1.41$
2.  **$(4,4)$ (Clase B):** Distancia $\approx 1.41$
3.  **$(1,1)$ (Clase A):** Distancia $\sqrt{(3-1)^2 + (3-1)^2} = \sqrt{2^2 + 2^2} = \sqrt{8} \approx 2.83$

### Votación:
* **Votos Clase A:** 2 (puntos $(2,2)$ y $(1,1)$)
* **Votos Clase B:** 1 (punto $(4,4)$)

**Resultado:** La clase ganadora con $k=3$ es la **Clase A**.

---

## 3. ¿Qué cambia entre $k=1$ y $k=3$?

El cambio fundamental reside en la **estabilidad** de la predicción y la **sensibilidad al ruido**:

* **Con $k$ pequeño ($k=1$):** El modelo es extremadamente sensible. Si el punto $(2,2)$ fuera un error de medición (ruido), la predicción cambiaría drásticamente. Esto suele llevar al *overfitting* (sobreajuste).
* **Con $k$ más grande ($k=3$):** La decisión es más "democrática". Al considerar más vecinos, el modelo suaviza la frontera de decisión, siendo menos probable que un solo dato atípico o ruidoso afecte negativamente la clasificación final.

## Ejercicio 9: Escalamiento de variables

**Enunciado completo:**

Dataset con:

* Edad (0–100)
* Ingreso (0–1,000,000)

Preguntas:

1. ¿Qué problema hay en k-NN?
2. ¿Cómo solucionarlo?

Tip: normalización / estandarización.

---

# El Problema de la Escala en k-NN y su Solución

## 1. ¿Qué problema hay en k-NN?

El algoritmo k-NN se basa en el cálculo de la **distancia euclidiana** entre puntos para determinar la similitud. El problema surge cuando las variables tienen escalas muy diferentes (por ejemplo, Edad vs. Ingreso):

$$d = \sqrt{(edad_1 - edad_2)^2 + (ingreso_1 - ingreso_2)^2}$$

### Consecuencias:
* **Dominancia:** La diferencia en el ingreso (que puede ser de millones) domina completamente el resultado de la raíz cuadrada.
* **Pérdida de información:** La variable "Edad" prácticamente no influye en la clasificación, aunque sea relevante.
* **Sesgo:** Los vecinos cercanos se eligen casi exclusivamente por similitud de ingreso, ignorando otras dimensiones del problema.

---

## 2. ¿Cómo solucionarlo?

La solución consiste en **escalar las variables** para que sus magnitudes sean comparables y contribuyan por igual al cálculo de la distancia.

### A) Normalización (Min-Max Scaling)
Lleva los datos a un rango fijo, generalmente $[0, 1]$.
$$x' = \frac{x - \min(X)}{\max(X) - \min(X)}$$
* *Resultado:* Tanto la Edad como el Ingreso quedan transformados al intervalo $[0, 1]$, permitiendo que ambos pesen lo mismo en la fórmula de distancia.

### B) Estandarización (Z-score Scaling)
Transforma los datos para que tengan una media $\mu = 0$ y una desviación estándar $\sigma = 1$.
$$x' = \frac{x - \mu}{\sigma}$$
* *Ventaja:* Es más robusta frente a valores atípicos (*outliers*) que la normalización.

## Ejercicio 10: Clasificación probabilística

**Enunciado completo:**

Dado el siguiente dataset con probabilidades condicionales:

* Spam: P(A)=0.6, P(B)=0.7
* No Spam: P(A)=0.2, P(B)=0.3

Prior:

* P(Spam)=0.4
* P(No Spam)=0.6

Nuevo correo contiene A y B.

Calcular:

1. P(Spam|datos)
2. P(No Spam|datos)
3. Clasificar
4. ¿La independencia es real?

# Clasificador Naive Bayes: Detección de Spam

## 1. Cálculo de Probabilidades Posteriores

Para clasificar si un correo es Spam basándonos en las características $A$ y $B$, calculamos las probabilidades proporcionales ($\propto$):

### P(Spam | datos)
* **Datos:** $P(A|Spam) = 0.6$, $P(B|Spam) = 0.7$, $P(Spam) = 0.4$
* **Cálculo:** $P(Spam|datos) \propto 0.6 \times 0.7 \times 0.4 = 0.168$

### P(No Spam | datos)
* **Datos:** $P(A|No \ Spam) = 0.2$, $P(B|No \ Spam) = 0.3$, $P(No \ Spam) = 0.6$
* **Cálculo:** $P(No \ Spam|datos) \propto 0.2 \times 0.3 \times 0.6 = 0.036$

---

## 2. Clasificación Final

Comparamos ambos resultados y clasificamos según el valor mayor:
$$0.168 > 0.036$$

**Resultado:** El correo es clasificado como **SPAM**.

### Normalización (Cálculo de probabilidad real)
Para obtener el porcentaje exacto:
* **P(Spam|datos):** $\frac{0.168}{0.168 + 0.036} = \frac{0.168}{0.204} \approx 82.4\%$
* **P(No Spam|datos):** $\approx 17.6\%$

---

## 3. El supuesto de Independencia

### ¿La independencia es real?
**No.** En el mundo real, casi nunca existe una independencia absoluta entre las características.

### ¿Por qué se llama "Naive" (Ingenuo)?
Se le llama así porque **asume que las palabras o características no tienen relación entre sí**, lo cual es generalmente falso. Por ejemplo, en un correo real, las palabras *"oferta"* y *"gratis"* suelen aparecer juntas con frecuencia.

A pesar de esta simplificación "ingenua", el algoritmo funciona sorprendentemente bien en la práctica, especialmente para la clasificación de texto y filtrado de correo no deseado.
