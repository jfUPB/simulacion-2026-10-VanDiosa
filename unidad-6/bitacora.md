# Unidad 6
## Bitácora de proceso de aprendizaje
### Actividad 01
📤Seleccionar dos imágenes o piezas de Tyler Hobbs, responder...   

✍️[Pieza 1: New Space #4 (Philodendron)](https://www.tylerxhobbs.com/works/new-space)     
<img width="923" height="341" alt="ACT1_1B" src="https://github.com/user-attachments/assets/2057921c-94ef-449d-a0b6-9298d5e2ec45" />

+ Composición: Es horizontal, tiene tres sillas dispuestas en el espacio. Dos estan agrupadas a la izquierda y la otra esta mas aislada a la derecha, como si hubiera una pareja y por otro lado un individuo
+ Densidad: La mayor densidad de tinta se encuentra en el marco de las sillas, donde el trazado es como mas cerrado que da la aparecia de q esas zonas son mas solidas. Por otro lado, las lineas que conectan y rodean las sillas son mas ligeras
+ Dirección del movimiento: El flujo no es lineal, si no que las lineas parecen como que se enrredas en objetos solidos invisibles, las lineas parecen vibrar
+ Color: Monocromatico negro. Creo que el color es clave, ya que, elimina las distracciones para que el ojo se centre en la textura y la forma
+ Ritmo: Da la impresion de un ritmo nervioso, sin fluidez, con trazos cortos que se enrredan, con frecuencia en las zonas donde se queria mayor densidad o intereses
+ Repetición y variación: A pesar de que la estructura de la silla se repite tres veces, la variacion del algoritmo permite que el ruido de los trazos sea distinto 
  
¿Por que esas decisiones son potentes?    
Creo que las decisiones que se tomaron lograron que la pieza se viera mas humana, usar un objeto tan cotidiano como unas sillas y dibujarlas con lineas caoticas da una sensacion como de fragil

(Hipotesis) ¿Que tipo de reglas o sistema podria estar detras de esta pieza?    
Pienso que es algo parecido a lo visto en la clase, de las corrientes invisibles, estas guiarian cada trazo. Tal vez se tiene una base invisible de la silla y el algoritmo dibuja sobre esta pero siguiendo una regla de desorden sonde la linea se pueda desviar de la forma

✍️[Pieza 2: Fidenza #725](https://www.tylerxhobbs.com/works/fidenza)    
<img width="182" height="216" alt="ACT1_2" src="https://github.com/user-attachments/assets/09d88b3e-cf10-42e3-b0ad-ad1fb0ac6245" />

+ Composición: Es de pantalla completa, muy saturada. No hay un pto de enfoque, el ojo puede viajar por todo el canva siguiendo como las curvas
+ Densidad: Es una pieza de alta densidad, no hay casi espacios vacios. Se puede ver que los bloques de colores estan apretados, generan mucha textura, y da una impresion de relieves
+ Dirección del movimiento: Se ve claramente que esta siguiendo un campo de flujo como los que vimos en clase. No hay lineas rectas, solo curvas y organizas, remolinos, corrientes, por todo el canva
+ Color: Se uso una paleta muy variada sobre un fondo color cremita. Los colores en pequeños bloqes me recordo a como la luz atraviesa los vitrales de las iglesias
+ Ritmo: Es un ritmo rapido, vibrante, con constante interrupcion por el cambio de colores
+ Repetición y variación: Hay una unidad basica que es un rectangulo, al cual se le varia el color, el ancho, y el angulo de giro

¿Por que esas decisiones son potentes?    
Siento que lograron que el codigo no se sienta frio, si no por el contario, calido, tanto asi, que me recordo como mencione anteriormente a los vitrales de las iglesia. La variacion de color hace que la pieza no se sienta como algo plano, si no que hay una luz detras de la pantalla 

(Hipotesis) ¿Que tipo de reglas o sistema podria estar detras de esta pieza?     
Al igual que la pieza anterior, hay un campo de flujo, que en este caso se usa para dibujar los rectangulos variables. La regla clave pienso que es el que el sistema decide aleatoriamente cada cuanto aparece un color dentro de cada linea de flujo. Tmb hay una especie de profunidad como, entonces puede que haya una regla donde los trazos mas gruesos destacan mas que los delgados

### Actividad 02   
📤En base al [capitulo 5 de libro The Nature of Code](https://natureofcode.com/autonomous-agents/), responder:

❓¿Qué es un agente autónomo?    
Un agente autonomo es un elemento que tiene su propio cerebro. El agente no se deja llevar como una particula comun, si no que tiene la capacidad de observar su entorno, procesa la informacion que adquiere y toma una decision en base a eso de a donde quiere ir

❓¿Qué es una steering force?    
Se traduce como fuerza de direccion. No es una fuerza que simplemente empuja, si no que es el resultado de una resta de vectores (Steering = Velocidad deseada - Velocidad actual). Tiene la funcion de darle direccion al movimiento actual para alinearse con la musion del agente

❓¿En qué se diferencia una steering force de fuerzas como gravedad, viento o fricción?    
Por un lado las fuerzas externas son vectores que se imponen desde el entorno, son globales y constantes sobre todos los objetos. Y las steering forces, son vectores que se generan internamente en cada agente, ajustan la dinamica segun la intencion que tenga cada uno

❓¿Por qué estas ideas son utiles para diseñar comportamiento visual?   
Al usar reglas de direccion en lugar de trayectorias fijas, el movimiento resultante no es una linea predecible, si no uno comportamiento que va evolucionando. Facilita el diseño de visuales que se sientan mas organicos, vivos y capaces de responder a estimulos externos


### Actividad 03   
📤Estudiar la seccion [Flow Fields](https://natureofcode.com/autonomous-agents/#flow-fields) y responder   

❓¿Cómo está construido el campo de flujo?   
Se construye sobre una rejilla invisible que cubre todo el lienzo, a cada celda se le asigna un angulo de direccion, normalmente usando un perlin noise para que los cambios de direccion sean suaves y no saltos aleatorios

❓¿Qué representa cada celda o vector del campo?   
Cada celda es como una señal de transito, que contiene un vector unitario que le indica a todo agente que pase por ahi hacia donde debe girar. Es una estructura tipo corriente

❓¿Cómo usa un agente su posición para consultar el campo?   
El agente toma sus coordenadas, las mapea para saber en que celda se encuentra y lee el vector de esa posicion especifica

❓¿Cómo se convierte el vector consultado en una decisión de movimiento?    
El vector consultado se convierte en la velocidad deseada del agente. Luego se aplica la formula que se menciono antes: Steering = Velocidad deseada - Velocidad actual, para que el agente gire suavemente hacia esa direccion en lugar de moverse de golpe

✍️Parametros importantes del sistema:
+ Resolucion -> Es el tamaño de cada celda, si la resolucion es alta (hay muchas celdas pequeñas), el flujo es mas detallado; por lo contrario si la resolucion es baja, el movimiento se ve mas rigido
+ MaxSpeed -> Es la velocidad maxima a la que puede ir el agente
+ MaxForce -> Es que tan fuerte puede girar el agente. Si es bajo, el agente tiene una curva de firo amplia; si es alto los agentes reaccionan instantaneamente al flujo
+ Cantidad de agentes -> Define la densidad. Pocos agentes crean lineas solas, miles de agnetes revelan la estructura completa del canva
+ Noise Step (xoff/yoff) -> Define que tan suave o caotico es el cambio de direccion en el espacio

✍️Realiza al menos una [modificación](https://editor.p5js.org/natureofcode/sketches/egribz8WV) y analiza el efecto visual que produce:    
La modificacion que hice fue en flowfield.js -> let angle = map(noise(xoff, yoff), 0, 1, 0, TWO_PI*4); -> multipliqué el ángulo final por 4. Este genero que los agentes tiendan a dar vueltas en circulos cerrados, ya que se forman unos espirales dentro de las corrientes. Paso de parecer un rio a un sistema de pequeños remolinos interconectados

❓¿Qué tipo de movimiento produce este algoritmo?   
Produce un movimiento logico pero organico. Se siente que fluye bajo las leyes de la naturaleza (aire, magnetismo, agua...) donde hay orden pero no repeticiones exactas

❓¿Qué sensaciones visuales te sugiere?   
Sugiere fluidez, serenidad y complejidad. Esta la sensacion de que hay algo invinsible organizando el caos

❓¿En qué tipo de pieza musical imaginas que podría funcionar bien?   
Lo primero que se me ocurre es musica Lo-fi, ya que los agentes tienen el mismo rimo constante, relajado y repetitivo con variaicones sutiles. Creo q tambien podria funcionar con musica ambiental, donde el sonido no tiene estructuras rigidas si no capas de texturas


### Actividad 04
📤Estudiar la seccion [Flocking](https://natureofcode.com/autonomous-agents/#flocking) y responder 

✍️Explica con tus palabras las tres reglas básicas:   
+ Separación -> Evita que los agentes choquen entre si. Cada agente mira a sus vecinos y si estan muy cerca, aplican una fuerza hacia el lado opuesto para mantener su espacio personal
+ Alineación -> Esta regla permite que cada agente mire hacia donde se estan moviendo sus vecinos, para luego ajustar su velocidad con el objetivo de apuntar en la misma direccion que los otros
+ Cohesión -> Mantiene unidos a los agentes. Cada uno calcula el centro de masa de sus vecinos (como conjunto) y aplica una fuerza para moverse hacia ese centro, evitando que el grupo se vea disperso

✍️Identifica qué parámetros controlan estas reglas   
+ Pesos -> En boid.js -> sep.mult(), ali.mult() y coh.mult() -> Cada una de las reglas tiene una importancia diferente, por ejemplo la separacion puede PESAR mas que la cohesion, por lo tanto el grupo se veria mas espaciado
+ neighborDistance -> En las funciones align y cohere -> Este valor define que tan lejos un agente puede ver a sus vecinos. Entre mas grande el radio, mas coordinado y masivo el grupo
+ desiredSeparation -> En la regla separate -> Este valor define el tamaño de la burbuja personal de cada agente
+ MaxSpeed y MaxForce -> Definen que tan rapido se mueven y que tan bruscos son sus giros al momento de seguir las reglas

✍️Modifica uno o más pesos del [sistema](https://editor.p5js.org/natureofcode/sketches/IkpBw96Sd) y describe el efecto visual y colectivo    
En boid.js, cambie los pesos de sep.mult() para tener mucha separacion, y de coh.mult() para tener casi que 0 de cohesion

Antes:
```js
    sep.mult(1.5);
    ali.mult(1.0);
    coh.mult(1.0);
```
Despues:
```js
    sep.mult(5.0);
    ali.mult(1.0);
    coh.mult(0.1);
```
El efecto visual que obtuve fue que el sistema paso de ser un grupo unido a tener agentes que rebotan violentamente entre ellos y evitan formar grupos. Fue un comportamiento disperso y caotico

✍️Describe el comportamiento emergente observado    
Al probar el codigo original, se puede ver un comportamiento fuido y estable. Se forman grupos que se mueven como si siguieran una mision, en caso de que uno se separa rapidamente busca otro grupo cercano al cual integrarse

❓¿Qué atmósfera visual produce el flocking?    
Produce una atmosfera cooperativa y de vida organica. Sentia que observaba un sistema natural (de pajaros, peces, insectos...) donde no hay un lider, ya que todos saben que hacer. Da una sensacion de constante movimiento y armonia

❓¿En qué tipo de relación con una canción podría funcionar mejor este algoritmo?    
Pienso que funcionaria muy bien con una cancion que tenga una estructura con muchas armonias vocales... Se me ocurre alguna cancion de kpop ya que tienen coreografias donde todos se meuven como un todo pero manteniendo una distancia, o musica clasica con varios violines o instrumentos de cuerda

### Actividad 05   
📤Completa una comparación entre flow fields y flocking    

|  | Flow Fields | Flocking |
| --- | --- | --- |
| Tipo de Movimiento | Continuo, fluido y predecible. Sigue una corriente invisible | Colectivo, dinamico y reactivo. Los agentes cambian de rumbo segun sus vecinos |
| Nivel de Control Visual | Alto. Uno puede diseñar el mapa de vectores, asi que se puede saber por donde pasaran los agentes | Medio. Uno puede definir las reglas, pero es el grupo el que decide su trayectoria final por si solo |
| Nivel de Emergencia (Cuando el grupo hace algo que no se programo directamente) | Bajo. El patron viene del campo de flujo, no de la interaccion entre agentes | Alto. El patron surge totalmente de como interactua cada agente con los otros |
| Atmósfera/Sensación | Serenidad, orden natural, calma  | Vida, cooperacion, agilidad, nerviosismo |
| Relación Musical | Texturas constantes, sonidos ambientales, diseños sonoros de paisajes | Ritmos marcados, percusiones, armonias vocales o instrumentales |
| Ventajas | Es muy eficiente cuando se quiere llenar el canva con texturas suaves | Crea visuales que se sienten vivas, y reaccionan organicamante |
| Limitaciones | Puede volverse estatico o aburrido si el campo se queda igual por mucho tiempo | Si hay demasiados agentes, los calculos puden poner lento el pc |

✍️Si quisieras diseñar visuales para una canción contemplativa, agresiva, melancólica o eufórica, ¿Cuál algoritmo usarías en cada caso y por qué?
+ Contemplativa -> Flow Fields. Que el sistema sea fluido gracias al campo de flujo, da la atmosfera de introspeccion. El movmiento suave, sin saltos bruscos considero que puede acompañar silencios y calmas en una cancion asi
+ Agresiva -> Flocking, con una separacion alta y mucha fuerza. Buscaria crear un movimiento erratico y de choque
+ Melancolica -> Flow Fields. Habria que usar corrientes con baja velocidad, para dar la sensacion de deriva, tristeza o nostalgia
+ Euforica -> Flocking, con alta cohesion y alineacion, para que hagan giros rapidos que proyecten como fuerza colectiva y union

## Bitácora de aplicación 
### Actividad 06 - Crystal Jellyfish 🪼

✍️Concepto visual   
El concepto se basa en la dualidad de la letra de la cancion Sea de BTS, donde el desierto y el mar se entrelazan. Con la pieza visual busco representar el ecosistema de las medusas cristalinas que habitan en el oceano profundo y abisal. Quiero que el sistema utilice un Flow Field (Campo de Flujo) para simular corrientes marinas invisibles y un comportamiento de separacion para darles autonomia y vida propia

La medusas -> No quiero que sean circulos si no una especie de semicirculo o de sombrilla, que se pueda contraer y expandir ritmicamente. Ademas que no sea solo la cabeza si no que posean tentaculos, y vayan dejando un leve rastro de su trayectoria

El oceano -> Quiero que sea oscuro y denso, que se sienta como con bastante friccion por la presion al estar en lo profundo

✍️Relación entre la visual y la canción   
La idea es que la pieza no sea solo un fondo bonito, si no, que tenga coherencia con la letra de la cancion, con su arco narrativo. Quiero que la respiracion de las medusas este sincronizado con la cancion, y que los cambios de frecuencias alteren la transparecio, brillo o color de estas, haciendo parecer que cuando cantan brillan y cuando no, estan apagadas

✍️Moodboard o referencias
<img width="1920" height="1080" alt="Moodboard" src="https://github.com/user-attachments/assets/5a4c2e4b-1ef8-4a68-9d2e-42d4dee8f0dd" />


✍️Boceto    
<img width="1920" height="1080" alt="Boceto" src="https://github.com/user-attachments/assets/74f832cc-42ca-4502-9160-2e2a8a51a69b" />


✍️Mapa de decisiones

✍️Mapa de interpretación   
La interaccion no es aleatoria, ya que el usuario dirige el ecosistema
+ El despertar del oceano al darle el click inicial, genera q el sistema cobre vida
+ Con el mouse se actua como una fuerza externa (marea), que altera el flow field. De esta forma se pueden agrupar o dispersar a las medusas segun la intencion de la parte de la cancion que este sonando

✍️Justificación del algoritmo elegido     
He seleccionado un sistema hibrido de Flow Field Interactuable y Comportamientos de Direccion (Separacion):

Flow Field-Campo de Flujo -> Elegi este algoritmo para representar la corriente invisible de la vida que menciona la cancion. Al ser interactuable, permite que el usuario actue como una fuerza de la naturaleza, obligando a los agentes a fluir en direcciones especificas, lo que refuerza la idea de un destino que se puede navegar pero no ignorar (que es masomenos el mensaje de la cancion)

Regla de Separacion-Flocking -> La quiero utilizar para dar autonomia. En lugar de ser particulas sin vida, las medusas calculan su distancia respecto a las demas. Esto asegura que la composicion visual sea siempre equilibrada y que la estetica no se ensucie por la superposicion caotica de una sobre otra

✍️Explicación de la relación audio-visual    
El sistema tiene la capcidad de traducir el espectro sonoro de Sea de forma organica mediante el uso de bandas de frecuencia personalizadas, entonces las frecuencias se encargan de las siguientes cosas:

+ Bajos: Controlan la expansion de la cabezita de las medusas (tamAnimado). Cuando el bajo suena, la medusa se infla un poco, simulando una pulsacion o un latido o una respiracion

+ Medios: Controlan el Brillo (Brightness) y la Saturacion. Cuando las voces de BTS entran en la mezcla, el color de las medusas se vuelve mas vibrante y menos grisaceo

+ Altos (Instrumentos agudos y armonicos): Afectan la Bioluminiscencia (shadowBlur) y la transparencia. Los sonidos agudos hacen que las medusas irradien luz 

+ Interpolacion Lineal (lerp): Es fundamental para la relacion audio-visual, ya que asegura que los cambios no sean bruscos, sino que se sientan como una respiracion biologica que reacciona y se relaja al ritmo de la melodia

🤖 Evidencia del uso de IA

✍️Código fuente    
```js
// --- BTS - SEA  ---
let medusas = [];
let song;       
let fft;        
let flowfield; 
let resolution = 60; 
let audioIniciado = false;
let cantMedusas = 40; 

function preload() {
  song = loadSound('Sea.mp3'); 
}

function setup() {
  createCanvas(windowWidth, windowHeight);
  // UNIDAD 1: ColorMode HSB para facilitar la bioluminiscencia (Hue, Sat, Brightness)
  colorMode(HSB, 360, 100, 100, 100); // HBS para mejor iluminacion
  
  // -----------------ANÁLISIS DE ENTORNO-----------------
  flowfield = new FlowField(resolution);
  fft = new p5.FFT(0.8, 256);

  // -----------------POBLACIÓN INICIAL-----------------
  for (let i = 0; i < cantMedusas; i++) {
    // Sintonía: Cada medusa escucha una "rebanada" diferente del espectro musical
    let banda = floor(map(i, 0, cantMedusas, 10, 190)); 
    medusas.push(new Medusa(banda));
  }
}

function draw() {
  background(235, 80, 5, 12); 

  if (!audioIniciado) {
    drawMessage();
    return;
  }

  // -----------------ANÁLISIS DE AUDIO-----------------
  let spectrum = fft.analyze(); 
  drawFlowVectors();
  updateFlowField();

  for (let m of medusas) {
    m.applyForce(m.follow(flowfield)); // Fuerza del campo de flujo
    m.applyForce(m.separate(medusas)); // Fuerza de separación (evita colisiones)
    
    // ---------------- MOTION 101-----------------
    m.update();
    m.display(spectrum); 
  }
}

class Medusa {
  constructor(banda) {
    // Estado físico inicial usando vectores
    this.pos = createVector(random(width), random(height));
    this.vel = p5.Vector.random2D();
    this.acc = createVector(0, 0);
    this.maxSpeed = random(3, 5); 
    this.maxForce = 0.3;
    
    this.rastroOral = [];
    this.tamBase = random(30, 60); 
    this.banda = banda; 
    this.hBase = random([180, 200, 280, 320]);
    
    this.energia = 0;// Energía suavizada para transiciones orgánicas
  }

  applyForce(f) { this.acc.add(f); }

  follow(ff) {
    let x = floor(constrain(this.pos.x / ff.resolution, 0, ff.cols - 1));
    let y = floor(constrain(this.pos.y / ff.resolution, 0, ff.rows - 1));
    let index = x + y * ff.cols;
    let desired = ff.field[index].copy().setMag(this.maxSpeed);
    return p5.Vector.sub(desired, this.vel).limit(this.maxForce);
  }

  separate(others) {
    let steer = createVector(0, 0);
    let count = 0;
    for (let other of others) {
      let d = dist(this.pos.x, this.pos.y, other.pos.x, other.pos.y);
      if (d > 0 && d < this.tamBase * 2) {
        steer.add(p5.Vector.sub(this.pos, other.pos).normalize().div(d));
        count++;
      }
    }
    if (count > 0) steer.div(count);
    return steer;
  }

  update() {
    // -----------------INTEGRACIÓN DE MOVIMIENTO-----------------
    this.vel.add(this.acc).limit(this.maxSpeed);
    this.pos.add(this.vel);
    this.acc.mult(0);

    // Gestión del rastro
    if (frameCount % 4 == 0) this.rastroOral.push(this.pos.copy());
    if (this.rastroOral.length > 7) this.rastroOral.shift();

    // Bordes infinitos
    if (this.pos.x < 0) this.pos.x = width;
    if (this.pos.x > width) this.pos.x = 0;
    if (this.pos.y < 0) this.pos.y = height;
    if (this.pos.y > height) this.pos.y = 0;
  }

  display(spectrum) {
    // -----------------REACTIVIDAD AL RITMO-----------------
    let nivelBanda = spectrum[this.banda];
    let targetEnergia = (nivelBanda > 105) ? map(nivelBanda, 105, 255, 0, 1) : 0;
    
    // Interpolación para que la reacción sea fluida y no brusca
    let ratio = (targetEnergia > this.energia) ? 0.2 : 0.05;
    this.energia = lerp(this.energia, targetEnergia, ratio);
    
    // Variables visuales derivadas de la música
    let tamAnimado = this.tamBase * (1 + (this.energia * 0.5));
    let sat = map(this.energia, 0, 1, 5, 95);
    let bri = map(this.energia, 0, 1, 15, 100);
    let alpha = map(this.energia, 0, 1, 5, 90); 

    // -----------------EFECTO BIOLUMINISCENTE-----------------
    drawingContext.shadowBlur = this.energia * 50;
    drawingContext.shadowColor = color(this.hBase, sat, bri, alpha);

    push();
    noFill();

    // DIBUJO DEL RASTRO
    for (let i = 0; i < this.rastroOral.length - 1; i++) {
      let p = this.rastroOral[i];
      stroke(this.hBase, sat, bri, map(i, 0, this.rastroOral.length, 0, alpha));
      strokeWeight(map(i, 0, this.rastroOral.length, tamAnimado * 0.4, 1));
      point(p.x, p.y);
    }

    // TENTÁCULOS (Oscilación con Seno)
    translate(this.pos.x, this.pos.y);
    rotate(this.vel.heading() + PI / 2);
    stroke((this.hBase + 25) % 360, sat * 0.7, bri, alpha * 0.5);
    strokeWeight(1);

    for (let t = 0; t < 6; t++) {
      let xOff = map(t, 0, 5, -tamAnimado * 0.7, tamAnimado * 0.7);
      beginShape();
      for (let j = 0; j < 8; j++) {
        let osc = sin(frameCount * 0.05 + j) * (10 * this.energia);
        let x = xOff + osc;
        let y = j * (tamAnimado * 0.4);
        curveVertex(x, y);
      }
      endShape();
    }

    // CABEZA
    fill(this.hBase, sat, bri, alpha * 0.4);
    stroke(this.hBase, sat, bri, alpha);
    strokeWeight(2);
    beginShape();
    for (let a = 0; a <= PI; a += 0.2) {
      let x = cos(a) * tamAnimado; // Coordenadas polares para generar la campana
      let y = sin(a) * tamAnimado * 0.7;
      vertex(x, -y);
    }
    endShape(CLOSE);
    pop();

    drawingContext.shadowBlur = 0; // Limpieza del buffer de sombra
  }
}

// --- CAMPO DE FLUJO ---

class FlowField {
  constructor(r) {
    this.resolution = r;
    this.cols = floor(width / r) + 1;
    this.rows = floor(height / r) + 1;
    this.field = new Array(this.cols * this.rows);
    // Inicialización de vectores (Corriente marina)
    for (let i = 0; i < this.field.length; i++) this.field[i] = createVector(1, 0);
  }
}

function drawFlowVectors() {
  let res = flowfield.resolution;
  stroke(200, 50, 100, 2);
  for (let i = 0; i < flowfield.cols; i++) {
    for (let j = 0; j < flowfield.rows; j++) {
      let v = flowfield.field[i + j * flowfield.cols];
      push(); translate(i * res + res/2, j * res + res/2);
      rotate(v.heading()); line(0, 0, res * 0.2, 0); pop();
    }
  }
}

function updateFlowField() {
  if (mouseIsPressed) { // Interacción Mouse-Fuerza
    let res = flowfield.resolution;
    let mouseV = createVector(mouseX - pmouseX, mouseY - pmouseY);
    if (mouseV.mag() > 0.1) {
      mouseV.normalize();
      for (let i = 0; i < flowfield.cols; i++) {
        for (let j = 0; j < flowfield.rows; j++) {
          if (dist(mouseX, mouseY, i * res, j * res) < 150) {
            flowfield.field[i + j * flowfield.cols].lerp(mouseV, 0.3);
          }
        }
      }
    }
  }
}

function mousePressed() {
  if (!audioIniciado) {
    userStartAudio();
    song.loop();
    audioIniciado = true;
  }
}

function drawMessage() {
  fill(0, 0, 100);
  noStroke();
  textAlign(CENTER, CENTER);
  textSize(20);
  text("BTS - SEA\nHaz clic para despertar el océano", width / 2, height / 2);
}
```

🌟[Sketch](https://editor.p5js.org/VanDiosa/sketches/fFCxRD9qX)    
🌟[Pantalla Completa](https://editor.p5js.org/VanDiosa/full/fFCxRD9qX)

📸Capturas     
<img width="1919" height="791" alt="Captura de pantalla 2026-04-17 085653" src="https://github.com/user-attachments/assets/54960177-87de-4b0b-a733-8d98c0a87c6f" />

<img width="1918" height="801" alt="Captura de pantalla 2026-04-17 085745" src="https://github.com/user-attachments/assets/3cce60ee-d9ee-4e3b-abe1-384bd110293f" />


## Bitácora de reflexión
