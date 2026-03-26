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
📤Luego de estudiar el  [Example 4.4: A System of Systems](https://natureofcode.com/particles/#example-44-a-system-of-systems), responder:

❓Comparación con Example 4.2:    
+ ¿Qué responsabilidades que antes estaban en draw() ahora están dentro de la clase Emitter?    
✍️Antes, el draw() tenia que ser el gestor y el creador. Ahora, esas tareas se encuentran en el emitter:
  + La gestion del array -> El emitter ahora es el dueño de la lista de particulas
  + El ciclo de limpieza -> El bucle for inverso, encargado de buscar las particulas muertas y eliminarlas con splice(), ahora vive dentro del emitter
  + Emision -> El método addParticle() se encarga de inyectar nuevos objetos al sistema

+ ¿Cuál es la ventaja de encapsular la lógica de emisión en una clase separada?    
✍️La ventaja principal es el aislamiento de la complejidad. Al mover la logica al Emitter, el programa principal (sketch) ya no necesita conocer los detalles internos de como funciona una particula o como se limpia la memoria, solo interactua con un gerente
  + Cada emisor puede tener su propia ubicacion, tasa de nacimiento y reglas de vida sin interferir con los demas
  + Se puede crear miltiples sistemas complejos con una sola linea de codigo, tratando al sistema de particulas como una unidad de nivel superior
  + Si se quiere cambiar por ejemplo el como mueren las particulas, solo se modifica la clase Emitter, y el cambio se aplica automaticamente a todos los sistemas activos en el sketch

+ En este ejemplo hay un array de emitters. ¿Quién crea los emitters? ¿Quién crea las partículas dentro de cada emitter?     
✍️El sketch.js crea los emitters -> Especificamente en la funcion mousePressed(). Cada clic genera un nuevo gerente de particulas en la posicion del mouse

  El Emitter crea las particulas dentro de su propio metodo addParticle() (El sketch ya no sabe como nace una particula, solo sabe que el emisor se encarga)

+ Dibuja un diagrama que muestre la jerarquía: sketch → [emitters] → [partículas]. ¿Cuántos niveles de “colección” hay?    
✍️

❓Transferencia conceptual:
+  Describe este ejemplo usando palabras que NO mencionen p5.js, JavaScript, ni ninguna herramienta específica. Usa solo términos como: entidad, estado, colección, emisor, ciclo de vida, fuerza   
✍️Tenemos una interfaz que reacciona a eventos. Cuando ocurre un evento, se genera un emisor en ese punto en especifico; este emisor es el responsable de gestionar un grupo dinamico de entidades

    El emisor gestiona el paso del tiempo para sus entidades... las produce de forma continua, les aplica fuerzas externas, y revisa constantemente su estado vital. Cuando una entidad agota su tiempo de vida, el emisor la saca del grupo para que el sistema no trabaje en vano. Esto permite que varios emisores operen al mismo tiempo, cada uno manejando su propia poblacion de de entidades de forma independiente

### Actividad 03   
📤Luego de estudiar el  [Example 4.5: A Particle System with Inheritance and Polymorphism](https://natureofcode.com/particles/#example-45-a-particle-system-with-inheritance-and-polymorphism), responder:

❓¿Qué tienen en común las subclases de partículas? ¿Qué tienen de diferente?    
✍️En comun -> Todas comparten el estado fisico (posicion, velocidad, aceleracion) y el estado vital (lifespan). Ademas comparten la logida del moviemnto (update, applyForce) y la condicion muerte (isDead)

Diferente -> Lo que cambia es la nueva capa de visualizacion. Mientras que la particula base dibuja un circulo estatico, la subclase confetti sobrescribe el metodo show() para dibujar un cudarado que rota segun su posicion

❓¿Por qué es importante que el Emitter no necesite saber qué tipo específico de partícula está gestionando? Explica esto con tus propias palabras.    
✍️Es importante porque permite que el sistema se agenerico. El emitter solo sabe que tiene una lista de objetos que saben correr y/o morir. Si el emitter tuviera que preguntar si es un circulo o un confetti aantes de cada accion, el codigo seria gigante y frgil. Al tratar a todas como una simple particula, el codigo se mantiene limpio y funcional sin importar que tan loca sea la apariencia de cada una

❓Si mañana quisieras agregar un tercer tipo de partícula, ¿Qué tendrías que crear y qué NO tendrías que modificar?    
✍️ Se tendria que crear una nueva clase y definir su propio metodo show(). Tambien un else if en el metodo addParticle() del emitter para que empiece a generarlas

  No se debe modificar el metodo run() del emitter, la logica del sketch.js, ni la clase particle original. En general el sistema de actualizacion y limpieza de memoria seguiria funcionando exactamente igual

❓Compara con Example 4.2: ¿Cambió la lógica del Emitter? ¿Cambió la lógica de muerte? ¿Qué capa del sistema se modificó y cuáles permanecieron intactas?    
✍️La logica del emitter no cambio, ya que sigue siendo un bucle que recorre un array hacia atras. Solo cambio el omento del nacimienot (addParticle) para aasi poder elegir entre dos tipos

La logica de la muerte tampoco cambio, ya que sin importan que tipo de particula sea, mueren cuando su lifespan es menor a cero

Se modifico la capa de visualizacion al crear el confetti, y ligeramente la capa de estructura para permitir la creacion aleatoria de distintos tipos. La capa de comportamiento fisico y vida, permanecio intacta

### Actividad 04   

## Bitácora de aplicación 


## Bitácora de reflexión
