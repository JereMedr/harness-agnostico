# IDE-Agnostic & Model-Agnostic Harness (Antigravity & Visual Studio Code)

Este repositorio es el **Catálogo Central (`HARNESS_HOME`)** que alimenta tus **Skills Globales** para trabajar en cualquier proyecto sin copiar archivos ni correr scripts.

---

## 1. Tus Skills Globales Instaladas

Puedes registrar globalmente en tu entorno (`~/.gemini/config/skills.json` o la configuración de tu agente) estas dos skills:

1. **`harness-orchestrator`** ([`SKILL.md`](./catalog/skills/harness-orchestrator/SKILL.md)):
   * Orquestador principal con economía de tokens, escritura física de `docs/changelog/changelog-<timestamp>.md`, pausa `Human-in-the-Loop`, recomendación `Secuencial` vs `Paralela`, ejecución limpia en `docs/tasks/` y limpieza final de `docs/tasks/`.
2. **`grill-me`** ([`SKILL.md`](./catalog/skills/grill-me/SKILL.md)):
   * Entrevista interactiva corta para alinear reglas de negocio y arquitectura antes de generar el changelog.

---

## 2. Cómo Invocar la Skill Global (Sin Copiar Archivos ni Rutas)

### En Google Antigravity (En cualquier carpeta o repositorio)
Como `harness-orchestrator` y `grill-me` ya están cargadas globalmente en Antigravity, solo abre cualquier proyecto y escribe en el chat:
> *"Usa el skill `harness-orchestrator` para..."* *(o *"Arranca con `grill-me` y `harness-orchestrator` para este requerimiento..."*).*

No necesitas pasarle ninguna ruta ni copiar `AGENTS.md`.

### En Visual Studio Code (Copilot / Cline / Roo Code)
Para que VS Code también tenga el skill global disponible en todos tus repositorios sin pegar rutas cada vez:
* En **VS Code Settings (`settings.json` de Usuario)** o en **User Prompts (`%APPDATA%/Code/User/prompts/harness.instructions.md`)**, apunta una sola vez a la ruta absoluta donde hayas clonado el repositorio:
  `<HARNESS_HOME>/catalog/skills/harness-orchestrator/SKILL.md`

---

## 3. Estructura del Catálogo Central (`HARNESS_HOME`)

```text
ide-agnostic-harness/
├── README.md                                        # Documentación general
├── AGENTS.md                                        # Reglas base del Orquestador
├── .agents/                                         # Configuración nativa Antigravity
├── .github/                                         # Configuración nativa VS Code
└── catalog/
    ├── agents/
    │   └── orchestrator.md                          # Protocolo del Agente Orquestador (Tier 1)
    ├── skills/
    │   ├── grill-me/SKILL.md                        # Skill Global: Entrevista pre-planificación
    │   └── harness-orchestrator/SKILL.md            # Skill Global: Orquestador (docs/changelog + docs/tasks)
    └── subagents/
        ├── subagent-frontend.md                     # Perfil limpio UI / Frontend
        ├── subagent-backend.md                      # Perfil limpio API / Backend
        ├── subagent-db.md                           # Perfil limpio Base de Datos
        ├── subagent-qa.md                           # Perfil limpio Testing / QA
        └── subagent-devops.md                       # Perfil limpio Docker / CI / Despliegue
```

---

## 4. Resumen de las 5 Fases que Ejecuta el Skill Global `harness-orchestrator`

En cualquier proyecto donde lo invoques, el skill gestiona todo dentro de `docs/`:
1. **Fase 1 (`grill-me`):** Te hace preguntas breves de alineación antes de planificar.
2. **Fase 2 (`docs/changelog/changelog-<timestamp>.md` + Pausa Humana):** Escribe el archivo físico con el **modelo autor en cabecera**, el **qué**, el **porqué**, la **recomendación `Secuencial` vs `Paralela`** y la **lista de tareas (`- [ ]`) con el modelo LLM delegado**. **Detiene su turno** para que leas y edites el archivo físico `.md`.
3. **Fase 3 (Re-lectura post-OK):** Cuando le das el OK en el chat, vuelve a leer `docs/changelog/changelog-<timestamp>.md` para tomar tus ediciones manuales.
4. **Fase 4 (`docs/tasks/` + Subagentes Limpios):** Crea las subtareas efímeras en `docs/tasks/subtask-XX.md` y lanza los subagentes con contexto limpio hasta que marquen `- [x]` en el changelog.
5. **Fase 5 (Verificación y Limpieza):** Una vez que verifican juntos que todo se cumplió con éxito, **borra los archivos de `docs/tasks/`** para mantener economía total de tokens.
