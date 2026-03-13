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

### Actividad 03   
📤Practicar creando una simulacion de un vehiculo(triangulo) que tenga un frente y se mueva en x con las teclas de flecha. Documentar el proceso de creacion    

✍️Primero se comenzo adaptando el movimiento de que el objeto en lugar de seguir el mouse se use la logica de movimiento con las flechas. Si se presiona la flecha izquierda se aplica una fuerza negativa en X y si se presiona la telca derecha una fuerza positiva. Aqui el triangulo se iria volando sin parar, por lo que era necesario limitar su velocidad, entonces se podria usar una fuerza de friccion en el update para que se sienta un vehiculo con peso: this.vel.mult(0.98)

Luego aprendi que en p5 el ángulo 0 apunta hacia la derecha en el eje x positivo, por lo que el triangulo no podria dibujarse hacia arriba, ya que al aplicarle rotacion se iria de lado. Es por eso que para que el heading funcione el dibujo debe de dibujarse mirando hacia la derecha, para que el triangulo rote correctamente

⭐[Sketch](https://editor.p5js.org/VanDiosa/sketches/oEFacef3i)

```js
let vehiculo;

function setup() {
  createCanvas(640, 360);
  vehiculo = new Vehiculo();
}

function draw() {
  background(240);

  if (keyIsDown(LEFT_ARROW)) {
    let fuerza = createVector(-0.1, 0);
    vehiculo.applyForce(fuerza);
  }
  if (keyIsDown(RIGHT_ARROW)) {
    let fuerza = createVector(0.1, 0);
    vehiculo.applyForce(fuerza);
  }

  vehiculo.update();
  vehiculo.checkEdges();
  vehiculo.show();
}

class Vehiculo {
  constructor() {
    this.pos = createVector(width / 2, height / 2);
    this.vel = createVector(0, 0);
    this.acc = createVector(0, 0);
    this.maxSpeed = 5;
    this.r = 10; // Tamaño del vehículo
  }

  applyForce(f) {
    this.acc.add(f);
  }

  update() {
    this.vel.add(this.acc);
    this.vel.limit(this.maxSpeed);
    this.pos.add(this.vel);
    this.acc.mult(0); // Motion 101: Reset de aceleración
    
    // Friccion para que no deslice infinitamente
    this.vel.mult(0.98); 
  }

  show() {
    let angle = this.vel.heading(); // Calcula el ángulo según la velocidad

    push();
    translate(this.pos.x, this.pos.y); // Trasladar al centro del objeto
    rotate(angle); // Rotar según el ángulo de la velocidad
    
    // Dibujo del triángulo apuntando a la derecha (eje X positivo)
    fill(127, 100, 255);
    stroke(0);
    strokeWeight(2);
    triangle(this.r * 2, 0, -this.r, -this.r, -this.r, this.r);
    pop();
  }

  checkEdges() {
    if (this.pos.x > width) this.pos.x = 0;
    else if (this.pos.x < 0) this.pos.x = width;
  }
}
```

### Actividad 04   
📤Luego de analizar la simulacion sobre [Motion 101 con fuerzas](https://editor.p5js.org/juanferfranco/sketches/jebkEAUpR). Responder las preguntas:   

❓¿Qué modificación hay que hacer al motion 101 cuando se quiere agregar fuerzas acumulativas? Trata de recordar por qué es necesario hacer esta modificación   

✍️El marco Motion 101 basico es aceleracion -> velocidad -> posicion. Sin embargo, cuando trabajamos con fuerzas acumulativas, no podemos simplemente igualar la aceleracion a una fuerza (como this.acceleration = force), porque si hay varias fuerzas actuando al tiempo (gravedad, viento, atracción), se borrarian unas a otras

En el codigo se usa this.acceleration.add(f) para ir sumando todos los empujones que recibe el objeto en un solo frame. Al final del update(), es obligatorio usar this.acceleration.mult(0)

❓Identifica dónde está el Attractor en la simulación. Cambia el color de este

✍️El Attractor se encuentra en el sketch.js, se crea en el setup() y se dibuja en el draw(). El Attractor es el objeto central que atrae a los demas. En el archivo attractor.js, dentro del método display(), encontre la logica de color:

```js
display() {
    ellipseMode(CENTER);
    stroke(0);
    if (this.dragging) {
      fill(50);
    } else if (this.rollover) {
      fill(100);
    } else {
      fill(255, 50, 50); // AQUI SE CAMBIA EL COLOR, LO PUSE ROJO
    }
    ellipse(this.position.x, this.position.y, this.mass * 2);
  }
```

❓Observa que el Attractor tiene dos atributos this.dragging y this.rollover. Estos atributos no se modifican en el código, pero permitirían mover el attractor con el mouse y cambiar su color cuando el mouse está sobre él. ¿Cómo podrías modificar el código para que esto funcione? considera las funciones que ofrece p5.js para interactuar con el mouse

✍️Aunque el código tenia las variables dragging y rollover, no pasaba nada porque el programa no estaba escuchando al mouse. Para arreglarlo se debia hacer lo siguiente:

+ Logica cambio de color (Rollover): Use la función dist() para medir que tan lejos esta el mouse del centro del atractor. Si la distancia es menor a la masa (el radio), se activa this.rollover = true y el color cambia para dar feedback visual de que lo estoy señalando

+ Logica de arrastre (Dragging): Para poder agarrar el objeto, hay que conectar los eventos del mouse con el atractor en tres pasos:
1. Use la función mousePressed() para que, justo cuando se hace clic, el programa revise si el mouse esta encima del circulo. Si es asi, se activa un interruptor (this.dragging = true)
   
2. Mientras ese interruptor este encendido, se le ordena al atractor que su posición sea igual a la del mouse (this.position = mouseX, mouseY). Asi el objeto se siente pegado al cursor mientras lo arrastro

3. Finalmente, con mouseReleased(), apagamos el interruptor al soltar el botón, dejando el atractor fijo en su nuevo lugar

⭐[Sketch](https://editor.p5js.org/VanDiosa/sketches/l7dIhu_W0)

En el attractor.js:
```js 
// Nueva función para detectar si el mouse está encima o si se hizo clic
  handleMouse(mx, my) {
    let d = dist(mx, my, this.position.x, this.position.y);
    // Rollover: si el mouse está cerquita del radio, se activa
    if (d < this.mass) {
      this.rollover = true;
    } else {
      this.rollover = false;
    }
    
    // Si estamos arrastrando, que la posición siga al mouse
    if (this.dragging) {
      this.position.x = mx;
      this.position.y = my;
    }
  }

  // Función para cuando presionamos el mouse
  handlePress(mx, my) {
    let d = dist(mx, my, this.position.x, this.position.y);
    if (d < this.mass) {
      this.dragging = true;
    }
  }

  // Función para cuando soltamos el mouse
  handleRelease() {
    this.dragging = false;
  }
```
En el sketch.js: 
```js 
function draw() {
  background(255);
  attractor.display();
  attractor.handleMouse(mouseX, mouseY); // Esta linea

  for (let m of movers) {
    let force = attractor.attract(m);
    m.applyForce(force);
    m.update();
    m.show();
  }
}

// Y AÑADE ESTAS DOS FUNCIONES AL FINAL DEL SKETCH
function mousePressed() {
  attractor.handlePress(mouseX, mouseY);
}

function mouseReleased() {
  attractor.handleRelease();
}
 ```

### Actividad 05   
📤Luego de explorar la simulacion sobre [coordenadas polares](https://editor.p5js.org/juanferfranco/sketches/fE5rCtDS1)     

❓¿Cuál es la relación entre r y theta con las posiciones x y y? Puedes repasar entonces la definición de coordenadas polares y cómo se convierten a coordenadas cartesianas.     

✍️Normalmente usamos coordenadas cartesianas (x, y) para ubicar un punto. Pero en este ejercicio usamos Coordenadas Polares, que definen la posicion mediante un radio (r) y un ángulo ($\theta$)

La relacion matematica es:
$x = r \cdot \cos(\theta)$
$y = r \cdot \sin(\theta)$

En el cóodigo, esto permite que el circulo se mueva en una trayectoria circular. Mientras el ángulo ($\theta$) aumenta, las funciones seno y coseno calculan la posicion exacta en el borde de un circulo de radio r

❓Modificacion 1 en la funcion draw()
 ```js
function draw() {
  background(255);
  // Translate the origin point to the center of the screen
  translate(width / 2, height / 2);
  //let v = p5.Vector.fromAngle(theta,r);
  let v = p5.Vector.fromAngle(theta); //MODIFICACION
  fill(127);
  stroke(0);
  strokeWeight(2);
  line(0, 0, v.x, v.y);
  circle(v.x, v.y, r);
  theta += 0.02;
  r = height * 0.5*sin(theta);
}
 ```

✍️Al hacer este cambio, el circulo se queda atrapado en el centro de la pantalla. La funcion p5.Vector.fromAngle(theta) es muy practica, pero si solo le pasas el ángulo ($\theta$), ella asume que el radio es 1. Como el radio es de apenas 1 píxel, el circulo esta rotando tan cerquita del centro que casi no se nota

❓Modificacion 2

✍️Se ve exactamente igual que cuando usábamos las fórmulas de cos() y sin() manualmente. El círculo vuelve a moverse en un circulo grande y fluido, tal como al principio. La linea se estira desde el centro hasta el circulo y todo se ve equilibrado.

Ocurre porque al escribir fromAngle(theta, r), le estamos pasando los dos datos necesarios: dirección e intensidad. p5.js hace el trabajo pesado por nosotros: toma el ángulo y lo multiplica internamente por el radio (r), dsndonos como resultado las posiciones x y y correctas sin tener que escribir las formulas trigonometricas completas. Es una forma mucho más limpia y eficiente de programar movimiento circular

⭐[Sketch](https://editor.p5js.org/VanDiosa/sketches/N6O4Qf63K)

### Actividad 06   
📤Luego de repasar que es una [funcion sinusoide](https://es.wikipedia.org/wiki/Sinusoide), recordar conceptos basicos, y jugar con el [ejemplo](https://editor.p5js.org/juanferfranco/sketches/201gcBvjy)      

✍️En esta actividad, tome el codigo de una función sinusoide y le añadi controles de teclado para ver como cambiaba el movimiento en tiempo real

Lo que aprendi modificando los parametros:
+ Amplitud (Flechas Arriba/Abajo): Es el alcance del movimiento. Al aumentar la amplitud con UP_ARROW, el circulo se aleja mucho mas del centro

+ Fase (Flechas Derecha/Izquierda): Es como un viaje en el tiempo. Al tocar las flechas laterales, el circulo negro se desplaza en su ciclo. Esto me permite hacer que los dos circulos empiecen en lugares distintos aunque tengan la misma velocidad

+ Periodo (La diferencia entre 120 y 100): Como puse un periodo mas corto al segundo circulo (period2 = 100), este se mueve mas rápido que el primero. Esto hace que se desfasan y se vuelvan a encontrar constantemente

Lo que me queda claro es que la función sin() es la herramienta perfecta para crear ciclos suaves. Al multiplicar el seno por la amplitud, controlo la distancia; y al sumar la fase, controlo el ritmo o el retraso del movimiento

⭐[Sketch del ejemplo modificado en clase](https://editor.p5js.org/VanDiosa/sketches/bFGOXlgFj)

### Actividad 07   
📤Luego de trata de aplicar lo aprendido en la unidad 1 y 3 modificando la [simulacion base](https://editor.p5js.org/natureofcode/sketches/b3HpgJa6F), documentar en la bitacora     

✍️El objetivo de esta actividad era romper la perfeccion de los osciladores basicos integrando aleatoriedad organica y leyes físicas. Por lo que en lugar de usar random() para la amplitud lo cambie por un Perlin Noise y asi generar una secuencia suave, donde los circulos parecen estar vivos

Ademas ya no usa la velocidad angular  de manera fija, si no q en su lugar usa una fuerza que aecta la velocidad a la q giran, el mov deja de ser un loop eifinito y empieza a reaccionar al entorno

El Perlin Noise le da esa imperfección natural que tienen los seres vivos al moverse, y las Fuerzas permiten que el sistema sea dinámico

⭐[Sketch del ejemplo modificado en clase](https://editor.p5js.org/VanDiosa/sketches/bFGOXlgFj)

Cambios en oscillator.js:
 ```js
class Oscillator {
  constructor() {
    this.angle = createVector();
    this.angleVelocity = createVector(0, 0);
    this.angleAcceleration = createVector(0, 0); // Unidad 3: Aceleración
    this.mass = random(1, 2); // Unidad 3: Masa
    
    this.offX = random(1000); // Unidad 1: Offset para Noise
    this.offY = random(1000);
  }

  // Unidad 3: Método para aplicar fuerzas
  applyForce(force) {
    let f = p5.Vector.div(force, this.mass);
    this.angleAcceleration.add(f);
  }

  update() {
    // Aplicamos la aceleración a la velocidad (Unidad 3)
    this.angleVelocity.add(this.angleAcceleration);
    this.angle.add(this.angleVelocity);
    this.angleVelocity.limit(0.05); // Para que no se vuelva loco
    this.angleAcceleration.mult(0); // Reset de fuerza

    // Unidad 1: Usar Noise para cambiar la amplitud dinámicamente
    this.amplitudeX = map(noise(this.offX), 0, 1, 50, width / 2);
    this.amplitudeY = map(noise(this.offY), 0, 1, 50, height / 2);
    this.offX += 0.01;
    this.offY += 0.01;
  }

  show() {
    let x = sin(this.angle.x) * this.amplitudeX;
    let y = sin(this.angle.y) * this.amplitudeY;

    push();
    translate(width / 2, height / 2);
    stroke(0, 50); // Un poco de transparencia para ver el rastro
    line(0, 0, x, y);
    fill(127, 200);
    circle(x, y, this.mass * 16); // El tamaño depende de la masa
    pop();
  }
}
 ```
Cambioe es sketch.js: 
 ```js
function draw() {
  background(255);
  let wind = createVector(0.001, 0.001); // Una fuerza pequeña

  for (let osc of oscillators) {
    osc.applyForce(wind); // Aplicamos fuerza (Unidad 3)
    osc.update();
    osc.show();
  }
}
 ```

### Actividad 08     
📤Luego de observar el [codigo base de una onda](https://editor.p5js.org/natureofcode/sketches/CQ19Yw0iT), modificarlo para que se mueva y documentar el proceso

✍️El codigo original dibujaba una onda estatica, para lograr que se desplazara como una ola de mar, tuve que realizar los siguientes cambios:

+ Primero el profe nos mostro que debiamos de mover la logica del bucle for del setup() al draw(), ya que, para que algo se mueva necesitamos que se redibuje constantemente
+ Luego cree una vrble llamada startAngle, primero el angulo siempre empezaba en 0 en cada frame, pero ahora en cada frame hay un incremento de esa nueva vrble con una velocidad (waveSpeed), logrando que el primer circulo empiece en una posicion de la onda un poco mas adelante cada vez
+ Finalmente dentro del bucle, se debia usar el let currentAngle = startAngle, para asegurarnos de que toda la fila de circulos se desplace en conjunto

⭐[Sketch del ejemplo modificado en clase](https://editor.p5js.org/VanDiosa/sketches/gd4K32QJx)

### Actividad 09     
📤Luego de observar el [codigo base de un sistema de resorte](https://editor.p5js.org/natureofcode/sketches/HZOUeCe9p), modificarlo para que sea un sistema de dos resortes conectados en serie y documentar el proceso

✍️Se tuvo que crear dos masas y dos resortes. El primer resorte sujetandose del techo, y el segundo anclado a la posicion de la primera masa

En el draw(), use spring2.anchor.set(bob1.position.x, bob1.position.y). Esto hace que cuando el primer bob se mueve, el segundo resorte se mueva con el, arrastrando a la segunda masa

Al pasar de uno a dos bobs, tuve que actualizar las funciones mousePressed y mouseReleased para que el código detectara el clic en cualquiera de las dos masas. Si no lo hacía, el programa lanzaba un error de "bob is not defined" orque el objeto original había cambiado de nombre a bob1 y bob2

⭐[Sketch del ejemplo modificado en clase](https://editor.p5js.org/VanDiosa/sketches/OwwF-GhsW)

### Actividad 10     
📤Luego de observar el [codigo base de un sistema de pendulo](https://editor.p5js.org/natureofcode/sketches/MQZWruTlD), modificarlo para que sea un sistema de dos pendulos conectados en serie y documentar el proceso

✍️Aqui se aplicaba una logica parecida a la de los resortes. La idea era q el segundo pendulo reaccionara dinamicamente a la posicion del primero

En el sketch, se tuvo que definir dos instancias/pendulos, el p1 anclado al centro del techo y el 02 con su punto de pivote que cambia en cada frame

En el draw(), se actualiza el pivote usando la posicion de la masa del primero con p2.pivot.set(p1.bob.x, p1.bob.y);, eso crea la conexion fisica y matematica par que sea como un brazo articulado. Al estar conectados, el movimiento se vuelve mucho mas complejo. Aunque cada pendulo calcula su propia aceleracion angular basada en la gravedad, el segundo se ve arrastrado por la inercia del primero

Lo mas interesante de este ejercicio fue ver que mientras el primer pendulo tiene un balanceo predecible, el segundo pendulo adquiere una energia mucho mas erratica porque su base se esta moviendo.

⭐[Sketch del ejemplo modificado](https://editor.p5js.org/VanDiosa/sketches/YkX3-e5CA)

## Bitácora de aplicación 

### Actividad 11: Resonancia Pendular 🎼🏮      
✍️ Concepto y Narrativa
La obra representa un "analizador de espectro vivo". La narrativa se basa en la visualizacion fisica del sonido, donde cada frecuencia (bajos, medios y altos) tiene un cuerpo material que reacciona a la musica. No es solo un grafico que sube y baja; son tres pendulos que "sienten" el impacto de las ondas sonoras. Los bajos, al ser mas pesados, mueven un pendulo mas largo y lento, mientras que los agudos mueven uno corto y frenetico. La musica aqui actua como una fuerza externa que rompe el equilibrio de la gravedad

✍️ Aplicación de Unidades (Reglas del Sistema)      
+ Unidad 1 (Ruido Perlin): Para que la punta del pendulo no fuera un circulo perfecto y rigido, use noise() para generar una pequeña distorsion en la posicion final. Esto hace que el rastro se sienta como una frecuencia vibrando y no como una linea de computadora

+ Unidad 2 (Vectores y Motion 101): Implemente el uso de p5.Vector para gestionar el origen y la posicion de los pendulos. El movimiento sigue el ciclo fundamental de Aceleracion → Velocidad → Posicion, aplicado aqui al sistema de angulos para lograr una oscilacion fluida

+ Unidad 3 (Leyes de la Naturaleza): El sistema aplica una acumulacion de fuerzas. Por un lado, la gravedad que intenta restaurar el equilibrio y, por otro, el "empuje" (fuerza externa) de la musica que genera el caos. Ademas, para que los pendulos no se volvieran locos, aplique una fuerza de friccion ($0.992$); esto simula la resistencia del aire, haciendo que la energia se disipe gradualmente si la musica se detiene
 
+ Unidad 4 (Péndulos y Coordenadas Polares): Esta es la base de la obra. Utilice un sistema de pendulos donde el movimiento se calcula de forma angular. Aplique la conversion de coordenadas polares a cartesianas para determinar la posicion exacta de la masa en cada frame: $x = r \cdot \sin(\theta)$, $y = r \cdot \cos(\theta)$. Esto permite que los objetos orbiten alrededor de su pivote de forma armonica.

⭐[Sketch](https://editor.p5js.org/VanDiosa/sketches/4-YyYDYhg)
```js
let track, fft;
let pBajo, pMedio, pAlto;
let listo = false;

function preload() {
  console.log("--- 📥 CARGANDO AUDIO... ---");
  track = loadSound('track.mp3', 
    () => { console.log("✅ AUDIO LISTO"); listo = true; }, 
    () => { console.error("❌ ERROR AL CARGAR"); }
  );
}

function setup() {
  createCanvas(windowWidth, windowHeight);
  background(10, 10, 15); 
  
  // -----------------ANÁLISIS DE AUDIO-----------------
  // Extraemos la energía del sonido para usarla como fuerza
  fft = new p5.FFT(0.8); 
  
  let pivoteX = width / 2;
  let pivoteY = height * 0.1;
  
  // -----------------UNIDAD 4: SISTEMA DE PÉNDULOS-----------------
  // Definimos longitudes distintas para cada frecuencia
  pBajo = new PenduloLuminoso(pivoteX, pivoteY, height * 0.7, color(100, 50, 255)); 
  pMedio = new PenduloLuminoso(pivoteX, pivoteY, height * 0.55, color(0, 200, 255));
  pAlto = new PenduloLuminoso(pivoteX, pivoteY, height * 0.4, color(255, 20, 80));
}

function draw() {
  // -----------------MEMORIA DEL TRAZO-----------------
  // El alpha en 1 permite que el color no se borre rápido y deje rastro
  background(10, 10, 15, 1); 

  if (track.isPlaying()) {
    fft.analyze();
    
    // -----------------REACCIÓN AL RITMO-----------------
    // Le pasamos el volumen de cada instrumento a su péndulo
    pBajo.update(fft.getEnergy("bass"));
    pBajo.show(fft.getEnergy("bass"));

    pMedio.update(fft.getEnergy("mid"));
    pMedio.show(fft.getEnergy("mid"));

    pAlto.update(fft.getEnergy("treble"));
    pAlto.show(fft.getEnergy("treble"));
  } else if (listo) {
    fill(255);
    textAlign(CENTER);
    text("DALE CLIC PARA SONAR", width/2, height/2);
  }
}

class PenduloLuminoso {
  constructor(x, y, l, colEstela) {
    this.origen = createVector(x, y); // UNIDAD 2: Punto de anclaje usando vectores
    this.pos = createVector();
    
    // -----------------ESTADO INICIAL DEL MOVIMIENTO-----------------
    this.angle = PI / 4; 
    this.angleV = 0; 
    this.l = l;
    this.colEstela = colEstela; 
    
    // UNIDAD 1: Valor inicial para que el ruido sea distinto en cada uno
    this.offNoise = random(1000);
  }

  update(energia) {
    // --------------------UNIDAD 4: OSCILACIÓN--------------------
    let g = 0.8; 
    let angleA = (-g / this.l) * sin(this.angle);
    
    // -----------------UNIDAD 3: FUERZA EXTERNA-EMPUJE DEL AUDIO-----------------
    // La música actúa como una fuerza externa que sacude el péndulo
    let empuje = map(energia, 0, 255, 0, 0.04);
    this.angleV += (this.angle > 0) ? -empuje : empuje;

    // -----------------FRENO DE SEGURIDAD-----------------
    // Evita que el péndulo dé la vuelta completa como un ventilador
    let limite = PI / 1.4;
    if (abs(this.angle) > limite) {
      this.angleV *= 0.5; 
      this.angle = (this.angle > 0) ? limite : -limite;
    }

    // -----------------UNIDAD 2: MOTION 101 (A->V->P)-----------------
    this.angleV += angleA;
    this.angleV *= 0.992; // UNIDAD 3: RESISTENCIA / FRICCIÓN
    this.angle += this.angleV;

    // -----------------UNIDAD 4: COORDENADAS POLARES-----------------
    // Pasamos el ángulo y radio a puntos X y Y para poder dibujarlo
    let dL = map(energia, 0, 255, 0, 150);
    this.pos.set((this.l + dL) * sin(this.angle), (this.l + dL) * cos(this.angle));
    this.pos.add(this.origen);

    // UNIDAD 1: Ruido Perlin para que la punta vibre orgánicamente
    this.offNoise += 0.02;
  }

  show(e) {
    // Brazo del péndulo
    stroke(255, 30); 
    strokeWeight(1);
    let pPure = createVector(this.l * sin(this.angle), this.l * cos(this.angle)).add(this.origen);
    line(this.origen.x, this.origen.y, pPure.x, pPure.y);

    // -----------------DIBUJO DEL RASTRO-----------------
    noStroke();
    let colConAlpha = color(red(this.colEstela), green(this.colEstela), blue(this.colEstela), 15);
    fill(colConAlpha);
    let tamEstela = map(e, 0, 255, 10, width * 0.07);
    circle(this.pos.x, this.pos.y, tamEstela);

    // UNIDAD 4: Masa del péndulo (Bola blanca)
    fill(255); 
    let tamCuerpo = map(e, 0, 255, 8, 25); 
    circle(this.pos.x, this.pos.y, tamCuerpo);
  }
}

function mousePressed() {
  if (track.isPlaying()) {
    track.pause();
  } else {
    track.play();
  }
}

function windowResized() { 
  resizeCanvas(windowWidth, windowHeight); 
}
```

📸Algunas capturas
<img width="898" height="727" alt="Captura de pantalla 2026-03-13 090519" src="https://github.com/user-attachments/assets/04261a31-c3de-4c01-b9e1-77f1773afc8f" />

<img width="898" height="729" alt="Captura de pantalla 2026-03-13 090527" src="https://github.com/user-attachments/assets/ce41c5bc-0396-444b-aa2c-9b0e949407c2" />


## Bitácora de reflexión












