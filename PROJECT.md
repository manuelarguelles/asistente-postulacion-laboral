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
- Uso o importación de `auto-postulacion-cvs`.
- Reutilización silenciosa de datos, prompts o credenciales de proyectos anteriores.

## Principios del agente

- Veracidad: no inventar experiencia, títulos, certificaciones ni logros.
- Trazabilidad: distinguir datos del usuario, requisitos de la oferta e inferencias.
- Control humano: toda acción externa requiere confirmación explícita.
- Privacidad: minimizar y proteger CVs, datos de contacto y documentos.
- Explicabilidad: justificar el puntaje o recomendación con criterios visibles.
- Reversibilidad: permitir editar, descartar y recuperar borradores.

## Stack

Pendiente de decisión durante discovery. La plataforma objetivo será cloud y el stack se elegirá según el MVP, el tiempo disponible y el costo operativo.

## Entregable inicial

- Repositorio limpio y privado.
- Aplicación web funcional.
- Agente conversacional con herramientas acotadas.
- Flujo de análisis de oferta y preparación de borradores.
- Documentación de seguridad, límites y decisiones.

## Enlaces

- Repositorio: pendiente de publicación.
- Demo: pendiente.
