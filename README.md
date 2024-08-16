# **chilaquiler-taskero**

## **Descripción del Proyecto**
**chilaquiler-taskero** es un gestor de tareas basado en la metodología GTD (Getting Things Done) que permite a los usuarios capturar, procesar, organizar, revisar y ejecutar sus tareas de manera eficiente. Está diseñado para mejorar la productividad personal y del equipo, proporcionando una solución completa para la gestión de proyectos y tareas en diferentes contextos.

## **Características Principales**
- **Captura de Tareas**: Captura rápida de ideas, tareas y compromisos, clasificación por contexto, y establecimiento de recordatorios.
- **Procesamiento de Tareas**: Clasificación en categorías de acción como "Hacer", "Delegar", "Aplazar" o "Eliminar".
- **Organización de Tareas**: Agrupación en listas y proyectos, con etiquetas y vista de calendario.
- **Revisión**: Panel de control para revisiones periódicas, con recordatorios automáticos.
- **Ejecución de Tareas**: Visualización por contexto y prioridad, seguimiento de tiempo, y finalización de tareas.
- **Accesibilidad y UX**: Diseño responsivo con Angular Material, optimizado para accesibilidad.
- **Seguridad**: Autenticación y autorización con JWT, protección de datos sensibles.

## **Tecnologías Utilizadas**
- **Backend**: Java con Spring Boot
- **Frontend**: Angular con Angular Material
- **Base de Datos**: H2 (Local), MySQL (Desarrollo y Producción)
- **Versionado de Base de Datos**: Liquibase
- **Despliegue**: Docker y Kubernetes
- **TDD**: Desarrollo basado en pruebas (TDD) tanto en el backend como en el frontend
- **CI/CD**: Integración continua y despliegue continuo (Jenkins o GitHub Actions)

## **Temario del Proyecto chilaquiler-taskero**

### **1. Configuración Inicial**
   - **1.1. Instalación del entorno de desarrollo**
     - Instalación de JDK 21 para el backend.
     - Configuración del entorno en IntelliJ IDEA o VS Code.
     - Instalación de Node.js y Angular CLI para el frontend.
   - **1.2. Creación del proyecto desde cero**
     - Estructura de carpetas del proyecto para backend y frontend.
     - Configuración inicial de `pom.xml` para Maven en el backend (sin Spring Initializr).
     - Configuración de Angular y Angular Material en el frontend.

### **2. Fundamentos de TDD (Test-Driven Development)**
   - **2.1. Introducción al TDD**
     - Conceptos básicos de TDD.
     - Ventajas del desarrollo basado en pruebas en un proyecto como **chilaquiler-taskero**.
   - **2.2. Configuración de dependencias para pruebas**
     - Configuración de JUnit 5 y Mockito para pruebas unitarias en el backend.
     - Configuración de Jasmine y Karma para pruebas en el frontend.
   - **2.3. Escribir la primera prueba**
     - Crear la primera prueba fallida en backend y frontend.
     - Implementar el código mínimo para pasar la prueba.

### **3. Creación del API REST para chilaquiler-taskero**
   - **3.1. Definición del modelo de dominio**
     - Crear clases de entidad para representar tareas, proyectos y usuarios según GTD.
     - Mapear entidades con JPA (Java Persistence API).
   - **3.2. Implementación del repositorio**
     - Crear interfaces de repositorio usando `CrudRepository`.
     - Pruebas unitarias para asegurar la integridad del repositorio.
   - **3.3. Implementación del servicio**
     - Crear clases de servicio para gestionar la lógica de negocio del gestor de tareas.
     - Pruebas unitarias para el servicio.
   - **3.4. Creación de controladores REST**
     - Definir controladores para manejar las solicitudes HTTP (GET, POST, PUT, DELETE).
     - Pruebas unitarias para controladores usando `MockMvc`.

### **4. Gestión de Errores y Excepciones**
   - **4.1. Manejo de excepciones con @ControllerAdvice**
     - Crear un manejador global para excepciones comunes en la aplicación.
     - Personalización de respuestas de error con mensajes claros para el usuario final.
   - **4.2. Validación de entradas**
     - Validaciones usando Hibernate Validator para asegurar datos consistentes.
     - Pruebas para validar el manejo de errores y respuestas.

### **5. Persistencia de Datos**
   - **5.1. Configuración de la base de datos local**
     - Configuración de H2 para el entorno de desarrollo local.
     - Versionado de la base de datos usando Liquibase.
     - Pruebas de integración con la base de datos H2.
   - **5.2. Configuración de la base de datos en desarrollo (Docker)**
     - Configuración de MySQL en Docker para el entorno de desarrollo.
     - Uso de Liquibase para versionar la base de datos en MySQL.
     - Pruebas de integración con Docker y MySQL.
   - **5.3. Configuración de la base de datos en producción (Kubernetes)**
     - Configuración de MySQL en Kubernetes para el entorno de producción.
     - Despliegue de scripts de Liquibase en producción.
     - Pruebas de integración en el entorno de producción.

### **6. Seguridad en el API**
   - **6.1. Introducción a Spring Security**
     - Configuración de seguridad básica para proteger los recursos del API.
     - Implementación de roles y permisos.
   - **6.2. Implementación de JWT (JSON Web Tokens)**
     - Configuración de JWT para autenticar y autorizar a los usuarios.
     - Protección de rutas sensibles usando JWT.
   - **6.3. Pruebas de seguridad**
     - Pruebas unitarias y de integración para validar la seguridad del API.

### **7. Desarrollo del Frontend con Angular**
   - **7.1. Configuración inicial de Angular**
     - Creación del proyecto Angular para **chilaquiler-taskero**.
     - Integración de Angular Material para una interfaz de usuario moderna.
   - **7.2. Aplicación de TDD en Angular**
     - Configuración de Jasmine y Karma.
     - Escribir pruebas antes de implementar cada componente y servicio.
   - **7.3. Uso de Angular Material y buenas prácticas**
     - Implementación de componentes UI siguiendo las guías de estilo de John Papa.
     - Aplicación de prácticas de accesibilidad (WAI-ARIA).
   - **7.4. Desarrollo de componentes y servicios**
     - Crear componentes y servicios para la gestión de tareas, proyectos y usuarios.
     - Pruebas unitarias para cada componente y servicio.
   - **7.5. Integración con el API REST**
     - Consumo del API desde Angular.
     - Pruebas de integración para asegurar la correcta comunicación entre frontend y backend.
   - **7.6. Desarrollo de una aplicación realista**
     - Diseñar y desarrollar la aplicación **chilaquiler-taskero** siguiendo la metodología GTD.
     - Implementación de funcionalidades clave como captura, organización y ejecución de tareas.

### **8. Despliegue en Docker**
   - **8.1. Creación del Dockerfile para el API**
     - Escribir un Dockerfile para crear la imagen del backend.
     - Crear una imagen de Docker para el backend y probarla localmente.
   - **8.2. Configuración de Docker Compose**
     - Configuración de servicios para el API y la base de datos en Docker Compose.
     - Pruebas del entorno de desarrollo usando Docker Compose.
   - **8.3. Despliegue del frontend en Docker**
     - Dockerización de la aplicación Angular.
     - Configuración del entorno completo (backend + frontend) usando Docker Compose.

### **9. Despliegue en Kubernetes**
   - **9.1. Introducción a Kubernetes**
     - Conceptos básicos de Kubernetes y su importancia en despliegues de producción.
     - Configuración de kubectl y minikube para pruebas locales.
   - **9.2. Despliegue del API en Kubernetes**
     - Creación de archivos de despliegue (Deployment, Service) para el backend.
     - Despliegue del backend en un clúster de Kubernetes.
   - **9.3. Despliegue del frontend en Kubernetes**
     - Creación de archivos de despliegue para la aplicación Angular.
     - Pruebas de la aplicación completa en Kubernetes.

### **10. Automatización y CI/CD**
   - **10.1. Configuración de un pipeline de CI/CD**
     - Integración con Jenkins o GitHub Actions para CI/CD.
     - Creación de un pipeline para construir, probar y desplegar **chilaquiler-taskero**.
   - **10.2. Pruebas automatizadas en el pipeline**
     - Integración de pruebas unitarias y de integración en el pipeline.
     - Despliegue automático en Kubernetes al pasar las pruebas.

### **11. Consideraciones Finales y Mejores Prácticas**
   - **11.1. Revisión del código y refactorización**
     - Uso de herramientas de análisis estático de código.
     - Aplicación de principios SOLID y técnicas de refactorización.
   - **11.2. Documentación del API**
     - Generación de documentación automática con Swagger/OpenAPI.
     - Mejores prácticas

 en la documentación de código y APIs.

## **Despliegue**
- **Entorno Local**: H2 con Maven para el backend y Angular CLI para el frontend.
- **Entorno de Desarrollo**: Docker con MySQL.
- **Entorno de Producción**: Kubernetes con MySQL, con despliegue automatizado a través de CI/CD.

## **Contribuciones**
Las contribuciones son bienvenidas. Por favor, sigue las pautas establecidas en [CONTRIBUTING.md](link_a_contributing).

## **Licencia**
Este proyecto está licenciado bajo la Licencia MIT. Consulta el archivo [LICENSE](link_a_license) para obtener más detalles.
