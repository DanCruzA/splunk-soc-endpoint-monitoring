# Mini-SIEM: Monitoreo de Seguridad de Endpoints con Splunk

## Descripción
Implementación de un entorno local de Splunk (mediante Docker) para la ingesta, correlación y análisis de eventos de seguridad (logs de autenticación) en un entorno Linux (Pop!_OS 22.04 LTS). Este proyecto simula las operaciones diarias de un Centro de Operaciones de Seguridad (SOC), aplicando análisis forense offline.

## Tecnologías Utilizadas
* **SIEM:** Splunk Enterprise
* **SO / Entorno:** Linux (Pop!_OS / Ubuntu), Docker
* **Lenguaje de Consulta:** SPL (Search Processing Language)

## Resultados y Detección
Se ingirió la evidencia forense (`auth.log`) y se estructuró una consulta SPL para extraer y contabilizar los procesos de seguridad ejecutados, identificando el uso de privilegios (`sudo`, `su`) y tareas automatizadas (`CRON`).

```text
source="auth.log"
| stats count by process
| sort - count
```
