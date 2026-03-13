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
## Descripción Técnica:
Esta captura evidencia la ejecución exitosa de un entorno SIEM local (Splunk Enterprise) para el análisis forense de un endpoint Linux. La interfaz muestra el módulo de Search & Reporting, donde se ha procesado la ingesta del registro de seguridad del sistema (auth.log).

## Detalles del Análisis:
* **Consulta SPL (Search Processing Language):** Se utilizó el comando stats count by process seguido de sort - count para extraer, estructurar y contabilizar los procesos responsables de los eventos de seguridad, ordenándolos por volumen de actividad.

* **Volumen de Datos:** Se procesaron y correlacionaron exitosamente 963 eventos de seguridad.

* **Visualización:** El resultado se representa mediante un gráfico circular (Pie Chart), permitiendo una rápida identificación visual de la distribución de los procesos.

* **Interpretación SOC (Threat Hunting):** El panel permite establecer una línea base (baseline) del comportamiento del sistema. Se observa el predominio esperado de tareas automatizadas y de gestión de sesiones (CRON, systemd-logind), mientras que aisla visualmente la actividad de procesos interactivos y de escalamiento de privilegios (como sudo, gdm-password y polkitd). Esta estructuración es vital para detectar anomalías, picos inusuales de intentos de autenticación o posibles movimientos laterales en una auditoría de seguridad.
