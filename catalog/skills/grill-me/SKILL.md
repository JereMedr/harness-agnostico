---
name: grill-me
description: >-
  Entrevista técnica y funcional interactiva para alinear requerimientos, reglas de negocio,
  arquitectura y casos borde con el desarrollador ANTES de generar el documento PROCEED.md
  o crear tareas task-XX.md. Úsala siempre al inicio de un proyecto o requerimiento nuevo.
---

# Skill: Entrevista de Alineación Pre-Planificación (`grill-me`)

## Propósito
Evitar que el Agente Orquestador asuma requerimientos o cree tareas (`task-XX.md`) prematuramente. Antes de escribir un plan o código, el Orquestador interroga de forma estructurada y concisa al desarrollador hasta despejar todas las decisiones clave.

## Reglas de Ejecución
1. **Cero Creación Prematura:** Mientras estés ejecutando `grill-me`, tienes **PROHIBIDO** crear archivos de código o boletos `tasks/task-XX.md`.
2. **Uso de Preguntas Interactivas:**
   - **En Antigravity:** Utiliza la herramienta nativa `ask_question` con opciones claras (marcando la opción recomendada con `(Recommended)`) o sugiere el comando `/grill-me`.
   - **En Cursor / VS Code:** Formula entre 3 y 5 preguntas numeradas de opción múltiple cortas y directas en el chat.
3. **Dimensiones Obligatorias a Indagar:**
   - **Reglas de Negocio y Flujos Críticos:** ¿Qué hace exactamente cada rol o módulo en los casos borde?
   - **Persistencia y Contratos de Datos:** ¿Qué entidades, estados y validaciones son obligatorios?
   - **Alcance del Sprint / Iteración:** ¿Qué entra en este lote de tareas y qué queda para después?
4. **Transición al Documento `.proceed`:**
   - Solo cuando el desarrollador responda las preguntas de `grill-me`, genera el documento `PROCEED.md` (y el Artifact con `RequestFeedback: true` en Antigravity) con la propuesta de tareas y la selección de modelos LLM.
