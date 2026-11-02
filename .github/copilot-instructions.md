# Instrucciones para Visual Studio Code (GitHub Copilot / Agent Mode / Cline / Roo)

Este workspace utiliza el **Harness Agnóstico Multi-IDE**.

1. Lee [`AGENTS.md`](../AGENTS.md) y [`catalog/skills/harness-orchestrator/SKILL.md`](../catalog/skills/harness-orchestrator/SKILL.md).
2. Sigue siempre las 5 fases:
   - **Fase 1:** Entrevista corta `grill-me`.
   - **Fase 2:** Escribe el archivo físico `docs/changelog/changelog-YYYYMMDD-HHMM.md` (indicando qué modelo lo escribió, el qué, el porqué, recomendación Secuencial/Paralela y modelos LLM delegados) y **detén tu turno** para que el desarrollador pueda leerlo y editarlo.
   - **Fase 3:** Cuando el desarrollador dé el OK, re-lee el `changelog-YYYYMMDD-HHMM.md` editado.
   - **Fase 4:** Crea las subtareas en `docs/tasks/subtask-XX.md` y despáchalas en subagentes limpios (`#runSubagent` / `new_task`) hasta que marquen `- [x]` en el changelog.
   - **Fase 5:** Tras verificar con el desarrollador, elimina todos los archivos dentro de `docs/tasks/` para ahorrar tokens.
