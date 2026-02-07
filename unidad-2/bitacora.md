# Unidad 2

## Bitácora de proceso de aprendizaje


## Bitácora de aplicación 
### Actividad 01
📤Exploración de artistas que usan vectores y movimiento

❓Qué trabajo te gustó más y por qué?    

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
✍️

❓¿Para qué sirve el método normalize()?   
✍️

❓Te encuentras con un periodista en la calle y te pregunta ¿Para qué sirve el método dot()? ¿Qué le responderías en un frase?   
✍️

❓El método dot() tiene una versión estática y una de instancia. ¿Cuál es la diferencia entre ambas?   
✍️

❓Ahora el mismo periodista curioso de antes te pregunta si le puedes dar una intuición geométrica acerca del producto cruz. Entonces te pregunta ¿Cuál es la interpretación geométrica del producto cruz de dos vectores? Tu respuesta debe incluir qué pasa con la orientación y la magnitud del vector resultante.   
✍️

❓¿Para que te puede servir el método dist()?   
✍️

❓¿Para qué sirven los métodos normalize() y limit()?   
✍️

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
📤

### Actividad 08
📤


## Bitácora de reflexión



