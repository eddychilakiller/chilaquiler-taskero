### Documento: Patrones de Diseño en **chilaquiler-taskero**

---

**Nombre del Proyecto:** chilaquiler-taskero  
**Versión:** 1.0  
**Fecha:** [Fecha de creación del documento]  
**Autor:** [Tu nombre o equipo]

---

## **1. Introducción**

Este documento describe los patrones de diseño que se implementarán en el desarrollo de **chilaquiler-taskero**. Los patrones de diseño son soluciones probadas y reutilizables para problemas comunes en el desarrollo de software, garantizando que el código sea modular, mantenible y extensible. Además, se incluirá el uso de mappers y decorators en Java para facilitar la conversión y el enriquecimiento de objetos.

### **1.1 Objetivo del Documento**

El objetivo de este documento es:
- Proporcionar una guía clara sobre los patrones de diseño a implementar en **chilaquiler-taskero**.
- Asegurar la coherencia y calidad en la estructura del código a lo largo del proyecto.
- Facilitar la colaboración y el mantenimiento del proyecto mediante enfoques estándar y bien comprendidos.

---

## **2. Patrones de Diseño en el Backend**

### **2.1 Patrón MVC (Modelo-Vista-Controlador)**

**Descripción:**  
El patrón MVC separa las responsabilidades de la lógica de negocio, la interfaz de usuario y el control de flujo, promoviendo una mayor modularidad y facilitando el mantenimiento y prueba del código.

- **Modelo:** Representa los datos y las reglas de negocio de la aplicación.
- **Vista:** En el contexto de una API REST, las vistas son las respuestas JSON enviadas al frontend.
- **Controlador:** Maneja las solicitudes HTTP y orquesta la lógica de negocio a través de servicios.

**Aplicación en chilaquiler-taskero:**
- **Modelos:** Entidades JPA que representan tablas de la base de datos como `Task`, `Project`, `User`.
- **Vistas:** Respuestas JSON estructuradas enviadas al frontend.
- **Controladores:** Controladores Spring que manejan las solicitudes HTTP.

**Ejemplo:**

```java
@RestController
@RequestMapping("/tasks")
public class TaskController {

    @Autowired
    private TaskService taskService;

    @GetMapping("/{id}")
    public ResponseEntity<TaskDTO> getTask(@PathVariable Long id) {
        TaskDTO task = taskService.getTaskById(id);
        return ResponseEntity.ok(task);
    }

    // Otros métodos de controlador
}
```

---

### **2.2 Patrón Repository**

**Descripción:**  
El patrón Repository encapsula la lógica de acceso a datos, proporcionando una interfaz entre la aplicación y la base de datos. Facilita el cambio de implementaciones de persistencia y mejora la mantenibilidad del código.

**Aplicación en chilaquiler-taskero:**
- **Repositorios:** Cada entidad principal (`Task`, `Project`, `User`) tendrá su propio repositorio que manejará las operaciones CRUD y consultas específicas.

**Ejemplo:**

```java
@Repository
public interface TaskRepository extends JpaRepository<Task, Long> {

    List<Task> findByProjectId(Long projectId);

    // Otras consultas personalizadas
}
```

---

### **2.3 Patrón Service Layer (Capa de Servicio)**

**Descripción:**  
El patrón Service Layer separa la lógica de negocio de la lógica de acceso a datos y de la interfaz de usuario. Esta capa actúa como un intermediario, donde se implementan las reglas de negocio y se orquesta el flujo de trabajo entre diferentes partes de la aplicación.

**Aplicación en chilaquiler-taskero:**
- **Servicios:** Se implementarán servicios para manejar la lógica de negocio asociada a tareas, proyectos, usuarios, etc.

**Ejemplo:**

```java
@Service
public class TaskService {

    @Autowired
    private TaskRepository taskRepository;

    public TaskDTO getTaskById(Long id) {
        Task task = taskRepository.findById(id).orElseThrow(() -> new ResourceNotFoundException("Task not found"));
        return new TaskDTO(task);
    }

    // Otros métodos de servicio
}
```

---

### **2.4 Patrón DTO (Data Transfer Object)**

**Descripción:**  
El patrón DTO se utiliza para transferir datos entre capas de la aplicación. Los DTOs son objetos simples que contienen solo datos, sin lógica de negocio, y se utilizan para transportar datos desde el backend al frontend, o entre capas del backend.

**Aplicación en chilaquiler-taskero:**
- **DTOs:** Se utilizarán DTOs para representar las tareas, proyectos y usuarios al transferir datos entre el backend y el frontend.

**Ejemplo:**

```java
public class TaskDTO {

    private Long id;
    private String title;
    private String description;
    private String status;
    private Date dueDate;

    // Constructores, getters y setters
}
```

---

### **2.5 Patrón Mapper**

**Descripción:**  
El patrón Mapper se utiliza para convertir objetos de un tipo a otro, como convertir entidades JPA a DTOs y viceversa. Esto simplifica la lógica en las capas de servicio y controlador, manteniendo el código limpio y organizado.

**Aplicación en chilaquiler-taskero:**
- **MapStruct:** Se utilizará MapStruct como la herramienta principal para implementar mappers, automatizando la conversión entre entidades y DTOs.

**Ejemplo:**

```java
@Mapper(componentModel = "spring")
public interface TaskMapper {

    TaskDTO toTaskDTO(Task task);

    Task toTask(TaskDTO taskDTO);
}
```

---

### **2.6 Patrón Decorator**

**Descripción:**  
El patrón Decorator se utiliza para añadir funcionalidad a objetos de manera flexible y reutilizable. Permite envolver un objeto existente con nuevas funcionalidades sin modificar su estructura original.

**Aplicación en chilaquiler-taskero:**
- **Decorators en Servicios:** Los decorators se pueden usar para añadir funcionalidades adicionales a los servicios, como logging, validaciones adicionales, o transformaciones antes de ejecutar la lógica principal.

**Ejemplo:**

```java
@Service
public class LoggingTaskServiceDecorator implements TaskService {

    private final TaskService delegate;

    public LoggingTaskServiceDecorator(TaskService delegate) {
        this.delegate = delegate;
    }

    @Override
    public TaskDTO getTaskById(Long id) {
        System.out.println("Fetching task with ID: " + id);
        return delegate.getTaskById(id);
    }

    // Otros métodos decorados
}
```

---

## **3. Patrones de Diseño en el Frontend**

### **3.1 Patrón Component-Based Architecture**

**Descripción:**  
Angular utiliza una arquitectura basada en componentes, donde la interfaz de usuario se divide en pequeñas partes reutilizables llamadas componentes. Cada componente encapsula su propio comportamiento, estado y plantilla.

**Aplicación en chilaquiler-taskero:**
- **Componentes:** Cada funcionalidad principal (como la lista de tareas, la vista de proyectos, etc.) se implementará como un componente independiente.

**Ejemplo:**

```typescript
@Component({
  selector: 'app-task-list',
  templateUrl: './task-list.component.html',
  styleUrls: ['./task-list.component.scss']
})
export class TaskListComponent {
  @Input() tasks: Task[];

  constructor() { }
}
```

---

### **3.2 Patrón Service Layer (Capa de Servicio en Angular)**

**Descripción:**  
En Angular, los servicios se utilizan para compartir datos y lógica de negocio entre componentes. El patrón Service Layer separa la lógica de negocio del manejo de la interfaz, promoviendo la reutilización y un código más limpio.

**Aplicación en chilaquiler-taskero:**
- **Servicios Angular:** Se implementarán servicios para manejar la lógica relacionada con la gestión de tareas, autenticación de usuarios, etc.

**Ejemplo:**

```typescript
@Injectable({
  providedIn: 'root'
})
export class TaskService {

  constructor(private http: HttpClient) { }

  getTasks(): Observable<Task[]> {
    return this.http.get<Task[]>('/api/tasks');
  }

  // Otros métodos del servicio
}
```

---

### **3.3 Patrón Observables y RXJS**

**Descripción:**  
Angular utiliza observables para manejar asincronismo, flujos de datos y eventos. RXJS proporciona un conjunto de operadores para trabajar con observables, permitiendo una manipulación fluida y eficiente de flujos de datos.

**Aplicación en chilaquiler-taskero:**
- **Observables:** Se utilizarán para manejar llamadas HTTP, formularios reactivos, y otros flujos de datos asíncronos.

**Ejemplo:**

```typescript
this.taskService.getTasks().subscribe(tasks => {
  this.tasks = tasks;
});
```

---

### **3.4 Patrón Dependency Injection (DI)**

**Descripción:**  
Angular utiliza inyección de dependencias para proporcionar instancias de servicios y otros objetos a los componentes de la aplicación. Esto permite la separación de responsabilidades y facilita las pruebas unitarias.

**Aplicación en chilaquiler-taskero:**
- **Inyección de Servicios:** Los servicios y otras dependencias serán inyectados en los componentes según sea necesario, utilizando el sistema de inyección de dependencias de Angular.

**Ejemplo:**

```typescript
@Component({
  selector: 'app-task-list',
  templateUrl: './task-list.component.html',
  styleUrls: ['./task-list.component.scss']
})
export class TaskListComponent {

  constructor(private taskService: TaskService) { }

  ngOnInit() {
    this.taskService.getTasks().subscribe(tasks => {
      this.tasks = tasks;
    });
  }
}
```

---

## **4. Conclusión**

La implementación de estos patrones de diseño en **chilaquiler-taskero** asegura que el código sea limpio, modular, mantenible y extensible. El

 uso de mappers y decorators en Java permitirá una conversión y enriquecimiento de objetos eficiente y reutilizable, lo que mejorará la calidad del código y la flexibilidad del sistema. Este documento servirá como guía para todos los desarrolladores, asegurando que las mejores prácticas se sigan consistentemente a lo largo del desarrollo del proyecto.

---

**Revisión y Aprobación:**

- [ ] Revisado por: [Nombre del revisor]
- [ ] Aprobado por: [Nombre del aprobador]
- Fecha de Revisión: [Fecha]
- Fecha de Aprobación: [Fecha]