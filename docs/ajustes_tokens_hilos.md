# Configuración de IA y continuidad de conversaciones

## Decisión de entrega
Se conserva GPT-5 nano mediante **Simple text prompt**, con la conexión integrada de Make. No se compra saldo de OpenAI ni se activa recarga automática. La conexión propia de OpenAI no participa del flujo activo.

Esta decisión prioriza la continuidad del piloto con los créditos disponibles en Make. La operación depende de esos créditos y de la vigencia de las conexiones Notion y Gmail; no se promete disponibilidad ilimitada.

## Límite de tokens: configuración ensayada
El 9 de noviembre de 2026 a las 19:42 (Argentina) se ejecutó únicamente un módulo aislado Generate a response con estos parámetros:

| Parámetro | Valor |
|---|---|
| Modelo | gpt-5-nano |
| Max Output Tokens | 1200 |
| Reasoning effort | minimal |
| Store | false |
| Create a new conversation | false |
| Prompt | Comprobación técnica sin datos de clientes |

La conexión renovada pasó Verify, pero la generación devolvió **429: You have no credits remaining**. No se generó texto ni se enviaron correos. Se descartaron los cambios del editor y se conservó la recepción original activa, sin ejecuciones incompletas.

[Historial de la prueba en Make](https://us2.make.com/2933793/scenarios/6962342/logs/719adaed5c504a22a1bad01bf17a5901). Requiere acceso a la cuenta.

**Alcance:** la entrada de la ejecución demuestra el valor configurado. No prueba una generación exitosa con ese máximo ni su aplicación en la versión activa. Simple text prompt no expone ese control en la configuración utilizada. El pedido de hasta 180 palabras en el prompt no sustituye un tope técnico de tokens.

## Conversaciones Gmail
Implementado y probado:
- Thread ID vacío: Send an email crea un correo.
- Thread ID presente: Reply to an email responde dentro del hilo leído de Notion.
- Ambas rutas conservan texto aprobado, destinatario del cliente, fecha, estado y registro de resultado.
- Se mantienen los filtros de aprobación, versión y envío previo, y Break sin reenvío automático ante fallo Gmail.

E07 conservó el hilo original; E08 creó uno nuevo. La segunda ejecución no duplicó mensajes. [Evidencia](../evidence/E07_E08_hilos.md).

Cada continuación se registra como un ticket nuevo con su aprobación y el hilo existente. No se elimina la fecha de un ticket enviado para forzar otro envío.

## Correspondencia con la consigna
La integración de OpenAI y el flujo operativo están demostrados. El requisito de configurar Max Tokens en la generación activa queda como limitación declarada de esta entrega sin compras adicionales. No se presenta el ensayo fallido como cumplimiento completo.

## Referencias
- [Módulos OpenAI de Make](https://apps.make.com/openai-modules)
- [Módulos Gmail de Make](https://apps.make.com/gmail-modules)
