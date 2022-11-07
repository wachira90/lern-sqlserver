# alter field calculate

## create table 

```
CREATE DATABASE sales_database;
USE sales_database;

CREATE TABLE sales(
    id INT IDENTITY(1,1) NOT NULL PRIMARY KEY,
    product_name VARCHAR(50),
    price money,
    quantity INT
);

```    

## insert data

```    
INSERT INTO sales(product_name, price, quantity)
VALUES ('iPhone Charger', $9.99, 10),
       ('Google Chromecast', $59.25, 5),
       ('Playstation DualSense Wireless Controller', $69.00, 100),
       ('Xbox Series S', $322.00, 3),
       ('Oculus QUest 2', $299.50, 7),
       ('Netgear Nighthawk', $236.30, 40),
       ('Redragon S101', $35.98, 100),
       ('Star Wars Action Figure', $17.50, 10),
       ('Mario Kart 8 Deluxe', $57.00, 5);
```       

## alter field calculate

```
ALTER TABLE sales ADD total_price AS price * quantity;
```
