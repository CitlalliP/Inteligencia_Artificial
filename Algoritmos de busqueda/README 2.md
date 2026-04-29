

## Problema 1

## Enunciado

Dado un nodo raíz con 6 instancias de clase «Sí» y 4 instancias de clase «No» (N = 10), calcula la entropía de Shannon H(S) del nodo y explica su interpretación.

## Solución

### ① Sumamos el total de instancias

* Clase Sí: 6
* Clase No: 4
* Total (N): 10

Probabilidades:

```text
P(Sí) = 6/10 = 0.6
P(No) = 4/10 = 0.4
```

### ② Fórmula de entropía

```text
H(S) = − Σ Pi · log2(Pi)
```

Caso binario:

```text
H(S) = −[P(Sí)·log2(P(Sí)) + P(No)·log2(P(No))]
```

### ③ Sustitución

```text
0.6 × log2(0.6) ≈ −0.4422
0.4 × log2(0.4) ≈ −0.5287

H(S) = −(−0.4422 − 0.5287)
H(S) = 0.9709 bits
```

### Interpretación

Como el valor está cerca de 1, el nodo tiene alta impureza.

---

# Problema 2

## Enunciado

Usando el dataset clásico del tiempo (Play Tennis) con 8 casos totales (4 Sí / 4 No) y atributos Clima, Humedad y Viento, construye el árbol ID3 calculando Ganancia de Información.

## Solución

### Entropía inicial

```text
H(S) = 1.0
```

### Fórmula general

```text
IG(S,A) = H(S) − Σ(|Sv| / |S|) · H(Sv)
```

### Ganancias

| Atributo | Ganancia de Información |
| -------- | ----------------------- |
| Clima    | 0.656                   |
| Humedad  | 0.062                   |
| Viento   | 0.049                   |

### Árbol final

```text
Clima
├── Soleado → NO
├── Nublado → SÍ
└── Lluvioso
    └── Viento
        ├── No → SÍ
        └── Sí → NO


```
## 1. Entropía del Conjunto Total $H(S)$

Analizamos la columna objetivo **«Jugar»**.
* **Total de casos:** 8
* **Distribución:** 4 Sí / 4 No (50/50)


Como la distribución es perfecta, la incertidumbre es máxima:
$$H(S) = -[0.5 \cdot \log_2(0.5) + 0.5 \cdot \log_2(0.5)] = 1.0$$

---

## 2. Ganancia de Información (IG)

La fórmula para calcular la ganancia al dividir por un atributo $A$ es:
$$IG(S, A) = H(S) - \sum \frac{|S_v|}{|S|} \cdot H(S_v)$$

---

## 3. Cálculo de IG para cada Atributo

### a) Clima
* **Soleado (3 casos):** 0 Sí, 3 No $\rightarrow H = 0$
* **Nublado (2 casos):** 2 Sí, 0 No $\rightarrow H = 0$
* **Lluvioso (3 casos):** 2 Sí, 1 No $\rightarrow H = -[\frac{2}{3}\log_2(\frac{2}{3}) + \frac{1}{3}\log_2(\frac{1}{3})] \approx 0.918$

**Entropía Residual (Clima):** $\frac{3}{8}(0) + \frac{2}{8}(0) + \frac{3}{8}(0.918) \approx 0.344$
**IG(Clima):** $1 - 0.344 = \mathbf{0.656}$

### b) Humedad
* **Alta (3 casos):** $H \approx 0.918$
* **Media (2 casos):** $H = 1$
* **Baja (3 casos):** $H \approx 0.918$

**Entropía Residual (Humedad):** $\frac{3}{8}(0.918) + \frac{2}{8}(1) + \frac{3}{8}(0.918) \approx 0.938$
**IG(Humedad):** $1 - 0.938 = \mathbf{0.062}$

### c) Viento
* **No (5 casos):** $H \approx 0.971$
* **Sí (3 casos):** $H \approx 0.918$

**Entropía Residual (Viento):** $\frac{5}{8}(0.971) + \frac{3}{8}(0.918) \approx 0.951$
**IG(Viento):** $1 - 0.951 = \mathbf{0.049}$

---

## 4. Selección del Nodo Raíz

Comparamos las ganancias:
1.  **Clima:** 0.656 (Ganador)
2.  **Humedad:** 0.062
3.  **Viento:** 0.049

El **nodo raíz** del árbol es **Clima**.

---

## 5. División y Refinamiento

Al dividir por **Clima**, observamos los subconjuntos:
* **Si Clima = Soleado:** Todos los casos son «No» $\rightarrow$ **Hoja pura**.
* **Si Clima = Nublado:** Todos los casos son «Sí» $\rightarrow$ **Hoja pura**.
* **Si Clima = Lluvioso:** Subconjunto mixto {Sí, Sí, No}. Se debe repetir el cálculo para Humedad y Viento en esta rama.

### Análisis para Clima = Lluvioso:
Observando los datos específicos:
* Lluvioso + Viento No $\rightarrow$ **Sí**
* Lluvioso + Viento No $\rightarrow$ **Sí**
* Lluvioso + Viento Sí $\rightarrow$ **No**

**Conclusión:** En la rama de clima lluvioso, el **Viento** separa perfectamente los datos. Sin viento se juega; con viento no se juega.
---

# Problema 3

## Enunciado

Random Forest produce predicciones:

```text
[1, 0, 1, 1, 0]
```

¿Cuál es la predicción final?

## Solución

Conteo:

| Clase | Votos |
| ----- | ----- |
| 1     | 3     |
| 0     | 2     |

Resultado:

```text
Predicción final = Clase 1
```

---

# Problema 4

## Enunciado

Explica overfitting en árboles profundos y cómo Random Forest lo reduce.

## Solución

### Overfitting

Un árbol de profundidad 20 memoriza el dataset y pierde generalización.

### Random Forest

* Bagging
* Feature Randomness

### Sin aleatoriedad

Todos los árboles serían idénticos.

---

# Problema 5

## Enunciado

Gradient Boosting con:

```text
y = [10,12,11,13,15]
ŷ = 10
η = 0.1
```

## Solución

### Residuos

```text
Residuo = y − ŷ
```

| y  | Predicción | Residuo |
| -- | ---------- | ------- |
| 10 | 10         | 0       |
| 12 | 10         | 2       |
| 11 | 10         | 1       |
| 13 | 10         | 3       |
| 15 | 10         | 5       |

### Actualización

```text
ŷ_nueva = ŷ_inicial + η × predicción_residuo
```

Ejemplo:

```text
10 + (0.1 × 2) = 10.2
```

---

# Problema 6

## Enunciado

Comparar Random Forest y Gradient Boosting.

## Tabla comparativa

| Característica    | Random Forest    | Gradient Boosting |
| ----------------- | ---------------- | ----------------- |
| Construcción      | Paralelo         | Secuencial        |
| Objetivo          | Reducir varianza | Reducir sesgo     |
| Sensibilidad      | Robusto          | Sensible          |
| Interpretabilidad | Media            | Baja              |

---

# Problema 7

## Enunciado

Aplicar K-Means con:

* A(1,1)
* B(2,2)
* C(8,8)
* D(9,9)

Centroides iniciales:

* C1 = (1,1)
* C2 = (9,9)

## Solución

### Clústeres

| Punto  | Clúster |
| ------ | ------- |
| A(1,1) | 1       |
| B(2,2) | 1       |
| C(8,8) | 2       |
| D(9,9) | 2       |

### Nuevos centroides

```text
C1 = (1.5,1.5)
C2 = (8.5,8.5)
```

---

# Problema 8

## Enunciado

Explicar efecto de elegir K pequeño o grande y aplicar método del codo.

## Tabla de inercia

| K | Inercia |
| - | ------- |
| 1 | 500     |
| 2 | 250     |
| 3 | 100     |
| 4 | 85      |
| 5 | 75      |

### Resultado

```text
K óptimo = 3
```

---

# Problema 9

## Enunciado

Aplicar DBSCAN con:

* eps = 2
* minPts = 3

Puntos:

* A(1,1)
* B(2,1)
* C(2,2)
* D(8,8)

## Resultado

| Punto  | Clasificación |
| ------ | ------------- |
| A(1,1) | Núcleo        |
| B(2,1) | Núcleo        |
| C(2,2) | Núcleo        |
| D(8,8) | Ruido         |

---

# Problema 10

## Enunciado

Dataset:

```text
{10, 12, 11, 13, 100}
```

Detectar outlier usando Z-Score e Isolation Forest.

## Solución

### Estadísticas

| Métrica             | Valor   |
| ------------------- | ------- |
| Media               | 29.2    |
| Varianza            | 1254.16 |
| Desviación estándar | 35.41   |
| Z-score(100)        | 1.99    |

### Interpretación

El valor 100 es un outlier debido a que se encuentra muy separado del resto.

### Isolation Forest

* Profundidad corta → anomalía
* Profundidad larga → dato normal
