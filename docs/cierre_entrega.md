# Correspondencia con la consigna

Fecha de cierre documental: 9 de noviembre de 2026.

| Criterio | Implementación y evidencia | Alcance |
|---|---|---|
| Arquitectura, 20 % | PDF con diagrama; dos escenarios Make exportados; capturas de nodos y rutas | Cuatro tecnologías: Make, Notion, OpenAI y Gmail |
| Estructuras de datos, 20 % | Cinco tablas Notion, estados, relaciones, diccionario y esquema JSON; contratos de transferencia | Diseño mediante instrucciones a IA en Notion. No se utilizó Omni AI de Airtable |
| Costos, 20 % | Comparación de herramientas, matriz ponderada, asignación de tareas y cálculo de sondeo | Claude y Batches documentados como ampliación; descuento Batch del 50 % explicado, no medido en la demo |
| Seguridad y resiliencia, 20 % | HITL antes del envío; filtros; rutas de faltantes y error; manual de recuperación y minimización | No certifica cumplimiento legal ni entrega exactamente una vez; se describen límites de módulos y recuperación |
| Dashboard, 20 % | Panel público de Notion con promedio de error, grupos de resultado y últimas ejecuciones | Acceso anónimo verificado; datos de ensayo, cobertura parcial |

## Entregables disponibles

- PDF de arquitectura y manual.
- Dos blueprints originales de Make en JSON.
- Enlace público al panel y a la base de ejecuciones en lectura.
- Seis capturas originales de escenarios y ejecuciones.
- Registro de pruebas, contratos, costos y manual operativo.

## Incorporación pendiente

El autor agregará el video final de aproximadamente tres minutos. El guion está en `docs/guion_video.md`; no debe mostrar credenciales ni direcciones personales. Los videos descartados no forman parte de la entrega.

## Límites documentados

La entrega demuestra el circuito principal y los casos de error requeridos con las herramientas disponibles. No se presenta como una instalación productiva con cobertura total de contingencias. Simple text prompt no expone un Max Tokens duro en la configuración utilizada. El esquema incluye campos opcionales que no se completan automáticamente. E03/E05 tienen evidencia parcial mientras no pueda identificarse cada bundle en su historial. Estos límites no se ocultan ni se sustituyen por pruebas simuladas.
