# Diccionario de datos real

Esquema leído de Notion el 9 de noviembre de 2026. Las obligatoriedades indicadas son reglas del flujo: Notion permite campos vacíos. La base se creó mediante instrucciones a IA y el conector Notion; no se utilizó Omni AI.

## Clientes demo

| Campo | Tipo | Opciones o relación |
| --- | --- | --- |
| Activo | checkbox |  |
| Cliente | title |  |
| Codigo | text |  |
| Correo | email |  |
| Plan | select | Basico, Profesional |

## Conocimiento

| Campo | Tipo | Opciones o relación |
| --- | --- | --- |
| Articulo | title |  |
| Categoria | select | Acceso, Uso, Facturacion |
| Contenido | text |  |
| Version | number |  |
| Vigente | checkbox |  |

## Tickets

| Campo | Tipo | Opciones o relación |
| --- | --- | --- |
| Aprobado el | date |  |
| Borrador | text |  |
| Categoria | select | Acceso, Uso, Facturacion, Otro |
| Cliente | relation | collection://be7f9b8e-ecf1-4ced-b977-ff0df9453cdf |
| Confianza | number |  |
| Consulta | text |  |
| Creado | created_time |  |
| Enviado el | date |  |
| Error detalle | text |  |
| Estado | select | Pendiente, Procesando, Esperando aprobacion, Aprobado, Rechazado, Enviando, Enviado, Error, Incompleto |
| Fuentes | relation | collection://9d8a47af-5444-4612-8819-9167a43a3d6f |
| Mensaje ID | text |  |
| Modelo | text |  |
| Texto aprobado | text |  |
| Thread ID | text |  |
| Ticket | title |  |
| Version | number |  |
| Version aprobada | number |  |

## Ejecuciones

| Campo | Tipo | Opciones o relación |
| --- | --- | --- |
| Codigo error | text |  |
| Creditos | number |  |
| Detalle seguro | text |  |
| Ejecucion | title |  |
| Es error | formula |  |
| Es terminado | formula |  |
| Etapa | text |  |
| Fin | date |  |
| Inicio | date |  |
| Intentos | number |  |
| Resultado | select | En curso, Correcto, Error, Bloqueado, Duplicado |
| Ticket | relation | collection://43dca525-20fb-4c2c-bf42-1cd81df58626 |

## Configuracion

| Campo | Tipo | Opciones o relación |
| --- | --- | --- |
| Descripcion | text |  |
| Parametro | title |  |
| Valor | text |  |

## Reglas y límites

- Tickets.Cliente enlaza el cliente; Fuentes enlaza Conocimiento; Ejecuciones.Ticket enlaza el ticket. La relación Fuentes existe pero el flujo aún no la completa automáticamente.
- Recepción valida Consulta no vacía y relación Cliente presente. El emisor está configurado para exigir exactamente un cliente activo con correo, texto aprobado, versiones iguales y fecha de aprobación; falta probar el envío completo.
- Version y Version aprobada son números; su igualdad no debe hacerse como texto. Confianza no se calcula actualmente.
- Mensaje ID no tiene restricción de unicidad global. No afirmar entrega exactamente una vez.
- Notion representa rich_text como arreglos; concatenar plain_text. Las fechas pueden ser null; comprobar presencia antes de acceder a start.
- Los estados Procesando y Error están disponibles en el esquema, pero no todas las rutas los escriben. El error inducido T06 se registró en Ejecuciones.
- Es error y Es terminado son fórmulas de Notion; no escribirlas desde Make. No usar Creditos como costo medido cuando esté vacío.
- No publicar Clientes ni Configuracion con correos reales. Un tablero compartido debe limitar las propiedades visibles y verificar permisos de las páginas relacionadas.
