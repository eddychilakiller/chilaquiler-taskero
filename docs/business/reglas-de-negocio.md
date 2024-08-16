### Documento 3: Reglas de Negocio para **chilaquiler-taskero**

---

**Nombre del Proyecto:** chilaquiler-taskero  
**Versión:** 1.0  
**Fecha:** [Fecha de creación del documento]  
**Autor:** [Tu nombre o equipo]

---

## **1. Introducción**

Las reglas de negocio de **chilaquiler-taskero** establecen las normas y restricciones que guiarán el comportamiento del sistema, asegurando que todas las operaciones dentro de la aplicación se realicen de acuerdo con los objetivos del proyecto y las expectativas de los usuarios. Este documento detalla las reglas que deben ser implementadas para mantener la coherencia, seguridad y funcionalidad del sistema.

### **1.1 Objetivo de las Reglas de Negocio**

El objetivo de las reglas de negocio es:
- **Garantizar la integridad de los datos** al aplicar validaciones estrictas en todas las interacciones del usuario.
- **Asegurar el cumplimiento de la metodología GTD**, facilitando la organización y gestión de tareas de acuerdo con los principios establecidos.
- **Proporcionar una experiencia de usuario segura y consistente** mediante la implementación de reglas claras y predecibles.

---

## **2. Reglas de Validación**

### **2.1 Validación de Tareas**

**Regla 1: Título de Tarea Obligatorio**  
- **Descripción:** Todas las tareas deben tener un título no vacío.
- **Implementación:** El sistema debe validar que el campo título no esté vacío antes de permitir la creación de una tarea.
- **Error si no se cumple:** "El título de la tarea es obligatorio."

**Regla 2: Longitud Máxima del Título**  
- **Descripción:** El título de una tarea no debe exceder los 100 caracteres.
- **Implementación:** El sistema debe truncar cualquier título que exceda esta longitud o mostrar un mensaje de error.
- **Error si no se cumple:** "El título de la tarea no puede exceder los 100 caracteres."

**Regla 3: Descripción Opcional**  
- **Descripción:** La descripción de la tarea es opcional, pero si se proporciona, no debe exceder los 500 caracteres.
- **Implementación:** El sistema debe truncar o rechazar descripciones que excedan esta longitud.
- **Error si no se cumple:** "La descripción de la tarea no puede exceder los 500 caracteres."

### **2.2 Validación de Fechas**

**Regla 4: Fecha de Creación Automática**  
- **Descripción:** La fecha de creación de una tarea debe ser generada automáticamente por el sistema y no debe ser modificable por el usuario.
- **Implementación:** El sistema debe registrar la fecha y hora de creación cuando la tarea es guardada por primera vez.

**Regla 5: Fecha Límite Opcional y Válida**  
- **Descripción:** La fecha límite de una tarea es opcional, pero si se establece, no puede ser una fecha pasada.
- **Implementación:** El sistema debe validar que la fecha límite no sea anterior a la fecha actual.
- **Error si no se cumple:** "La fecha límite no puede ser en el pasado."

**Regla 6: Recordatorios Antes de la Fecha Límite**  
- **Descripción:** Los recordatorios de las tareas deben configurarse para ocurrir antes de la fecha límite.
- **Implementación:** El sistema debe validar que cualquier recordatorio se programe para una fecha anterior a la fecha límite establecida.
- **Error si no se cumple:** "El recordatorio debe ser antes de la fecha límite."

### **2.3 Validación de Contextos y Etiquetas**

**Regla 7: Asignación de Contexto Opcional**  
- **Descripción:** El contexto de una tarea es opcional, pero si se asigna, debe ser uno de los contextos predefinidos por el usuario.
- **Implementación:** El sistema debe validar que cualquier contexto asignado esté dentro de la lista de contextos definidos por el usuario.
- **Error si no se cumple:** "El contexto asignado no es válido."

**Regla 8: Etiquetas Múltiples Permitidas**  
- **Descripción:** Una tarea puede tener múltiples etiquetas, pero no debe haber duplicados.
- **Implementación:** El sistema debe eliminar etiquetas duplicadas al guardar una tarea.
- **Error si no se cumple:** "Las etiquetas duplicadas no están permitidas."

### **2.4 Validación de Proyectos**

**Regla 9: Asignación a un Proyecto Opcional**  
- **Descripción:** Las tareas pueden (pero no están obligadas) a ser asignadas a un proyecto. Si se asigna, el proyecto debe existir.
- **Implementación:** El sistema debe validar que cualquier proyecto asignado esté registrado en la base de datos.
- **Error si no se cumple:** "El proyecto asignado no existe."

**Regla 10: Tareas Únicas dentro de un Proyecto**  
- **Descripción:** Dentro de un proyecto, no deben existir dos tareas con el mismo título.
- **Implementación:** El sistema debe validar que no se creen tareas duplicadas dentro de un mismo proyecto.
- **Error si no se cumple:** "Ya existe una tarea con este título en el proyecto."

---

## **3. Reglas de Seguridad**

### **3.1 Autenticación y Autorización**

**Regla 11: Autenticación Obligatoria**  
- **Descripción:** Todos los usuarios deben autenticarse antes de acceder al sistema.
- **Implementación:** El sistema debe validar el JWT (JSON Web Token) en cada solicitud para verificar la autenticidad del usuario.
- **Error si no se cumple:** "Autenticación requerida."

**Regla 12: Gestión de Roles**  
- **Descripción:** El sistema debe gestionar diferentes niveles de acceso basados en roles (ej. Usuario, Administrador).
- **Implementación:** Las rutas y acciones deben ser protegidas según el rol del usuario autenticado.
- **Error si no se cumple:** "No tienes permisos suficientes para realizar esta acción."

### **3.2 Protección de Datos**

**Regla 13: Encriptación de Contraseñas**  
- **Descripción:** Todas las contraseñas de usuario deben ser encriptadas antes de ser almacenadas en la base de datos.
- **Implementación:** Utilizar algoritmos de hashing seguros (como bcrypt) para encriptar las contraseñas.
- **Error si no se cumple:** "Error en la gestión de la contraseña."

**Regla 14: Control de Sesiones**  
- **Descripción:** Las sesiones de usuario deben expirar después de un tiempo de inactividad definido (ej. 30 minutos).
- **Implementación:** Implementar control de expiración de sesiones a través del manejo del JWT.
- **Error si no se cumple:** "Sesión expirada. Por favor, inicia sesión nuevamente."

**Regla 15: Protección contra CSRF**  
- **Descripción:** Implementar protección contra ataques CSRF (Cross-Site Request Forgery) en todas las solicitudes sensibles.
- **Implementación:** Utilizar tokens CSRF en formularios y solicitudes POST.
- **Error si no se cumple:** "Token CSRF no válido."

---

## **4. Reglas de Gestión de Tareas**

### **4.1 Estados de Tareas**

**Regla 16: Estados Permitidos de una Tarea**  
- **Descripción:** Una tarea puede estar en uno de los siguientes estados: Pendiente, En Proceso, Completada, Delegada, Aplazada.
- **Implementación:** El sistema debe validar que una tarea solo cambie a un estado permitido.
- **Error si no se cumple:** "Estado de tarea no válido."

**Regla 17: Transición de Estados**  
- **Descripción:** Las tareas deben seguir una secuencia lógica en su transición de estados (ej. de Pendiente a En Proceso, luego a Completada).
- **Implementación:** El sistema debe validar la secuencia de transición entre estados.
- **Error si no se cumple:** "Transición de estado no permitida."

### **4.2 Gestión de Prioridades**

**Regla 18: Prioridades Predefinidas**  
- **Descripción:** Las tareas pueden tener uno de los siguientes niveles de prioridad: Baja, Media, Alta.
- **Implementación:** El sistema debe permitir solo estos valores de prioridad al crear o editar una tarea.
- **Error si no se cumple:** "Prioridad no válida."

**Regla 19: Cambio de Prioridad**  
- **Descripción:** El usuario puede cambiar la prioridad de una tarea en cualquier momento.
- **Implementación:** El sistema debe permitir el cambio de prioridad y reflejarlo en la ordenación de las listas.
- **Error si no se cumple:** "No se pudo cambiar la prioridad de la tarea."

---

## **5. Reglas de Notificaciones**

### **5.1 Configuración de Notificaciones**

**Regla 20: Notificaciones Programables**  
- **Descripción:** Los usuarios pueden configurar notificaciones para recibir alertas sobre tareas específicas.
- **Implementación:** El sistema debe permitir la configuración de recordatorios antes de la fecha límite de la tarea.
- **Error si no se cumple:** "No se pudo programar la notificación."

**Regla 21: Desactivación de Notificaciones**  
- **Descripción:** Los usuarios pueden desactivar notificaciones para tareas individuales o globalmente.
- **Implementación:** El sistema debe ofrecer opciones de configuración para activar/desactivar notificaciones.
- **Error si no se cumple:** "No se pudo cambiar la configuración de notificaciones."

### **5.2 Envío de Notificaciones**

**Regla 22: Envío de Recordatorios**  
- **Descripción:** El sistema debe enviar

 recordatorios según la configuración del usuario, a través de correo electrónico o notificaciones push.
- **Implementación:** Utilizar servicios de notificación para enviar alertas en los momentos programados.
- **Error si no se cumple:** "No se pudo enviar el recordatorio."

**Regla 23: Notificación de Tareas Vencidas**  
- **Descripción:** El sistema debe notificar al usuario cuando una tarea ha vencido.
- **Implementación:** Programar notificaciones automáticas para tareas cuya fecha límite haya pasado.
- **Error si no se cumple:** "No se pudo enviar la notificación de tarea vencida."

---

## **6. Conclusión**

Las reglas de negocio definidas para **chilaquiler-taskero** son fundamentales para garantizar que el sistema opere de manera coherente, segura y eficiente. Estas reglas deben ser implementadas rigurosamente en el desarrollo para asegurar que la experiencia del usuario esté alineada con las expectativas y principios establecidos.

---

**Revisión y Aprobación:**

- [ ] Revisado por: [Nombre del revisor]
- [ ] Aprobado por: [Nombre del aprobador]
- Fecha de Revisión: [Fecha]
- Fecha de Aprobación: [Fecha]