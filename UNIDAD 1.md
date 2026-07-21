# ☄️UNIDAD 1

La gracia de una bitacora es poder poner alli todos tus analisis y descubrimientos a medida que avanzas en la unidad.

Quizas no es obligatorio hacer esto y a la persona que quizaaaaaaas lo lea le de cancer visual pq Sara Ruiz es horrible escribiendo en el teclado de un pc.
Pero aun asi quiero documentar todo. lo encuentro divertido...

## 🌟 ACTIVIDAD 1

- ✨ **ANÁLISIS DE VIDEOS**
>
> Me parece impresionante las miles de maneras tan diferentes que los artistas tienen para describir este arte de tipo generativo. Pero todos coinciden en lo mismo... 
> Que la aleatoriedad es uno de los factores mas importantes.
>
> Me encanta porque este tipo de arte es el que personalmente para mi representa mejro para mi lo inexplicable que son las emociones humanas.
> Ya que cuando sentimos emociones nunca sabremos que tan fuerte nos van a afectar dependiendi del contexto de la situación, lo mismo es aqui, todos los artistas 
> mencionan que siempre tienen eideas al empezar pero que jamas saben como va a quedar el resultado final.

## 🌟 ACTIVIDAD 2

- ✨ **ANÁLISIS CODIGO EXAMPLE 0.1: A TRADITIONAL RANDOM WALK**
>
> Este ejemplo me gusta y es bastante sencillo porque utiliza una probabilidad uniforme para seleccionar culaquier digito del 0 al 4 para mover o dibujar nuevas 
> posiciones del cuadrito en el siguiente frame (sin borrar el frame anterior)

## 🌟 ACTIVIDAD 3

- ✨ **DIFERENCIA ENTRE LA DISTRIBUCIÓN UNIFORME Y NO UNIFORME DE NÚMEROS ALEATORIOS**
>
> Cuando hablamos de la distribucion uniforme nos referimos a que haya una probabilidad igual o establedia para sacar un resultado en particular. Cuando hablamos 
> de la no uniforme es cuando esa probabilidad para sacar cualquier valor se ve sesgado por cualquier circunstancia y deja de ser uniforme.
> 
> Hagamos un ejemplo con los numero aleatorios. supongamos que del 0 al 4 hay 0.25% de probabilidades de sacar cualquier numero, es bastante equitativo. 
> peeeeeeeeeero, la cosa cambia si por ejemplo tengo valores desde el -5 hasta el 25, obviamente hay mas posibilidades de sacar un numero posiivo que uno negativo,
> porque, obviamente los resultados se segan ya que di mas valores positivos que negativos.

- ✨ **CÓDIGO CON DISTRIBUCIÓN NO UNIFORME**
>
> El ejercicio era bastante sencillo. Bastaba con modificar las probabilidades en el codigo de modo en que existieran mas facilidad para irse por un lado en 
> particular. (Para el caso de la clase, la idea era hacer que tuviera una tendencia hacia la derecha)

```JavaScript
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
    this.x = width / 2;
    this.y = height / 2;
  }

  show() {
    stroke(0);
    point(this.x, this.y);
  }

  step() {
    const choice = floor(random(4));
    if (choice == 0 || choice == 1) {
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
```
## 🌟 ACTIVIDAD 4 

- ✨ **ANÁLISIS CODIGO EXAMPLE 0.1: A TRADITIONAL RANDOM WALK**
>
> Okay okay, digamos que a la final hice algo similar pero diferente....
>
> Inicialemnte pensé. hey, y en vez de que sea en una linea lo haga en forma de estrella. entonces a medida qye pasa el tiempo se va formando una estrella y no una linea. Claude hizo el siguiente código.
>
```JavaScript
let starPoints;

function setup() {
  createCanvas(640, 240);
  background(255);
  starPoints = makeStar(320, 120, 40, 100, 5); // centro, radio interno, radio externo, puntas
}

function draw() {
  // 1. Elegir un punto al azar a lo largo del contorno de la estrella
  let t = random(starPoints.length);
  let i = floor(t);
  let next = (i + 1) % starPoints.length;
  let lerpAmt = t - i;

  let baseX = lerp(starPoints[i].x, starPoints[next].x, lerpAmt);
  let baseY = lerp(starPoints[i].y, starPoints[next].y, lerpAmt);

  // 2. Aplicar dispersión gaussiana alrededor de ese punto del contorno
  let x = randomGaussian(baseX, 4);
  let y = randomGaussian(baseY, 4);

  noStroke();
  fill(0, 10);
  circle(x, y, 8);
}

// Genera los vértices de una estrella de n puntas
function makeStar(cx, cy, innerR, outerR, n) {
  let pts = [];
  let angleStep = PI / n;
  for (let i = 0; i < n * 2; i++) {
    let r = i % 2 === 0 ? outerR : innerR;
    let angle = i * angleStep - HALF_PI;
    pts.push(createVector(cx + r * cos(angle), cy + r * sin(angle)));
  }
  return pts;
}
```
> y se veia asi despues de unos 10 segundos mas o menos
> 
> <img width="832" height="376" alt="image" src="https://github.com/user-attachments/assets/30e94eaf-87e1-4592-ad54-0d49b190c5a8" />
>
> Pero despues dije. que pelle. Entonces pense que esos trazos parecen a cuando dibujas y dependiendo de tu pulso y que tan fuerte estas apretando, aparecen tonos mas oscuros o mas claros. Asi que en vez de que formara una estrella, pedi que mateara la posicion del mouase en cada frame para ase crear un trazo personalizado. Claude generó esto.
> 
```JavaScript
function setup() {
  createCanvas(500, 500);
  background(200); // solo se llama una vez, en setup
}

function draw() {
  // La media de la gaussiana ahora es la posición del mouse
  let x = randomGaussian(mouseX, 5);
  let y = randomGaussian(mouseY, 5);

  noStroke();
  fill(0, 10);
  circle(x, y, 16);
}
```
> Despues de algunos intentos trate de hacer una carita feliz. no se si se entiende jajaja
>
> <img width="667" height="662" alt="Captura de pantalla 2026-07-21 181315" src="https://github.com/user-attachments/assets/53b7b45d-2e7e-4f5c-ba47-70922ebf4481" />
>
> Y despues dije. le falta para que cambies el color.... entonces claude genero lo siguiente
>
```JavaScript
let currentColor;

function setup() {
  createCanvas(500, 500);
  background(200);
  currentColor = [0, 0, 0]; // negro por defecto

  createButton('Negro').mousePressed(() => currentColor = [0, 0, 0]);
  createButton('Blanco').mousePressed(() => currentColor = [255, 255, 255]);
  createButton('Amarillo').mousePressed(() => currentColor = [255, 220, 0]);
  createButton('Azul').mousePressed(() => currentColor = [30, 100, 240]);
  createButton('Rojo').mousePressed(() => currentColor = [230, 30, 30]);
}

function draw() {
  let x = randomGaussian(mouseX, 5);
  let y = randomGaussian(mouseY, 5);

  noStroke();
  fill(currentColor[0], currentColor[1], currentColor[2], 10);
  circle(x, y, 16);
}
```
> Y consegui pintar esto (de algo me tenia que servir teoria del color)
> <img width="657" height="648" alt="image" src="https://github.com/user-attachments/assets/094fd7e3-95af-43ab-b7ec-edb4018ff0c4" />
