# Resultados de MATLAB y revisión numérica

Se compararon pasa bajos + notch FIR y pasa bajos + notch IIR sobre la misma señal. El informe analiza magnitud, fase, impulso, retardo de grupo, polos y ceros, señal temporal y FFT (pp. 31–46). En el FIR de orden alto, el propio informe descarta el cálculo directo de raíces como indicador fiable del notch. Para el IIR informa módulos máximos de polo inferiores a uno en ambas etapas. La estabilidad numérica del firmware requeriría comprobar sus coeficientes cuantizados.

| Magnitud de la tabla de p. 45 | FIR | IIR |
|---|---:|---:|
| Ganancia teórica a 50 Hz | −94,109 dB | −53 dB |
| Cambio espectral informado por FFT | −34,0285 dB | −45,3226 dB |
| RMSE informado | 0,032103 | 0,52097 |
| SNR informada | 20,8828 dB | −3,2276 dB |

La magnitud de la transferencia y el cociente obtenido sobre un segmento finito de señal son evaluaciones distintas. La tabla favorece al FIR en RMSE y SNR para el ensayo reportado. El IIR tiene menor orden y mayor reducción de la componente observada en la FFT. Faltan los vectores, referencia exacta, alineación temporal y parámetros espectrales para recalcular las métricas. Son resultados publicados por los autores.

## Comprobaciones independientes

| Fuente | Comprobación | Interpretación |
|---|---|---|
| p. 12, Nyquist indicado como 360 Hz | 360/2 = 180 Hz, coincidente con la ecuación de la misma página | 360 Hz es la frecuencia de muestreo. |
| pp. 12–16, Kaiser | Δω = 2π·10/360 ≈ 0,17453; β ≈ 3,3953. El techo de 32/(2,285·Δω) es 81. | 82 coeficientes y retardo de 40,5 muestras (112,5 ms). |
| pp. 18–21, 35 y 45, Hamming | Δω = 2π·2/360. La estimación 8π/Δω da 720. Con los dos órdenes, (81+720)/2 = 400,5 muestras. | El retardo de la cascada FIR es 1,1125 s; el del pasa bajos aislado es 0,1125 s. |
| pp. 22–27 y 45, Butterworth | La p. 22 introduce segundo orden. Con bordes predeformados a 40 y 50 Hz y requisitos 1/40 dB, el orden mínimo calculado es techo(21,313) = 22. | La tabla final utiliza 22. Los dos polos de p. 27 son insuficientes para certificar el filtro de orden 22. |
| pp. 27–30, notación | El numerador de la forma factorizada de p. 27 imprime un término en z positivo; la ecuación en diferencias usa una muestra anterior. | Para la sección causal corresponde z⁻¹. Verificar los coeficientes originales antes de reconstruir. |
| pp. 28 y 45, notch IIR | La transformación rechaza banda duplica el orden del prototipo declarado: 8 × 2 = 16. | Junto con el pasa bajos de 22, el orden total tabulado es 38. |

La forma de onda, el espectro y los errores deben interpretarse con la latencia de cada alternativa. El informe no acredita una validación diagnóstica.
