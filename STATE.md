# State — 2026-09-08

## Current Phase

Fase 0 — kickoff y discovery.

## Current Task

Crear un repositorio limpio para un agente nuevo de asistencia en postulaciones laborales.

## Decisions Made

- Proyecto independiente de `auto-postulacion-cvs`.
- No se importará código, memoria, prompts, datos ni credenciales del proyecto anterior.
- El agente preparará y analizará postulaciones, pero no enviará acciones externas sin confirmación.
- Nombre de trabajo: `asistente-postulacion-laboral`.
- Repositorio: público en GitHub (`manuelarguelles/asistente-postulacion-laboral`).
- Stack inicial propuesto: Next.js + TypeScript + Tailwind + Zod + Vercel AI SDK, PostgreSQL + Prisma, Railway Storage Bucket y Redis/worker solo cuando el MVP lo requiera.
- Despliegue objetivo: Railway con servicio web, migraciones pre-deploy, health check y ambientes staging/production.

## Blockers

- Faltan decisiones de stack, proveedor cloud y fuentes de ofertas.
- Faltan criterios concretos para el score de ajuste.
- Falta confirmar proveedor LLM, autenticación y política de almacenamiento de documentos.

## Next Action

Responder las preguntas de `docs/BRIEF.md` y cerrar el diseño del MVP.
