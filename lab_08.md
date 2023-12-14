# 1.a
```mysql
create table uczestnicy as select * from wikingowie.uczestnicy;
create table etapy_wyprawy as select * from wikingowie.etapy_wyprawy;
create table sektor as select * from wikingowie.sektor;
create table wyprawa as select * from wikingowie.wyprawa;
select * from uczestnicy;
select * from wyprawa;
select * from sektor;
select * from ekwipunek;
select * from kreatura;
```
# 1.b
```mysql
SELECT k.nazwa FROM kreatura k left join uczestnicy u on k.idKreatury=u.id_wyprawy WHERE id_wyprawy IS NULL;
```

# 1.c 
```mysql
SELECT u.id_uczestnika, sum(ilosc) FROM ekwipunek e inner join kreatura k on k.idKreatury=e.idKreatury 
inner join uczestnicy u on k.idKreatury=u.id_uczestnika
inner join wyprawa w on w.id_wyprawy=u.id_wyprawy
group by u.id_uczestnika;
```



