# Sistema de Gestión de Biblioteca 📚

Este proyecto tiene como objetivo diseñar y desarrollar una base de datos relacional para gestionar eficientemente los recursos de una biblioteca, incluyendo libros, usuarios y préstamos.

## Objetivos del Proyecto

1. Crear un modelo de base de datos que refleje las operaciones clave de una biblioteca.
2. Implementar tablas y relaciones que aseguren integridad referencial.
3. Facilitar consultas eficientes para el seguimiento de préstamos y disponibilidad de libros.

## Tecnologías Utilizadas

- MySQL
- PostgreSQL
- SQLite
- SQL estándar

> "Una biblioteca es un hospital para la mente." — Anonymous

Consulta este recurso sobre diseño de bases de datos para bibliotecas en [Vertabelo Database Modeler](https://vertabelo.com/blog/database-for-library-system/).

![Modelo de base de datos para biblioteca](https://vertabelo.com/blog/wp-content/uploads/2016/04/library-database-model.png)

## Ejemplo de Código

```sql
CREATE TABLE Libros (
    id_libro INT PRIMARY KEY,
    titulo VARCHAR(100),
    autor VARCHAR(100),
    año_publicacion INT,
    disponible BOOLEAN
);

CREATE TABLE Usuarios (
    id_usuario INT PRIMARY KEY,
    nombre VARCHAR(100),
    correo VARCHAR(100)
);

CREATE TABLE Prestamos (
    id_prestamo INT PRIMARY KEY,
    id_libro INT,
    id_usuario INT,
    fecha_prestamo DATE,
    fecha_devolucion DATE,
    FOREIGN KEY (id_libro) REFERENCES Libros(id_libro),
    FOREIGN KEY (id_usuario) REFERENCES Usuarios(id_usuario)
);
