# Zadania lab 04
## zad 1
###### zad 1, pkt 1
```sql
create table postac( id_postaci int auto_increment primary key, nazwa varchar(40), rodzaj enum('wiking', 'ptak', 'kobieta'), data_ur date, wiek int unsigned);

+------------+----------+---------+------------+------+
| id_postaci | nazwa    | rodzaj  | data_ur    | wiek |
+------------+----------+---------+------------+------+
|          1 | Bjorn    | wiking  | 1700-11-09 |  323 |
|          2 | Drozd    | ptak    | 2020-01-10 |    3 |
|          3 | Tesciowa | kobieta | 1970-05-03 |   53 |
+------------+----------+---------+------------+------+
3 rows in set (21.37 sec)

mysql> insert into postac values(default,'Tesciowa','kobieta','1970-05-03',53);

```
## zad 2

```sql
create table walizka( id_walizki int primary key auto_increment, pojemnosc int unsigned, kolor enum('rozowy', 'czerwony', 'teczowy', 'zolty'), id_wlasciciela int, foreign key(id_wlasciciela) references postac(id_postaci) on delete cascade);

alter table walizka alter kolor set default 'rozowy';

mysql> describe walizka;
+----------------+---------------------------------------------+------+-----+---------+----------------+
| Field          | Type                                        | Null | Key | Default | Extra          |
+----------------+---------------------------------------------+------+-----+---------+----------------+
| id_walizki     | int                                         | NO   | PRI | NULL    | auto_increment |
| pojemnosc      | int unsigned                                | YES  |     | NULL    |                |
| kolor          | enum('rozowy','czerwony','teczowy','zolty') | YES  |     | rozowy  |                |
| id_wlasciciela | int                                         | YES  | MUL | NULL    |                |
+----------------+---------------------------------------------+------+-----+---------+----------------+


insert into walizka values(default,50,default,1);

insert into walizka values(default,50,default,3);

select * from walizka;
+------------+-----------+--------+----------------+
| id_walizki | pojemnosc | kolor  | id_wlasciciela |
+------------+-----------+--------+----------------+
|          1 |        50 | rozowy |              1 |
|          2 |        50 | rozowy |              3 |
+------------+-----------+--------+----------------+



```
## zad 3
```sql
create table izba (
adres_budynku varchar(50) not null,
adres_izby varchar(50) not null,
metraz mediumint unsigned,
wlasciciel int,
foreign key (wlasciciel)
references postac(id_postaci) on delete set null
);

alter table izba add column
kolor varchar(30) default 'czarny'
after metraz;

insert into izba values
('kolejowa 23','spiżarnia',10,default,1);

alter table izba add primary key(adres_budynku, nazwa_izby);

+---------------+------------+--------+--------+------------+
| adres_budynku | nazwa_izby | metraz | kolor  | wlasciciel |
+---------------+------------+--------+--------+------------+
| kolejowa 23   | spizarnia  |     10 | czarny |          1 |
+---------------+------------+--------+--------+------------+



```

## zad 4
```sql
create table przetwory (
id_przetworu int auto_increment primary key, 
rok_produkcji smallint default 1654, 
id_wykonawcy int, foreign key (id_wykonawcy) references postac(id_postaci),
zawartosc varchar(100),
dodatek varchar(50) default 'papryczka chilli',
id_konsumenta int, foreign key (id_konsumenta) references postac(id_postaci)
);

insert into przetwory values (default,default,1,'bigos',default,3);


+--------------+---------------+--------------+-----------+------------------+---------------+
| id_przetworu | rok_produkcji | id_wykonawcy | zawartosc | dodatek          | id_konsumenta |
+--------------+---------------+--------------+-----------+------------------+---------------+
|            1 |          1654 |            1 | bigos     | papryczka chilli |             3 |
+--------------+---------------+--------------+-----------+------------------+---------------+
```

## zad 5
```sql
insert into postac values(default,'Gilli','wiking','1691-08-08',332); #to razy 5

create table statek(
nazwa_statku varchar(100) primary key not null,
rodzaj_statku enum('slup','brygantyna','galeon'),
data_wodowania date,
max_ladownosc int unsigned);
select * from postac;
insert into statek values('tytanik','galeon','2020-11-12','83');
insert into statek values('caleuche','slup','2018-10-11','20');
update postac set funkcja='kapitan' where id_postaci=1;




```


https://dillinger.io/ <---- to ważne


tekst **pogrubiony** lub _kursywa_

```sql
SELECT * FROM osoba;
```

```python
def funkcja():
  print("Ala ma kota")
```
polecenie `SELECT` służy wybieraniu danych z bazy

lista tego typu
1. Punkt 1.
2.  Punkt 2.
   2.1. punkt 2.1
3. itd
4. itd
5. itd

lista tamtego typu
* punkt 1
* punkt 2
  * punkt 2.1
  * punkt 2.2
