## BEFORE i AFTER
## INSERT UPDATE DELETE
## NEW -> INSERT, UPDATE
## OLD-> UPDATE, DELETE
# 1
```mysql
DELIMITER //
CREATE TRIGGER kreatura_before_insert 
BEFORE INSERT ON kreatura
FOR EACH ROW 
BEGIN 
	IF NEW.waga<=0
	THEN 
		SET NEW.waga=1;
	END IF;
END
//
DELIMITER;
```
```mysql
# 2
SELECT w.id_wyprawy, w.nazwa, w.data_rozpoczecia, w.data_zakonczenia, k.nazwa
FROM wyprawa w inner join kreatura k on k.idKreatury=w.kierownik
WHERE id_wyprawy=1;
BEFORE DELETE ON wyprawa 
FOR EACH ROW
BEGIN;

SHOW TRIGGERS;
SHOW CREATE TRIGGER nazwa;
DROP TRIGGER nazwa;
```
