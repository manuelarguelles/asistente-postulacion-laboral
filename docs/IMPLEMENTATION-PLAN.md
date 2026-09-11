# Plan de implementación — Chambas MVP

## Forma de trabajo

Implementación incremental con TDD. Cada fase termina con pruebas ejecutables, documentación actualizada y revisión independiente. No se automatizan postulaciones ni se envían datos a portales.

## Fase 0 — Preparación y baseline

- Aislar código legado y crear entorno FastAPI, configuración tipada, `.env.example`, logging seguro y health check.
- Configurar PostgreSQL local, Alembic y almacenamiento local abstracto.
- Definir contratos para IA, extracción, fuentes y LaTeX.
- Verificar que la aplicación arranca y pasa el health check.

## Fase 1 — Identidad, aprobación y seguridad

- Google OAuth, sesiones seguras, rol administrador y estados pendiente/aprobada/suspendida/eliminada.
- Pantallas y registro versionado de términos, privacidad y consentimiento de IA.
- Panel admin mínimo para aprobar, suspender y consultar auditoría.
- Cifrado de campos sensibles, minimización de logs y autorización por propietario.
- Tests de autenticación, autorización, consentimiento y acceso cruzado.

## Fase 2 — Perfil y documentos

- Modelar usuario, perfil, CV original, archivo, versión derivada y proceso.
- Validar PDF, MIME real, tamaño y contenido potencialmente malicioso.
- Extraer texto nativo; activar OCR por baja calidad; mostrar formulario editable.
- Implementar límites de CV y eliminación/exportación.
- Tests de PDF válido, escaneado, corrupto y límites.

## Fase 3 — Convocatorias multimodales

- Entrada de URL, texto e imagen, permitiendo combinaciones.
- Lector HTTP seguro para GetOnBoard/LinkedIn públicos: timeouts, redirects controlados, SSRF protection y límites.
- OCR + visión para imágenes; normalización de requisitos; detección de conflictos.
- Revisión y confirmación antes del análisis.
- Tests de URL accesible/bloqueada, texto+imagen, conflicto y fuentes insuficientes.

## Fase 4 — Análisis y conversación

- Adaptador configurable de IA y salida estructurada validada.
- Resumen, tabla cumple/parcial/no evidenciado y brechas con evidencia.
- Preguntas por brechas críticas, incertidumbre explícita y prohibición de invenciones.
- Chat limitado al perfil, convocatoria y resultado actual.
- Rate limit por usuario/IP/operación/estado; HTTP 429.
- Tests deterministas, fallos de proveedor, timeout, reintentos y abuso.

## Fase 5 — CV LaTeX y revisión

- Inspeccionar el adaptador mínimo de `projects/auto-postulacion-cvs`.
- Reutilizar plantillas y datos compatibles mediante interfaz aislada.
- Generar LaTeX, compilar con `tectonic` en entorno controlado y capturar errores.
- Selección de plantilla, nombre de versión, edición y máximo de tres iteraciones.
- Tests de compilación, caracteres especiales, datos faltantes y PDF final.

## Fase 6 — Integración y endurecimiento

- Completar E2E registro → PDF.
- Revisar teclado, foco, contraste, labels, errores y responsive móvil.
- Tests de CSRF, SSRF, subida de archivos, autorización, secretos y rate limit.
- Retención automática de 30 días, borrado relacionado y exportación.
- Evaluar abuso, falsos positivos y revisión humana.

## Fase 7 — Railway y entrega

- Configurar Railway, variables, PostgreSQL, almacenamiento, migraciones, health check y staging privado.
- Conectar `chambas.analizodatos.com` y ejecutar smoke tests sin datos reales.
- Documentar instalación, arquitectura, seguridad, límites y demo reproducible.

## Verificación por entrega

Formateo/lint → unit tests → integración PostgreSQL → E2E → auditoría de seguridad → smoke test staging. Registrar comandos y resultados en `ARTIFACT.md`; registrar observaciones independientes en `VERDICT.md`.
