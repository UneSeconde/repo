# lab04
## zad 1
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

+--------------+---------------+----------------+---------------+
| nazwa_statku | rodzaj_statku | data_wodowania | max_ladownosc |
+--------------+---------------+----------------+---------------+
| caleuche     | slup          | 2018-10-11     |            20 |
| tytanik      | galeon        | 2020-11-12     |            83 |
+--------------+---------------+----------------+---------------+


update postac set funkcja='kapitan' where id_postaci=1;
alter table postac add jaki_Statek varchar(100);
alter table postac add foreign key (jaki_statek) references statek(nazwa_Statku);
update postac set jaki_statek='caleuche' where id_postaci=7;

+------------+----------+---------+------------+------+---------+-------------+
| id_postaci | nazwa    | rodzaj  | data_ur    | wiek | funkcja | jaki_Statek |
+------------+----------+---------+------------+------+---------+-------------+
|          1 | Bjorn    | wiking  | 1700-11-09 |  323 | kapitan | tytanik     |
|          2 | Drozd    | ptak    | 2020-01-10 |    3 | NULL    | tytanik     |
|          3 | Tesciowa | kobieta | 1935-05-03 |   88 | NULL    | NULL        |
|          4 | Asgaut   | wiking  | 1702-03-12 |  321 | NULL    | caleuche    |
|          5 | Bork     | wiking  | 1698-05-12 |  325 | NULL    | caleuche    |
|          6 | Diarf    | wiking  | 1690-05-12 |  333 | NULL    | tytanik     |
|          7 | Einar    | wiking  | 1693-10-03 |  330 | NULL    | caleuche    |
|          8 | Gilli    | wiking  | 1691-08-08 |  332 | NULL    | tytanik     |
+------------+----------+---------+------------+------+---------+-------------+

delete from izba;
drop table izba;



```
# lab05
## zad 1
```sql
delete from postac where wiek=332;

alter table przetwory
drop foreign key przetwory_ibfk_2;

alter table postac change
id_postaci id_postaci int;

alter table postac drop primary key;

```

## zad 2
```sql
alter table postac add column pesel char(11) first;
update postac set pesel='53817293811' + id_postaci;
alter table postac add primary key(pesel);

alter table postac modify rodzaj enum('wiking','ptak','kobieta','syrena');

insert into postac values(53817293819,8,'Gertruda nieszczera','syrena','1691-08-08',332,default,default);
```

## zad 3
```sql
update postac set jaki_statek='tytanik' where nazwa like '%a%';

insert into statek values('santa maria','brygantyna','1950-10-11','60');
update statek set max_ladownosc=max_ladownosc*0.3 where data_wodowania >='1901-01-01' and data_wodowania <= '2000-12-31';

alter table postac add check(wiek<1000);
#update postac set wiek=2000 where nazwa='bjorn';
#Error Code: 3819. Check constraint 'postac_chk_1' is violated.

```
## zad 4
```sql
alter table postac modify rodzaj enum('wiking','ptak','kobieta','syrena','waz');
insert into postac values(53817293820,9,'waz loko','waz','1993-08-08',30,null,null);

create table marynarz like postac;
insert into marynarz select * from postac where jaki_statek is not null;

alter table marynarz add foreign key(jaki_statek) references statek(nazwa_statku);
```
## zad 5
```sql
update postac set jaki_statek=null;

delete from postac where id_postaci=4;

alter table marynarz drop foreign key marynarz_ibfk_1;
delete from statek;

alter table postac drop foreign key postac_ibfk_1;
drop table statek;

create table zwierz(id_zwierzaka int primary key auto_increment, nazwa varchar(80), wiek smallint);

insert into zwierz values(default, 'drozd', 3);
insert into zwierz values(default, 'waz loko', 30);
```

# lab 06
## zad 1
create table kreatura as select * from
wikingowie.kreatura;



create table zasob as select * from
wikingowie.zasob;


create table ekwipunek as select * from
wikingowie.ekwipunek;


select * from zasob where rodzaj='jedzenie';
select idZasobu, ilosc from zasob where idZasobu in (1,3,5);

##zad 2
select * from kreatura;
select * from kreatura where rodzaj <> 'wiedzma' and  udzwig>50 or udzwig=50;
select * from zasob where waga between 2 and 5;
select * from kreatura where nazwa='%or%' and udzwig between 30 and 70;

## zad 3
select * from zasob;
select * from zasob where month(datapozyskania) =7 or month(datapozyskania)=8;
select * from zasob where rodzaj is not null order by waga asc;
select * from kreatura where dataur is not null order by dataur asc limit 5

##zad 4
select distinct(rodzaj) from kreatura;
select distinct rodzaj from zasob;
select * from zasob where rodzaj is null;
select concat(nazwa, ' - ', rodzaj) from kreatura where rodzaj like 'wi%';
select concat('Ala', 'ma', 'kota') as zdanie;
select concat(nazwa, 'to id=', idkreatury) from kreatura;
select concat(nazwa, ' - ', rodzaj) from kreatura where rodzaj like 'wi%';
select * from zasob;
select concat(nazwa ,ilosc*waga) from zasob where year(datapozyskania) between 2000 and 2007;

##zad 5
select * from zasob where rodzaj='jedzenie';
select concat(nazwa, ' netto = ', waga*0.7, ', waga odpadow = ', waga*0.3) from zasob where rodzaj='jedzenie';
select * from zasob where rodzaj is null;
select distinct nazwa,rodzaj from zasob where nazwa like 'Ba%' or nazwa like '%os'order by nazwa;



https://dillinger.io/ <---- to ważne
