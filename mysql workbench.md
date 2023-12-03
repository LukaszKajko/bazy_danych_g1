# zadanie 5
```sql

insert into postac   ;

create table statek  ;

insert into statek   ;

alter title postac and column funkcja  ;

update postac set..where...  ;
#dodajemy kolumnę która posłuży jako kolumna klucza obcego do tabeli statek
alter table postac add column statek varchar(60) ;
#dodajemy klucz obcy
alter table postac add foreign key..  ;

update postac set statek=.. where... ;

delete from izba where ....;

drop table izba;


create table przetwory(
dodatek varchar(60) default ("papryczka chilli"),
id_przetworu int auto_increment PRIMARY KEY,
rok_produkcji smallint default(1654),
foreign key(id_wykonawcy),
zawartosc text,
references postac(id_postaci),

);
create table izba(
adres_budynku varchar(60) PRIMARY KEY,
nazwa_izby varchar(60) PRIMARY KEY,
metraz int unsigned);
insert into izba values
("Wojska Polskiego 6", "spiżarnia", 15);

create table postac(
id_postaci int auto_increment primary key,
nazwa varchar(40) not null,
rodzaj enum("wiking", "ptak", "kobieta"),
data_ur date,
wiek int unsigned
);
insert into postac values
("Bjorn", "wiking", "1990-08-31", 33),
("Drozd", "ptak", "2003-06-09", 20),
("Tesciowa", "kobieta","1945-05-05", 88);
insert into postac values
(default, "Astrid", "wiking", "2005-02-20", 18),
(default, "olaf", "wiking", "2010-03-10", 13),
(default, "Ragnar", "wiking", "2001-10-30", 22),
(default, "Ivar", "wiking", "1999-01-12", 24),
(default, "Thor", "wiking", "1980-05-10", 43);

create table statek(
nazwa_statku varchar(60) primary key,
rodzaj_statku enum("galeon", "fregata"),
data_wodowania date,
max_ladownosc int unsigned);
insert into statek values
("czarna perła", "galeon", "16-11-2015", 15),
("xpp", "fregata", "15-10-2019", 45);
select * from statek;
select * from postac;
update postac set statek= "fregata" where nazwa = Bjorn
alter title postac and column(funkcja)varchar(60);
delete from izba where spiżarnia;
drop table izba;
delete from postac 
where rodzaj = "wiking" 
and nazwa <> "Bjorn"
order by data_ur asc limit 2;

describe postac;
alter table postac change id_postaci id_postaci int;
alter table postac modify id_postaci int;
alter table postac drop primary key;

show create table postac;
```
# zadanie 2
```sql
alter table postac add column pesel char(11) first;
alter table postac add primary key(pesel);
select * from postac;
update postac set pesel= '13563847543' + id_postaci;
select '13563847543' + id_postaci from postac;
```
# zad2 punkt.b 
```sql
alter table postac modify rodzaj enum("wiking", "ptak", "kobieta", "syrena");
insert into postac values
( "45829371839", 4, "Gertruda Nieszczera", "syrena", "1890-03-03", 133);
desc postac;
#% - dowolny ciąg znaków _ = dokładnie 1 znak
update postac set statek= "fregata"
select nazwa from postac where nazwa like '[a]';

#select nazwa from postac where regexp "[ae]";
select * from statek;
#where data_wodowania >= "1901-01-01"
#and data_wodowania <= "2000-12-31"
#where data_wodowania between "1901-01-01" and "2000-12-31";

update statek
set max_ladownosc = max_ladownosc * 0,7
where year(data_wodowania)
between 1901 and 2000;
```
# zad 3 c
```sql
#instrukcja check 
alter table postac add check (wiek <= 1000);
update postac set wiek = 2000 where nazwa='Bjorn';
#zadanie 4
#krok 1 dodanie węża do pola rodzaj
alter table postac modify rodzaj enum("wiking", "ptak", "kobieta", "syrena", "wąż");
insert into postac values
( "99929371839", 5, "Loko", "wąż", "2005-05-05", 18);
```
# zad4 b
```sql
create table marynarz like postac;
create table marynarz2
select pesel, nazwa, rodzaj from postac;
select * from marynarz2;
insert into marynarz select * from postac
where statek is not null;
select* from marynarz;
alter table marynarz modify statek foreign key references to statek;
```
## opcja nr2
```sql
create table marynarz3 as select * from postac
where statek is not null;

update statek null

usnac statki
drop statek
insert into select(nazwa,wiek,liczba)
```
## a
```sql
update marynarz set nazwa_statku= null where id_postaci=1, 2, 3, 4, 5;
```
## b 
```sql
drop table postac where nazwa = 'olaf';
```
## c 

## d 
```sql
drop table statek;
```
## e
```sql
create table zwierz select id_postaci, nazwa, wiek from postac;
```
## f 
```sql
insert into zwierz select * from postac 
where rodzaj=('wąż', 'ptak');
```
# lab06
```sql
create table kreatura as select * from wikingowie.kreatura;
create table zasob as select * from wikingowie.zasob;
create table ekwipunek as select * from wikingowie.ekwipunek;
desc kreatura;
SELECT * FROM kreatura;
SELECT * FROM zasob;
SELECT * FROM zasob WHERE rodzaj="jedzenie";
SELECT idZasobu, ilosc FROM ekwipunek WHERE idKreatury IN (1,2,3);
SELECT * FROM kreatura WHERE NOT nazwa="wiedzma" AND udzwig>=50;
SELECT * FROM zasob WHERE waga between "2" AND "5";
SELECT * FROM kreatura WHERE nazwa='%or%' AND udzwig between "30" AND "70";
SELECT * FROM zasob where MONTH(dataPozyskania) between 07 and 08;
SELECT * FROM zasob ORDER BY rodzaj;
SELECT * FROM kreatura ORDER BY dataUR DESC LIMIT 5;
SELECT distinct rodzaj FROM zasob; #nie powtarzają się rodzaje, unikalość
SELECT distinct(rodzaj) FROM kreatura;
SELECT nazwa, ilosc, rodzaj FROM zasob WHERE rodzaj='jedzenie' and ilosc=1;
SELECT concat('Ala', 'ma', 'kota');   #złączanie wartości
SELECT concat(nazwa, 'to', 'id', idKreatury);
SELECT rodzaj, nazwa FROM kreatura WHERE rodzaj LIKE 'wi%'; #pokazuje tylko rodzaje zaczynające się na "wi"
SELECT (ilosc * waga) FROM zasob
where year(dataPozyskania)
between 2000 and 2007;
SELECT SUM((ilosc * waga) * 0.3) FROM zasob
where year(dataPozyskania)
between 2000 and 2007;
SELECT SUM((ilosc * waga) * 0.7) FROM zasob
where year(dataPozyskania)
between 2000 and 2007;

SELECT * FROM zasob WHERE rodzaj IS NULL; #wyświetla tylko puste
SELECT * FROM zasob WHERE nazwa LIKE 'Ba%' OR nazwa LIKE'%os' ORDER BY nazwa ASC;

```

