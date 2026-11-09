# Costos y decisiones de arquitectura

La prioridad del piloto fue funcionar con las cuentas disponibles y sin comprar suscripciones ni activar recargas. Eso no convierte la inferencia en ilimitada: Make descuenta créditos y el costo depende del modelo, los tokens, las operaciones y los reintentos.

## Comparación de herramientas

| Componente | Selección | Alternativa | Motivo |
|---|---|---|---|
| Orquestación | Make | n8n autohospedado | Cuenta y conexiones disponibles; evita instalar y mantener un servidor para esta entrega. |
| Memoria | Notion | Airtable | Tablas relacionadas, estados y publicación de vistas con la cuenta disponible. |
| Borrador | GPT-5 nano mediante Simple text prompt | GPT-4o-mini, Gemini o Claude | Resolvió consultas breves con la conexión administrada por Make. No se compararon modelos en un benchmark. |
| Comunicación | Gmail | Slack o WhatsApp API | Permite aviso interno y respuesta de prueba sin alta de plantillas ni otro canal. |
| Panel | Tablas Notion con cálculos | Gráficos de Notion | Evita la limitación de gráficos del plan gratuito. |

## Matriz de decisión: orquestador

Puntuación de diseño entre 1 y 5, donde 5 es más favorable para este proyecto. No representa una clasificación universal.

| Criterio | Peso | Make | n8n propio |
|---|---:|---:|---:|
| Cuenta y conexiones disponibles | 30 % | 5 | 1 |
| Desembolso inicial y mantenimiento | 30 % | 5 | 3 |
| Control técnico | 20 % | 3 | 5 |
| Tiempo de implementación | 20 % | 5 | 2 |
| Total ponderado | 100 % | **4,60** | **2,60** |

## Asignación de tareas

| Trabajo | Decisión | Estado |
|---|---|---|
| Estados, campos obligatorios, versiones, correo y fechas | Filtros y mapeos; no gastar tokens en comparaciones mecánicas | Implementado |
| Redacción breve con tres artículos de soporte | GPT-5 nano, una llamada por ticket válido | Implementado y probado |
| Lectura de contratos extensos o documentos ambiguos | Evaluar Claude, exigir citas y revisión humana antes de usar sus conclusiones | Estrategia de ampliación, no ejecutada |
| Etiquetado de tickets históricos y evaluación masiva sin urgencia | Batch API fuera del circuito de respuesta al cliente | Estrategia de ampliación, no ejecutada |

GPT-4o-mini es un ejemplo de la consigna, no el modelo utilizado. El piloto usa GPT-5 nano. Tampoco se declara uso de Claude ni de Batches que no haya ocurrido.

## Presupuesto del piloto

Sondeo: 2 escenarios × 4 consultas diarias × 30 días = **240 consultas mensuales**. Con intervalos de 15 minutos serían 5.760. La reducción es **95,83 % del sondeo**, no del costo total.

Al sondeo se suman el procesamiento de cada ticket, IA y reintentos. El envío T02 consumió siete operaciones y siete créditos, según su historial. No corresponde usar ese valor como precio de la generación con IA. El consumo de IA puede incluir tokens además de operaciones.

El contexto se limita a artículos vigentes (máximo diez en la consulta) y el prompt pide hasta 180 palabras. Esto reduce texto innecesario, pero **no equivale a configurar un límite duro de tokens**. La versión observada de Simple text prompt no expuso Max Tokens. Para un límite técnico estricto se requiere otro módulo o conexión y nueva validación.

## Batches: ahorro aplicable y cómo medirlo

La documentación de Anthropic indica un descuento del 50 % frente a la inferencia estándar comparable. Para una carga elegible de costo estándar C, el costo Batch sería 0,5 × C. Ejemplo ilustrativo: USD 10 pasan a USD 5; no es una factura ni un ahorro realizado por Mesa Clara.

Se propone utilizarlo sólo para tareas no urgentes: etiquetar históricos, resumir métricas y evaluar respuestas. No se debe hacer esperar una respuesta de soporte inmediata por un lote. El diseño de ampliación debe registrar custom_id, estado por solicitud, tokens, errores y versión del modelo; recuperar los resultados, relacionarlos con el ticket y evitar reenvíos de lotes completos por un único error.

Para certificar ahorro real habría que ejecutar la misma carga y modelo, registrar tokens de entrada/salida y tarifas, y comparar el subtotal de inferencia. Deben agregarse por separado los créditos de Make y las operaciones de consulta. Como aquí no se ejecutó esa carga, el descuento es una condición comercial documentada, **no un ahorro medido**.

## Fuentes

Consultadas el 9 de noviembre de 2026:

- [Make: créditos y consumo de IA](https://help.make.com/credits).
- [Anthropic: procesamiento por lotes](https://platform.claude.com/docs/en/build-with-claude/batch-processing).

Las tarifas y los modelos disponibles pueden cambiar. Revalidar antes de ampliar el piloto.
