# Laboratorio 3 - Problema del cóctel 

Este laboratorio aborda el problema del cóctel, que consiste en aislar una fuente de sonido en un entorno con múltiples emisores. A lo largo del repositorio, se implementan técnicas de procesamiento digital de señales, como el Análisis de Componentes Independientes (ICA) y Beamforming, para separar las señales capturadas por un arreglo de micrófonos y evaluar experimentalmente la efectividad de cada método.

# 1. Configuración del sistema
Como primer paso para configurar el sistema se ubicaron tres micrófonos:
Estos micrófonos se ubicaron a 6 m de distancia entre ellos,como se muestra en el siguiente bosquejo:



![image](https://github.com/user-attachments/assets/df980857-d875-415e-ad2c-4b8ce2195409)
# 2. Captura de la señal.

1. Se grabaron tres señales mediante la voz de tres personas; las frases que dijeron en la captura fueron las siguientes:

Persona 1(Paula Vanessa):"Por accidente le pegue a la ventana de la vecina y la rompí"

🎧 [Escuchar el audio](https://github.com/Maria-Paula05/Laboratorio-3/blob/main/AUDIO1.wav)

Persona 2(María Paula):"Mi comida favorita es la hamburguesa sin verduras."

🎧 [Escuchar el audio](https://github.com/Maria-Paula05/Laboratorio-3/blob/main/AUDIO2.wav)

Persona 1(Juan Pablo):"Las medusas existen desde hace más de 600 millones de años lo que las hace más antiguas que los dinosaurios los tiburones e incluso los árboles."

🎧 [Escuchar el audio](https://github.com/Maria-Paula05/Laboratorio-3/blob/main/AUDIO3.wav)

Estas frases fueron grabadas al tiempo y se almacenaron en los dispositivos en archivos .wav.

2. Luego se capturaron las señales del ruido de fondo con los tres micrófonos.

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

```python
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

# Señales audio-fondo y cálculo de SNR (3) 


```python
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

# 3. Analisis temporal y espectral de las señales capturadas por los micrófonos.

**Caracteristicas principales de cada fuente sonora:**

En este caso, se tienen tres fuentes sonoras:

1. Voces humanas
   
Cada una de las tres voces tendrá características distintas, dependiendo de la persona que habla:

- Timbre: Cada voz tiene un tono único (grave, agudo, nasal, suave, áspera, etc.).

- Intensidad: Algunas voces pueden sonar más fuertes o más suaves según la distancia al micrófono o la manera de hablar.

- Velocidad y ritmo: Algunas personas pueden hablar rápido, pausado, con énfasis en ciertas palabras.

- Entonación: Puede haber variaciones según la emoción (tono serio, alegre, enojado, triste, etc.).

- Ubicación espacial: En un audio estéreo, las voces pueden ubicarse en distintos puntos (izquierda, derecha o centro).

2. Música de fondo
   
La música también tiene varias características que afectan cómo se percibe en el audio:

- Timbre: Dependerá de los instrumentos utilizados (piano, guitarra, sintetizador, etc.).

- Volumen: Puede ser baja para no opacar las voces o alta si es el elemento principal en algunos momentos.

- Ritmo y tempo: Puede ser rápida, lenta, con cambios de velocidad.

- Estilo: Puede ser clásica, electrónica, rock, jazz, etc., lo que influye en la atmósfera del audio.

- Presencia: Puede sonar de fondo de manera constante o variar su intensidad en diferentes momentos.

3. Efectos de sonido 
Los efectos de sonido pueden aportar realismo o dramatismo al audio:

- Naturales: Sonidos de la universidad, viento, pasos, murmullos de fondo.

- Artificiales: Transiciones, ruidos añadidos en edición, eco, reverberación.

- Ubicación espacial: Al igual que las voces, pueden posicionarse en distintos puntos del estéreo (izquierda, derecha, fondo).

- Propósito: Pueden ser utilizados para ambientar, enfatizar acciones o mejorar la experiencia sonora.

Análisis y gráfica de un audio: El análisis y graficación de audio permiten examinar una señal en el dominio del tiempo y la frecuencia para comprender sus características.

- Análisis temporal: La forma de onda muestra cómo cambia la amplitud del sonido, permitiendo identificar eventos como golpes o pausas.

```python
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
```
![image](https://raw.githubusercontent.com/Maria-Paula05/Laboratorio-3/refs/heads/main/ONDA.png)

- Análisis frecuencial: La Transformada Rápida de Fourier (FFT) convierte la señal al dominio de la frecuencia, mostrando qué frecuencias están presentes y su intensidad en decibeles (dB).

    Permite identificar sonidos graves o agudos, analizar ruido y comparar señales de distintos micrófonos.

```python
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
![image](https://raw.githubusercontent.com/Maria-Paula05/Laboratorio-3/refs/heads/main/FFT.png)

# 4. Métodos de separación de fuentes
# ICA
*"El Análisis de Componentes Independientes (ICA) es una técnica estadística que permite separar señales mezcladas asumiendo que sus fuentes son estadísticamente independientes. Se utiliza en el procesamiento de audio para aislar sonidos individuales a partir de una mezcla." (Learn Statistics Easily, 2024).*

El proceso para separar fuentes comienza con la carga de archivos de audio, asegurando que todas las señales mezcladas tengan la misma frecuencia de muestreo y longitud. Luego, se aplica el Análisis de Componentes Independientes (ICA) para separar las fuentes sonoras, asumiendo que son estadísticamente independientes.
Para mejorar la calidad del audio extraído, se utiliza un filtro pasa banda (100 Hz - 4000 Hz), eliminando frecuencias no deseadas. Luego, la señal se normaliza y convierte al formato int16, optimizándola para su almacenamiento. Finalmente, el archivo se guarda en formato .wav.

```python
import librosa
import numpy as np
import matplotlib.pyplot as plt
from sklearn.decomposition import FastICA
import soundfile as sf

# Cargar el audio
audio_path1 = 'AUDIO3.wav'
y1, sr1 = librosa.load(audio_path1, mono=True)
fs = sr1 
duration = len(y1) / fs

# Asegurar que la señal sea de dos canales para ICA
y2 = np.roll(y1, 1000)
audios_mixtos = np.column_stack([y1, y2])

# Aplicar FastICA
ica = FastICA(n_components=2)
audios_separados = ica.fit_transform(audios_mixtos)

# Seleccionar la primera fuente estimada
senal_aislada = audios_separados[:, 0]

# Ajustar amplitudes al mismo nivel
senal_aislada /= np.max(np.abs(senal_aislada))  # Normalizar entre [-1,1]
senal_aislada *= np.max(np.abs(y1))  # Escalar a la misma amplitud que AUDIO3

# Guardar la señal aislada
sf.write("VOZ3.wav", senal_aislada, fs)
print("Se guardó la señal aislada con ICA en 'VOZ3.wav'.")

# Cálculo de SNR basado en la señal original como referencia
def calculate_snr(original, isolated):
    original = original[:len(isolated)]  # Asegurar mismo tamaño
    noise = original - isolated  # Calcular ruido
    signal_power = np.mean(original ** 2)
    noise_power = np.mean(noise ** 2)
    snr = 10 * np.log10(signal_power / noise_power) if noise_power > 0 else float('inf')
    return snr

snr_aislada = calculate_snr(y1, senal_aislada)
print(f"SNR de AUDIO3 aislado: {snr_aislada:.2f} dB")

# Graficar AUDIO3 original y aislado
plt.figure(figsize=(12, 6))
plt.subplot(2, 1, 1)
plt.plot(np.linspace(0, duration, len(y1)), y1, color="green")
plt.xlabel("Tiempo (s)")
plt.ylabel("Amplitud (Normalizada)")
plt.title("AUDIO3 Original")

plt.subplot(2, 1, 2)
plt.plot(np.linspace(0, duration, len(senal_aislada)), senal_aislada, color="blue")
plt.xlabel("Tiempo (s)")
plt.ylabel("Amplitud (Normalizada)")
plt.title("AUDIO3 Aislado")

plt.tight_layout()
plt.show()

```
**Comparación señal aislada / la señal original**

Por ultimo se compara la señal aislada con la señal original mediante métricas de calidad, para cuantificar el desempeño de la separación y evaluar la efectividad del proceso.


*Se guardó la señal aislada con ICA en 'VOZ3.wav'.*

*SNR de AUDIO3 aislado: 16.92 dB*
![image](https://raw.githubusercontent.com/Maria-Paula05/Laboratorio-3/refs/heads/main/AISLADA.png)

🎧 [AUDIO 3](https://github.com/Maria-Paula05/Laboratorio-3/blob/main/AUDIO3.wav)
🎧 [VOZ3](VOZ3.wav)

# Beamforming
*"Beamforming es una técnica que se utiliza para mejorar la relación señal-ruido de las señales recibidas, eliminar fuentes de interferencia no deseadas y enfocar señales transmitidas a ubicaciones específicas." (Beamforming, s.f.)*

```python

folder_path = "C:\\Users\\paula\\Desktop\\COCTEL"

# 🎤 Cargar audios de los micrófonos
fs, mic1 = wav.read(os.path.join(folder_path, "AUDIO1.wav"))
_, mic2 = wav.read(os.path.join(folder_path, "AUDIO2.wav"))
_, mic3 = wav.read(os.path.join(folder_path, "AUDIO3.wav"))

signals = np.vstack([mic1, mic2, mic3])

# Posiciones actualizadas de los micrófonos según la imagen
mic_positions = np.array([
    [-3, 6],  # Mic 1 (izquierda)
    [3, 6],   # Mic 2 (derecha)
    [0, -1],  # Mic 3 (abajo en el centro)
]).T  # Transpuesta para el formato correcto

# Dirección de la persona central (asumimos que está en (0,0))
angle = np.pi / 2  # 90°

# 🛠 Crear beamformer Delay-and-Sum
R = mic_positions  # Matriz de posiciones
beamformer = pra.beamforming.DelayAndSum(R, fs, nfft=256)  # Intentar con DelayAndSum

# Apuntar el beamformer a la dirección deseada
beamformer.steer(azimuth=angle, colatitude=np.pi/2)  

# Aplicar beamforming
output_signal = beamformer.process(signals)

# Guardar el audio resultante
output_path = os.path.join(folder_path, "voz_central_beamforming.wav")
wav.write(output_path, fs, output_signal.astype(np.int16))

print(f"Audio procesado guardado en: {output_path}")

```

# SNR

Es una medida que compara el nivel de una señal deseada con el nivel del ruido de fondo en un sistema de audio o comunicaciones. Se expresa generalmente en decibeles (dB)
                                                                                               SNR=10log10(Pseñal/Pruido)
                                                                                               
Un SNR alto (mayor cantidad de dB) significa que la señal es mucho más fuerte que el ruido, lo que resulta en una mejor calidad de audio, mientras que un SNR bajo (menor cantidad de dB) indica que el ruido es comparable o incluso mayor que la señal, lo que puede dificultar la interpretación de la información transmitida.

# 5. Preguntas a resolver
**¿Cómo afecta la posición relativa de los micrófonos y las fuentes sonoras en la efectividad de la separación de señales?**

- Posición relativa de los micrófonos: la posición de los micrófonos y las fuentes sonoras afecta significativamente la efectividad en la separación de señales debido a la distancia, la direccionalidad y el rechazo de interferencias.

- Distancia y ángulo: Un mayor espaciamiento entre micrófonos mejora la capacidad de separar señales basadas en la diferencia de tiempo de llegada y la fase.

- Rechazo de ruido: Un correcto posicionamiento minimiza interferencias y maximiza la captación de la señal deseada.

- Efecto de diafonía: Si las fuentes están muy cercanas o alineadas, puede ser más difícil separar sus señales debido a la superposición de frecuencias.

- Ambiente acústico: La reverberación y los reflejos pueden alterar la captación, por lo que la ubicación de los micrófonos debe optimizarse para minimizar estos efectos.

**¿Qué mejoras implementaría en la metodología para obtener mejores resultados?**

- Optimización de la disposición espacial

    Aumentar la separación entre micrófonos para mejorar la diferenciación de las señales según la diferencia de tiempo de llegada.
    Ubicar los micrófonos estratégicamente para minimizar interferencias y reflexiones no deseadas.

- Reducción de ruido y diafonía

    Utilizar micrófonos direccionales o configuraciones de matrices para mejorar la captación de la señal deseada y reducir interferencias.
    Implementar filtros de acondicionamiento de señales para minimizar el ruido ambiental.

- Calibración y caracterización precisa

    Realizar pruebas previas de caracterización de los micrófonos para identificar su respuesta en diferentes condiciones.
    Aplicar técnicas de normalización y ajuste de ganancia para mantener niveles de señal óptimos.

- Mejora en el procesamiento de señales

    Aplicar técnicas avanzadas de separación de fuentes como algoritmos de análisis de componentes independientes (ICA) o filtrado adaptativo.
    Implementar modelos de machine learning o técnicas de deep learning para mejorar la separación de señales en entornos ruidosos.

- Simulación y pruebas experimentales

    Realizar simulaciones previas mediante software como MATLAB o Proteus para ajustar los parámetros del sistema antes de la implementación real.
    Efectuar mediciones en diferentes condiciones para evaluar la robustez del método y ajustar los parámetros necesarios.

# 6. Conclusiones
- La resolución experimental del problema del cóctel demostró que es posible aislar parcialmente una voz específica entre múltiples fuentes sonoras. Para ello, implementamos dos técnicas: Análisis de Componentes Independientes (ICA) y Beamforming. Los resultados indicaron que ICA logró una separación más clara, aunque aún incompleta, de la voz objetivo.

- El principal obstáculo fue la calidad de la captura de audio. Factores como la disposición inadecuada de los celulares, variaciones en la ganancia y condiciones acústicas desfavorables afectaron los datos iniciales, limitando la efectividad del procesamiento posterior.

- El mejor desempeño de ICA en comparación con Beamforming sugiere que la calidad de los datos de entrada fue un factor determinante en los resultados, más que la técnica de procesamiento utilizada.
  
# Referencias

-   Transformación rápida de Fourier FFT (s.f.).
https://www.nti-audio.com/es/servicio/conocimientos/transformacion-rapida-de-fourier-fft

-   Rivera, E., Moreno, R., Pérez, H., & Nakano, M. (2020). Separación de señales usando análisis de componentes principales y muestreo compresivo con mediciones mínimas. CIT Informacion Tecnologica, 31(1), 287–300. https://doi.org/10.4067/s0718-07642020000100287

-   Acaro, X., Molina, M., Corapi, P., Molina Villacis, M., Reamache Rivera, G. J., & Castillo García, J. V. (2021). Interfaz gráfica para el análisis de audio y sonidos urbanos (CasRem). Investigación, Tecnología e Innovación, 13(14), 29–42. https://doi.org/10.53591/iti.v13i14.1308

-   Marengo Rodriguez, F. A., Roveri, E. A., Guerrero, J. M. R., Treffiló, M., & Miyara, F. (s.f). ANÁLISIS COMPARATIVO DE CODIFICADORES DE AUDIO SIN PÉRDIDAS. Edu.ar. Recuperado el 28 de febrero de 2025, de https://www.fceia.unr.edu.ar/acustica/codecdigital/archivos/comparativo-codificadores-sin-perdidas-UNTREF.pdf

-   Beamforming. (s.f.). MATLAB & Simulink. https://la.mathworks.com/discovery/beamforming.html
