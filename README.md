# 💨 HumoCodigo (WebGL Fluid Simulation)

**Simulación de dinámica de fluidos de alto rendimiento para la web.**

Este proyecto implementa una simulación física de humo y fluidos utilizando **WebGL 2.0** (con fallback a WebGL 1.0). El efecto se renderiza en un elemento `<canvas>` que actúa como fondo (`z-index: -2`), permitiendo colocar contenido HTML superpuesto mientras el humo fluye e interactúa detrás.

## 📋 Características Principales

### 🧪 Física de Fluidos en GPU
* **Shaders Personalizados:** Utiliza un conjunto complejo de **Fragment Shaders** en GLSL para calcular las diferentes etapas de la dinámica de fluidos: advección, divergencia, vorticidad y presión.
* **Renderizado FBO (Frame Buffer Object):** Emplea técnicas de *Double Buffering* (intercambio de texturas de lectura/escritura) para mantener el estado de la velocidad y la densidad del humo cuadro a cuadro.

### 🎮 Modos de Interacción
El proyecto incluye dos comportamientos lógicos distintos:
1.  **Modo Automático (`smoke-simulation.js`):** El humo se mueve por sí solo siguiendo patrones aleatorios suaves, ideal para fondos decorativos que no requieren intervención del usuario. Un script calcula vectores de movimiento aleatorios periódicamente.
2.  **Modo Interactivo (`hola.js`):** Permite al usuario "dibujar" con el humo utilizando el mouse o gestos táctiles en pantallas móviles.

### 🎨 Personalización Visual
* **Configuración Global:** Variables ajustables para controlar la disipación de la densidad, la viscosidad de la velocidad, el radio de la "mancha" de humo y la turbulencia (Curl noise).

## 📂 Estructura del Proyecto

* `index.html`: Punto de entrada. Estructura el canvas a pantalla completa y carga el script principal.
* `smoke-simulation.js`: **Script Principal (Automático)**. Contiene toda la lógica de WebGL, compilación de shaders y el bucle de animación autónomo.
* `hola.js`: **Script Alternativo (Interactivo)**. Versión modificada donde la fuente del humo sigue el cursor del mouse o el dedo.

## 🚀 Instalación y Uso

1.  Clona el repositorio o descarga los archivos.
2.  Abre el archivo `index.html` en cualquier navegador moderno con soporte WebGL.
3.  **Para cambiar de modo:**
    * **Automático:** Asegúrate de que `index.html` apunte a `<script src="smoke-simulation.js"></script>`.
    * **Interactivo:** Cambia la referencia en `index.html` a `<script src="hola.js"></script>`.

## ⚙️ Configuración (Hardcoded)

Puedes ajustar el comportamiento físico del humo editando el objeto `config` al inicio de los archivos JavaScript (`smoke-simulation.js` o `hola.js`):

```javascript
var config = {
  TEXTURE_DOWNSAMPLE: 1,      // Calidad de la textura (mayor número = menos resolución, más rendimiento)
  DENSITY_DISSIPATION: 0.995, // Qué tan rápido desaparece el humo (cercano a 1 = dura más)
  VELOCITY_DISSIPATION: 0.995,// Qué tan rápido se frena el movimiento
  PRESSURE_DISSIPATION: 0.8,  // Disipación de presión
  PRESSURE_ITERATIONS: 25,    // Calidad de la simulación de presión (más alto = más lento)
  CURL: 30,                   // Cantidad de remolinos/vorticidad
  SPLAT_RADIUS: 0.015         // Tamaño del pincel/emisor
};
