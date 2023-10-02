# SQL

Table Schema 

<img width="289" alt="Screenshot 2023-10-02 at 14 38 34" src="https://github.com/xyanaxa/RESTfulBooker/assets/101880097/9f3fd2ba-97b4-4f69-a177-6ea1841606f2">


1. Show first name, last name, and gender of patients whose gender is 'M'
```
SELECT first_name,last_name,gender FROM patients
WHERE gender='M';
```
<img width="833" alt="Screenshot 2023-10-02 at 14 19 37" src="https://github.com/xyanaxa/RESTfulBooker/assets/101880097/20768ac6-f2da-4f61-b91e-e7df2a040919">

2. Show unique birth years from patients and order them by ascending.
```
SELECT DISTINCT YEAR(birth_date) AS birth_year
FROM patients
ORDER BY birth_year ASC;
```
<img width="837" alt="Screenshot 2023-10-02 at 14 30 27" src="https://github.com/xyanaxa/RESTfulBooker/assets/101880097/7c023a67-bedc-4daa-8020-664e0b3771ae">

3. Show patient_id and first_name from patients where their first_name start and ends with 's' and is at least 6 characters long.
```
SELECT patient_id, first_name FROM patients
WHERE first_name LIKE 's____%s';
```
<img width="842" alt="Screenshot 2023-10-02 at 14 33 46" src="https://github.com/xyanaxa/RESTfulBooker/assets/101880097/d5072fcb-d1cd-42d6-a105-adbfd643c44b">

4. Show the total amount of male patients and the total amount of female patients in the patients table.
Display the two results in the same row.

```
SELECT 
  (SELECT count(*) FROM patients WHERE gender='M') AS male_count, 
  (SELECT count(*) FROM patients WHERE gender='F') AS female_count;
```
<img width="838" alt="Screenshot 2023-10-02 at 14 42 00" src="https://github.com/xyanaxa/RESTfulBooker/assets/101880097/1ecc45f5-e996-48ca-ae6d-3070a0a1a8b0">

5. Show first and last name, allergies from patients which have allergies to either 'Penicillin' or 'Morphine'. Show results ordered ascending by allergies then by first_name then by last_name.

```
SELECT first_name, last_name, allergies FROM patients
WHERE allergies IN ('Penicillin', 'Morphine')
ORDER BY allergies, first_name, last_name;
```
<img width="842" alt="Screenshot 2023-10-02 at 15 03 09" src="https://github.com/xyanaxa/RESTfulBooker/assets/101880097/72c587ca-a7b2-4cae-b73f-6abf9a054412">

