# SQL (Structured Query Language)

**_• Set any DB as default Schema_** <br>
USE database_name;

**_• Creating Database_** <br>
CREATE DATABASE db_students;

**_• Creating Table_** <br>
CREATE TABLE db_students.personal (
id INT NOT NULL AUTO_INCREMENT,
name VARCHAR(50) NOT NULL,
phone VARCHAR(10) NOT NULL UNIQUE,
age INT NOT NULL CHECK (age >= 18),
gender VARCHAR(1) NOT NULL,
city INT NOT NULL,
country VARCHAR(90) DEFAULT 'Pakistan',
PRIMARY KEY (id),
FOREIGN KEY (city) REFERENCES cities (cid)
);

#### -- OR --<br>

CREATE TABLE personal (
id INT NOT NULL AUTO_INCREMENT,
name VARCHAR (50) NOT NULL,
percentage INT NOT NULL,
age INT NOT NULL,
gender VARCHAR(1) NOT NULL,
city INT NOT NULL,
PRIMARY KEY(id),
FOREIGN KEY (city) REFERENCES City (cid)
);

**_• Inserting Values into columns_** <br>
INSERT INTO db_students.personal1 (name, age, gender, phone, city, country) VALUES 
("Hassan" , 25, "M", 1234567891, 1, "Pakistan"),
("Khan" , 20, "M", 1254567892, 2, "India"),
("Elile" , 22, "F", 1244567899, 3, "USA"),
("Ali" , 30, "M", 1234267899, 4, "UAE"),
("Jabbar" , 20, "M", 1134567869, 4, "Pakistan"),
("Yumna" , 18, "F", 1234567879, 1, "Pakistan");

**_• Update the specific column data_** <br>
UPDATE db_students.personal SET email = "info@mail.com" WHERE id = 1;

**_• Update column data from column 1 to column 10_** <br>
UPDATE db_students.personal SET email = "info@justmail.com" WHERE id BETWEEN 1 AND 10;

**_• Delete row_** <br>
DELETE FROM db_students.personal WHERE id = 4;

**_• Delete column_** <br>
ALTER TABLE db_students.personal DROP COLUMN city;

**_• Add column_** <br>
ALTER TABLE db_students.personal ADD email VARCHAR(80) NOT NULL UNIQUE;

**_• Add a foreign key to an existing table in SQL_**
ALTER TABLE db_students.personal ADD FOREIGN KEY (city) REFERENCES db_students.cities (cid);

**_• Checking foreign keys and refrences column names_** <br>
SELECT * 
FROM information_schema.REFERENTIAL_CONSTRAINTS 
WHERE constraint_schema = 'db_students' 
AND table_name = 'personal1';

**_• Watch data accosiated with FK and PK_** <br>
SELECT * FROM personal INNER JOIN city ON personal.city = city.cid;

**_• Watch with only allias names_** <br>
SELECT * FROM personal p INNER JOIN city c ON p.city = c.cid;

**_• Watch only you want to display specific columns data_** <br>
SELECT p.id, p.name, p.percentage, p.gender, c.cityname
FROM personal p JOIN city c
ON p.city = c.cid
WHERE c.cityname = "Quetta"
ORDER BY p.id;

**_• Watch dual table relation data_** <br>
SELECT std.s_id AS ID, std.name AS "Student Name", std.age AS Age, c.city_name AS City , cr.course_name AS Courses FROM students std
INNER JOIN city c ON std.city = c.c_id
INNER JOIN courses cr ON std.course = cr.cr_id;

**_• Watch total data from specific table for e.g: Total students from each city_** <br>
SELECT city_name AS "City Name", COUNT(std.city) as Total
FROM students std INNER JOIN city c ON std.city = c.c_id
GROUP BY city
ORDER BY COUNT(std.city) DESC;

**_• Search course id by course name_** <br>
SELECT cr_id FROM courses WHERE course_name = "MBBS";

**_• Search Query_** <br>
SELECT name FROM students
WHERE course = (SELECT cr_id FROM courses WHERE course_name = "MBA");

**_• Multi search Query_** <br>
SELECT name FROM students
WHERE course IN (SELECT cr_id FROM courses WHERE course_name IN ("MBA", "MBBS"));

**_• Show all names if course exist_** <br>
SELECT name FROM students
WHERE EXISTS (SELECT cr_id FROM courses WHERE course_name IN ("MBA"));

**_• Show 0 names if course exist_** <br>
SELECT name FROM students
WHERE NOT EXISTS (SELECT cr_id FROM courses WHERE course_name IN ("MBA"));

**_• Show conditional based data_** <br>
WHERE age >= 10;

**_• Show equal based data_** <br>
WHERE age = 18 OR age = 21;

-- OR -- <br>

WHERE age IN (18, 21);

**_• Create an INDEX on column_** <br>
CREATE INDEX salID ON employees (salary);

**_• Show all indexes in current table_** <br>
SHOW INDEX FROM db_office.employees;

**_• Delete a specific INDEX on column_** <br>
DROP INDEX salID ON employees
