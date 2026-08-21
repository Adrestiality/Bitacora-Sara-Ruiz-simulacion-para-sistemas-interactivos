# ☄️UNIDAD 3

## ✨Instrumento funcional y publicado

>
> https://adrestiality.github.io/REPOSITORIO_UNIDAD3_SIMULACION/
>

## ✨ **Mapa del sistema**

**🌿ESTADOS**:

**🔹Morfing entre Geometrías:** 

Cambia de forma (Esfera, Cubo o Reloj de Arena) mediante una interpolación suave de 1.5 segundos entre el punto actual y el objetivo.Las fuerzas físicas siguen activas durante la transición para mantener un movimiento orgánico

**🔹Estado de Pausa e Inercia:** 

Permite congelar la simulación o reiniciar las velocidades y posiciones a su distribución geométrica base.

**🌿FÍSICAS**

**🔹Radial (Atracción/Repulsión):** 

Atrae las partículas hacia el cursor o las repele lejos de él. Es fuerte de cerca, débil de lejos e incluye un suavizado para evitar velocidades infinitas en el centro.

**🔹Vórtice:** 

Aplica un impulso perpendicular a la dirección radial, haciendo que las partículas giren en espiral alrededor del punto central en lugar de ir en línea recta.

**🔹Fricción (Drag):** 

Funciona como la resistencia del aire o agua. Frena las partículas proporcionalmente a su velocidad para evitar que aceleren sin control.

**🔹Viento:** 

Empuja constante y uniformemente a todas las partículas en una dirección específica del espacio 3D.

**🔹Atractor de Lorenz:** 

Guía las partículas a lo largo de un sistema dinámico caótico, creando un patrón de movimiento con la clásica forma de "alas de mariposa".

**🔹Turbulencia (Curl Noise):** 

Genera remolinos y ráfagas suaves mediante un campo de fluido incompresible, evitando que las partículas colapsen o se acumulen.

**🔹Onda de Choque (Pulse):** 

Empuja las partículas hacia afuera mediante una onda esférica que nace en el origen y se expande periódicamente.

**🔹Flujo de Bandada (Boids):** 

Coordina el movimiento colectivo como un cardumen de peces mediante ondas trigonométricas globales, sin requerir cálculos individuales entre partículas.

**🔹Presión por Densidad:** 

Mide la concentración de partículas en una grilla 3D y empuja la materia desde las zonas muy pobladas hacia las áreas más vacías.

**🌿CONTROLES**:

| Tecla / Acción | Efecto Principal en la Simulación |
| :--- | :--- |
| **1** | Morfing a forma de **Esfera 3D** |
| **2** | Morfing a forma de **Cubo** |
| **3** | Morfing a forma de **Reloj de Arena** |
| **P** | Alterna entre modo **LAB** (con GUI y helpers) y **PERFORMANCE** (sin interfaz) |
| **R** | Reinicia la posición y velocidad de todas las partículas (reset()) |
| **- (Menos)** | Activa **Caída Libre** (Wind_y = -9.81) y cambia a la paleta **Verde / Fucsia** |
| **+ (Más)** | Restaura parámetros por defecto y cambia a la paleta **Azul / Amarillo** |
| **Flecha Izquierda / Derecha** | Modifica el viento en el eje X (Wind_x -/+ 0.15) y actualiza la paleta según la dirección |
| **Flecha Arriba / Abajo** | Modifica el viento en el eje Y (Wind_y +/- 0.15) y actualiza la paleta según la dirección |
| **N / M** | Incrementa / decrementa la fuerza del **Atractor de Lorenz** |
| **V / B** | Incrementa / decrementa la turbulencia por **Curl Noise** |
| **X / C** | Incrementa / decrementa la **Onda de Choque (Pulse)** |
| **J / K** | Incrementa / decrementa la **Presión por Densidad Espacial** |
| **U / I** | Incrementa / decrementa el flujo de **Bandada (Boids)** |
| **Click Izquierdo (Mouse)** | Fuerza de **Atracción Radial** instantánea hacia la posición del cursor (Strength = 8.0) |
| **Click Derecho (Mouse)** | Fuerza de **Repulsión Radial** instantánea desde la posición del cursor (Strength = -6.0) |
| **Mover Cursor** | Actualiza la posición del **Atractor / Helper 3D** proyectado sobre el plano Z = 0 mediante Raycasting |

## ✨ **Ficha de fuerzas**

**🔹Fuerza Radial (Atracción / Repulsión):**

Calcula un vector unitario hacia el atractor y escala la magnitud inversamente al cuadrado de la distancia, sumando un término de suavizado (`softening`) en el denominador para evitar divisiones por cero
  
  `F_radial = ((p_attractor - p) / (||p_attractor - p|| + 0.0001)) * (Strength / (||p_attractor - p||^2 + softening^2)) * radialEnabled`

**🔹Vórtice (Rotación Tangencial):**

Aplica el producto cruz entre el vector unitario del eje Z (`vec3(0, 0, 1)`) y la dirección radial, generando una fuerza perpendicular que induce una rotación en espiral
  
  `F_vortex = (z_axis x r_dir) * vortexStrength * vortexEnabled`

**🔹Fricción / Drag (Resistencia Lineal):**

Fuerza de frenado directamente opuesta al vector de velocidad actual y proporcional al coeficiente de arrastre
  
  `F_drag = -1.0 * v * dragCoefficient * dragEnabled`

**🔹Viento:**

Vector tridimensional constante que aplica una aceleración uniforme a todo el sistema
  
  `F_wind = Vector3(wind.x, wind.y, wind.z) * windEnabled`

**🔹Atractor de Lorenz (Sistema Caótico):**

Evalúa el sistema de ecuaciones diferenciales continuas de Lorenz con las constantes `sigma = 10`, `rho = 28` y `beta = 8/3`
  
  `dx/dt = sigma * (y - x)`  
  `dy/dt = x * (rho - z) - y`  
  `dz/dt = x * y - beta * z`  
  `F_lorenz = (v_lorenz - v) * lorenzStrength * lorenzEnabled`

**🔹Curl Noise (Turbulencia Incompresible):**

Calcula el rotacional de un campo escalar de ruido Perlin 3D (`mx_noise_vec3`) mediante aproximación por diferencias finitas. Garantiza divergencia cero (`div(F) = 0`), simulando un fluido incompresible sin puntos de colapso
  
  `F_curl = rotacional(A) = (dAz/dy - dAy/dz, dAx/dz - dAz/dx, dAy/dx - dAx/dy) * curlStrength * curlEnabled`

**🔹Onda de Choque / Pulse Wave:**
  
Onda esférica concéntrica cuyo radio crece linealmente con el tiempo (`r_wave = (time * speed) mod maxRadius. La magnitud sobre las partículas sigue una atenuación con distribución
  
  `F_pulse = dir_pulse * exp(-((dist - r_wave)^2) / width^2) * (pulseStrength / (1.0 + 0.15 * dist)) * pulseEnabled`

**🔹Flujo de Bandada / Boids Flow Field:**
  
Genera un campo de velocidad continuo basado en funciones trigonométricas entrelazadas en los tres ejes sin calcular vecindades
  
  `v_flow = Vector3(sin(y * k + t), cos(z * k + t), sin(x * k + t)) * 2.5`  
  `F_boids = (v_flow - v) * boidsStrength * boidsEnabled`

**🔹Presión por Densidad (Grilla 3D / Spatial Hash):**

Primero acumula la masa de partículas por celda en una grilla.Luego calcula el gradiente negativo de densidad (`-grad(rho)`) mediante diferencias finitas para empujar las partículas hacia las zonas de menor concentración
  
  `grad_x = (rho[x+1,y,z] - rho[x-1,y,z]) / 2`  
  `grad_y = (rho[x,y+1,z] - rho[x,y-1,z]) / 2`  
  `grad_z = (rho[x,y,z+1] - rho[x,y,z-1]) / 2`  
  `F_pressure = -Vector3(grad_x, grad_y, grad_z) * pressureStrength * pressureEnabled`


## ✨ **Registro de pruebas**

La verdad es que este trabajo loe mpece 3 veces. Y las 4 versiones con tematicas muy diferentes. asi que las pruebas adjuntadas tendran cosas de las tres versiones. au que algunas cosas no quedaron en el final

Se que la gracia de esta seccion del registro de pruebas es poner diferentes tests individuales pq el resto de cosas va a ir en la biatcora de la ia pero considere que seria interesante poner aqui todas las veriones de mi sufrimiento y dolor 

**🔹PRUEBA 1**

En el concepto original de todo este proyecto, queria hacer una simulacion de la vida humana pero en particulas. algo asi como lo que quise hacer en la actividad anterior del particle life. Aunque obviamente aqui la idea era hacer un sistema de particulas interactivo a modo de arte visual en tiempo real, tambien queria que las propias particulas tuvieran vida, se crearan que se reproducieran y que murieran. 

Las fisicas que tenia proyectadas para ese momento era que las particulas poduieran crear sociedades agrupandose en diferentes conjuntos, que pudieran crear culturas y religiones que trascendieran de cichas sociedades, creando asi unos vortex, queria que tambien hubieran cosas impredecibles como eventos catastroficos para la sociedad, entonces habia un temblor y tenian que empezar a construir desde 0

he aqui algunas capturas de cuando tenia esas fisicas. aunque visualmente no se entiende mucho

<img width="1086" height="725" alt="Captura de pantalla 2026-08-17 180026" src="https://github.com/user-attachments/assets/ada2f01d-4ee8-4234-b1eb-3c8cd7ab0c49" />
<img width="1265" height="796" alt="Captura de pantalla 2026-08-17 180031" src="https://github.com/user-attachments/assets/6b9327c6-5a7d-4d40-8247-dc372553a3be" />
<img width="1470" height="944" alt="Captura de pantalla 2026-08-17 180045" src="https://github.com/user-attachments/assets/31c017cf-993e-4198-89e1-323f4c3be3bc" />
<img width="1501" height="770" alt="Captura de pantalla 2026-08-17 180054" src="https://github.com/user-attachments/assets/5b02affb-53b6-4672-aa13-4f863bb7ede2" />
<img width="1481" height="734" alt="Captura de pantalla 2026-08-17 180100" src="https://github.com/user-attachments/assets/630fbb55-3940-4d2c-88d9-1c0653759e14" />
<img width="1476" height="836" alt="Captura de pantalla 2026-08-17 180106" src="https://github.com/user-attachments/assets/514b7d1e-16be-440c-9f05-032146a4d5a3" />

En una de estas imagenes tambien se ve una esfera. para ese momento lo que queria era sacar las particulas del cubo y ponerlas en otra figura. 

Aunque funcionaba, la verdad considere que estaba muy simple y cutre. Las particulas por mas que queria no parecian tener vida propia y solo seguian atracciones y desordenes. entonces volvi a empezar (en realidad gemini daño los codigos y decidi tomarlo como una señar divina para volver a empezar)

**🔹PRUEBA 2**

Para este segundo intento de realizar todo este trabajo, decidi reutilizar mucho del concepto anterior y trasnformarlo a la galaxia. Estrellas, sistemas solares, agujeros negros, clusters y poco mas

Como en la prueba anterior descubri que es imposible que se púeda hacer una simulacion individual para cada particula mientras hay una simulacion mas grande corriendo, entonces deje de insistir con hacer qaue las particulas se vieran como con vida propia

Para las fisicas decidi volver a implementar cosas similares para empezar. hacer una figura diferente a la de un cubo, sino una esfera. Queria que todo se viera muy etereo entonces insisti mucho en la formacion de nebulosas. 

queria cosas asi:

<img width="427" height="468" alt="image" src="https://github.com/user-attachments/assets/7606888a-e576-4404-96db-da37bcc9832d" />

Queria que los clicks del mouse me permitieran atraer y disipar constantemente, ademas de las clasicas atracciones y comportamientos que ya llevaba desde la idea anterior

<img width="1462" height="598" alt="Captura de pantalla 2026-08-18 151834" src="https://github.com/user-attachments/assets/e8249d44-6300-4ccf-b89b-8843d2a6b8a3" />
<img width="1495" height="734" alt="Captura de pantalla 2026-08-18 153416" src="https://github.com/user-attachments/assets/6a04c1b8-bf82-46eb-ba3a-50595fedebf5" />
<img width="1514" height="674" alt="Captura de pantalla 2026-08-18 153420" src="https://github.com/user-attachments/assets/c8b6f8de-b3f8-4c38-8045-6258a3ca534c" />
<img width="1022" height="872" alt="Captura de pantalla 2026-08-18 154349" src="https://github.com/user-attachments/assets/bb7abcee-10ad-4a79-bbc0-9b3df8af1f2e" />
<img width="1179" height="864" alt="Captura de pantalla 2026-08-18 155143" src="https://github.com/user-attachments/assets/2bc3edd4-2abe-4a5b-83e2-4318201ac544" />
<img width="859" height="751" alt="Captura de pantalla 2026-08-18 155155" src="https://github.com/user-attachments/assets/701f7d2c-37fb-46d8-a38c-caa13c0440b4" />

La primera imagen que tiene colores rojos me dio mucha motivacion. de verdad parecia un agujero negro. pero a medida que daba mas prompts para que la fisica de las particulas pareciera mas natural y hasta liquida, estaba pasando algo muy maluco y era que las particulas muy rapidamente encontraban un estado estable. entonces me molestaba un monton porque si iba a hacer la coreografia en frente de los demas y me demoraba 0.1 segundos ya se estancaban en los bordes y era deprimente....

entonces, volvi a empezar :)

de igual modo tratando de arreglar eso fue que gemini lo volvio a dañar entonceeeeeeeeeeeeeeees fue otra señal divina

**🔹PRUEBA 3**

Lamentablemente para esta prueba de aqui no tome ninguna captura. y aqui ya tambien deje de ponerle fe en una tematica o significado.

pero para este punto ya estaba un poco harta de saber que si iba a funcionar y que no. entonces empece desde las cosas mas absurdas hasta los mas ccomplejo que era la integracion de nuevas fisicas

vi que varios de mis compañeros cambiaban con mucha facilidad la forma de las figuras durante sus presentaciones. tambien queria eso. asi que empece a pedirle que las particulas tuvieran estados difernetes. una esfera, un cubo y un reloj de arena. y funciono, pero de manera diferente... 

Lo que queria cambiar era el limite. todas las particulas por mas que se crearan o se destruyeran estaban contenidas en un cubo o una esfera. queria cambiar especificamente ese contenedor. pero lo que hizo el codigo fue que agrupaba y reseteaba las posiciones en forma de cubo, de esfera y de reloj de arena... no estaba mal ajajja, por eso lo deje

Luego empece con los clicks del mouse. igual que antes, queria que uno atrejaera y otro expulsara. 

De ahi si empece con algunas fisicas. algunos de mis amigos hacian que sus particulas se vieran como agua. me parecia hermoso. trate de implementarlo tambien pero no se veian tan liquidos como la version anterior pero no me molestaba aun.

Eventualmente los presets originales dejaron de funcionar por algun motivo, y cuando le pedi cambiar los colores se destruyo todo ???? 

entonces decidi quedarme con los archivos que solo modificaban las particulas con las figuras y lo de los clicks y volver a empezaaaaaaaaaaar

**🔹PRUEBA 4 **

Aqui, insisto. deje de preocuparme por hacer un diseño con significado. ya solo queria una amalgama de interacciones que se viera eterea y ya

Reutilizando el codigo que aun medio servia en la version anterior, decidi ya solo que la ia solita hiciera lo que quisiera. Me olvide de modificar las particulas individualemente hablando, olvide de cambiarles el color y de crear figuras especificas con la experiencia (a excepcion de los presets de esfera, cubo, reloj de arena)

Aqui le pregunte a gemini que me diera un listado de fisicas que podria añadir ademas de lo que ya habia. he de ahi el por que todas las fisicas tienen ecuaciones matematicas. pq la ia las genero. ya estaba cansada de tratar fisicas y que siempre se dañaran los codigos

eventualmente logre algunas fisicas de manera propia, como aplicar graverdad y que la forma en la que se repelaban las partidulas con el mouse se vieran un poco mejor

<img width="958" height="750" alt="Captura de pantalla 2026-08-19 055743" src="https://github.com/user-attachments/assets/5de9ca1f-3023-4bba-92d7-31506fe67441" />
<img width="1220" height="788" alt="Captura de pantalla 2026-08-19 191104" src="https://github.com/user-attachments/assets/f06f4887-8c85-4c7b-9d2d-5737401d97ff" />
<img width="556" height="474" alt="Captura de pantalla 2026-08-19 191117" src="https://github.com/user-attachments/assets/9340a2bd-bb36-4285-8179-4188b4d79b49" />
<img width="901" height="459" alt="Captura de pantalla 2026-08-19 191122" src="https://github.com/user-attachments/assets/93e05b59-7a08-470c-b89d-7148a0afa729" />
<img width="1132" height="711" alt="Captura de pantalla 2026-08-19 191125" src="https://github.com/user-attachments/assets/e347f389-67cc-4dc8-8404-7892f97c62ed" />
<img width="655" height="604" alt="Captura de pantalla 2026-08-19 191131" src="https://github.com/user-attachments/assets/5e5b48dc-d37a-408a-9a5f-20073090a323" />
<img width="366" height="448" alt="Captura de pantalla 2026-08-19 191156" src="https://github.com/user-attachments/assets/f597835f-36c0-42c1-bb04-029e011b7887" />
<img width="929" height="882" alt="Captura de pantalla 2026-08-19 193326" src="https://github.com/user-attachments/assets/a80ddeb1-e51f-43a2-af02-91ff42c86e4d" />

## ✨ **Score visual**

Desde que empece el trabajo queria lograr un efecto muy etereo y liquido con las partidulas. reconozco que me encantan los efectos como corrientes, telarañas... todo lo que sean lineas que pareciera que conectan las personas, aunque lamentablemente no pude lograr este objetivo debido a que perdia demasiado tiempo peleando con la ia y que tambien con mucha facilidad la ia dañaba los codigos y parecia no poder arreglarlos. 

Asi que cambie mi objetivo a querer que al menos los efectos que causara se parecieran a ese trend de cuando te daban un baño de mirella o escarcha y que hubiese MUCHO REBOTE para que las fisicas se vieran mas como sifueran miles de pelotas rebotando 

dado quje ninguna de mis ideas conceptuales fue usada al final, usare este espacio para darle un significado al sistema que quedo en una ultima estancia.... me gusta ver este trabajo finalmente como los sentimientos. 

sabes que son las imagenes? las imagenes son las representaciones visuales de las palabras que usamos a diario. por ejemplo cuando digo proyecto pienso en hombres armando una maqueta.... pero si te digo la palabra sentimientos, que imagen viene a tu cabeza?? la verdad es que yo me imaguno siluetas, amalgamas o nubes de diferentes densidades y colores que tienen comportamientos espontaneos e impredecibles

cuando se mueven de manera alocada y rebotan es porque son intensas. si se empiezan a disipar es porque ya son muy endebles y cuando tienen la gravedad activa es porque se vuelven monotonas. 

ya ya. y la cancion a que va? la propuesta de diseño es para la cancion no para el significado que yo quisiera hacer

## ✨ **Bitácora de IA**

>
>uwu
>

- ✨ **Autoevaluación ponderada**

>
>uwu
>
