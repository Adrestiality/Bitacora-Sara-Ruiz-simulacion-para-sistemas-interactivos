# ☄️UNIDAD 4

- **Despliegue de la Actividad:** [Ver Actividad Interactiva](https://adrestiality.github.io/REPOSITORIO_UNIDAD4_SIMULACION/)

## 🌟1.Ideación

La verdad es que el proceso de ideacion fue una completa locura y caos. porque la unidad me parecia muy interesante, proponia mucha libertad y posibilidad de hacer muchas cosas nuevas. PERO NO SABIA QUE HACEEEEEEEEEEER. 

La verdad es que termine inspirada en el trabajo de un amiguito que tenia una especie de maya 3d, lo que me llevo a pernsar en el entorno 3d, y luego pense en un juego llamado monument valley que es muy minimalista y trata principalmente sobre la perspectiva y el mundo 3d.

La idea es la isguiente. eciste un plano y un pequeño bichito negro por ahi caminando. delos cuadors de dicho plano puedes crear pilares verticales y horizontales de longitudes aleatorias y todos empiezan a resonar. la gracia es que crees tu propia torre y el bichito ira escalandola tratandose de sumar a la melodia. si el bichito deja de moverse pq ya no hay mas pilares para escalar, va  adestruir todo lo que hay de torre. imaginatelo como esos problemas de la vida que siempre estan ahi pero que te pueden estancar y destruir todo de golpe si dejas que esten mucho tiempo.

Si lo vemos desde la perspectiva de la actividad, la gracia es que los pilares y el bicho resuenan de manera distinta. deberan hacer lo posible para unificarse en una melodia sin parar demasiado tiempo.

## 🌟2. Proceso de Creación

Aqui genuinamente decidi reutilizar el repositorio de la unidad anterior. es bastante util la verdad. 

Luego decidi seguir la recomendacion de mis amiguitas. que es sentarse con chat gpt y explicarle el proyecto de manera super detallada y con dibujitos como funciona mi idea, y que luego el hiciera los prompts oara antigravity. genuinamente esta es la parte donde todo me da mucha más pereza.

<img width="1280" height="1600" alt="1" src="https://github.com/user-attachments/assets/62ebf901-a5cf-4c00-9491-9e0025c1c4e9" />
<img width="1280" height="1600" alt="2" src="https://github.com/user-attachments/assets/3ad5f8b6-8abb-47fc-b83e-039898106a7c" />
<img width="1280" height="1600" alt="3" src="https://github.com/user-attachments/assets/7a3d7f08-38e4-4113-bd0c-6999755b8ac9" />
<img width="1280" height="1600" alt="4" src="https://github.com/user-attachments/assets/19b50a08-d2f3-4ef2-8c9c-755e1492f190" />
<img width="1280" height="1600" alt="5" src="https://github.com/user-attachments/assets/664c6925-f484-432d-9343-0bff8a24af5f" />
<img width="1280" height="1600" alt="6" src="https://github.com/user-attachments/assets/f1ef11ef-c446-494a-9764-c2bb798dbbfe" />
<img width="1280" height="1600" alt="7" src="https://github.com/user-attachments/assets/d9cfb227-cc60-4461-b18d-62f6c9a0b794" />
<img width="1280" height="1600" alt="8" src="https://github.com/user-attachments/assets/720043b4-1b5d-4dfa-83c6-18f8999fc84f" />
<img width="1280" height="1600" alt="8" src="https://github.com/user-attachments/assets/14d8d6c0-5893-4bcf-a599-2eba10c5fb88" />

Luego de pasar todo a antigravity tuve que rehacer ajustes tecnicos. como, por ejemplo, el bichito se salia del margen de la cuadricula y era como bro??

<img width="327" height="432" alt="Captura de pantalla 2026-09-06 214724" src="https://github.com/user-attachments/assets/fa1c9288-a5ba-4a8a-8523-19d14f3b853e" />
<img width="562" height="443" alt="Captura de pantalla 2026-09-07 234545" src="https://github.com/user-attachments/assets/ff0be1ba-894d-4f5b-a36e-8d2809b7489e" />
<img width="567" height="742" alt="Captura de pantalla 2026-09-07 234550" src="https://github.com/user-attachments/assets/398ee253-52f1-456b-a6a0-097ed72d27d1" />


## 🌟3.¿Cómo funciona el juego?

La actividad interactiva consiste en crear pilares para que el bichito los recorra y suba, haciendo que todos los pilares resuenen en conjunto sin que se destruya la torre. Si el bichito se queda más de 6 segundos quieto, destruye la torre, cae al suelo y toca empezar de nuevo.

### Los Pilares
Tú no puedes elegir exactamente qué pilar poner; te salen de manera aleatoria (como si fueran cartas):
* **Verticales (4 tipos):** de 4, 3, 2 y 1 casillas.
* **Horizontales (3 tipos):** de 3, 2 y 1 casillas.
* Cada tipo se diferencia por un **color diferente**.

## 🌟4. Controles e Interfaz

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

## 🌟5. Autoevaluación

| Criterio / Autoevaluación | Puntaje |
| :--- | :---: |
| Leí y verifiqué que mi proyecto cumple con los requisitos mínimos de la unidad. | **25 pts** |
| Puedo explicar claramente qué representa cada variable del modelo de Kuramoto en mi proyecto. | **25 pts** |
| Puedo explicar claramente cómo las variables del modelo producen el comportamiento observado en mi proyecto. | **25 pts** |
| Puedo demostrar que mi proyecto cumple con los objetivos establecidos en la unidad. | **25 pts** |
| **Puntaje Total** | **100 pts** |
