# Secuencia de prompts — TP 1: Worst UI Login Challenge

Conversación conducida con **Claude Code** (claude-sonnet-4-6) en **Claude Desktop**.

---

## Prompt 1 — Pedido de plan
> "me pidieron hacer un repo en donde entregue la peor UI posible. Se me ocurre hacer una serie de desafios para login. Antes de comenzar por favor haz un plan de lo que vamos a hacer"

**Anotación:** Claude propuso 7 niveles de horror UX clásico (botón que escapa, campo amnésico, colores aleatorios, etc.). Útil como punto de partida pero demasiado genérico — no tenía identidad visual propia.

---

## Prompt 2 — Pivote creativo
> "antes de seguir, podemos hacer los niveles inspirados en videojuegos? estilo doom, una batalla pseudo pokemon sencilla, tic tac toe, un mini nivel estilo mario, algo asi? o es mucho para un solo html"

**Anotación:** El modelo confirmó que era factible en un solo HTML sin dependencias. Propuso 6 niveles con estimación de dificultad técnica por nivel. Doom fue marcado como el más complejo por necesitar raycasting.

---

## Prompt 3 — Simplificación
> "simplifica para que no sea tan extenso, pero que siga siendo divertido. Agregarias algo mas?"

**Anotación:** Se recortó a 4 niveles + intro. El modelo sugirió la barra de carga falsa como transición entre niveles — fue la mejor adición emergente de esta ronda. El nivel de Doom fue descartado acá.

---

## Prompt 4 — Implementación
> "dale, pruebalo"

**Anotación:** El modelo generó el `index.html` completo (~720 líneas) en un solo turno. Funcionó en su mayoría en el primer intento. El TTT con minimax resultó genuinamente inganable. El efecto de scanlines CSS fue un agregado no pedido que mejoró la estética.

---

## Prompt 5 — Ajustes de UX (ironía intencional)
> "haria lo de la verificacion de identidad 1 sola vez para que sea mas rapido, tarda mucho. quiero que mario tambien se pueda jugar con WASD"

**Anotación:** Dos fixes quirúrgicos. Interesante: mejorar la UX de una "peor UI posible" es un meta-problema. Se redujo el loader de 3 ciclos a 2. WASD ya estaba en el código pero no documentado en el hint de pantalla.

---

## Prompt 6 — Nivel extra
> "agregaria un nivel adicional despues de mario, capaz si podemos hacer doom? o el space invaders"

**Anotación:** Se eligió Space Invaders por ser más confiable que Doom en canvas puro. El chiste del nivel (controles invertidos sin avisar) fue propuesto por el modelo. El juego base funciona correctamente — la dificultad artificial es solo que izquierda y derecha están swapeados.

---

## Prompt 7 — Bug fix
> "en el nivel de mario no hay ninguna bandera visible"

**Anotación:** `fillText()` con emoji no es confiable en `<canvas>`. La solución fue reemplazar el emoji 🚩 por una figura geométrica (triángulo amarillo + palo gris) dibujada con primitivas de canvas. Lección: evitar emoji en canvas.
