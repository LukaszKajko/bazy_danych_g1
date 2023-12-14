## avg(), sum(), min(), max(), count()
## group by
## having - określa dodatkowy warunek filtrowania

# 1.a
```sql
SELECT SUM(waga) FROM kreatura WHERE  rodzaj='wiking';
```
# 1.b
```sql
SELECT SUM(waga)/SUM(rodzaj='wiking') FROM kreatura WHERE  rodzaj='wiking';
SELECT * FROM kreatura order by rodzaj;
SELECT rodzaj, count(*) FROM kreatura GROUP BY rodzaj;
```
# 1.c
```sql
SELECT rodzaj, avg(2023 - year(dataUR)) AS wiek FROM kreatura group by rodzaj;
```
# 2.a 
```sql
SELECT * FROM zasob;
```
# 2.b
```sql
SELECT avg(waga) FROM zasob WHERE ilosc > 4 group by rodzaj having SUM(waga) > 10;
```
# 2.c
```sql
SELECT avg(waga) FROM zasob WHERE ilosc > 4 group by rodzaj having count(*) > 1;
SELECT rodzaj, count(distinct (nazwa)) from zasob group by rodzaj having count(*) > 1;
```
# 3.a
```sql
SELECT * FROM kreatura, ekwipunek WHERE kreatura.idKreatury=ekwipunek.idKreatury;
SELECT k.nazwa, e.idZasobu, e.ilosc FROM kreatura k inner join ekwipunek e on k.idKreatury=e.idKreatury
inner join zasob z on e.idZasobu=z.idZasobu;
```
# 3.b
```sql
SELECT k.nazwa, e.idZasobu, e.nazwa FROM kreatura k left join ekwipunek e on k.idKreatury=e.idKreatury inner join zasob z on e.idZasobu=z.idZasobu;
```
# 3.c
```sql
SELECT k.nazwa, e.idZasobu, e.ilosc FROM kreatura k left join ekwipunek e on k.idKreatury=e.idKreatury
 where e.idKreatury is null; #left join - warunek z null
SELECT idKreatury FROM kreatura WHERE idKreatury
not in (SELECT distinct idKreatury FROM ekwipunek WHERE idKreatury is not null);
```
# 4.a 
```sql
SELECT * FROM kreatura NATURAL JOIN ekwipunek;
```
# 4.b 
```sql
SELECT k.nazwa, k.dataUR, z.rodzaj FROM  kreatura k inner join ekwipunek e on k.idKreatury=e.idKreatury
inner join zasob z on e.idZasobu=z.idZasobu
where z.rodzaj ='jedzenie' order by k.dataUr desc limit 5;
```
## określanie niezbędnych kolumn
## koreślanie filtrów (where)
## pozostałe (having, order by, limit)
# 4.c
```sql
select concat(k1.nazwa,'-',k2.nazwa) FROM kreatura k1 inner join kreatura k2 on k1.idKreatury-k2.idKreatury = 5;
```
# 5.a
```sql
SELECT k.rodzaj, avg(e.ilosc * z.waga) FROM  kreatura k inner join ekwipunek e on k.idKreatury=e.idKreatury
inner join zasob z on e.idZasobu=z.idZasobu
where k.rodzaj not in ('małpa', 'wąż') and e.ilosc < 30
group by k.rodzaj;
```
# 5.b
```sql
SELECT rodzaj, min(dataUr) najmłodsza, max(dataUr) najstarsza from kreatura group by rodzaj;
```
