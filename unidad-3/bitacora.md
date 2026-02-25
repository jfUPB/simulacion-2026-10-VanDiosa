# Unidad 3

## Bitácora de proceso de aprendizaje

### Actividad 01   
📤Luego ver el video con la [charla de Robert Hodgin](https://www.youtube.com/watch?v=vmUodu6K-bA)   

✍️Primero que todo lo que mas me gusto fue que el señor robert, siendo un teso, admite que se bajoneo al ver que una ia hacia en segundos lo que a él le tomaba meses, preguntandose lo mismo q nosotros posiblemente nos hemos preguntado: ¿Para que nos matamos aprendiendo, estudiando, haciendo, si una maquina lo saca sin dificultad?

Como yo soy de la linea de animacion, este curso en especifico, he estado usando la ia para poder aterrizar las ideas que me vienen a la mente en cada unidad, para asi no trabarme tanto en la parte tecnica, considero que la forma adecuada de usar la ia, es como un compañero, una mano derecha, trabajar en conjunto, no simplemente tragar entero sin masticar, sin revisar, sin profundizar, sin corregir, ya que, lo que hace especial a las cosas es el proceso

### Actividad 02   
📤Seguir la actividad realizada en clase, en visual studio code. Y reportar en la bitacora las reflexiones de lo aprendido    

❓¿Por qué es necesario multiplicar la aceleración por cero en cada frame? ¿Por qué se multiplica por cero justo al final de update()?   

✍️La aceleracion son empujones que se reciben en ciertos momentos, por ejemplo el viento te empuja pero no se queda ahi pegado para siempre acelerandote infinitamente. Se usa: acceleration.mult(0), para restear la aceleracion y que en el siguiente frame se calculen fuerzas nuevas

❓Recuerda esta cuestión por favor: paso por valor y paso por referencia. En este caso, force es objeto de la clase p5.Vector, es decir, es un objeto que se pasa por referencia. ¿Qué implica esto?   
Entonces cómo debería ser el método applyForce para que funcione correctamente sin asumir que la masa es igual a 1?   

✍️Implica que cuando le pasamos el vector a la funcion applyForce, no se le pasa una copia si no que se altera directamente la vrble global. Por eso es que se usa: let f = p5.Vector.div(force, 10), para crear un vector nuevo (una copia)

### Actividad 03   
📤Luego de analizar el [material de clase](https://natureofcode.com/forces/#creating-forces), crear tres obras generativas para cada una de las siguientes fuerzas: Fricción, Resistencia al aire y fluidos, Atracción gravitacional

✍️[Friccion](https://editor.p5js.org/VanDiosa/sketches/70ebk7fMP)    
Partiendo de la base del texto, cree un ejemplo donde la friccion se viera ligada a un segmento en especifico de la suuperficie, y que ademas se pudiera recibir algun feedback mas visual cuando el objeto tocara ese segmento. Ademas cambie la interactividad del viento por que el usuario pueda lanzar de forma mas controlada el objeto y asi poder ver como actua este desde diferentes angulos y asi

✍️[Resistencia al aire y fluidos](https://editor.p5js.org/VanDiosa/sketches/ZpnR2Xik4)    
En este ejemplo, quise crear dos capas con diferentes coeficientes, para poder observar como cada objeto frenaba de diferente forma dependiendo de la densidad y la masa. De igual forma quice añadir un cambio de color para indetificar el tipo de fuerza que actuaba sobre ellos

✍️[Atracción gravitacional](https://editor.p5js.org/VanDiosa/sketches/QODbTH6Wn)   
Para el ultimo ejercicio, simplemente lo transforme para que se viera como una representacion orbital. Ademas le coloque transparencia al fondo, para poder ver el rastro del planeta, y tmb aumente la constante gravitacional para que el movimiento fuera mas dinamico

## Bitácora de aplicación 

## Bitácora de reflexión


