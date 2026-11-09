# Mesa Clara - Ecosistema de soporte con IA

**Estado: implementación parcial verificada. No entregar todavía como final completo.**

Stack: Make + Notion + OpenAI GPT-5 nano (Simple text prompt de Make) + Gmail. Caso ficticio de soporte SaaS: un ticket consulta artículos vigentes, genera borrador, notifica al responsable y debe esperar aprobación antes del envío final.

## Implementado y verificado

- Base relacional en Notion: Clientes demo, Conocimiento, Tickets, Ejecuciones y Configuracion.
- Escenario de recepción con filtros, GPT, borrador, aviso Gmail y registro.
- Seis ejecuciones de recepción, incluidas consultas incompletas e instrucción maliciosa.
- Error de validación inducido en el módulo IA registrado automáticamente; Break ejecutado.
- Escenario emisor creado; sin aprobaciones dejó pasar cero tickets.
- T02 completado: aprobación humana, correo enviado con el texto exacto, fecha/hilo guardados y registro Correcto. [Verificación](evidence/T02_envio_verificado.md).
- Dashboard interno: tasa de errores sobre registros terminados y tablero de resultados.

## Archivos

- `docs/Mesa_Clara_Arquitectura_y_Manual.pdf`: arquitectura, modelo, costos, seguridad, pruebas y brechas.
- [Blueprint original de recepción](workflows/01_recepcion.blueprint.json) y [blueprint original de envío](workflows/02_envio.blueprint.json): exportados de Make y aportados por el usuario; JSON y mapeos revisados. [Instrucciones de importación](workflows/LEER_ANTES_DE_IMPORTAR.md).
- `tests/resultados.csv`: resultados observados y pruebas pendientes.
- `tests/aprobacion_T02.json`: aprobación textual del caso de demostración.
- `docs/guion_video.md`: guion; no sustituye el video.
- `evidence/ESTADO.md`: capturas a recuperar; no se fabricaron evidencias.
- `enlaces.json`: destinos reales y entregables aún sin enlace.

## Repositorio de entrega

https://github.com/Malczewski94/mesa-clara-automatizacion-ia

[Ver PDF de arquitectura y manual](docs/Mesa_Clara_Arquitectura_y_Manual.pdf) · [Pruebas](tests/resultados.csv) · [Lógica del flujo](workflows/)

## Enlaces de trabajo

Notion: https://app.notion.com/p/413a709292e9810ba33edfab203ab1a7

Recepción: https://us2.make.com/2933793/scenarios/6962342/edit

Envío: https://us2.make.com/2933793/scenarios/6963384/edit

Requieren acceso a las cuentas. No se verificó publicación de solo lectura.

## Pendientes antes de la entrega

1. Incorporar al PDF y anexos la verificación de T02 del 9/11 a las 13:22; el envío ya está confirmado.
2. Probar versión obsoleta y rechazo. La segunda ejecución de T02 ya se verificó sin correo duplicado. Completar rutas para fallos de Notion/Gmail previos al envío y fallos del registro posterior.
3. Incorporar capturas reales: los dos blueprints originales ya están publicados.
4. Publicar dashboard sin correo personal ni datos sensibles; verificar acceso anónimo.
5. Incorporar las evidencias visuales finales al completar las verificaciones.
6. Grabar demo de 3 minutos y activar programación dentro del presupuesto gratuito.

## Límites explícitos de la rúbrica

No se ejecutaron Claude ni Batch API ni Omni AI. El 50% de Batches es una comparación de tarifas para una extensión propuesta, no ahorro medido. Simple text prompt no mostró Max Tokens; 180 palabras es una instrucción, no un límite duro. No hay deduplicación global por Mensaje ID. El modelo relacional se generó mediante IA en Notion. El camino aprobado del emisor está verificado; faltan casos adicionales de bloqueo y evidencia visual.

## Anexos técnicos actualizados

- `docs/esquema_notion.json`: esquema leído de las cinco bases reales, sin registros personales.
- `docs/diccionario_datos.md`: tipos, relaciones y límites de validación.
- `contracts/`: estructuras JSON y mapeos documentados; no son evidencias de ejecución.
- `docs/cierre_entrega.md`: orden de cierre y criterios para declarar cada entregable completo.
