# Caso de Estudio: Optimización de Infraestructura de Red y Resolución de Incidentes

## 1. Contexto y Desafío
En este caso se aborda la intervención realizada en una infraestructura de red local que presentaba caídas intermitentes del servicio, conflictos de direcciones IP duplicadas y lentitud generalizada en la transferencia de datos. 

Este escenario generaba un alto volumen de tickets de soporte diario, afectando la operatividad de los departamentos administrativo y operativo.

* **Rol:** Administrador de Soporte e Infraestructura TI.
* **Impacto inicial:** Pérdida de conectividad intermitente en más de 40 terminales de trabajo.

## 2. Diagnóstico Técnico
Para identificar la causa raíz del problema, se aplicó un proceso metódico de diagnóstico de hardware, software y topología de red:

1. **Monitoreo de Tráfico:** Uso de herramientas de análisis de paquetes (Wireshark) para identificar tormentas de broadcast causadas por un bucle físico en la capa 2 (switches no administrables).
2. **Auditoría de Direccionamiento:** Uso de comandos de diagnóstico (`ping`, `arp -a`, `nslookup`) para rastrear los conflictos de IP. Se detectaron dispositivos personales (smartphones) obteniendo IPs estáticas asignadas a servidores locales debido a la falta de control en el servidor DHCP.

## 3. Implementación de la Solución
Se ejecutó un plan de reestructuración y gestión de sistemas para estabilizar la red:

* **Eliminación del Bucle:** Identificación del cableado redundante defectuoso en los switches de distribución y sustitución de hardware dañado.
* **Segmentación de Red (Subredes):** Configuración del enrutador principal para separar el tráfico mediante la creación de subredes lógicas:
  * **Subred 1 (Administración/Servidores):** Direccionamiento estático y IPs reservadas.
  * **Subred 2 (Operaciones/Usuarios):** Asignación dinámica regulada por DHCP con tiempos de concesión (lease time) de 8 horas.
  * **Subred 3 (Invitados/Wi-Fi):** Aislada de la red local principal para garantizar la seguridad de los activos de la empresa.
* **Control de Acceso:** Implementación de filtrado por direcciones MAC en el punto de acceso inalámbrico corporativo.

## 4. Resultados Obtenidos
Tras la intervención y la reconfiguración del entorno, se lograron los siguientes indicadores de éxito:

* **Estabilidad del 99.9%** en la red local durante las semanas posteriores a la implementación.
* **Reducción del 85%** en el volumen de tickets de soporte técnico relacionados con conectividad y redes.
* **Eliminación total** de los conflictos de direcciones IP duplicadas.
* **Optimización del rendimiento:** Aumento en la velocidad de respuesta de las aplicaciones internas y bases de datos locales gracias a la reducción del tráfico basura (broadcast).
