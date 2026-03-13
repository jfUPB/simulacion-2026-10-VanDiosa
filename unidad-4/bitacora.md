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

## Bitácora de aplicación 



## Bitácora de reflexión






