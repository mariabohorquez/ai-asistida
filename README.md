# Introducción al Desarrollo de Software Asistido por IA — FIUBA Posgrado

Trabajos prácticos de la materia **Introducción al Desarrollo de Software Asistido por IA** de la Especialización en Inteligencia Artificial, FIUBA.

---

## TP 1 — Worst UI Login Challenge

Una serie de minijuegos inspirados en videojuegos clásicos que actúan como "verificación de identidad" frustrante antes de llegar al formulario de login real. Construido en una sola conversación con **Claude Code** (claude-sonnet-4-6) como demostración del flujo de desarrollo asistido por IA: plan → pivote creativo → implementación → iteración — todo en un único `index.html` sin dependencias externas.

### Cómo usarlo

Abrí `index.html` con doble click. No requiere servidor, build tools ni conexión a internet.

### Niveles

| # | Nombre | Mecánica del horror |
|---|--------|---------------------|
| 0 | Press Start | El botón de inicio escapa del cursor |
| — | Verificando identidad... | Barra de progreso que falla antes de "No se pudo verificar. Continuando igual." |
| 1 | Tic Tac Toe | La IA usa minimax perfecto — es matemáticamente imposible ganar |
| 2 | Pokémon Battle | Tu pokémon tiene 1 HP, el rival tiene 999. "RENDIRSE" es la única salida viable |
| 3 | Super Login Bros. | Plataformer en canvas donde la bandera huye cuando te acercás |
| 4 | Space Auth Invaders | Space Invaders jugable con los controles izquierda/derecha invertidos |
| 5 | Formulario final | Los labels se intercambian cada 2.5s. El botón grande dice "Cerrar sesión". El link "Cancelar" es el login real |

### Construcción

Construido en una sola conversación con **Claude Code** en **Claude Desktop** (claude-sonnet-4-6). Claude Desktop incluye un panel de preview de HTML en tiempo real, lo que permitió iterar visualmente el artefacto sin salir de la conversación. El flujo fue iterativo: plan → pivote creativo → simplificación → implementación → ajustes → nivel extra → bug fixes.

El constraint de un solo `index.html` sin dependencias externas resultó ser una guía útil: obligó a soluciones simples (canvas primitives en lugar de sprites, CSS puro para el efecto de scanlines, minimax en ~20 líneas).

### Qué funcionó

- **La barra de carga falsa** fue la mejor idea emergente — no estaba en el plan original, fue sugerida por el modelo como transición.
- **El TTT con minimax** es genuinamente inganable, no tramposamente inganable.
- **Space Invaders con controles invertidos** tiene el efecto deseado: el jugador tarda unos segundos en darse cuenta de qué está mal.
- El **estilo visual CRT** (scanlines CSS + paleta verde sobre negro) dio coherencia estética a niveles muy distintos.

### Qué no funcionó

- **Emoji en `<canvas>`**: `fillText('🚩')` no renderiza de forma confiable. La bandera de Mario fue reemplazada por primitivas geométricas.
- **Doom descartado**: hubiera requerido raycasting (~200 líneas extra) por una ganancia marginal respecto a Space Invaders.
- El modelo tendió a generar código más prolijo de lo necesario en la primera versión. Requirió un prompt explícito de simplificación.

### Prompts utilizados

Ver [`prompts.md`](prompts.md) para la secuencia completa de prompts con anotaciones.
