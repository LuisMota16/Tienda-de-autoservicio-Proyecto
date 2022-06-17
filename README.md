# Tienda-de-autoservicio-Proyecto
Proyecto de Python
Drop database if exists Oxxo;
Create database Oxxo;
Use Oxxo;
Create table Caja (
    Codigo INT Primary key,
    Mostrador INT
);
INSERT INTO Caja VALUES
('240','1'),
('200','2'),
('1200','3');

Create table Cajero(
    ID Int Primary Key,
    Nombre VARCHAR(255)
);
INSERT INTO Cajero VALUES 
('01', 'BEATRIZ HOLGADO'),
('02', 'VANESA NATALIA'),
('03', 'MARIA VICTORIA'),
('04', 'JOSE CARLOS');

Create table Articulo(
Codigo INT PRIMARY KEY,
Nombre VARCHAR(100),
Precio Float NOT NULL ,
Stock INT NOT NULL,
Categoria VARCHAR(100) NOT NULL
);
INSERT INTO Articulo VALUES
('00525','Cerveza Modelo','32.00','55','Licor'),
('0148','Cerveza Heineken','35.00','30','Licor'),
('12698','Yoghurt Durazno','19.90','40','Lacteo'),
('12697','Yoghut Fresa','18.55','30','Lacteo'),
('00025','Azucar','17.50','30','Basico'),
('06453','Frijoles refritos La sierra','30.90','25','Basico'),
('45698','Atun en aceite Dolores','12.30','39','Basico'),
('98324','Arroz','27.00','30','Basico'),
('78521','Escoba plástico','35.00','5','Hogar'),
('639840','Polvo de sabor Tang','4.00','50','Polvo sabor'),
('963250','Polvo de sabor Zuko','4.50','45','Polvo sabor');


Create table Venta(
    Cajero INT NOT NULL,
    Caja INT NOT NULL,
    Articulo INT NOT NULL,
    Comprobante varchar(20) NOT NULL,
    Nventa INT AUTO_INCREMENT PRIMARY KEY,
    FOREIGN KEY (Cajero) REFERENCES Cajero(ID),
    FOREIGN KEY (Caja) REFERENCES Caja(Codigo),
    FOREIGN KEY (Articulo) REFERENCES Articulo(Codigo)
);

INSERT INTO Venta VALUES
('01', '240', '45698','001','1'),
('02', '200', '00025','002','2'),
('03', '1200', '12697','003','3'),
('04', '1200', '00525','004','4'),
('01', '240', '00025','005','5'),
('02', '200', '12698','006','6'),
('03', '200', '12697','007','7'),
('04', '240', '0148','008','8'),
('01', '200', '00025','009','9'),
('02', '240', '12698','010','10'),
('03', '1200', '45698','011','11'),
('04', '1200', '00525','012','12'),
('01', '240', '0148','013','13'),
('02', '1200', '98324','014','14'),
('03', '240', '78521','015','15'),
('04', '200', '639840','016','16'),
('01', '200', '00525','017','17'),
('02', '240', '963250','018','18'),
('03', '1200', '45698','019','19'),
('04', '1200', '98324','020','20'),
('01', '1200', '00525','021','21');


Select Nombre,Precio FROM Articulo;
Select SUM(Precio),MIN(Precio),MAX(Precio), AVG(Precio) FROM Articulo;
Select Nombre from Articulo order by Categoria;
Select Nombre,Precio from Articulo where Categoria <>'Basico';
Select AVG(Precio), Categoria FROM Articulo GROUP BY Categoria;

Delimiter$$
create trigger actualizarstock
after insert on Articulo FOR EACH ROW
declare
begin
    update Articulos
    set cantidadstock = cantidadstock = new.cantidad
    where codigoarticulo = :new.codigoarticulo;
End$$
Delimiter;

Select codigoarticulo, nombre, cantidadstock from Articulos where codigoarticulo = '00525';

INSERT INTO Articulo VALUES(1,'00525',51,32.00);


Delimiter$$
Create trigger actualizarprecioproducto
Before update on Articulo
For each ROW
Begin   
if NEW.Coste <> OLD.Coste 
then
Set New.precio=NEW.Coste *2;
End if,
End$$
Delimiter;

Update Articulo Set Coste= 5 where codigo=00525;
Select * from Articulo;

