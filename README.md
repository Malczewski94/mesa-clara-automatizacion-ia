# Mesa Clara | Automatización de soporte con IA

**Flujo principal probado y activo cada seis horas. La entrega conserva brechas explícitas frente a la rúbrica.**

Make + Notion + OpenAI GPT-5 nano + Gmail. Un ticket recupera conocimiento, genera un borrador, avisa al responsable y espera aprobación humana antes de enviar. Caso ficticio de soporte SaaS.

## Documentación de entrega

- [PDF: arquitectura y manual operativo](docs/Mesa_Clara_Arquitectura_y_Manual.pdf)
- [Blueprint original: recepción](workflows/01_recepcion.blueprint.json)
- [Blueprint original: envío aprobado](workflows/02_envio.blueprint.json)
- [Panel ejecutivo público — solo lectura](https://wobbly-muse-d95.notion.site/Panel-ejecutivo-Mesa-Clara-413a709292e981f9887feff8e745cb49)
- [Capturas reales de escenarios y ejecuciones](evidence/capturas/)
- [Video documental de 3 minutos](video/Mesa_Clara_Recorrido_Documental_3min.mp4) — sin audio; no es una grabación en vivo de Make.
- [Pruebas](tests/resultados.csv), [verificación de T02](evidence/T02_envio_verificado.md) y [cierre operativo](evidence/CIERRE_PUBLICO.md).
- [Diccionario de datos](docs/diccionario_datos.md), [esquema Notion](docs/esquema_notion.json) y [contratos JSON](contracts/).

## Panel público y evidencias

El panel se comprobó sin iniciar sesión: seis registros visibles, distribuidos en tres Correcto, dos Bloqueado y un Error. La tasa de error es 1/6 (16,7 %); Notion muestra el promedio redondeado como 0,17. Las tablas y el cálculo sustituyen los gráficos sujetos al límite del plan gratuito. Incluye un fallo inducido de prueba y cobertura parcial; no son métricas de producción.

La ejecución incompleta de T06 se retiró de la cola después de documentarla. Make confirmó la cola vacía y la desaparición del aviso de bloqueo. El historial y el registro de error permanecen disponibles.

## Resultado verificado

Se observaron seis ejecuciones de recepción, incluidas consultas incompletas, instrucción maliciosa y error de validación inducido. T02 completó el envío el 9/11/2026 a las 13:22 Argentina: correo con texto exacto aprobado, fecha e hilo en Notion y registro Correcto. Una segunda ejecución no generó otro correo.

E03 (versiones diferentes) y E05 (rechazo) quedaron sin fecha/hilo y no se encontraron nuevas respuestas después del ensayo adicional. La inspección individual de sus filtros fue inconcluyente: se documentan como verificación parcial, no como pruebas plenamente auditadas.

Los dos escenarios quedaron **Active / Every 6 hours**. Frecuencia elegida para limitar sondeos: aproximadamente 240 consultas mensuales entre ambos, más consumo de procesamiento e IA. No es un SLA de atención inmediata. No se compraron créditos ni se activaron recargas.

## Alcance y limitaciones

- Incorporar al repositorio el video actualizado de tres minutos con capturas reales. Ya está generado; el archivo enlazado arriba es el recorrido documental anterior.
- Completar contingencias para todos los módulos de Notion/Gmail y verificar individualmente E03/E05.
- No se usaron Omni AI, Claude ni Batch API. La estrategia de costos distingue propuestas de consumo real; el 50 % de Batches no se declara ahorro medido.
- Simple text prompt no expuso Max Tokens. No hay deduplicación global por Mensaje ID ni garantía de entrega exactamente una vez.

## Operación e importación

[Instrucciones](workflows/LEER_ANTES_DE_IMPORTAR.md). Los blueprints originales se preservan sin alterar la lógica. Se exportaron antes del ajuste final de programación; [configuración operativa](workflows/configuracion_operativa.json) documenta el horario vigente. En otra cuenta hay que reasignar conexiones, bases y propiedades.

[Recepción en Make](https://us2.make.com/2933793/scenarios/6962342/edit) · [Envío en Make](https://us2.make.com/2933793/scenarios/6963384/edit) · [Base del proyecto](https://app.notion.com/p/413a709292e9810ba33edfab203ab1a7)

El panel muestra métricas sobre registros parciales de demostración, con errores inducidos. No representan resultados de producción. Ningún entregable contiene claves de API ni contraseñas identificadas en la revisión.
