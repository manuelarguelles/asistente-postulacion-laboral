# Asistente de Postulación Laboral

## Visión

Construir un agente que ayude a una persona a descubrir oportunidades laborales relevantes, entender los requisitos de cada puesto, evaluar el ajuste con su perfil y preparar materiales de postulación personalizados, manteniendo al usuario dentro del ciclo de decisión.

La primera versión no postulará automáticamente ni enviará información a terceros sin confirmación explícita.

## Problema

Buscar empleo implica revisar muchas ofertas, comparar requisitos, adaptar el CV y preparar respuestas repetitivas. El agente debe reducir trabajo operativo sin inventar experiencia, alterar datos personales ni enviar postulaciones a espaldas del usuario.

## Usuario inicial

Una persona que busca empleo y dispone de un CV, preferencias laborales y posiblemente varias versiones de su perfil profesional.

## Alcance propuesto para el MVP

1. Registrar preferencias de búsqueda: rol, seniority, ubicación, modalidad, salario y tecnologías.
2. Ingresar ofertas laborales mediante texto, URL o archivo autorizado por el usuario.
3. Extraer requisitos y separar requisitos obligatorios de deseables.
4. Comparar la oferta con el perfil del usuario y explicar fortalezas, brechas y nivel de ajuste.
5. Generar un borrador de CV adaptado y/o carta de presentación sin inventar información.
6. Mantener historial de ofertas, decisiones y estado de cada postulación.
7. Conversar con el usuario sobre una oferta mostrando la evidencia usada.

## Fuera de alcance inicial

- Postulación automática o envío de formularios sin confirmación por oferta.
- Acceso a cuentas personales de portales de empleo sin diseño de seguridad aprobado.
- Scraping masivo de sitios que lo prohíban.
- Automatización de postulaciones o acceso autenticado a portales; sí se reutilizará mediante un adaptador aislado su componente LaTeX aprobado.
- Reutilización silenciosa de datos, prompts o credenciales de proyectos anteriores.

## Principios del agente

- Veracidad: no inventar experiencia, títulos, certificaciones ni logros.
- Trazabilidad: distinguir datos del usuario, requisitos de la oferta e inferencias.
- Control humano: toda acción externa requiere confirmación explícita.
- Privacidad: minimizar y proteger CVs, datos de contacto y documentos.
- Explicabilidad: justificar el puntaje o recomendación con criterios visibles.
- Reversibilidad: permitir editar, descartar y recuperar borradores.

## Stack aprobado — local primero, Railway después

El stack inicial será un monolito modular Python/FastAPI por su encaje con LaTeX y el tiempo disponible. Se podrá separar el worker cuando el procesamiento asíncrono lo justifique. La especificación y el plan aprobados están en `docs/SPEC.md` y `docs/IMPLEMENTATION-PLAN.md`.

### Aplicación

- **FastAPI + Jinja2 + HTMX**: aplicación web y UI progresiva.
- **SQLAlchemy + Alembic**: modelo, acceso y migraciones PostgreSQL.
- **Adaptadores configurables** para IA, extracción, fuentes y LaTeX/tectonic.

### Datos y archivos

- **PostgreSQL administrado por Railway**: usuarios, perfiles, ofertas, análisis, borradores y auditoría.
- **SQLAlchemy/Alembic**: esquema, migraciones y acceso tipado; migraciones ejecutadas antes del despliegue.
- **Railway Storage Bucket compatible con S3**: CVs y documentos; usar URLs prefirmadas y no pasar archivos grandes por el servidor web.
- **Redis administrado por Railway, solo cuando sea necesario**: cola de trabajos, rate limiting y tareas asíncronas.

### Procesamiento y despliegue

- **Servicio web Railway**: FastAPI, health check y `PORT` proporcionado por Railway.
- **Worker Railway opcional**: mismo repositorio, proceso separado para extracción de documentos, generación de borradores y tareas largas.
- **Dockerfile si necesitamos un entorno reproducible para tectonic/OCR**.
- **GitHub autodeploy + ambientes staging/production**.

### Observabilidad y seguridad

- Logs estructurados y endpoint `/api/health`.
- Variables secretas exclusivamente en Railway; nunca en Git ni en `NEXT_PUBLIC_*`.
- Auth gestionada por la aplicación/proveedor elegido en discovery, con autorización por usuario.
- Retención mínima de documentos, eliminación/exportación de datos y auditoría de acciones.

### Arquitectura inicial

```text
Navegador
   │
   ▼
Next.js web + Route Handlers ───► PostgreSQL (Railway)
   │                                      │
   ├──► LLM provider vía AI SDK           └── Prisma migrations
   ├──► S3-compatible Bucket (documentos)
   └──► Redis + Worker Railway (fase posterior)
```

La elección se basa en que Railway documenta despliegues directos de Next.js con PostgreSQL, variables referenciadas entre servicios, migraciones pre-deploy, Redis, workers y buckets. [Guía oficial Next.js + Postgres](https://docs.railway.com/guides/nextjs) · [Guía oficial full-stack](https://docs.railway.com/guides/fullstack-nextjs)

## Entregable inicial

- Repositorio limpio y privado.
- Aplicación web funcional.
- Agente conversacional con herramientas acotadas.
- Flujo de análisis de oferta y preparación de borradores.
- Documentación de seguridad, límites y decisiones.

## Enlaces

- Repositorio: pendiente de publicación.
- Demo: pendiente.
