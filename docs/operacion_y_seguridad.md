# Operación y seguridad

Mesa Clara prepara respuestas de soporte para una empresa ficticia de software. La IA redacta; una persona decide qué texto puede salir. El envío utiliza ese texto aprobado, sin pedirle al modelo que vuelva a escribirlo.

## Alta y aprobación

1. Crear un ticket con Consulta, Cliente y Estado `Pendiente`. Cada consulta debe tener su propio identificador de origen.
2. Recepción consulta el conocimiento vigente, guarda Borrador y Modelo, cambia a `Esperando aprobacion` y notifica al responsable definido en Configuracion.
3. Revisar respuesta y fuentes. Completar Texto aprobado, Version aprobada y Aprobado el. Cambiar a `Aprobado` al final. Para rechazar, usar `Rechazado`.
4. El emisor relee el ticket, compara versiones como números y comprueba que no tenga fecha de envío. Requiere exactamente un cliente activo con correo.
5. Antes de Gmail marca `Enviando`; después guarda `Enviado`, fecha e hilo. Una modificación posterior del texto exige retirar la aprobación, incrementar Version y revisar otra vez.

Los escenarios consultan cada seis horas. Para una demostración se puede usar Run once, respetando el mismo orden de aprobación. El tiempo de espera humano no se incluye en la latencia del sistema. Cada etapa puede esperar hasta seis horas por programación.

## Recuperación de incidentes

| Situación | Comportamiento implementado | Recuperación |
|---|---|---|
| Consulta vacía o cliente ausente | Ruta Incompleto y log Bloqueado, sin IA | Corregir el origen. Recepción observa creación: una edición sola no equivale a ticket nuevo. Reprocesar expresamente el caso sin crear dos envíos. |
| Error en módulo IA | Log Error y Break; configuración de hasta 3 reintentos, separados por 15 minutos | Revisar tipo de error. Un modelo inválido no se arregla esperando; corregir configuración antes de reanudar. |
| Fallo en Gmail | Log de conciliación y Break sin reenvío automático | Buscar correo por asunto, destinatario e hilo. Si se envió, completar el registro; si no, reautorizar un único intento. |
| Gmail envió y falla el guardado Notion | Puede permanecer Enviando | No volver a Aprobado a ciegas. Conciliar Gmail y completar fecha/hilo manualmente. |
| Falla Notion o un módulo sin manejador específico | Error visible en Make; almacenamiento de ejecuciones incompletas configurado | Reparar conexión o datos, revisar qué operaciones ya se ejecutaron y resolver el elemento de la cola. No asumir que todas las rutas escribieron en Ejecuciones. |
| La cola frena nuevas ejecuciones | Procesamiento secuencial espera la resolución | Escenario → Incomplete executions. Inspeccionar el elemento. Reintentar sólo si es seguro; descartar únicamente pruebas o casos conciliados. |

La prueba T06 dejó un elemento incompleto que detenía recepción. Se retiró sólo ese elemento después de documentarlo; la cola quedó vacía y desapareció el aviso. No se borró el historial ni se repitió un envío. Es una demostración del costo operativo de usar Break con ejecución secuencial.

## Datos y permisos

- Finalidad: preparar y controlar respuestas de soporte. Esta entrega utiliza datos ficticios y un destinatario de prueba del propietario.
- Datos enviados a IA: consulta y artículos vigentes. El correo del cliente se consulta aparte para Gmail. La separación de campos no anonimiza texto libre: el operador debe evitar incluir datos personales en Consulta.
- No ingresar contraseñas, tarjetas, documentos de identidad, datos médicos ni claves API en tickets, prompts o logs.
- Logs: código, etapa, resultado, fecha y relación con el ticket. Evitar copiar íntegramente mensajes de error que incluyan cabeceras, tokens o datos personales.
- Permisos: operador para revisar y aprobar; administrador para conexiones y escenarios; evaluador en lectura del panel público. Tickets, Clientes y Configuracion permanecen privados.
- Retención definida para el piloto: consultas y borradores hasta 30 días después del cierre; logs minimizados durante 90 días. La revisión y eliminación son manuales, no un borrado automático implementado.
- Credenciales: conexiones de Make. El repositorio contiene referencias de conexión y de bases, no claves de autenticación. Al importar se deben reasignar.
- Para operar con datos reales, el responsable debe validar finalidad, base de tratamiento, proveedores y retención aplicables. Esta demostración no constituye una certificación legal.

## Control diario

Revisar colas incompletas, tickets Enviando sin confirmación y estados Error/Bloqueado. Confirmar que los escenarios sigan activos y que el saldo de créditos alcance. En el panel, distinguir errores técnicos de rechazos de validación. Un aumento de bloqueos puede indicar entradas defectuosas, no una caída del modelo.

## Límites de la versión

No hay una transacción atómica entre Gmail y Notion ni una restricción global de unicidad por Mensaje ID. La secuencia probada evita reenviar T02, pero no garantiza exactamente una entrega bajo toda condición de concurrencia. No se probó una caída real de Gmail. La ruta T06 verifica la captura de un error de validación del módulo, no una indisponibilidad del proveedor.
