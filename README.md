# API ForoHub

API desarrollada con Spring Boot para la gestión de tópicos en un foro, con autenticación mediante JWT. Incluye funcionalidades CRUD y control de acceso seguro para usuarios autenticados.

---

## **Tecnologías Utilizadas**

- **Java 17**
- **Spring Boot 3.4**
- **Maven**
- **Lombok**
- **Spring Web**
- **Spring Data JPA**
- **Flyway Migration**
- **MySQL**
- **Spring Security**
- **JSON Web Tokens (JWT)**

---

## **Requisitos**

1. **Java 17** o superior.
2. **MySQL** configurado localmente o en la nube.
3. **Postman** o herramienta similar para probar los endpoints.

---

## **Estructura de la Base de Datos**

### Tabla `topico`
| Campo           | Tipo        | Descripción                     |
|------------------|-------------|---------------------------------|
| `id`            | BIGINT      | Identificador único             |
| `titulo`        | VARCHAR(255)| Título del tópico               |
| `mensaje`       | TEXT        | Contenido del tópico            |
| `fecha_creacion`| DATETIME    | Fecha de creación del tópico    |
| `status`        | ENUM        | Estado del tópico (Ej. ACTIVO)  |
| `autor_id`      | BIGINT      | Relación con la tabla `usuario` |
| `curso_id`      | BIGINT      | Relación con la tabla `curso`   |

### Tabla `usuario`
| Campo           | Tipo        | Descripción                     |
|------------------|-------------|---------------------------------|
| `id`            | BIGINT      | Identificador único             |
| `nombre`        | VARCHAR(255)| Nombre del usuario              |
| `email`         | VARCHAR(255)| Correo electrónico              |
| `password`      | VARCHAR(255)| Contraseña del usuario          |

### Tabla `curso`
| Campo           | Tipo        | Descripción                     |
|------------------|-------------|---------------------------------|
| `id`            | BIGINT      | Identificador único             |
| `nombre`        | VARCHAR(255)| Nombre del curso                |
| `categoria`     | VARCHAR(255)| Categoría del curso             |

---

## **Endpoints**

### **Autenticación**
1. **POST /login**  
   - **Descripción**: Genera un token JWT para el usuario autenticado.
   - **Cuerpo**:
     ```json
     {
       "email": "usuario@correo.com",
       "password": "contraseña"
     }
     ```

2. **POST /usuarios**
   - **Descripción**: Registra un nuevo usuario.
   - **Cuerpo**:
     ```json
     {
       "nombre": "Usuario Ejemplo",
       "email": "usuario@correo.com",
       "password": "contraseña"
     }
     ```

---

### **Tópicos**
1. **POST /topicos**
   - **Descripción**: Crea un nuevo tópico.
   - **Cuerpo**:
     ```json
     {
       "titulo": "Título del tópico",
       "mensaje": "Contenido del tópico",
       "cursoId": 1
     }
     ```
   - **Respuesta**:
     ```json
     {
       "id": 1,
       "titulo": "Título del tópico",
       "mensaje": "Contenido del tópico",
       "fecha_creacion": "2024-01-01T12:00:00",
       "status": "ACTIVO",
       "autor": "Usuario Ejemplo",
       "curso": "Curso de Java"
     }
     ```

2. **GET /topicos**
   - **Descripción**: Lista todos los tópicos registrados.

3. **GET /topicos/{id}**
   - **Descripción**: Obtiene el detalle de un tópico por ID.

4. **PUT /topicos/{id}**
   - **Descripción**: Actualiza un tópico existente.
   - **Cuerpo**:
     ```json
     {
       "titulo": "Nuevo título",
       "mensaje": "Nuevo contenido"
     }
     ```

5. **DELETE /topicos/{id}**
   - **Descripción**: Elimina un tópico por ID.

---

### **Seguridad y Autenticación**

- La API utiliza **JWT** para la autenticación.
- Para acceder a los endpoints protegidos, incluye el token JWT en el encabezado de las solicitudes:



---

## **Configuración Inicial**

1. **Configurar MySQL**
 - Crear una base de datos llamada `foro_hub`.

2. **Configurar el archivo `application.properties`**
 ```properties
 spring.datasource.url=jdbc:mysql://localhost:3306/foro_hub
 spring.datasource.username=tu_usuario
 spring.datasource.password=tu_contraseña
 spring.jpa.hibernate.ddl-auto=validate

 # Configuración JWT
 jwt.secret=mi_clave_secreta
 jwt.expiration=86400000


mvn spring-boot:run
