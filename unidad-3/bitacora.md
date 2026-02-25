# Unidad 3

## Bitácora de proceso de aprendizaje

### Actividad 01   
📤Luego ver el video con la [charla de Robert Hodgin](https://www.youtube.com/watch?v=vmUodu6K-bA)   

✍️Primero que todo lo que mas me gusto fue que el señor robert, siendo un teso, admite que se bajoneo al ver que una ia hacia en segundos lo que a él le tomaba meses, preguntandose lo mismo q nosotros posiblemente nos hemos preguntado: ¿Para que nos matamos aprendiendo, estudiando, haciendo, si una maquina lo saca sin dificultad?

Como yo soy de la linea de animacion, este curso en especifico, he estado usando la ia para poder aterrizar las ideas que me vienen a la mente en cada unidad, para asi no trabarme tanto en la parte tecnica, considero que la forma adecuada de usar la ia, es como un compañero, una mano derecha, trabajar en conjunto, no simplemente tragar entero sin masticar, sin revisar, sin profundizar, sin corregir, ya que, lo que hace especial a las cosas es el proceso

### Actividad 02   
📤Seguir la actividad realizada en clase, en visual studio code. Y reportar en la bitacora las reflexiones de lo aprendido    

❓¿Por qué es necesario multiplicar la aceleración por cero en cada frame? ¿Por qué se multiplica por cero justo al final de update()?   

✍️La aceleracion son empujones que se reciben en ciertos momentos, por ejemplo el viento te empuja pero no se queda ahi pegado para siempre acelerandote infinitamente. Se usa: acceleration.mult(0), para restear la aceleracion y que en el siguiente frame se calculen fuerzas nuevas

❓Recuerda esta cuestión por favor: paso por valor y paso por referencia. En este caso, force es objeto de la clase p5.Vector, es decir, es un objeto que se pasa por referencia. ¿Qué implica esto?   
Entonces cómo debería ser el método applyForce para que funcione correctamente sin asumir que la masa es igual a 1?   

✍️Implica que cuando le pasamos el vector a la funcion applyForce, no se le pasa una copia si no que se altera directamente la vrble global. Por eso es que se usa: let f = p5.Vector.div(force, 10), para crear un vector nuevo (una copia)

### Actividad 03   
📤Luego de analizar el [material de clase](https://natureofcode.com/forces/#creating-forces), crear tres obras generativas para cada una de las siguientes fuerzas: Fricción, Resistencia al aire y fluidos, Atracción gravitacional

✍️[Friccion](https://editor.p5js.org/VanDiosa/sketches/70ebk7fMP)    
Partiendo de la base del texto, cree un ejemplo donde la friccion se viera ligada a un segmento en especifico de la suuperficie, y que ademas se pudiera recibir algun feedback mas visual cuando el objeto tocara ese segmento. Ademas cambie la interactividad del viento por que el usuario pueda lanzar de forma mas controlada el objeto y asi poder ver como actua este desde diferentes angulos y asi

✍️[Resistencia al aire y fluidos](https://editor.p5js.org/VanDiosa/sketches/ZpnR2Xik4)    
En este ejemplo, quise crear dos capas con diferentes coeficientes, para poder observar como cada objeto frenaba de diferente forma dependiendo de la densidad y la masa. De igual forma quice añadir un cambio de color para indetificar el tipo de fuerza que actuaba sobre ellos

✍️[Atracción gravitacional](https://editor.p5js.org/VanDiosa/sketches/QODbTH6Wn)   
Para el ultimo ejercicio, simplemente lo transforme para que se viera como una representacion orbital. Ademas le coloque transparencia al fondo, para poder ver el rastro del planeta, y tmb aumente la constante gravitacional para que el movimiento fuera mas dinamico

## Bitácora de aplicación 
### Actividad 04: Espectro Colectivo🐟🐠   

✍️Historia   
Quiero que la obra muestre un ecosistema marino, donde al inicio se vea un gran grupo de peces nadando tranquilamente por el espacio. Luego, la paz se rompe cuando un depredador (el mouse) los ataca, generando panico entre los peces y activando un sentido de supervivencia, el cual se caracterisa por agruparse en sus respectivos cardumenes. Lamentablemente los peces mas lentos o que pertenecen a grupos muy pequeños, corren el riesgo de volverse mas vulnerables, siendo atrapados por el depredador hasta que este quiera liberarlos

✍️El vinculo entre la narrativa y las fuerzas  
Usando lo aprendido en la unidad use las siguientes reglas para manipular la aceleracion de los peces:
+ Resistencia al agua-Drag: esta fuerza se opone a la velocidad de los peces, con el objetivo de que no se sientan como puntos a lo loco por el canva, si no, como lo que son: cuerpos con masa nadando en un fluido real
  
+ Atraccion de cardumen: esta fuerza busca agrupar a los peces por su colores cuando hay peligro. Cada pez calcula la distancia a sus compañeros mas cercanos y genera una FUERZA DE ATRACCION hacia ellos

+ Fuerza de huida y captura: el depredador genera una FUERZA DE REPULCION que acelera a los peces lejos de el, pero si el pez entra en un radio, una fuerza de captura anula su aceleracion por lo que queda pegado al mouse

Por otro lado cada pez tiene una masa distinta, por lo que los mas pesados tardan mas en acelerar, siendo la fisica parte clave de sus posibilidades de supervivencia. Ademas tal como aprendimos en la actividad 2, la aceleracion se resetea en cada frame para que el comportamiento del cardumen se sienta mas dinamico 

⭐[Sketch](https://editor.p5js.org/VanDiosa/sketches/tbnmxkhKu)

```js
let cardumen = [];
let cantidad = 120; 
let coloresClanes;

function setup() {
  createCanvas(windowWidth, windowHeight);
  coloresClanes = [
    color(255, 50, 50, 220),   // Rojo
    color(50, 255, 100, 220),  // Verde
    color(50, 150, 255, 220),  // Azul
    color(255, 200, 50, 220)   // Amarillo
  ];
  
  for (let i = 0; i < cantidad; i++) {
    cardumen.push(new Pez());
  }
}

function draw() {
  background(10, 25, 45, 60);
  
  let mousePos = createVector(mouseX, mouseY);

  for (let p of cardumen) {
    if (mouseIsPressed) { // INTERACCION MOUSE
      let direccionMouse = p5.Vector.sub(p.pos, mousePos);
      let distMouse = direccionMouse.mag();

      // -----------------FUERZA DE ATRACCION-CAPTURA-----------------
      if (p.atrapado || distMouse < 50) { 
        p.atrapado = true; 
        p.pos.x = lerp(p.pos.x, mouseX + p.offset.x, 0.2); 
        p.pos.y = lerp(p.pos.y, mouseY + p.offset.y, 0.2);
        p.vel.mult(0); // Anula la velocidad propia 
      } 
      else {
        // -----------------FUERZA DE REPULSION-HUIDA-----------------
        if (distMouse < 300) {
          let huida = direccionMouse.copy();
          huida.setMag(1.2);
          p.applyForce(huida);
        }

        // -----------------FORMACION DEL CARDUMEN-----------------
        let vecinos = 0;
        for (let other of cardumen) {
          if (p !== other && p.clanID === other.clanID && !other.atrapado) {
            let d = p5.Vector.dist(p.pos, other.pos);
            if (d < 120 && vecinos < 4) { 
              let atraccion = p5.Vector.sub(other.pos, p.pos);
              atraccion.setMag(0.25);
              p.applyForce(atraccion);
              vecinos++;
            }
            if (d < 30) { 
              let sep = p5.Vector.sub(p.pos, other.pos);
              sep.setMag(0.5);
              p.applyForce(sep);
            }
          }
        }
      }
    } else {
      // -----------------ESTADO DE REPOSO-----------------
      let vagar = p.vel.copy();
      vagar.rotate(random(-0.2, 0.2)); 
      vagar.setMag(0.1); 
      p.applyForce(vagar);
      
      if (p.vel.mag() < 1.5) {
        p.vel.setMag(1.5);
      }
    }

    // -----------------RESISTENCIA AL AGUA-----------------
    let drag = p.vel.copy();
    drag.mult(-0.04);
    p.applyForce(drag);

    p.update(); // MOTION 101: Aceleracion->Velocidad->Posicion
    p.checkEdges();
    p.show();
  }
}

function mouseReleased() { 
  for (let p of cardumen) { // EFECTO DE LIBERACION
    if (p.atrapado) {
      p.atrapado = false;
      let impulso = p5.Vector.random2D().mult(random(10, 15));
      p.applyForce(impulso);
    }
  }
}

class Pez {
  constructor() {
    this.pos = createVector(random(width), random(height));
    this.vel = p5.Vector.random2D().mult(random(2, 4));
    this.acc = createVector(0, 0);
    this.mass = random(1.5, 3); // A mayor masa aceleracion mas lenta
    this.clanID = floor(random(4));
    this.color = coloresClanes[this.clanID];
    this.atrapado = false;
    this.offset = createVector(random(-30, 30), random(-30, 30)); // Offset para que no queden todos amontonados 
  }

  applyForce(f) { // Segunda Ley de Newton: F=m*a -> a=F/m
    let force = p5.Vector.div(f, this.mass);
    this.acc.add(force);
  }

  update() {
    if (!this.atrapado) {
      this.vel.add(this.acc); // La aceleracion cambia la velocidad
      this.vel.limit(mouseIsPressed ? 7 : 2.5); // Limite segun estado
      this.pos.add(this.vel); // La velocidad cambia la posicion
      this.acc.mult(0); // Reset de aceleracion
    }
  }

  show() {
    let angle = this.vel.heading(); // Direccion de nado
    push();
    translate(this.pos.x, this.pos.y);
    rotate(angle);
    fill(this.color);
    noStroke();
    
    // DIBUJO DEL PEZ
    ellipse(0, 0, this.mass * 6, this.mass * 4); // CuerpO
    triangle(-this.mass * 2, 0, -this.mass * 6, this.mass * 3, -this.mass * 6, -this.mass * 3); // Cola
    fill(0);
    circle(this.mass * 1.5, -this.mass * 0.5, this.mass * 0.8); // Ojo
    pop();
  }

  checkEdges() { // Logica de bordes infinitos
    if (this.pos.x > width) this.pos.x = 0;
    if (this.pos.x < 0) this.pos.x = width;
    if (this.pos.y > height) this.pos.y = 0;
    if (this.pos.y < 0) this.pos.y = height;
  }
}
```

📸Algunas capturas
<img width="1919" height="793" alt="Captura de pantalla 2026-02-25 160225" src="https://github.com/user-attachments/assets/b6d66735-0759-45c5-b036-a2a895ba4e69" />

<img width="1919" height="794" alt="Captura de pantalla 2026-02-25 160317" src="https://github.com/user-attachments/assets/cfe46bd0-72a5-44c0-b65c-7819a80c5000" />


## Bitácora de reflexión



