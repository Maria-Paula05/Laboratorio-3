# Laboratorio-3
# Librerías utilizadas a lo largo del laboratorio 

```phyton
import librosa
import matplotlib.pyplot as plt
import numpy as np
```

# 1.Configuración del sistema
Como primer paso para configurar el sistema se ubicaron tres micrófonos:
Estos micrófonos se ubicaron a 6 m de distancia entre ellos,como se muestra en el siguiente bosquejo:



![image](https://github.com/user-attachments/assets/df980857-d875-415e-ad2c-4b8ce2195409)
# 2.Captura de la señal.

1.Se grabaron tres señales mediante la voz de tres personas; las frases que dijeron en la captura fueron las siguientes:


Persona 1(Paula Vanessa):

🎧 [Escuchar el audio](https://github.com/Maria-Paula05/Laboratorio-3/blob/main/AUDIO1.wav)

Persona 2(María Paula):"Mi comida favorita es la hamburguesa sin verduras."

🎧 [Escuchar el audio](https://github.com/Maria-Paula05/Laboratorio-3/blob/main/AUDIO2.wav)

Persona 1(Juan Pablo:"Las medusas existen desde hace más de 600 millones de años lo que las hace más antiguas que los dinosaurios los tiburones e incluso los árboles."

🎧 [Escuchar el audio](https://github.com/Maria-Paula05/Laboratorio-3/blob/main/AUDIO3.wav)

Estas frases fueron grabadas al tiempo y se almacenaron en los dispositivos en archivos .wav.

2.Luego se capturaron las señales del ruido de fondo con los tres micrófonos.

Ruido de fondo 1:

🎧 [Escuchar el audio](https://github.com/Maria-Paula05/Laboratorio-3/blob/main/FONDO1.wav)

Ruido de fondo 2:

🎧 [Escuchar el audio](https://github.com/Maria-Paula05/Laboratorio-3/blob/main/FONDO2.wav)

Ruido de fondo 3:

🎧 [Escuchar el audio](https://github.com/Maria-Paula05/Laboratorio-3/blob/main/FONDO3.wav)

# Señales audio-fondo y cálculo de SNR (1) 
```python
audio_path1 = 'AUDIO1.wav'
audio_path2 = 'FONDO1.wav'
y1, sr1 = librosa.load(audio_path1)
y2, sr2 = librosa.load(audio_path2)

time1 = np.linspace(0, len(y1) / sr1, num=len(y1))
time2 = np.linspace(0, len(y2) / sr2, num=len(y2))

plt.figure(figsize=(12, 6))

# Primera señal (AUDIO 1)
plt.subplot(2, 1, 1)
plt.plot(time1, y1, label="Forma de onda AUDIO 1", alpha=0.7)
plt.title('Forma de onda de AUDIO 1')
plt.xlabel('Tiempo (s)')
plt.ylabel('Amplitud (normalizada)')
plt.legend()

# Segunda señal (RUIDO DE FONDO 1)
plt.subplot(2, 1, 2)
plt.plot(time2, y2, label="Forma de onda RUIDO DE FONDO 1", color='orange', alpha=0.7)
plt.title('Forma de onda de RUIDO DE FONDO 1')
plt.xlabel('Tiempo (s)')
plt.ylabel('Amplitud (normalizada)')
plt.legend()

plt.tight_layout()
plt.show()

min_len = min(len(y1), len(y2))
y1, y2 = y1[:min_len], y2[:min_len]

AUDIO1 = np.mean(y1 ** 2)
FONDO1 = np.mean(y2 ** 2)
snr_db = 10 * np.log10(AUDIO1 / FONDO1)

print(f"SNR: {snr_db:.2f} dB")
````
![image](https://github.com/user-attachments/assets/2c4374f9-2675-46d1-b46e-4eddc2325b2e)

SNR:38.29

# Señales audio-fondo y cálculo de SNR (2) 

# Cargar los archivos de audio

```phyton
audio_path1 = 'AUDIO2.wav'
audio_path2 = 'FONDO2.wav'
y1, sr1 = librosa.load(audio_path1)
y2, sr2 = librosa.load(audio_path2)

# Crear los ejes de tiempo
time1 = np.linspace(0, len(y1) / sr1, num=len(y1))
time2 = np.linspace(0, len(y2) / sr2, num=len(y2))

# Graficar ambas señales
plt.figure(figsize=(12, 6))

# Primera señal (AUDIO 1)
plt.subplot(2, 1, 1)
plt.plot(time1, y1, label="Forma de onda AUDIO 2", alpha=0.7)
plt.title('Forma de onda de AUDIO 2')
plt.xlabel('Tiempo (s)')
plt.ylabel('Amplitud (normalizada)')
plt.legend()

# Segunda señal (RUIDO DE FONDO 1)
plt.subplot(2, 1, 2)
plt.plot(time2, y2, label="Forma de onda RUIDO DE FONDO 2", color='red', alpha=0.7)
plt.title('Forma de onda de RUIDO DE FONDO 2')
plt.xlabel('Tiempo (s)')
plt.ylabel('Amplitud (normalizada)')
plt.legend()

plt.tight_layout()
plt.show()

min_len = min(len(y1), len(y2))
y1, y2 = y1[:min_len], y2[:min_len]

# Calcular la SNR en dB (Señal: y1, Ruido: y2)
AUDIO2 = np.mean(y1 ** 2)
FONDO2 = np.mean(y2 ** 2)
snr_db = 10 * np.log10(AUDIO2 / FONDO2)

# Separación vertical
offset = 2
y2_shifted = y2 + offset

time = np.arange(len(y1)) / sr1

print(f"SNR: {snr_db:.2f} dB")
```
![image](https://github.com/user-attachments/assets/6ef3002a-2e6d-4c74-88ee-14cc33946a79)

SNR:37.43

# Señales audio-fondo y cálculo de SNR (2) 


```phyton
audio_path1 = 'AUDIO3.wav'
audio_path2 = 'FONDO3.wav'
y1, sr1 = librosa.load(audio_path1)
y2, sr2 = librosa.load(audio_path2)

# Crear los ejes de tiempo
time1 = np.linspace(0, len(y1) / sr1, num=len(y1))
time2 = np.linspace(0, len(y2) / sr2, num=len(y2))

# Graficar ambas señales
plt.figure(figsize=(12, 6))

# Primera señal (AUDIO 1)
plt.subplot(2, 1, 1)
plt.plot(time1, y1, label="Forma de onda AUDIO 3", alpha=0.7)
plt.title('Forma de onda de AUDIO 3')
plt.xlabel('Tiempo (s)')
plt.ylabel('Amplitud (normalizada)')
plt.legend()

# Segunda señal (RUIDO DE FONDO 1)
plt.subplot(2, 1, 2)
plt.plot(time2, y2, label="Forma de onda RUIDO DE FONDO 3", color='green', alpha=0.7)
plt.title('Forma de onda de RUIDO DE FONDO 1')
plt.xlabel('Tiempo (s)')
plt.ylabel('Amplitud (normalizada)')
plt.legend()

plt.tight_layout()
plt.show()

min_len = min(len(y1), len(y2))
y1, y2 = y1[:min_len], y2[:min_len]

# Calcular la SNR en dB (Señal: y1, Ruido: y2)
AUDIO3 = np.mean(y1 ** 2)
FONDO3 = np.mean(y2 ** 2)
snr_db = 10 * np.log10(AUDIO3 / FONDO3)

# Separación vertical
offset = 2
y2_shifted = y2 + offset

time = np.arange(len(y1)) / sr1

print(f"SNR: {snr_db:.2f} dB")
```
![image](https://github.com/user-attachments/assets/cfc70543-ca08-4083-b598-1d8097ceba38)

SNR:26.89

# 3.Analisis temporal y espectral de las señales capturadas por los micrófonos.

Caracteristicas principales de cada fuente sonora:



Análisis y gráfica de un audio:

El análisis y graficación de audio permiten examinar una señal en el dominio del tiempo y la frecuencia para comprender sus características.

-Un archivo de audio se convierte en una serie de valores numéricos que representan su variación en el tiempo.

-Análisis temporal: La forma de onda muestra cómo cambia la amplitud del sonido, permitiendo identificar eventos como golpes o pausas.

-Análisis frecuencial: La Transformada Rápida de Fourier (FFT) convierte la señal al dominio de la frecuencia, mostrando qué frecuencias están presentes y su intensidad en decibeles (dB).

-Permite identificar sonidos graves o agudos, analizar ruido y comparar señales de distintos micrófonos.

```phyton
audio_paths = ['AUDIO1.wav', 'AUDIO2.wav', 'AUDIO3.wav']
signals = []
sampling_rates = []

for path in audio_paths:
    y, sr = librosa.load(path, sr=None)  # Mantener frecuencia original
    signals.append(y)
    sampling_rates.append(sr)

# Análisis Temporal: Graficar las formas de onda
plt.figure(figsize=(12, 8))
for i, y in enumerate(signals):
    plt.subplot(3, 1, i+1)
    librosa.display.waveshow(y, sr=sampling_rates[i], alpha=0.7)
    plt.title(f'Forma de onda - Micrófono {i+1}')
    plt.xlabel('Tiempo (s)')
    plt.ylabel('Amplitud (dB)')
    plt.xticks(np.linspace(0, len(y) / sampling_rates[i], num=5))  # Etiquetas en el eje x
    plt.yticks(np.linspace(np.min(y), np.max(y), num=5))  # Etiquetas en el eje y

plt.tight_layout()
plt.show()

# Análisis Espectral: Aplicar FFT y visualizar espectros de frecuencia
plt.figure(figsize=(12, 8))
for i, y in enumerate(signals):
    N = len(y)  # Número de muestras
    T = 1.0 / sampling_rates[i]  # Período de muestreo
    freqs = np.fft.rfftfreq(N, T)  # Frecuencias
    fft_vals = 20 * np.log10(np.abs(np.fft.rfft(y)) + 1e-6)  # Convertir amplitud a dB  # Magnitud de la FFT

    plt.subplot(3, 1, i+1)
    plt.plot(freqs, fft_vals, label=f'Espectro - Micrófono {i+1}')
    plt.xlim(0, 5000)  # Limitar a 5 kHz (frecuencias de voz humana)
    plt.xlabel('Frecuencia (Hz)')
    plt.ylabel('Amplitud (dB)')
    plt.xticks(np.linspace(0, 5000, num=6))  # Etiquetas en el eje x
    plt.yticks(np.linspace(np.min(fft_vals), np.max(fft_vals), num=5))  # Etiquetas en el eje y
    plt.legend()

plt.tight_layout()
plt.show()
```
![image](https://github.com/user-attachments/assets/4db6ddca-792b-413f-8cf3-adb39022b9dc)


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
