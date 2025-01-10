# WORK
MODULO 1
1. Selecciona el nombre y apellido de los usuarios que tienen menos de 30 años y se registraron después del 1 de enero de 2020.
Ordena los resultados por fecha de registro en orden descendente.
```SQL
USE tienda;
SELECT *
FROM Usuarios
ORDER BY fecha_registro DESC;

SELECT 
	nombre, 
	apellido,
          fecha_registro
FROM Usuarios
WHERE edad < 30 AND fecha_registro > '2020-01-01'
ORDER BY fecha_registro DESC;
```

2.Obtén el nombre y precio de los productos que tienen un stock disponible mayor o igual a 10 y cuyo precio sea menor o igual a $50.
Ordena los resultados por precio en orden ascendente.
```SQL
USE tienda;

SELECT 
      nombre_producto,
      precio,
      stock_disponible
FROM Productos
WHERE stock_disponible >= 10 AND precio <= 50
ORDER BY precio ASC;
```

3. Recupera el identificador del pedido, fecha del pedido y total del pedido para aquellos pedidos realizados antes del 1 de enero de 2024 y cuyo total del pedido sea mayor a $100.
Ordena los resultados por fecha del pedido en orden descendente.
```SQL
USE tienda;
SELECT *
FROM Pedidos;

SELECT 
      pedido_id,
      fecha_pedido,
      total_pedido
FROM Pedidos
WHERE fecha_pedido < '2024-01-01' AND total_pedido > 100
ORDER BY fecha_pedido ASC;
```

4. Muestra la descripción del producto y el stock disponible de aquellos productos que tengan menos de 10 piezas disponibles en stock.
Ordena alfabéticamente los resultados.
```SQL
USE tienda;
SELECT *
FROM Productos;

SELECT 
      descripcion,
      stock_disponible
FROM Productos
WHERE stock_disponible < 10
ORDER BY nombre_producto;
```

5.Obtén los correos electrónicos de los usuarios que son parte de la Tercera Edad y se hayan registrado en el último mes de información.
Ordena alfabéticamente los resultados por dirección de correo electrónico.
```SQL
USE tienda;
SELECT *
FROM Usuarios;

SELECT 
     correo_electronico,
     edad, 
     fecha_registro
FROM Usuarios
WHERE edad >= 65 
ORDER BY fecha_registro = MONTH(12) AND correo_electronico ASC;
```

MODULO 2
Dentro de SQL, escribe diversas consultas para resolver las siguientes situaciones, 
utilizando solamente las cláusulas SELECT, FROM, WHERE, ORDER BY, así como operadores relacionales y lógicos, 
funciones de agregación, GROUP BY y HAVING.

1. Encuentra el número total de usuarios registrados cuya edad sea mayor o igual a 30 años.

```SQL
USE tienda;
SELECT 
      nombre,
      edad
FROM Usuarios
WHERE edad >= 30;
```
2. Lista los productos que tienen un precio mayor a $50 ordenados por nombre de producto de forma ascendente.
```SQL
SELECT 
      nombre_producto,
      precio
FROM Productos
ORDER BY nombre_producto ASC;
```

3. Calcula la edad promedio de usuarios por fecha de registro.
```SQL
SELECT 
      AVG(edad)
FROM Usuarios;
```

4. Encuentra el identificador del producto y la cantidad vendida en cada pedido, donde la cantidad vendida sea mayor a 10 unidades, 
ordenado por el identificador del producto de forma descendente.
```SQL
SELECT *
FROM Productos;
SELECT *
FROM Pedidos;

SELECT 
	pr.producto_id,
          pd.total_pedidos
FROM Productos as pr
INNER JOIN 
Pedidos AS pd
ORDER BY producto_id ASC;
```
5. Muestra los usuarios que se registraron en el último mes, ordenados por fecha de registro de forma ascendente.

```SQL
SELECT *
FROM Usuarios
ORDER BY fecha_registro = MONTH(12);
```

MODULO 3

1. Consulta 1: Escribe una consulta para seleccionar el nombre y apellido de los usuarios que tienen más de 18 años.

2. Consulta 2: Escribe una consulta para seleccionar el ID y la fecha de los pedidos que contienen productos actualmente agotados en el inventario.

3. Consulta 3: Escribe una consulta para mostrar el nombre del usuario y la cantidad total de pedidos realizados por cada usuario.

4. Consulta 4: Productos con Precio Superior al PromedioEscribe una consulta para seleccionar el nombre del producto y su precio para todos los productos cuyo precio sea superior al precio promedio de todos los productos.

5. Consulta 5: Añade a la consulta anterior el precio promedio como columna para poder comparar los resultados.
```SQL
USE tienda;
SELECT * 
FROM Usuarios
WHERE edad > 18;

SELECT 
	DISTINCT(pr.producto_id),
	pd.fecha_pedido,
          pr.stock_disponible = 0
FROM Productos as pr
JOIN Pedidos AS pd;

SELECT 
	nombre,
          pd.total_pedido
FROM Usuarios
JOIN Pedidos as pd;

SELECT 
	nombre_producto,
          precio,
          avg(precio) 
FROM Productos
WHERE precio > (SELECT AVG(precio) FROM Productos);
```
MODULO 4
1. Utiliza INNER JOIN para combinar la tabla de Pedidos con la tabla de Usuarios 
y obtén el nombre de usuario y la fecha en que se realizó cada pedido.
```sql
SELECT *
FROM Pedidos;
SELECT * 
FROM Usuarios;

SELECT 
 us.user_id,
 us.nombre,
 pd.fecha_pedido
FROM Usuarios as us
INNER JOIN 
 Pedidos as pd
ON us.user_id = pd.pedido_id;
```

2. Utiliza LEFT JOIN para combinar la tabla de Productos con la tabla de Detalles_Pedido 
y obtén el nombre del producto, la cantidad y el precio unitario para cada detalle de pedido.
 Si un producto no tiene un detalle de pedido, muestra NULL para las columnas correspondientes.

```SQL
SELECT *
FROM Productos;
SELECT *
FROM Detalles_Pedido;

SELECT
 pr.nombre_producto,
       dp.cantidad,
       dp.precio_unitario
FROM Detalles_Pedido AS dp
LEFT JOIN Productos AS pr
 ON pr.producto_id = dp.producto_id;
```

3. Utiliza RIGHT JOIN para combinar la tabla de Pedidos con la tabla de Usuarios 
y obtener el nombre de usuario y la fecha de pedido para cada pedido.

Incluye todos los pedidos, incluso si no hay un usuario asociado al pedido.
```SQL
SELECT * 
FROM Pedidos;
SELECT * 
FROM Usuarios;

SELECT 
 us.nombre,
       pd.fecha_pedido
FROM Pedidos AS pd
RIGHT JOIN Usuarios AS us
       ON pd.user_id = us.user_id;
```

4. Utiliza UNION para combinar los nombres de los productos de la tabla Productos y 
Detalles_Pedido, en un sólo conjunto de resultados.

5. Utiliza CROSS JOIN para generar todas las posibles combinaciones entre los 
nombres de usuario de la tabla Usuarios y los nombres de producto de la tabla Productos.
