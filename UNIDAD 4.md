# UNIDAD 4

- **Repositorio de la Actividad:** [REPOSITORIO_UNIDAD4_SIMULACION](https://github.com/Adrestiality/REPOSITORIO_UNIDAD4_SIMULACION)
- **Despliegue de la Actividad:** [Ver Actividad Interactiva](https://adrestiality.github.io/REPOSITORIO_UNIDAD4_SIMULACION/)

## 1. Generación de Ideas y Propuesta

Para el proceso de esta actividad me costó mucho pensar en una propuesta. La temática de sonido me parecía muy entretenida y con muchas posibilidades, pero admito que me costó bastante dar con una idea. 

Eventualmente me inspiré en el trabajo de uno de mis compañeros, que consistía en una cuadrícula en 3D. De ahí tomé la base de la cuadrícula 3D y me acordé de un juego que se llama *Monument Valley*, que es de perspectivas, muy geométrico pero muy minimalista. Pensé: *"¿y qué tal si usamos ambas cosas?"*. Sumándole a eso mis conocimientos de 3D, donde el modelado consiste mucho en extruir caras y polígonos, decidí mezclar todo esto.

### La propuesta
La idea es empezar con un plano. De ese plano puedes extruir pilares para ir construyendo una torre, y puedes extruir diferentes tipos de pilares, ya sean verticales u horizontales. 

Mezclándolo con las necesidades de este reto de diseño:
* Cada pilar es un agente diferente dependiendo de su longitud y su posición.
* Cada uno tiene ritmos y tiempos diferentes dentro de la ecuación del muro.
* La idea es que a medida que añades pilares, estos terminen sincronizándose en una melodía.

### El bichito (el antagonista)
Luego de analizarlo varias veces e incluso hablarlo con el docente, llegamos a la idea de que se estaba formando un jueguito donde tú creas tu propia torre. Sin embargo, sentía que le faltaba una motivación para seguir jugando. 

Por eso añadí un agente más: un **bichito** (que en realidad es como una bolita llena de ojitos). Es como el problema o el antagonista, pero no porque sea malo, sino porque es algo con lo que tienes que aprender a lidiar:
* El bichito también es un agente y una parte decisiva de la mezcla. Empieza a escalar los pilares a medida que los vas creando.
* Si pasa mucho tiempo en un pilar o en un conjunto de pilares (más de 6 segundos quieto/estable), los destruye. Su capacidad es destruir cuando la cosa se vuelve monótona.
* Cuando destruye la estructura, cae al piso y le toca a uno volver a escalar y construir.



## 2. Proceso de Creación

### Repositorio y Servidor
Decidí reutilizar el repositorio de la unidad anterior para tener la página web lista. El servidor funcionaba muy bien, así que valía la pena aprovecharlo.

### Proceso con la IA
Como suelo tener bastantes conflictos con varias IAs (Gemini, ChatGPT, Claude, etc.), decidí hacer lo siguiente por recomendación de los demás:
1. Le expliqué detalladamente mi idea a ChatGPT y le dije que me hiciera **todas las preguntas que quisiera** para que entendiera bien lo que quería lograr.
2. Abrí Blender, hice unos modelos 3D rápidos y se los pasé a ChatGPT para que tuviera súper claro el concepto visual.
3. Le pedí a ChatGPT que me armara **6 prompts progresivos** para pasárselos a AntiGravity y que hiciera el código paso a paso con base en lo que discutimos.

<img width="1280" height="1600" alt="1" src="https://github.com/user-attachments/assets/62ebf901-a5cf-4c00-9491-9e0025c1c4e9" />
<img width="1280" height="1600" alt="2" src="https://github.com/user-attachments/assets/3ad5f8b6-8abb-47fc-b83e-039898106a7c" />
<img width="1280" height="1600" alt="3" src="https://github.com/user-attachments/assets/7a3d7f08-38e4-4113-bd0c-6999755b8ac9" />
<img width="1280" height="1600" alt="4" src="https://github.com/user-attachments/assets/19b50a08-d2f3-4ef2-8c9c-755e1492f190" />
<img width="1280" height="1600" alt="5" src="https://github.com/user-attachments/assets/664c6925-f484-432d-9343-0bff8a24af5f" />
<img width="1280" height="1600" alt="6" src="https://github.com/user-attachments/assets/f1ef11ef-c446-494a-9764-c2bb798dbbfe" />
<img width="1280" height="1600" alt="7" src="https://github.com/user-attachments/assets/d9cfb227-cc60-4461-b18d-62f6c9a0b794" />
<img width="1280" height="1600" alt="8" src="https://github.com/user-attachments/assets/720043b4-1b5d-4dfa-83c6-18f8999fc84f" />
<img width="1280" height="1600" alt="8" src="https://github.com/user-attachments/assets/14d8d6c0-5893-4bcf-a599-2eba10c5fb88" />


### Ajustes y pulido
Obviamente, después de pasar los prompts a AntiGravity quedaron cosas por pulir y me tocó hacer varios prompts adicionales:
* El bichito no salió negro como quería, sino lila.
* Las proporciones no se calculaban bien y por algún motivo los cubos se cruzaban al ponerlos.
* A veces el bichito explotaba y se salía de la cuadrícula.
* El bichito no sonaba (y se suponía que era un agente de sonido).
* Los sonidos de la torre eran bonitos pero muy lentos, entonces le faltaba dinamismo y ritmo.
* Los pilares eran bastante difíciles de poner al inicio.

<img width="327" height="432" alt="Captura de pantalla 2026-09-06 214724" src="https://github.com/user-attachments/assets/fa1c9288-a5ba-4a8a-8523-19d14f3b853e" />
<img width="562" height="443" alt="Captura de pantalla 2026-09-07 234545" src="https://github.com/user-attachments/assets/ff0be1ba-894d-4f5b-a36e-8d2809b7489e" />
<img width="567" height="742" alt="Captura de pantalla 2026-09-07 234550" src="https://github.com/user-attachments/assets/398ee253-52f1-456b-a6a0-097ed72d27d1" />


## 3. ¿Cómo funciona el juego?

La actividad interactiva consiste en crear pilares para que el bichito los recorra y suba, haciendo que todos los pilares resuenen en conjunto sin que se destruya la torre. Si el bichito se queda más de 6 segundos quieto, destruye la torre, cae al suelo y toca empezar de nuevo.

### Los Pilares
Tú no puedes elegir exactamente qué pilar poner; te salen de manera aleatoria (como si fueran cartas):
* **Verticales (4 tipos):** de 4, 3, 2 y 1 casilla.
* **Horizontales (3 tipos):** de 3, 2 y 1 casilla.
* Cada tipo se diferencia por un **color diferente**.



## 4. Controles e Interfaz

* **Cambio de Eje:** Para los pilares horizontales, puedes cambiar su eje con una tecla especial al momento de insertarlos.
* **Saltar Pieza:** Si no quieres usar el pilar que te salió, puedes saltar a la siguiente pieza, pero no puedes elegir cuál te va a salir.
* **Control de Acoplamiento (Fuerza):** Te permite regular qué tan fuerte se acoplan los osciladores.
* **Estadísticas en Pantalla:** Muestra datos en tiempo real de **coherencia**, **sincronización** y **oscilaciones**. También te avisa si la organización es estable (o te das cuenta tú mismo por el sonido si las cosas empiezan a salir mal).
* **Métricas:** Muestra qué tan alta es la torre y la cantidad de pilares que has puesto.
* **Cámara e Isometría:** Hay un menú para cambiar la perspectiva isométrica de la torre. Esto es clave porque, al igual que en *Monument Valley*, al cambiar la perspectiva haces que el bichito pueda pasar de un pilar a otro que visualmente se conectan aunque en el espacio 3D no lo estén.
* **Control de Osciladores:**
  * Hay un menú de osciladores para controlar la oscilación del bichito y de cada pilar según su número.
  * **Selección Directa:** Si seleccionas un pilar en específico dándole clic en la escena 3D, puedes manipular su oscilación directamente arrastrando el control, sin tener que buscarlo en el menú.
  * **Molestar Pilares:** Hay un botón para desestabilizar o "molestar" a todos los pilares juntos a la vez y ver cómo reaccionan.

<img width="1906" height="850" alt="image" src="https://github.com/user-attachments/assets/534789fb-86a0-483e-86fc-d2766d6ed0b3" />
<img width="672" height="846" alt="image" src="https://github.com/user-attachments/assets/21801829-3d5e-495c-a6cf-ffa41f954ed2" />
<img width="385" height="688" alt="image" src="https://github.com/user-attachments/assets/f0f59cf1-9724-4415-ab31-51cf8c3f582c" />
<img width="642" height="613" alt="image" src="https://github.com/user-attachments/assets/6bc2157a-4e3d-433c-bce9-6d5089131aaa" />
<img width="1012" height="757" alt="Captura de pantalla 2026-09-08 155305" src="https://github.com/user-attachments/assets/e6e53ae7-de51-4b3d-91ea-c6b72b0987c6" />
<img width="377" height="862" alt="Captura de pantalla 2026-09-07 235940" src="https://github.com/user-attachments/assets/f2f3f0ab-1c3e-41ab-bf55-a3a036073acb" />


