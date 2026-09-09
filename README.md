# Asistente de Postulación Laboral

Agente nuevo, independiente y construido desde cero para ayudar a una persona a organizar, evaluar y preparar postulaciones laborales de manera responsable.

## Estado

Proyecto recién iniciado. La visión, el alcance inicial y las preguntas abiertas están en [PROJECT.md](PROJECT.md).

## Regla de independencia

Este repositorio no reutiliza código, prompts, credenciales, datos, memoria ni decisiones de `auto-postulacion-cvs`. Cualquier componente compartido deberá diseñarse y documentarse explícitamente en este proyecto.

## Documentación

- [PROJECT.md](PROJECT.md): visión, usuarios, límites y decisiones iniciales.
- [ROADMAP.md](ROADMAP.md): plan por fases para el MVP.
- [STATE.md](STATE.md): estado actual y siguiente acción.
- [docs/BRIEF.md](docs/BRIEF.md): brief de descubrimiento y preguntas abiertas.

## Seguridad inicial

- No incluir CVs reales, documentos personales, tokens ni credenciales en Git.
- Usar `.env` local con permisos `600` cuando se agreguen secretos.
- Toda acción externa —por ejemplo, enviar una postulación— deberá requerir confirmación explícita.
