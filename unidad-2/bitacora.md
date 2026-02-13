# Unidad 2

## Bitácora de proceso de aprendizaje

### Actividad 01
📤Exploración de artistas que usan vectores y movimiento

❓Qué trabajo te gustó más y por qué?  
✍️El q mas me llamo la atencion y me gusto fue Legion (2022/2023) de Raven Kwok. Me parecio muy interesante como se uso la tecnologia para convertir el cuerpo humano en un sisteme de particulas vivo. Visualmente me parece muy llamativo como se pudo usar los vectores para generar esa experiencia donde las figuras de los cuerpos interactuan entre si y se deforman

Lo que mas me gusto fue q no es una animacion sin mas, si no que se van capturando las poses reales cada segundo, de esta forma el espectador es parte del sistema

### Actividad 02
📤Analizando el ejemplo: [Example 1.2: Bouncing Ball with Vectors](https://natureofcode.com/vectors/#example-12-bouncing-ball-with-vectors)

❓¿Cómo funciona la suma dos vectores en p5.js?    
✍️ En p5.js los vectores no son simples numeros si no objetos con varios componentes (x, y), por eso mismo no se pueden sumar comun y corriente. Para sumar vectores se usa .add(). Ejemplo:

position.add(velocity) -> Aqui internamente lo que se hace es sumar componente por componente, position.x + velocity.x  & position.y + velocity.y 

Se podria hacer usando cuatro variables pero de este modo solo usamos dos objetos

❓¿Por qué esta línea position = position + velocity; no funciona?   
✍️En p5.js se usa JavaScript y ese lenguaje el operador + solo sabe sumar numeros o juntar textos. Position y velocity son objetos(vectores), el lenguaje no sabe como mezclarlos entonces va a lanzar errores pq intenta convertirlos en texto, por eso es que usamos el .add()

### Actividad 03
📤Tomar uno de los ejemplos de random walks del Capítulo 0 y conviértalo en vectores de uso. Parti del [Example 0.1](https://natureofcode.com/random/#example-01-a-traditional-random-walk)

❓¿Qué tuviste que hacer para hacer la conversión propuesta?   
✍️ Se debia de reemplazar las variables this.x y this.y por un objeto this.position que fuera creado con createVector(). Luego en step() en lugar de sumar las variables se usa el .add() para asi actualizar la posicion

⭐[Sketch modificado](https://editor.p5js.org/VanDiosa/sketches/QloCyuy-z)   
```js
// The Nature of Code
// Daniel Shiffman
// http://natureofcode.com

let walker;

function setup() {
  createCanvas(640, 240);
  walker = new Walker();
  background(255);
}

function draw() {
  walker.step();
  walker.show();
}

class Walker {
  constructor() {
    this.position=createVector(width/2, height/2); //sustiuir los componentes por un vector
  }

  show() {
    stroke(0);
    //point(this.x, this.y);
    point(this.position.x, this.position.y);
  }

  step() {
    let stepDirection = createVector(0,0); //Vector para la direccion
    const choice = floor(random(4));
    
    // nuevo if
    if (choice == 0) {
      stepDirection.x = 1;
    } else if (choice == 1) {
      stepDirection.x = -1;
    } else if (choice == 2) {
      stepDirection.y = 1;
    } else {
      stepDirection.y = -1;
    }
    
    //suma de los vectores direccion y velocidad
    this.position.add(stepDirection)
  }
}

```


### Actividad 04
📤Experimentar con el siguiente codigo:
```js
let position;

function setup() {
    createCanvas(400, 400);
    position = createVector(6,9);
    console.log(position.toString());
    playingVector(position);
    console.log(position.toString());
    noLoop();
}

function playingVector(v){
    v.x = 20;
    v.y = 30;
}

function draw() {
    background(220);
    console.log("Only once");
}
```
⭐[Sketch](https://editor.p5js.org/VanDiosa/sketches/DIB-yaKPT)   

❓¿Qué resultado esperas obtener en el programa anterior?   
✍️Que el primer console.log muestre (6, 9) y el segundo tmb, pensando que la funcion playingVector recibe una copia y no modifica el vector original

❓¿Qué resultado obtuviste?   
<img width="389" height="102" alt="image" src="https://github.com/user-attachments/assets/12436436-7b14-4992-b7f9-cd980875a307" />    
✍️La funcion playingVector si modifico directamente el vector original, lo cual podemos ver en el segundo console.log

❓Recuerda los conceptos de paso por valor y paso por referencia en programación.   
✍️Paso por valor -> Crea una copia nueva del dato. Se puede cambiar la copia y el original seguiria igual

Paso por referencia -> No se crea una copia, si no que se comparte como una direccion del objeto original, si se edita la direccion el cambio se ve reflejado en el original

❓¿Qué tipo de paso se está realizando en el código?   
✍️Se realiza un paso por referencia. Al pasar position a la funcion, le estamos dando permiso de entrar y modificar sus coordenadas internas (x,y) directamente en la memoria

❓¿Qué aprendiste?   
✍️Aprendi que en JavaScript, los vectores son objetos y se manejan por referencia. Si quiero que una funcion use un vector sin alterar el original, debo enviarle una copia usando .copy(), algo asi: playingVector(position.copy());

### Actividad 05
📤Explorar el concepto de la clase [p5.Vector](https://p5js.org/reference/p5/p5.Vector/)

❓¿Para qué sirve el método mag()? Nota que hay otro método llamado magSq(). ¿Cuál es la diferencia entre ambos? ¿Cuál es más eficiente?   
✍️mag() -> Calcula la longitud/magnitud del vector usando pitagoras
magSq() -> Calcula esa misma longitud pero al cuadrado (sin sacar la raiz cuadrada)

La diferencia es q magSq() nos ahorra el calculo de la raiz cuadrada, es mucho mas eficiente puesto que la raiz cuadrada es una operacion matematica costosa

❓¿Para qué sirve el método normalize()?   
✍️Sirve para convertir cualquier vector en un vector unitario (de magnitud 1) sin cambiar su direccion

❓Te encuentras con un periodista en la calle y te pregunta ¿Para qué sirve el método dot()? ¿Qué le responderías en un frase?   
✍️Es una forma de medir que tanto se encima o alinean dos vectores, y asi saber si aputan acia el mismo lado, si son perpendiculares o si tienen direcciones opuestas

❓El método dot() tiene una versión estática y una de instancia. ¿Cuál es la diferencia entre ambas?   
✍️Instancia -> v1.dot(v2) -> Se llama desde un vector ya creado. Devuelve un numero (el producto punto), pero no modifica los valores de v1
Estatica -> p5.Vector.dot(v1, v2) -> Es una funcion general que recibe dos vectores, los compara y da un resultado sin necesidad de q se llamen el uno al otro

❓Ahora el mismo periodista curioso de antes te pregunta si le puedes dar una intuición geométrica acerca del producto cruz. Entonces te pregunta ¿Cuál es la interpretación geométrica del producto cruz de dos vectores? Tu respuesta debe incluir qué pasa con la orientación y la magnitud del vector resultante.   
✍️El resultado es un nuevo vector que es perpendicular al plano formado por los dos originales
+ Orientacion: sigue la regla de la mano derecha (determina si el vector va hacia "arriba" o "abajo" del plano)
+ Magnitud: El tamaño del vector resultante es igual al area del paralelogramo que forma los dos vectores originales

❓¿Para que te puede servir el método dist()?   
✍️Sirve para calcular la distancia en pixeles entre dos puntos representados por vectores

❓¿Para qué sirven los métodos normalize() y limit()?   
✍️normalize() -> Reduce la fuerza del vector a 1 para estandarizar la direccion
limit() -> Pone un limite a la magnitud. Si el vector supera el maximo que se le coloca, lo recorta a ese tamaño; si es menor lo deja igual

### Actividad 06
📤Modificar el siguiente codigo para generar este resultado:

```js
function setup() {
    createCanvas(100, 100);
}

function draw() {
    background(200);

    let v0 = createVector(50, 50);
    let v1 = createVector(30, 0);
    let v2 = createVector(0, 30);
    let v3 = p5.Vector.lerp(v1, v2, 0.5);
    drawArrow(v0, v1, 'red');
    drawArrow(v0, v2, 'blue');
    drawArrow(v0, v3, 'purple');
}

function drawArrow(base, vec, myColor) {
    push();
    stroke(myColor);
    strokeWeight(3);
    fill(myColor);
    translate(base.x, base.y);
    line(0, 0, vec.x, vec.y);
    rotate(vec.heading());
    let arrowSize = 7;
    translate(vec.mag() - arrowSize, 0);
    triangle(0, arrowSize / 2, 0, -arrowSize / 2, arrowSize, 0);
    pop();
}
```

⭐[Codigo modificado](https://editor.p5js.org/VanDiosa/sketches/Bu3K0DqLU)   

❓¿Cómo funciona lerp() y lerpColor().   
✍️ Ambas funciones se relacionan con la interpolacion lineal, o sea, su objetivo es encontrar un valor intermedio entre dos extremos

+ lerp(): Calcula un numero que esta a una distancia X entre el inicio y el fin. Por ejemplo el caso del codigo modificado se usa para calcular la posicion del vector 3 

+ lerpColor(): En lugar de calcular numeros simples, interpola componentes de color (RGBA). En el codigo de esta actividad se usa para que el vector cambie de azul a rojo mientras de desplaza

❓¿Cómo se dibuja una flecha usando drawArrow()?   
✍️Es una funcion personalizada que usa matrices y sus transformaciones, para evitar calculos matematicos dificiles. Los pasos que realiza son:
1. Traslada el origen a donde se quiere dibujar la flecha
2. Dibuja el cuerpo de la flecha desde el nuevo origen
3. Rota el lienzo en la direccion de la fleca
4. Dibuja la punta con un triangulo al final de la linea
5. Limpia con push y pop para resetear el lienzo

### Actividad 07
📤Leer la seccion del texto guía llamada [Motion with vectors](https://natureofcode.com/vectors/#motion-with-vectors) (marco de movimiento llamado motion 101) y el [ejemplo 1.7](https://natureofcode.com/vectors/#example-17-motion-101-velocity). Luego, reesponder:

❓¿Cuál es el concepto del marco motion 101 y cómo se interpreta geométricamente?
✍️Es un sistema de 3 pasos que se repiten:
1. La aceleracion se suma a la velocidad
2. La velocidad se le suma a la posicion
3. Se dibuja el objeto en esa nueva posicion

✍️Geometricamente lo que entendi e imagino es q el movimiento se puede construir como una flecha en un mapa. La posicion es el origen de donde sale todo, la velocidad (la linea) es el segmento que dice que tan largo es el paso y hacia donde va, y la aceleracion (la punta o cabeza) es la que dirige y jala el cuerpo hacia la nueva direccion

❓¿Cómo se aplica motion 101 en el ejemplo?
✍️En el ejemplo 1.7 aplico usando una clase llamda Mover, para que de esta forma el objeto tenga su propio cerebro. Se divide en tres:
+ Constructor -> Se crean los tres vectores: position, velocity, aceleration; y se inicializan con valores aleatorios o constantes pequeñas
+ Metodo update() -> aqui ocuree el sistema, cada que el programa se actualiza la aceleracion cambia a la velocidad y la velocidad mueve el punto de posicion
+ Metodo show() -> aqui se toma el vector position y se dibuja el circulo ahi

Por otro lado en update() ocurre la logica: 
```js
this.velocity.add(this.acceleration); // La aceleración cambia la velocidad
this.velocity.limit(10);              // Evitamos que gane velocidad infinita
this.position.add(this.velocity);     // La velocidad cambia la posición
```
En el metodo show() se dibuja la forma en las coordenadas actuales de: this.position.x y this.position.y

En el ejemplo ejemplo 1.8 el motion 101 se aplica integrando la clase al flujo principal del programa:
+ En setup() -> nace el objeto y se ejecutan las configuracion del constructor
+ En draw() -> se crea el ciclo del movimiento d ela siguiente forma:
  1. mover.update(): el objeto ejecuta la logica de aceleracion->velocidad->posicion
  2. mover.checkEdges(): aqui se aplica una regla extra para el objeto al salir de la pantalla aparezca del otro lado
  3. mover.show(): se renderiza el resultado final en el lienzo

### Actividad 08
📤¿Qué observaste cuando usas cada una de las aceleraciones propuestas?   
✍️ Al experimentar con los tres algoritmos, observe los siguientes comportamientos:    

+ Aceleracion Constante: (continuando con el ejemplo del carro) el objeto me parece que se mueve como si su mortor estuviera siempre en la misma direccion, ademas al inicio arranca lento pero luego va ganando como velocidad. Su movimiento fue mecanico y predecible
+ Aceleracion Aleatoria: el objeto se ve como si estuviera nervioso, la aceleracion cambia en cada frame por lo que el objeto cambia de direccion constantemente. Comparandolo con el random walker siento que este se siente un poco mas fluido y natural, ya q la aceleracion cambia gradualmente por lo que se parece al movimiento que haria un insecto
+ Aceleracion hacia el mouse: el objeto persigue el cursor, me parecio interesante que no se queda quieto sobre el cursor si no q orbita al rededor de el. Da la sensacion de un iman, al ser un movimiento dinamico y como intencionado

## Bitácora de aplicación   

## Bitácora de reflexión







