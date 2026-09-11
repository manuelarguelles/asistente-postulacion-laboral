# State — 2026-09-10

## Current Phase

Fase 0 completada — diseño aprobado; listo para implementación.

## Current Task

Implementar el MVP de Chambas (`chambas.analizodatos.com`).

## Decisions Made

- Proyecto independiente de `auto-postulacion-cvs`.
- No se importará código, memoria, prompts, datos ni credenciales del proyecto anterior.
- El agente preparará y analizará postulaciones, pero no enviará acciones externas sin confirmación.
- Nombre de trabajo: `asistente-postulacion-laboral`.
- Repositorio: público en GitHub (`manuelarguelles/asistente-postulacion-laboral`).
- Stack aprobado: monolito Python/FastAPI + Jinja2/HTMX + SQLAlchemy/Alembic + PostgreSQL.
- IA: DeepSeek V4 Flash si está disponible, mediante adaptador configurable y fallback.
- CV: texto nativo + OCR + revisión editable; convocatorias URL/texto/imagen combinables.
- LaTeX: adaptador aislado reutilizando `auto-postulacion-cvs` y `tectonic`.
- Local primero; Railway después; rate limiting, abuso, consentimiento, cifrado, retención y WCAG incluidos.

## Blockers

- Falta ejecutar el plan de implementación.

## Next Action

Iniciar Fase 0 del plan en `docs/IMPLEMENTATION-PLAN.md`.
