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


## Bitácora de reflexión


