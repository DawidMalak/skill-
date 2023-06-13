# skill-

-- SQLite DBbrowser
-- CREATED BY DAWID MALAK 
-- DBname FirmaTransportowa

/* VALUES USED IN THIS DATABASE DOES NOT CONTAIN ACCURATE REAL LIFE DATA 
   THEY ARE MAINLY MADE UP ONLY FOR DEMONSTRATION PURPOSES.
   I CREATED THIS SMALL DATA BASE WITH CAN BY USED FOR SMALL TRANSPORT COMPANY FOR MONITORING 
   FLEET,EMPLOYEES,ROUTES,TACHOGRAPCH DRIVING TIME,ETC 
   HAVING ACTUALL EXACT DATA DOWNLOADED FROM VEHICLE ONBOARD UNIT IT WOULD BE POSSIBLE TO
   REARRANGE LAST TABLE "drivingtime" MORE EXPANDED ACCURATE AND PROFESSIONAL WAY FOR CALCULATING
   DRIVING TIME ,DAYLI BRAKE,DISTANCE,FUEL USAGE,AS WELL AS "directions" TABLE
   COULD BE ALTERED WITH CLIENT'S ADDRESES,CARGO,COUNTRY OF START AND COUNTRY OF END AS IS REGUIRED 
   BY ONBOARD UNIT AND EU LAWS AS COMPULSORY DAILY INPUT */
   
   
	_ _       _		   _		     _	   _	  _  _	
	_	  _    _ _	   _	       _	   _    _   _
	_   _   _   _		 _    _	   _	   _	  _   _
	_____	 _______	 ___________	   _    _____ 
	_ _ 	_		    _	 __	   	  __     _	  _ _



--CREATING TABLE vehicles  

CREATE TABLE IF NOT EXISTS vehicles ( 


id					      INTEGER NOT NULL,
mark				      TEXT	NOT NULL, 
number_plate		  TEXT	NOT NULL  	CHECK ( length (number_plate) == 7 ),
euro				      INTEGER	NOT NULL  	CHECK (	euro > 0 AND euro <= 6 ),
chassis				    TEXT	NOT NULL,	
volume				    TEXT 	NOT NULL,  
year_of_prod 		  TEXT	NOT NULL	CHECK (length (year_of_prod) == 10 ), 
time_of_insert		TEXT	DEFAULT CURRENT_TIMESTAMP,

PRIMARY KEY (id) 
 
);

INSERT INTO vehicles 
(id,mark,number_plate,euro,chassis,volume,year_of_prod) 

VALUES 
(1,'Scania'		,'CBY443G','4','Tauntliner'		,'88m3','05-10-2010'),
(2,'Man'   		,'CBG849H','5','Flatbed	'  		,'30m3','07-11-2012'),		
(3,'Scania'		,'CYP153G','6','Tauntliner'		,'88m3','06-06-2015'),
(4,'Ford'  		,'CBY227J','6','Tandem    '		,'120m3','02-04-2016'),
(5,'Renault'	,'CHY899S','4','Flatbed	  '		,'30m3','01-10-2009'),
(6,'Man'		  ,'CFF772P','5','Hiab Crane'		,'30m3','02-05-2014'),
(7,'Ford'		  ,'CVN385C','5','Tandem    '		,'120m3','02-06-2013'),
(8,'Volvo'		,'CYB343F','6','Tipper    '		,'80m3','07-07-2018'),
(9,'Daf'		  ,'CDD909G','5','Silo      '		,'80m3','06-09-2017'),
(10,'Renault'	,'CHJ678A','4','Hiab Crane'		,'30m3','03-04-2008'),
(11,'Volvo'		,'CPO221A','5','Box       '		,'90m3','01-01-2014'),
(12,'Daf'		  ,'CTF476T','6','Tanker    '		,'60m3','05-04-2020'),
(13,'Daf'		  ,'CAA190U','5','Silo      '		,'80m3','09-12-2018'),
(14,'Man'		  ,'CBG456W','6','Flatbed   '		,'30m3','10-12-2019'),
(15,'Scania'	,'CSR356R','4','Silo      '		,'80m3','06-11-2011'),
(16,'Ford'		,'COP936R','6','Tandem    '		,'120m3','16-09-2021'),
(17,'Scania'	,'CWR212K','5','Tipper    '		,'80m3','24-11-2015'),
(18,'Ford'		,'CCS669L','4','Walking Floor  ','92m3','15-05-2010'),
(19,'Daf'		  ,'CAL470I','5','Tauntliner'		,'88m3','16-03-2019'),
(20,'Volvo'		,'CNM890E','5','Walking Floor'  ,'92m3','21-02-2021');


-- DML shortcuts

DROP TABLE vehicles; 
SELECT * FROM vehicles;
DELETE FROM vehicles WHERE; 
UPDATE vehicles SET WHERE; 
ALTER TABLE vehicles ADD COLUMN; 

-- CREATING TABLE drivers

CREATE TABLE IF NOT EXISTS drivers (

id				    INTEGER 	NOT NULL, 
worker_id	  	INTEGER 	NOT NULL UNIQUE,
first_name		TEXT 		NOT NULL,
last_name	  	TEXT		NOT NULL, 
age				    INTEGER 	NOT NULL CHECK ( age >18 AND age < 65 ),
gender		  	TEXT 		NOT NULL CHECK ( gender = 'Man' OR gender = 'Woman'), 

PRIMARY KEY (worker_id) ,
FOREIGN KEY (id) REFERENCES vehicles(id) 

);


INSERT INTO drivers ( id,worker_id,first_name,last_name,age,gender) 

VALUES

(1,12,'David'		  ,'Malak'	  ,40,'Man'),   
(2,46,'Paul'	  	,'Admas'	  ,63,'Man'),
(3,11,'Adam'	  	,'Jones'	  ,24,'Man'), 
(4,18,'Caroline'	,'Malak'	  ,37,'Woman'), 
(5,15,'John'		  ,'Carmack'  ,50,'Man'), 
(6,33,'Aaron'		  ,'Desner'	  ,57,'Man'), 
(7,01,'Jason'	  	,'Coles'	  ,34,'Man'), 
(8,05,'Kirk'	  	,'DeVault'  ,21,'Man'), 
(9,13,'James'	  	,'Patron'	  ,36,'Man'), 
(10,10,'Pauline'	,'Kowalsky' ,52,'Woman'), 
(11,99,'George'		,'Harris'	  ,60,'Man'), 
(12,67,'Dwayne'		,'Nitro'	  ,39,'Man'), 
(13,45,'Sully'		,'Black'	  ,30,'Woman'), 
(14,23,'Irina'		,'Floors'	  ,28,'Woman'), 
(15,20,'Andrew'		,'Lynn'		  ,37,'Man'), 
(16,89,'Malcolm'	,'Daniels'	,20,'Man'), 
(17,06,'Sony'		  ,'Cash'		  ,44,'Man'), 
(18,17,'Chris'		,'Mood'		  ,31,'Man'), 
(19,24,'Shaun'		,'Dallas'	  ,32,'Man'), 
(20,63,'Jeff'	  	,'Sunny'	  ,19,'Man');

--DML shortcuts

DROP TABLE drivers; 
SELECT * FROM drivers;
DELETE FROM drivers WHERE; 
UPDATE drivers SET WHERE; 
ALTER TABLE drivers ADD COLUMN; 


SELECT * FROM vehicles AS t1 LEFT JOIN drivers AS t2 ON t1.id = t2.id;


-- CREATING TABLE direction

CREATE TABLE IF NOT EXISTS direction ( 

id 			  	INTEGER NOT NULL, 
worker_id		INTEGER NOT NULL,		
country 		TEXT 	NOT NULL,			
city   			TEXT	NOT NULL,			

PRIMARY KEY (id), 
FOREIGN KEY (worker_id) REFERENCES drivers (worker_id) ON UPDATE CASCADE  ON DELETE CASCADE,
FOREIGN KEY (id) REFERENCES vehicles (id) 

 );
 
 
INSERT INTO direction (id,worker_id,country,city)

VALUES  

(1,12,		'Poland'	  	,'Bydgoszcz'),
(2,46,		'Englad'		  ,'Bornemouth'),
(3,11,		'Portugal' 	  ,'Lagos'),
(4,18,		'Germany'		  ,'Bonn'),
(5,15,		'Slovakia'	  ,'Bratyslava'),
(6,33,		'Belgium'		  ,'Antwerpia'),
(7,01,		'Spain'			  ,'Valencia'),
(8,05,		'Nederlands'	,'Haga'),
(9,13,		'Spain'			  ,'Malaga'),
(10,10,		'France'		  ,'Rennes'),
(11,99,		'Ostria'		  ,'Innsbruck'),
(12,67,		'Switzerland'	,'Lozanna'),
(13,45,		'Norway'		  ,'Stavanger'),
(14,23,		'Spain'			  ,'Saragossa'),
(15,20,		'Denmark'		  ,'Esbjerg'),
(16,89,		'France'		  ,'Tuluza'),
(17,06,		'England'		  ,'Nottingham'),
(18,17,		'Portugal'		,'Porto'),
(19,24,		'Germany'		  ,'Stuttgard'),
(20,63,	  'Slovakia'	  ,'Koszyce');


 
 
-- DML shortcuts

DROP TABLE directions; 
SELECT * FROM directions ;
DELETE FROM directions WHERE; 
UPDATE directions SET country = 'England' WHERE worker_id == 46; 

--ALTERING

ALTER TABLE directions ADD COLUMN 
route_from  TEXT DEFAULT 'Poland'; 

/* COPYING TABLE FROM direction to new_directions in order to change COLUMN leyout 
and revert action with new table name of old column as DIRECTIONS*/
--------------------------------------------------------------------------------------------------------------

-- CREATING NEW TABLE new_directions

CREATE TABLE new_directions (

id 			    	INTEGER NOT NULL, 
worker_id	  	INTEGER	NOT NULL,
route_from		TEXT    DEFAULT 'Poland',		
country 		  TEXT 	NOT NULL,			
city   			  TEXT	NOT NULL,

PRIMARY KEY (id), 
FOREIGN KEY (worker_id) REFERENCES drivers (worker_id) ON UPDATE CASCADE  ON DELETE CASCADE,
FOREIGN KEY (id) REFERENCES vehicles (id) 

 );
 
-- COPYING  
INSERT INTO  new_directions (id,worker_id,route_from,country,city) 
SELECT id,worker_id,route_from,country,city FROM direction;

SELECT * FROM new_directions;

INSERT INTO  new_directions (id,worker_id,route_from,country,city) 
SELECT id,worker_id,route_from,country,city FROM direction;


-- DROPING OLD TABLE directions

DROP TABLE IF EXISTS direction;

-- CREATING TABLE AGAIN WITH NEW COLUMN route_from

CREATE TABLE IF NOT EXISTS directions (

id 				    INTEGER NOT NULL, 
worker_id		  INTEGER	NOT NULL,
route_from		TEXT    DEFAULT 'Poland',		
country 		  TEXT 	NOT NULL,			
city   		  	TEXT	NOT NULL,

PRIMARY KEY (id), 
FOREIGN KEY (worker_id) REFERENCES drivers (worker_id) ON UPDATE CASCADE  ON DELETE CASCADE,
FOREIGN KEY (id) REFERENCES vehicles (id) 

);

-- COPYING 

INSERT INTO  directions (id,worker_id,route_from,country,city) 
SELECT id,worker_id,route_from,country,city FROM new_directions;

SELECT * FROM directions;

DROP TABLE IF EXISTS new_directions;

---------------------------------------------------------------------------------------------------------------

-- CREATING TABLE drivingtime

CREATE TABLE IF NOT EXISTS "drivingtime" (

id					  INTEGER  PRIMARY KEY AUTOINCREMENT,
worker_id			INTEGER  NOT NULL,
week_no				INTEGER  NOT NULL,
weekday 			TEXT	 NOT NULL,
"Start"				TIME, 			
"end" 				TIME,
distance 			INTEGER	 CHECK (distance  >= 0 ),
			
 
FOREIGN KEY (worker_id) REFERENCES drivers (worker_id)
);



INSERT INTO "drivingtime" (worker_id,week_no,weekday,"start","end",distance
)
 
VALUES
(12,33,'Monday','07:30:01','15:28:01',406),  
(46,33,'Monday','08:44:07','16:32:02',632),
(11,33,'Monday','07:16:16','17:45:04',555), 
(18,33,'Monday','12:30:34','20:10:01',374), 
(15,33,'Monday','11:40:17','20:12:01',508), 
(33,33,'Monday','12:32:15','22:00:05',572), 
(01,33,'Monday','10:33:16','21:20:04',343), 
(05,33,'Monday','12:01:01','20:10:01',620), 
(13,33,'Monday','04:40:12','14:33:03',405),
(10,33,'Monday','03:15:17','11:12:01',520), 
(99,33,'Monday','04:31:01','12:32:56',605), 
(67,33,'Monday','07:16:12','16:43:45',393), 
(45,33,'Monday','11:20:13','21:21:32',590), 
(23,33,'Monday','08:00:01','16:56:02',280), 
(20,33,'Monday','12:00:30','17:10:06',455), 
(89,33,'Monday','15:17:22','01:19:33',603), 
(06,33,'Monday','16:30:01','23:15:21',444), 
(17,33,'Monday','08:12:12','20:36:02',700), 
(24,33,'Monday','06:33:02','18:34:01',566), 
(63,33,'Monday','05:30:16','17:56:12',621);


INSERT INTO "drivingtime" (worker_id,week_no,weekday,"start","end",distance
) 

VALUES
(12,33,'Tuesday','07:45:01','14:29:05',400),   
(46,33,'Tuesday','06:44:07','15:23:03',630),
(11,33,'Tuesday','07:45:16','15:55:03',387), 
(18,33,'Tuesday','10:30:34','18:30:02',467), 
(15,33,'Tuesday','09:40:17','17:21:01',600), 
(33,33,'Tuesday','10:32:15','15:19:01',160), 
(01,33,'Tuesday','10:33:16','18:33:12',420), 
(05,33,'Tuesday','04:01:01','12:21:01',299), 
(13,33,'Tuesday','04:40:12','16:22:10',750),
(10,33,'Tuesday','06:15:17','18:12:01',520), 
(99,33,'Tuesday','10:31:01','15:24:04',300), 
(67,33,'Tuesday','12:16:12','16:10:02',299), 
(45,33,'Tuesday','11:20:13','20:15:01',468), 
(23,33,'Tuesday','08:00:01','17:00:01',500), 
(20,33,'Tuesday','07:00:30','18:21:01',478), 
(89,33,'Tuesday','09:17:22','17:21:02',400), 
(06,33,'Tuesday','06:30:01','18:44:31',600), 
(17,33,'Tuesday','10:12:12','16:55:01',317), 
(24,33,'Tuesday','11:33:02','18:12:01',406), 
(63,33,'Tuesday','12:30:16','22:30:01',503);


INSERT INTO drivingtime ( worker_id,week_no,weekday,"start","end",distance
)
 
VALUES
(12,33,'Wednesday','06:30:01','16:22:31',665),   
(46,33,'Wednesday','06:44:07','18:12:21',635),
(11,33,'Wednesday','05:16:16','14:45:12',244), 
(18,33,'Wednesday','11:30:34','20:42:45',372), 
(15,33,'Wednesday','10:40:17','18:32:23',503), 
(33,33,'Wednesday','09:32:15','19:12:45',573), 
(01,33,'Wednesday','08:33:16','18:23:12',342), 
(05,33,'Wednesday','05:01:01','16:45:03',256), 
(13,33,'Wednesday','06:40:12','15:43:08',358),
(10,33,'Wednesday','09:15:17','18:32:34',512), 
(99,33,'Wednesday','03:31:01','13:13:23',620), 
(67,33,'Wednesday','10:16:12','18:15:11',349), 
(45,33,'Wednesday','08:20:13','16:17:32',303), 
(23,33,'Wednesday','08:00:01','17:31:54',528), 
(20,33,'Wednesday','11:00:30','20:16:22',537), 
(89,33,'Wednesday','09:17:22','21:19:11',620), 
(06,33,'Wednesday','13:30:01','23:47:34',344), 
(17,33,'Wednesday','06:12:12','16:23:21',631), 
(24,33,'Wednesday','05:33:02','18:12:11',232), 
(63,33,'Wednesday','07:30:16','19:46:55',519);


INSERT INTO drivingtime (worker_id,week_no,weekday,"start","end",distance
)
 
VALUES
(12,33,'Thursday','07:30:01','15:28:01',406),   
(46,33,'Thursday','08:44:07','16:32:02',632),
(11,33,'Thursday','07:16:16','17:45:04',555), 
(18,33,'Thursday','12:30:34','20:10:01',374), 
(15,33,'Thursday','11:40:17','20:12:01',508), 
(33,33,'Thursday','12:32:15','22:00:05',572), 
(01,33,'Thursday','10:33:16','21:20:04',343), 
(05,33,'Thursday','12:01:01','20:10:01',620), 
(13,33,'Thursday','04:40:12','14:33:03',405),
(10,33,'Thursday','03:15:17','11:12:01',520), 
(99,33,'Thursday','04:31:01','12:32:56',605), 
(67,33,'Thursday','07:16:12','16:43:45',393), 
(45,33,'Thursday','11:20:13','21:21:32',590), 
(23,33,'Thursday','08:00:01','16:56:02',280), 
(20,33,'Thursday','12:00:30','17:10:06',455), 
(89,33,'Thursday','15:17:22','01:19:33',603), 
(06,33,'Thursday','16:30:01','23:15:21',444), 
(17,33,'Thursday','08:12:12','20:36:02',700), 
(24,33,'Thursday','06:33:02','18:34:01',566), 
(63,33,'Thursday','05:30:16','17:56:12',621);


INSERT INTO drivingtime (worker_id,week_no,weekday,"start","end",distance
)
 
VALUES
(12,33,'Firday','06:30:01','16:22:31',665),   
(46,33,'Firday','06:44:07','18:12:21',635),
(11,33,'Firday','05:16:16','14:45:12',244), 
(18,33,'Firday','11:30:34','20:42:45',372), 
(15,33,'Firday','10:40:17','18:32:23',503), 
(33,33,'Firday','09:32:15','19:12:45',573), 
(01,33,'Firday','08:33:16','18:23:12',342), 
(05,33,'Firday','05:01:01','16:45:03',256), 
(13,33,'Firday','06:40:12','15:43:08',358),
(10,33,'Firday','09:15:17','18:32:34',512), 
(99,33,'Firday','03:31:01','13:13:23',620), 
(67,33,'Firday','10:16:12','18:15:11',349), 
(45,33,'Firday','08:20:13','16:17:32',303), 
(23,33,'Firday','08:00:01','17:31:54',528), 
(20,33,'Firday','11:00:30','20:16:22',537), 
(89,33,'Firday','09:17:22','21:19:11',620), 
(06,33,'Firday','13:30:01','23:47:34',344), 
(17,33,'Firday','06:12:12','16:23:21',631), 
(24,33,'Firday','05:33:02','18:12:11',232), 
(63,33,'Firday','07:30:16','19:46:55',519);


INSERT INTO drivingtime (worker_id,week_no,weekday,"start","end",distance
)
 
VALUES
(12,33,'Saturday','00:00:00','00:00:00',0),   
(46,33,'Saturday','00:00:00','00:00:00',0),
(11,33,'Saturday','00:00:00','00:00:00',0), 
(18,33,'Saturday','00:00:00','00:00:00',0), 
(15,33,'Saturday','11:23:45','15:11:02',301), 
(33,33,'Saturday','00:00:00','00:00:00',0), 
(01,33,'Saturday','00:00:00','00:00:00',0), 
(05,33,'Saturday','00:00:00','00:00:00',0), 
(13,33,'Saturday','00:00:00','00:00:00',0),
(10,33,'Saturday','00:00:00','00:00:00',0), 
(99,33,'Saturday','00:00:00','00:00:00',0), 
(67,33,'Saturday','00:00:00','00:00:00',0), 
(45,33,'Saturday','00:00:00','00:00:00',0), 
(23,33,'Saturday','00:00:00','00:00:00',0), 
(20,33,'Saturday','00:00:00','00:00:00',0), 
(89,33,'Saturday','10:20:15','18:01:10',530), 
(06,33,'Saturday','00:00:00','00:00:00',0), 
(17,33,'Saturday','00:00:00','00:00:00',0), 
(24,33,'Saturday','00:00:00','00:00:00',0), 
(63,33,'Saturday','00:00:00','00:00:00',0);												


INSERT INTO drivingtime ( worker_id,week_no,weekday,"start","end",distance
)
 
VALUES
(12,33,'Sunday','00:00:00','00:00:00',0),   
(46,33,'Sunday','00:00:00','00:00:00',0),
(11,33,'Sunday','00:00:00','00:00:00',0), 
(18,33,'Sunday','00:00:00','00:00:00',0), 
(15,33,'Sunday','00:00:00','00:00:00',0), 
(33,33,'Sunday','00:00:00','00:00:00',0), 
(01,33,'Sunday','00:00:00','00:00:00',0), 
(05,33,'Sunday','00:00:00','00:00:00',0), 
(13,33,'Sunday','00:00:00','00:00:00',0),
(10,33,'Sunday','00:00:00','00:00:00',0), 
(99,33,'Sunday','00:00:00','00:00:00',0), 
(67,33,'Sunday','00:00:00','00:00:00',0), 
(45,33,'Sunday','00:00:00','00:00:00',0), 
(23,33,'Sunday','00:00:00','00:00:00',0), 
(20,33,'Sunday','00:00:00','00:00:00',0), 
(89,33,'Sunday','00:00:00','00:00:00',0), 
(06,33,'Sunday','00:00:00','00:00:00',0), 
(17,33,'Sunday','00:00:00','00:00:00',0), 
(24,33,'Sunday','00:00:00','00:00:00',0), 
(63,33,'Sunday','00:00:00','00:00:00',0);

-- DML shortcuts

DROP TABLE drivingtime; 
SELECT * FROM drivingtime ;
DELETE FROM drivingtime WHERE ;
UPDATE drivingtime SET WHERE ;
ALTER TABLE drivingtime ADD COLUMN; 

-- QUERIES
 
SELECT
t1.worker_id,
t1.first_name,
t1.last_name, 
t2.mark,
t2.chassis,
t3.distance,
t4.country
FROM drivers AS t1 
LEFT JOIN Vehicles AS t2 ON t1.id = t2.id
LEFT JOIN drivingtime AS t3 ON t2.id = t3.id
LEFT JOIN directions AS t4 ON t3.id = t4.id
ORDER BY t1.worker_id ASC;

SELECT AVG(distance) AS avg_dist 
FROM drivingtime WHERE worker_id == 63;

SELECT drivingtime."end"- drivingtime."Start" AS hr_per_day 
FROM drivingtime WHERE worker_id == 12 OR worker_id == 63 
LIMIT 10;

SELECT age, COUNT(*)AS Number_of_employees 
FROM drivers GROUP BY age ORDER BY age DESC;

SELECT number_plate FROM vehicles WHERE euro = 5;

SELECT worker_id,first_name,last_name FROM drivers WHERE worker_id IN 
(SELECT worker_id FROM drivingtime WHERE weekday LIKE 'saturday' AND distance != 0);  

SELECT 
t1.first_name,
t1.last_name,
t2.country 
FROM drivers AS t1 
LEFT JOIN directions AS t2 ON t1.worker_id = t2.worker_id WHERE t1.gender LIKE 'woman';

-- VIEW

CREATE VIEW ladies_at_work_V AS
SELECT 
t1.first_name,
t1.last_name,
t2.country 
FROM drivers AS t1 
LEFT JOIN directions AS t2 ON t1.worker_id = t2.worker_id WHERE t1.gender LIKE 'woman';

SELECT * FROM ladies_at_work_V

-- INDEX

CREATE INDEX idx_drivers 
ON drivers (id,worker_id,first_name,last_name,age,gender);
EXPLAIN QUERY PLAN SELECT * FROM drivers WHERE gender LIKE 'Woman'
DROP INDEX idx_drivers;


-- TRIGER 

CREATE TRIGGER drivingtime_update BEFORE UPDATE ON drivingtime 
BEGIN

SELECT CASE

WHEN NEW.week_no LIKE 53 THEN RAISE (ABORT ,'MAX WEEKS IN THE YEAR IS 52')
END;
END;

UPDATE drivingtime SET week_no = 53 WHERE worker_id == 20;

DROP TRIGGER drivingtime_update;






-- THE END 
