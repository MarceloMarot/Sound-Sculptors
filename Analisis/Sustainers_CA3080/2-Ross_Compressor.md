


# Ross Compressor

Este compresor/sustainer es el diseño de referencia para muchos otros pedales de su tipo. El corazón de esta etapa es el integrado CA3080, un amplificador de tranconductancia (OTA).

<image src="Ross_Compressor/Ross_Compressor_v2.png"  alt="Ross Compressor.png" >

## Señal de Entrada

Para analizar mejor el funcionamiento del sistema se creó una señal monofónica cuya envolvente sea similar al de una señal de guitarra real, pasando por cuatro etapas temporales: *rise*, *fall*, *sustain* y *release*.

<image src="Ross_Compressor/vguitarra.png"  alt="vguitarra.png" >

Las amplitudes y tiempos relativos de cada tiempo fueron elegidos arbitrariamente.

## Alimentacion y tension de referencia

La tensión de referencia para las etapas internas se crea con un divisor de tensión resistivo que entrega en vacío alrededor de 2,9V respecto al negativo. Con el capacitor de 47uF se consigue cortar las frecuencias de corte a partir de 0,2Hz.

<image src="Ross_Compressor/referencia.png"  alt="referencia.png" >

## Buffer de entrada 

<image src="Ross_Compressor/buffer_entrada.png"  alt="buffer_entrada.png" >

El buffer de entrada está formado con un transistor

R1 y C4 cortan a 1060Hz, por ello C4  (ARREGÑLAR) !!!!!!)

C3 acopla las altas frecuencias 


deja pasar las frecuencias por encima de 50Hz aproximadamente






## Ganancia y polarizacion del OTA 

<image src="Ross_Compressor/ganancia.png"  alt="ganancia.png" >




### Equivalente en continua 

<image src="Ross_Compressor/equivalente_continua.png"  alt="equivalente_continua.png" >

Thevening --> convertir a modelo T

### Equivalente en alterna

<image src="Ross_Compressor/equivalente_alterna.png"  alt="equivalente_alterna.png" >

<image src="Ross_Compressor/eq_entrada.png"  alt="ecualizacion_entrada.png" >

baja frecuencia: salida al 12% 








Rampa de frecuencia de 1kHz a 9kHz



GANANCIA TOTAL :  900*2/17 = 106
 
### Ganancia Continua




La etapa de ganancia del


Corriente de salida y ganancia diferencial:


$ i_{O}  = \frac{I_{POL}}{2 \cdot V_{T}} v_{dif}  ~~~~~~~~~~~ ~~~~~~~~~~~ ~~~~~~~~~~~~~~~~ corriente ~~ salida $

$ A_{O} = R_{CARGA} \cdot \frac{i_{O}}{v_{diff}} \equiv R_{16} \cdot \frac{I_{POL}}{2 \cdot V_{T}} \le 900 ~~~~~~~~~~~~ ganancia $

La ganancia de continua del amplificador de transconductancia es de ¡900 veces! la tensión entre sus pines de entrada.

Desde el punto de vista de laseñal


### Polarizacion

Si R9 y R14 tienen un disbalance del 10% la tension de error introducida será de :
- 210mV(en vacio)
- **450uV** (con R10 y R11 en medio)

Errores de salida:

$ |V_{O(V_{OS})}| = A_{O} \cdot V_{OS}  ~~~~~~~~~~~~ (tension ~~ offset)$




$ |V_{O(I_{BIAS})}| \leq  \frac{A_{O} \cdot  (R_{10}+R_{11}) \cdot } {10} \cdot I_{BIAS} ~~~~~~~~~~~~ (corriente ~~ polarizacion)$

$ |V_{O(I_{OS})}| \approx  A_{O} \cdot \frac{(R_{10}+R_{11})}{2} \cdot I_{OS}     ~~~~~~~~~~~~ (corriente ~~ offset)$


Se calculan los rangos de error de salida típicos debidos a cada fuente de error del integrado CA3080:

| Parámetro | Valor tipico | Error salida (tipico) |
| :---: |:---:| :---:|
| $V_{OS}$  |  $ \pm 0.4mV $|  $ \pm 400mV $ |
| $I_{BIAS}$ | $ 2uA $ | $ \pm 400mV $  |
| $I_{OS}$  | $ \pm 0,12uA $   |  $ \pm 120mV $    |

Se observa que el error total de salida díficilmente supere el voltio de desviación, por ello el circuito funcionará bien la gran mayoría de las veces sin necesidad de hacer ajustes ni reemplazar componentes

Los errores de salida máximos debidos a cada tipo de error son:

| Parámetro | Valor maximo | Error salida (maximo) |
|:---:|:---:|:---:|
| $V_{OS}$| $ \pm 5mV $|  $ \pm 5V $  |
| $I_{BIAS}$ |  $ \pm 5uA $ | $ \pm 1V $ |
| $I_{OS}$  | $ \pm 0,6uA $ |   $ \pm 600mV $ |

En este caso el error debido a la tensión de offset puede anular por completo el funcionamiento del OTA al empujar su salida a sus valores límite, saturando el dispositivo. Para estas circunstancias 



IABC = 500μA

Estos datos de la hoja de datos asumen una corriente de polarizacion de 500μA. En el circuito real esta corriente no supera los 300uA. 

### Trimmer corrección 

El trimmer ayuda a corregir el error debido a la tensión de offset de entrada al introducir un disbalance controlado entre las entradas del OTA.

$ |V_{correccion}| \le  \frac{R_{TRIM}}{R_{9}+2 \cdot (R_{12}+R_{13})}  \cdot V_{CC}   \approx 10mV $

El valor de corrección máxima es de 10mV, más que suficientes para compensar la tensión de ofset de entrada. 

Cabe destacar que el trimmer no permite compensar los errores debidos a las corrientes de polarización de entrada y de corriente de offset porque éstos varían dramáticamente durante el funcionamiento del circuito.



## Detector de Envolvente y Correccion de Ganancia

<image src="Ross_Compressor/detector_envolvente.png"  alt="detector_envolvente.png" >

### Deteccion de amplitud

La salida del OTA se envia a una etapa a transistores que añade buffer e inversion de señal. Del emisor del transistor Q2 se obtiene una réplica de baja impedancia que alimentará tanto al detector de pico positivo como al potenciometro de volumen, en tanto que el colector producirá una réplica invertida que excitará al detector de picos negativos.

Los dos bloques detectores de picos son circuitalmente idénticos.

- C13 y C15 hacen los acoplamientos de alterna 

- R19 y R22 referencian la señal de entrada al negativo.

- Q3 y Q4 detectan los picos positivos y conducen de forma apreciable a partir de los 500mV.

- D1 y D2 conducen durante los picos negativos , paliando parcialmente el desplazamiento de nivel.

El desplazamiento de señal se debe a que las junturas base-esmisor de los transistores usados no conducen con la misma facilidad que las junturas de los diodos en antiparalelo.


<image src="Ross_Compressor/buffer_detectores.png"  alt="buffer_detectores.png">


Nótese que la señal inversa producida por R18 es ligeramente mayor que la de R17 debido a que por R18 pasa también la corriente del circuito de volumen, el cual exige un 17% de corriente adicional


400mV de pico

desplazamiento de nivel de +150mV



## Correccion de ganacia

Los dos detectores de amplitud inyectan pulsos de corriente al circuito RC de R21 y C14, los cuales controlan a su vez la tensión de control de la etapa de ganancia.

<image src="Ross_Compressor/pulsos_vcontrol.png"  alt="pulsos_vcontrol.png">

- Durante el pico inicial casi toda la corriente proveniente de los transistores es absorbida por C14, haciendo que éste se descargue progresivamente y empujando así la tensión de control hacia el negativo;

- Cuando se entra en la etapa de *sustain* los pulsos de corriente decaen en amplitud dramáticamente y sólo absorberán parcialmente la corriente media de R21, por lo que comienza una subida lenta de la tensión de C14 y de la tensión de control;

- Cuando la señal de salida cae por debajo del umbral los pulsos de corriente desaparecen y la resistencia R21 carga progresivamente a C14 hasta que éste alcance la tensión de alimentación. El resultado es una exponencial decreciente con una constante de tiempo RC de 1,5 segundos.







## Dinamica de salida

La tensión de control es directamente proporcional a la ganancia del OTA. 

Ajustando el potenciómetro de volumen para que el volumen de la señal clean de guitarra sea el mismo que el del sustainer

<image src="Ross_Compressor/vcontrol_salida.png"  alt="vcontrol_salida.png" >

En resumen, los efectos del sustainer sobre la señal son:

- Estabilizar la amplitud durante la etapa de sustain ;
- Si la ganancia es suficiente, prolongar temporalmente el sustain.

Como contrapartida:
- Remarca el pico al comienzo de la señal (*rise*);
- Aumenta el ruido de fondo debido a la ganancia que introduce el efecto.

## Notas sucesivas

# TASA COMPRESION


# ACORDES



