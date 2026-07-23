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

- ✨ **SKETCH EN P5JS QUE REPRESENTE LA DISTRIBUCIÓN NORMAL**
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
> Despues de algunos intentos trate de hacer una araña???. no se si se entiende jajaja
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
> 
> <img width="657" height="648" alt="image" src="https://github.com/user-attachments/assets/094fd7e3-95af-43ab-b7ec-edb4018ff0c4" />

## 🌟 ACTIVIDAD 5

- ✨ **MODIFICACION DEL TRADITIONAL RANDOM WALK CON LÉVY FLIGHT**
>
> La verdad es que aunque entendi el concepto del levy flight, no super incorporrarlo por mi cuenta. hice uso de claude para la actividad. esto es lo que generó
>
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
    // Genera un número siguiendo la distribución y = x
    // (valores grandes son más probables que los chicos)
    const r = this.levyValue();

    // r va de 0 a 1. Lo escalamos para que sea el "tamaño de paso".
    // Elevamos a una potencia para exagerar los saltos grandes y ocasionales.
    const stepSize = pow(r, -2); // esto puede dar números MUY grandes a veces

    const xstep = random(-1, 1) * stepSize;
    const ystep = random(-1, 1) * stepSize;

    this.x += xstep;
    this.y += ystep;
  }

  // Distribución donde los valores grandes tienen más probabilidad (y = x)
  levyValue() {
    let x, y;
    do {
      x = random(1); // candidato
      y = random(1); // "umbral" de aceptación
    } while (y > x); // si el umbral es más alto que el candidato, se rechaza y se reintenta
    return x;
  }
}
```
> y asi se ve
> 
> <img width="811" height="345" alt="image" src="https://github.com/user-attachments/assets/e1e16743-00d7-4ba2-a88d-ff9951ca6d06" />

- ✨ **EXPLICACIÓN DE LA TÉCNICA**
>
> A ver, las primeras veces lo que hice fue tratar de poner el fragmento de codigo de la pagina de explicacion donde se establece la probabilidad de salto, pero la verdad es que no funciono. el codigo no parecia hacer nada particular o no funcionaba. lo que esperaba obtener en estos intentos era que el random walk ya no fuesen lineas sino puntos en lugares mas separados como minimo.
>
> Dado que mi iq no es suficiente, recurri a la ia. Claude aquí no se establece un valor fijo para crear el salto de distancia larga. Sino que el valor cambia en cada frame. Para ello la función llamada levyValue lo que hace es sacar dos valores aleatorios, x e y. Si x de chepa es menor que y, se rechaza ese intento y se vuelve a probar con un nuevo,  par de x e y (eso es lo que hace el while). Esto se repite hasta que x sea mayor o igual que y, recién ahí se acepta ese x y se lo devuelve como el valor final. x termina siendo el valor de r... Dentro de estos ciclos, hay un 90% de probabilidades de que salga un valor muy grande y solo un 10% de probabilidades de que salga un valor pequeño (es que necesitamos para la condicion de salto)
>
> Luego en la linea const stepSize = pow(r, -2), lo que hace es 1/r^2, de modo en que los valores grandes (que casi siempre salen) se traducen como movimientos super pequqños en el lienzo) y los valores peques (los dificiles de sacar) se traducen como movimientos enooormes en el lienzo.
>
> Funciona este metodo por el while que se hace en cada frame se puede hacer mas facil o mas dificil de superar.

## 🌟 ACTIVIDAD 6

- ✨ **RUIDO DE PERLIN APLICADO A UN NUEVO EJEMPLO**
>
> POR ALGUN MOTIVO ME COSTO ENTENDER EL RUIDO DE PERLIN. Y ES BIEN BOBO. No se porque empece a interpretar el ruido de perlin al revés. crei que el ruido de perlin era que los valores aleatorios eran completamente diferentes unos de si, Y ERA AL REVESSS, el ruido de perlin te da como de a conjuntos de numeros, pues, como que incrementa o disminuye valores pero muy suavemente, no de manera brusca, obviamente sin salirse de lo aleatorio
>
> Para el ejercicio hice uso 1000% de claude, porque queria visualizar el ruido de perlin en un entorno 3d. Algo asi como un generador de mapas 3d o de relieves 3d. Me gusta crear historias de fantasia, pero muchas veces me cuesta imagianrme el relieve de un entorno ficticio. siempre quise tener una especie de generador de mapas personalizado para hacer mis propios mapas pero en 3d, no como los genericos en 2d...entonces por eso pense que seria genial hacer el ejercicio en 3d....
>
> obviamente aqui no estoy personalizando nada, pero es cool ver un relieve simulado en 3d 
>
```JavaScript
let cols, rows;
let scl = 20;
let w = 1200;
let h = 1200;
let terrain = [];
let noiseScale = 0.1;
function setup() {
  createCanvas(700, 600, WEBGL);
  cols = w / scl;
  rows = h / scl;
  let yoff = 0;
  for (let y = 0; y < rows; y++) {
    let xoff = 0;
    let row = [];
    for (let x = 0; x < cols; x++) {
      row.push(map(noise(xoff, yoff), 0, 1, -100, 100));
      xoff += noiseScale;
    }
    terrain.push(row);
    yoff += noiseScale;
  }
}
function draw() {
  background(20);
  orbitControl();
  rotateX(PI / 3);
  translate(-w / 2, -h / 2);
  stroke(120, 200, 255);
  noFill();
  for (let y = 0; y < rows - 1; y++) {
    beginShape(TRIANGLE_STRIP);
    for (let x = 0; x < cols; x++) {
      vertex(x * scl, y * scl, terrain[y][x]);
      vertex(x * scl, (y + 1) * scl, terrain[y + 1][x]);
    }
    endShape();
  }
}
```
>
> Se visualiza algo asi
>
> <img width="892" height="677" alt="image" src="https://github.com/user-attachments/assets/60723544-3c87-4098-a677-1af123ba22bc" />
>
> Lamentablemente tras ejecutarse normalmente aparece un error, y el programa se para debido a que siente multiples loops funcionando al tiempo.
>
> Segun entiendo es debido a la densidad de la malla con la que se trabaja. Si bajo la malla, la VERDAD la magia con el ruido de perlin se pierde
>
> PERO HEEEY, y si lo animamos? Veamos que logramos.
>
```JavaScript
let cols, rows;
let scl = 40;      // grilla menos densa para que la animación sea fluida
let w = 1200;
let h = 1200;
let terrain = [];
let noiseScale = 0.1;
let zoff = 0;       // el offset que avanza con el tiempo

function setup() {
  createCanvas(700, 600, WEBGL);
  pixelDensity(1);
  cols = w / scl;
  rows = h / scl;
}

function draw() {
  background(20);
  orbitControl();
  rotateX(PI / 3);
  translate(-w / 2, -h / 2);

  // Recalcular el terreno cada frame, usando zoff como "tiempo"
  let yoff = 0;
  terrain = [];
  for (let y = 0; y < rows; y++) {
    let xoff = 0;
    let row = [];
    for (let x = 0; x < cols; x++) {
      row.push(map(noise(xoff, yoff, zoff), 0, 1, -100, 100));
      xoff += noiseScale;
    }
    terrain.push(row);
    yoff += noiseScale;
  }
  zoff += 0.01; // avanzar de a poquito en la tercera dimensión

  stroke(120, 200, 255);
  noFill();
  for (let y = 0; y < rows - 1; y++) {
    beginShape(TRIANGLE_STRIP);
    for (let x = 0; x < cols; x++) {
      vertex(x * scl, y * scl, terrain[y][x]);
      vertex(x * scl, (y + 1) * scl, terrain[y + 1][x]);
    }
    endShape();
  }
}
```
>
> Lamentanblemente no puedo adjuntar video. pero se ve interesante
>
> He aqui unas capturas.
>
><img width="903" height="667" alt="image" src="https://github.com/user-attachments/assets/69636081-ce59-46f3-a9e9-43287d26835d" />
><img width="897" height="682" alt="image" src="https://github.com/user-attachments/assets/d0c7349c-24a6-42e8-81df-e0dd2cd5cee4" />
><img width="887" height="665" alt="image" src="https://github.com/user-attachments/assets/c32ea60e-019b-4436-bd91-36f5c961cd57" />
>
>Obviamente tuve que rebajarle a la densidad de la malla aqui, pero siento que no se ve maaaal estando animado...

## 🌟 ACTIVIDAD 7: RETO DE DISEÑO

- ✨ **FASE DE IDEACIÓN**
>
> Antes de empezar a tirar prompts a claude necesitaba una idea para trabajar. He de admitir que cuando me dicen "piensa que estos es para una feria o para una empresa" la verdad es que me bloquea durisimo. ya no me deja idear con completa libertad.
>
> Pese a ello, pude idear las dos siguientes ideas.
>
> 1: Mi primera opción fue crear una especie de simulador de evolucion de relieves del planeta. Es decir, en pantalla se veria como un territorio podria evolucionar (crear rios, montañas, valles, etc etc) y dichos comportamientos estarian definidos por varias distrubuciones diferentes.
>
> Para la interactividad estaba pensando que el usuario representara desastres naturales o cosas que afectan el flujo de la evolucion.
>
> Entonces, por ejemplo, en el plano se estan formando dos montañas y un rio, pero el usuario decide interactuar y manda un terremoto, o una inundación. afectando el flujo evolutivo. el rio pudo verse bloqueado por piedras de una de las montañas, o una de las montañas se derrumbo o etc etc. cosas asi
>
> 2. Mi segunda opcion esta inspirada en la novela del problema de los tres cuerpos. En resumen, existe un planeta lejano que esta orbitado por 3 estrellas inestables que irremediablemente acaban chocando con el planeta y termianndo miles de civilizaciones una y otra y otra vez. Asi que las personas de este planeta trataban de buscar una solucion para predecir el fin de sus eras. pero era imposible. La novela va de cientificos de la tierra tratando de resolver el sistema de ese planeta
>
> Entonces para la experiencia, pensaba hacer era recrear el problema de los tres cuerpos. Donde de manera estandar podemos ver las estrellas orbitando alrededor del planeta. y sus trayectorias tenian ruido de perlin y levy flight donde ocasionalente chocaban con el planeta y la experiencia se volvia a empezar.
>
> Para la interactividad pense en añadir botones o deslizadores que te permitian jugar a ser DIOS. ya que pense en que pudieras modificar el tamaño y velocidad constantemente del planeta y las estrellas. pero aun asi, pese a las modificaciones es inevitable que en algun momento todo se vuelva a chocar
>
> Finalmente mi amiguito juan manuel me convencio de que la segunda idea era mejor. entonces me fui por esa

- ✨ **FASE DE AGARRAME A PUÑOS CON CLAUDE**
>
> Mentiras, no me agarre a puños con claude. pero el codigo es tan largo que me toco usar 3 cuentas para hacer todo el codigo
>
> 1. PRIMER PROMPT
>
> El primer mensaje que le mande en un chat nuevo fue basicamente un recorderis de la novela del problema de los tres cuerpos. y una idea basica de lo que queria. una experiencia viusal donde se muestren las tres estrellas orbitando alrededor del planeta con su respectivo ruido de perlin y el salto de levy.
>
> Me tiro un codigo bastante completo, lindo esteticamente y funcional pero tenia los siguientes problemas: las estrellas nacian desde el centro con el planeta. por lo que la probabilidad de explotar desde el segundo 0 (la verdad vine a entender eso mucho despues. pero si pasaba que todo explotaba desde el segundo 0) y tambien sacaba unos errores
>
> 2. SEGUNDO Y TERCER PROMPT
>
> Para los siguientes prompts le pedi a claude que arreglara los errores que salian y corregir las posiciones de inicio o spawn de las estrellas para evitar los choques inmediatos. Tambien le pedi que regulara la velocidad de las estrellas.
>
> 3. CUARTO Y QUINTO PROMPT
>
> Para este momento descubri que cuando las estrellas se movian tambien podian retrocerderse. lo cual era un poco extraño. Asi que para estos prompts le pedi que condicionara el movimiento de las estrellas a solamente hacia adelante y que regulara el radio de orbita para que las estrellas estuvieran mas pegados al planeta y fuese mas rapido los impactos para que no fuese tan monotono
>
> 4. SEXTO Y SÉPTIMO PROMPT
> 
> Ahora que la experiencia visual base estaba lista, faltaba la parte intercativa. Asi que los ultimos prompts fueron para pedir a claude que añadiera deslizadores que modificaran los tamaños o velocidades de los cuerpos. PERO, modificar las velocidades queria que implicara algo, es decir, que tuviera consecuencias. Asi que pedi que las velocidades al ser modificadas, aumentaran el ruido de perlin y aumentaran las probabilidades de salto de levy, inestabilizando incluso mas el sistema.
>
> Finalizando aqui el proceso de creación de la experiencia.

