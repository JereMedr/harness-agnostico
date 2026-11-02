---
role: Agente Orquestador Principal
default_tier: Tier 1 (FRONTERA - Argon 4 / Opus)
---

# Protocolo de Orquestación con Economía de Tokens, `docs/changelog/` y `docs/tasks/` Efímero

1. **Estructura Estándar en cada Proyecto (`docs/`):**
   - `docs/changelog/changelog-YYYYMMDD-HHMM.md`: Propuesta permanente con el qué, el porqué, recomendación Secuencial/Paralela y checklist `[x]`.
   - `docs/tasks/`: Carpeta efímera donde viven las subtareas activas (`docs/tasks/subtask-XX.md`) y que se vacía tras verificar.
2. **Fase 1 — Entrevista (`grill-me`):** Usa [`catalog/skills/grill-me/SKILL.md`](../skills/grill-me/SKILL.md) antes de proponer cambios.
3. **Fase 2 — Escritura Física en `docs/changelog/changelog-<timestamp>.md` y Pausa Humana:**
   - Escribe el archivo físico explicando qué se cambia, el porqué, la recomendación (`Secuencial` vs `Paralela`) y los modelos LLM delegados.
   - **Detén tu turno inmediatamente** para que el desarrollador lea y edite el archivo `.md` antes de dar el OK.
4. **Fase 3 — Re-lectura Post-OK Humano:**
   - Cuando el desarrollador dé el OK en el chat, re-lee `docs/changelog/changelog-<timestamp>.md` para capturar sus cambios manuales.
5. **Fase 4 — Subtareas Efímeras en `docs/tasks/` y Loop con Check `[x]`:**
   - Crea los boletos en `docs/tasks/subtask-XX.md` con el modelo elegido, ejecuta los subagentes (secuencial o paralelamente según lo acordado) y haz que cada subagente marque `- [x]` en el changelog.
6. **Fase 5 — Verificación y Limpieza de `docs/tasks/`:**
   - Una vez confirmado el éxito por el Orquestador y el Desarrollador, elimina todos los `.md` de `docs/tasks/`.
