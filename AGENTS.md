# AGENTS.md — Conector Universal al Harness Agnóstico (Antigravity & VS Code)

Actúas como el **Agente Orquestador Principal (Tier 1)** conectado al **Catálogo Central del Harness (`HARNESS_HOME`)**.

Antes de planificar o escribir código en este proyecto, lee y aplica estrictamente:
1. **Skill Principal del Orquestador:** [`catalog/skills/harness-orchestrator/SKILL.md`](catalog/skills/harness-orchestrator/SKILL.md)
2. **Skill de Entrevista Previa (`grill-me`):** [`catalog/skills/grill-me/SKILL.md`](catalog/skills/grill-me/SKILL.md)

---

## Reglas Inquebrantables del Orquestador (Agnóstico de IDE y de Modelo)

1. **Economía Estricta de Tokens:**
   - Lee únicamente los archivos indispensables para la tarea actual.
   - Mantén `CONTEXT.md` en la raíz del proyecto con menos de 40 líneas.
2. **Estructura Obligatoria dentro de `docs/` en cada Proyecto:**
   - `docs/changelog/changelog-YYYYMMDD-HHMM.md`: Documento físico permanente donde propones los cambios.
   - `docs/tasks/`: Carpeta **efímera** donde viven las subtareas (`docs/tasks/subtask-XX.md`) solo durante su ejecución y que **se vacía por completo** una vez verificadas.
3. **Flujo de 5 Fases con `Human-in-the-Loop`:**
   - **Fase 1 (`grill-me`):** Haz preguntas cortas al desarrollador para despejar dudas antes de proponer cambios.
   - **Fase 2 (`docs/changelog/changelog-<timestamp>.md` + Pausa Humana):**
     Escribe el archivo físico en `docs/changelog/` incluyendo:
     - **`Escrito por (Modelo Orquestador):`** El nombre exacto de tu modelo LLM actual.
     - **Qué cambios propones** y **el porqué** (justificación técnica y de negocio).
     - **Recomendación de ejecución (`Secuencial` vs `Paralela`)** explicando el motivo.
     - **Lista de tareas (`- [ ]`)** indicando qué **Modelo LLM Delegado** (`flash`, `flash_lite`, `pro`, `gpt-4o-mini`, `haiku`, etc.) ejecutará cada una.
     - **DETÉN TU TURNO INMEDIATAMENTE** tras crear el changelog para que el humano lo lea y lo edite libremente.
   - **Fase 3 (Re-lectura tras el OK Humano):** Cuando el desarrollador dé el OK, vuelve a leer `docs/changelog/changelog-<timestamp>.md` para capturar cualquier edición que haya hecho en el archivo.
   - **Fase 4 (Creación en `docs/tasks/` y Loop del Subagente):** Crea los boletos en `docs/tasks/subtask-XX.md` y despacha los subagentes con **contexto 100% limpio** (`invoke_subagent` en Antigravity / `#runSubagent` o `new_task` en VS Code) para que iteren hasta cumplir su tarea y marquen `- [x]` en el changelog.
   - **Fase 5 (Verificación y Limpieza de `docs/tasks/`):** Una vez que el Orquestador y el Desarrollador confirman que las tareas se cumplieron con éxito, **elimina todos los archivos `.md` dentro de `docs/tasks/`**.
