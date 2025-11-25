# UIII-Act-7-models.py-DACA
# Imagen de las tablas
<img width="1182" height="596" alt="image" src="https://github.com/user-attachments/assets/b4254a71-aa0b-4337-bb00-7c91f8fd01be" />

# Models.py

    -- Tabla de Propietarios
    CREATE TABLE Propietarios (
        id_propietario INT AUTO_INCREMENT PRIMARY KEY,
        nombre VARCHAR(100),
        apellido VARCHAR(100),
        telefono VARCHAR(20),
        email VARCHAR(100),
        direccion_propietario VARCHAR(255),
        fecha_registro DATE,
        dni VARCHAR(20)
    );
    
    -- Tabla de Propiedades
    CREATE TABLE Propiedades (
        id_propiedad INT AUTO_INCREMENT PRIMARY KEY,
        direccion VARCHAR(255),
        tipo_propiedad VARCHAR(50),
        num_habitaciones INT,
        num_banos INT,
        superficie_m2 DECIMAL(10,2),
        precio_venta DECIMAL(15,2),
        precio_alquiler DECIMAL(15,2),
        estado_propiedad VARCHAR(50),
        fecha_publicacion DATE,
        descripcion TEXT,
        id_propietario INT,
        FOREIGN KEY (id_propietario) REFERENCES Propietarios(id_propietario)
    );
    
    -- Tabla de Clientes Inmobiliarios
    CREATE TABLE Clientes_Inmobiliaria (
        id_cliente INT AUTO_INCREMENT PRIMARY KEY,
        nombre VARCHAR(100),
        apellido VARCHAR(100),
        telefono VARCHAR(20),
        email VARCHAR(100),
        preferencias_propiedad TEXT,
        presupuesto_maximo DECIMAL(15,2),
        fecha_registro DATE,
        dni VARCHAR(20)
    );
    
    -- Tabla de Agentes Inmobiliarios
    CREATE TABLE Agentes_Inmobiliarios (
        id_agente INT AUTO_INCREMENT PRIMARY KEY,
        nombre VARCHAR(100),
        apellido VARCHAR(100),
        telefono VARCHAR(20),
        email VARCHAR(100),
        licencia_agente VARCHAR(50),
        fecha_contratacion DATE,
        salario DECIMAL(10,2),
        comision_porcentaje DECIMAL(5,2)
    );
    
    -- Tabla de Visitas a Propiedades
    CREATE TABLE Visitas_Propiedad (
        id_visita INT AUTO_INCREMENT PRIMARY KEY,
        id_propiedad INT,
        id_cliente INT,
        id_agente INT,
        fecha_visita DATE,
        hora_visita TIME,
        comentarios_cliente TEXT,
        calificacion_propiedad INT,
        FOREIGN KEY (id_propiedad) REFERENCES Propiedades(id_propiedad),
        FOREIGN KEY (id_cliente) REFERENCES Clientes_Inmobiliaria(id_cliente),
        FOREIGN KEY (id_agente) REFERENCES Agentes_Inmobiliarios(id_agente)
    );
    
    -- Tabla de Contratos de Venta
    CREATE TABLE Contratos_Venta (
        id_contrato_venta INT AUTO_INCREMENT PRIMARY KEY,
        id_propiedad INT,
        id_propietario INT,
        id_cliente INT,
        id_agente INT,
        fecha_contrato DATE,
        precio_final DECIMAL(15,2),
        fecha_cierre DATE,
        estado_contrato VARCHAR(50),
        comision_agente DECIMAL(10,2),
        FOREIGN KEY (id_propiedad) REFERENCES Propiedades(id_propiedad),
        FOREIGN KEY (id_propietario) REFERENCES Propietarios(id_propietario),
        FOREIGN KEY (id_cliente) REFERENCES Clientes_Inmobiliaria(id_cliente),
        FOREIGN KEY (id_agente) REFERENCES Agentes_Inmobiliarios(id_agente)
    );
    
    -- Tabla de Contratos de Alquiler
    CREATE TABLE Contratos_Alquiler (
        id_contrato_alquiler INT AUTO_INCREMENT PRIMARY KEY,
        id_propiedad INT,
        id_propietario INT,
        id_cliente INT,
        id_agente INT,
        fecha_inicio DATE,
        fecha_fin DATE,
        monto_alquiler_mensual DECIMAL(10,2),
        estado_contrato VARCHAR(50),
        deposito_garantia DECIMAL(10,2),
        FOREIGN KEY (id_propiedad) REFERENCES Propiedades(id_propiedad),
        FOREIGN KEY (id_propietario) REFERENCES Propietarios(id_propietario),
        FOREIGN KEY (id_cliente) REFERENCES Clientes_Inmobiliaria(id_cliente),
        FOREIGN KEY (id_agente) REFERENCES Agentes_Inmobiliarios(id_agente)
    );
