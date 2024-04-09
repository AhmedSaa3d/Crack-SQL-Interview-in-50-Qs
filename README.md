# Crack-SQL-Interview-in-50-Qs
  - Solve LeetCode Challenges in SQL
  - [Problems Link](https://leetcode.com/studyplan/top-sql-50/) 
## 1.Select [5P]
 - [1757 Recyclable and Low Fat Products](https://leetcode.com/problems/recyclable-and-low-fat-products/description/?envType=study-plan-v2&envId=top-sql-50)
   ``` sql
     select product_id
     from Products
     where low_fats = 'Y' and recyclable = 'Y'
   ```
 - [584 Find Customer Referee](https://leetcode.com/problems/find-customer-referee/description/?envType=study-plan-v2&envId=top-sql-50)
   ``` sql
   select name
   from Customer
   where referee_id != 2 or referee_id is null
   ```
- [595. Big Countries](https://leetcode.com/problems/big-countries/description/?envType=study-plan-v2&envId=top-sql-50)
  ``` sql
  select name, population, area
  from World
  where area >= 3000000 or population >= 25000000
  ```
- [1148. Article Views I](https://leetcode.com/problems/article-views-i/description/?envType=study-plan-v2&envId=top-sql-50)
  ``` sql
  select Distinct(author_id) as id
  from Views
  where author_id = viewer_id
  order by author_id asc
  ```
- [1683. Invalid Tweets](https://leetcode.com/problems/invalid-tweets/description/?envType=study-plan-v2&envId=top-sql-50)
  ``` mysql
  select tweet_id 
  from Tweets
  where length(content) > 15
  ```
- []()
  ``` sql
  ```
- []()
  ``` sql
  ```
  - []()
  ``` sql
  ```
- []()
  ``` sql
  ```

- []()
  ``` sql
  ```
- []()
  ``` sql
  ```


  
       
