# The-warehouse

## *Relational Schema*
![img](https://upload.wikimedia.org/wikipedia/commons/4/47/Sql_warehouse.png)

## *Table creation code*
```SQL 
   CREATE TABLE Warehouses (
   Code INTEGER PRIMARY KEY NOT NULL,
   Location TEXT NOT NULL ,
   Capacity INTEGER NOT NULL 
 );
 
 CREATE TABLE Boxes (
   Code TEXT PRIMARY KEY NOT NULL,
   Contents TEXT NOT NULL ,
   Value REAL NOT NULL ,
   Warehouse INTEGER NOT NULL, 
   CONSTRAINT fk_Warehouses_Code FOREIGN KEY (Warehouse) REFERENCES Warehouses(Code)
 );
 ```
## *Sample dataset*
```SQL INSERT INTO Warehouses(Code,Location,Capacity) VALUES (1,'Chicago',3);
 INSERT INTO Warehouses(Code,Location,Capacity) VALUES (2,'Chicago',4);
 INSERT INTO Warehouses(Code,Location,Capacity) VALUES (3,'New York',7);
 INSERT INTO Warehouses(Code,Location,Capacity) VALUES (4,'Los Angeles',2);
 INSERT INTO Warehouses(Code,Location,Capacity) VALUES (5,'San Francisco',8);

 INSERT INTO Boxes(Code,Contents,Value,Warehouse) VALUES ('0MN7','Rocks',180,3);
 INSERT INTO Boxes(Code,Contents,Value,Warehouse) VALUES ('4H8P','Rocks',250,1);
 INSERT INTO Boxes(Code,Contents,Value,Warehouse) VALUES ('4RT3','Scissors',190,4);
 INSERT INTO Boxes(Code,Contents,Value,Warehouse) VALUES ('7G3H','Rocks',200,1);
 INSERT INTO Boxes(Code,Contents,Value,Warehouse) VALUES ('8JN6','Papers',75,1);
 INSERT INTO Boxes(Code,Contents,Value,Warehouse) VALUES ('8Y6U','Papers',50,3);
 INSERT INTO Boxes(Code,Contents,Value,Warehouse) VALUES ('9J6F','Papers',175,2);
 INSERT INTO Boxes(Code,Contents,Value,Warehouse) VALUES ('LL08','Rocks',140,4);
 INSERT INTO Boxes(Code,Contents,Value,Warehouse) VALUES ('P0H6','Scissors',125,1);
 INSERT INTO Boxes(Code,Contents,Value,Warehouse) VALUES ('P2T6','Scissors',150,2);
 INSERT INTO Boxes(Code,Contents,Value,Warehouse) VALUES ('TU55','Papers',90,5);
```

## *Exercises*
1. Select all warehouses.

2. Select all boxes with a value larger than $150.

3. Select all distinct contents in all the boxes.

4. Select the average value of all the boxes

5. Select the warehouse code and the average value of the boxes in each warehouse.

6. Same as previous exercise, but select only those warehouses where the average value of the boxes is greater than 150.

7. Select the code of each box, along with the name of the city the box is located in.

8. Select the warehouse codes, along with the number of boxes in each warehouse. Optionally, take into account that some warehouses are empty (i.e., the box count should show up as zero, instead of omitting the warehouse from the result).

9. Select the codes of all warehouses that are saturated (a warehouse is saturated if the number of boxes in it is larger than the warehouse's capacity).

10. Select the codes of all the boxes located in Chicago.

11. Create a new warehouse in New York with a capacity for 3 boxes.

12. Create a new box, with code "H5RT", containing "Papers" with a value of $200, and located in warehouse 2.

13. Reduce the value of all boxes by 15%.

14. Apply a 20% value reduction to boxes with a value larger than the average value of all the boxes.

15. Remove all boxes with a value lower than $100.

16. Remove all boxes from saturated warehouses.

## Answers
```SQL
1.SELECT * FROM Warehouses;

2.SQL SELECT * FROM Boxes WHERE Value > 150;```

3.SQL SELECT DISTINCT * FROM Boxes;```

4.SQL SELECT AVG(Value) FROM Boxes;```

5.SQL SELECT Warehouse, AVG(Value) FROM Boxes GROUP BY Warehouse;```

6.SQL SELECT Warehouse, AVG(Value) FROM Boxes GROUP BY Warehouse HAVING AVG(Value) > 150;```

7.SQL SELECT Boxes.Code, Location FROM Warehouses INNER JOIN Boxes  ON Warehouses.Code = Boxes.Warehouse;```

8.SQL SELECT Warehouses.Code, COUNT(Boxes.Code) FROM Warehouses LEFT JOIN Boxes ON Warehouses.Code = Boxes.Warehouse GROUP BY Warehouses.Code;```

9.SQL SELECT Code FROM Warehouses  WHERE Capacity < ( SELECT COUNT(*)  FROM Boxes  WHERE Warehouse = Warehouses.Code);```

10.SQL SELECT B.Code FROM Warehouses RIGHT OUTER JOIN Boxes B on Warehouses.Code = B.Warehouse WHERE Location = 'Chicago;```

11.SQL INSERT INTO Warehouses (Code, Location, Capacity) VALUES (6, 'New York',3);```

12.SQL INSERT INTO Boxes(Code, Contents, Value, Warehouse) VALUES ('H5RT', 'Papers', 200, 2);```

13.SQL UPDATE Boxes SET Value = Value * 0.85 WHERE Code = '0MN7';```

14.SQL UPDATE Boxes SET Value = Value * 0.80 WHERE Value > (SELECT AVG(Value) FROM (SELECT * FROM Boxes);```

15.SQL DELETE FROM Boxes WHERE Value < 100;```

16.SQL DELETE FROM Warehouses;``` 
