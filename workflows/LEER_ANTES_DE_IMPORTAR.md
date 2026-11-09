# Blueprints originales de Make

Los archivos de entrega son:

- [01_recepcion.blueprint.json](01_recepcion.blueprint.json): exportación original aportada por el usuario.
- [02_envio.blueprint.json](02_envio.blueprint.json): exportación original aportada por el usuario.

Se conservaron sus bytes y lógica. Los archivos con `_reconstruido` en el nombre son versiones preliminares, no deben usarse para la entrega ni importarse en lugar de los originales.

Validación: ambos JSON se pueden interpretar; se revisaron módulos, filtros, rutas de error y mapeos. No se encontraron correos personales ni claves en texto plano. Los IDs de conexiones son referencias de Make, no credenciales; las credenciales no se transfieren mediante estos archivos.

## Importación en otra cuenta

1. Importar cada blueprint en un escenario nuevo; no sobrescribir los escenarios de demostración.
2. Elegir conexiones propias de Notion y Gmail.
3. Sustituir IDs de bases/páginas de Notion si se replica la base y refrescar el esquema y los identificadores de propiedades.
4. Comprobar el disparador efectivo: recepción `select=create`; envío `select=update`. El label de restauración visual del emisor dice created time, pero el parámetro efectivo es update.
5. Establecer el punto de inicio sin consumir registros históricos y revisar destinatarios antes de probar.
6. Mantener la programación desactivada hasta terminar las verificaciones.

T02 ya completó el camino aprobado y una segunda ejecución no duplicó el correo. La importación en otra cuenta no fue probada. Los IDs de infraestructura son fijos del entorno; los datos del ticket, destinatario, borrador y texto aprobado son dinámicos.

SHA-256 de los adjuntos originales:

- Recepción: `adf0de0da42387bafea870ed8e4f6bc16fd1d11fcb4b7c9f97d7740f23f0c8ac`
- Envío: `7631db70b231f0f920dc8981de4e6b65627bf94871af8cc98742f21e0e44e6ea`

Limitaciones vigentes: sin tope duro Max Tokens, deduplicación global ni contingencias en todos los módulos. Las capturas, panel público, video y actualización del PDF siguen pendientes.
