### 2.1: Introducción al TDD (Test-Driven Development)

#### **2.1 Introducción al TDD**

El Desarrollo Guiado por Pruebas, conocido como TDD (Test-Driven Development), es una práctica de desarrollo de software en la que las pruebas unitarias se escriben antes del código de producción. El proceso de TDD sigue un ciclo repetitivo de tres pasos: **Red**, **Green** y **Refactor**. Este enfoque no solo ayuda a escribir código más limpio y libre de errores, sino que también asegura que el código esté siempre cubierto por pruebas automáticas, facilitando la detección de errores y garantizando la calidad del software.

---

### **¿Qué es TDD?**

TDD es una metodología de desarrollo que se enfoca en la creación de pruebas antes de implementar la funcionalidad del código. En lugar de escribir código primero y luego agregar pruebas, TDD invierte este proceso, lo que permite al desarrollador concentrarse en los requisitos y el diseño antes de escribir una sola línea de código de producción.

### **El Ciclo TDD: Red, Green, Refactor**

1. **Red (Escribir una Prueba que Falla)**:
   - El primer paso en TDD es escribir una prueba automatizada para una nueva funcionalidad o una mejora a la funcionalidad existente. 
   - Esta prueba debe fallar inicialmente porque la funcionalidad aún no ha sido implementada.
   - Es importante comenzar con pruebas simples que se centren en una pequeña parte del comportamiento esperado.
   - **Ejemplo**: Si estamos implementando un método que suma dos números, la primera prueba podría ser comprobar si la suma de 2 + 2 es igual a 4.
   
   ```java
   @Test
   void testSum() {
       Calculator calculator = new Calculator();
       int result = calculator.add(2, 2);
       assertEquals(4, result);
   }
   ```

   - **Resultado**: La prueba debe fallar porque el método `add` no ha sido implementado.

2. **Green (Escribir el Código Mínimo para Pasar la Prueba)**:
   - El siguiente paso es escribir el código más simple posible que haga que la prueba escrita anteriormente pase.
   - En esta fase, la prioridad es hacer que la prueba sea exitosa, sin preocuparse demasiado por la elegancia o la eficiencia del código.
   - **Ejemplo**: Implementamos el método `add` en la clase `Calculator` para que la prueba pase.

   ```java
   public class Calculator {
       public int add(int a, int b) {
           return a + b;
       }
   }
   ```

   - **Resultado**: La prueba ahora debería pasar exitosamente, mostrando que el código cumple con la funcionalidad básica requerida.

3. **Refactor (Mejorar el Código Respetando la Prueba)**:
   - Una vez que la prueba pasa, el siguiente paso es refactorizar el código para mejorar su estructura, legibilidad y eficiencia, sin cambiar su comportamiento.
   - Las pruebas existentes actúan como una red de seguridad, asegurando que las mejoras en el código no rompan la funcionalidad existente.
   - **Ejemplo**: Si después de implementar el método `add`, notamos que se puede optimizar o simplificar el código, realizamos los cambios necesarios y volvemos a ejecutar la prueba para asegurarnos de que todavía pase.
   
   ```java
   public class Calculator {
       // En este caso, el código es lo suficientemente simple y no necesita refactorización
       public int add(int a, int b) {
           return a + b;
       }
   }
   ```

   - **Resultado**: El código ahora es más limpio o más eficiente, y todas las pruebas siguen pasando.

### **Beneficios de TDD**

1. **Mayor Confianza en el Código**:
   - TDD permite escribir código con un alto grado de confianza, ya que cada nueva funcionalidad se implementa con una prueba automatizada que garantiza que el código funciona como se espera.

2. **Diseño de Código Mejorado**:
   - Al escribir las pruebas antes que el código, los desarrolladores tienden a pensar más en la interfaz y el diseño del código, lo que generalmente resulta en un diseño más limpio y modular.

3. **Prevención de Errores**:
   - TDD ayuda a prevenir errores antes de que lleguen al código de producción, reduciendo la cantidad de bugs y facilitando el mantenimiento del software.

4. **Facilita el Refactoring**:
   - Con un conjunto de pruebas automatizadas, los desarrolladores pueden refactorizar el código con confianza, sabiendo que cualquier cambio que rompa la funcionalidad será capturado por las pruebas.

5. **Documentación Viva**:
   - Las pruebas actúan como documentación viva del comportamiento del sistema. Otros desarrolladores pueden revisar las pruebas para entender cómo se espera que funcione el código.

### **Mejores Prácticas para Implementar TDD**

1. **Escribir Pruebas Simples y Focalizadas**:
   - Cada prueba debe enfocarse en un aspecto específico del comportamiento del código. Esto facilita la detección de errores y mantiene las pruebas manejables.

2. **Mantener el Ciclo TDD Corto**:
   - Intenta completar el ciclo Red-Green-Refactor lo más rápido posible. Ciclos cortos y frecuentes facilitan la detección de problemas y aseguran un desarrollo más ágil.

3. **No Saltarse la Fase de Refactorización**:
   - La refactorización es clave para mantener el código limpio y eficiente. No omitas este paso, ya que es esencial para la calidad del software.

4. **Automatizar la Ejecución de Pruebas**:
   - Integra las pruebas en el pipeline de CI/CD para que se ejecuten automáticamente cada vez que se realicen cambios en el código, garantizando que el código siempre esté cubierto por pruebas.

5. **Escribir Pruebas Antes de Corregir Bugs**:
   - Antes de corregir un bug, escribe una prueba que demuestre la existencia del problema. Luego, corrige el código para hacer que la prueba pase, asegurando que el bug no reaparezca en el futuro.

### **TDD en el Contexto de chilaquiler-taskero**

En el proyecto **chilaquiler-taskero**, TDD será una herramienta fundamental para asegurar que el gestor de tareas basado en GTD funcione correctamente y cumpla con los requisitos definidos. Aplicaremos TDD tanto en el backend, utilizando frameworks como JUnit y Mockito, como en el frontend con herramientas como Jasmine y Karma. Esto garantizará que cada funcionalidad del proyecto esté respaldada por pruebas automatizadas, manteniendo el código limpio, modular y fácil de mantener.

#### **Ejemplo Práctico en chilaquiler-taskero:**

Supongamos que queremos implementar la funcionalidad de agregar una tarea en el gestor de tareas. El ciclo TDD sería el siguiente:

1. **Red**:
   - Escribimos una prueba que verifica que una nueva tarea se agrega correctamente al sistema.
   
   ```java
   @Test
   void testAddTask() {
       TaskService taskService = new TaskService();
       Task task = new Task("Comprar leche");
       taskService.addTask(task);
       assertTrue(taskService.getTasks().contains(task));
   }
   ```

   - Esta prueba fallará porque `addTask` aún no está implementado.

2. **Green**:
   - Implementamos el método `addTask` para que la prueba pase.

   ```java
   public class TaskService {
       private List<Task> tasks = new ArrayList<>();

       public void addTask(Task task) {
           tasks.add(task);
       }

       public List<Task> getTasks() {
           return tasks;
       }
   }
   ```

   - Ahora, la prueba debería pasar.

3. **Refactor**:
   - Revisamos el código para ver si hay mejoras que podamos hacer, como asegurar que la lista de tareas sea inmutable o aplicar patrones de diseño para una mejor estructura.

   ```java
   public class TaskService {
       private List<Task> tasks = new ArrayList<>();

       public void addTask(Task task) {
           tasks.add(task);
       }

       public List<Task> getTasks() {
           return Collections.unmodifiableList(tasks);
       }
   }
   ```

   - Después de la refactorización, volvemos a ejecutar las pruebas para asegurarnos de que todo sigue funcionando correctamente.

---

### **Ubicación de la Documentación en el Proyecto**

Esta documentación sobre TDD puede ser colocada en la carpeta `docs/tutorials/step-by-step` del proyecto, bajo un archivo llamado `03-introduccion-TDD.md`. De esta manera, los desarrolladores y participantes del taller tendrán acceso a una guía clara y detallada sobre TDD y cómo aplicarlo en el proyecto **chilaquiler-taskero**.

```bash
chilaquiler-taskero/
│
├── docs/
│   ├── tutorials/
│   │   ├── step-by-step/
│   │   │   ├── 01-instalacion-entorno-mac.md   # Documentación del punto 1.1
│   │   │   ├── 02-creacion-proyecto.md         # Documentación del punto 1.2
│   │   │   ├── 03-introduccion-TDD.md          # Documentación del punto 2.1
│   │   │   └── ...                             # Otros archivos de la guía paso a paso
│   │   └── ...
│   └── ...
```

Este archivo proporcionará una base sólida sobre TDD, explicando tanto los conceptos como las prácticas

 que se aplicarán durante el desarrollo del proyecto.