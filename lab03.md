# lab03 zad1
```mysql
SELECT imie, nazwisko, data_urodzenia FROM pracownik;
```
# zad2
```mysql
SELECT imie, nazwisko, datediff(now(), data_urodzenia) FROM pracownik;
```
# zad3
```mysql
SELECT dzial, count(id_pracownika) FROM pracownik group by dzial;
```
# zad4 
```mysql
SELECT nazwa_towaru, count(id_towaru) FROM towar group by nazwa_towaru;
```
# zad5
```mysql
SELECT k.nazwa_kategori, group_concat(t.nazwa_towaru) FROM towar t inner join
kategoria k on k.id_kategori=t.kategoria group by k.nazwa_kategori;
```
# zad6
```mysql
SELECT round(AVG(pensja), 2) from pracownik;
```
# zad7
```mysql
SELECT AVG(pensja) from pracownik where ('2024'-year(data_zatrudnienia)) > 5;
SELECT data_zatrudnienia, pensja FROM pracownik;
```
# zad8
```mysql
SELECT t.nazwa_towaru, pw.towar, sum(pw.ilosc) FROM
pozycja_zamowienia pw inner join towar t on pw.towar=t.id_towaru
group by towar order by sum(pw.ilosc) desc limit 10;
```
# zad9
```mysql
SELECT z.numer_zamowienia, sum(pw.ilosc*pw.cena) FROM zamowienie z inner join
pozycja_zamowienia pw on z.id_zamowienia=pw.zamowienie 
WHERE quareter(z.data_zamowienia)=1 AND YEAR(z.data_zamowienia)=2017
group by z.id_zamowienia;
```
# zad10
```mysql
SELECT z.numer_zamowienia, sum(pw.ilosc*pw.cena) FROM zamowienie z inner join
pozycja_zamowienia pw on z.id_zamowienia=pw.zamowienie  inner join pracownik p on p.id_pracownika=z.pracownik_id_pracownika
group by pw.id_pracownika order by wartosc desc;
```
