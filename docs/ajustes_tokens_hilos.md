# Ajustes de tokens y conversación

Estado: Gmail implementado y probado; límite técnico de tokens bloqueado por falta de créditos en la API.

## Avance comprobado
- OpenAI: la clave renovada pasó Verify. El 9 de noviembre a las 19:42 (Argentina) se probó un módulo aislado con GPT-5 nano, Max Output Tokens = 1200, esfuerzo mínimo, Store = false y sin crear conversación. La API devolvió `[429] You have no credits remaining`. No generó texto ni envió correos. Se descartó el módulo de prueba sin cambiar el flujo activo.
- Gmail: el blueprint fue importado, guardado, reabierto y probado en Make. E07 respondió dentro del hilo original; E08 creó un correo nuevo; la reejecución no duplicó mensajes. [Evidencia](../evidence/E07_E08_hilos.md).
- Para completar la prueba hace falta crédito disponible en la API. La clave ya es válida. No se compró saldo ni se activó recarga automática.

## Límite técnico de generación
El módulo Simple text prompt actual no expone Max Output Tokens. Limitar el prompt a 180 palabras no configura un tope técnico.
Cambio previsto: OpenAI Generate a response con conexión propia, GPT-5 nano, Max Output Tokens = 1200, razonamiento mínimo cuando esté disponible y Store = false. El tope incluye razonamiento y salida visible. Reutilizar el prompt dinámico y la ruta de error; mapear en Borrador la salida textual real del nuevo módulo.
Antes de sustituir el módulo activo se debe comprobar la conexión con una generación aislada, sin correo. Un límite alcanzado o texto vacío debe bloquear el borrador, registrarse y quedar para revisión; no debe presentarse como respuesta completa.
No se ha comprado saldo ni contratado un plan.

## Respuestas en el hilo
El flujo actual crea un correo o responde en un hilo existente según el Thread ID de Notion.
Cambio implementado: conservar todos los controles de aprobación y cliente, y separar dos rutas excluyentes después del bloqueo de envío:
- Thread ID vacío: Send an email, como actualmente.
- Thread ID presente: Reply to an email, con el identificador leído nuevamente de Notion, destinatario específico del cliente y el texto aprobado escapado.
La ruta nueva debe persistir el Thread ID devuelto, la fecha y el estado Enviado; conservar registro de éxito y error con Break sin reintento de envío.
No se debe sustituir el hilo del cliente por el hilo del aviso interno al aprobador. Una continuación se registra como un nuevo ticket vinculado al mismo cliente y al hilo existente, con nueva aprobación; no se borra la fecha de un ticket ya enviado para forzar un reenvío.

## Pruebas de aceptación
1. Generación con el límite numérico visible en la entrada del módulo y consumo registrado.
2. Manejo de respuesta incompleta o vacía sin notificación de borrador listo.
3. Verificado E08: nuevo mensaje y Thread ID persistido.
4. Verificado E07: mismo Thread ID de entrada y salida, destinatario correcto y texto técnico exacto.
5. Verificada segunda ejecución sin duplicados. Los filtros de rechazo y versiones distintas se conservaron; su prueba específica previa es E03/E05.

## Referencias
- [Módulos OpenAI de Make](https://apps.make.com/openai-modules)
- [Módulos Gmail de Make](https://apps.make.com/gmail-modules)
