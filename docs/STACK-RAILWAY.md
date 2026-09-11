# Stack y despliegue Railway

## Decisión

Empezar con un servicio web Next.js y PostgreSQL. Mantener Redis, worker y bucket como componentes activables por necesidad, no como requisitos del primer commit funcional.

## Servicios Railway

### 1. Web

- Fuente: repositorio GitHub, rama `main` después de integrar la rama de documentación.
- Runtime: Node.js detectado por Railpack.
- Producción: `next build` y servidor standalone.
- Variables: `DATABASE_URL`, `AUTH_SECRET`, credenciales del proveedor LLM y variables del bucket.
- Health check: `/api/health`.

### 2. PostgreSQL

- Fuente de verdad transaccional para perfiles, ofertas, análisis y borradores.
- `DATABASE_URL` se consume mediante una variable referenciada desde el servicio web.
- Migraciones: `npx prisma migrate deploy` como pre-deploy command.

### 3. Bucket S3-compatible

- CVs y documentos se suben directamente con URLs prefirmadas.
- El backend nunca debe registrar el contenido completo de un documento en logs.
- Las claves deben usar identificadores internos, no correos ni nombres completos.

### 4. Redis + Worker — fase posterior

- Activar cuando extracción, parsing o generación excedan el tiempo de una petición web.
- Cola con BullMQ; el worker usa el mismo repositorio y variables privadas.
- El worker no requiere dominio público.

## Reglas Railway

- Escuchar en `0.0.0.0` y usar `PORT` de Railway.
- No hardcodear `localhost` para servicios cloud.
- No exponer secretos con prefijo `NEXT_PUBLIC_`.
- Separar staging y production.
- Probar cada migración en staging antes de production.

## Orden de implementación

1. Next.js + health check + una pantalla mínima.
2. PostgreSQL + Prisma + migración inicial.
3. Perfil y carga manual de oferta.
4. Integración LLM con salida estructurada y citas de evidencia.
5. Bucket para documentos.
6. Redis/worker solo si una prueba de carga o el flujo de documentos lo exige.
