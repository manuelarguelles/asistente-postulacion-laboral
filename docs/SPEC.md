# Especificación aprobada — Chambas

**Dominio:** `chambas.analizodatos.com`  
**Estado:** aprobada por Manuel el 2026-09-10  
**MVP:** adaptación de CV a convocatorias laborales

## Objetivo

Permitir que cualquier persona cargue un CV PDF y una convocatoria mediante URL, texto, imagen o combinación. El sistema extrae y confirma la información, analiza coincidencias y brechas, permite iterar y genera un CV adaptado en PDF usando la solución LaTeX existente.

## Alcance del MVP

- Google OAuth, aprobación manual de nuevos usuarios y uso restringido mientras esperan.
- Un perfil por usuario, hasta tres CV originales y múltiples CV derivados por convocatoria.
- Extracción de texto nativo + OCR cuando sea necesario + formulario editable de revisión.
- URLs públicas de GetOnBoard y LinkedIn cuando sea posible; texto e imagen complementarios.
- OCR + visión para imágenes y confirmación ante conflictos entre fuentes.
- Resumen y tabla de requisitos: cumple, parcial o no evidenciado.
- Preguntas por brechas críticas; nunca inventar experiencia, títulos o competencias.
- Iteración mediante chat acotado y edición directa.
- Plantilla LaTeX seleccionable y salida PDF; idioma igual al de la convocatoria.
- Retención inicial de 30 días, exportación y eliminación.

Carta de presentación, entrevistas y Playwright/CDP con perfil LinkedIn quedan fuera del MVP.

## Arquitectura

Monolito Python/FastAPI con Jinja2, HTMX y CSS/Tailwind ligero; SQLAlchemy + PostgreSQL; tareas en segundo plano para extracción, OCR/visión y compilación. El proveedor/modelo de IA será configurable: objetivo inicial DeepSeek V4 Flash si está disponible, con fallback. Un adaptador aislado reutilizará plantillas y `tectonic` de `auto-postulacion-cvs`, sin copiar el proyecto completo.

Desarrollo local con PostgreSQL y almacenamiento local; despliegue posterior en Railway con PostgreSQL administrado y almacenamiento persistente u object storage.

## Seguridad, privacidad y abuso

- Datos clasificados por sensibilidad; CV, contacto, ubicación e historial son personales/sensibles.
- TLS, cifrado en reposo y campos sensibles cifrados con AEAD; claves fuera de la base.
- Logs con IDs pseudonimizados; nunca CVs, prompts o respuestas completas.
- Consentimiento versionado para tratar datos y enviarlos a proveedores/modelos de IA.
- Términos contra suplantación, falsificación, fraude, spam, scraping no autorizado y automatización abusiva.
- Detección progresiva: advertencia, limitación temporal, bloqueo y revisión; ningún bloqueo permanente solo por automatización.
- Objetivo WCAG 2.2 AA y diseño móvil accesible.

## Límites iniciales

Pendientes: 2 análisis diarios. Aprobados: 10. Hasta 3 iteraciones por proceso y 3 CV originales por usuario. Límites separados para archivos, URLs, OCR/visión y LaTeX; límites por usuario/IP; HTTP 429 con reintento y auditoría de consumo.

## Aceptación

Debe funcionar localmente el flujo: registro → aprobación → cargar CV → extraer/revisar → ingresar convocatoria → resolver conflictos → analizar → iterar → compilar → descargar PDF. Se cubrirán errores de extracción, OCR, URL bloqueada, datos faltantes, rate limit y compilación.
