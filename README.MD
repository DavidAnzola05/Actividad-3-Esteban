Parte 1 – Análisis conceptual (Devart)
1. ¿Qué problema principal busca resolver la normalización en una base de datos y por qué es crítica en sistemas empresariales?

La normalización busca eliminar la redundancia y evitar inconsistencias en los datos.
Es crítica en sistemas empresariales porque permite que la información sea más confiable, evita duplicados, reduce errores en los registros y facilita el mantenimiento de la base de datos a largo plazo.

2. Diferencias entre 1NF, 2NF y 3NF según los ejemplos del artículo

1NF (Primera Forma Normal):
Los datos deben ser atómicos. No puede haber campos con listas, valores múltiples o repetidos. Cada celda debe contener un solo dato.

2NF (Segunda Forma Normal):
Debe cumplir 1NF. Además, todos los atributos deben depender por completo de la clave primaria.
Elimina dependencias parciales cuando hay claves compuestas.

3NF (Tercera Forma Normal):
Debe cumplir 2NF.
Elimina las dependencias transitivas, es decir, datos que dependen de otro atributo que no es clave.
Cada dato debe depender únicamente de la clave primaria.

3. Situación donde la normalización mejora la integridad pero aumenta la complejidad en consultas SQL

Cuando se separa la información en múltiples tablas para reducir la redundancia —por ejemplo, separar Clientes, Órdenes, Productos y Detalles de Orden— la integridad mejora, pero la consulta se vuelve más compleja porque exige usar JOINs entre varias tablas para obtener un solo reporte.

4. Cómo la normalización previene anomalías de actualización, inserción y eliminación

Actualización:
Evita que el mismo dato esté repetido en varias filas, lo que previene que algunos registros queden desactualizados.

Inserción:
Permite registrar información sin depender de otros datos que no existen aún (evita no poder insertar entradas incompletas).

Eliminación:
Impide que al borrar un registro se pierdan datos importantes asociados, separando correctamente las entidades en tablas distintas.

5. Dos beneficios y dos desventajas de una normalización estricta

 Beneficios:

Mayor integridad y coherencia de los datos.

Facilita el mantenimiento y reduce errores en actualizaciones.

Desventajas:

Las consultas se vuelven más complejas por la cantidad de tablas involucradas.

Puede disminuir el rendimiento en consultas pesadas debido a múltiples JOINs.

Parte 2 – Implementación práctica (Fred’s Furniture con Docker)

En esta fase se implementó la base de datos normalizada de Fred’s Furniture dentro de un contenedor Docker utilizando MySQL Server.
El objetivo fue demostrar cómo los contenedores permiten desarrollar y desplegar sistemas empresariales en entornos controlados, portátiles y reproducibles.

1. Creación del entorno Docker

Se ejecutó el siguiente comando para crear el contenedor de base de datos:

docker run -d --name freds-mysql -e MYSQL_ROOT_PASSWORD=1234 -e MYSQL_DATABASE=freds_furniture_normalized -p 3307:3306 mysql:latest


Esto generó un contenedor activo con MySQL escuchando en el puerto 3307.

2. Conexión al contenedor

Se accedió al cliente MySQL dentro del contenedor con:

docker exec -it freds-mysql mysql -u root -p

3. Creación de las tablas

Dentro de la base freds_furniture_normalized se ejecutaron las sentencias SQL para crear las tablas:

Customers

Products

Orders

OrderDetails

Estas tablas mantienen las relaciones mediante claves foráneas para asegurar la integridad referencial.

4. Verificación

Al ejecutar SHOW TABLES; se confirmó la correcta creación de todas las tablas.

5. Resultados

La base quedó estructurada bajo el modelo normalizado (3NF).

El entorno es totalmente replicable en cualquier equipo con Docker.

Se reduce el riesgo de errores de configuración y se facilita el despliegue.

Conclusión:
La implementación en Docker demuestra cómo esta tecnología mejora la portabilidad y consistencia de los entornos de desarrollo, alineándose con prácticas modernas de DevOps e infraestructura ágil.