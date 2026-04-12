# 📈 GráficoBase – Visualizador de Activos Financieros

Herramienta de visualización técnica para activos financieros usando datos de Yahoo Finance. Genera gráficos de precio con indicadores técnicos (SMA, EMA, RSI) en un estilo oscuro y minimalista.

---

## 📊 ¿Qué hace este proyecto?

Con una sola línea de código, podés generar un gráfico profesional de cualquier activo disponible en Yahoo Finance (acciones, ETFs, criptomonedas, índices) que incluye:

- Precio de cierre histórico
- Medias móviles simples (SMA) y exponenciales (EMA) configurables
- Índice de Fuerza Relativa (RSI)
- Escala lineal o logarítmica
- Diseño oscuro con marca de agua

![image alt](https://github.com/hijjuani/my-chart/blob/a35c68cb05bb889d97ae793017c4d81d3e249093/Chart%20Example.png)

```python
plot = GráficoBase(ticker='SPY', period='3y', sma_period=[100], ema_period=[20, 200], scale='linear')
plot.mostrar()
```

---

## 🧠 Teoría: Indicadores Técnicos

### Precio de cierre

El precio de cierre es el valor del activo al final de la sesión de mercado. Es la referencia más usada en análisis técnico porque refleja el consenso final del mercado en cada jornada.

---

### Media Móvil Simple (SMA)

La **SMA** (*Simple Moving Average*) promedia los últimos `n` precios de cierre con igual ponderación:

```
SMA(n) = (P₁ + P₂ + ... + Pₙ) / n
```

- Suaviza el ruido del precio y revela la tendencia subyacente.
- Períodos cortos (ej. SMA 20) son más reactivos; períodos largos (ej. SMA 200) indican tendencia estructural.
- Un cruce del precio por encima de la SMA 200 suele interpretarse como señal alcista (*golden cross*).

---

### Media Móvil Exponencial (EMA)

La **EMA** (*Exponential Moving Average*) pondera más los precios recientes, usando una fórmula recursiva:

```
EMA(t) = Precio(t) × k + EMA(t-1) × (1 - k)
         donde k = 2 / (n + 1)
```

- Reacciona más rápido que la SMA ante cambios de precio.
- Muy usada en estrategias de momentum y cruces de medias (ej. EMA 20 sobre EMA 200).

---

### Índice de Fuerza Relativa (RSI)

El **RSI** (*Relative Strength Index*) es un oscilador que mide la velocidad y magnitud de los movimientos de precio, acotado entre 0 y 100:

```
RSI = 100 - (100 / (1 + RS))
      donde RS = Promedio de ganancias / Promedio de pérdidas  (en n períodos)
```

- **RSI > 70:** zona de sobrecompra → posible corrección.
- **RSI < 30:** zona de sobreventa → posible rebote.
- El período estándar es 14 sesiones (valor por defecto).

---

### Escala logarítmica

Para activos con grandes variaciones históricas de precio (criptomonedas, acciones de alto crecimiento), la escala logarítmica es preferible a la lineal porque representa variaciones **porcentuales** iguales como distancias visuales iguales, facilitando la comparación entre distintos períodos del histórico.

---

## 🗂️ Estructura del proyecto

```
grafico-base/
│
├── grafico_base.py      # Clase principal con toda la lógica
├── requirements.txt
└── README.md
```

---

## ⚙️ Instalación

### Requisitos

- Python 3.11+

```bash
pip install -r requirements.txt
```

---

## ▶️ Uso

```python
from grafico_base import GráficoBase

# Ejemplo básico
plot = GráficoBase(ticker='AAPL', period='1y')
plot.mostrar()

# Con indicadores
plot = GráficoBase(
    ticker='BTC-USD',
    period='2y',
    sma_period=[50, 200],
    ema_period=[20],
    rsi_period=14,
    scale='log'
)
plot.mostrar()
```

### Parámetros

| Parámetro    | Tipo         | Default      | Descripción                                              |
|--------------|--------------|--------------|----------------------------------------------------------|
| `ticker`     | `str`        | requerido    | Símbolo del activo (ej. `'SPY'`, `'BTC-USD'`, `'GGAL'`) |
| `period`     | `str`        | `'2y'`       | Período histórico: `'1y'`, `'2y'`, `'5y'`, `'max'`, etc.|
| `sma_period` | `list[int]`  | `[]`         | Períodos para SMA (ej. `[50, 200]`)                      |
| `ema_period` | `list[int]`  | `[]`         | Períodos para EMA (ej. `[20, 200]`)                      |
| `rsi_period` | `int`        | `14`         | Período para el cálculo del RSI                          |
| `scale`      | `str`        | `'linear'`   | Escala del eje Y: `'linear'` o `'log'`                   |

---

## 📚 Referencias

- Wilder, J. W. (1978). *New Concepts in Technical Trading Systems.* Trend Research.
- Murphy, J. J. (1999). *Technical Analysis of the Financial Markets.* New York Institute of Finance.
- [Yahoo Finance API – yfinance](https://github.com/ranaroussi/yfinance)

---

## 📝 Licencia

MIT License. Libre para usar, modificar y distribuir.
