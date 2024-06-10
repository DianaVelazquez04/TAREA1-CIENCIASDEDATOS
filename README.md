# TAREA1-CIENCIASDEDATOS
Documentación y Publicación en GitHub
1. Crear un repositorio en GitHub
Accede a GitHub y crea un nuevo repositorio llamado consultorio_medico.
Clona el repositorio en tu máquina local:
sh
Copiar código
git clone https://github.com/tu-usuario/consultorio_medico.git
cd consultorio_medico
2. Estructura del Proyecto
Dentro del directorio del proyecto, crea la siguiente estructura de carpetas y archivos:

Copiar código
consultorio_medico/
├── database/
│   ├── create_tables.sql
│   └── populate_tables.sql
├── notebooks/
│   └── consultorio_medico.ipynb
├── scripts/
│   └── connect_db.py
├── README.md
└── requirements.txt
3. Esquema de la Base de Datos
En el archivo database/create_tables.sql, define el esquema de la base de datos:

sql
Copiar código
CREATE DATABASE consultorio_medico;

USE consultorio_medico;

CREATE TABLE pacientes (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(100),
    apellido VARCHAR(100),
    fecha_nacimiento DATE,
    direccion VARCHAR(255)
);

CREATE TABLE citas (
    id INT AUTO_INCREMENT PRIMARY KEY,
    paciente_id INT,
    fecha DATE,
    hora TIME,
    motivo VARCHAR(255),
    FOREIGN KEY (paciente_id) REFERENCES pacientes(id)
);
4. Población de la Base de Datos
En el archivo database/populate_tables.sql, añade datos de ejemplo:

sql
Copiar código
USE consultorio_medico;

INSERT INTO pacientes (nombre, apellido, fecha_nacimiento, direccion)
VALUES 
('Juan', 'Perez', '1980-01-01', 'Calle Falsa 123'),
('Maria', 'Gomez', '1990-02-02', 'Avenida Siempre Viva 456');

INSERT INTO citas (paciente_id, fecha, hora, motivo)
VALUES 
(1, '2023-06-15', '10:00:00', 'Chequeo general'),
(2, '2023-06-16', '11:00:00', 'Dolor de cabeza');
5. Conexión a la Base de Datos desde Python
En el archivo scripts/connect_db.py, utiliza mysql-connector-python para conectarte a la base de datos:

python
Copiar código
import mysql.connector

def connect_to_db():
    connection = mysql.connector.connect(
        host="localhost",
        user="tu_usuario",
        password="tu_contraseña",
        database="consultorio_medico"
    )
    return connection

def get_pacientes():
    connection = connect_to_db()
    cursor = connection.cursor()
    cursor.execute("SELECT * FROM pacientes")
    result = cursor.fetchall()
    for row in result:
        print(row)
    cursor.close()
    connection.close()

if __name__ == "__main__":
    get_pacientes()
6. Desarrollo de la Interfaz en Jupyter Notebook
En el archivo notebooks/consultorio_medico.ipynb, implementa la lógica de tu proyecto y el análisis de datos.

7. Archivo README
En el archivo README.md, proporciona las instrucciones detalladas:

markdown
Copiar código
# Consultorio Médico

## Descripción
Este proyecto implementa una base de datos para gestionar un consultorio médico y permite la interacción con dicha base de datos utilizando Python.

## Requisitos
- MySQL
- Python 3.x
- Jupyter Notebook
- Paquetes de Python: `mysql-connector-python`, `pandas`, `jupyter`

## Configuración de la Base de Datos

1. Crear la base de datos y las tablas:
    ```sh
    mysql -u tu_usuario -p < database/create_tables.sql
    ```

2. Poblar la base de datos con datos de ejemplo:
    ```sh
    mysql -u tu_usuario -p < database/populate_tables.sql
    ```

## Instalación de Dependencias

1. Crear un entorno virtual:
    ```sh
    python -m venv env
    source env/bin/activate  # En Windows usa `env\Scripts\activate`
    ```

2. Instalar los paquetes necesarios:
    ```sh
    pip install -r requirements.txt
    ```

## Ejecución del Programa

1. Ejecutar el script de conexión a la base de datos:
    ```sh
    python scripts/connect_db.py
    ```

2. Abrir el Jupyter Notebook:
    ```sh
    jupyter notebook notebooks/consultorio_medico.ipynb
    ```

## Ejemplo de Uso
Dentro del notebook, puedes ejecutar las celdas para interactuar con la base de datos y realizar análisis sobre los datos de pacientes y citas.

## Contribuciones
Las contribuciones son bienvenidas. Por favor, crea un fork del repositorio y abre un pull request con tus cambios.

## Licencia
Este proyecto está licenciado bajo la Licencia MIT.
8. Requisitos del Proyecto (requirements.txt)
En el archivo requirements.txt, lista las dependencias del proyecto:

Copiar código
mysql-connector-python
pandas
jupyter
9. Documentación y Publicación en GitHub
Sube tu código a GitHub:

sh
Copiar código
git add .
git commit -m "Inicializar el proyecto consultorio_medico"
git push origin main
Has documentado y publicado tu proyecto en GitHub.
