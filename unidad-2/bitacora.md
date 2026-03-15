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
### Actividad 09 : Latidos de Oro 💛    

✍️ Concepto de Latidos de Oro   
Latidos de oro explora la estética de la vulnerabilidad y la resiliencia a través de la técnica japonesa del [Kintsugi](https://psicologiaymente.com/cultura/kintsugi-psicologia-de-resiliencia-en-cultura-japonesa). En esta obra, el corazón se presenta como un sistema dinámico formado por hilos de energía que oscilan entre el orden y la entropía (la tendencia natural de un sistema hacia el desorden y la pérdida de estructura).

La obra destaca que la belleza no reside en la perfección inicial, sino en la capacidad de reconstruirse. Al interactuar con ella, el espectador se convierte en un agente del caos; sin embargo, es a través de esa ruptura provocada que el sistema transforma sus hilos rojos en cicatrices de oro. El propósito es recordar que lo recuperado tras una crisis posee un valor superior a lo original

✍️Reglas aplicadas para la aceleracion   
Utilicé el marco Motion 101 (Aceleración → Velocidad → Posición) aplicando tres reglas distintas de manipulación para la aceleración:

+ Aceleración Aleatoria (Caos): Al presionar C, las partículas reciben una aceleración basada en vectores aleatorios (p5.Vector.random2D()). Esto genera una dispersión explosiva y elimina el orden inicial

+ Aceleración Atractiva (Reconstrucción): Al soltar la tecla, se calcula la aceleración como la diferencia entre la posición actual y la fórmula del corazón. Esto crea una fuerza de retorno que sutura la forma
  
+ Aceleración por Ruido (Perlin Noise): Para que el corazón no se viera estático, el punto de destino de cada partícula se desplaza constantemente usando noise(). Esto genera un efecto visual de pulsacion biologica, de latido

✍️Interacción y Memoria   
La obra tiene memoria, ya que se uso una interpolación lineal (lerp) para que el oro aparezca progresivamente. Mientras más tiempo se mantenga la tecla (C) presionada, más dorada se vuelve la estructura al reconstruirse. Al soltar la tecla, las partículas buscan de nuevo la posición del mouse mediante una aceleración atractiva. Sin embargo, no se detienen en seco; debido a su velocidad, los fragmentos entran en una órbita constante alrededor del puntero

⭐[Sketch](https://editor.p5js.org/VanDiosa/sketches/ghsjehJwT)   
```js
let fragmentos = [];
let cantidad = 500; // Poblacion de particulas
let nivelOro = 0; // Contador para el kintsugi, transicion de color

function setup() {
  createCanvas(windowWidth, windowHeight);
  colorMode(HSB, 360, 100, 100, 100); // HSB -> tono, saturacion, brillo
  
  for (let i = 0; i < cantidad; i++) {
    fragmentos.push(new Fragmento(i));
  }
}

function draw() {
  background(240, 60, 3, 15); // Fondo con alpha bajo para la estelas de mov

  //-----------------------CAOS, INTERACTIVIDAD TECLADO-----------------------
  let esCaos = keyIsPressed && (key === 'c' || key === 'C');

  if (esCaos) {
    nivelOro = lerp(nivelOro, 100, 0.003); // Incremento progresivo del color oro
  }

  //-----------------------CICLO DE VIDA DE LOS FRAGMENTOS-----------------------
  for (let f of fragmentos) {
    f.update(esCaos); // Calcula la logica de aceleracion->velocidad->posicion (Motion 101)
    f.show(esCaos); // 3. Se dibuja el objeto en su nueva posicion
  }
}

class Fragmento {
  constructor(index) {
    this.pos = createVector(random(width), random(height)); // Posicion inicial
    this.vel = p5.Vector.random2D(); // Velocidad aleatoria inicial
    this.acc = createVector(); // Aceleracion aleatoria inicial
    this.index = index;
    this.maxSpeed = 8; // Limite de velocidad
    
    //-----------------------COLOR INICIAL-----------------------
    if (random(1) > 0.07) { // 7%
      this.miColor = random(340, 360); // 93% -> Rojos
    } else {
      this.miColor = random(180, 300); // 7% -> Colores sorpresa
    }
  }

  update(caos) {
    //-----------------------MANIPULACION ACELERACION-----------------------
    if (caos) {
      // ACELERACIÓN ALEATORIA: Caos
      this.acc = p5.Vector.random2D().mult(random(6));
    } else {
      // ACELERACIÓN ATRACTIVA: Corazón
      let t = map(this.index, 0, cantidad, 0, TWO_PI);
      let x = 16 * pow(sin(t), 3);
      let y = -(13 * cos(t) - 5 * cos(2 * t) - 2 * cos(3 * t) - cos(4 * t));
      
      // PERLIN NOISE: Genera el latido
      let variacion = noise(frameCount * 0.03, this.index * 0.1) * 15;
      let target = createVector(x * (14 + variacion/10) + mouseX, y * (14 + variacion/10) + mouseY);
      
      // RESTA DE VECTORES: para la atraccion de orbita al mouse
      let dir = p5.Vector.sub(target, this.pos);
      dir.setMag(0.9); // Magnitud de la fuerza de atraccion
      this.acc = dir;
    }

    //-----------------------APLICACIÓN MOTION 101-----------------------
    this.vel.add(this.acc); // 1. La aceleracion se suma a la velocidad
    this.vel.limit(this.maxSpeed); // No superar la vel maxima
    this.pos.add(this.vel); //2. La velocidad se le suma a la posicion
    this.vel.mult(0.94); // Friccion de la orbita, moderar el mov
    this.acc.mult(0); // Reset de aceleracion para el siguiente frame
  }

  show(caos) {
    if (caos) {
      stroke(this.miColor, 90, 100, 100); // Estetica de particulas como chispas
      strokeWeight(random(1, 2.5));
    } else {
      let probOro = map(nivelOro, 0, 100, 2, 80); // LÓGICA KINTSUGI: Probabilidad de volverse oro según nivelOro
      
      if (random(100) < probOro) {
        stroke(48, 80, 100, 90); 
        strokeWeight(map(nivelOro, 0, 100, 2, 4)); // Oro más grueso
      } else {
        stroke(this.miColor, 75, 85, 75); // Color rojo base
        strokeWeight(2);
      }
    }
    
    // DIBUJO DE ESTELA: Línea desde posición actual hacia atrás según velocidad
    line(this.pos.x, this.pos.y, this.pos.x - this.vel.x * 1.6, this.pos.y - this.vel.y * 1.6);
  }
}
```

📸Algunas capturas
<img width="1919" height="794" alt="Captura de pantalla 2026-02-13 001634" src="https://github.com/user-attachments/assets/b1458e09-f6d0-4350-aabf-7b004bb37d67" />
<img width="1919" height="796" alt="Captura de pantalla 2026-02-13 001654" src="https://github.com/user-attachments/assets/d7ea8ed5-1000-419a-a828-c54b178c0b49" />
<img width="1919" height="798" alt="Captura de pantalla 2026-02-13 001724" src="https://github.com/user-attachments/assets/59bb035a-e059-4e5a-b0d8-0e3f5a7c796f" />


## Bitácora de reflexión
### Actividad 10: Magnetismo Cromático🧲   
✍️ Concepto de Magnetismo Cromático   
La obra generativa trata de explorar la identidad individual y la pertencia a un grupo. Esta inspirada en el concepto de Clusters de Jeffrey Ventrella, cada agente posee un color que determina su comportamiento social. Cuando se encuentran en reposo, los agentes muestran atraccion hacia el cursos, pero ante un estimulo se revelan y agrupan por afinidad cromatica buscando refugio en las esquinas

✍️Interacción      
La obra no es estática, depende totalmente de la presencia del usuario para evolucionar:
+ El usuario actúa como una fuerza gravitacional. El mouse es un centro de atracción, al hacer click, se activa el "Magnetismo Cromático", el cual fuerza a los agentes a migrar hacia sus esquinas. El uso del espacio actúa como un freno, permitiendo observar los detalles del movimienot

+ Inspirado en Jared Tarbell, el lienzo no se borra por completo en cada frame. Al usar una opacidad reducida en el fondo, la aplicación genera una memoria del movimiento

⭐[Sketch](https://editor.p5js.org/VanDiosa/sketches/eA0mvDqIS)   
```js
let agentes = [];
let cantidad = 45;
let gravedadGlobal = false;

function setup() {
  createCanvas(windowWidth, windowHeight);
  colorMode(HSB, 360, 100, 100, 100); // HSB -> tono, saturacion, brillo
  background(0);
  
  for (let i = 0; i < cantidad; i++) {
    agentes.push(new Agente());
  }
}

function draw() {
  background(240, 60, 3, 15); 

  fill(0, 0, 100, 60); 
  noStroke();
  textSize(14);
  text("TRIBUS: [CLICK] Cada color a su esquina | [G] Gravedad | [ESPACIO] Freno", 30, 40);
  
  //-----------------------CICLO DE LOS AGENTES-----------------------
  for (let a of agentes) {
    a.update();
    a.show();
  }
}

function keyPressed() {
  if (key === 'g' || key === 'G') {
    gravedadGlobal = !gravedadGlobal;
  }
}

class Agente {
  constructor() { // Inicializacion de Vectores (Motion 101)
    this.pos = createVector(random(width), random(height));
    this.vel = p5.Vector.random2D().mult(5);
    this.acc = createVector();
    this.maxSpeed = random(8, 15);
    this.maxForce = 0.8;
    
    //-----------------------LOGICA DE CLUSTERS-----------------------
    let r = random(1);
    if (r < 0.33) {
      this.hueBase = 190; // Azul
      this.esquina = createVector(0, 0); // Arriba Izquierda
    } else if (r < 0.66) {
      this.hueBase = 330; // Rosa
      this.esquina = createVector(width, 0); // Arriba Derecha
    } else {
      this.hueBase = 45;  // Naranja
      this.esquina = createVector(width / 2, height); // Abajo Centro
    }
    
    this.strokeW = random(15, 45); 
  }

 update() {
    let fuerza;
    
    if (gravedadGlobal) {
      fuerza = createVector(0, 0.5); // Fuerza constante hacia abajo
    } else {
      let mouse = createVector(mouseX, mouseY);
      
      if (mouseIsPressed) {
        // Repulsion al Mouse
        let irAEsquina = p5.Vector.sub(this.esquina, this.pos);
        irAEsquina.setMag(2.0); 
        
        let huirMouse = p5.Vector.sub(this.pos, mouse);
        huirMouse.setMag(1.5);
        
        fuerza = p5.Vector.add(irAEsquina, huirMouse);
      } else {
         // Atraccion al Mouse
        fuerza = p5.Vector.sub(mouse, this.pos);
        fuerza.setMag(1.0);
      }
    }

    // Freno
    if (keyIsPressed && key === ' ') {
      this.vel.mult(0.8); 
      fuerza.mult(0);
    }

    //-----------------------APLICACIÓN MOTION 101-----------------------
    this.acc.add(fuerza);
    this.vel.add(this.acc);
    this.vel.limit(this.maxSpeed);
    this.pos.add(this.vel);
    this.acc.mult(0);

    // Rebote de bordes
    if (this.pos.x < 0 || this.pos.x > width) this.vel.x *= -1;
    if (this.pos.y < 0 || this.pos.y > height) this.vel.y *= -1;
    this.pos.x = constrain(this.pos.x, 0, width);
    this.pos.y = constrain(this.pos.y, 0, height);
  }

  show() {
    let h = map(this.vel.mag(), 0, this.maxSpeed, this.hueBase + 20, this.hueBase - 20); // Color dinamico dependiendo de la vel
    // Estela de luz
    stroke(h, 80, 100, 12); 
    strokeWeight(this.strokeW);
    line(this.pos.x - this.vel.x, this.pos.y - this.vel.y, this.pos.x, this.pos.y);
    // Nucleo
    noStroke();
    fill(h, 70, 100, 30);
    circle(this.pos.x, this.pos.y, this.strokeW / 1.8);
  }
}
```

📸Algunas capturas
<img width="1919" height="790" alt="Captura de pantalla 2026-02-13 151444" src="https://github.com/user-attachments/assets/38cd0b2b-2c16-492a-92b8-7e0f460ff86b" />
Separacion por grupos:
<img width="1437" height="588" alt="Captura de pantalla 2026-02-13 151251" src="https://github.com/user-attachments/assets/86897817-819f-4610-889d-ae7b6b2e9e93" />
Gravedad:
<img width="1449" height="601" alt="Captura de pantalla 2026-02-13 151355" src="https://github.com/user-attachments/assets/71c361f1-df3b-4572-82c2-e318ed9d678d" />
Freno:
<img width="1918" height="777" alt="Captura de pantalla 2026-02-13 151549" src="https://github.com/user-attachments/assets/a6bbb4fa-e1f9-4da5-b2c9-9c690d7ab077" />







