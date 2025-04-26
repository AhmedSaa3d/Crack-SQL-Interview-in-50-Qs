# Crack SQL Interview in 50 QS
  * Solve LeetCode Challenges in structured query language using MS SQL SERVER  [Problems Link](https://leetcode.com/studyplan/top-sql-50/) 
  * EASY   : 32 Prpblems
  * MEDIUM : 17 Problems
  * HRAD   : 1  Problem
  
## 1.Select [5P]
 * [1757 Recyclable and Low Fat Products](https://leetcode.com/problems/recyclable-and-low-fat-products/description/?envType=study-plan-v2&envId=top-sql-50) * Easy
   ``` sql
    SELECT product_id
    FROM Products
    WHERE low_fats = 'Y' AND recyclable = 'Y'
   ```
 * [584 Find Customer Referee](https://leetcode.com/problems/find-customer-referee/description/?envType=study-plan-v2&envId=top-sql-50) * Easy
   ``` sql
   SELECT name
   FROM Customer
   WHERE referee_id IS NULL OR referee_id <> 2
   ```
* [595. Big Countries](https://leetcode.com/problems/big-countries/description/?envType=study-plan-v2&envId=top-sql-50) * Easy
  ``` sql
  SELECT name, population, area
  FROM World
  WHERE area >= 3000000 OR population >= 25000000
  ```
* [1148. Article Views I](https://leetcode.com/problems/article-views-i/description/?envType=study-plan-v2&envId=top-sql-50) * Easy
  ``` sql
  SELECT DISTINCT author_id AS id
  FROM Views
  WHERE author_id = viewer_id
  ORDER BY author_id
  ```
* [1683. Invalid Tweets](https://leetcode.com/problems/invalid-tweets/description/?envType=study-plan-v2&envId=top-sql-50) * Easy
  ``` sql
  SELECT tweet_id
  FROM Tweets
  WHERE LEN(content) > 15
  ```
## 2.Basic Joins [9P]
  * [1378. Replace Employee ID With The Unique Identifier](https://leetcode.com/problems/replace-employee-id-with-the-unique-identifier/description/?envType=study-plan-v2&envId=top-sql-50) * Easy
    ``` sql
    SELECT U.unique_id, E.name
    FROM Employees E LEFT OUTER JOIN EmployeeUNI U
    ON E.id = U.id
    ```
  * [1068. Product Sales Analysis I](https://leetcode.com/problems/product-sales-analysis-i/description/?envType=study-plan-v2&envId=top-sql-50) * Easy
    ``` sql
    SELECT P.product_name, S.year, S.price
    FROM Sales S INNER JOIN Product P
    ON S.product_id = P.product_id
    ```
  * [1581. Customer Who Visited but Did Not Make Any Transactions](https://leetcode.com/problems/customer-who-visited-but-did-not-make-any-transactions/description/?envType=study-plan-v2&envId=top-sql-50) * Easy
    ``` sql
    SELECT customer_id, COUNT(customer_id) AS 'count_no_trans'
    FROM Visits V LEFT OUTER JOIN Transactions T
    ON V.visit_id = T.visit_id
    WHERE transaction_id IS NULL
    GROUP BY customer_id
    ORDER BY 1
    ```
  * [197. Rising Temperature](https://leetcode.com/problems/rising-temperature/description/?envType=study-plan-v2&envId=top-sql-50) * Easy
    ``` sql
    SELECT y.id
    FROM Weather x INNER JOIN Weather y
    ON DATEDIFF(DAY, x.recordDate, y.recordDate) = 1 AND y.temperature > x.temperature
    ```
  * [1661. Average Time of Process per Machine](https://leetcode.com/problems/average-time-of-process-per-machine/description/?envType=study-plan-v2&envId=top-sql-50) * Easy
    ``` sql
    SELECT x.machine_id, round(AVG(y.timestamp - x.timestamp), 3) [processing_time]
    FROM Activity x INNER JOIN Activity y
    ON x.machine_id = y.machine_id AND x.process_id = y.process_id AND x.activity_type = 'start' AND y.activity_type = 'end'
    GROUP BY x.machine_id
    ```
  * [577. Employee Bonus](https://leetcode.com/problems/employee-bonus/description/?envType=study-plan-v2&envId=top-sql-50) * Easy
    ``` sql
    SELECT E.name, B.bonus
    FROM Employee AS E LEFT OUTER JOIN Bonus AS B
    ON E.empId = B.empId
    WHERE B.bonus < 1000 OR B.bonus IS NULL
    ```
  * [1280. Students and Examinations](https://leetcode.com/problems/students-and-examinations/description/?envType=study-plan-v2&envId=top-sql-50) * Easy
    ``` sql
    SELECT s.student_id, s.student_name, j.subject_name, COUNT(x.subject_name) AS attended_exams
    FROM Students s CROSS JOIN Subjects j LEFT JOIN Examinations x 
    ON s.student_id = x.student_id AND j.subject_name = x.subject_name
    GROUP BY s.student_id, s.student_name, j.subject_name
    ORDER BY s.student_id ASC, j.subject_name ASC
    ```
  * [570. Managers with at Least 5 Direct Reports](https://leetcode.com/problems/managers-with-at-least-5-direct-reports/description/?envType=study-plan-v2&envId=top-sql-50) * Medium
    ``` sql
    SELECT e1.name
    FROM Employee e1 JOIN Employee e2
    ON e1.id = e2.managerId
    GROUP BY e1.name, e1.id
    HAVING COUNT(e1.id) >= 5
    ```
  * [1934. Confirmation Rate](https://leetcode.com/problems/confirmation-rate/description/?envType=study-plan-v2&envId=top-sql-50) * Medium
    ``` sql
    SELECT s.user_id, ROUND(AVG(IIF(c.action = 'confirmed', 1.00, 0.00)), 2) AS confirmation_rate
    FROM Signups s LEFT OUTER JOIN Confirmations c
    ON s.user_id = c.user_id
    GROUP BY s.user_id
    ```
## 3.Basic Aggregate Functions [8P]
  * [620. Not Boring Movies](https://leetcode.com/problems/not-boring-movies/description/?envType=study-plan-v2&envId=top-sql-50) - Easy
    ``` sql
    SELECT *
    FROM Cinema
    WHERE id % 2 = 1 AND description != 'boring'
    ORDER BY rating DESC
    ```
  * [1251. Average Selling Price](https://leetcode.com/problems/average-selling-price/description/?envType=study-plan-v2&envId=top-sql-50) - Easy
    ``` sql
    SELECT p.product_id, ISNULL(ROUND(SUM(CONVERT(DECIMAL ,p.price) * u.units) / SUM(u.units), 2), 0) AS average_price
    FROM Prices p LEFT OUTER JOIN UnitsSold u
    ON p.product_id = u.product_id AND u.purchase_date >= p.start_date AND u.purchase_date <= p.end_date
    GROUP BY p.product_id
    ```
  * [1075. Project Employees I](https://leetcode.com/problems/project-employees-i/description/?envType=study-plan-v2&envId=top-sql-50) - Easy
    ``` sql
    SELECT p.project_id, ROUND(AVG(CAST(e.experience_years AS DECIMAL)),2) AS average_years
    FROM Employee e INNER JOIN Project p
    ON e.employee_id = p.employee_id
    GROUP BY p.project_id
    ```
  * [1633. Percentage of Users Attended a Contest](https://leetcode.com/problems/percentage-of-users-attended-a-contest/description/?envType=study-plan-v2&envId=top-sql-50) - Easy
    ``` sql
    SELECT contest_id, ROUND(COUNT(user_id) * 1.00 / (SELECT COUNT(*) FROM Users) * 100.00 , 2) AS percentage 
    FROM Register
    GROUP BY contest_id
    ORDER BY percentage DESC, contest_id ASC
    ```
  * [1211. Queries Quality and Percentage](https://leetcode.com/problems/queries-quality-and-percentage/description/?envType=study-plan-v2&envId=top-sql-50) - Easy
    ``` sql
    SELECT query_name, ROUND(AVG(rating*1.00 / position), 2) AS quality, ROUND(SUM(IIF(rating < 3 , 1 , 0)) * 100.00 / COUNT(*), 2) AS poor_query_percentage
    FROM Queries
    GROUP BY query_name
    ```
  * [1193. Monthly Transactions I](https://leetcode.com/problems/monthly-transactions-i/description/?envType=study-plan-v2&envId=top-sql-50) - Medium
    ``` sql
    SELECT FORMAT(trans_date,'yyy-MM') AS month, country,
           COUNT(*) AS trans_count,
           SUM(IIF(state = 'approved',1,0)) AS approved_count,
           SUM(amount) AS trans_total_amount,
           SUM(IIF(state = 'approved', amount, 0)) AS approved_total_amount
    FROM Transactions
    GROUP BY FORMAT(trans_date,'yyy-MM'), country
    ```
  * [1174. Immediate Food Delivery II](https://leetcode.com/problems/immediate-food-delivery-ii/description/?envType=study-plan-v2&envId=top-sql-50) - Medium
    ``` sql
    SELECT ROUND(SUM(IIF(order_date = customer_pref_delivery_date , 1 , 0)) * 100.00 / COUNT(*), 2) AS immediate_percentage
    FROM Delivery d
    INNER JOIN(
         SELECT customer_id, MIN(order_date) AS first_order FROM Delivery GROUP BY customer_id
    ) cmd
    ON d.customer_id = cmd.customer_id AND d.order_date = cmd.first_order
    ```
  * [550. Game Play Analysis IV](https://leetcode.com/problems/game-play-analysis-iv/description/?envType=study-plan-v2&envId=top-sql-50) - Medium
    ``` sql
    SELECT ROUND(COUNT(*) * 1.00 / (SELECT COUNT(DISTINCT player_id) from Activity), 2) AS fraction
    FROM (SELECT player_id, MIN(event_date) AS event_date FROM activity GROUP BY player_id) AS First_Player_Login
    LEFT JOIN Activity a
    ON First_Player_Login.player_id = a.player_id 
    WHERE DATEADD(DAY, 1, First_Player_Login.event_date) = a.event_date
    ```
## 4.Sorting and Grouping [7P]
  * [2356. Number of Unique Subjects Taught by Each Teacher](https://leetcode.com/problems/number-of-unique-subjects-taught-by-each-teacher/description/?envType=study-plan-v2&envId=top-sql-50) - Easy
    ``` sql
    SELECT teacher_id, COUNT(DISTINCT subject_id) AS cnt
    FROM Teacher
    GROUP BY teacher_id
    ```
  * [1141. User Activity for the Past 30 Days I](https://leetcode.com/problems/user-activity-for-the-past-30-days-i/description/?envType=study-plan-v2&envId=top-sql-50) - Easy
    ``` sql
    SELECT activity_date AS day, COUNT(DISTINCT user_id) AS active_users
    FROM Activity
    WHERE activity_date <= '2019-07-27' AND activity_date >= '2019-06-28'
    GROUP BY activity_date
    ```
  * [1070. Product Sales Analysis III](https://leetcode.com/problems/product-sales-analysis-iii/description/?envType=study-plan-v2&envId=top-sql-50) - Medium
    ``` sql
    SELECT s1.product_id, s1.year AS first_year, s1.quantity, s1.price
    FROM Sales s1 LEFT JOIN 
        (SELECT product_id, MIN(year) AS year FROM Sales GROUP BY product_id) AS s2
    ON  s1.product_id = s2.product_id AND s1.year = s2.year
    WHERE s2.product_id IS NOT NULL
    ```
  * [596. Classes More Than 5 Students](https://leetcode.com/problems/classes-more-than-5-students/description/?envType=study-plan-v2&envId=top-sql-50) - Easy
    ``` sql
    SELECT class
    FROM Courses
    GROUP BY class
    HAVING COUNT(student) >= 5
    ```
  * [1729. Find Followers Count](https://leetcode.com/problems/find-followers-count/description/?envType=study-plan-v2&envId=top-sql-50) - Easy
    ``` sql
    SELECT user_id, COUNT(follower_id) AS followers_count
    FROM Followers
    GROUP BY user_id
    ORDER BY user_id
    ```
  * [619. Biggest Single Number](https://leetcode.com/problems/biggest-single-number/description/?envType=study-plan-v2&envId=top-sql-50) - Easy
    ``` sql
    SELECT MAX(num) AS num
    FROM (SELECT num FROM MyNumbers GROUP BY num HAVING COUNT(num) = 1) AS single_nums
    ```
  * [1045. Customers Who Bought All Products](https://leetcode.com/problems/customers-who-bought-all-products/description/?envType=study-plan-v2&envId=top-sql-50) - Medium
    ``` sql
    SELECT customer_id
    FROM Customer
    GROUP BY customer_id
    HAVING COUNT(DISTINCT product_key) = (SELECT COUNT(*) FROM Product)
    ```
 ## 5.Advanced Select and Joins [7P]
 * [1731. The Number of Employees Which Report to Each Employee](https://leetcode.com/problems/the-number-of-employees-which-report-to-each-employee/description/?envType=study-plan-v2&envId=top-sql-50) - Easy
   ``` sql
   SELECT a.employee_id, a.name, COUNT(b.reports_to) AS reports_count, ROUND(AVG(b.age*1.00), 0) AS average_age
   FROM Employees a INNER JOIN Employees b
   ON a.employee_id = b.reports_to
   GROUP BY a.employee_id, a.name
   ORDER BY a.employee_id
   ```
* [1789. Primary Department for Each Employee](https://leetcode.com/problems/primary-department-for-each-employee/description/?envType=study-plan-v2&envId=top-sql-50) - Easy
   ``` sql
  SELECT e1.employee_id, e1.department_id
  FROM Employee e1 LEFT JOIN Employee e2 
  ON e1.employee_id = e2.employee_id AND e2.primary_flag = 'Y'
  WHERE e1.primary_flag = 'Y' OR e2.employee_id IS NULL
  ```
* [610. Triangle Judgement](https://leetcode.com/problems/triangle-judgement/description/?envType=study-plan-v2&envId=top-sql-50) - Easy
   ``` sql
  SELECT x, y, z, 
    CASE 
        WHEN x + y > z AND x + z > y AND y + z > x THEN 'Yes'
        ELSE 'No'
    END AS triangle
  FROM Triangle
  ```
* [180. Consecutive Numbers](https://leetcode.com/problems/consecutive-numbers/description/?envType=study-plan-v2&envId=top-sql-50) - Medium
   ``` sql
   SELECT DISTINCT l1.num AS ConsecutiveNums
   FROM Logs l1 JOIN Logs l2
   ON l1.id+1 = l2.id AND l1.num = l2.num
   JOIN Logs l3
   ON l2.id+1 = l3.id AND l2.num = l3.num
  ```  
* [1164. Product Price at a Given Date](https://leetcode.com/problems/product-price-at-a-given-date/?envType=study-plan-v2&envId=top-sql-50) - Medium
   ``` sql
  SELECT product_id, new_price as price
  FROM Products
  WHERE (product_id, change_date) IN
  (
    SELECT product_id, MAX(change_date) 
    FROM products
    WHERE change_date <= '2019-08-16'
    GROUP BY product_id
  )  
  UNION
  SELECT product_id, 10 as price
  FROM Products
  GROUP BY product_id
  HAVING MIN(change_date) > '2019-08-16' 
  ORDER BY product_id
  ```
* [1204. Last Person to Fit in the Bus](https://leetcode.com/problems/last-person-to-fit-in-the-bus/?envType=study-plan-v2&envId=top-sql-50) - Medium
   ``` sql
  SELECT person_name
  FROM(
      SELECT person_name, weight, @sum := @sum + weight AS cumulativeSum
      FROM
        (SELECT * FROM Queue ORDER BY turn ASC) AS turnTable,
        (SELECT @sum := 0) AS init
  ) AS cumulativeTable
  WHERE cumulativeSum <= 1000
  ORDER BY cumulativeSum DESC
  LIMIT 1;
  ```
* [1907. Count Salary Categories](https://leetcode.com/problems/count-salary-categories/?envType=study-plan-v2&envId=top-sql-50) - Medium
   ``` sql
  SELECT 'Low Salary' AS category, SUM(CASE WHEN income < 20000 THEN 1 ELSE 0 END) AS accounts_count
  FROM Accounts
  UNION ALL
  SELECT 'Average Salary' AS category, SUM(CASE WHEN income BETWEEN 20000 AND 50000 THEN 1 ELSE 0 END) AS accounts_count
  FROM Accounts
  UNION ALL
  SELECT 'High Salary' AS category, SUM(CASE WHEN income > 50000 THEN 1 ELSE 0 END) AS accounts_count
  FROM Accounts;
  ```       
 ## 6.Subqueries [7P]
 * [1978. Employees Whose Manager Left the Company](https://leetcode.com/problems/employees-whose-manager-left-the-company/description/?envType=study-plan-v2&envId=top-sql-50) - Easy
   ``` sql
   SELECT employee_id
   FROM employees
   WHERE  salary < 30000 and 
       manager_id NOT IN(
            SELECT employee_id
            FROM employees
      )
   ORDER BY employee_id
   ```
 * [626. Exchange Seats](https://leetcode.com/problems/exchange-seats/description/?envType=study-plan-v2&envId=top-sql-50) - Medium
   ``` sql
   SELECT s1.id, s2.student
   FROM Seat s1
   LEFT JOIN Seat s2
   ON s2.id = 
   CASE 
     WHEN s1.id % 2 = 0 THEN s1.id - 1 
     WHEN s1.id % 2 = 1 AND (SELECT COUNT(*) FROM Seat) = s1.id THEN s1.id
     WHEN s1.id % 2 = 1 THEN s1.id + 1
   END;
   ```
 * [1341. Movie Rating](https://leetcode.com/problems/movie-rating/description/?envType=study-plan-v2&envId=top-sql-50) - Medium
   ``` sql
   select name as results
   from (
    select u.name, count(u.name) as cnt 
    from movieRating as m
    join users as u
    on u.user_id = m.user_id
    group by u.name
    order by cnt desc, u.name asc
    limit 1
   ) as innerTble1
   UNION ALL
   select title as results
   from (
    select s.title, avg(m.rating) as rat 
    from movieRating as m
    join movies as s
    on s.movie_id = m.movie_id
    where MONTH(m.created_at) = 2 AND YEAR(m.created_at) = 2020
    group by s.title
    order by rat desc, s.title asc
    limit 1
   ) as innerTble2
   ```
 * [1321. Restaurant Growth](https://leetcode.com/problems/restaurant-growth/?envType=study-plan-v2&envId=top-sql-50) - Medium
  ``` sql

  ```
 * [602. Friend Requests II: Who Has the Most Friends](https://leetcode.com/problems/friend-requests-ii-who-has-the-most-friends/?envType=study-plan-v2&envId=top-sql-50) - Medium
  ``` sql

  ```
 * [585. Investments in 2016](https://leetcode.com/problems/investments-in-2016/?envType=study-plan-v2&envId=top-sql-50) - Medium
  ``` sql
  SELECT ROUND(SUM(tiv_2016), 2) AS tiv_2016
  FROM Insurance
  WHERE tiv_2015 IN(
     SELECT tiv_2015
     FROM Insurance
     GROUP BY tiv_2015
     HAVING COUNT(*) > 1 -- Duplicate ROWS
  )AND (lat, lon) IN(
     SELECT lat, lon
     FROM Insurance
     GROUP BY lat, lon
     HAVING COUNT(*) = 1 -- UNIQUE ROWS
  );
  ```
 * [185. Department Top Three Salaries](https://leetcode.com/problems/department-top-three-salaries/description/?envType=study-plan-v2&envId=top-sql-50) - Hard
  ``` sql

  ```

 ## 7.Advanced String Functions / Regex / Clause [7P]
* [1667. Fix Names in a Table](https://leetcode.com/problems/fix-names-in-a-table/description/?envType=study-plan-v2&envId=top-sql-50) - Easy
  ``` sql
  SELECT user_id, CONCAT(
        UPPER(SubSTRING(name, 1, 1)),
        LOWER(SUBSTRING(name, 2, LEN(name)))
        ) as name
  FROM Users
  ORDER BY user_id
  ```
* [1527. Patients With a Condition](https://leetcode.com/problems/patients-with-a-condition/description/?envType=study-plan-v2&envId=top-sql-50) - Easy
  ``` sql
  SELECT patient_id , patient_name, conditions
  FROM Patients
  WHERE conditions LIKE '% DIAB1__ %' OR
        conditions LIKE 'DIAB1__ %' OR
        conditions LIKE '% DIAB1__' OR
        conditions LIKE 'DIAB1__'  
  ```
* [196. Delete Duplicate Emails](https://leetcode.com/problems/delete-duplicate-emails/description/?envType=study-plan-v2&envId=top-sql-50) - Easy
  ``` sql
  DELETE p1
  FROM Person p1, Person p2
  WHERE p1.email = p2.email AND p1.id > p2.id
  ```
* [176. Second Highest Salary](https://leetcode.com/problems/second-highest-salary/description/?envType=study-plan-v2&envId=top-sql-50) - Medium
  ``` sql 
  SELECT ISNULL((
                SELECT DISTINCT salary
                FROM Employee
                ORDER BY salary DESC 
                OFFSET 1 ROWS FETCH NEXT 1 ROWS ONLY
  ), NULL) AS SecondHighestSalary
  ```
* [1484. Group Sold Products By The Date](https://leetcode.com/problems/group-sold-products-by-the-date/description/?envType=study-plan-v2&envId=top-sql-50) - Easy
  ``` sql
  SELECT sell_date, 
       COUNT(product) AS num_sold, 
       STRING_AGG(product, ',') WITHIN GROUP (ORDER BY product) AS products
  FROM ( SELECT sell_date, product FROM Activities GROUP BY sell_date, product ) AS DistinctProducts
  GROUP BY sell_date
  ORDER BY sell_date
  ```
* [1327. List the Products Ordered in a Period](https://leetcode.com/problems/list-the-products-ordered-in-a-period/description/?envType=study-plan-v2&envId=top-sql-50) - Easy
  ``` sql
  SELECT p.product_name, SUM(o.unit) AS unit
  FROM Products p INNER JOIN Orders o
  ON p.product_id = o.product_id
  WHERE YEAR(o.order_date) = '2020' AND MONTH(o.order_date) = '02'
  GROUP BY p.product_name
  HAVING SUM(o.unit) >= 100
  ```
* [1517. Find Users With Valid E-Mails](https://leetcode.com/problems/find-users-with-valid-e-mails/description/?envType=study-plan-v2&envId=top-sql-500) - Easy
  ``` sql
  SELECT user_id, name, mail
  FROM Users
  WHERE RIGHT(mail, 13) = '@leetcode.com'
        AND LEFT(mail, LEN(mail) - 13) LIKE '[A-Za-z]%'
        AND LEFT(mail, LEN(mail) - 13) NOT LIKE '%[^A-Za-z0-9_.-]%'
  ```
