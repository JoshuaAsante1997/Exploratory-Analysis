# Data Exploration 

## Table of Contents 

- [SQL scripts written to gain insights](#sql-scripts-written-to-gain-insights)
- [Recommendations](#recommendations)
  


### Project Overview

The aim of this project is to see what valuable insights can be gained from the library database that I created. I seek to identify trends that can be used
to help improve the librarys operations.


### Data sources

For the purpose of this project my main source for the data relating to this project, is from 
my library database.


## Tools 

- MySQL

## Exploratory Data Analysis (EDA)

   EDA used to answer the following key questions:

   - What is the most borrowed book?
   - What was the most popular renting month for 2023 and then for 2024?
   - What member borrowed the most books?
   - How many genres are there per author?
   - What is the most popular genre?
   - What is the number of active vs inactive library memberships?
   - How many books are there per genre?
   - What is the total number of books per author?

     ## SQL scripts written to gain insights
     
     ```sql
     -- Most borrowed book --
     
     SELECT bw.book_id,
            b.title,
            COUNT(bw.borrowing_id) AS times_borrowed
     FROM borrowings AS bw
     JOIN
     books AS b ON bw.book_id = b.book_id
     GROUP BY b.book_id
     ORDER BY times_borrowed DESC;
     ```
     ![Screenshot 2024-05-04 at 02 58 47](https://github.com/JoshuaAsante1997/Library-Database/assets/149339304/21596f9a-5bf4-49dd-8e0e-a500b4eb7a0f)

```sql
-- Most popular renting months in 2023 --

SELECT YEAR(borrowing_date) AS year_booked,
       MONTH(borrowing_date) AS month_booked,
       COUNT(borrowing_date) AS total_borrows
FROM borrowings
WHERE YEAR(borrowing_date) = 2023
GROUP BY year_booked, month_booked
ORDER BY year_booked, month_booked;
```
![Screenshot 2024-05-04 at 03 09 02](https://github.com/JoshuaAsante1997/Library-Database/assets/149339304/97308f46-2033-4f4b-b81e-b9435889903d)

```sql
-- Most popular renting months in 2024 --

SELECT YEAR(borrowing_date) AS year_booked,
       MONTH(borrowing_date) AS month_booked,
       COUNT(borrowing_date) AS total_borrows
FROM borrowings
WHERE YEAR(borrowing_date) = 2024
GROUP BY year_booked, month_booked
ORDER BY year_booked, month_booked;
```
![Screenshot 2024-05-04 at 03 11 59](https://github.com/JoshuaAsante1997/Library-Database/assets/149339304/984f4dc1-acd9-429b-9cad-6d3814770e4d)

```sql
-- Members who borrow the most books--

SELECT member_id,
       COUNT(borrowing_id) AS number_of_borrows
FROM borrowings
GROUP BY member_id
ORDER BY number_of_borrows DESC;
```
![Screenshot 2024-05-04 at 03 15 31](https://github.com/JoshuaAsante1997/Library-Database/assets/149339304/f4bf3317-fc07-493d-bea3-7337d9d0c94e)

```sql
-- genres per author--

SELECT a.author_name,
       COUNT(DISTINCT g.genre_id) AS total_genres
FROM authors AS a
JOIN
books AS b ON b.genre_id = g.genre_id
GROUP BY a.author_name;
```
![Screenshot 2024-05-04 at 03 19 15](https://github.com/JoshuaAsante1997/Library-Database/assets/149339304/74b3b531-b32b-419f-bec1-a3cc2892952b)


```sql
-- Most popular genre--

SELECT g.genre_name,
       COUNT(bw.book_id) AS total_borrowed
FROM borrowings AS bw
JOIN
books AS b ON b.book_id = bw.book_id
JOIN
genres AS g ON b.genre_id = g.genre_id
GROUP BY g.genre_name
ORDER BY total_borrowed DESC;
```
![Screenshot 2024-05-04 at 03 22 45](https://github.com/JoshuaAsante1997/Library-Database/assets/149339304/5e8ff8db-724e-44ac-b475-0ac5c4a900d3)

```sql
-- Number of active vs inactive memberships--

SELECT membership_status
COUNT(member_id) AS total_members
FROM members
GROUP BY membership_status;
```
![Screenshot 2024-05-04 at 03 25 04](https://github.com/JoshuaAsante1997/Library-Database/assets/149339304/02153fec-60fe-4e3d-b4db-0c7652cc882a)

```sql
-- How many books per genre--

SELECT g.genre_name,
       COUNT(b.book_id) AS number_of_books
FROM books AS b
JOIN
genres AS g ON b.genre_id = g.genre_id
GROUP BY g.genre_name;
```
![Screenshot 2024-05-04 at 03 27 30](https://github.com/JoshuaAsante1997/Library-Database/assets/149339304/1301c1ac-94f3-4785-94ed-51d559b85cc5)

```sql
-- Total books per author--

SELECT a.author_name,
       COUNT(b.book_id) AS books_available,
       g.genre_name
FROM authors AS a
JOIN
books AS b ON a.author_id = b.author_id
JOIN
genres AS g ON b.genre_id = g.genre_id
GROUP BY a.author_name,g.genre_name
ORDER BY author_name;
```
![Screenshot 2024-05-04 at 03 34 23](https://github.com/JoshuaAsante1997/Library-Database/assets/149339304/3f65c389-c47d-47a2-b244-bf870e1c704e)

### Recommendations

The results and recommendations are summarised as follows: [Download here](https://github.com/JoshuaAsante1997/Library-Database/files/15209902/Data.exploration.findings.pdf)


