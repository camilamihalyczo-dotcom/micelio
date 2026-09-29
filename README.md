# 🍄 Micelio Cyborg — Control Rítmico LED (Web Bluetooth BLE)

Interfaz web progresiva diseñada para controlar tiras LED direccionables (Dream Color / Mr Star) vía **Bluetooth Low Energy (BLE)** mediante la **Web Bluetooth API** y la **Web Audio API**.

El sistema sustituye las secuencias cerradas de fábrica por un algoritmo de detección de ritmo (*Beat Detection*) en tiempo real ejecutado directamente en el navegador del teléfono, alternando entre una paleta personalizada de **Blanco** y **Celeste** al compás de la música capturada por el micrófono.

---

## 🚀 Aplicación en Vivo
Accede directamente desde el navegador **Google Chrome** (Android / PC con Bluetooth):  
👉 **[https://camilamihalyczo-dotcom.github.io/micelio/](https://camilamihalyczo-dotcom.github.io/micelio/)**

---

## 🛠️ Especificaciones Técnicas

* **Tecnología:** HTML5, CSS3, JavaScript nativo (sin dependencias ni frameworks pesados).
* **APIs de Navegador:**
  * **Web Bluetooth API:** Conexión y control por atributos GATT sin requerir servidor backend.
  * **Web Audio API:** Análisis espectral por Transformada Rápida de Fourier (FFT de 256 muestras).
* **Parámetros BLE del Controlador:**
  * **Nombre del Dispositivo:** `GATT--DEMO`
  * **Service UUID:** `0xFFF0` (`0000fff0-0000-1000-8000-00805f9b34fb`)
  * **Write Characteristic UUID:** `0xFFF3` (`0000fff3-0000-1000-8000-00805f9b34fb`)
  * **Permisos:** `WRITE`, `WRITE NO RESPONSE`

---

## 🎧 Algoritmo de Detección de Ritmo (*Beat Detection*)

A diferencia de los detectores simples por umbral de volumen:
1. **Filtro de Frecuencias Bajas:** Monitorea exclusivamente las frecuencias entre 20 Hz y 150 Hz (donde residen los bombos, golpes de percusión y notas graves).
2. **Promedio Dinámico Móvil:** Mantiene un búfer circular de energía reciente. Se dispara un golpe de ritmo (*beat*) únicamente cuando la energía instantánea supera al promedio ponderado por el factor de sensibilidad.
3. **Anti-rebote (*Debounce*):** Incluye una ventana de bloqueo de 180 ms para evitar falsos positivos o dobles disparos en un solo compás.
4. **Paleta Rítmica:**
   * **Golpe 1:** Blanco brillante (`#FFFFFF`).
   * **Golpe 2:** Celeste vibrante (`#00B4D8`).
   * **Reposo / Silencio:** Celeste tenue de fondo (`#000F1E`).

---

## 📋 Pasos para la Prueba

1. **Condiciones previas:**
   * Conectar la tira LED a su fuente de 5V.
   * Cerrar totalmente la app *Mr Star* y *nRF Connect* (incluso de aplicaciones recientes en segundo plano).
   * Activar **Bluetooth** y **Ubicación (GPS)** en el teléfono Android.
2. **Conexión:**
   * Abrir el enlace en Google Chrome y presionar **"1. Conectar Tira LED"**.
   * Seleccionar `GATT--DEMO` y presionar **Vincular**.
3. **Identificación de Protocolo:**
   * Seleccionar el **Protocolo 1** y tocar los botones **Test Blanco** y **Test Celeste**.
   * Si la tira no cambia de color, cambiar al **Protocolo 2**, **3** o **4** hasta ver respuesta en las luces.
4. **Modo Rítmico:**
   * Presionar **"2. Iniciar Detección de Ritmo"**.
   * Conceder el permiso de acceso al micrófono solicitado por Chrome.
   * Reproducir música cerca del teléfono; la tira alternará entre blanco y celeste con cada golpe de bajo.
   * Calibrar el control deslizante de **Sensibilidad** si el ambiente tiene mucho o poco volumen.

---

## 📄 Licencia
Proyecto libre y abierto bajo licencia MIT para experimentación, domótica e ingeniería inversa de hardware comercial.
