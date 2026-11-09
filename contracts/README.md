# Contratos de transferencia

Estos JSON documentan estructuras y mapeos. No son exportaciones de ejecuciones ni solicitudes listas para enviar: los valores {{...}} deben resolverse en Make. No incluyen credenciales ni direcciones personales.

| Archivo | Integración | Uso |
| --- | --- | --- |
| consulta_conocimiento.request.json | Notion POST database/query | Solo artículos Vigente=true; máximo 10 |
| guardar_borrador.request.json | Notion PATCH page | Resultado y modelo de Simple text prompt |
| registrar_error.request.json | Notion POST pages | Ejemplo parametrizado de registro relacionado |
| gmail_envio.mapping.json | Make Gmail | Mapeo de entrada y threadId de salida |

La IA devuelve texto en result y nombre del modelo en model. No devuelve JSON estructurado validado. Los ejemplos de Notion usan el contrato legado 2022-06-28 utilizado por el escenario; migrar a data sources requiere revisar endpoints y mappings.

La igualdad de versiones, el estado aprobado, la fecha de aprobación y la ausencia de fecha de envío se comprueban en filtros del emisor, no en estos JSON. Si Gmail envía pero falla el guardado posterior, conciliar el correo antes de reintentar: el registro no es una transacción atómica.
