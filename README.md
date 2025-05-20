# 🌱 Interpolación del crecimiento de la planta

**Materia:** Análisis Numérico  
**Integrantes:**
- Rudy Luis Mamani Choque  
- Fabricio Emanuel Martínez Condorena  
- Alvin Akin Mamani Maldonado  
- Gabriel Romero Dueñas  

Este proyecto presenta una comparación entre distintos métodos de interpolación polinomial, aplicados al crecimiento de especies vegetales como **Eugenia stipitata** e **Inga spectabilis**.


Se estima la **altura de la planta en el día 170**, usando:

- 📌 Interpolación de Newton  
- 📌 Interpolación de Lagrange  
- 📌 Interpolación por Splines cúbicos  
- 📌 Regresión Polinomial

---

## 📊 Datos utilizados

| Día | Altura (cm) |
|-----|-------------|
| 30  | 16          |
| 60  | 22          |
| 90  | 28          |
| 120 | 34          |
| 150 | 40          |
| 180 | 45          |
| 210 | 50          |
| 240 | 54          |
| 270 | 58          |
| 300 | 59.5        |
| 320 | 59.15       |

---

## 1️⃣ Interpolación por Newton

### 🧠 Descripción

El método de Newton se basa en **diferencias divididas**. Se construye un polinomio progresivo que va sumando términos basados en el cambio entre valores sucesivos. Es eficiente si deseas añadir nuevos puntos sin recalcular todo desde cero.

### 📐 Fórmula general

\[
P(x) = a_0 + a_1(x - x_0) + a_2(x - x_0)(x - x_1) + \dots
\]

### 📸 Resultado en Excel

![Interpolación de Newton](./Screenshot%202025-04-20%20001113.png)

### 📈 Resultado

> **Altura estimada para el día 170:** `22.1612 cm`  
> *(Nota: este cálculo fue hecho con una tabla diferente que inicia en 10 cm)*

---

## 2️⃣ Interpolación por Lagrange

### 🧠 Descripción

El polinomio de Lagrange utiliza todos los puntos para construir la siguiente expresión:

\[
P(x) = \sum_{i=0}^{n} y_i \cdot L_i(x)
\quad\text{donde}\quad
L_i(x) = \prod_{j=0, j \ne i}^{n} \frac{x - x_j}{x_i - x_j}
\]

Este método asegura que el polinomio pase exactamente por todos los puntos.

### 📸 Resultado en Excel

![Interpolación de Lagrange](./Screenshot%202025-04-20%20001128.png)

### 📈 Resultado

> **Altura estimada para el día 170:** `43.55 cm`

---

## 3️⃣ Interpolación por Splines cúbicos

### 🧠 Descripción

Divide los datos en intervalos, y en cada uno construye un polinomio cúbico que garantiza suavidad (continuidad en las derivadas primera y segunda).

\[
S_i(x) = a_i + b_i(x - x_i) + c_i(x - x_i)^2 + d_i(x - x_i)^3
\]

En el spline **natural**, se cumple que \(c_0 = 0\) y \(c_n = 0\).

### 📘 Pasos clave

1. Calcular diferencias \( h_i \)
2. Construir sistema lineal \(A \cdot \vec{c} = \vec{b'}\)
3. Resolver para \(c_i\), luego obtener \(b_i\) y \(d_i\)
4. Evaluar el spline correspondiente según el intervalo

### 📸 Resultado en Excel

![Interpolación por Splines](./Screenshot%202025-04-20%20001151.png)

### 📈 Resultado

> **Altura estimada para el día 170:** `43.3918 cm`

---

## 4️⃣ Regresión Polinomial

### 🧠 Descripción

Ajusta un polinomio de grado \(n\) (en este caso grado 4) a los datos, **minimizando el error cuadrático** (Mínimos Cuadrados). No pasa exactamente por todos los puntos, pero se adapta suavemente al comportamiento general.

\[
y = a_0 + a_1x + a_2x^2 + a_3x^3 + a_4x^4
\]

Se implementó en Excel usando:

- Columnas con \(x, x^2, x^3, x^4\)
- `ESTIMACION.LINEAL` (o `LINEST` en inglés) para obtener los coeficientes
- Evaluación del polinomio en \(x = 170\)

### 📸 Resultado en Excel

![Regresión Polinomial](./Screenshot%202025-04-20%20001205.png)

### 📈 Resultado

> **Altura estimada para el día 170:** `43.2985 cm`

---

## 📊 Comparación general

| Método       | Estimación (día 170) |
|--------------|----------------------|
| Newton       | 22.1612 cm           |
| Lagrange     | 43.55 cm             |
| Spline       | 43.3918 cm           |
| Regresión    | 43.2985 cm           |

✅ Newton usó una tabla distinta, por eso su valor varía bastante.  
Los otros métodos convergen a valores cercanos, lo cual valida su robustez.

---

## 🗂 Estructura del proyecto

