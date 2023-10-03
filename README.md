# SQL

Table Schemas

<img width="289" alt="Screenshot 2023-10-02 at 14 38 34" src="https://github.com/xyanaxa/RESTfulBooker/assets/101880097/9f3fd2ba-97b4-4f69-a177-6ea1841606f2">

<img width="292" alt="Screenshot 2023-10-03 at 17 00 56" src="https://github.com/xyanaxa/SQL/assets/101880097/9f8e336d-d762-4373-909f-ac8909ed99f2">



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

6. Show the city and the total number of patients in the city.
Order from most to least patients and then by city name ascending.

```
SELECT city,
COUNT(*) AS num_patients FROM patients
GROUP BY city
ORDER BY num_patients DESC, city asc;
```
<img width="842" alt="Screenshot 2023-10-03 at 11 45 35" src="https://github.com/xyanaxa/SQL/assets/101880097/4e4a8620-019b-4a6d-9d32-a7dc4a9928fa">

7. Show patient_id, first_name, last_name from patients whos diagnosis is 'Dementia'.

Primary diagnosis is stored in the admissions table.

```
SELECT patients.patient_id, first_name, last_name
FROM patients
JOIN admissions ON admissions.patient_id = patients.patient_id
WHERE diagnosis = 'Dementia';
```
<img width="835" alt="Screenshot 2023-10-03 at 17 02 07" src="https://github.com/xyanaxa/SQL/assets/101880097/279dd05b-9558-4315-aeca-51a62909de6c">

8. We are looking for a specific patient. Pull all columns for the patient who matches the following criteria:
- First_name contains an 'r' after the first two letters.
- Identifies their gender as 'F'
- Born in February, May, or December
- Their weight would be between 60kg and 80kg
- Their patient_id is an odd number
- They are from the city 'Kingston'

```
SELECT * FROM patients
WHERE first_name LIKE '__r%'
  AND gender = 'F'
  AND MONTH(birth_date) IN (2, 5, 12)
  AND weight BETWEEN 60 AND 80
  AND patient_id % 2 = 1
  AND city = 'Kingston';
```
<img width="839" alt="Screenshot 2023-10-03 at 17 07 33" src="https://github.com/xyanaxa/SQL/assets/101880097/fc6d23f5-f740-4461-b7fa-4827679708f8">

9. For each day display the total amount of admissions on that day. Display the amount changed from the previous date.

```
SELECT admission_date,
count(admission_date) as admission_day,
count(admission_date) - LAG(count(admission_date)) OVER(ORDER BY admission_date) AS admission_count_change 
FROM admissions
group by admission_date
```
<img width="832" alt="Screenshot 2023-10-03 at 17 09 00" src="https://github.com/xyanaxa/SQL/assets/101880097/2d962b5a-8ec6-48d9-8745-e514bf5662fc">

10. Show patient_id, first_name, last_name from patients whose does not have any records in the admissions table. (Their patient_id does not exist in any admissions.patient_id rows.)

```
SELECT patients.patient_id,first_name,last_name from patients
where patients.patient_id
not in (select admissions.patient_id from admissions)
```
<img width="841" alt="Screenshot 2023-10-03 at 17 44 59" src="https://github.com/xyanaxa/SQL/assets/101880097/41f5fb37-6dc3-44e9-a4ca-4eb30dc000b5">




