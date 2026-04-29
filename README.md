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

## Ejercicio 7: SVM con Kernel

**Enunciado completo:**

Un dataset NO es linealmente separable.

Preguntas conceptuales:

1. ¿Por qué falla un SVM lineal?
2. ¿Por qué usar un kernel?
3. En un ejemplo con datos en forma de círculo, explicar cómo el kernel RBF soluciona el problema.
4. Dar un ejemplo real.

---

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
