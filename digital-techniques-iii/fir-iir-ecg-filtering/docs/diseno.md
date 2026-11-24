# Diseño digital

El registro se procesa a 360 muestras/s. El informe considera deriva de línea base, movimiento de electrodos, actividad muscular e interferencia de red. Las dos etapas seleccionadas actúan sobre altas frecuencias y la componente de red; la deriva de baja frecuencia requiere otro tratamiento. El objetivo es comparar cadenas sobre el registro, sin establecer rendimiento clínico.

| Etapa | Especificación del informe | Diseño FIR | Diseño IIR |
|---|---|---|---|
| Pasa bajos | Paso hasta 40 Hz, rechazo desde 50 Hz, 1 dB y 40 dB | Ideal con corte a 45 Hz, ventana Kaiser | Prototipo Butterworth y transformación bilineal |
| Rechaza banda | Paso hasta 46 Hz y desde 54 Hz, rechazo de 48 a 52 Hz | Inversión espectral de un pasabanda con cortes ideales a 47 y 53 Hz, ventana Hamming | Transformación de prototipo Butterworth a rechaza banda |

Para el FIR, $H(z)=\sum_{n=0}^{M}h[n]z^{-n}$. Se desplaza la respuesta ideal a $M/2$, se multiplica por la ventana y se obtiene una respuesta impulsiva finita y simétrica. En el notch, se resta el pasabanda ideal al impulso centrado. La ventana determina el compromiso entre ancho de transición y lóbulos laterales (pp. 11–21).

Para el IIR se predeforman los bordes con $\Omega=2f_s\tan(\pi f/f_s)$ y se aplica $s=2f_s(1-z^{-1})/(1+z^{-1})$. Cada sección de segundo orden tiene numerador y denominador de grado dos en $z^{-1}$. La respuesta de la cascada es el producto de sus secciones. Los polos determinan la cola de la respuesta impulsiva, y el retardo de grupo es $-d\arg H/d\omega$. La implementación en secciones evita expandir el polinomio de alto orden en precisión simple (pp. 22–39, 55–56).

[Revisión del orden y los retardos](resultados.md).
