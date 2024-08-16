### Documento: Especificación de la API para **chilaquiler-taskero**

---

**Nombre del Proyecto:** chilaquiler-taskero  
**Versión:** 1.0  
**Fecha:** [Fecha de creación del documento]  
**Autor:** [Tu nombre o equipo]

---

## **1. Introducción**

Este documento describe la especificación de la API REST para **chilaquiler-taskero**. La API permitirá la interacción entre el frontend y el backend, facilitando la gestión de tareas, proyectos y usuarios. La especificación incluye los endpoints principales, los métodos HTTP utilizados, las estructuras de los cuerpos de las solicitudes y las respuestas, y los códigos de estado esperados.

### **1.1 Objetivo del Documento**

El objetivo de este documento es:
- Proporcionar una guía detallada sobre los endpoints de la API.
- Asegurar que las interacciones entre el frontend y el backend sean coherentes y eficientes.
- Facilitar la implementación y prueba de la API mediante una especificación clara y precisa.

---

## **2. Endpoints de la API**

### **2.1 `/api/tasks`**

**Descripción:**  
Maneja la creación, actualización, obtención y eliminación de tareas.

**Operaciones:**

- **GET `/api/tasks`**
  - **Descripción:** Obtiene todas las tareas del usuario autenticado.
  - **Respuesta:**
    - **Código 200:** Lista de tareas.
    - **Cuerpo:**
      ```json
      [
        {
          "id": 1,
          "title": "Comprar leche",
          "description": "Comprar leche en el supermercado",
          "status": "PENDING",
          "dueDate": "2024-08-21T10:00:00Z",
          "projectId": 2,
          "context": "@Casa"
        },
        // Otras tareas...
      ]
      ```

- **GET `/api/tasks/{id}`**
  - **Descripción:** Obtiene los detalles de una tarea específica.
  - **Parámetros:**
    - `id` (path): ID de la tarea a obtener.
  - **Respuesta:**
    - **Código 200:** Detalles de la tarea.
    - **Cuerpo:**
      ```json
      {
        "id": 1,
        "title": "Comprar leche",
        "description": "Comprar leche en el supermercado",
        "status": "PENDING",
        "dueDate": "2024-08-21T10:00:00Z",
        "projectId": 2,
        "context": "@Casa"
      }
      ```
    - **Código 404:** Tarea no encontrada.

- **POST `/api/tasks`**
  - **Descripción:** Crea una nueva tarea.
  - **Cuerpo de la Solicitud:**
    ```json
    {
      "title": "Comprar leche",
      "description": "Comprar leche en el supermercado",
      "dueDate": "2024-08-21T10:00:00Z",
      "projectId": 2,
      "context": "@Casa"
    }
    ```
  - **Respuesta:**
    - **Código 201:** Tarea creada exitosamente.
    - **Cuerpo:**
      ```json
      {
        "id": 1,
        "title": "Comprar leche",
        "description": "Comprar leche en el supermercado",
        "status": "PENDING",
        "dueDate": "2024-08-21T10:00:00Z",
        "projectId": 2,
        "context": "@Casa"
      }
      ```

- **PUT `/api/tasks/{id}`**
  - **Descripción:** Actualiza una tarea existente.
  - **Parámetros:**
    - `id` (path): ID de la tarea a actualizar.
  - **Cuerpo de la Solicitud:**
    ```json
    {
      "title": "Comprar leche y pan",
      "description": "Comprar leche y pan en el supermercado",
      "dueDate": "2024-08-22T10:00:00Z",
      "status": "IN_PROGRESS"
    }
    ```
  - **Respuesta:**
    - **Código 200:** Tarea actualizada exitosamente.
    - **Código 404:** Tarea no encontrada.

- **DELETE `/api/tasks/{id}`**
  - **Descripción:** Elimina una tarea.
  - **Parámetros:**
    - `id` (path): ID de la tarea a eliminar.
  - **Respuesta:**
    - **Código 204:** Tarea eliminada exitosamente.
    - **Código 404:** Tarea no encontrada.

---

### **2.2 `/api/projects`**

**Descripción:**  
Maneja la creación, actualización, obtención y eliminación de proyectos.

**Operaciones:**

- **GET `/api/projects`**
  - **Descripción:** Obtiene todos los proyectos del usuario autenticado.
  - **Respuesta:**
    - **Código 200:** Lista de proyectos.
    - **Cuerpo:**
      ```json
      [
        {
          "id": 2,
          "name": "Proyecto Personal",
          "description": "Proyecto para tareas personales",
          "tasks": [
            {
              "id": 1,
              "title": "Comprar leche",
              "status": "PENDING"
            }
          ]
        }
      ]
      ```

- **GET `/api/projects/{id}`**
  - **Descripción:** Obtiene los detalles de un proyecto específico.
  - **Parámetros:**
    - `id` (path): ID del proyecto a obtener.
  - **Respuesta:**
    - **Código 200:** Detalles del proyecto.
    - **Cuerpo:**
      ```json
      {
        "id": 2,
        "name": "Proyecto Personal",
        "description": "Proyecto para tareas personales",
        "tasks": [
          {
            "id": 1,
            "title": "Comprar leche",
            "status": "PENDING"
          }
        ]
      }
      ```
    - **Código 404:** Proyecto no encontrado.

- **POST `/api/projects`**
  - **Descripción:** Crea un nuevo proyecto.
  - **Cuerpo de la Solicitud:**
    ```json
    {
      "name": "Proyecto Trabajo",
      "description": "Proyecto para tareas de trabajo"
    }
    ```
  - **Respuesta:**
    - **Código 201:** Proyecto creado exitosamente.
    - **Cuerpo:**
      ```json
      {
        "id": 3,
        "name": "Proyecto Trabajo",
        "description": "Proyecto para tareas de trabajo"
      }
      ```

- **PUT `/api/projects/{id}`**
  - **Descripción:** Actualiza un proyecto existente.
  - **Parámetros:**
    - `id` (path): ID del proyecto a actualizar.
  - **Cuerpo de la Solicitud:**
    ```json
    {
      "name": "Proyecto Trabajo Actualizado",
      "description": "Descripción actualizada del proyecto"
    }
    ```
  - **Respuesta:**
    - **Código 200:** Proyecto actualizado exitosamente.
    - **Código 404:** Proyecto no encontrado.

- **DELETE `/api/projects/{id}`**
  - **Descripción:** Elimina un proyecto.
  - **Parámetros:**
    - `id` (path): ID del proyecto a eliminar.
  - **Respuesta:**
    - **Código 204:** Proyecto eliminado exitosamente.
    - **Código 404:** Proyecto no encontrado.

---

### **2.3 `/api/users`**

**Descripción:**  
Maneja la gestión de usuarios, incluyendo registro, autenticación, y obtención de perfiles.

**Operaciones:**

- **POST `/api/users/register`**
  - **Descripción:** Registra un nuevo usuario.
  - **Cuerpo de la Solicitud:**
    ```json
    {
      "username": "usuario123",
      "email": "usuario@example.com",
      "password": "contraseñaSegura"
    }
    ```
  - **Respuesta:**
    - **Código 201:** Usuario registrado exitosamente.
    - **Cuerpo:**
      ```json
      {
        "id": 5,
        "username": "usuario123",
        "email": "usuario@example.com"
      }
      ```
    - **Código 400:** Error en los datos de registro (por ejemplo, correo electrónico ya registrado).

- **POST `/api/users/login`**
  - **Descripción:** Autentica un usuario y genera un token JWT.
  - **Cuerpo de la Solicitud:**
    ```json
    {
      "email": "usuario@example.com",
      "password": "contraseñaSegura"
    }
    ```
  - **Respuesta:**
    - **Código 200:** Autenticación exitosa.
    - **Cuerpo:**
      ```json
      {
        "token": "jwt_token_generado"
      }
      ```
    - **Código 401:** Credenciales inválidas.

- **GET `/api/users/me`**
  - **Descripción:** Obtiene el perfil del usuario autenticado

.
  - **Respuesta:**
    - **Código 200:** Detalles del perfil del usuario.
    - **Cuerpo:**
      ```json
      {
        "id": 5,
        "username": "usuario123",
        "email": "usuario@example.com"
      }
      ```
    - **Código 401:** Usuario no autenticado.

---

## **3. Autenticación y Autorización**

### **3.1 Uso de JWT (JSON Web Tokens)**

- **Proceso de Autenticación:**
  1. El usuario se registra o inicia sesión a través de los endpoints `/api/users/register` o `/api/users/login`.
  2. Si la autenticación es exitosa, se genera un token JWT y se devuelve al cliente.
  3. El cliente debe incluir este token en el encabezado `Authorization: Bearer <token>` en todas las solicitudes subsecuentes.

- **Protección de Endpoints:**
  - Todos los endpoints, excepto `/api/users/register` y `/api/users/login`, requerirán un token JWT válido.
  - Los tokens serán verificados en cada solicitud, asegurando que el usuario esté autenticado antes de acceder a los recursos protegidos.

### **3.2 Manejo de Roles**

- **Roles de Usuario:**
  - El sistema manejará roles de usuario, como `USER` y `ADMIN`, para restringir el acceso a ciertos endpoints.
  - Los roles se definirán en el perfil del usuario y se utilizarán para autorizar acciones específicas dentro del sistema.

---

## **4. Códigos de Estado**

### **4.1 Códigos de Estado Comunes**

- **200 OK:** La solicitud fue exitosa y la respuesta contiene los datos solicitados.
- **201 Created:** El recurso fue creado exitosamente.
- **204 No Content:** La solicitud fue exitosa, pero no hay contenido en la respuesta (usualmente para eliminaciones).
- **400 Bad Request:** La solicitud es inválida (por ejemplo, datos incorrectos o mal formateados).
- **401 Unauthorized:** El usuario no está autenticado o el token JWT es inválido.
- **403 Forbidden:** El usuario no tiene permisos para realizar la acción solicitada.
- **404 Not Found:** El recurso solicitado no fue encontrado.
- **500 Internal Server Error:** Ocurrió un error inesperado en el servidor.

---

## **5. Conclusión**

La especificación de la API para **chilaquiler-taskero** proporciona una base sólida para la interacción entre el frontend y el backend. Este documento debe ser revisado y actualizado a medida que el desarrollo avance, asegurando que todos los componentes del sistema estén alineados y que las funcionalidades se implementen de manera coherente y eficiente.

---

**Revisión y Aprobación:**

- [ ] Revisado por: [Nombre del revisor]
- [ ] Aprobado por: [Nombre del aprobador]
- Fecha de Revisión: [Fecha]
- Fecha de Aprobación: [Fecha]
