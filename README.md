# Sistema de Reservas de Hotel 🏨  

Este proyecto gestiona reservas, habitaciones y clientes de un hotel mediante una base de datos relacional.  

## Objetivos del Proyecto  
1. Modelar una base de datos para operaciones hoteleras.  
2. Mantener integridad en reservas y disponibilidad.  
3. Optimizar consultas de ocupación y estadías.  

## Tecnologías Utilizadas  
- MySQL / PostgreSQL / SQLite  
- SQL estándar  

> *"Un buen sistema de reservas es clave para la satisfacción del huésped."*  

![Modelo DB para hotel](descarga.png)  

## Estructura SQL  

```sql
-- Tabla de Habitaciones  
CREATE TABLE Habitaciones (  
    id_habitacion INT PRIMARY KEY,  
    numero VARCHAR(10) UNIQUE,  
    tipo ENUM('Individual', 'Doble', 'Suite', 'Familiar'),  
    capacidad INT NOT NULL,  
    precio_noche DECIMAL(10,2) CHECK (precio_noche > 0),  
    estado ENUM('Disponible', 'Ocupada', 'Mantenimiento')  
);  

-- Tabla de Clientes  
CREATE TABLE Clientes (  
    id_cliente INT AUTO_INCREMENT PRIMARY KEY,  
    nombre VARCHAR(100) NOT NULL,  
    email VARCHAR(100) UNIQUE,  
    telefono VARCHAR(20),  
    documento VARCHAR(20) UNIQUE  
);  

-- Tabla de Reservas  
CREATE TABLE Reservas (  
    id_reserva INT AUTO_INCREMENT PRIMARY KEY,  
    id_habitacion INT,  
    id_cliente INT,  
    fecha_entrada DATE NOT NULL,  
    fecha_salida DATE NOT NULL,  
    estado ENUM('Confirmada', 'Cancelada', 'En curso', 'Finalizada'),  
    FOREIGN KEY (id_habitacion) REFERENCES Habitaciones(id_habitacion),  
    FOREIGN KEY (id_cliente) REFERENCES Clientes(id_cliente),  
    CHECK (fecha_salida > fecha_entrada)  
);  

-- Tabla de Servicios Adicionales  
CREATE TABLE Servicios (  
    id_servicio INT AUTO_INCREMENT PRIMARY KEY,  
    nombre VARCHAR(50) NOT NULL,  
    precio DECIMAL(10,2) CHECK (precio >= 0)  
);  

-- Tabla de Servicios por Reserva  
CREATE TABLE Servicios_Reserva (  
    id INT AUTO_INCREMENT PRIMARY KEY,  
    id_reserva INT,  
    id_servicio INT,  
    fecha DATE NOT NULL,  
    cantidad INT DEFAULT 1,  
    FOREIGN KEY (id_reserva) REFERENCES Reservas(id_reserva),  
    FOREIGN KEY (id_servicio) REFERENCES Servicios(id_servicio)  
);  
