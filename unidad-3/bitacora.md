# Unidad 3

## Bitácora de proceso de aprendizaje

### Actividad 01   
📤Luego ver el video con la [charla de Robert Hodgin](https://www.youtube.com/watch?v=vmUodu6K-bA)   

✍️Primero que todo lo que mas me gusto fue que el señor robert, siendo un teso, admite que se bajoneo al ver que una ia hacia en segundos lo que a él le tomaba meses, preguntandose lo mismo q nosotros posiblemente nos hemos preguntado: ¿Para que nos matamos aprendiendo, estudiando, haciendo, si una maquina lo saca sin dificultad?

Como yo soy de la linea de animacion, este curso en especifico, he estado usando la ia para poder aterrizar las ideas que me vienen a la mente en cada unidad, para asi no trabarme tanto en la parte tecnica, considero que la forma adecuada de usar la ia, es como un compañero, una mano derecha, trabajar en conjunto, no simplemente tragar entero sin masticar, sin revisar, sin profundizar, sin corregir, ya que, lo que hace especial a las cosas es el proceso

## Bitácora de aplicación 
### Actividad 02   
📤Seguir la actividad realizada en clase, en visual studio code. Y reportar en la bitacora las reflexiones de lo aprendido    

❓¿Por qué es necesario multiplicar la aceleración por cero en cada frame? ¿Por qué se multiplica por cero justo al final de update()?   

✍️La aceleracion son empujones que se reciben en ciertos momentos, por ejemplo el viento te empuja pero no se queda ahi pegado para siempre acelerandote infinitamente. Se usa: acceleration.mult(0), para restear la aceleracion y que en el siguiente frame se calculen fuerzas nuevas

❓Recuerda esta cuestión por favor: paso por valor y paso por referencia. En este caso, force es objeto de la clase p5.Vector, es decir, es un objeto que se pasa por referencia. ¿Qué implica esto?   
Entonces cómo debería ser el método applyForce para que funcione correctamente sin asumir que la masa es igual a 1?   

✍️Implica que cuando le pasamos el vector a la funcion applyForce, no se le pasa una copia si no que se altera directamente la vrble global. Por eso es que se usa: let f = p5.Vector.div(force, 10), para crear un vector nuevo (una copia)


## Bitácora de reflexión

