# Ajustes de tokens y conversación

Estado: implementación en Make y pruebas todavía pendientes. Los blueprints principales conservan la versión previamente verificada.

## Avance comprobado
- OpenAI: la conexión propia devolvió `[401] Your API key has expired. Create a new API key to continue.` al cargar modelos. Se confirmó que Generate a response expone Max Output Tokens. No se sustituyó el módulo activo ni se compró saldo.
- Gmail: se configuró Reply to an email en el editor con conexión existente, Thread ID dinámico, destinatario específico y texto aprobado. A partir de esa exportación real se preparó el [blueprint con rutas de nuevo correo y respuesta](../workflows/pendientes/02_envio_hilos.blueprint.json).
- El archivo conserva los filtros de aprobación y cliente, y duplica persistencia y manejo de errores para la nueva ruta. Es una versión preparada, **no desplegada ni probada en vivo**. La carga del archivo agotó el tiempo de espera y el navegador perdió la sesión antes de confirmar importación y guardado.
- Para tokens hace falta renovar la API key en la conexión OpenAI de Make. La clave nunca debe incluirse en GitHub ni en el chat.

## Límite técnico de generación
El módulo Simple text prompt actual no expone Max Output Tokens. Limitar el prompt a 180 palabras no configura un tope técnico.
Cambio previsto: OpenAI Generate a response con conexión propia, GPT-5 nano, Max Output Tokens = 1200, razonamiento mínimo cuando esté disponible y Store = false. El tope incluye razonamiento y salida visible. Reutilizar el prompt dinámico y la ruta de error; mapear en Borrador la salida textual real del nuevo módulo.
Antes de sustituir el módulo activo se debe comprobar la conexión con una generación aislada, sin correo. Un límite alcanzado o texto vacío debe bloquear el borrador, registrarse y quedar para revisión; no debe presentarse como respuesta completa.
No se ha comprado saldo ni contratado un plan.

## Respuestas en el hilo
El flujo actual crea un correo y guarda su Thread ID. Falta reutilizar un hilo de entrada.
Cambio previsto: conservar todos los controles de aprobación y cliente, y separar dos rutas excluyentes después del bloqueo de envío:
- Thread ID vacío: Send an email, como actualmente.
- Thread ID presente: Reply to an email, con el identificador leído nuevamente de Notion, destinatario específico del cliente y el texto aprobado escapado.
La ruta nueva debe persistir el Thread ID devuelto, la fecha y el estado Enviado; conservar registro de éxito y error con Break sin reintento de envío.
No se debe sustituir el hilo del cliente por el hilo del aviso interno al aprobador. Una continuación se registra como un nuevo ticket vinculado al mismo cliente y al hilo existente, con nueva aprobación; no se borra la fecha de un ticket ya enviado para forzar un reenvío.

## Pruebas de aceptación pendientes
1. Generación con el límite numérico visible en la entrada del módulo y consumo registrado.
2. Manejo de respuesta incompleta o vacía sin notificación de borrador listo.
3. Ticket sin hilo: nuevo mensaje y Thread ID persistido.
4. Ticket de continuación: mismo Thread ID de entrada y salida, destinatario correcto y texto aprobado exacto.
5. Segunda ejecución sin duplicados; rechazo y versiones distintas siguen bloqueados.

## Referencias
- [Módulos OpenAI de Make](https://apps.make.com/openai-modules)
- [Módulos Gmail de Make](https://apps.make.com/gmail-modules)
