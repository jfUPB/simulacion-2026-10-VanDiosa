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

⭐[Sketch en p5.js]() que representa una distribución normal de otra forma. El profe nos dijo q partieramos del ejemplo y lo modificaramos, asi quedo el codigo:

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


## Bitácora de aplicación 


## Bitácora de reflexión

