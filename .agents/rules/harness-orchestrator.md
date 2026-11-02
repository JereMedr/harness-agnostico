---
trigger: always_on
description: Conector nativo de Google Antigravity al Harness Agnóstico Multi-IDE
---

# Regla de Orquestación Antigravity (`harness-orchestrator`)

Sigue estrictamente [`AGENTS.md`](../../AGENTS.md) y la skill [`catalog/skills/harness-orchestrator/SKILL.md`](../../catalog/skills/harness-orchestrator/SKILL.md):

1. **Fase 1 (`grill-me`):** Realiza preguntas cortas antes de planificar.
2. **Fase 2 (`docs/changelog/changelog-<timestamp>.md` + Pausa Humana):** Escribe el changelog físico con el modelo autor en cabecera, el qué, el porqué, la recomendación (`Secuencial` vs `Paralela`) y los modelos delegados. **Detén tu turno** sin llamar a `ask_question` ni `invoke_subagent` para que el humano lea y edite el `.md`.
3. **Fase 3 (Re-lectura):** Cuando el humano dé el OK, vuelve a leer el `changelog-<timestamp>.md`.
4. **Fase 4 (`docs/tasks/` + `invoke_subagent`):** Crea los boletos en `docs/tasks/subtask-XX.md` y lanza `invoke_subagent(TypeName="self", Model="<flash|flash_lite|pro|inherit>")` en contexto limpio hasta que marquen `- [x]` en el changelog.
5. **Fase 5 (Limpieza):** Una vez verificado con el desarrollador, borra los `.md` de `docs/tasks/`.
