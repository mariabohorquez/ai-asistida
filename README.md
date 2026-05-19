# Introducción al Desarrollo de Software Asistido por IA — FIUBA Posgrado

Trabajos prácticos de la materia **Introducción al Desarrollo de Software Asistido por IA** de la Especialización en Inteligencia Artificial, FIUBA.

---

## Trabajos prácticos

| # | Título | Carpeta |
|---|--------|---------|
| TP 1 | Worst UI Login Challenge | [`tp1/`](tp1/) |
| TP 2 | OpenAPI YAML — Backend del Login Challenge | [`tp2/`](tp2/) |

---

## TP 1 — Worst UI Login Challenge

Una serie de minijuegos inspirados en videojuegos clásicos que actúan como "verificación de identidad" frustrante antes de llegar al formulario de login real. Construido en una sola conversación con **Claude Code** (claude-sonnet-4-6) como demostración del flujo de desarrollo asistido por IA: plan → pivote creativo → implementación → iteración — todo en un único `index.html` sin dependencias externas.

### Cómo usarlo

Abrí `tp1/index.html` con doble click. No requiere servidor, build tools ni conexión a internet.

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

Ver [`tp1/prompts.md`](tp1/prompts.md) para la secuencia completa de prompts con anotaciones.

---

## TP 2 — OpenAPI YAML: Backend del Login Challenge

Diseño del contrato de API REST para el backend del juego construido en TP 1. El archivo [`tp2/openapi.yaml`](tp2/openapi.yaml) describe todos los recursos, schemas y respuestas de error siguiendo el estándar OpenAPI 3.1.

### Concepto

En lugar de usar una app de tareas genérica, el API modela el propio juego:

| Recurso | Descripción |
|---|---|
| `challenges` | Los 6 niveles del Login Challenge (Press Start, TTT, Pokémon, Mario, Space Invaders, Formulario) |
| `challenges/{id}/attempts` | Los intentos de cada jugador en cada nivel |
| `leaderboard` | Ranking global agregado por jugador |

La jerarquía `challenges → attempts` refleja que un intento no existe sin un desafío que lo contenga.

### Construcción

Construido en una conversación con **Claude Code** (claude-sonnet-4-6) en **Claude Desktop**. Flujo: concepto → primer draft del YAML → validación en [Swagger Editor](https://editor.swagger.io) → segunda iteración con el endpoint de leaderboard.

### Qué funcionó

- Conectar el API con el juego de TP 1 hizo trivial definir los recursos: los niveles son los `challenges`, las sesiones de juego son los `attempts`.
- Especificar el esquema de entrada (`ChallengeInput`, `AttemptInput`) separado del esquema de salida (`Challenge`, `Attempt`) evita tener que documentar por qué el output tiene campos que el input no acepta (como `id` o `createdAt`).
- `format: date-time` en los campos de fecha hace que Swagger UI los valide automáticamente sin extra config.

### Decisiones de diseño

- `leaderboard` vive en primer nivel y no anidado bajo `challenges` porque es una vista agregada sobre todos los desafíos, no un sub-recurso de uno en particular.
- Se usó `nullable: true` en lugar del estilo OpenAPI 3.1 puro (`type: [integer, "null"]`) por compatibilidad con Swagger Editor y la mayoría de los generadores de código.

### Prompts utilizados

Ver [`tp2/prompts.md`](tp2/prompts.md) para la secuencia completa de prompts con anotaciones.
