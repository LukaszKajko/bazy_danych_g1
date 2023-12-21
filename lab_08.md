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
# 2.a

# 2.b 
SELECT ew.sektor, s.nazwa, ew.kolejnosc, w.data_rozpoczecia, k.nazwa
FROM etapy_wyprawy ew inner join sektor s on ew.sektor=s.id_sektora 
inner join wyprawa w on w.id_wyprawy=ew.idWyprawy
inner join kreatura k on k.idKreatury=w.kierownik
order by w.data_rozpoczecia asc, ew.kolejnosc asc;

# 3.a
SELECT s.nazwa, ew.sektor FROM sektor s left join etapy_wyprawy ew on s.id_sektora=ew.sektor;

# 3.b
SELECT k.nazwa, if(count(u.id_uczestnika)))>0,
 'brał udział w wyprawie', 'nie brał udziału w wyprawie' FROM
 uczestnicy u right join kreatura k on k.idKreatury=u.id_uczestnika
group by k.nazwa;

# 4.a 
SELECT w.nazwa, sum(length(ew.dziennik)) FROM
wyprawa w inner join etapy_wyprawy ew on w.id_wyprawy=ew.idWyprawy group by w.nazwa HAVING sum(length(ew.dziennik))<400;

# 4.b 
SELECT w.nazwa, (z.waga*z.ilosc/count(distinct u.id_uczestnika)) FROM
wyprawa w inner join uczestnicy u on w.id_wyprawy=u.id_wyprawy
inner join kreatura k on u.id_uczestnika=k.idKreatury
inner join ekwipunek e on k.idKreatury=e.idKreatury
inner join zasob z on e.idZasobu=z.idZasobu
group by w.nazwa;

# 5
SELECT k.nazwa, datediff(w.data_rozpoczecia, k.dataUR) FROM
kreatura k inner join uczestnicy u on k.idKreatury=u.id_uczestnika
inner join wyprawa w on u.id_wyprawy=w.id_wyprawy
inner join etapy_wyprawy ew on w.id_wyprawy=ew.idWyprawy
where ew.sektor=7;



