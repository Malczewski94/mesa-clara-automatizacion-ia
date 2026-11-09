# Rechazo y versión obsoleta

Prueba controlada del 9 de noviembre de 2026, 16:25:57 (Argentina).

## Preparación

Se actualizaron los dos registros de prueba para que el disparador de modificaciones los detectara. No se alteraron sus condiciones de aprobación:

- E03: Estado Aprobado, Version 2 y Version aprobada 1. Debe detenerse en la validación de aprobación vigente.
- E05: Estado Rechazado, versiones 1 y 1. Debe detenerse en Solo aprobaciones.

Ambos conservaron fecha de envío e hilo vacíos después de la prueba.

## Registro observado en Make

| Paso | Evento |
|---|---|
| Detectar cambios de aprobación | Operación completada |
| Releer ticket antes de enviar | Una entrada no pasó el filtro |
| Releer ticket antes de enviar | Una operación completada |
| Leer cliente relacionado | La entrada no pasó el filtro |
| Gmail | Sin operación de envío en el registro |

Total: **dos operaciones y dos créditos**. La consulta de Gmail por los textos distintivos de ensayo no encontró mensajes enviados. El estado y las versiones se comprobaron además por lectura directa de Notion.

La secuencia confirma los bloqueos esperados para los dos casos controlados: E05 no satisface el primer filtro y E03 no satisface la igualdad numérica de versiones después de releer el ticket. No es una garantía universal frente a concurrencia o cambios externos entre operaciones.

Los números junto al nombre de los módulos son sus identificadores, no cantidades de operaciones. Para esta comprobación se utilizó el registro Simple log y el total del encabezado.
