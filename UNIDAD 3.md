# ☄️UNIDAD 3

## 🌟 RETO DE DISEÑO

- ✨ **Instrumento funcional y publicado**

>
> https://adrestiality.github.io/REPOSITORIO_UNIDAD3_SIMULACION/
>

- ✨ **Mapa del sistema**

>**ESTADOS**:
>
>**Morfing entre Geometrías:** 
>
>Cambia de forma (Esfera, Cubo o Reloj de Arena) mediante una interpolación suave de 1.5 segundos entre el punto actual y el objetivo.Las fuerzas físicas siguen activas durante la transición para mantener un movimiento orgánico
>
> **Estado de Pausa e Inercia:** 
>
>Permite congelar la simulación o reiniciar las velocidades y posiciones a su distribución geométrica base.

>**FÍSICAS**
>
>**Radial (Atracción/Repulsión):** 
>
>Atrae las partículas hacia el cursor o las repele lejos de él. Es fuerte de cerca, débil de lejos e incluye un suavizado para evitar velocidades infinitas en el centro.
>
>**Vórtice:** 
>
>Aplica un impulso perpendicular a la dirección radial, haciendo que las partículas giren en espiral alrededor del punto central en lugar de ir en línea recta.
>
>
>**Fricción (Drag):** 
>
>Funciona como la resistencia del aire o agua. Frena las partículas proporcionalmente a su velocidad para evitar que aceleren sin control.
>
>**Viento:** 
>
>Empuja constante y uniformemente a todas las partículas en una dirección específica del espacio 3D.
>
>**Atractor de Lorenz:** 
>
> Guía las partículas a lo largo de un sistema dinámico caótico, creando un patrón de movimiento con la clásica forma de "alas de mariposa".
>
>**Turbulencia (Curl Noise):** 
>
>Genera remolinos y ráfagas suaves mediante un campo de fluido incompresible, evitando que las partículas colapsen o se acumulen.
>
>**Onda de Choque (Pulse):** 
>
>Empuja las partículas hacia afuera mediante una onda esférica que nace en el origen y se expande periódicamente.
>
>**Flujo de Bandada (Boids):** 
>
>Coordina el movimiento colectivo como un cardumen de peces mediante ondas trigonométricas globales, sin requerir cálculos individuales entre partículas.
>
>**Presión por Densidad:** 
>
> Mide la concentración de partículas en una grilla 3D y empuja la materia desde las zonas muy pobladas hacia las áreas más vacías.

>**CONTROLES**:
>
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
>

- ✨ **Ficha de fuerzas**

>
>## Fuerzas Físicas (Formulación Matemática en Markdown)

* **Fuerza Radial (Atracción / Repulsión):**
  Calcula un vector unitario hacia el atractor y escala la magnitud inversamente al cuadrado de la distancia, sumando un término de suavizado (`softening`) en el denominador para evitar divisiones por cero[span_0](start_span)[span_0](end_span):
  
  `F_radial = ((p_attractor - p) / (||p_attractor - p|| + 0.0001)) * (Strength / (||p_attractor - p||^2 + softening^2)) * radialEnabled`[span_1](start_span)[span_1](end_span)

* **Vórtice (Rotación Tangencial):**
  Aplica el producto cruz entre el vector unitario del eje Z (`vec3(0, 0, 1)`) y la dirección radial, generando una fuerza perpendicular que induce una rotación en espiral[span_2](start_span)[span_2](end_span):
  
  `F_vortex = (z_axis x r_dir) * vortexStrength * vortexEnabled`[span_3](start_span)[span_3](end_span)

* **Fricción / Drag (Resistencia Lineal):**
  Fuerza de frenado directamente opuesta al vector de velocidad actual y proporcional al coeficiente de arrastre[span_4](start_span)[span_4](end_span):
  
  `F_drag = -1.0 * v * dragCoefficient * dragEnabled`[span_5](start_span)[span_5](end_span)

* **Viento:**
  Vector tridimensional constante que aplica una aceleración uniforme a todo el sistema[span_6](start_span)[span_6](end_span):
  
  `F_wind = Vector3(wind.x, wind.y, wind.z) * windEnabled`[span_7](start_span)[span_7](end_span)

* **Atractor de Lorenz (Sistema Caótico):**
  Evalúa el sistema de ecuaciones diferenciales continuas de Lorenz con las constantes `sigma = 10`, `rho = 28` y `beta = 8/3`[span_8](start_span)[span_8](end_span):
  
  `dx/dt = sigma * (y - x)`[span_9](start_span)[span_9](end_span)  
  `dy/dt = x * (rho - z) - y`[span_10](start_span)[span_10](end_span)  
  `dz/dt = x * y - beta * z`[span_11](start_span)[span_11](end_span)  
  `F_lorenz = (v_lorenz - v) * lorenzStrength * lorenzEnabled`[span_12](start_span)[span_12](end_span)

* **Curl Noise (Turbulencia Incompresible):**
  Calcula el rotacional de un campo escalar de ruido Perlin 3D (`mx_noise_vec3`) mediante aproximación por diferencias finitas[span_13](start_span)[span_13](end_span). Garantiza divergencia cero (`div(F) = 0`), simulando un fluido incompresible sin puntos de colapso[span_14](start_span)[span_14](end_span):
  
  `F_curl = rotacional(A) = (dAz/dy - dAy/dz, dAx/dz - dAz/dx, dAy/dx - dAx/dy) * curlStrength * curlEnabled`[span_15](start_span)[span_15](end_span)

* **Onda de Choque / Pulse Wave:**
  Onda esférica concéntrica cuyo radio crece linealmente con el tiempo (`r_wave = (time * speed) mod maxRadius`)[span_16](start_span)[span_16](end_span). La magnitud sobre las partículas sigue una atenuación con distribución gaussiana[span_17](start_span)[span_17](end_span):
  
  `F_pulse = dir_pulse * exp(-((dist - r_wave)^2) / width^2) * (pulseStrength / (1.0 + 0.15 * dist)) * pulseEnabled`[span_18](start_span)[span_18](end_span)

* **Flujo de Bandada / Boids Flow Field:**
  Genera un campo de velocidad continuo basado en funciones trigonométricas entrelazadas en los tres ejes sin calcular vecindades $O(N^2)$[span_19](start_span)[span_19](end_span):
  
  `v_flow = Vector3(sin(y * k + t), cos(z * k + t), sin(x * k + t)) * 2.5`[span_20](start_span)[span_20](end_span)  
  `F_boids = (v_flow - v) * boidsStrength * boidsEnabled`[span_21](start_span)[span_21](end_span)

* **Presión por Densidad (Grilla 3D / Spatial Hash):**
  Primero acumula la masa de partículas por celda en una grilla de $16 \times 16 \times 16$[span_22](start_span)[span_22](end_span). Luego calcula el gradiente negativo de densidad (`-grad(rho)`) mediante diferencias finitas para empujar las partículas hacia las zonas de menor concentración[span_23](start_span)[span_23](end_span):
  
  `grad_x = (rho[x+1,y,z] - rho[x-1,y,z]) / 2`[span_24](start_span)[span_24](end_span)  
  `grad_y = (rho[x,y+1,z] - rho[x,y-1,z]) / 2`[span_25](start_span)[span_25](end_span)  
  `grad_z = (rho[x,y,z+1] - rho[x,y,z-1]) / 2`[span_26](start_span)[span_26](end_span)  
  `F_pressure = -Vector3(grad_x, grad_y, grad_z) * pressureStrength * pressureEnabled`[span_27](start_span)[span_27](end_span)

>

- ✨ **Registro de pruebas**

>
>uwu
>

- ✨ **Score visual**

>
>uwu
>

- ✨ **Bitácora de IA**

>
>uwu
>

- ✨ **Autoevaluación ponderada**

>
>uwu
>
