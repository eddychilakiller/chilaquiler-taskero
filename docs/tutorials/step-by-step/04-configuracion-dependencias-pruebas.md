### 2.2: Configuración de Dependencias para Pruebas

#### **2.2 Configuración de Dependencias para Pruebas**

Para implementar TDD (Test-Driven Development) en el proyecto **chilaquiler-taskero**, es esencial configurar correctamente las dependencias necesarias para realizar pruebas unitarias y de integración tanto en el backend como en el frontend. A continuación se detallan los pasos para configurar estas dependencias en ambos lados del proyecto.

---

### **2.2.1 Configuración de Dependencias en el Backend (Java)**

El backend del proyecto **chilaquiler-taskero** utiliza Spring Boot, por lo que se aprovecharán las capacidades de pruebas integradas en Spring, junto con JUnit 5 y Mockito, que son las herramientas más comunes para realizar pruebas unitarias y de integración en proyectos Java.

#### **2.2.1.1 Actualización del archivo `pom.xml`**

1. **Agregar dependencias para pruebas en `pom.xml`**:
   - Abre el archivo `backend/pom.xml` y asegúrate de que contiene las siguientes dependencias para JUnit 5, Spring Boot Test, y Mockito:

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
                <exclusions>
                <exclusion>
                    <groupId>org.junit.vintage</groupId>
                    <artifactId>junit-vintage-engine</artifactId>
                </exclusion>
            </exclusions>
            </dependency>
        <dependency>
            <groupId>org.mockito</groupId>
            <artifactId>mockito-core</artifactId>
            <version>5.12.0</version>
            <scope>test</scope>
        </dependency>
        <dependency>
            <groupId>org.mockito</groupId>
            <artifactId>mockito-junit-jupiter</artifactId>
            <version>5.12.0</version>
        </dependency>

        <dependency>
            <groupId>org.assertj</groupId>
            <artifactId>assertj-core</artifactId>
                <version>3.26.3</version>
            <scope>test</scope>
        </dependency>

        <dependency>
            <groupId>org.hamcrest</groupId>
            <artifactId>hamcrest</artifactId>
                <version>3.0</version>
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

   - **Descripción de las dependencias**:
     - **Spring Boot Starter Test**: Incluye todo lo necesario para realizar pruebas en un proyecto Spring Boot, como JUnit 5, AssertJ, Hamcrest, y Mockito. También excluimos JUnit Vintage, que no es necesario si usamos JUnit 5.
     - **Mockito Core y Mockito JUnit Jupiter**: Mockito es un marco de pruebas que permite la creación de objetos simulados (mocks) para probar interacciones entre componentes.
     - **AssertJ y Hamcrest**: Proveen una API fluida para hacer aserciones más legibles y expresivas en las pruebas.

2. **Actualizar las dependencias del proyecto**:
   - Una vez añadidas las dependencias, ejecuta el siguiente comando en la terminal para actualizar el proyecto y descargar las dependencias:

   ```bash
   mvn clean install
   ```

#### **2.2.1.2 Configuración de la estructura de pruebas**

3. **Organización de las pruebas en la estructura del proyecto**:
   - En la carpeta `backend/src/test/java/com/chilaquiler/taskero`, puedes organizar tus pruebas en subcarpetas para reflejar la estructura del código de producción. Por ejemplo:

   ```bash
   backend/src/test/java/com/chilaquiler/taskero
   ├── service/                          # Pruebas para la capa de servicio
   ├── controller/                       # Pruebas para la capa de controladores
   ├── repository/                       # Pruebas para la capa de repositorios
   └── model/                            # Pruebas para la capa de modelos/entidades
   ```

#### **2.2.1.3 Ejemplo de una prueba unitaria simple**

4. **Crear una prueba unitaria con JUnit 5 y Mockito**:
   - Supongamos que queremos probar un servicio que gestiona tareas. Crearemos una prueba simple para verificar la adición de una tarea.

   **Paso 1**: Crea una clase de servicio:

   ```java
   // src/main/java/com/chilaquiler/taskero/service/TaskService.java
   package com.chilaquiler.taskero.service;

   import com.chilaquiler.taskero.model.Task;
   import java.util.ArrayList;
   import java.util.List;

   public class TaskService {
       private final List<Task> tasks = new ArrayList<>();

       public void addTask(Task task) {
           tasks.add(task);
       }

       public List<Task> getTasks() {
           return new ArrayList<>(tasks);
       }
   }
   ```

   **Paso 2**: Crea una prueba unitaria para este servicio:

   ```java
   // src/test/java/com/chilaquiler/taskero/service/TaskServiceTest.java
   package com.chilaquiler.taskero.service;

   import com.chilaquiler.taskero.model.Task;
   import org.junit.jupiter.api.Test;
   import static org.junit.jupiter.api.Assertions.*;

   class TaskServiceTest {

       @Test
       void testAddTask() {
           TaskService taskService = new TaskService();
           Task task = new Task("Comprar leche");

           taskService.addTask(task);

           assertTrue(taskService.getTasks().contains(task));
       }
   }
   ```

   - **Explicación**:
     - Esta prueba verifica que cuando se añade una tarea al servicio, la tarea aparece en la lista de tareas gestionadas por el servicio.

### **2.2.2 Configuración de Dependencias en el Frontend (Angular)**

El frontend del proyecto **chilaquiler-taskero** utiliza Angular, que por defecto viene con herramientas de prueba como Jasmine y Karma. Estas herramientas permiten realizar pruebas unitarias en los componentes, servicios y otros elementos de Angular.

#### **2.2.2.1 Confirmación de dependencias de pruebas en Angular**

1. **Verificar dependencias de pruebas en `package.json`**:
   - Asegúrate de que `package.json` incluya las siguientes dependencias y scripts para pruebas:

   ```json
   {
     "devDependencies": {
       "@angular-devkit/build-angular": "~16.0.0",
       "@angular/cli": "~16.0.0",
       "@angular/compiler-cli": "~16.0.0",
       "@angular/language-service": "~16.0.0",
       "@types/jasmine": "~4.0.0",
       "@types/jasminewd2": "~2.0.10",
       "jasmine-core": "~4.3.0",
       "jasmine-spec-reporter": "~7.0.0",
       "karma": "~6.4.0",
       "karma-chrome-launcher": "~3.1.0",
       "karma-coverage": "~2.2.0",
       "karma-jasmine": "~5.0.0",
       "karma-jasmine-html-reporter": "^2.0.0",
       "ts-node": "~10.0.0",
       "typescript": "~5.0.0"
     },
     "scripts": {
       "ng": "ng",
       "start": "ng serve",
       "build": "ng build",
       "test": "ng test",
       "lint": "ng lint",
       "e2e": "ng e2e"
     }
   }
   ```

   - **Descripción de las dependencias**:
     - **Jasmine**: Framework de pruebas para escribir especificaciones de pruebas.
     - **Karma**: Ejecutador de pruebas que ejecuta las pruebas en navegadores reales.
     - **@types/jasmine**: Definiciones de tipo para Jasmine, necesarias para TypeScript.

2. **Instalar o actualizar dependencias**:
   - Si necesitas instalar o actualizar dependencias, ejecuta el siguiente comando en la carpeta `frontend`:

   ```bash
   npm install
   ```

#### **2.2.2.2 Organización de pruebas en Angular**

3. **Organización de pruebas en Angular**:
   - Angular organiza automáticamente las pruebas junto a los archivos de código. Cada componente, servicio o módulo tiene su archivo de prueba correspondiente con la extensión `.spec.ts`.

   **Ejemplo**: Si tienes un componente `TaskListComponent`, Angular generará automáticamente un archivo de prueba llamado `task-list.component.spec.ts` cuando creas el componente.

   ```bash
   frontend/src/app/components/task-list/
   ├── task-list.component.ts        # Componente Angular
   └── task-list.component.spec.ts   # Prueba unitaria del componente
   ```

#### **2.2.2.3 Ejemplo de una prueba unitaria simple en Angular**

4. **Crear una prueba unitaria con Jasmine y Karma**:
   - Vamos a escribir una prueba simple para verificar que un componente Angular se crea correctamente.

   **Paso 1**: Asegúrate de que tienes un componente creado:

   ```typescript
   // src/app/components/task-list/task-list.component.ts
   import { Component } from '@angular/core';

   @Component({
     selector: 'app-task-list',
     templateUrl: './task-list.component.html',
     styleUrls: ['./task-list.component.scss']
   })
   export class TaskListComponent {
     tasks: string[] =

 ['Comprar leche', 'Llamar a Juan'];

     constructor() { }
   }
    ```

   **Paso 2**: Escribe una prueba unitaria para verificar que el componente se crea correctamente:

   ```typescript
   // src/app/components/task-list/task-list.component.spec.ts
   import { ComponentFixture, TestBed } from '@angular/core/testing';
   import { TaskListComponent } from './task-list.component';

   describe('TaskListComponent', () => {
     let component: TaskListComponent;
     let fixture: ComponentFixture<TaskListComponent>;

     beforeEach(async () => {
       await TestBed.configureTestingModule({
         declarations: [ TaskListComponent ]
       })
       .compileComponents();
     });

     beforeEach(() => {
       fixture = TestBed.createComponent(TaskListComponent);
       component = fixture.componentInstance;
       fixture.detectChanges();
     });

     it('should create the component', () => {
       expect(component).toBeTruthy();
     });

     it('should have two tasks', () => {
       expect(component.tasks.length).toBe(2);
     });
   });
   ```

   - **Explicación**:
     - **TestBed** es una clase Angular que permite configurar un entorno de prueba para un componente.
     - **ComponentFixture** es una envoltura alrededor del componente, permitiendo acceder y manipular su instancia en las pruebas.
     - Las pruebas verifican que el componente se crea correctamente y que la lista de tareas contiene dos elementos.

5. **Ejecutar pruebas en Angular**:
   - Ejecuta las pruebas en Angular utilizando Karma:

   ```bash
   ng test
   ```

   - Esto abrirá un navegador que ejecutará las pruebas y mostrará los resultados en la consola.