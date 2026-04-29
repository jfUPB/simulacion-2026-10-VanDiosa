# Unidad 7

## Bitácora de proceso de aprendizaje   
### Actividad 01   
📤En base al trabajo de [Ji Lee](https://pleaseenjoy.com/#/word-as-image/), responder lo planteado:   

✍️Análisis de ejemplos de Ji Lee   
  <img width="202" height="202" alt="ACT1 1 1" src="https://github.com/user-attachments/assets/44a60112-9c3c-453e-b87b-9fb91456abde" />
  La letra "C" actua como una boca que se come al resto de los caracteres. El caos de las letras internas representa la acumulación y el desorden, dos caracteristicas propias del consumo excesivo   
  <img width="200" height="201" alt="ACT1 1 2" src="https://github.com/user-attachments/assets/11034e01-d798-4682-9b11-2d7f3ae28c6f" />
  Utiliza la jerarquia de escala. La letra "I" central crecio desmedidamente hasta aplastar a las demas, buscando simbolizar como un sistema prioriza un elemento sobre la base de la estructura   
  <img width="198" height="200" alt="ACT1 1 3" src="https://github.com/user-attachments/assets/68393838-3335-416e-beb5-87aea75ef890" />
  Al separar la "G" y colocarla debajo, Ji Lee hace una referencia historica y anatomica a la oreja cortada del artista, es como si el nombre fuera un retrato   

❓¿Cómo la manipulación tipográfica refuerza el significado?   
La manipulación tipografica no es solamente decorativa, si no funcional. Ji Lee usa:   
+ La escala para mostrar poder o presion
+ El desplazamiento para sugerir eventos o acciones (como caer o amputar)
+ La sustitución de partes de letras por formas geometricas (montañas, manecillas de reloj) para anclar la palabra a un objeto
Ji Lee busca reforzar el significado porque obliga al ojo a no solo leer la palabra, sino a interpretarla como un objeto con peso, historia y contexto

✍️Propuestas de palabras propias (Representación Visual)   
<img width="2480" height="3508" alt="ACT1 DIBUJOS" src="https://github.com/user-attachments/assets/3a96d473-bc7f-4523-84fb-a04d77d260e0" />

+ FRAGIL-> Una tipografia con grietas. Las letras "F-R--G-I-L" estan fijas y muy apretadas entre si, dejando un hueco muy exacto para la letra "A". La letra "A" se encuentra aislada y caida, esperando que alguien la coloque

+ DERRETIR-> Letras cuadradas y gruesas, de color celeste, para dar a entender que son hielos. El fondo muestra particulas cayendo (nieve). En el escenario hay un sol el cual segun su cercania va derritiendo mas rapido o mas lento la palabra

+ SOL-> El escenario es un cielo azul oscuro. Las letras "S--L" estan camufladas con el color del fondo, pero aun asi tienen un espacio entre ellas. La letra "O" es un circulo brillante y calido que actaa como un sol, iluminando lo que tiene cerca

✍️Palabra seleccionada   
La palabra que mas me interesa desarrollar es "FRAGIL". Elegi esta ya que presenta un reto de precision y tension, donde el usuario debe interactuar con extremo cuidado; si la comparo con las otras palabras que son mas atmosfericas, pienso que "FRAGIL" es mas desafiante

### Actividad 02    
📤Luego de estudiar el capitulo del libro relacionado con [Matter.js](https://natureofcode.com/physics-libraries/)    

✍️Explica con tus palabras qué hace cada uno de esos conceptos:    
+ Engine: Motor -> Es el cerebro que calcula la fisica. No se ve fisicamente, pero el toma decisiones cuadro a cuadro, hacia donde cae cada cosa o como chocan, todo basado en leyes matematicas
+ World: Mundo -> Es el escenario donde todo sucede; en donde se añaden lo objetos y donde existen las fuerzas globales (por ejemplo la gravedad)
+ Bodies: Cuerpos -> Son los objetos fisicos (rectangulos, circulos o formas complejas). Tienen propiedades como masa, friccion, rebote, etc. Sin un cuerpo, una letra es solo un dibujo, ya que el cuerpo le permite ser un objeto que se cae y golpea
+ Constraint (Restriccion) -> Es una cuerda, resorte o clavo que une dos cuerpos, o un cuerpo a un punto fijo
+ MouseConstraint -> Es la herramienta que permite que el usuario pueda manipular el mundo fisico, atraves del cursor puede agarrar, arrastrar y lanzar cuerpos

✍️Replica al menos dos experimentos básicos integrando Matter.js con p5.js    

📎📸Incluye código y capturas o enlaces   

✍️Describe qué tipo de comportamiento físico te interesa explorar en tu palabra    
Luego de pensar varias opciones, el comportamiento final para FRÁGIL es que, si el usuario no tiene cuidado, la fisica lo "castigue"

Quiero intentar que las letras F-R--G-I-L se vean fragmentadas y que tengan un limite de aguante. El usuario debe colocar la letra A en su lugar; si lo hace con demasiada fuerza, velocidad o sin precisión, el golpe contra las otras letras ocasionara que estas se desmoronen por el impacto

La idea es que la garra (MouseConstraint) no se sienta rigida o estable, sino como si la letra estuviera colgando de un hilo inestable. De esta forma, el usuario se ve obligado a moverse con calma y cautela. En resumen, la fisica de esta pieza debe transmitir la sensación constante de estar a punto de romperse

### Actividad 03    
✍️Realiza al menos dos experimentos simples de audio-reactividad   

✍️Explica qué dato estás leyendo del audio    

✍️Explica qué comportamiento visual o físico activa ese dato   

✍️Describe qué tipo de respuesta sonora te serviría más para tu palabra y por qué   
Pense para mayor inmersion, pense en utilizar la amplitud (captada por el microfono) del sonido ambiente como fuente de perturbacion, que sea como una vibracion fisica sobre la letra A

De esta forma si el lugar esta en silencio, el nivel de complejidad para colocarla sera el normal/basico. Pero, si el microfono detecta picos de amplitud (un aplauso, un grito o musica fuerte), esa energia producira un temblor fisico aplicado a la letra

¿Por que este dato?   
Porque añade una capa de dificultad a la pieza. El usuario no solo tiene que ser preciso con la mano (mouse), sino que debe guardar silencio o controlar el entorno sonoro para que la letra no vibre demasiado. Si hay mucho ruido, la letra A temblara tanto que sera mas dificil encajarla sin golpear y destruir el resto de la palabra. Quiero dar a entender que la fragilidad no se encuentra solo en el objeto si no en el entorno en el que existe

### Actividad 04   
🔗 Muestra una prueba inicial   
[Sketch prueba](https://editor.p5js.org/VanDiosa/sketches/GsfldQElj)

<img width="475" alt="ACT4 1" src="https://github.com/user-attachments/assets/728749ff-96bf-4653-8854-af4050dfb65e" />
<img width="475" alt="ACT4 2" src="https://github.com/user-attachments/assets/96209535-bf49-4e05-9720-397bf1789def" />


✍️Explica qué parte de la palabra construiste    
Para esta exploracion, me queria enfocar en la respuesta al audio con sentido semantico. Especificamente construi la letra A (sencilla), mientras que el resto de las letras estan representadas por bloques rectangulares estaticos

✍️Explica qué propiedad física manipulaste   
He manipulado tres propiedades clave de los cuerpos en Matter.js:
+ FrictionAir (Fricción de aire): La configure en un valor de 0.05 para que el movimiento de la letra no sea tan constante, dandole una sensación de peso y resistencia
+ Restitution (Rebote): Ajustada en 0.5 para que las colisiones no sean elasticas, sino que la letra pierda energia al chocar, reforzando la idea de algo que se golpea y se detiene
+ isStatic: Los bloques secundarios inician con esta propiedad en true para que parezcan solidos, pero se cambia a false tras recibir un impacto de la letra "A" con suficiente velocidad

✍️Explica qué aspecto del audio afecta qué comportamiento    
Utilice la Amplitud (volumen) capturada directamente desde el microfono. El nivel de volumen se mapea para generar impulsos de fuerza (vectorial) en direcciones aleatorias mediante el comando applyForce

Implemente un umbral (volDirecto > 0.06) para que el sistema ignore el ruido de fondo y solo reaccione a sonidos intencionales como la voz, haciendo que la letra vibre proporcionalmente a la intensidad del grito o el habla

✍️Evalúa qué funcionó y qué no para el significado que quieres construir    
+ Lo que funciono -> La integracion de la fisica con el audio es exitosa. La letra reacciona cuando hay ruido, lo cual transmite perfectamente el concepto de fragilidad ante el entorno. El uso de un limitador de velocidad fue clave para que la pieza no se enloqueciera visualmente y se mantuviera dentro del canvas
+ Lo que NO funciono -> Al principio, el microfono no detectaba nada y la letra no se movia. Al intentar arreglarlo, se volvio tan sensible que cualquier ruido pequeño (como roces) hacia que la letra saliera disparada fuera de la pantalla. Me tomo varias pruebas para lograr que se se viera bien, tenia que limitar la velocidad de la letra y filtrar los ruidos de fondo, para que el movimiento fuera una vibracion tensa y no un error donde la pieza simplemente desapareciera de la pantalla


## Bitácora de aplicación 
### Actividad 05 - FRÁGIL: Fractura Profunda 🪨🔨    
✍️Palabra elegida    
FRÁGIL   

✍️Justificación conceptual

✍️Análisis de su significado visual y comportamental.

✍️Moodboard o referencias    
<img width="1920" height="1080" alt="MOODBOARDU7" src="https://github.com/user-attachments/assets/7a5c16d9-a978-429f-8121-952f663338c5" />

✍️Bocetos    
<img width="2480" height="1004" alt="ACT1 DIBUJOS - copia" src="https://github.com/user-attachments/assets/f13eca65-43dc-497d-acff-67f0d39aa321" />

✍️Mapa de decisiones     


✍️Mapa de interpretación    
+ La Garra: Representa la manipulacin externa o el control. El usuario tiene el poder de decidir cuando y donde aplicar la fuerza
+ La Letra Á: Funciona como el catalizador del caos. Su color rojo vibrante contrasta con el gris de las demas, marcandola como un objeto de peligro o energia pura
+ El Colapso: La destruccion de las letras fijas representan una perdida de la estructura
+ La Voz como Vibración: El volumen capturado por el microfono no se interpreta como musica, sino como energia. Se convierte el sonido en una fuerza invisible que puede desestabilizar la letra A, interpretando la voz como una herramienta de caos que pone a prueba la resistencia de lo que parecia seguro

✍️Explicación de la relación entre audio y comportamiento    
El volumen capturado (volDirecto) se traduce en un vector de fuerza aleatorio aplicado al centro de masa de la letra roja. A mayor volumen, la letra se sacude con más violencia

🤖Evidencia del uso de IA.

✍️Código fuente    
```js
/**
 * ACTIVIDAD 05: FRÁGIL - Fractura Profunda
 */

let engine, world, letraA, bloques = [];
let constraintGarra, volDirecto = 0, audioIniciado = false;
const { Engine, World, Bodies, Constraint, Vector, Body, Events } = Matter;

function setup() {
  createCanvas(windowWidth, windowHeight);
  engine = Engine.create();
  world = engine.world;
  world.gravity.y = 1.3;
  
  // Ajuste para colisiones más precisas
  engine.enableSleeping = false; 

  // 1. LÍMITES ULTRA-GRUESOS (Blindaje de 500px)
  World.add(world, [
    Bodies.rectangle(width/2, height + 250, width, 500, { isStatic: true, label: 'suelo' }),
    Bodies.rectangle(-250, height/2, 500, height * 2, { isStatic: true }), // Pared Izq
    Bodies.rectangle(width + 250, height/2, 500, height * 2, { isStatic: true }), // Pared Der
    Bodies.rectangle(width / 2, height / 2 + 175, 161, 15, { isStatic: true, label: 'soporte' })
  ]);

  let cx = width / 2;
  let cy = height / 2 + 80;

  createLetra(cx - 275, cy - 15, 110, 180, 'F', 0.18);
  createLetra(cx - 165, cy, 110, 180, 'R', -0.06); 
  createLetra(cx + 126, cy, 125, 180, 'G', 0.10); 
  createLetra(cx + 226, cy, 60, 180, 'I', -0.15);
  createLetra(cx + 326, cy, 110, 180, 'L', 0.08);

  letraA = Bodies.rectangle(width - 200, height - 120, 130, 155, {
    restitution: 0.1, frictionAir: 0.01, density: 0.005, label: 'Á'
  });
  Body.setAngle(letraA, PI/2); 
  World.add(world, letraA);

  Events.on(engine, 'collisionStart', (event) => {
    event.pairs.forEach(pair => {
      verificarYQuebrar(pair.bodyA, pair.bodyB);
      verificarYQuebrar(pair.bodyB, pair.bodyA);
    });
  });
}

function draw() {
  background(230, 230, 235);
  Engine.update(engine);
  dibujarMonitorAudio();
  
  // 2. SEGURO MANUAL: Si la letra intenta fugarse, la devolvemos
  if (letraA.position.x < 0) Body.setPosition(letraA, { x: 50, y: letraA.position.y });
  if (letraA.position.x > width) Body.setPosition(letraA, { x: width - 50, y: letraA.position.y });

  bloques.forEach(b => dibujarObjeto(b));
  dibujarObjeto(letraA);

  if (constraintGarra) {
    constraintGarra.pointA = { x: mouseX, y: mouseY };
    stroke(100, 150); strokeWeight(1.5);
    let posB = Vector.add(letraA.position, Vector.rotate(constraintGarra.pointB, letraA.angle));
    line(mouseX, mouseY, posB.x, posB.y);
  }

  if (audioIniciado && volDirecto > 0.03) {
    let s = volDirecto * 45; 
    Body.applyForce(letraA, letraA.position, { x: random(-s, s), y: random(-s, s) });
  }

  drawGarraPro();
}

function dibujarObjeto(b) {
  push();
  translate(b.position.x, b.position.y);
  rotate(b.angle);
  
  let col = (b.label === 'Á' || b.parentTxt === 'Á') ? color(190, 50, 50) : color(110, 115, 120);

  if (b.label === 'fragmento') {
    fill(col); noStroke();
    beginShape();
    // Dibujamos usando los vértices reales del cuerpo para que la forma sea exacta
    b.vertices.forEach(v => vertex(v.x - b.position.x, v.y - b.position.y));
    endShape(CLOSE);
  } else {
    textAlign(CENTER, CENTER); textFont('Arial Black'); textSize(180);
    fill(red(col)-60, green(col)-60, blue(col)-60);
    text(b.label, 7, 9);
    fill(col); noStroke();
    text(b.label, 0, 0);

    randomSeed(b.id);
    stroke(255, 140); 
    for(let i=0; i<8; i++) {
      strokeWeight(random(1, 4));
      let x = random(-40, 40); let y = random(-60, 60);
      line(x, y, x + random(-30, 30), y + random(-30, 30));
    }
  }
  pop();
}

function verificarYQuebrar(objA, objB) {
  if (objA.label === 'Á' && objB.isStatic && objB.label !== 'fragmento' && objB.label !== 'soporte' && objB.label !== 'suelo') {
    for (let i = bloques.length - 1; i >= 0; i--) {
      if (bloques[i] === objB) {
        generarFragmentosPoligonales(objB);
        bloques.splice(i, 1);
        World.remove(world, objB);
      }
    }
  }
}

function generarFragmentosPoligonales(body) {
  let div = 5; 
  let w = body.w / div;
  let h = body.h / div;

  for (let i = 0; i < div; i++) {
    for (let j = 0; j < div; j++) {
      let ox = (j - div/2) * w;
      let oy = (i - div/2) * h;
      
      // Vértices irregulares
      let puntos = [
        { x: ox - w/2 + random(-8, 8), y: oy - h/2 + random(-8, 8) },
        { x: ox + w/2 + random(-8, 8), y: oy - h/2 + random(-8, 8) },
        { x: ox + w/2 + random(-8, 8), y: oy + h/2 + random(-8, 8) },
        { x: ox - w/2 + random(-8, 8), y: oy + h/2 + random(-8, 8) }
      ];

      let p = Bodies.fromVertices(body.position.x + ox, body.position.y + oy, puntos, {
        isStatic: false, friction: 0.5, density: 0.001
      });

      if (p) {
        p.label = 'fragmento';
        p.parentTxt = body.label;
        Body.setVelocity(p, { x: random(-4, 4), y: random(-4, 2) });
        World.add(world, p);
        bloques.push(p);
      }
    }
  }
}

// Funciones de soporte
function createLetra(x, y, w, h, label, angle) {
  let b = Bodies.rectangle(x, y, w, h, { isStatic: true, label: label });
  b.w = w; b.h = h; Body.setAngle(b, angle);
  bloques.push(b); World.add(world, b);
}

function mousePressed() {
  if (!audioIniciado) activarAudio();
  let mouseVec = { x: mouseX, y: mouseY };
  if (Matter.Bounds.contains(letraA.bounds, mouseVec)) {
    let offset = Vector.sub(mouseVec, letraA.position);
    let rotatedOffset = Vector.rotate(offset, -letraA.angle);
    constraintGarra = Constraint.create({
      pointA: { x: mouseX, y: mouseY }, bodyB: letraA, pointB: rotatedOffset, stiffness: 0.25, length: 0
    });
    World.add(world, constraintGarra);
    letraA.friction = 0;
  }
}

function mouseReleased() {
  if (constraintGarra) { World.remove(world, constraintGarra); constraintGarra = null; letraA.friction = 0.5; }
}

function drawGarraPro() {
  push(); translate(mouseX, mouseY);
  stroke(60); strokeWeight(2); line(0, -mouseY, 0, -20);
  rectMode(CENTER); fill(80, 85, 95); noStroke(); rect(0, -15, 45, 25, 4);
  stroke(50); strokeWeight(6); noFill();
  beginShape(); vertex(-15, 0); bezierVertex(-25, 10, -40, 25, -30, 45); endShape();
  beginShape(); vertex(15, 0); bezierVertex(25, 10, 40, 25, 30, 45); endShape();
  pop();
}

function dibujarMonitorAudio() {
  push(); fill(100, 30); noStroke(); rect(width-110, 20, 90, 15, 4);
  if (audioIniciado) { fill(100, 150, 255, 180); rect(width-110, 20, map(volDirecto, 0, 0.4, 0, 90), 15, 4); }
  pop();
}

async function activarAudio() {
  const stream = await navigator.mediaDevices.getUserMedia({ audio: true });
  const audioCtx = new (window.AudioContext || window.webkitAudioContext)();
  const source = audioCtx.createMediaStreamSource(stream);
  const processor = audioCtx.createScriptProcessor(2048, 1, 1);
  source.connect(processor); processor.connect(audioCtx.destination);
  processor.onaudioprocess = (e) => {
    let input = e.inputBuffer.getChannelData(0);
    let sum = 0; for (let v of input) sum += v*v;
    volDirecto = Math.sqrt(sum / input.length);
  };
  audioIniciado = true;
}
```

🌟[Sketch](https://editor.p5js.org/VanDiosa/sketches/xJKX4DySV)    
🌟[Pantalla Completa](https://editor.p5js.org/VanDiosa/full/xJKX4DySV)

📸Capturas o registros de la pieza.
<img width="941" height="732" alt="ACT 5 1" src="https://github.com/user-attachments/assets/b4662162-94fb-4b06-b4b8-a3ff2d71f076" />

-
<img width="954" height="728" alt="ACT 5 2" src="https://github.com/user-attachments/assets/a61690f3-96df-4da2-bc4b-15f50989ff38" />

-
<img width="944" height="723" alt="ACT 5 3" src="https://github.com/user-attachments/assets/34065836-9eb5-4559-8658-8d0e376092ce" />

-
## Bitácora de reflexión
