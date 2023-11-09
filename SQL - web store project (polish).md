## Opis projektu
:triangular_flag_on_post: Projekt został wykonany podczas rocznego kursu - "Zajavka" na podstawie poleceń do projektu.

![image](https://github.com/Martyelny/Portfolio/assets/115575209/f57455f0-dedd-4bf6-84ce-2e6f027968a4)
![image](https://github.com/Martyelny/Portfolio/assets/115575209/432a7dd4-38b7-4fe2-957e-39831b22debb)

## Polecenia
**1. Stwórz wspomnianą bazę danych.**
```sql
CREATE DATABASE zajavka_store;
```
**2. Stwórz w bazie danych opisane tabele.**
```sql
CREATE TABLE CUSTOMER(
	ID INT PRIMARY KEY,
	USER_NAME VARCHAR(32) NOT NULL UNIQUE,
	EMAIL VARCHAR(32) NOT NULL UNIQUE,
	NAME VARCHAR(32) NOT NULL,
	SURNAME VARCHAR(32) NOT NULL,
	DATE_OF_BIRTH DATE,
	TELEPHONE_NUMBER VARCHAR(32)
);

CREATE TABLE PRODUCER(
	ID INT PRIMARY KEY,
	PRODUCER_NAME VARCHAR(32) NOT NULL UNIQUE,
	ADDRESS VARCHAR(128)
);

CREATE TABLE PRODUCT(
	ID INT PRIMARY KEY,
	PRODUCT_CODE VARCHAR(64) NOT NULL UNIQUE,
	PRODUCT_NAME VARCHAR(64) NOT NULL,
	PRODUCT_PRICE NUMERIC(7,2) NOT NULL,
	ADULTS_ONLY BOOLEAN NOT NULL,
	DESCRIPTION TEXT NOT NULL,
	PRODUCER_ID INT NOT NULL,
	CONSTRAINT FK_PRODUCT_PRODUCER
		FOREIGN KEY (PRODUCER_ID)
			REFERENCES PRODUCER (ID)
);

CREATE TABLE PURCHASE(
	ID INT PRIMARY KEY,
	CUSTOMER_ID INT NOT NULL,
	PRODUCT_ID INT NOT NULL,
	QUANTITY INT NOT NULL,
	DATE_TIME TIMESTAMP WITH TIME ZONE NOT NULL,
	CONSTRAINT FK_PURCHASE_CUSTOMER
		FOREIGN KEY (CUSTOMER_ID)
			REFERENCES CUSTOMER (ID),
	CONSTRAINT FK_PURCHASE_PRODUCT
		FOREIGN KEY (PRODUCT_ID)
			REFERENCES PRODUCT (ID)
);

CREATE TABLE OPINION(
	ID INT PRIMARY KEY,
	CUSTOMER_ID INT NOT NULL,
	PRODUCT_ID INT NOT NULL,
	STARS SMALLINT CHECK (STARS BETWEEN 1 AND 5) NOT NULL,
	COMMENT TEXT NOT NULL,
	DATE_TIME TIMESTAMP WITH TIME ZONE NOT NULL,
	CONSTRAINT FK_OPINION_CUSTOMER
		FOREIGN KEY (CUSTOMER_ID)
			REFERENCES CUSTOMER (ID),
	CONSTRAINT FK_OPINION_PRODUCT
		FOREIGN KEY (PRODUCT_ID)
			REFERENCES PRODUCT (ID)
);
```
**3. Mając stworzone tabele, zasil je danymi.**
```sql
INSERT INTO CUSTOMER (ID, USER_NAME, EMAIL, NAME, SURNAME, DATE_OF_BIRTH, TELEPHONE_NUMBER) VALUES
(1, 'dmcgettrick0', 'dmcgettrick0@infoseek.cjp', 'Dorris', 'McGettrick', '1986-11-18', '90-261-3997'),
(2, 'gseaking1', 'gseaking1@wikipedia.org', 'Gretchen', 'Seaking', '1983-2-25', null),
(3, 'lthurnham2', 'lthurnham2@php.net', 'Libbey', 'Thurnham', '1986-11-15', null);

INSERT INTO PRODUCER (ID, PRODUCER_NAME, ADDRESS) VALUES
(1, 'Heidenreich-Mayer', '477 Hoffman Crossing'),
(2, 'Hayes Group', '8 Novick Street'),
(3, 'Goyette, Dietrich and Cassin', '995 Cambridge Street');

INSERT INTO PRODUCT (ID, PRODUCT_CODE, PRODUCT_NAME, PRODUCT_PRICE, ADULTS_ONLY, DESCRIPTION, PRODUCER_ID) VALUES
(1, '58394-014', 'Chivas Regal - 12 Year Old', 16.29, false, 'Befv mcmo tgzs rpgt zcpb', 1),
(2, '55319-866', 'Fennel', 38.49, false, 'Lbyq bfwo pqux mppe tjpq', 2),
(3, '0008-0407', 'Muffin Batt - Ban Dream Zero', 14.85, false, 'Sujh xcjs dhjx djeb vbdp', 3);

INSERT INTO PURCHASE (ID, CUSTOMER_ID, PRODUCT_ID, QUANTITY, DATE_TIME) VALUES
(1, 85, 24, 4, '2018-06-14 09:46:57 -03:00'),
(2, 91, 23, 7, '2018-06-28 22:39:39 +05:00'),
(3, 27, 40, 4, '2017-12-08 21:08:56 -01:00');

INSERT INTO OPINION (ID, CUSTOMER_ID, PRODUCT_ID, STARS, COMMENT, DATE_TIME) VALUES
(1, 69, 39, 3, 'Giaa tuh zszyqsn rhqh wmidxby ezwxa', '2016-07-17 21:20:32 -05:00'),
(2, 94, 2, 3, 'Ncdk gaz dxlsblh zuxs shpaofs wssbs', '2018-02-07 08:56:46 +07:00'),
(3, 80, 4, 1, 'Xrku cvm nhukkdv rrxd sfmhwin cfppg', '2015-01-11 04:26:17 +07:00');
```
Dane wygenerowane zostały ze strony www.mackaroo.com. W celu utrzymania porządku pokazane zostały 3 przykładowe rekordy do każdej tabeli.

Tabele posiadają następującą liczbę rekordów:
* **CUSTOMER** - 100 rekordów
* **PRODUCER** - 20 rekordów
* **PRODUCT** - 50 rekordów
* **PURCHASE** - 300 rekordów
* **OPINION** - 140 rekordów

**4. Usuń wszystkie opinie o ocenie niższej niż 4.**
```sql
DELETE FROM OPINION
WHERE STARS < 4;
```
```sql
SELECT * FROM OPINION;
```
**:rewind: PRZED:**

![image](https://github.com/Martyelny/Portfolio/assets/115575209/720a9b2a-1401-462b-bf01-d6c077d061c5)
**:fast_forward: PO:**

![image](https://github.com/Martyelny/Portfolio/assets/115575209/6f4a3ed6-089d-403b-a295-6692b54811c2)

**5. Wyświetl unikalne kody produktów, które zostały zakupione przed datą '2020-02-01'.**
```sql
SELECT DISTINCT PR.PRODUCT_CODE
FROM PURCHASE AS PUR
  INNER JOIN PRODUCT AS PR ON PUR.PRODUCT_ID = PR.ID
WHERE PUR.DATE_TIME < '2020-02-01'
ORDER BY PRODUCT_CODE;
```
![image](https://github.com/Martyelny/Portfolio/assets/115575209/54d68dfb-2143-40b3-82c1-e7c3dcf5c7ef)

**6. Wyświetl na ekranie kody oraz ilość dokonanych transakcji zakupowych dla 5 produktów, które
pojawiają się w największej ilości transakcji. Wynik posortuj malejąco na podstawie ilości
dokonanych transakcji zakupowych. Ilość dokonanych transakcji zakupowych nie oznacza, że
produkt jest kupowany najczęściej w obrębie jednej transakcji zakupowej, tylko oznacza, że produkt
pojawia się w największej ilości dokonanych transakcji zakupowych.**
```sql
SELECT PRODUCT_CODE, COUNT(*) AS PRODUCT_COUNT
FROM PURCHASE AS PUR
  INNER JOIN PRODUCT AS PR ON PUR.PRODUCT_ID = PR.ID
GROUP BY PR.PRODUCT_CODE
ORDER BY PRODUCT_COUNT DESC
LIMIT 5;
```
![image](https://github.com/Martyelny/Portfolio/assets/115575209/4e57eb56-8e6f-41ab-bd4e-354cadb7fa5e)

**7. Wyświetl na ekranie wszystkich klientów którzy zakupili produkty przeznaczone dla dorosłych
(flaga ADULTS_ONLY ustawiona na true).**
```sql
SELECT DISTINCT CUS.ID, CUS.NAME, CUS.SURNAME, PR.PRODUCT_CODE, ADULTS_ONLY
FROM PURCHASE
  INNER JOIN PRODUCT AS PR ON PRODUCT_ID = PR.ID
  INNER JOIN CUSTOMER AS CUS ON CUSTOMER_ID = CUS.ID
WHERE PR.ADULTS_ONLY IS TRUE;
```
![image](https://github.com/Martyelny/Portfolio/assets/115575209/a6e94c24-9407-45cb-8e8b-542b0d2ced91)

**8. Wprowadzamy promocję w naszym sklepie i chcemy aby wszystkie produkty od producenta Bruen
Group, które kosztują więcej niż 50 pieniędzy zostały przecenione na 40 pieniędzy.**
```sql
UPDATE PRODUCT
SET PRODUCT_PRICE = 40
WHERE 
PRODUCER_ID IN (SELECT ID FROM PRODUCER WHERE PRODUCER_NAME = 'Bruen Group') 
AND PRODUCT_PRICE > 50;
```
```sql
SELECT * FROM PRODUCT
WHERE PRODUCER_ID IN (SELECT ID FROM PRODUCER WHERE PRODUCER_NAME = 'Bruen Group');
```
**:rewind: PRZED:**

![image](https://github.com/Martyelny/Portfolio/assets/115575209/fe7165c0-90c8-440a-829b-24fdf59ddf64)

**:fast_forward: PO:**

![image](https://github.com/Martyelny/Portfolio/assets/115575209/eee07a35-e954-44b2-a0a6-7e8874af4398)

**9. Znajdź osoby, które wystawiły co najmniej jedną opinię o wartości 5 gwiazdek.**
```sql
SELECT DISTINCT CUSTOMER_ID, USER_NAME, STARS
FROM OPINION AS OP
  INNER JOIN CUSTOMER AS CUS ON CUSTOMER_ID = CUS.ID
WHERE STARS = 5
ORDER BY CUSTOMER_ID
```
![image](https://github.com/Martyelny/Portfolio/assets/115575209/653e9982-21b6-4359-8281-03524a3e1941)

**10. Znajdź producenta, który sprzedaje najwięcej produktów w naszym sklepie.**
```sql
SELECT PRODUCER_NAME, COUNT(PRODUCT_CODE) PC
FROM PURCHASE AS PUR
  INNER JOIN PRODUCT AS PR ON PRODUCT_ID = PR.ID
  INNER JOIN PRODUCER AS PRD ON PRODUCER_ID = PRD.ID
GROUP BY PRODUCER_NAME
ORDER BY PC DESC
LIMIT 1;
```
![image](https://github.com/Martyelny/Portfolio/assets/115575209/0a146736-f0c2-4186-bfd4-6c0f376eacf4)

**11. Wyświetl na ekranie drugi najdroższy produkt (minimum nazwa i cena). Możesz wykorzystać
klauzulę OFFSET.**
```sql
SELECT PRODUCT_NAME, PRODUCT_PRICE
FROM PRODUCT
ORDER BY PRODUCT_PRICE DESC
OFFSET 1
LIMIT 1;
```
![image](https://github.com/Martyelny/Portfolio/assets/115575209/6cdf97b0-803f-4381-bb59-f18e9acbe6a9)

**12. Wyświetl na ekranie nazwy 10 najczęściej ocenianych produktów.**
```sql
SELECT PRODUCT_NAME, COUNT(*)
FROM OPINION
  INNER JOIN PRODUCT AS PR ON PRODUCT_ID = PR.ID
GROUP BY PRODUCT_NAME
ORDER BY COUNT DESC
LIMIT 10;
```
![image](https://github.com/Martyelny/Portfolio/assets/115575209/3bea9453-66c6-492d-9d3e-36d18a7831fd)

**13. Oblicz ile zarobiliśmy w naszym sklepie w każdym miesiącu od uruchomienia sklepu.**
```sql
WITH TMP AS(
	SELECT
		DATE_TRUNC('month', PUR.DATE_TIME) AS DATE_TIME,
		PUR.QUANTITY,
		PR.PRODUCT_PRICE,
		PUR.QUANTITY * PR.PRODUCT_PRICE AS INCOME_PER_PRODUCT
	FROM PURCHASE PUR
		INNER JOIN PRODUCT PR ON PR.ID = PUR.PRODUCT_ID
	ORDER BY DATE_TIME, INCOME_PER_PRODUCT
)
SELECT TMP.DATE_TIME, SUM(TMP.INCOME_PER_PRODUCT) AS INCOME
	FROM TMP
GROUP BY TMP.DATE_TIME
ORDER BY TMP.DATE_TIME;
```
![image](https://github.com/Martyelny/Portfolio/assets/115575209/290bb58d-4838-48e3-bd9a-3c3a80815ac1)

