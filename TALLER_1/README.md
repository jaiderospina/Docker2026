## Guía de Laboratorio: Dockerización de MariaDB y Publicación en Docker Hub

### 1. Objetivos
*   Configurar y desplegar un contenedor local de **MariaDB**.
*   Gestionar el esquema de base de datos de forma remota mediante **MySQL Workbench**.
*   Persistir y distribuir el entorno mediante la creación y subida de una imagen personalizada 

a **Docker Hub**.

---

### 2. Requisitos Previos
*   Docker Desktop (o Docker Engine en Linux) instalado y funcionando.
*   MySQL Workbench instalado.
*   Cuenta activa en [Docker Hub](https://hub.docker.com/).

---

### 3. Procedimiento

#### Fase A: Despliegue y Configuración Local
1.  **Levantar el contenedor:** Ejecuta el siguiente comando para iniciar una instancia de MariaDB.
    ```bash
    docker run --name lab-mariadb -e MYSQL_ROOT_PASSWORD=my-secret-pw -p 3306:3306 -d mariadb:latest
    ```
2.  **Conexión Externa:** 
    *   Abre **MySQL Workbench**.
    *   Crea una nueva conexión: `Hostname: 127.0.0.1`, `Port: 3306`, `Username: root`.
    *   Crea una base de datos llamada `Laboratorio_DB` y una tabla de prueba `Usuarios`.

#### Fase B: Creación de la Imagen Personalizada
1.  **Commit de cambios:** Para capturar la configuración actual y los datos iniciales en una nueva imagen:
    ```bash
    docker commit lab-mariadb tu_usuario_dockerhub/mariadb-lab-ready:v1.0
    ```
2.  **Login en Docker Hub:**
    ```bash
    docker login -u tu_usuario_dockerhub
    ```
3.  **Push a la nube:**
    
```bash
    docker push tu_usuario_dockerhub/mariadb-lab-ready:v1.0
    ```

---

### 4. Estructura del Overview (Docker Hub)
Para una calificación óptima, el "Description" en Docker Hub debe seguir esta estructura:

*   **Project Title:** Nombre claro del proyecto.
*   **Quick Start:** Comando `docker pull` y `docker run` necesario para replicar el laboratorio.
*   **Environment Variables:** Listado de variables (`MYSQL_ROOT_PASSWORD`, etc.).
*   **Database Schema:** Descripción breve de las tablas incluidas por defecto.
*   **Author:** Información de contacto o perfil académico.

---

### 5. Métricas de Calificación

| Criterio | Indicador de Logro | Puntaje (0-5) |
| :--- | :--- | :---: |
| **Configuración Docker** | El contenedor corre localmente y mapea correctamente el puerto 3306. | 1.0 |
| **Integración Workbench** | Se demuestra la creación de tablas y manipulación de datos desde el cliente GUI. | 1.0 |
| **Gestión de Imagen** | La imagen se genera con el tag correcto y se sube exitosamente a Docker Hub. | 1.5 |
| **Documentación (Overview)** | El README en Docker Hub es profesional, incluye comandos de ejecución y descripción técnica. | 1.0 |
| **Seguridad Básica** | Uso de variables de entorno para credenciales en lugar de valores embebidos. | 0.5 |

---

### Entregables
1.  Enlace al repositorio público en **Docker Hub**.
2.  Captura de pantalla de la conexión exitosa en **MySQL Workbench**.
3.  Breve informe con los comandos utilizados durante el proceso.
4.  Documentar todo en este repositorio en una carpeta por grupo.
```