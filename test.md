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
