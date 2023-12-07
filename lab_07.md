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
