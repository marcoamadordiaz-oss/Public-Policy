# Determinantes de la Disponibilidad Hídrica en Cuencas Mexicanas

## Descripción
Análisis de regresión OLS sobre 720 cuencas hidrológicas mexicanas para identificar
los factores que determinan la disponibilidad de agua superficial, usando datos
abiertos de CONAGUA (SINA).

## Pregunta de investigación
¿Qué factores del balance hídrico explican la disponibilidad de agua
en las cuencas mexicanas?

## Datos
- **Fuente:** CONAGUA — Sistema Nacional de Información del Agua (SINA)
- **Unidad de análisis:** Cuenca hidrológica (n = 720)
- **Variable dependiente:** ln(Disponibilidad hídrica) — transformación
  logarítmica para corregir sesgo en la distribución original

## Especificación del modelo
ln(D) = β₀ + β₁ln(Ab) + β₂ln(Uc_a) + β₃Rxy + β₄ln(Ev) + β₅(Dummies RH) + ε

| Variable | Descripción |
|---|---|
| ln(Ab) | Log del volumen concesionado |
| ln(Uc_a) | Log del uso agrícola |
| Rxy | Escurrimiento natural |
| ln(Ev) | Log de evaporación |
| Dummies RH | Efectos fijos por región hidrológica (36 regiones) |

## Proceso metodológico
1. Exploración y limpieza: detección de sesgo extremo en Y → transformación log
2. Modelo OLS inicial → VIF alto (17.4) entre escurrimiento y concesionado
3. Corrección de multicolinealidad: eliminación de log_escurrimiento (VIF < 4)
4. Diagnóstico de heterocedasticidad → corrección con errores robustos HC3
5. Modelo final con HC3

## Resultados principales
- **R² ajustado = 0.716** — el modelo explica el 71.6% de la variación
- **log_concesionado** (β = 0.718, p < 0.001) — único predictor continuo
  significativo: un 1% de aumento en el volumen concesionado se asocia
  con un 0.72% de aumento en disponibilidad
- **Efectos regionales fuertes:** RH_18 (Baja California, β = −7.09) y
  RH_12 (Lerma-Santiago, β = −3.15) muestran déficit estructural severo.
  RH_29 (Usumacinta, β = +1.46) y RH_27 (β = +1.45) concentran
  la mayor disponibilidad

## Limitaciones
- Heterocedasticidad estructural por heterogeneidad entre cuencas
  pequeñas y grandes (corregida con HC3)
- Autocorrelación espacial no modelada explícitamente (DW = 0.923)
- Colas pesadas en residuales (Kurtosis = 8.18) por cuencas atípicas

## Extensiones futuras
- Modelos de regresión espacial (SAR, SEM) para capturar autocorrelación
- Análisis separado por tamaño de cuenca
- Modelo logístico para predecir probabilidad de déficit hídrico