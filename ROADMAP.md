# Roadmap

## Fase 0 — Kickoff y discovery [✅]

- Especificación aprobada para `chambas.analizodatos.com`.
- Monolito Python/FastAPI, PostgreSQL local → Railway y adaptador LaTeX definidos.
- Rate limiting, seguridad, consentimiento, abuso y accesibilidad incluidos.

## Fase 1 — Baseline e identidad [🔄]

- FastAPI, configuración, health check, PostgreSQL/Alembic y almacenamiento abstracto.
- Google OAuth, aprobación manual, consentimiento versionado y rol administrador.
- Cifrado, autorización, logs seguros y auditoría.

## Fase 2 — Perfil, documentos y convocatorias [⏳]

- PDF nativo/OCR/revisión editable.
- URL, texto e imagen combinables; extracción segura y conflictos visibles.
- Perfil y hasta tres CV originales; retención, exportación y borrado.

## Fase 3 — Análisis y CV LaTeX [⏳]

- Análisis de coincidencias/brechas con IA configurable.
- Chat acotado, preguntas de brechas y rate limiting.
- Adaptador `auto-postulacion-cvs`/`tectonic`, iteración y PDF.

## Fase 4 — Verificación y entrega [⏳]

- Tests unitarios, integración y E2E; accesibilidad y seguridad.
- Detección de abuso y revisión humana.
- Railway, staging privado, dominio, smoke tests y documentación.

## Recorte de emergencia

Si el tiempo es limitado, entregar solo: Google OAuth/aprobación, un CV PDF, una convocatoria URL/texto/imagen, análisis y PDF LaTeX revisable. No incluir cartas, entrevistas ni automatización de portales.
