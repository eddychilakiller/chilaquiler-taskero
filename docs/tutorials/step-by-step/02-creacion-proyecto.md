### Desarrollo del Punto 1.2: Creación del Proyecto desde Cero

El objetivo de este paso es configurar la estructura inicial tanto del backend como del frontend para el proyecto **chilaquiler-taskero**, sin utilizar herramientas automáticas como Spring Initializr, sino creando todo manualmente para un mayor control y entendimiento del proceso.

---

#### **1.2 Creación del Proyecto desde Cero**

#### **1.2.1 Configuración del Proyecto Backend**

##### **1.2.1.1 Estructura de Carpetas**

1. **Crear la estructura básica**:
   - Abre una terminal y navega al directorio donde deseas crear el proyecto.
   - Ejecuta los siguientes comandos para crear la estructura de carpetas del backend:

   ```bash
   mkdir -p backend/src/main/java/com/chilaquiler/taskero
   mkdir -p backend/src/main/resources
   mkdir -p backend/src/test/java/com/chilaquiler/taskero
   mkdir -p backend/src/test/resources
   ```

   Esto creará la estructura básica de carpetas para el código fuente (`main`) y para las pruebas (`test`).

##### **1.2.1.2 Creación del archivo `pom.xml`**

2. **Crear el archivo `pom.xml`**:
   - En la carpeta `backend/`, crea un archivo `pom.xml` y añade la siguiente configuración básica:

   ```xml
        <project xmlns="http://maven.apache.org/POM/4.0.0"
                xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
                xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
            <modelVersion>4.0.0</modelVersion>

            <groupId>com.chilaquiler.taskero</groupId>
            <artifactId>chilaquiler-taskero-backend</artifactId>
            <version>1.0.0</version>
            <packaging>jar</packaging>

            <name>chilaquiler-taskero-backend</name>
            <description>Backend for Chilaquiler Taskero using Spring Boot</description>

            <properties>
                <java.version>21</java.version>
                <spring.boot.version>3.3.2</spring.boot.version>
            </properties>

            <dependencies>
                <!-- Spring Boot Starter Dependencies -->
                <dependency>
                    <groupId>org.springframework.boot</groupId>
                    <artifactId>spring-boot-starter-web</artifactId>
                    <version>${spring.boot.version}</version>
                </dependency>
                <dependency>
                    <groupId>org.springframework.boot</groupId>
                    <artifactId>spring-boot-starter-data-jpa</artifactId>
                    <version>${spring.boot.version}</version>
                </dependency>
                <dependency>
                    <groupId>org.springframework.boot</groupId>
                    <artifactId>spring-boot-starter-security</artifactId>
                    <version>${spring.boot.version}</version>
                </dependency>

                <!-- H2 Database for Development -->
                <dependency>
                    <groupId>com.h2database</groupId>
                    <artifactId>h2</artifactId>
                    <version>2.1.214</version> <!-- Adjust the version as needed -->
                    <scope>runtime</scope>
                </dependency>

                <!-- Spring Boot Test Starter -->
                <dependency>
                    <groupId>org.springframework.boot</groupId>
                    <artifactId>spring-boot-starter-test</artifactId>
                    <version>${spring.boot.version}</version>
                    <scope>test</scope>
                </dependency>
            </dependencies>

            <build>
                <plugins>
                    <plugin>
                        <groupId>org.springframework.boot</groupId>
                        <artifactId>spring-boot-maven-plugin</artifactId>
                    </plugin>
                </plugins>
            </build>
        </project>

   ```

   - Este archivo `pom.xml` define las dependencias básicas para un proyecto Spring Boot, incluyendo el web starter, JPA, seguridad, y la base de datos H2 para desarrollo.

##### **1.2.1.3 Configuración del Archivo `application.properties`**

3. **Crear el archivo de configuración `application.properties`**:
   - En la carpeta `backend/src/main/resources/`, crea un archivo llamado `application.properties` con la siguiente configuración básica:

   ```properties
   # Configuración de la base de datos
   spring.datasource.url=jdbc:h2:mem:taskerodb;DB_CLOSE_DELAY=-1;DB_CLOSE_ON_EXIT=FALSE
   spring.datasource.driverClassName=org.h2.Driver
   spring.datasource.username=sa
   spring.datasource.password=password
   spring.jpa.database-platform=org.hibernate.dialect.H2Dialect
   spring.h2.console.enabled=true

   # Configuración de JPA
   spring.jpa.hibernate.ddl-auto=update
   ```

   - Esta configuración establece la base de datos H2 en memoria para el entorno de desarrollo, permitiendo que el esquema se actualice automáticamente.

##### **1.2.1.4 Creación de la Clase Principal**

4. **Crear la clase principal de la aplicación**:
   - En `backend/src/main/java/com/chilaquiler/taskero`, crea un archivo llamado `ChilaquilerTaskeroApplication.java` con el siguiente contenido:

   ```java
   package com.chilaquiler.taskero;

   import org.springframework.boot.SpringApplication;
   import org.springframework.boot.autoconfigure.SpringBootApplication;

   @SpringBootApplication
   public class ChilaquilerTaskeroApplication {
       public static void main(String[] args) {
           SpringApplication.run(ChilaquilerTaskeroApplication.class, args);
       }
   }
   ```

   - Esta clase principal contiene el punto de entrada para la aplicación Spring Boot.

#### **1.2.2 Configuración del Proyecto Frontend**

##### **1.2.2.1 Creación del Proyecto Angular**

1. **Inicializar el proyecto Angular**:
   - Navega a la carpeta raíz del proyecto `chilaquiler-taskero/` en la terminal.
   - Ejecuta el siguiente comando para crear el proyecto Angular:
   
   ```bash
   ng new frontend --routing --style=scss
   ```
   
   - Este comando crea un nuevo proyecto Angular con soporte para enrutamiento y con SCSS como preprocesador de CSS.

2. **Navegar al directorio del proyecto**:
   - Una vez creado, navega a la carpeta `frontend`:
   
   ```bash
   cd frontend
   ```

3. **Instalar Angular Material**:
   - Ejecuta el siguiente comando para instalar Angular Material:
   
   ```bash
   ng add @angular/material
   ```
   
   - Sigue las instrucciones para seleccionar un tema y configurar la animación global.

4. **Configurar los ambientes de desarrollo**:
   - Angular ya ha creado por defecto los archivos `environment.ts` y `environment.prod.ts` en la carpeta `src/environments/`. Puedes personalizarlos según las necesidades del proyecto.

##### **1.2.2.2 Estructura de Componentes y Módulos**

5. **Organizar la estructura de componentes y módulos**:
   - Dentro de `frontend/src/app/`, organiza los módulos y componentes para una mejor escalabilidad y mantenimiento. Por ejemplo:
   
   ```bash
   mkdir -p frontend/src/app/modules
   mkdir -p frontend/src/app/components
   mkdir -p frontend/src/app/services
   ```

   - Crea módulos separados para diferentes funcionalidades, como autenticación, gestión de tareas, y dashboard.

6. **Configurar rutas iniciales**:
   - Abre el archivo `app-routes.module.ts` y configura las rutas iniciales, por ejemplo:
   
   ```typescript
   import { NgModule } from '@angular/core';
   import { RouterModule, Routes } from '@angular/router';

   const routes: Routes = [
     { path: '', redirectTo: '/dashboard', pathMatch: 'full' },
     { path: 'dashboard', loadChildren: () => import('./modules/dashboard/dashboard.module').then(m => m.DashboardModule) },
     { path: '**', redirectTo: '/dashboard' }
   ];

   @NgModule({
     imports: [RouterModule.forRoot(routes)],
     exports: [RouterModule]
   })
   export class AppRoutingModule { }
   ```
##### **1.2.2.2.1 Crear un modulo de Ejemplo**
   - Crea un módulo de ejemplo
    ```bash
        cd frontend/src/app/modules
        ng generate module dashboard
    ```   

##### **1.2.2.3 Crear un Componente de Ejemplo**

7. **Crear un componente inicial**:
   - Crea un componente de ejemplo para verificar que todo esté funcionando correctamente:
   
   ```bash
    cd frontend/src/app/
    ng generate component components/task-list
   ```
   
   - Este comando genera un componente `TaskListComponent` dentro de la carpeta `components`.

8. **Ejecutar la aplicación Angular**:
   - Ejecuta la aplicación para verificar que todo esté configurado correctamente:
   
   ```bash
   ng serve
   ```

   - Abre el navegador en `http://localhost:4200` para ver la aplicación en funcionamiento.
