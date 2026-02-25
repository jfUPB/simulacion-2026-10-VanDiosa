# Unidad 1

## Bitácora de proceso de aprendizaje
### Actividad 01
📤Piensa y describe en una sola frase y en tus propias palabras cómo la aleatoriedad influye en el arte generativo.     
En el [video sobre Tyler](https://www.youtube.com/watch?si=vJd_8lXJ5X__litL&v=8tTGJvijoDw&feature=youtu.be) entendi que la aletoriedad en el arte generativo permite que el artista seda parte del control al algoritmo, al sistema, consiguiendo de esa forma que las obras tengan resultados naturales al ser inesperados

### Actividad 02
📤Partiendo del codigo de ejemplo: Example 0.1: A Traditional Random Walk del [texto guía].(https://editor.p5js.org/natureofcode/sketches/5C69XyrlsR)

✍️Al modificarlo espero que el circulo se desplazara unicamente hacia la derecha y hacia abajo, ya q modifique las opciones para que produzcan todas el mismo tipo de desplazamiento

⭐[Codigo modificado](https://editor.p5js.org/VanDiosa/sketches/zoZvnQZru)

```js
/* ORIGINAL
  step() {
    const choice = floor(random(4)); //floor: funcion para redondear hacia abajo, random es de 1 a 4 sin incluir el 4
    if (choice == 0) {
      this.x++;
    } else if (choice == 1) {
      this.x--;
    } else if (choice == 2) {
      this.y++;
    } else {
      this.y--;
    }
  }
}
*/
  

step() { // VARIANTE QUE HICE
    const choice = floor(random(4));
    if (choice == 0) {
      this.x++;
    } else if (choice == 1) {
      this.x++; <=CAMBIO DE SIGNO
    } else if (choice == 2) {
      this.y++;
    } else {
      this.y++; <=CAMBIO DE SIGNO
    }
  }
}
```

✍️Al ejecutar el codigo se genero una trayectoria diagonal. Si cocurrio lo que esperaba pq elimine los movimientos negativos en ambos ejes, por lo que ya no habia un balance en las probabilidades de aletoriedad, paso de ser un movimiento aleatorio a uno dirigido

### Actividad 03
📤Analizando este [ejemplo](https://p5js.org/reference/p5/randomGaussian/)

¿Cuál es la diferencia entre una distribución uniforme y una no uniforme de números aleatorios?    
✍️Una distribucion uniforme da la misma probabilidad a todos los valores posibles mientras q la no uniforme favorece o tiene preferencias por ciertos valores, de esta forma hace q algunos resultados ocurran con mayor frecuencia que otros sin eliminar la aleatoriedad

⭐[Codigo modificado](https://editor.p5js.org/VanDiosa/sketches/H50eJOlq9) de la caminata aleatoria para que utilice una distribución no uniforme, favoreciendo el movimiento hacia la derecha

```js
/*ORIGINAL:
  step() {
    const choice = floor(random(4));
    if (choice == 0) {
      this.x++;
    } else if (choice == 1) {
      this.x--;
    } else if (choice == 2) {
      this.y++;
    } else {
      this.y--;
    }
  }
*/
  step() {
  let r = random(1); //se quita el floor ya q no necesitamos redondear valores

    if (r < 0.5) {
      this.x++;//50% de probabilidad derecha
    } else if (r < 0.7) {
      this.x--;//20% izquierda
    } else if (r < 0.9) {
      this.y++;//15% abajo
    } else {
      this.y--;//15% arriba
    }
  }
}
```

### Actividad 04
📤Analizando este [ejemplo](https://natureofcode.com/random/#example-04-a-gaussian-distribution)

⭐[Sketch en p5.js](https://editor.p5js.org/VanDiosa/sketches/z6BGZ2dyG) que representa una distribución normal de otra forma. El profe nos dijo q partieramos del ejemplo y lo modificaramos, asi quedo el codigo:

```js
function setup() {
  createCanvas(640, 240);
  background(255);
}

function draw() {
  //{!1} A normal distribution with mean 320 and standard deviation 60
  // let x = randomGaussian(320, 60); //primer argumento media, segundo es la desviacion
  let x = randomGaussian(320, 30);
  let r = randomGaussian(8,10);
  let y =randomGaussian(120,30);
  noStroke();
  fill(0, 10);
  //circle(x, 120, 16); // x,y,radio
  circle(x, y, r);
}
```
✍️En el ejemplo la posicion en x variaba segun randomGaussian(), por lo q la distribucion normal se visualizaba unicamente en el eje horizonal formando una linea que era mas densa en el centro

En la modificacion que hice, aplique la distribucion normal no solo en el ejex si no tambien en el eje y en el radio del circulo; de esta forma la visualizacion se transformo en una nube de puntos con mayor concentracion en el centro del canvas

<img width="349" height="146" alt="Unidad1Actividad4" src="https://github.com/user-attachments/assets/96b099dc-40e4-4251-bebf-bb53af213c3d" />

### Actividad 05
📤Luego de analizar el concepto de [Lévy flight](https://natureofcode.com/random/#a-custom-distribution-of-random-numbers)

✍️Parti del ejemplo de [caminata aleatoria tradicional](https://editor.p5js.org/natureofcode/sketches/5C69XyrlsR), donde el walker se movia con pasos constantes y una distribución uniforme en todas las direcciones, lo que provocaba que visitara muchas veces las mismas zonas del espacio

✍️Use Levy flight para que el walker no se moviera siempre igual y pudiera dar saltos largos de vez en cuando. Esperaba obtener un movimiento donde apesar de predominar los pasos pequeños, aparecen algunos desplazamientos grandes que cambian la zona de exploracion, lo cual se ve reflejado en la diferencia entre los puntos rojos (pasos cortos) y negros (saltos largos) del sketch

```js
let walker;

function setup() {
  createCanvas(640, 240);
  walker = new Walker();
  background(255);
  
  frameRate(15); // velocidad
}

function draw() {
  walker.step();
  walker.show();
}

class Walker {
  constructor() {
    this.x = width / 2;
    this.y = height / 2;
    
    this.lastStep = 0; // almacena el tamaño del ultimo paso
  }

  show() { //MODIFICADO
    strokeWeight(4); //tamaño del punto para mejor visibilidad

    if (this.lastStep > 30) {
      stroke(255, 0, 0); // pasos pequeños: rojo. comun
    } else {
      stroke(0); // saltos largos: negro. raro
    }

    point(this.x, this.y);
  }

  step() { //MODIFICADO
    // tamaño del paso:
    let stepSize = this.acceptReject() * 100;
    this.lastStep = stepSize;
    // direccion: 
    let angle = random(TWO_PI);
    // movimienot:
    this.x += cos(angle) * stepSize;
    this.y += sin(angle) * stepSize;

    // evita que se salga del canvas
    this.x = constrain(this.x, 0, width);
    this.y = constrain(this.y, 0, height);
  }

  acceptReject() { //NUEVO
   while (true) {
      let r1 = random(1); // posible tamaño
      let r2 = random(1); // numero que decide
      if (r2 < r1) { 
        return r1;// se acepto r1
      }
    }
  }
}
```

⭐[Sketch en p5.js](https://editor.p5js.org/VanDiosa/sketches/_NlisBze4)

<img width="389" height="151" alt="Unidad1Actividad5" src="https://github.com/user-attachments/assets/082c5ab8-c90a-48a1-bc8e-96b0b1244e71" />

### Actividad 06
📤Luego de analizar el concepto de [ruido Perlin](https://natureofcode.com/random/#a-smoother-approach-with-perlin-noise)

✍️Parti de: [A graph of Perlin noise values over time](https://editor.p5js.org/VanDiosa/sketches/VDoKo4Zjf). 

✍️Para esta actividad pense en comparar directamente el ruido aleatorio con el ruido Perlin en un mismo sketch, de esta forma podria terminar de comprender los conceptos y sus diferencias. Arriba se muestran valores generados con random() y abajo con noise(). Esto permite ver como el ruido Perlin genera movimientos suaves y continuos, mientras que el ruido uniforme produce cambios y movimientos impredecibles

```js
let t = 0; //vrble tiempo para el perlin

function setup() {
  createCanvas(640, 240);
  background(255);
}

function draw() {
  // RANDOM (arriba)
  let xr = random(width); // #random entre 0 y 640
  fill(0, 50);
  noStroke();
  circle(xr, 60, 8);

  // PERLIN (abajo)
  let xp = map(noise(t), 0, 1, 0, width); // noise(t): #entre 0 y 1, pero con el map se transforma ese rango a 0-640
  fill(0, 50);
  circle(xp, 180, 8);

  t += 0.01;
}
```

⭐[Sketch en p5.js](https://editor.p5js.org/VanDiosa/sketches/_NlisBze4)

<img width="255" height="92" alt="Unidad1Actividad6" src="https://github.com/user-attachments/assets/3b80fe51-d103-4f03-8121-fb1acae320f6" />

## Bitácora de aplicación 
### Actividad 07 🛩️
✍️¿Que es una obra generativa?    
Es aquella q por lo menos una parte es creada por un sistema autonomo. Es un tipo de arte, donde el artista no dibuja linea por linea d eforma manual, si no, que diseña el conjunto de reglas/algoritmos y cede parte del control al pc

✍️Mi obra generativa:    
+ Distribucion normal (Gaussiana): La utilizo para definir el tamaño de los aviones y su velocidad maxima. La mayoria tiene un tamaño promedio, pero aparecen algunos mas grandes y lentos, otros mas pequeños y rapidos, de esta forma visualmente no es una poblacon uniforme
  
+ Perlin noise: Lo aplique para generar el viento, hace que este cambiando de direccion de forma organiza y suave para que los aviones vuelen con naturalidad
  
+ Levy flight: Lo use para generar unos eventos como de teletransportacion. Hay una probabilidad baja de que un avion se detenga, cargue como energia volviendose rojo, y haga un salto largo y rapido

+ Interactividad: Con el mouse al presionarlo se genera un campo de atraccion alterando el viento y atrayendo los aviones hacia el puntero. Ademas el color de los aviones cmabia segun la orientacion de este, si los muevo para la derecha cambian a tonos calidos y si los muevo para la izquierda se vuelven tonos frios


```js
let planes = [];
let zoff = 0; // vrble del tiempo para el perlin noise y evitar que se estatico
let flowField = [];
let resolution = 20; // cuadricula del viento
let cols, rows; // columnas, filas

function setup() {
  createCanvas(windowWidth, windowHeight);
  cols = floor(width / resolution);
  rows = floor(height / resolution);
  flowField = new Array(cols * rows); // array para almacenar la direccion del viento

  // CREACION DE AVIONES, DISTRIBUCION NORMAL ------------
  for (let i = 0; i < 100; i++) {
    let pSize = randomGaussian(12, 7); // media 12 y desviacion 7
    pSize = constrain(pSize, 4, 25); // para q no sean ni enanos ni gigantes
    planes.push(new PaperPlane(pSize));
  }
  background(240);
}

function draw() {
  background(240, 25); 

  let yoff = 0;
  for (let y = 0; y < rows; y++) {
    let xoff = 0;
    for (let x = 0; x < cols; x++) {
      let index = x + y * cols;
      
      // PERLIN NOISE ------------------------------------
      let angle = noise(xoff, yoff, zoff) * TWO_PI * 2; // noise() valor entre 0 y 1, se multiplica para generar un angulo de giro
      let v = p5.Vector.fromAngle(angle); // creacion de flecha con el angulo
      v.setMag(0.4); // fuerza del viento
      flowField[index] = v;
      
      xoff += 0.1; // pasos del viento, 0.1 para q sea suave
    }
    yoff += 0.1;
  }
  zoff += 0.005; // al cambiarlo, el viento rota suave en el siguiente frame

  // CICLO DE VIDA DE LOS AVIONES ------------------------
  for (let plane of planes) { // si no esta saltando, sigue el flujo normal
    if (!plane.isPreparingJump) {
      plane.follow(flowField); // sigue el viento
      if (mouseIsPressed) plane.attract(mouseX, mouseY); // atraccion con el mouse
    }
    plane.update(); // calcula nueva posicion
    plane.edges(); // si se sale de la pantalla aparece por el otro lado
    plane.show();
  }
}

class PaperPlane {
  constructor(pSize) {
    this.pos = createVector(random(width), random(height)); // posicion inicial
    this.prevPos = this.pos.copy(); // copia de la posicion inicial para el origen de la linea roja
    this.vel = createVector(0, 0); // vo=0
    this.acc = createVector(0, 0); // fo=0
    this.pSize = pSize; // tamaño dado por el random gaussian
    
    this.maxSpeed = map(pSize, 4, 25, 7, 2); // pequeño, grande, vel pequeño, vel grande
    
    // Estados levy:
    this.isPreparingJump = false;
    this.jumpTimer = 0; // tiempo faltante para saltar
    this.justJumped = false;
  }

  // LEVY  -------------------------------------------------
  levyLogic() {
    this.justJumped = false;

    // Probabilidad del 0.3% de que empiece un salto
    if (!this.isPreparingJump && random(1) < 0.003) {
      this.isPreparingJump = true;
      this.jumpTimer = 20; // Se queda quieto por 20 frames
    }

    if (this.isPreparingJump) {
      this.vel.mult(0); // Se queda quieto mientras carga
      this.acc.mult(0);
      this.jumpTimer--;
      
      // TELETRANSPORTACIÓN
      if (this.jumpTimer <= 0) {
        this.prevPos = this.pos.copy(); // Guardamos donde estaba justo antes del salto
        let jump = p5.Vector.random2D().mult(random(60, 120));
        this.pos.add(jump);
        this.isPreparingJump = false;
        this.justJumped = true; // Para dibujar la estela un frame
      }
    }
  }
  
// LECTOR DEL VIENTO --------------------------------------
  follow(vectors) {
    let x = floor(this.pos.x / resolution);
    let y = floor(this.pos.y / resolution);
    let index = constrain(x + y * cols, 0, flowField.length - 1);
    this.applyForce(vectors[index]); // aplicar la fuerza del viento
  }

  applyForce(force) {
    this.acc.add(force); // sumar fuerzas a la aceleracion
  }

 // ATRACCION MOUSE ------------------------------------
  attract(mx, my) {
    let force = p5.Vector.sub(createVector(mx, my), this.pos); // crear flecha del noise hacia el mouse
    force.setMag(0.7);
    this.applyForce(force);
  }

  update() {
    this.levyLogic(); // Maneja la pausa y el salto
    
    if (!this.isPreparingJump) {
      this.vel.add(this.acc);
      this.vel.limit(this.maxSpeed); // para no superar tamaño
      this.pos.add(this.vel);
      this.acc.mult(0);
    }
  }

  // DIBUJO Y ESTETICA ------------------------------------
  show() {
    // Efecto de salto (Rojo)
    if (this.justJumped) {
      stroke(255, 0, 0, 200); 
      strokeWeight(2);
      line(this.prevPos.x, this.prevPos.y, this.pos.x, this.pos.y);
    }

    push();
    colorMode(HSB, 360, 100, 100, 100); // Cambiamos temporalmente a modo artistico para que el amarillo sea fácil de sacar
    translate(this.pos.x, this.pos.y); // Mover el origen al avion
    rotate(this.vel.heading()); // Rotar segun la dirección del vuelo
    
    let thick = map(this.pSize, 4, 25, 0.5, 3); // controlar grosor segun el tamaño del avion
    strokeWeight(thick);
    
    if (this.isPreparingJump) {
      stroke(0, 100, 100); // Rojo en HSB
      fill(0, 100, 100, 30);
    } else {
      // COLOR SEGÚN DIRECCIÓN:
      // Si va a la derecha (cos +) es amarillo, a la izquierda (cos -) es azul.
      let angle = this.vel.heading(); 
      let hu = map(cos(angle), -1, 1, 200, 45); 
      stroke(hu, 70, 80, 60); // Color, Saturación, Brillo, Opacidad
      noFill();
    }
    
    // Forma del avion:
    beginShape();
    vertex(this.pSize * 1.5, 0);
    vertex(-this.pSize, -this.pSize / 2);
    vertex(-this.pSize / 2, 0);
    vertex(-this.pSize, this.pSize / 2);
    endShape(CLOSE);
    
    pop();
    colorMode(RGB, 255); // Volvemos a RGB para no dañar el resto del sketch
  }
  
  // Comportamiento de bordes (Efecto estela)
  edges() {
    if (this.pos.x > width) this.pos.x = 0;
    if (this.pos.x < 0) this.pos.x = width;
    if (this.pos.y > height) this.pos.y = 0;
    if (this.pos.y < 0) this.pos.y = height;
  }
}

function windowResized() {
  resizeCanvas(windowWidth, windowHeight);
  cols = floor(width / resolution);
  rows = floor(height / resolution);
  flowField = new Array(cols * rows);
}
```

⭐[Sketch en p5.js](https://editor.p5js.org/VanDiosa/sketches/DjNyb2Obn)

<img width="733" height="364" alt="Unidad1Actividad7" src="https://github.com/user-attachments/assets/5077499f-d7ab-4b76-a74d-fe518d64c34c" />

## Bitácora de reflexión

### Actividad 08

✍️Diferencia entre random() y noise()    
+ random() genera valores impredecibles, sin relacion entre uno y el otro. Como son numeros independientes visualmente se producen movimientos bruscos
+ noise() genera valores que cambian de forma suve y continua. Siguen siendo numeros impredecibles pero con un cambio gradual que se ve visualmente ordenado

random() lo usaria para generar caos, quiebres o variaciones drasticas, y noise() lo usaria cuando quiero movimientos naturales (viento, agua, etc) y organicos

✍️¿Que es una distribucion de probabilidad?. Caminada aleatoria: distribucion uniforme vs distribucion normal
Una distribucion de probabilidad es que tan probable es que ocurra ciertos valores dentro de un conjunto de datos, no todos los valores aparecen con la misma frecuencia
+ Distribucion uniforme: Todos los valores tienen la misma probabilidad, por lo que los resultados son parejos y repetitivos
+ Distribucion normal: los valores se concentran en un promedio, por lo q los valores de los extremos aparecen pocas veces. Los resultados son mas organicos y variados

✍️¿Cuál es el papel de la aleatoriedad en el arte generativo?
En el arte generativo la aleatoriedad es fundamental pq permite que la obra no sea igual a otra y que el sistema pueda tener de alguna forma autonomia. Entre las funciones que cumple esta:
+ Evitar patrones rigidos a traves de una variacion visual
+ Simular comportamientos naturales

✍️Aleatoriedad usada en la actividad 7
En la obra que realice combine diferentes tipos de aleatoriedad. Hablando de uno en especifico, destaco el del levy flight, hay una probabilidad muy baja de que uno de los aviones se detenga, recargue y haga un salto muy largo y rapido

Considero que fue una eleccion adecuada, ya que destaca entre el movimiento continuo del resto de la obra por ser un momento de sorpresa visual. La mayoria de los aviones se compartan de manera fuida pero de vez en cuando ocurre el evento inesperado lo que atrae la atencion del espectador

✍️¿Qué es una caminata (walk) y qué hace especial al Lévy flight?
Una caminata en simulacion es un modelo donde hay un objeto que se desplaza paso a paso siguiento ciertas reglas q contienen un grado de aleatoriedad

Una caminata de tipo ley flight se caracterisa porque combina muchos movimientos cortos con unos pocos saltos largos. Genera trayectorias irregulares, asi como se pueden ver en la naturaleza. En mi obra este tipo de caminata la evidencia con los momentos de teleltransportaccion, rompiendo el movimiento continuo del resto de aviones
