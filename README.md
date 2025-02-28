# Laboratorio-3

# 1.Configuración del sistema
Como primer paso para configurar el sistema se ubicaron tres micrófonos:
Estos micrófonos se ubicaron a 6 m de distancia entre ellos,como se muestra en el siguiente bosquejo:
![image](https://github.com/user-attachments/assets/df980857-d875-415e-ad2c-4b8ce2195409)
# 2.Captura de la señal.
Se grabaron tres señales mediante la voz de tres personas; las frases que dijeron en la captura fueron las siguientes:
Persona 1:
Persona 2:
Persona 3:"Mi comida favorita es la hamburguesa sin verduras"

# 3.Analisis temporal y espectral de las señales capturadas por los micrófonos.

Caracteristicas principales de cada fuente sonora:


Tranformada de Fourier rápida:

# 3.Métodos de separación de fuentes
 # ICA
 
# 4.SNR

Es una medida que compara el nivel de una señal deseada con el nivel del ruido de fondo en un sistema de audio o comunicaciones. Se expresa generalmente en decibeles (dB)
                                                                                               SNR=10log10(Pseñal/Pruido) 

Un SNR alto (mayor cantidad de dB) significa que la señal es mucho más fuerte que el ruido, lo que resulta en una mejor calidad de audio, mientras que un SNR bajo (menor cantidad de dB) indica que el ruido es comparable o incluso mayor que la señal, lo que puede dificultar la interpretación de la información transmitida.





# 5 Preguntas a resolver
-¿Cómo afecta la posición relativa de los micrófonos y las fuentes sonoras en la efectividad de la separación de señales?

La posición relativa de los micrófonos y las fuentes sonoras afecta significativamente la efectividad en la separación de señales debido a la distancia, la direccionalidad y el rechazo de interferencias.

Distancia y ángulo: Un mayor espaciamiento entre micrófonos mejora la capacidad de separar señales basadas en la diferencia de tiempo de llegada y la fase.

Rechazo de ruido: Un correcto posicionamiento minimiza interferencias y maximiza la captación de la señal deseada.

Efecto de diafonía: Si las fuentes están muy cercanas o alineadas, puede ser más difícil separar sus señales debido a la superposición de frecuencias.

Ambiente acústico: La reverberación y los reflejos pueden alterar la captación, por lo que la ubicación de los micrófonos debe optimizarse para minimizar estos efectos.

-¿Qué mejoras implementaría en la metodología para obtener mejores resultados?

Optimización de la disposición espacial

Aumentar la separación entre micrófonos para mejorar la diferenciación de las señales según la diferencia de tiempo de llegada.
Ubicar los micrófonos estratégicamente para minimizar interferencias y reflexiones no deseadas.

Reducción de ruido y diafonía

Utilizar micrófonos direccionales o configuraciones de matrices para mejorar la captación de la señal deseada y reducir interferencias.
Implementar filtros de acondicionamiento de señales para minimizar el ruido ambiental.

Calibración y caracterización precisa

Realizar pruebas previas de caracterización de los micrófonos para identificar su respuesta en diferentes condiciones.
Aplicar técnicas de normalización y ajuste de ganancia para mantener niveles de señal óptimos.

Mejora en el procesamiento de señales

Aplicar técnicas avanzadas de separación de fuentes como algoritmos de análisis de componentes independientes (ICA) o filtrado adaptativo.
Implementar modelos de machine learning o técnicas de deep learning para mejorar la separación de señales en entornos ruidosos.

Simulación y pruebas experimentales

Realizar simulaciones previas mediante software como MATLAB o Proteus para ajustar los parámetros del sistema antes de la implementación real.
Efectuar mediciones en diferentes condiciones para evaluar la robustez del método y ajustar los parámetros necesarios.
