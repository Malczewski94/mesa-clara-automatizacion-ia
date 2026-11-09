# Cierre de entrega

## 1. Verificar el emisor

T02 ya tiene autorización humana de la versión 1. No solicitarla otra vez ni enviar el correo fuera de Make. Antes de ejecutar, leer el ticket y verificar que no exista fecha de envío; revisar Gmail si aparece Enviando para evitar duplicar un envío cuyo registro falló.

Abrir escenario 6963384, ejecutar Run once y comprobar cada filtro. Si el cursor ya consumió T02, establecer de forma controlada el punto de inicio del disparador para incluir su actualización, manteniendo filtros y sin recrear tickets. Comprobar destinatario de demostración, texto exacto aprobado, un solo correo, Thread ID, fecha y registro Correcto. Guardar captura real del historial ocultando correo personal y credenciales.

## 2. Casos pendientes

| Caso | Preparación | Aceptación |
| --- | --- | --- |
| Versión obsoleta | Ticket ficticio aprobado con versiones diferentes | No llama Gmail |
| Rechazo | Ticket ficticio Rechazado | No llama Gmail |
| Repetición | Reprocesar el ticket enviado | No segundo correo |
| Error de proveedor IA | Fallo controlado del proveedor, si es posible sin costo | Registro seguro y recuperación; distinguir de validación local |
| Fallo posterior al envío | Revisar recuperación del guardado | Conciliación antes de reintentar |

Agregar contingencias de Notion y avisos Gmail pendientes. Registrar fechas e IDs de ejecución reales. El error T06 fue de validación del módulo y no acredita una caída del proveedor.

## 3. Exportar y publicar

Exportar ambos blueprints directamente de Make. Sustituir las reconstrucciones solo después de verificar los archivos exportados. Revisar tokens, conexiones, correos y contenido personal antes de subir. No usar capturas del PDF como evidencia del sistema real.

Publicar una página de panel de solo lectura con datos ficticios, KPI de resultados y cobertura explícita. Comprobar el enlace sin sesión y los permisos de páginas relacionadas; no exponer Clientes ni Configuracion con correos reales.

Repositorio dedicado: https://github.com/Malczewski94/mesa-clara-automatizacion-ia. Actualizar allí los blueprints finales y las capturas cuando se verifiquen. Mantener enlaces.json con URLs comprobadas.

Grabar los tres minutos con el guion adjunto después de verificar el envío. Ocultar secretos y datos personales. No presentar el guion como video.

## 4. Condición de cierre

La entrega sigue parcial hasta verificar envío completo, exportaciones, capturas, acceso público al panel, video y repositorio. Claude, Batch y Omni AI no se ejecutaron: documentar la selección gratuita y la brecha respecto de la rúbrica, sin afirmar ahorros medidos ni uso inexistente.
