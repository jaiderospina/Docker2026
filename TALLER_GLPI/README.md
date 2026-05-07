
## 🧪 Laboratorio: Despliegue Orientado a Repositorio Oficial (GLPI)

#### 1. Introducción y Contexto

El objetivo es desplegar una instancia funcional de GLPI utilizando únicamente las definiciones del repositorio oficial. Se requiere un enfoque de **infraestructura como código** (IaC) para garantizar que el servicio sea reproducible y seguro.


**Para este laboratorio, el enfoque cambia de una guía técnica a un **desafío de ingeniería**. Se debe interactuar directamente con la documentación y el repositorio oficial de GLPI para construir la solución, aplicando los principios de soberanía de datos y despliegue local que caracterizan el entorno de trabajo.**


#### 2. Objetivos de la Práctica

*   **Investigación Técnica:** Interpretar los archivos de configuración (`docker-compose`, `Dockerfile` o `env`) directamente desde la fuente oficial.
*   **Orquestación Local:** Configurar un entorno de contenedores que garantice la persistencia de la base de datos y los archivos de configuración.
*   **Gestión de Secretos:** Implementar el uso de variables de entorno para evitar la exposición de credenciales.

---

### 3. Guía de Ejecución (Paso a Paso)

**Fase I: Análisis del Repositorio**
1.  Emplear el repositorio oficial de GLPI en Docker Hub.
- https://hub.docker.com/r/glpi/glpi
2.  Identificar las **etiquetas (tags)** disponibles para seleccionar la versión más estable.
3.  Analizar las **variables de entorno obligatorias** requeridas por la imagen para conectarse a una base de datos (host, usuario, password y nombre de la BD).

**Fase II: Diseño de la Infraestructura**

1.  **Definición de Servicios:** Crear un diseño donde coexistan el contenedor de aplicación y el de base de datos (MariaDB o MySQL).
2.  **Mapeo de Puertos:** Establecer un puerto local que no entre en conflicto con otros servicios del sistema.
3.  **Persistencia:** Investigar las rutas internas de la imagen oficial (usualmente bajo `/var/lib/...`) para montar volúmenes locales y evitar la pérdida de datos al detener los contenedores.

**Fase III: Despliegue y Validación**

1.  Ejecutar la descarga de imágenes y el levantamiento de servicios.
2.  Realizar la vinculación inicial a través de la interfaz web, asegurando que la aplicación "vea" al contenedor de la base de datos por su nombre de servicio en la red de Docker.

**Fase iv: Publicar en github**


1. Publicar y documentar en dockerhub.
2. Realizar un overview siguiendo el presentado por GLPI.
 
---

### 4. Métricas de Calificación (Escala 1-10)

La evaluación se centrará en la capacidad del estudiante para abstraer la solución sin plantillas prefabricadas:

| Criterio | Indicador de Logro | Puntaje |
| :--- | :--- | :---: |
| **Autonomía de Investigación** | El despliegue coincide estrictamente con las especificaciones del repositorio oficial consultado. | 2.5 |
| **Aislamiento y Red** | Uso correcto de una red privada de Docker para la comunicación entre la aplicación y la BD. | 1.5 |
| **Estrategia de Volúmenes** | Implementación de volúmenes persistentes que sobrevivan a un `docker down`. | 2.0 |
| **Abstracción de Credenciales** | Uso de archivos externos o variables de entorno para la configuración sensible. | 1.5 |
| **Funcionalidad del Servicio** | El sistema es capaz de completar el asistente de instalación y permitir el acceso al dashboard. | 1.5 |
| **Resolución de Problemas** | Documentación de los errores encontrados durante la interpretación del repositorio y su solución. | 1.0 |
| **Total** | | **10.0** |

---

### ⚠️ Restricciones de la Práctica
*   **Prohibición de Código:** No se permite el uso de archivos `docker-compose.yml` encontrados en tutoriales de terceros; solo se admite lo derivado de la documentación oficial.
*   **Soberanía de Datos:** Toda la infraestructura debe correr en un nodo de cómputo local, sin dependencias de servicios externos de base de datos.