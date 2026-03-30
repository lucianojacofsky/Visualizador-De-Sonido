# 🎵 Visualizador de Música en Tiempo Real

Un visualizador de audio interactivo construido con **Web Audio API** y **Canvas API** que reacciona a la música en tiempo real.

## Demo

Cargá un archivo de audio o activá el micrófono para ver las visualizaciones en acción.

## Características

- **4 modos de visualización**
  - **Barras** — espectro de frecuencias con gradiente de color dinámico
  - **Onda** — forma de onda en tiempo real del audio crudo
  - **Radial** — expansión circular de frecuencias desde el centro
  - **Partículas** — sistema de partículas reactivo a los bajos
- **Entrada de audio dual** — archivos locales (MP3, WAV, OGG, etc.) o micrófono
- **Control de sensibilidad** — ajuste de ganancia para señales débiles o fuertes
- **Responsive** — se adapta al tamaño del contenedor

## Tecnologías

| Tecnología | Uso |
|---|---|
| [Web Audio API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Audio_API) | Procesamiento y análisis de audio |
| [Canvas API](https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API) | Renderizado 2D en tiempo real |
| `AnalyserNode` | Extracción de datos de frecuencia y forma de onda |
| `AudioContext` | Grafo de nodos de audio |

## Cómo funciona

### Grafo de audio

```
Fuente (archivo/micrófono)
        ↓
   AnalyserNode  ←── FFT Size: 2048
        ↓
  AudioDestination
```

El `AnalyserNode` expone dos métodos clave:

- `getByteFrequencyData()` → array con la intensidad de cada frecuencia (para barras y radial)
- `getByteTimeDomainData()` → array con la forma de onda cruda (para el modo onda)

### Parámetros del analizador

```javascript
analyser.fftSize = 2048;              // Resolución del análisis (potencia de 2)
analyser.smoothingTimeConstant = 0.8; // Suavizado entre frames (0–1)
```

## Uso

### Desde archivo

1. Hacé clic en **Cargar audio**
2. Seleccioná un archivo de audio local
3. La reproducción comienza automáticamente en loop

### Desde micrófono

1. Hacé clic en **Micrófono**
2. Aceptá el permiso del navegador
3. El visualizador reacciona al sonido ambiente en tiempo real

> **Nota:** El modo micrófono no conecta la fuente al destino de audio para evitar feedback. El audio se analiza pero no se reproduce.

## Estructura del código

```
visualizer/
├── index.html       # Markup y controles UI
├── style.css        # Estilos (o inline en el ejemplo)
└── visualizer.js    # Lógica de Web Audio API y Canvas
```

### Funciones principales

| Función | Descripción |
|---|---|
| `initAudio()` | Crea el `AudioContext` y el `AnalyserNode` |
| `connectSource(src)` | Conecta una nueva fuente al analizador |
| `drawBars(data)` | Renderiza el modo barras |
| `drawWave(data)` | Renderiza el modo onda |
| `drawRadial(data)` | Renderiza el modo radial |
| `drawParticles(data)` | Renderiza el modo partículas |
| `draw()` | Loop principal con `requestAnimationFrame` |

## Compatibilidad

| Navegador | Soporte |
|---|---|
| Chrome / Edge | ✅ Completo |
| Firefox | ✅ Completo |
| Safari | ✅ (requiere interacción del usuario para iniciar `AudioContext`) |
| Opera | ✅ Completo |

> Los navegadores móviles pueden requerir interacción del usuario antes de iniciar el contexto de audio (política de autoplay).

## Recursos

- [Web Audio API — MDN](https://developer.mozilla.org/en-US/docs/Web/API/Web_Audio_API)
- [Canvas API Tutorial — MDN](https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API/Tutorial)
- [Ejemplos de Web Audio — MDN GitHub](https://github.com/mdn/webaudio-examples)
- [AnalyserNode — MDN](https://developer.mozilla.org/en-US/docs/Web/API/AnalyserNode)

## Licencia

MIT
