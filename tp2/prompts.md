# Secuencia de prompts — TP 2: OpenAPI YAML

Conversación conducida con **Claude Code** (claude-sonnet-4-6) en **Claude Desktop**.

---

## Prompt 1 — Concepto
> "momento de trabajar en el segundo TP de la materia. En la imagen explican los requerimientos. Quiero que el API sea el backend del juego que hicimos en TP1. Antes de arrancar, planificá qué recursos usar"

**Anotación:** El modelo propuso usar `challenges` para los niveles del juego y `attempts` para los intentos de cada jugador. La jerarquía `challenges → attempts` justifica el path nesting de forma natural. También sugirió separar los schemas de entrada (`ChallengeInput`) de los de salida (`Challenge`) — la salida tiene campos como `id` y `createdAt` que no tienen sentido en el body de un POST.

---

## Prompt 2 — Generación del YAML
> "generá el openapi.yaml completo con esos recursos. Versión OpenAPI 3.1, servidor en localhost:8000"

**Anotación:** El modelo generó el archivo completo en un turno. Cubrió los requisitos de la consigna sin que hiciera falta pedirlo explícitamente: GET/POST/DELETE en ambos recursos, errores 400 y 404, schemas con `type`, `required`, `format: date-time` y `enum`.

---

## Prompt 3 — Iteración: leaderboard
> "sin tocar los paths anteriores, agregá un endpoint /leaderboard que devuelva un ranking global de jugadores"

**Anotación:** El modelo tocó únicamente el bloque `paths` (agregó `/leaderboard`) y `components/schemas` (agregó `LeaderboardEntry`), sin modificar nada de lo anterior. El endpoint quedó en primer nivel y no anidado bajo `challenges` porque es una vista agregada de todos los desafíos, no un sub-recurso de uno en particular.
