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
<a name="evidencia5"></a>
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
> 2: Mi segunda opcion esta inspirada en la novela del problema de los tres cuerpos. En resumen, existe un planeta lejano que esta orbitado por 3 estrellas inestables que irremediablemente acaban chocando con el planeta y termianndo miles de civilizaciones una y otra y otra vez. Asi que las personas de este planeta trataban de buscar una solucion para predecir el fin de sus eras. pero era imposible. La novela va de cientificos de la tierra tratando de resolver el sistema de ese planeta
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
> 5. OCTAVO Y NOVENO PROMPT
> 
> Finalmente, solo me faltaba realizar ajustes como organizar las cosas de la proporcion en pantalla y detalles de particulas. nada muy extravagante hasta que por algun motivo claude dejo de entregarme codigos funionales. asi que si. a la final si me agarre a puños con claude
> 
> Pero despues de esto, la experiencia quedo lista.
>
> Ahora veamos una explicacion fancy del trabaajo dada por claude.

- ✨ **DESCRIPCIÓN DE LA EXPERIENCIA**
<a name="evidencia3"></a>
> La pieza traduce *El problema de los tres cuerpos* a la entrada de un festival de ciencia y creatividad: un planeta orbita en el centro de un sistema de tres estrellas cuyo movimiento es fundamentalmente impredecible. El visitante puede intervenir —ajustando tamaños y velocidades— pero nunca controlar del todo: cada ajuste altera las reglas de las *otras* dos estrellas, no solo la que toca. Cada movimiento sigue una regla matemática precisa, pero la combinación nunca es predecible: la incertidumbre no es ausencia de reglas.
>
<a name="evidencia2"></a>
> **Conceptos combinados**
>
>- **Ruido de Perlin**: deriva angular y radial de cada estrella — caos suave que construye tendencia.
>- **Vuelo de Lévy** (Mantegna): saltos súbitos e improbables que rompen el patrón.
>- **Distribución normal**: una nube de "polvo" gaussiano por estrella, cuya dispersión es amplia justo tras un reinicio y se estrecha con el tiempo.
>
<a name="evidencia1"></a>
>**Los cinco momentos, traducidos en comportamiento**
>
> **Posibilidad**: Tras un colapso, la nube gaussiana es amplia: casi cualquier posición cercana es plausible.
> 
> **Tendencia**: El ruido de Perlin acumula una deriva correlacionada que construye una dirección reconocible.
> 
> **Normalidad**:  La nube se contrae con el tiempo: la mayoría de las posiciones quedan cerca de lo habitual.
> 
> **Excepción**: El salto de Lévy saca a una estrella de su territorio y descubre una configuración nueva.
> 
> **Influencia**:  Los deslizadores no controlan directamente ninguna estrella: alteran las probabilidades de las otras dos (perturbación cruzada).
> 
- ✨ **CÓDIGO**
<a name="evidencia4"></a>
```JavaScript
// ---------------------------------------------------------
// EL PROBLEMA DE LOS TRES CUERPOS
// Actividad 07 — Reto de diseño: Navegar la incertidumbre
//
// Lienzo fijo 1080x1920 (formato vertical tipo TikTok, 9:16).
// Se ajusta a cualquier pantalla vía CSS (letterbox), pero
// internamente siempre se dibuja sobre 1080x1920 exactos.
// ---------------------------------------------------------

const CANVAS_W = 1080;
const CANVAS_H = 1920;
let dispW, dispH, dispX, dispY; // caja de despliegue (letterbox) en la ventana real

let stars = [];
let planet;
let collapsed = false;
let collapseTimer = 0;
let stats = { colapsos: 0, tiempoVivo: 0 };
let shakeAmt = 0;
let systemStartFrame = 0;
let dustParticles = [];

const STAR_COLORS = ['#f38ba8', '#f9e2af', '#89b4fa'];
const STAR_NAMES = ['roja', 'amarilla', 'azul'];

// --- parámetros de saltos de Lévy ---
const JUMP_PROB_BASE = 0.0018;
const JUMP_PROB_TENSION = 0.012;
const JUMP_MAG_MAX = 170;
const JUMP_DECAY_FRAMES = 30;
const JUMP_COOLDOWN_FRAMES = 55;

// --- parámetros de órbita (re-escalados para 1080x1920) ---
const SPAWN_RADIUS = 220;
const BASE_ANGULAR_SPEED = 0.018;
const ANGULAR_SPEED_VARIATION = 0.016;
const LERP_SPEED = 0.16;
const INHERENT_SPEED_SPREAD = 0.55;

// --- parámetros de tamaño (re-escalados) ---
const PLANET_SIZE_DEFAULT = 44;
const STAR_SIZE_DEFAULT = 38;
const COLLISION_MARGIN = 14;

// --- perturbación cruzada (influencia del visitante) ---
const DISTURBANCE_JUMP_FACTOR = 0.01;
const DISTURBANCE_NOISE_FACTOR = 0.02;

// --- física del planeta (anclado, ya no queda capturado en órbita) ---
const CENTROID_PULL = 0.0015;
const ANCHOR_PULL = 0.006;
const PLANET_DAMPING = 0.88;

// --- polvo de distribución normal (posibilidad → tendencia → normalidad) ---
const DUST_PER_STAR = 2;
const DUST_SIGMA_START = 110;
const DUST_SIGMA_END = 17;
const DUST_SETTLE_FRAMES = 220;
const DUST_LIFE = 46;

// --- UI ---
let uiPanel;
let planetSizeSlider;
let starSizeSliders = [];
let starSpeedSliders = [];

function setup() {
  let cnv = createCanvas(CANVAS_W, CANVAS_H);
  cnv.id('sketch-canvas');
  colorMode(RGB);
  injectGlobalStyle();
  fitCanvasToWindow();
  createUI();
  initSystem();
}

function injectGlobalStyle() {
  let style = createElement('style', `
    html, body { margin: 0; padding: 0; overflow: hidden; background: #000; }
    #ui-panel { font-family: monospace; color: #cdd6f4; }
    #ui-panel input[type=range] { height: 14px; margin: 3px 0; accent-color: #89b4fa; width: 100%; }
    #ui-panel div { font-size: 20px; }
  `);
  style.parent(document.head);
}

function fitCanvasToWindow() {
  let winAspect = windowWidth / windowHeight;
  let targetAspect = CANVAS_W / CANVAS_H; // 0.5625 = 9:16
  if (winAspect > targetAspect) {
    dispH = windowHeight;
    dispW = dispH * targetAspect;
  } else {
    dispW = windowWidth;
    dispH = dispW / targetAspect;
  }
  dispX = (windowWidth - dispW) / 2;
  dispY = (windowHeight - dispH) / 2;

  let cnv = select('#sketch-canvas');
  cnv.style('position', 'fixed');
  cnv.style('left', dispX + 'px');
  cnv.style('top', dispY + 'px');
  cnv.style('width', dispW + 'px');
  cnv.style('height', dispH + 'px');
}

function createUI() {
  uiPanel = createDiv('');
  uiPanel.id('ui-panel');
  uiPanel.style('position', 'fixed');
  uiPanel.style('background', 'rgba(17,17,27,0.85)');
  uiPanel.style('padding', '16px 20px');
  uiPanel.style('border-radius', '14px');
  uiPanel.style('z-index', '10');
  uiPanel.style('line-height', '1.15');

  createDiv('🪐 planeta').parent(uiPanel).style('margin-top', '0');
  planetSizeSlider = createSlider(20, 95, PLANET_SIZE_DEFAULT, 1);
  planetSizeSlider.parent(uiPanel);

  for (let i = 0; i < 3; i++) {
    let labelColor = STAR_COLORS[i];
    let sizeLabel = createDiv(`⭐ ${STAR_NAMES[i]} tam.`);
    sizeLabel.parent(uiPanel);
    sizeLabel.style('margin-top', '10px');
    sizeLabel.style('color', labelColor);
    let sSize = createSlider(15, 70, STAR_SIZE_DEFAULT, 1);
    sSize.parent(uiPanel);
    starSizeSliders.push(sSize);

    let speedLabel = createDiv(`⭐ ${STAR_NAMES[i]} vel.`);
    speedLabel.parent(uiPanel);
    speedLabel.style('margin-top', '5px');
    speedLabel.style('color', labelColor);
    let sSpeed = createSlider(0.2, 3, 1, 0.05);
    sSpeed.parent(uiPanel);
    starSpeedSliders.push(sSpeed);
  }

  positionSliderPanel();
}

// Ancla el panel a la esquina superior derecha del lienzo mostrado,
// escalándolo (sin moverse) para que se vea proporcional en
// cualquier tamaño de pantalla.
function positionSliderPanel() {
  if (!uiPanel) return;
  let k = dispW / CANVAS_W;
  let baseW = 300; // ancho de diseño, en el espacio de referencia 1080
  let marginRight = 28;
  let marginTop = 28;
  let anchorRightX = dispX + dispW - marginRight;
  let anchorTopY = dispY + marginTop;

  uiPanel.style('width', baseW + 'px');
  uiPanel.style('left', (anchorRightX - baseW) + 'px');
  uiPanel.style('top', anchorTopY + 'px');
  uiPanel.style('transform', `scale(${k})`);
  uiPanel.style('transform-origin', 'top right');
}

function initSystem() {
  stars = [];
  for (let i = 0; i < 3; i++) {
    let startAngle = (TWO_PI / 3) * i;
    stars.push({
      noffR: random(1000),
      noffA: random(1000),
      angle: startAngle,
      radius: random(170, 260),
      pos: createVector(cos(startAngle) * SPAWN_RADIUS, sin(startAngle) * SPAWN_RADIUS),
      color: STAR_COLORS[i],
      trail: [],
      jump: createVector(0, 0),
      jumpDecay: 0,
      jumpCooldown: 0,
      inherentSpeedFactor: random(1 - INHERENT_SPEED_SPREAD, 1 + INHERENT_SPEED_SPREAD)
    });
  }
  planet = {
    pos: createVector(0, 0),
    vel: createVector(0, 0),
    trail: []
  };
  collapsed = false;
  collapseTimer = 0;
  systemStartFrame = frameCount;
  dustParticles = [];
}

// Genera un paso con distribución de Lévy (cola pesada) usando
// el algoritmo de Mantegna para vuelos alfa-estables.
function levyStep(alpha = 1.5) {
  let sigma = pow(
    (gammaApprox(1 + alpha) * sin(PI * alpha / 2)) /
    (gammaApprox((1 + alpha) / 2) * alpha * pow(2, (alpha - 1) / 2)),
    1 / alpha
  );
  let u = randomGaussian(0, sigma);
  let v = randomGaussian(0, 1);
  return u / pow(abs(v), 1 / alpha);
}

function gammaApprox(x) {
  return sqrt(2 * PI / x) * pow((x / Math.E) * sqrt(x * sinh(1 / x) + 1 / (810 * pow(x, 6))), x);
}
function sinh(x) { return (Math.exp(x) - Math.exp(-x)) / 2; }

function draw() {
  let planetSize = planetSizeSlider.value();
  let starSizes = starSizeSliders.map(s => s.value());
  let starSpeeds = starSpeedSliders.map(s => s.value());

  let deviations = starSpeeds.map(v => abs(v - 1));
  let disturbance = [0, 0, 0];
  for (let j = 0; j < 3; j++) {
    let sum = 0;
    for (let i = 0; i < 3; i++) if (i !== j) sum += deviations[i];
    disturbance[j] = sum;
  }

  push();
  translate(width / 2, height / 2);
  if (shakeAmt > 0) {
    translate(random(-shakeAmt, shakeAmt), random(-shakeAmt, shakeAmt));
    shakeAmt *= 0.9;
  }

  background(5, 6, 10, 40);

  if (collapsed) {
    drawCollapse();
    pop();
    return;
  }

  stats.tiempoVivo++;

  let minDist = Infinity;
  for (let i = 0; i < stars.length; i++) {
    minDist = min(minDist, p5.Vector.dist(stars[i].pos, planet.pos));
    for (let j = i + 1; j < stars.length; j++) {
      minDist = min(minDist, p5.Vector.dist(stars[i].pos, stars[j].pos));
    }
  }
  let tension = constrain(map(minDist, 0, 600, 1, 0), 0, 1);
  let t = frameCount * 0.006;

  // dispersión de la nube gaussiana: amplia al reiniciar (posibilidad),
  // se estrecha con el tiempo (tendencia → normalidad)
  let age = frameCount - systemStartFrame;
  let dustSigma = lerp(DUST_SIGMA_START, DUST_SIGMA_END, constrain(age / DUST_SETTLE_FRAMES, 0, 1));

  for (let idx = 0; idx < stars.length; idx++) {
    let s = stars[idx];
    let extraNoiseSpeed = disturbance[idx] * DISTURBANCE_NOISE_FACTOR;
    let jumpProb = JUMP_PROB_BASE + tension * JUMP_PROB_TENSION + disturbance[idx] * DISTURBANCE_JUMP_FACTOR;

    let rNoise = map(noise(s.noffR + t), 0, 1, -95, 95);
    let speedNoise = map(noise(s.noffA + t), 0, 1, 0, ANGULAR_SPEED_VARIATION + extraNoiseSpeed);
    let ownSpeedMult = starSpeeds[idx] * s.inherentSpeedFactor;
    s.angle += (BASE_ANGULAR_SPEED + speedNoise) * ownSpeedMult;
    let rad = s.radius + rNoise;
    let target = createVector(cos(s.angle) * rad, sin(s.angle) * rad);

    if (s.jumpCooldown > 0) s.jumpCooldown--;

    if (random() < jumpProb && s.jumpDecay <= 0 && s.jumpCooldown <= 0) {
      let dir = random(TWO_PI);
      let mag = constrain(abs(levyStep(1.4)) * 28, 0, JUMP_MAG_MAX);
      s.jump = createVector(cos(dir) * mag, sin(dir) * mag);
      s.jumpDecay = JUMP_DECAY_FRAMES;
    }
    if (s.jumpDecay > 0) {
      target.add(p5.Vector.mult(s.jump, s.jumpDecay / JUMP_DECAY_FRAMES));
      s.jumpDecay--;
      if (s.jumpDecay <= 0) s.jumpCooldown = JUMP_COOLDOWN_FRAMES;
    }

    s.pos.lerp(target, LERP_SPEED);
    s.trail.push(s.pos.copy());
    if (s.trail.length > 70) s.trail.shift();

    for (let d = 0; d < DUST_PER_STAR; d++) {
      dustParticles.push({
        pos: createVector(
          s.pos.x + randomGaussian(0, dustSigma),
          s.pos.y + randomGaussian(0, dustSigma)
        ),
        life: DUST_LIFE,
        color: s.color
      });
    }
  }

  let centroid = createVector(0, 0);
  for (let s of stars) centroid.add(s.pos);
  centroid.mult(1 / stars.length);

  let toCentroid = p5.Vector.sub(centroid, planet.pos).mult(CENTROID_PULL);
  let toOrigin = p5.Vector.sub(createVector(0, 0), planet.pos).mult(ANCHOR_PULL);
  planet.vel.add(toCentroid).add(toOrigin);
  planet.vel.mult(PLANET_DAMPING);
  planet.pos.add(planet.vel);

  planet.trail.push(planet.pos.copy());
  if (planet.trail.length > 50) planet.trail.shift();

  for (let idx = 0; idx < stars.length; idx++) {
    let s = stars[idx];
    let collisionDist = planetSize / 2 + starSizes[idx] / 2 + COLLISION_MARGIN;
    if (p5.Vector.dist(s.pos, planet.pos) < collisionDist) {
      collapsed = true;
      collapseTimer = 0;
      stats.colapsos++;
      shakeAmt = 55;
    }
  }

  updateAndDrawDust();
  drawTrails();
  drawStars(starSizes);
  drawPlanet(planetSize);
  pop();

  drawUI(tension, minDist, disturbance);
}

function updateAndDrawDust() {
  noStroke();
  for (let i = dustParticles.length - 1; i >= 0; i--) {
    let p = dustParticles[i];
    p.life--;
    if (p.life <= 0) {
      dustParticles.splice(i, 1);
      continue;
    }
    let a = map(p.life, 0, DUST_LIFE, 0, 60);
    fill(colorAlpha(p.color, a));
    circle(p.pos.x, p.pos.y, 5);
  }
  if (dustParticles.length > 700) dustParticles.splice(0, dustParticles.length - 700);
}

function drawTrails() {
  noFill();
  for (let s of stars) {
    for (let i = 0; i < s.trail.length; i++) {
      let a = map(i, 0, s.trail.length, 0, 120);
      stroke(colorAlpha(s.color, a));
      strokeWeight(4);
      point(s.trail[i].x, s.trail[i].y);
    }
  }
  for (let i = 0; i < planet.trail.length; i++) {
    let a = map(i, 0, planet.trail.length, 0, 150);
    stroke(255, 255, 255, a);
    strokeWeight(5);
    point(planet.trail[i].x, planet.trail[i].y);
  }
}

function colorAlpha(hex, a) {
  let c = color(hex);
  return color(red(c), green(c), blue(c), a);
}

function drawStars(starSizes) {
  for (let idx = 0; idx < stars.length; idx++) {
    let s = stars[idx];
    let sz = starSizes[idx];
    noStroke();
    let c = color(s.color);
    for (let r = sz * 2.1; r > 0; r -= 12) {
      fill(red(c), green(c), blue(c), 10);
      circle(s.pos.x, s.pos.y, r * 2);
    }
    fill(c);
    circle(s.pos.x, s.pos.y, sz);
  }
}

function drawPlanet(planetSize) {
  noStroke();
  fill(255, 255, 255, 25);
  circle(planet.pos.x, planet.pos.y, planetSize * 2.2);
  fill(230, 235, 255);
  circle(planet.pos.x, planet.pos.y, planetSize);
}

function drawCollapse() {
  collapseTimer++;
  fill(255, random(80, 180), 80, 200 - collapseTimer * 3);
  noStroke();
  circle(0, 0, collapseTimer * 19);

  if (collapseTimer > 1 && collapseTimer < 40) {
    for (let i = 0; i < 3; i++) {
      let ang = random(TWO_PI);
      let d = collapseTimer * random(7, 21);
      fill(255, 200, 150, 180);
      circle(cos(ang) * d, sin(ang) * d, random(7, 16));
    }
  }

  push();
  resetMatrix();
  fill('#f38ba8');
  textAlign(CENTER, CENTER);
  textSize(42);
  text('el sistema colapsó — el planeta fue destruido', width / 2, height / 2 + 190);
  textSize(28);
  fill('#a6adc8');
  text('era inevitable, pero nunca fue predecible cuándo', width / 2, height / 2 + 250);
  pop();

  if (collapseTimer > 90) initSystem();
}

function drawUI(tension, minDist, disturbance) {
  push();
  resetMatrix();
  noStroke();
  textSize(24);
  textAlign(LEFT, TOP);
  let x = 28;
  let y = 28;
  let lh = 34;
  let lines = [
    ['el problema de los tres cuerpos', '#cdd6f4'],
    [`tensión del sistema: ${(tension * 100).toFixed(1)}%`, tension > 0.5 ? '#f38ba8' : '#a6e3a1'],
    [`distancia mínima: ${minDist.toFixed(0)}px`, '#a6adc8'],
    [`colapsos totales: ${stats.colapsos}`, '#a6adc8'],
    [`frames desde el último colapso: ${stats.tiempoVivo}`, '#a6adc8'],
    [`perturbación roja: ${disturbance[0].toFixed(2)}`, '#f38ba8'],
    [`perturbación amarilla: ${disturbance[1].toFixed(2)}`, '#f9e2af'],
    [`perturbación azul: ${disturbance[2].toFixed(2)}`, '#89b4fa']
  ];
  for (let i = 0; i < lines.length; i++) {
    fill(lines[i][1]);
    text(lines[i][0], x, y + i * lh);
  }
  pop();
}

function windowResized() {
  fitCanvasToWindow();
  positionSliderPanel();
}
```
ENLACE: https://editor.p5js.org/Adrestiality/full/3xtbVnZ6R
ENLACE + EDITOR: https://editor.p5js.org/Adrestiality/sketches/3xtbVnZ6R

- ✨ **FOTOOOS**
<img width="490" height="592" alt="image" src="https://github.com/user-attachments/assets/9e7efb46-99d7-450b-9ea7-d780dd11148e" />
<img width="501" height="551" alt="image" src="https://github.com/user-attachments/assets/7ef64508-8b68-4cce-9f03-7a54fa4bd4a8" />
<img width="660" height="712" alt="image" src="https://github.com/user-attachments/assets/96ba7f8b-60bf-4c67-a47a-8988815760ce" />

## 🌟 ACTIVIDAD 8: AUTOEVALUACIÓN

>**Encargo completo:** interpreto los cinco momentos dentro de un mismo sistema visual.
> 
> CUMPLE
>
> [evidencia 1](#evidencia1)
>
>**Simulación con intención:** utilizo al menos tres conceptos de la unidad para comunicar las ideas del encargo.
>
>	CUMPLE
>
>[evidencia  2](#evidencia2)
>
>**Interacción significativa:** la interacción modifica el comportamiento o las probabilidades del sistema, que también funciona sin intervención.
>
> CUMPLE
>
>[evidencia 3](#evidencia3)
>
>**Prototipo funcional:** la experiencia puede ejecutarse y recorrerse completa sin errores que impidan comprenderla.
>
> CUMPLE
>
>[evidencia 4](#evidencia4)
>
>**Proceso documentado:** la bitácora evidencia avances, decisiones, dificultades, soluciones, uso de IA y enlace al prototipo.
>
> CUMPLE
>
>[evidencia 5](#evidencia5)
>
