---
name: harness-orchestrator
description: >-
  Skill global Multi-IDE con economía estricta de tokens y Human-in-the-Loop real:
  1) Ejecuta grill-me, 2) Escribe el archivo físico docs/changelog/changelog-<timestamp>.md
  con el qué, el porqué, la lista de tareas con modelos LLM y la recomendación de ejecución
  (Secuencial vs Paralela), y DETIENE su turno para que el humano lea y edite el archivo,
  3) Al recibir el OK del humano, re-lee el changelog editado, crea las subtareas en docs/tasks/,
  ejecuta los subagentes hasta marcar [x] y limpia docs/tasks/ al verificar.
---

# Skill Global: Harness Orquestador Multi-IDE (`docs/changelog/` + `docs/tasks/` Efímero)

Esta skill gobierna al **Agente Orquestador (Tier 1)** bajo principios de **Economía Extrema de Tokens** y **Pausa Humana Obligatoria sobre el Changelog Físico**, 100% libre de scripts externos.

## Estructura Estándar en Cada Proyecto
Todo proyecto gestionado con este Harness utiliza dentro de su carpeta `docs/`:
- `docs/changelog/changelog-YYYYMMDD-HHMM.md`: Registro físico permanente (qué, porqué, modelos LLM y checks `[x]`).
- `docs/tasks/`: Carpeta **efímera** donde se escriben las subtareas (`docs/tasks/subtask-XX.md`) tras el OK humano y se borran al finalizar la verificación.

## Catálogo Central (`HARNESS_HOME`)
- `./catalog/` (o la ruta donde esté clonado el repositorio)
  - Entrevista previa: `catalog/skills/grill-me/SKILL.md`
  - Perfiles de Subagentes: `catalog/subagents/subagent-*.md`
  - Skills técnicas: `catalog/skills/<skill>/SKILL.md`

---

## Flujo Obligatorio de 5 Fases

### Fase 1: Entrevista Corta de Alineación (`grill-me`)
1. Antes de proponer cambios, activa [`catalog/skills/grill-me/SKILL.md`](../grill-me/SKILL.md) para despejar dudas clave con el desarrollador (`ask_question` o preguntas directas).
2. **Prohibido** escribir en `docs/tasks/` o tocar código en esta fase.

---

### Fase 2: Escritura del Archivo Físico `docs/changelog/changelog-<timestamp>.md` y Pausa `Human-in-the-Loop`
Con las respuestas del desarrollador, crea el archivo físico en el repositorio del proyecto:
- **Ruta:** `docs/changelog/changelog-YYYYMMDD-HHMM.md`
- **Metadato obligatorio en cabecera:** Debe indicar explícitamente **`Escrito por (Modelo Orquestador): <Nombre del LLM activo>`** (ej. `Gemini 4 Argon (Medium) — Tier 1 Frontera` o `Claude Opus`).
- **Secciones obligatorias del archivo:**
  1. **Contexto y Propuesta de Cambios:** Qué se va a construir o modificar.
  2. **El Porqué de los Cambios (Justificación Arquitectónica y de Negocio):** Por qué se toma cada decisión.
  3. **Recomendación de Estrategia de Ejecución (`Secuencial` vs `Paralela`):** Analiza si existe dependencia de código entre subtareas.
  4. **Checklist de Tareas Planeadas (`- [ ]`) y Modelos LLM Delegados:** Lista editable donde cada tarea especifica qué modelo inferior se propone (`flash`, `flash_lite`, `pro`), qué `skill` usará y qué `target_files` tocará.

> **REGLA CRÍTICA DE PAUSA HUMANA (FINALIZAR TURNO):**
> En el turno donde creas `docs/changelog/changelog-YYYYMMDD-HHMM.md`:
> - **NO** llames a `ask_question` (para no bloquear la pantalla con un modal).
> - **NO** crees archivos en `docs/tasks/`.
> - **NO** lances ningún subagente.
> - Entrega al desarrollador el enlace al archivo físico `docs/changelog/changelog-YYYYMMDD-HHMM.md` junto con tu recomendación (`Secuencial` vs `Paralela`), e indícale que puede abrir el `.md`, leerlo, **editar directamente el archivo si quiere cambiar modelos, agregar o quitar puntos**, y responder en el chat con su OK cuando esté listo.

---

### Fase 3: Re-lectura del Changelog Editado por el Humano
Cuando el desarrollador responde dando el OK para correr los subagentes:
1. **PRIMERO lee nuevamente `docs/changelog/changelog-YYYYMMDD-HHMM.md` con `read_file`** para capturar cualquier modificación, ajuste de modelo LLM o criterio extra que el humano haya escrito manualmente en el archivo físico.
2. Respeta la estrategia de ejecución acordada (`Secuencial` o `Paralela`).

---

### Fase 4: Creación de Subtareas en `docs/tasks/` y Loop de Ejecución con Check `[x]`
1. Crea los boletos efímeros en `docs/tasks/subtask-XX.md` reflejando exactamente lo aprobado en el changelog físico y el `model_id` elegido.
2. Despacha los subagentes con contexto 100% limpio (`invoke_subagent` en Antigravity con `Model: "<flash|flash_lite|pro>"`, o subagente nativo en Cursor/VS Code):
   - **Si es Secuencial:** Lanza la `subtask-01`, espera a que termine y marque `[x]` en el changelog, y recién entonces lanza la `subtask-02`.
   - **Si es Paralela:** Lanza las subtareas independientes en simultáneo.
3. Cada subagente lee **únicamente** `CONTEXT.md`, su `docs/tasks/subtask-XX.md` y su `skill_path`, itera hasta cumplir los criterios, pasa su boleto a `status: completed` y **marca con `- [x]` su ítem en `docs/changelog/changelog-<timestamp>.md`**.

---

### Fase 5: Verificación Conjunta y Limpieza de `docs/tasks/` (Economía de Tokens)
1. El Orquestador verifica que todos los ítems de `docs/changelog/changelog-<timestamp>.md` tengan su check `- [x]` y reporta al Desarrollador.
2. Una vez que el Orquestador y el Desarrollador aseguran que las tareas fueron realizadas con éxito:
   - Se eliminan todos los archivos `.md` de `docs/tasks/` (dejando `docs/tasks/` vacía para ahorrar tokens).
   - Se actualiza el estado de `docs/changelog/changelog-<timestamp>.md` a `VERIFIED_AND_CLOSED`.
