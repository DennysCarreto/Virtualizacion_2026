# Virtualizacion
Tareas durante el transcurso del curso

# Tarea 04 - Conexión IPSec

## Descripción
Implementación de un túnel VPN IPSec en modo túnel entre Site-A y Site-B a través de un router ISP, permitiendo tráfico HTTPS seguro.

## Evidencia de Conexión HTTPS
![Prueba HTTPS](Capturas/ConexionExitosa.png)

## Verificación del Túnel IPSec
* **Estado ISAKMP:** `QM_IDLE`
* **Encapsulación / Desencapsulación:** Tráfico cifrado exitoso entre `192.168.10.0/24` y `192.168.20.0/24`.

### Comprobación R1 (Site-A)
![Comprobación R1](Capturas/R0comprobacion.png)

### Comprobación R3 (Site-B)
![Comprobación R3](Capturas/r2comprobacion.png)

## Configuraciones de Routers

### R1 - Site-A (Router0)
![Configuración R1](Capturas/R0.png)

### ISP - Internet (RISP1)
![Configuración ISP](Capturas/RISP1.png)

### R3 - Site-B (Router2)
![Configuración R3](Capturas/confR2.png)