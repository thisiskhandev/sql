# SQL (Structured Query Language)
**_• Creating Database_**
CREATE DATABASE db_students;

**_• Creating Table_**
CREATE TABLE db_students.personal (
id INT NOT NULL UNIQUE AUTO_INCREMENT,
name VARCHAR(50) NOT NULL,
phone VARCHAR(10) NOT NULL UNIQUE,
age INT NOT NULL CHECK (age >= 18),
gender VARCHAR(1) NOT NULL,
city INT NOT NULL,
country VARCHAR(90) DEFAULT 'Pakistan',
PRIMARY KEY (id),
FOREIGN KEY (city) REFERENCES cities (cid)
);

**_• Inserting Values into columns_**
INSERT INTO db_students.personal1 (name, age, gender, phone, city, country) VALUES 
("Hassan" , 25, "M", 1234567891, 1, "Pakistan"),
("Khan" , 20, "M", 1254567892, 2, "India"),
("Elile" , 22, "F", 1244567899, 3, "USA"),
("Ali" , 30, "M", 1234267899, 4, "UAE"),
("Jabbar" , 20, "M", 1134567869, 4, "Pakistan"),
("Yumna" , 18, "F", 1234567879, 1, "Pakistan");

**_• Update the specific column data_**
UPDATE db_students.personal SET email = "info@mail.com" WHERE id = 1;

**_• Update column data from column 1 to column 10_**
UPDATE db_students.personal SET email = "info@justmail.com" WHERE id BETWEEN 1 AND 10;

**_• Delete row_**
DELETE FROM db_students.personal WHERE id = 4;

**_• Delete column_**
ALTER TABLE db_students.personal DROP COLUMN city;

**_• Add column_**
ALTER TABLE db_students.personal ADD email VARCHAR(80) NOT NULL UNIQUE;

**_• To add a foreign key to an existing table in SQL_**
ALTER TABLE db_students.personal ADD FOREIGN KEY (city) REFERENCES db_students.cities (cid);

**_• Checking foreign keys and refrences column names_**
SELECT * 
FROM information_schema.REFERENTIAL_CONSTRAINTS 
WHERE constraint_schema = 'db_students' 
AND table_name = 'personal1';
