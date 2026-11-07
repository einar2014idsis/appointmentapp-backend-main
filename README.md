# Appointment App | Backend

API académica para gestionar datos de una aplicación de salud, implementada con Java y Spring Boot. El proyecto Maven se encuentra en `appointmentapp-backend-main/`.

## Funcionalidades implementadas

- Operaciones REST de listado, consulta por identificador, creación, actualización y eliminación para pacientes, médicos, exámenes y especialidades.
- DTO, validaciones y conversión entre modelos y DTO con ModelMapper.
- Manejo centralizado de excepciones y ejemplo de respuesta HATEOAS para especialidades.
- Modelos JPA adicionales para consultas, recetas, productos, ventas, roles y usuarios. La presencia de un modelo no implica que tenga un endpoint terminado: los controladores de producto, categoría, familia y laboratorio están vacíos en esta rama.

## Tecnologías y arquitectura

Java 21, Spring Boot 3.5.5, Spring Web, Spring Data JPA/Hibernate, MySQL, Maven, Lombok, ModelMapper y Spring HATEOAS. El `pom.xml` también declara un controlador PostgreSQL; la configuración activa usa MySQL.

Dentro de `appointmentapp-backend-main/src/main/java/com/health/`, `controller/` recibe solicitudes, `service/` contiene servicios, `repository/` accede a datos, `model/` define entidades y `dto/` los objetos de intercambio. `exception/` concentra el manejo de errores. Las relaciones se definen en las entidades JPA.

## Endpoints

Los recursos `/patients`, `/medics`, `/exams` y `/specialties` exponen operaciones CRUD. Por ejemplo, `GET http://localhost:9090/patients` lista pacientes y `GET http://localhost:9090/specialties/hateoas/1` solicita una especialidad con enlaces. Consulta cada controlador para los cuerpos y respuestas exactos.

## Configuración y ejecución

Instala JDK 21, Maven y MySQL. Configura `spring.datasource.url`, usuario y contraseña en `src/main/resources/application.properties` o mediante variables de entorno; el puerto configurado es 9090 y `ddl-auto=update` permite que Hibernate actualice el esquema. Usa una base de desarrollo y revisa esta opción antes de aplicar cambios a datos existentes.

```bash
cd appointmentapp-backend-main
mvn spring-boot:run
```

En Windows también se incluye `mvnw.cmd`. Para pruebas: `mvn test`. El frontend relacionado requiere revisar las rutas y CORS: la configuración del cliente y los endpoints de esta rama deben coincidir. El código revisado no configura un esquema completo de autenticación y autorización; añádelo antes de tratar datos reales.
