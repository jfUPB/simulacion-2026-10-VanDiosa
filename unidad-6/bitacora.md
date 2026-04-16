# Unidad 6
## Bitácora de proceso de aprendizaje
### Actividad 01
📤Seleccionar dos imágenes o piezas de Tyler Hobbs, responder...   

✍️[Pieza 1: New Space #4 (Philodendron)](https://www.tylerxhobbs.com/works/new-space)     
<img width="923" height="341" alt="ACT1_1B" src="https://github.com/user-attachments/assets/2057921c-94ef-449d-a0b6-9298d5e2ec45" />

+ Composición: Es horizontal, tiene tres sillas dispuestas en el espacio. Dos estan agrupadas a la izquierda y la otra esta mas aislada a la derecha, como si hubiera una pareja y por otro lado un individuo
+ Densidad: La mayor densidad de tinta se encuentra en el marco de las sillas, donde el trazado es como mas cerrado que da la aparecia de q esas zonas son mas solidas. Por otro lado, las lineas que conectan y rodean las sillas son mas ligeras
+ Dirección del movimiento: El flujo no es lineal, si no que las lineas parecen como que se enrredas en objetos solidos invisibles, las lineas parecen vibrar
+ Color: Monocromatico negro. Creo que el color es clave, ya que, elimina las distracciones para que el ojo se centre en la textura y la forma
+ Ritmo: Da la impresion de un ritmo nervioso, sin fluidez, con trazos cortos que se enrredan, con frecuencia en las zonas donde se queria mayor densidad o intereses
+ Repetición y variación: A pesar de que la estructura de la silla se repite tres veces, la variacion del algoritmo permite que el ruido de los trazos sea distinto 
  
¿Por que esas decisiones son potentes?    
Creo que las decisiones que se tomaron lograron que la pieza se viera mas humana, usar un objeto tan cotidiano como unas sillas y dibujarlas con lineas caoticas da una sensacion como de fragil

(Hipotesis) ¿Que tipo de reglas o sistema podria estar detras de esta pieza?    
Pienso que es algo parecido a lo visto en la clase, de las corrientes invisibles, estas guiarian cada trazo. Tal vez se tiene una base invisible de la silla y el algoritmo dibuja sobre esta pero siguiendo una regla de desorden sonde la linea se pueda desviar de la forma

✍️[Pieza 2: Fidenza #725](https://www.tylerxhobbs.com/works/fidenza)    
<img width="182" height="216" alt="ACT1_2" src="https://github.com/user-attachments/assets/09d88b3e-cf10-42e3-b0ad-ad1fb0ac6245" />

+ Composición: Es de pantalla completa, muy saturada. No hay un pto de enfoque, el ojo puede viajar por todo el canva siguiendo como las curvas
+ Densidad: Es una pieza de alta densidad, no hay casi espacios vacios. Se puede ver que los bloques de colores estan apretados, generan mucha textura, y da una impresion de relieves
+ Dirección del movimiento: Se ve claramente que esta siguiendo un campo de flujo como los que vimos en clase. No hay lineas rectas, solo curvas y organizas, remolinos, corrientes, por todo el canva
+ Color: Se uso una paleta muy variada sobre un fondo color cremita. Los colores en pequeños bloqes me recordo a como la luz atraviesa los vitrales de las iglesias
+ Ritmo: Es un ritmo rapido, vibrante, con constante interrupcion por el cambio de colores
+ Repetición y variación: Hay una unidad basica que es un rectangulo, al cual se le varia el color, el ancho, y el angulo de giro

¿Por que esas decisiones son potentes?    
Siento que lograron que el codigo no se sienta frio, si no por el contario, calido, tanto asi, que me recordo como mencione anteriormente a los vitrales de las iglesia. La variacion de color hace que la pieza no se sienta como algo plano, si no que hay una luz detras de la pantalla 

(Hipotesis) ¿Que tipo de reglas o sistema podria estar detras de esta pieza?     
Al igual que la pieza anterior, hay un campo de flujo, que en este caso se usa para dibujar los rectangulos variables. La regla clave pienso que es el que el sistema decide aleatoriamente cada cuanto aparece un color dentro de cada linea de flujo. Tmb hay una especie de profunidad como, entonces puede que haya una regla donde los trazos mas gruesos destacan mas que los delgados

### Actividad 02   
📤En base al [capitulo 5 de libro The Nature of Code](https://natureofcode.com/autonomous-agents/), responder:

❓¿Qué es un agente autónomo?    
Un agente autonomo es un elemento que tiene su propio cerebro. El agente no se deja llevar como una particula comun, si no que tiene la capacidad de observar su entorno, procesa la informacion que adquiere y toma una decision en base a eso de a donde quiere ir

❓¿Qué es una steering force?    
Se traduce como fuerza de direccion. No es una fuerza que simplemente empuja, si no que es el resultado de una resta de vectores (Steering = Velocidad deseada - Velocidad actual). Tiene la funcion de darle direccion al movimiento actual para alinearse con la musion del agente

❓¿En qué se diferencia una steering force de fuerzas como gravedad, viento o fricción?    
Por un lado las fuerzas externas son vectores que se imponen desde el entorno, son globales y constantes sobre todos los objetos. Y las steering forces, son vectores que se generan internamente en cada agente, ajustan la dinamica segun la intencion que tenga cada uno

❓¿Por qué estas ideas son utiles para diseñar comportamiento visual?   
Al usar reglas de direccion en lugar de trayectorias fijas, el movimiento resultante no es una linea predecible, si no uno comportamiento que va evolucionando. Facilita el diseño de visuales que se sientan mas organicos, vivos y capaces de responder a estimulos externos


### Actividad 03   
📤Estudiar la seccion [Flow Fields](https://natureofcode.com/autonomous-agents/#flow-fields) y responder   

❓¿Cómo está construido el campo de flujo?   
Se construye sobre una rejilla invisible que cubre todo el lienzo, a cada celda se le asigna un angulo de direccion, normalmente usando un perlin noise para que los cambios de direccion sean suaves y no saltos aleatorios

❓¿Qué representa cada celda o vector del campo?   
Cada celda es como una señal de transito, que contiene un vector unitario que le indica a todo agente que pase por ahi hacia donde debe girar. Es una estructura tipo corriente

❓¿Cómo usa un agente su posición para consultar el campo?   
El agente toma sus coordenadas, las mapea para saber en que celda se encuentra y lee el vector de esa posicion especifica

❓¿Cómo se convierte el vector consultado en una decisión de movimiento?    
El vector consultado se convierte en la velocidad deseada del agente. Luego se aplica la formula que se menciono antes: Steering = Velocidad deseada - Velocidad actual, para que el agente gire suavemente hacia esa direccion en lugar de moverse de golpe

✍️Parametros importantes del sistema:
+ Resolucion -> Es el tamaño de cada celda, si la resolucion es alta (hay muchas celdas pequeñas), el flujo es mas detallado; por lo contrario si la resolucion es baja, el movimiento se ve mas rigido
+ MaxSpeed -> Es la velocidad maxima a la que puede ir el agente
+ MaxForce -> Es que tan fuerte puede girar el agente. Si es bajo, el agente tiene una curva de firo amplia; si es alto los agentes reaccionan instantaneamente al flujo
+ Cantidad de agentes -> Define la densidad. Pocos agentes crean lineas solas, miles de agnetes revelan la estructura completa del canva
+ Noise Step (xoff/yoff) -> Define que tan suave o caotico es el cambio de direccion en el espacio

✍️Realiza al menos una [modificación](https://editor.p5js.org/natureofcode/sketches/egribz8WV) y analiza el efecto visual que produce:    
La modificacion que hice fue en flowfield.js -> let angle = map(noise(xoff, yoff), 0, 1, 0, TWO_PI*4); -> multipliqué el ángulo final por 4. Este genero que los agentes tiendan a dar vueltas en circulos cerrados, ya que se forman unos espirales dentro de las corrientes. Paso de parecer un rio a un sistema de pequeños remolinos interconectados

❓¿Qué tipo de movimiento produce este algoritmo?   
Produce un movimiento logico pero organico. Se siente que fluye bajo las leyes de la naturaleza (aire, magnetismo, agua...) donde hay orden pero no repeticiones exactas

❓¿Qué sensaciones visuales te sugiere?   
Sugiere fluidez, serenidad y complejidad. Esta la sensacion de que hay algo invinsible organizando el caos

❓¿En qué tipo de pieza musical imaginas que podría funcionar bien?   
Lo primero que se me ocurre es musica Lo-fi, ya que los agentes tienen el mismo rimo constante, relajado y repetitivo con variaicones sutiles. Creo q tambien podria funcionar con musica ambiental, donde el sonido no tiene estructuras rigidas si no capas de texturas


### Actividad 04
📤Estudiar la seccion [Flocking](https://natureofcode.com/autonomous-agents/#flocking) y responder 

✍️Explica con tus palabras las tres reglas básicas:   
+ Separación -> Evita que los agentes choquen entre si. Cada agente mira a sus vecinos y si estan muy cerca, aplican una fuerza hacia el lado opuesto para mantener su espacio personal
+ Alineación -> Esta regla permite que cada agente mire hacia donde se estan moviendo sus vecinos, para luego ajustar su velocidad con el objetivo de apuntar en la misma direccion que los otros
+ Cohesión -> Mantiene unidos a los agentes. Cada uno calcula el centro de masa de sus vecinos (como conjunto) y aplica una fuerza para moverse hacia ese centro, evitando que el grupo se vea disperso

✍️Identifica qué parámetros controlan estas reglas   
+ Pesos -> En boid.js -> sep.mult(), ali.mult() y coh.mult() -> Cada una de las reglas tiene una importancia diferente, por ejemplo la separacion puede PESAR mas que la cohesion, por lo tanto el grupo se veria mas espaciado
+ neighborDistance -> En las funciones align y cohere -> Este valor define que tan lejos un agente puede ver a sus vecinos. Entre mas grande el radio, mas coordinado y masivo el grupo
+ desiredSeparation -> En la regla separate -> Este valor define el tamaño de la burbuja personal de cada agente
+ MaxSpeed y MaxForce -> Definen que tan rapido se mueven y que tan bruscos son sus giros al momento de seguir las reglas

✍️Modifica uno o más pesos del [sistema](https://editor.p5js.org/natureofcode/sketches/IkpBw96Sd) y describe el efecto visual y colectivo    
En boid.js, cambie los pesos de sep.mult() para tener mucha separacion, y de coh.mult() para tener casi que 0 de cohesion

Antes:
```js
    sep.mult(1.5);
    ali.mult(1.0);
    coh.mult(1.0);
```
Despues:
```js
    sep.mult(5.0);
    ali.mult(1.0);
    coh.mult(0.1);
```
El efecto visual que obtuve fue que el sistema paso de ser un grupo unido a tener agentes que rebotan violentamente entre ellos y evitan formar grupos. Fue un comportamiento disperso y caotico

✍️Describe el comportamiento emergente observado    
Al probar el codigo original, se puede ver un comportamiento fuido y estable. Se forman grupos que se mueven como si siguieran una mision, en caso de que uno se separa rapidamente busca otro grupo cercano al cual integrarse

❓¿Qué atmósfera visual produce el flocking?    
Produce una atmosfera cooperativa y de vida organica. Sentia que observaba un sistema natural (de pajaros, peces, insectos...) donde no hay un lider, ya que todos saben que hacer. Da una sensacion de constante movimiento y armonia

❓¿En qué tipo de relación con una canción podría funcionar mejor este algoritmo?    
Pienso que funcionaria muy bien con una cancion que tenga una estructura con muchas armonias vocales... Se me ocurre alguna cancion de kpop ya que tienen coreografias donde todos se meuven como un todo pero manteniendo una distancia, o musica clasica con varios violines o instrumentos de cuerda

### Actividad 05   
📤

## Bitácora de aplicación 


## Bitácora de reflexión
