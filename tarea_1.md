# Subconsultas 
# Desarrollar los siguientes ejercicios usando subconsultas:

## DB INVOICE
1.- Número total de facturas realizadas por cada cliente:

 nombre_cliente | direccion | nro_facturas

```
SELECT 
    c.full_name, 
    c.address,
    (SELECT COUNT(*) FROM invoice i WHERE i.client_id = c.id) AS total_facturas
FROM 
    clients c;
```
Captura:
![Captura de pantalla 2024-07-01 230256](https://github.com/CarlosQ18a/tarea_1/assets/146890782/165b0221-daba-41db-90e1-fcd3d45053ac)


2.- Listar nombre y correo de los clientes junto a su compra mas cara realizada:

nombres |  correo   | total_mas_alto
```
SELECT 
    c.full_name, 
    c.email, 
    (SELECT MAX(i.total) FROM invoice i WHERE i.client_id = c.id) AS compra_cara
FROM 
    clients c;

```
Captura:
![Captura de pantalla 2024-07-01 230512](https://github.com/CarlosQ18a/tarea_1/assets/146890782/242dc7a3-5247-4cd5-b6f6-3926539eb3bf)


3.- Listar las facturas donde sus totales sean mayores al promedio de las facturas:

fecha_factura | total 
```
SELECT i.created_at, i.total
FROM invoice i
WHERE (SELECT AVG(i.total)
FROM invoice i ) < i.total;
```
Captura:

![Captura de pantalla 2024-07-01 230715](https://github.com/CarlosQ18a/tarea_1/assets/146890782/812451f7-a6a6-48b3-9630-df6cb44ad6be)

 
 ---
 
### DB EVENT
### Crear dos ejemplo con la base de datos event. Uno con subconsulta en SELECT y otro con subconsulta  en WHERE

1.- Listar una lista de conferencias, incluyendo el número total de asistentes registrados en cada conferencia:

id | nombre_conferencia | nombre_expositor | hora_inicio | fecha | numero_asistentes

```
SELECT 
    conf.id, 
    conf.title AS nombre_conferencia, 
    conf.speaker AS nombre_expositor, 
    conf.hour AS hora_inicio, 
    conf.day AS fecha, 
    conf.total_attendees AS numero_asistentes,
    (SELECT COUNT(*) FROM conference otra_conf WHERE otra_conf.id = conf.id) AS subconsulta
FROM 
    conference conf;
```
Captura:

![Captura de pantalla 2024-07-01 234209](https://github.com/CarlosQ18a/tarea_1/assets/146890782/fccc908d-8f69-4546-be3c-253b0182e125)

2.- Listar una lista de conferencias, incluyendo el número total de asistentes registrados en cada conferencia:

id | titulo_conferencia | expositor_principal | hora_evento | dia_evento | asistentes_totales

```
SELECT 
    c.id, 
    c.title AS titulo_conferencia, 
    c.speaker AS expositor_principal, 
    c.hour AS hora_evento, 
    c.day AS dia_evento, 
    c.total_attendees AS asistentes_totales
FROM 
    conference c
WHERE 
    c.total_attendees > 0; 
```
Captura:
![Captura de pantalla 2024-07-01 233740](https://github.com/CarlosQ18a/tarea_1/assets/146890782/f889fcba-d67c-4880-9df9-05fc7c972668)

