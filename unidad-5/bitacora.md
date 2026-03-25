# Unidad 5
## Bitácora de proceso de aprendizaje
### Actividad 01   
📤Luego de estudiar el [Example 4.2: An Array of Particles](https://natureofcode.com/particles/#example-42-an-array-of-particles), responder:

❓Capa de comportamiento:
+ ¿Qué propiedades tiene cada partícula? Clasifícalas: ¿Cuáles definen su estado físico? ¿Cuáles su estado vital?   
✍️Cada particula tiene las siguientes propiedades:
  + Estado fisico -> position, velocity, acceleration. Son los vectorers que definen donde esta y hacia donde va
  + Estado vital -> lifespan. Es una variable escalar que empieza en 255.0 , actua como el reloj biologico de cada particula

+ ¿Qué condición determina que una partícula “muere”? ¿Es una muerte instantánea o gradual?   
✍️En este codigo que analizamos, la muerte es gradual en su valor (lifespan -=2), pero instantanea en su eliminacion. El metodo llamado isDead() chequea si el contador llego a cero

+ ¿Cómo se actualiza la partícula en cada frame? Identifica el patrón motion 101 dentro de la partícula   
✍️Este patron esta dentro del update(). La aceleracion suma a la velocidad, la velocidad a la posicion, y se usa acceleration.mult(0) para limpiar las fuezas en cada frame

❓Capa de estructura:
+ ¿Quién crea las partículas? ¿En qué momento?    
✍️Las particulas se crean en el draw() usando particles.push(new Particle(...)). Esto significa que nace una particula nueva en cada frame

+ ¿Quién decide cuándo eliminar una partícula del array?   
✍️En el draw(), hay un gestor, el cual pregunta a cada particula con la funcion isDead() y decide usar splice(i,1) para borrarla de la cadena (array)

+ ¿Por qué se recorre el array en orden inverso para eliminar? ¿Qué pasaría si no se hiciera así?   
✍️Al usar splice para eliminar un elemento, los indices de los elementos que quedan se desplazan hacia la izquierda. Si se recorre el array hacia adelante, por ejemplo al borrar el elemento 3, el que era el 4 pasa a ser el 3. En la siguiente iteracion, el bucle salta al 4 originalr, saltandose un elemento sin revisar     

  Sabiendo lo anterior, al veir desde el final, si se borra el i, los que cambian de indice son los que estan despues del i, los cuales ya fueron procesados

+ Si no eliminaras nunca las partículas, ¿Qué pasaría con la memoria y el rendimiento? Haz el experimento: comenta la línea que elimina y observa el frame rate   
✍️Al comentar esta linea: particles.splice(i, 1); el array crece infinitamente. En pocos segundos se tiene muchos objetos en la RAM, la CPU del pc trata de calcular la fisica de particulas q ni se alcanzan a ver, por lo que los FPS caen drasticamente congelando el navegador

❓Capa de visualización:
+ ¿Qué elementos visuales usa para representar una partícula?      
✍️En este caso solo se usa un circulo relleno de gris

+ ¿Cómo se conecta el “tiempo de vida” con la apariencia visual?     
✍️Se usa this.lifepan para el canal Alpha (transparencia) en fill() y en stroke(), para que a medidad que la particula muera, se vaya desvaneciendo suvemente

+ Si quisieras cambiar la representación visual (por ejemplo, usar líneas en vez de círculos), ¿Qué cambiarías y qué NO cambiarías?    
✍️Se cambia simplemente la funcion circle() por line(), en el metodo show(). No se toca ni el movimiento, ni el array, ni los calculos de muerte, ya que se busca cambiar solo loe stetico


### Actividad 02   

### Actividad 03   

### Actividad 04   

## Bitácora de aplicación 


## Bitácora de reflexión
