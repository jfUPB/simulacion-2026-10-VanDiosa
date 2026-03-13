# Unidad 4

## Bitácora de proceso de aprendizaje
### Actividad 01   
📤Despues de revisar la obra de Memo Akten: [Simple Harmoni Motion](https://www.memo.tv/works/simple-harmonic-motion/). Los aspectos que más me llamaron la atencion fueron...     

✍️Lo q más me llamo la atencion de Memo es como logra que algo tan cuadriculado como las matematicas y el movimiento armmonico simple termine sintiendose como algo organico y vivo

Me parece muy interesante como la base de todo es una simple oscilacion como la de un pendulo, que al tener varios puntos con frecuencias desfasadas crea patrones que parecen coreografias. Adicional me gusta mucho que la musica no es un relleno, si no que el movimiento se ve sincronizado con las notas

### Actividad 02   
📤A partir de la primera simulacion relacionada con el [manejo de ángulos](https://editor.p5js.org/juanferfranco/sketches/R1iTVQjzm), responder:    

❓¿Qué está pasando en esta simulación? ¿Cuál es la interacción?   

✍️En esta simulacion se puede ver el dibujo de una barra con dos circulos en los extremos. La interaccion es a traves del teclado, cada que se presiona cualquier tecla, la variable angle aumenta 0.1 radianes haciendo que el objeto rote de a poco   

❓Nota que en cada frame se está trasladando el origen del sistema de coordenadas al centro de la pantalla. ¿Por qué crees que se hace esto?   

✍️Por defecto el origen (0,0) del canva se encuentra en la esquina superior izquierda. Si rotaramos desde ahi, el objeto giraria alrededor de la esquina, pareceria como una puerta; por ello se usa el traslate, para mover el origen al centor del canvas y de esta forma hacer q el objeto rote sobre su propio eje

❓Cuál es la relación entre el sistema de coordenadas y la función rotate().    

✍️rotate() siempre gira el sistema de coordenadas completo(el canva), no solo el dibujo. Es como si giraramos una hoja de papel sobre la que se ha dibujado, todo lo que se dibuja despues del rotate() saldra inclinado segun el angulo     

❓Observa que al dibujar los elementos gráficos parece que se está dibujando en la posición (0, 0) del sistema de coordenadas. ¿Por qué crees que se hace esto? y ¿Por qué aunque en cada frame se hace lo mismo, los elementos gráficos rotan?    

✍️Se dibuja en (0,0) porque tras el translate, ese punto ya es el centro de nuestra pantalla. Los elementos rotan aunque el codigo diga siempre siempre circle(50,0,...) ya que lo que cambia es la inclinacion del plano. Es mas facil decirle al objeto dibujate en el centro y girar el canva, que estas calculando en cada frame la posicion de cada punto    

📤Analizando la segunda simulcion relacionado con que un [objeto tenga un frente](https://editor.p5js.org/natureofcode/sketches/bZqHGYbRQ)

❓Identifica el marco motion 101. ¿Qué es lo que se está haciendo en este marco?   

✍️En esta simulacion en especifico:
1. Acumular fuerza en la aceleracion (la direccion hacia el mouse)
2. Sumar aceleracion a la velocidad
3. Limitar velocidad para que no se descontrole
4. Sumar velocidad a la posicion
5. Resetear la aceleracion    

❓¿Qué hace la función heading()?   

✍️Esta funcion toma un vector (en este caso especifico la velocidad) y nos dice exactamente cual es su ángulo de direccion en radianes. Es la que nos permite saber hacia donde esta mirando el objeto mientras se mueve

❓¿Qué hace la función push() y pop()? Realiza algunos experimentos para entender su funcionamiento.   

✍️push()->guarda el estado actual del sistema (posicion, rotacion, colores
pop()->restaura ese estado. Si se quitara esa linea, el siguiente translate() se sumaria al anterior y se acumularia sin parar

❓¿Qué hace rectMode(CENTER)? Realiza algunos experimentos para entender su funcionamiento.   

✍️Por defecto, p5.js dibuja los rectangulos desde la esquina superior izquierda (CORNER). Si intentamos rotar un rectangulo asi, el giro se veria cojo o desequilibrado porque el eje estaria en una esquina. rectMode(CENTER) hace que el punto (x, y) que le damos sea el corazón del rectangulo

Si lo cambiamos a CORNER, el rectangulo deja de girar como una helice centrada y parece que esta revoleando alrededor de un punto externo. Para efectos de esta simulacion, el CENTER es lo que permite que el objeto mantenga su eje de rotacion justo en el medio de su masa

❓¿Cuál es la relación entre el ángulo de rotación y el vector de velocidad? Trata de dibujar en un papel el vector de velocidad y cómo se relaciona con el ángulo de rotación y la operación de traslación y rotación.   

✍️La relacion es de orientacion. El vector de velocidad nos dice hacia donde se desplaza el objeto en el plano x, y. Para que el objeto parezca que mira hacia donde va, usamos velocity.heading() para extraer el ángulo de ese vector y se lo pasamos a rotate()

## Bitácora de aplicación 



## Bitácora de reflexión

