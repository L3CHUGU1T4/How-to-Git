 ---

# **📌 MySQL Cheat Sheet 🐬**  

# **🔹 1️⃣ Conexión a MySQL**
```sh
mysql -u root -p
```
📌 Iniciar sesión como usuario `root`.

```sh
mysql -u usuario -p -h host
```
📌 Conectar a un servidor remoto.

---

# **🔹 2️⃣ Bases de Datos**
```sql
SHOW DATABASES;
```
📌 Listar todas las bases de datos.  

```sql
CREATE DATABASE mi_base;
```
📌 Crear una base de datos.  

```sql
USE mi_base;
```
📌 Usar una base de datos específica.  

```sql
DROP DATABASE mi_base;
```
📌 Eliminar una base de datos.

---

# **🔹 3️⃣ Tablas**
```sql
SHOW TABLES;
```
📌 Listar todas las tablas en la base de datos actual.  

```sql
CREATE TABLE usuarios (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(50) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    edad INT DEFAULT 18,
    creado_en TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```
📌 Crear una tabla `usuarios`.  

```sql
DESCRIBE usuarios;
```
📌 Ver la estructura de la tabla.  

```sql
DROP TABLE usuarios;
```
📌 Eliminar una tabla.  

---

# **🔹 4️⃣ Insertar Datos**
```sql
INSERT INTO usuarios (nombre, email, edad) 
VALUES ('Juan Pérez', 'juan@email.com', 25);
```
📌 Insertar un nuevo usuario.  

```sql
INSERT INTO usuarios (nombre, email) 
VALUES ('María García', 'maria@email.com');
```
📌 Insertar sin especificar `edad` (se usa el valor por defecto `18`).  

```sql
INSERT INTO usuarios (nombre, email, edad) 
VALUES 
('Carlos López', 'carlos@email.com', 30),
('Ana Torres', 'ana@email.com', 22);
```
📌 Insertar múltiples filas.

---

# **🔹 5️⃣ Consultar Datos**
```sql
SELECT * FROM usuarios;
```
📌 Seleccionar todos los registros.  

```sql
SELECT nombre, email FROM usuarios;
```
📌 Seleccionar columnas específicas.  

```sql
SELECT * FROM usuarios WHERE edad >= 25;
```
📌 Filtrar registros con `WHERE`.  

```sql
SELECT * FROM usuarios WHERE nombre LIKE 'J%';
```
📌 Filtrar por nombres que comiencen con "J".  

```sql
SELECT * FROM usuarios ORDER BY edad DESC;
```
📌 Ordenar los resultados por edad (descendente).  

```sql
SELECT * FROM usuarios LIMIT 5;
```
📌 Mostrar solo los primeros 5 registros.  

---

# **🔹 6️⃣ Actualizar Datos**
```sql
UPDATE usuarios SET edad = 28 WHERE nombre = 'Juan Pérez';
```
📌 Cambiar la edad de Juan Pérez a 28.  

```sql
UPDATE usuarios SET email = 'nuevo@email.com' WHERE id = 1;
```
📌 Cambiar el email del usuario con `id = 1`.  

---

# **🔹 7️⃣ Eliminar Datos**
```sql
DELETE FROM usuarios WHERE id = 2;
```
📌 Eliminar el usuario con `id = 2`.  

```sql
DELETE FROM usuarios WHERE edad < 18;
```
📌 Eliminar usuarios menores de edad.  

```sql
TRUNCATE TABLE usuarios;
```
📌 **Eliminar todos los datos** de la tabla sin borrar su estructura.  

---

# **🔹 8️⃣ Claves Primarias y Foráneas**
```sql
CREATE TABLE pedidos (
    id INT AUTO_INCREMENT PRIMARY KEY,
    usuario_id INT,
    total DECIMAL(10,2) NOT NULL,
    FOREIGN KEY (usuario_id) REFERENCES usuarios(id) ON DELETE CASCADE
);
```
📌 **Clave foránea**: Si un usuario es eliminado, sus pedidos también se eliminan (`ON DELETE CASCADE`).  

---

# **🔹 9️⃣ Joins (Uniones de Tablas)**
```sql
SELECT usuarios.nombre, pedidos.total 
FROM usuarios 
JOIN pedidos ON usuarios.id = pedidos.usuario_id;
```
📌 **INNER JOIN**: Muestra usuarios con pedidos.  

```sql
SELECT usuarios.nombre, pedidos.total 
FROM usuarios 
LEFT JOIN pedidos ON usuarios.id = pedidos.usuario_id;
```
📌 **LEFT JOIN**: Muestra **todos** los usuarios, aunque no tengan pedidos.  

---

# **🔹 🔟 Funciones Agregadas**
```sql
SELECT COUNT(*) FROM usuarios;
```
📌 Contar cuántos usuarios hay.  

```sql
SELECT AVG(edad) FROM usuarios;
```
📌 Obtener la edad promedio.  

```sql
SELECT MAX(edad) FROM usuarios;
```
📌 Encontrar la edad más alta.  

```sql
SELECT MIN(edad) FROM usuarios;
```
📌 Encontrar la edad más baja.  

```sql
SELECT SUM(total) FROM pedidos;
```
📌 Sumar el total de todos los pedidos.  

---

# **📌 1️⃣1️⃣ Subconsultas**
```sql
SELECT * FROM usuarios 
WHERE edad = (SELECT MAX(edad) FROM usuarios);
```
📌 Seleccionar el usuario más viejo.  

---

# **📌 1️⃣2️⃣ Creación de Vistas**
```sql
CREATE VIEW vista_usuarios_mayores AS 
SELECT * FROM usuarios WHERE edad >= 18;
```
📌 Crear una vista para usuarios mayores de edad.  

```sql
SELECT * FROM vista_usuarios_mayores;
```
📌 Consultar la vista como si fuera una tabla normal.  

---

# **📌 1️⃣3️⃣ Índices para Optimizar Consultas**
```sql
CREATE INDEX idx_email ON usuarios(email);
```
📌 Acelera las búsquedas en la columna `email`.  

---

# **📌 1️⃣4️⃣ Usuarios y Permisos**
```sql
CREATE USER 'usuario'@'localhost' IDENTIFIED BY 'clave';
GRANT ALL PRIVILEGES ON mi_base.* TO 'usuario'@'localhost';
FLUSH PRIVILEGES;
```
📌 Crear un usuario y darle permisos en la base `mi_base`.  

---

# **📌 🚀 Bonus: Modelo Relacional**
Si quieres que tu equipo **visualice la estructura de la base de datos**, usa **dbdiagram.io** para crear diagramas ER con código.  
Ejemplo:  

```dbml
Table usuarios {
  id int [primary key, auto_increment]
  nombre varchar(50)
  email varchar(100) [unique]
  edad int
}

Table pedidos {
  id int [primary key, auto_increment]
  usuario_id int [ref: > usuarios.id]
  total decimal(10,2)
}
```

📌 **Esto generará un diagrama ER visual de las relaciones.**  

---
