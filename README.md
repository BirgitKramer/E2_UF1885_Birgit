# E2 UF1885 - Detección, análisis y resolución de incidencias (ERP-CRM)

**Alumno:** Birgit  
**Fecha:** 2026-02-04  
**Entorno:** Ubuntu Server + Docker  
**Contenedores:** odoo-dev (CRM) | postgres-dev (BD)

---

## 1. Análisis inicial del sistema y parámetros de rendimiento
### 1.1 Servicios de acceso al CRM
- Descripción:
  - Acceso al ERP/CRM (aplicacion web):container odoo-dev-PPF
  - El servicio de base de datos: contenedor postgres-dev-PPF
  - Servicio de publicacion de puerto /acceso web: Docker pubblica 8069/tcp
  - Red y DNS del sistema: interfaz la IP 192.168.1.131
  - Acceso administrativo remoto: SSH en 22/tcp para tareas de sopporte
- Evidencias: evidencias/01_analisis/

### 1.2 Parámetros (CPU / RAM / Disco / Red) y relación con CRM+BD
- %Cpu(s):  0.0 us,  0.0 sy,  0.0 ni, 97.6 id//load average: 0.32, 0.10, 0.03
- Conclusiones: no hay saturacion de CPU
- 
- RAM Mem: 10Gi total       838Mi used      9.2Gi free
- Conclusiones: hay suficiente memoria, no hay pression ahora mismo con la RAM
- Disco /dev/sda2        98G  9.3G   84G  11%
- Red 
Relacion CRM*BD
---

## 2. Monitorización de procesos y detección de sobrecarga
### 2.1 Proceso problemático detectado
- Proceso/servicio:
  - Contenedor postgres_dev-PPF (servicio PostgreSQL para ERP/CRM)
  - Proceso interno forzado: yes > /dev/null & (generador carga CPU)
- Datos y justificación:
  - CPU % (postgres_dev-PPF 14498.27%,indica saturacion del core
  - Consumo de memoria baja 112.7MiB / 10.6GiB   1.04%
  - Saturacion se produce a nivel del CPU
- Impacto en el CRM:
  - Lentidtud extrema en operaciones que dependen de la base de datos
  - Usuarios perciben bloqueos y esperas prolongadas

## 3. Resolución de una incidencia técnica simulada
### 3.1 Síntomas
- Los usarios no pueden accer als CRM
- La URL del servicio no responde: "Failed to connect"
### 3.2 Diagnóstico
- Verificar el estdo  de los contenedores (docker ps)
- El contenedor odoo-dev-PPF no se encuentro en ejecucion

### 3.3 Acción aplicada
- Se produce a restablecer el servicio de contendor, arrancando nuevamente
  ```
  sudo docker start odoo-dev-PPF
  ```
### 3.4 Verificación
- Verificacion estado del contenedor
  ```
  sudo docker ps
  ```
### 3.5 Rollback
- En esta situacion consiste en arrancar el contenedor como se inicia en la accion aplicada

## 4. Simulación de saturación del sistema (CPU o Memoria)
- Técnica utilizada:
  - Simulacion saturacion de memoria RAM mediante ejecuccion de un proceso que consume gran cantidad de memoria 
  - provocando una reduccion importante de la memoria libre.
- Datos capturados:
  - free -h > antes y despues de la simulacion
  - vmstat 1 5 > antes y despues de la simulacion
- Análisis:
  - Antes de la simulacion el sistema disponia de 8.8Gi de memoria disponible. Tras la simulacion,
   memoria libre se mantien a 8.8Gi, con lo que el sistema se encuentra normal.  
- Verificación requisitos HW/SW:
- 
- Registro:

---

## 5. Documentación y registro técnico
### 5.1 Incidencias detectadas / Acciones / Resultados
### 5.2 Interpretación de documentación en inglés (monitorización / rendimiento / administración CRM)
- Fragmento 1 (EN):
- Interpretación (ES):
- Fragmento 2 (EN):
- Interpretación (ES):
- Fragmento 3 (EN):
- Interpretación (ES):
