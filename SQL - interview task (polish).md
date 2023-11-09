## Opis zadania
W bazie danych PostgreSQL stwórz tabelę, która będzie przechowywać dane o pracownikach: imię, nazwisko, data urodzenia, kwota wynagrodzenia oraz początek i koniec zatrudnienia. Na bazie stworzonej tabeli stwórz widok zmaterializowany prezentujący aktualnie zatrudnionych pracowników (imię, nazwisko oraz kwota wynagrodzenia) oraz widok – raport pokazujący liczbę pracowników zatrudnionych w kolejnych latach.

## Rozwiązanie
**1. Stworzenie tabeli pracowników.**
```sql
CREATE TABLE EMPLOYEES(
	ID SERIAL PRIMARY KEY,
	NAME VARCHAR(64) NOT NULL,
	SURNAME VARCHAR(64) NOT NULL,
	DATE_OF_BIRTH DATE,
	SALARY_AMOUNT NUMERIC(10,2) NOT NULL,
	START_OF_EMPLOYMENT DATE NOT NULL,
	END_OF_EMPLOYMENT DATE
);
```
```sql
SELECT * FROM EMPLOYEES;
```
![image](https://github.com/Martyelny/Portfolio/assets/115575209/5f684295-d369-4486-a932-453ee0534769)

**2. Wprowadzenie dodatkowych danych w postaci recordów, aby pokazać wyniki zadania.**
```sql
INSERT INTO EMPLOYEES 
(ID, NAME, SURNAME, DATE_OF_BIRTH, SALARY_AMOUNT, START_OF_EMPLOYMENT, END_OF_EMPLOYMENT)
VALUES 
(default, 'Aleksander', 'Wypłata', '1995-02-17', 8796.14, '2022-02-09', '2023-08-09'),
(default, 'Anna', 'Kowalska', '1994-08-17', 4563.10, '2019-10-10', NULL),
(default, 'Patryk', 'Suchy', null, 3258.00, '2022-10-09', '2018-01-09'),
(default, 'Zofia', 'Nowak', '1992-02-18', 5541.18, '2016-02-09', '2023-08-18');
```
```sql
SELECT * FROM EMPLOYEES;
```
![image](https://github.com/Martyelny/Portfolio/assets/115575209/e792bee6-7ccd-43c2-8eee-66d137850f49)

**3. Stworzenie widoku zmaterializowanego prezentujący aktualnie zatrudnionych pracowników.**
```sql
CREATE MATERIALIZED VIEW CURRENT_EMPLOYEES AS
SELECT NAME, SURNAME, SALARY_AMOUNT 
FROM EMPLOYEES
WHERE END_OF_EMPLOYMENT IS NULL;
```
```sql
SELECT * FROM CURRENT_EMPLOYEES;
```
![image](https://github.com/Martyelny/Portfolio/assets/115575209/aa2db9fc-3ece-42e3-b8b6-fa7755740891)

**4. Stworzenie widoku - raportu pracowników w kolejnych latach.**
```sql
CREATE VIEW EMPLOYEE_REPORT AS
SELECT EXTRACT(YEAR FROM START_OF_EMPLOYMENT) AS YEAR, COUNT(*) AS NUMBER_OF_EMPLOYEES
FROM EMPLOYEES
GROUP BY YEAR
ORDER BY YEAR DESC;
```
```sql
SELECT * FROM EMPLOYEE_REPORT;
```
![image](https://github.com/Martyelny/Portfolio/assets/115575209/19b7a70a-23b3-4079-90de-914c099a7758)
