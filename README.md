# Crack SQL Interview in 50 QS
  * Solve LeetCode Challenges in structured query language usign MySql [Problems Link](https://leetcode.com/studyplan/top-sql-50/) 
  * EASY :   32 Prpblem
  * MEDIUM : 17 Problem
  * HRAD :   1P Problem
  
## 1.Select [5P]
 * [1757 Recyclable and Low Fat Products](https://leetcode.com/problems/recyclable-and-low-fat-products/description/?envType=study-plan-v2&envId=top-sql-50) * Easy
   ``` sql
     select product_id
     from Products
     where low_fats = 'Y' and recyclable = 'Y'
   ```
 * [584 Find Customer Referee](https://leetcode.com/problems/find-customer-referee/description/?envType=study-plan-v2&envId=top-sql-50) * Easy
   ``` sql
   select name
   from Customer
   where referee_id != 2 or referee_id is null
   ```
* [595. Big Countries](https://leetcode.com/problems/big-countries/description/?envType=study-plan-v2&envId=top-sql-50) * Easy
  ``` sql
  select name, population, area
  from World
  where area >= 3000000 or population >= 25000000
  ```
* [1148. Article Views I](https://leetcode.com/problems/article-views-i/description/?envType=study-plan-v2&envId=top-sql-50) * Easy
  ``` sql
  select Distinct(author_id) as id
  from Views
  where author_id = viewer_id
  order by author_id asc
  ```
* [1683. Invalid Tweets](https://leetcode.com/problems/invalid-tweets/description/?envType=study-plan-v2&envId=top-sql-50) * Easy
  ``` sql
  select tweet_id 
  from Tweets
  where length(content) > 15
  ```
  
## 2.Basic Joins [9P]
  * [1378. Replace Employee ID With The Unique Identifier](https://leetcode.com/problems/replace-employee-id-with-the-unique-identifier/description/?envType=study-plan-v2&envId=top-sql-50) * Easy
    ``` sql
    select unique_id, name
    from Employees
    left join EmployeeUNI
    on Employees.id = EmployeeUNI.id
    ```
  * [1068. Product Sales Analysis I](https://leetcode.com/problems/product-sales-analysis-i/description/?envType=study-plan-v2&envId=top-sql-50) * Easy
    ``` sql
    select product_name, year, price
    from Sales
    inner join Product
    on Product.product_id = Sales.product_id
    ```
  * [1581. Customer Who Visited but Did Not Make Any Transactions](https://leetcode.com/problems/customer-who-visited-but-did-not-make-any-transactions/description/?envType=study-plan-v2&envId=top-sql-50) * Easy
    ``` sql
    SELECT customer_id, COUNT(*) AS count_no_trans
    FROM Visits
    WHERE visit_id NOT IN (SELECT visit_id FROM Transactions)
    GROUP BY customer_id;
    ```
  * [197. Rising Temperature](https://leetcode.com/problems/rising-temperature/description/?envType=study-plan-v2&envId=top-sql-50) * Easy
    ``` sql
    select w2.id
    from weather w1
    inner join weather w2
    on w2.temperature > w1.temperature and datediff(w2.recordDate, w1.recordDate) = 1
    ```
  * [1661. Average Time of Process per Machine](https://leetcode.com/problems/average-time-of-process-per-machine/description/?envType=study-plan-v2&envId=top-sql-50) * Easy
    ``` sql
    select a1.machine_id, round(avg(a2.timestamp * a1.timestamp),3) as processing_time
    from activity as a1, activity as a2
    where a1.machine_id = a2.machine_id and a1.process_id = a2.process_id and a1.activity_type = "start" and a2.activity_type = "end"
    group by a1.machine_id
    ```
  * [577. Employee Bonus](https://leetcode.com/problems/employee-bonus/description/?envType=study-plan-v2&envId=top-sql-50) * Easy
    ``` sql
    select e.name, b.bonus
    from Employee as e 
    left join bonus as b
    on e.empId = b.empId 
    where b.bonus < 1000 or b.bonus is null
    ```
  * [1280. Students and Examinations](https://leetcode.com/problems/students-and-examinations/description/?envType=study-plan-v2&envId=top-sql-50) * Easy
    ``` sql
   
    ```
  * [570. Managers with at Least 5 Direct Reports](https://leetcode.com/problems/managers-with-at-least-5-direct-reports/description/?envType=study-plan-v2&envId=top-sql-50) * Medium
    ``` sql
     select name
    from employee
    where id in (
                  select managerId
                  from employee
                  group by managerId
                  having count(id) >= 5
              )
    ```
  * [1934. Confirmation Rate](https://leetcode.com/problems/confirmation-rate/description/?envType=study-plan-v2&envId=top-sql-50) * Medium
    ``` sql
    select s.user_id, round(
          ifnull (count( case when action = 'confirmed' then 1 end) / count(action), 0), 2) as confirmation_rate
    from signups as s
    left join confirmations c
    on s.user_id = c.user_id
    group by user_id
    ```
    
## 3.Basic Aggregate Functions [8P]
  * [620. Not Boring Movies](https://leetcode.com/problems/not-boring-movies/description/?envType=study-plan-v2&envId=top-sql-50) - Easy
    ``` sql
    select id, movie, description, rating
    from Cinema
    where description <> "boring" and mod(id,2) = 1 
    order by rating desc
    ```
  * [1251. Average Selling Price](https://leetcode.com/problems/average-selling-price/description/?envType=study-plan-v2&envId=top-sql-50) - Easy
    ``` sql
    select p.product_id, ifnull(round(sum(u.units*p.price)/sum(u.units),2),0) as average_price
    from Prices as p
    left join UnitsSold as u
    on p.product_id = u.product_id and u.purchase_date >= p.start_date and u.purchase_date <= p.end_date
    group by p.product_id
    ```
  * [1075. Project Employees I](https://leetcode.com/problems/project-employees-i/description/?envType=study-plan-v2&envId=top-sql-50) - Easy
    ``` sql
    select p.project_id, round(avg(e.experience_years),2) as average_years
    from Project as p
    left join Employee as e
    on p.employee_id = e.employee_id
    group by p.project_id
    ```
  * [1633. Percentage of Users Attended a Contest](https://leetcode.com/problems/percentage-of-users-attended-a-contest/description/?envType=study-plan-v2&envId=top-sql-50) - Easy
    ``` sql
    select r.contest_id ,round((count(u.user_id) / (select count(user_id) from Users))*100.00,2) as percentage
    from Register as r
    left join Users as u
    on r.user_id = u.user_id
    group by r.contest_id
      order by percentage desc, r.contest_id asc
    ```
  * [1211. Queries Quality and Percentage](https://leetcode.com/problems/queries-quality-and-percentage/description/?envType=study-plan-v2&envId=top-sql-50) - Easy
    ``` sql
    select query_name, round( sum(rating/position)/count(query_name), 2) as quality,
         round(count(CASE WHEN rating < 3 THEN 1 END) / count(rating) * 100, 2)  as poor_query_percentage
    from queries
    where query_name is not null
    group by query_name
    ```
  * [1193. Monthly Transactions I](https://leetcode.com/problems/monthly-transactions-i/description/?envType=study-plan-v2&envId=top-sql-50) - Medium
    ``` sql
    select CONCAT(YEAR(trans_date), '-', LPAD(MONTH(trans_date), 2, '0')) AS month,
         country, 
         count(state) as trans_count,
         sum(case when state = 'approved' then 1 else 0 end) as approved_count,
         sum(amount) as trans_total_amount,
         sum(case when state = 'approved' then amount else 0 end) as approved_total_amount
    from transactions
    group by month, country
    ```
  * [1174. Immediate Food Delivery II](https://leetcode.com/problems/immediate-food-delivery-ii/description/?envType=study-plan-v2&envId=top-sql-50) - Medium
    ``` sql
    select ROUND(
           SUM(
              CASE WHEN order_date = customer_pref_delivery_date THEN 1 ELSE 0 END
              ) 
              / COUNT(*) * 100 , 2
             ) as immediate_percentage
    from delivery
    where (customer_id,order_date) in (
                    select customer_id,min(order_date) 
                    from delivery 
                    group by customer_id
                    )
    ```
  * [550. Game Play Analysis IV](https://leetcode.com/problems/game-play-analysis-iv/description/?envType=study-plan-v2&envId=top-sql-50) - Medium
    ``` sql
    select round( count(a.player_id) / (select count(distinct player_id) from activity), 2) as fraction
    from (select player_id, min(event_date) as event_date from activity group by player_id) as b
    left join activity as a
    on b.player_id = a.player_id 
    where DATE_ADD(b.event_date, INTERVAL 1 DAY) = A.event_date; 
    ```
    
## 4.Sorting and Grouping [7P]
  * [2356. Number of Unique Subjects Taught by Each Teacher](https://leetcode.com/problems/number-of-unique-subjects-taught-by-each-teacher/description/?envType=study-plan-v2&envId=top-sql-50) - Easy
    ``` sql
    select teacher_id, count(distinct subject_id) as cnt
    from teacher
    group by teacher_id
    ```
  * [1141. User Activity for the Past 30 Days I](https://leetcode.com/problems/user-activity-for-the-past-30-days-i/description/?envType=study-plan-v2&envId=top-sql-50) - Easy
    ``` sql
    select activity_date as day, count(distinct user_id) as active_users
    from activity
    where activity_date between '2019-06-28' and '2019-07-27'
    group by activity_date
    ```
  * [1070. Product Sales Analysis III](https://leetcode.com/problems/product-sales-analysis-iii/description/?envType=study-plan-v2&envId=top-sql-50) - Medium
    ``` sql
    select product_id, year as first_year, quantity, price
    from sales as s
    where (product_id, year) in (
      select product_id, min(year)
      from sales
      group by product_id
    )
    ```
  * [596. Classes More Than 5 Students](https://leetcode.com/problems/classes-more-than-5-students/description/?envType=study-plan-v2&envId=top-sql-50) - Easy
    ``` sql
    select class
    from courses
    group by class
    having count(distinct student) >= 5
    ```
  * [1729. Find Followers Count](https://leetcode.com/problems/find-followers-count/description/?envType=study-plan-v2&envId=top-sql-50) - Easy
    ``` sql
    select user_id , count(follower_id) as followers_count
    from followers
    group by user_id
    order by user_id asc
    ```
  * [619. Biggest Single Number](https://leetcode.com/problems/biggest-single-number/description/?envType=study-plan-v2&envId=top-sql-50) - Easy
    ``` sql
    SELECT CASE 
      WHEN COUNT(*) > 0 THEN MAX(num)
      ELSE NULL
      END 
      AS num
    FROM (
      SELECT num
      FROM MyNumbers
      GROUP BY num
      HAVING COUNT(num) = 1
    ) as myNewNumbers;
    ```
  * [1045. Customers Who Bought All Products](https://leetcode.com/problems/customers-who-bought-all-products/description/?envType=study-plan-v2&envId=top-sql-50) - Medium
    ``` sql
    select customer_id
    from customer
    group by customer_id
    having count(distinct product_key) = (select count(product_key) from product)
    ```
    
 ## 5.Advanced Select and Joins [7P]
 * [1731. The Number of Employees Which Report to Each Employee](https://leetcode.com/problems/the-number-of-employees-which-report-to-each-employee/description/?envType=study-plan-v2&envId=top-sql-50) - Easy
   ``` sql
   select e1.employee_id, e1.name,
       count(e2.reports_to) as reports_count, round(avg(e2.age)) as average_age
   from employees as e1
   join employees as e2
   on e1.employee_id = e2.reports_to
   group by e1.employee_id
   order by employee_id
   ```
* [1789. Primary Department for Each Employee](https://leetcode.com/problems/primary-department-for-each-employee/description/?envType=study-plan-v2&envId=top-sql-50) - Easy
   ``` sql
  SELECT employee_id, department_id
  FROM Employee
  WHERE primary_flag = 'Y'
  UNION
  SELECT employee_id, department_id
  FROM Employee
  GROUP BY employee_id
  HAVING count(employee_id) = 1;
  ```
* [610. Triangle Judgement](https://leetcode.com/problems/triangle-judgement/description/?envType=study-plan-v2&envId=top-sql-50) - Easy
   ``` sql
  SELECT x, y, z, 
    CASE 
        WHEN x + y > z AND x + z > y AND y + z > x THEN 'Yes'
        ELSE 'No'
    END AS triangle
  FROM Triangle;
  ```
* [180. Consecutive Numbers](https://leetcode.com/problems/consecutive-numbers/description/?envType=study-plan-v2&envId=top-sql-50) - Medium
   ``` sql
   SELECT DISTINCT L1.num AS ConsecutiveNums
  FROM Logs L1
  INNER JOIN Logs L2 
  ON L1.id - L2.id = 1 AND L1.num = L2.num
  INNER JOIN Logs L3 
  ON L1.id - L3.id = 2 AND L1.num = L3.num
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
  SELECT product_id, '10' as price
  FROM Products
  GROUP BY product_id
  HAVING MIN(change_date) > '2019-08-16' 
  ORDER BY product_id
  ```
* [1204. Last Person to Fit in the Bus](https://leetcode.com/problems/last-person-to-fit-in-the-bus/?envType=study-plan-v2&envId=top-sql-50) - Medium
   ``` sql
  
  ```
* [1907. Count Salary Categories](https://leetcode.com/problems/count-salary-categories/?envType=study-plan-v2&envId=top-sql-50) - Medium
   ``` sql
  SELECT 'Low Salary' AS category , COUNT(account_id) AS accounts_count 
  FROM Accounts 
  WHERE income < 20000
  UNION
  SELECT 'Average Salary' AS category , COUNT(account_id) AS accounts_count 
  FROM Accounts 
  WHERE income >= 20000 AND income <= 50000
  UNION
  SELECT 'High Salary' AS category , COUNT(account_id) AS accounts_count 
  FROM Accounts 
  WHERE income > 50000;
  ```       
 ## 6.Subqueries [7P]
 * [1978. Employees Whose Manager Left the Company](https://leetcode.com/problems/employees-whose-manager-left-the-company/description/?envType=study-plan-v2&envId=top-sql-50) - Easy
   ``` sql
   select employee_id
   from   employees
   where  salary < 30000 and 
       manager_id not in(
            select employee_id
            from employees
      )
   order by employee_id
   ```
 * [626. Exchange Seats](https://leetcode.com/problems/exchange-seats/description/?envType=study-plan-v2&envId=top-sql-50) - Medium
   ``` sql

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

  ```
 * [185. Department Top Three Salaries](https://leetcode.com/problems/department-top-three-salaries/description/?envType=study-plan-v2&envId=top-sql-50) - Hard
  ``` sql

  ```

 ## 7.Advanced String Functions / Regex / Clause [7P]
* [1667. Fix Names in a Table](https://leetcode.com/problems/fix-names-in-a-table/description/?envType=study-plan-v2&envId=top-sql-50) - Easy
  ``` sql
  select user_id, 
      concat(
          upper(left(name,1)) , 
          lower(right(name, length(name)-1))) as name
  from users
  order by user_id
  ```
* [1527. Patients With a Condition](https://leetcode.com/problems/patients-with-a-condition/description/?envType=study-plan-v2&envId=top-sql-50) - Easy
  ``` sql
  select *
  from patients
  where conditions LIKE '% DIAB1__ %' OR
       conditions LIKE 'DIAB1__ %' OR
       conditions LIKE '% DIAB1__' OR
       conditions LIKE 'DIAB1__' 
  ```
* [196. Delete Duplicate Emails](https://leetcode.com/problems/delete-duplicate-emails/description/?envType=study-plan-v2&envId=top-sql-50) - Easy
  ``` sql
  delete p
  from person as p , person as s
  where p.email = s.email and p.id > s.id 
  ```
* [176. Second Highest Salary](https://leetcode.com/problems/second-highest-salary/description/?envType=study-plan-v2&envId=top-sql-50) - Medium
  ``` sql 
  select (case when count(distinct salary) > 1 then (
    select salary from (
        select distinct salary from employee order by salary desc limit 2
    ) as emp order by salary asc limit 1
  ) else null end) as SecondHighestSalary
  from employee
  ```
* [1484. Group Sold Products By The Date](https://leetcode.com/problems/group-sold-products-by-the-date/description/?envType=study-plan-v2&envId=top-sql-50) - Easy
  ``` sql
  select sell_date, 
       count(distinct(product)) as num_sold,
       GROUP_CONCAT(distinct(product) SEPARATOR ',' ) as products 
  from activities
  group by sell_date
  order by sell_date
  ```
* [1327. List the Products Ordered in a Period](https://leetcode.com/problems/list-the-products-ordered-in-a-period/description/?envType=study-plan-v2&envId=top-sql-50) - Easy
  ``` sql
  select p.product_name, sum(o.unit) as unit
  from products as p
  left join orders as o
  on p.product_id = o.product_id
  where YEAR(o.order_date) = 2020
      AND MONTH(o.order_date) = 2
  group by p.product_id
  having unit >= 100  
   # another sol use --> WHERE DATE_FORMAT(O.order_date,'%Y-%m') ='2020-02'
  ```
* [1517. Find Users With Valid E-Mails](https://leetcode.com/problems/find-users-with-valid-e-mails/description/?envType=study-plan-v2&envId=top-sql-500) - Easy
  ``` sql
  select *
  from users
  where mail regexp '^[a-zA-Z][a-zA-Z0-9_.-]*@leetcode\\.com$'
  ```
