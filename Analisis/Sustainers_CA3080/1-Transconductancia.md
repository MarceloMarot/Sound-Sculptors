





# Amplificadores de transconductancia (OTA)



<image src="Transconductancia/0 - esquema.png" width=500px alt="0 - esquema.png" >



Los amplificadores de transconductancia (OTA) son ampificadores cuya entrada es una *tensión diferencial* (es decir la diferencia de tensiones  entre las entradas) en tanto que su salida es una corriente: 

$$ v_{DIF} = \left(v_{IN^+} - v_{IN^-} \right) $$

$$ i_O = gm \cdot v_{DIF} $$

El parámetro *gm* es la *transconductancia*. Este parámetro depende de la corriente de polarización $I_{POL}$ ($I_{BIAS}$ en la notación angloparlante), la cual se controla desde afuera del dispositivo. La fórmula aproximada de la transconductancia es:

$$ gm =  \simeq \frac{I_{POL}}{50mV} [mS]  $$     



La unidad de medida de la transconductancia es el siemens (S), el cual suele indicarse en las hojas técnicas antiguas como 'mho'. 

$$ 1 S = 1 mho = \frac{1 A}{1 V}$$


La tensión de salida dependerá de la corriente salida y de la impedancia de carga conectada a la salida. Si ésta es una resistencia:

$$ v_O = R_0 \cdot i_O = R_0 \cdot gm \cdot v_{diff}  $$

La ganancia de tensión es la relación entre la tensión de salida respecto a la tensión de entrada:

$$ A_0 = \frac {v_O}{v_{diff}}$$

La ganancia de tensión tendrá entonces la expresión:

$$ A_0 =  R_0 \cdot gm = \frac{R_O \cdot I_{POL}}{50mV}$$

El valor máximo de corriente a la salida viene dado por la corriente ingresada por el pin de polarización $I_{POL}$. Ésta normalmente es controlada con una tensión de control y una resistencia.

$$  I_{POL} = \frac{V_{CONTROL}-V_{\gamma}}{R_{POL}} 

\simeq  \frac{V_{CONTROL}-0.6V}{R_{POL}}  $$


Nótes que la tension de control aparece referenciada a la alimentación negativa y no a la referencia de señal.

Si se combinan las expresiones previas se puede obtener una expresión para la ganancia de tensión total:

$$ A_0 \simeq   \frac{R_O }{0.05V} \cdot  \frac{V_{CONTROL}-0.6V}{R_{POL}}  $$


Con los valores del esquema y, asumiendo que la tensión de control va de 0.6V a 10.6V, dicha ganancia está comprendida entre 0 y 20.

La amplitud de la tensión de salida viene limitada por la corriente de polarización y la resistencia de carga:

$$ \left|V_{0max} \right| \simeq   {R_O } \cdot {I_{POL}}   $$

En el esquema cómo se desempeña la etapa de transconductancia del esquema suponiendo una entrada sinusoidal de frecuencia 100Hz y amplitud 25mV, con una tension de control que da saltos de 2V:

<image src="Transconductancia/2B - control amplitud.png"  alt="2B - control amplitud.png">

Se verifica cómo la amplitud de salida es directamente proporcional a la corriente inyectada al pin de polarización. La ganancia lograda en cada caso es ligeramente inferior a la calculada. 

La entrada de señal del dispositivo tiene un rango lineal limitado al rango de los milivoltios. En el siguiente diagrama se evaluan distintas amplitudes de entrada que van desde los 25mV (rojo) hasta los 150mV (magenta) haciendo la corriente de polarización fija en 1mA (Vcontrol de 10.6V):


<image src="Transconductancia/1A - salida.png"  alt="1A - salida.png">

Con una amplitud de entrada de 25mV (rojo) la reproducción es casi perfecta y la ganancia es el 90% de la calculada. Para amplitudes mayores se observa cómo la tensión de salida tiende a 'aplanarse' en sus picos.

<image src="Transconductancia/1B - salida fft lineal.png"  alt="1B - salida fft lineal.png">

Los armónicos impares son dominantes en este dispositivo. Esto tiene que ver con el aplanamiento prácticamente idéntico para ambos semiciclos. 

Al observar la representación logarítmica de la FFT se puede apreciar mejor la amplitud de los armónicos añadidos:

<image src="Transconductancia/1C - salida fft db.png"  alt="1C - salida fft db.png">




