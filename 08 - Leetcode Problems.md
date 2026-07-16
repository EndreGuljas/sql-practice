# LeetCode SQL 50

---

## Problem Index

### 001–010

- [001. Recyclable and Low Fat Products](01-Problems-001-010.md#001-recyclable-and-low-fat-products)
- [002. Find Customer Referee](01-Problems-001-010.md#002-find-customer-referee)
- [003. Big Countries](01-Problems-001-010.md#003-big-countries)
- [004. Article Views I](01-Problems-001-010.md#004-article-views-i)
- [005. Invalid Tweets](01-Problems-001-010.md#005-invalid-tweets)
- [006. Replace Employee ID With The Unique Identifier](01-Problems-001-010.md#006-replace-employee-id-with-the-unique-identifier)
- [007. Product Sales Analysis I](01-Problems-001-010.md#007-product-sales-analysis-i)
- [008. Customer Who Visited but Did Not Make Any Transactions](01-Problems-001-010.md#008-customer-who-visited-but-did-not-make-any-transactions)
- [009. Rising Temperature](01-Problems-001-010.md#009-rising-temperature)
- [010. Average Time of Process per Machine](01-Problems-001-010.md#010-average-time-of-process-per-machine)

---

### 011–020

- [011. Employee Bonus](02-Problems-011-020.md#011-employee-bonus)
- [012. Students and Examinations](02-Problems-011-020.md#012-students-and-examinations)
- [013. Managers with at Least 5 Direct Reports](02-Problems-011-020.md#013-managers-with-at-least-5-direct-reports)
- [014. Confirmation Rate](02-Problems-011-020.md#014-confirmation-rate)
- [015. Not Boring Movies](02-Problems-011-020.md#015-not-boring-movies)
- [016. Average Selling Price](02-Problems-011-020.md#016-average-selling-price)
- [017. Project Employees I](02-Problems-011-020.md#017-project-employees-i)
- [018. Percentage of Users Attended a Contest](02-Problems-011-020.md#018-percentage-of-users-attended-a-contest)
- [019. Queries Quality and Percentage](02-Problems-011-020.md#019-queries-quality-and-percentage)
- [020. Monthly Transactions I](02-Problems-011-020.md#020-monthly-transactions-i)

---

### 021–030

- [021. Immediate Food Delivery II](03-Problems-021-030.md#021-immediate-food-delivery-ii)
- [022. Game Play Analysis IV](03-Problems-021-030.md#022-game-play-analysis-iv)
- [023. Number of Unique Subjects Taught by Each Teacher](03-Problems-021-030.md#023-number-of-unique-subjects-taught-by-each-teacher)
- [024. User Activity for the Past 30 Days I](03-Problems-021-030.md#024-user-activity-for-the-past-30-days-i)
- [025. Product Sales Analysis III](03-Problems-021-030.md#025-product-sales-analysis-iii)
- [026. Classes With at Least 5 Students](03-Problems-021-030.md#026-classes-with-at-least-5-students)
- [027. Find Followers Count](03-Problems-021-030.md#027-find-followers-count)
- [028. Biggest Single Number](03-Problems-021-030.md#028-biggest-single-number)
- [029. Customers Who Bought All Products](03-Problems-021-030.md#029-customers-who-bought-all-products)
- [030. Number of Employees Reporting to Each Employee](03-Problems-021-030.md#030-number-of-employees-reporting-to-each-employee)

---

### 031–040

- [031. Primary Department for Each Employee](04-Problems-031-040.md#031-primary-department-for-each-employee)
- [032. Triangle Judgement](04-Problems-031-040.md#032-triangle-judgement)
- [033. Consecutive Numbers](04-Problems-031-040.md#033-consecutive-numbers)
- [034. Product Price at a Given Date](04-Problems-031-040.md#034-product-price-at-a-given-date)
- [035. Last Person to Fit in the Bus](04-Problems-031-040.md#035-last-person-to-fit-in-the-bus)
- [036. Count Salary Categories](04-Problems-031-040.md#036-count-salary-categories)
- [037. Employees Whose Manager Left the Company](04-Problems-031-040.md#037-employees-whose-manager-left-the-company)
- [038. Exchange Seats](04-Problems-031-040.md#038-exchange-seats)
- [039. Movie Rating](04-Problems-031-040.md#039-movie-rating)
- [040. Restaurant Growth](04-Problems-031-040.md#040-restaurant-growth)

---

### 041–050

- [041. Friend Requests II: Who Has the Most Friends](05-Problems-041-050.md#041-friend-requests-ii-who-has-the-most-friends)
- [042. Investments in 2016](05-Problems-041-050.md#042-investments-in-2016)
- [043. Department Top Three Salaries](05-Problems-041-050.md#043-department-top-three-salaries)
- [044. Fix Names in a Table](05-Problems-041-050.md#044-fix-names-in-a-table)
- [045. Patients With a Condition](05-Problems-041-050.md#045-patients-with-a-condition)
- [046. Delete Duplicate Emails](05-Problems-041-050.md#046-delete-duplicate-emails)
- [047. Second Highest Salary](05-Problems-041-050.md#047-second-highest-salary)
- [048. Group Sold Products By The Date](05-Problems-041-050.md#048-group-sold-products-by-the-date)
- [049. List the Products Ordered in a Period](05-Problems-041-050.md#049-list-the-products-ordered-in-a-period)
- [050. Find Users With Valid E-Mails](05-Problems-041-050.md#050-find-users-with-valid-e-mails)

# LeetCode SQL 50 — Problems 001–010

---

# 001. Recyclable and Low Fat Products

## Objective

Return the IDs of products that are both recyclable and low fat.

### Tables

#### Products

| Column | Type |
|---------|------|
| product_id | int |
| low_fats | enum('Y','N') |
| recyclable | enum('Y','N') |

---

## My Solution

```sql

```

---

## Explanation

```

```

---

# 002. Find Customer Referee

## Objective

Return every customer that was **not** referred by the customer with ID 2.

### Tables

#### Customer

| Column | Type |
|---------|------|
| id | int |
| name | varchar |
| referee_id | int |

---

## My Solution

```sql

```

---

## Explanation

```

```

---

# 003. Big Countries

## Objective

Return countries that satisfy at least one of the following:

- Large land area
- Large population

### Tables

#### World

| Column | Type |
|---------|------|
| name | varchar |
| continent | varchar |
| area | int |
| population | int |
| gdp | bigint |

---

## My Solution

```sql

```

---

## Explanation

```

```

---

# 004. Article Views I

## Objective

Find authors who viewed at least one of their own articles.

Return each qualifying author only once.

### Tables

#### Views

| Column | Type |
|---------|------|
| article_id | int |
| author_id | int |
| viewer_id | int |
| view_date | date |

---

## My Solution

```sql

```

---

## Explanation

```

```

---

# 005. Invalid Tweets

## Objective

Return the IDs of tweets whose content exceeds the allowed character limit.

### Tables

#### Tweets

| Column | Type |
|---------|------|
| tweet_id | int |
| content | varchar |

---

## My Solution

```sql

```

---

## Explanation

```

```

---

# 006. Replace Employee ID With The Unique Identifier

## Objective

Return each employee together with their unique identifier, if one exists.

### Tables

#### Employees

| Column | Type |
|---------|------|
| id | int |
| name | varchar |

#### EmployeeUNI

| Column | Type |
|---------|------|
| id | int |
| unique_id | int |

---

## My Solution

```sql

```

---

## Explanation

```

```

---

# 007. Product Sales Analysis I

## Objective

Return each product together with its corresponding sale information.

### Tables

#### Sales

| Column | Type |
|---------|------|
| sale_id | int |
| product_id | int |
| year | int |
| quantity | int |
| price | int |

#### Product

| Column | Type |
|---------|------|
| product_id | int |
| product_name | varchar |

---

## My Solution

```sql

```

---

## Explanation

```

```

---

# 008. Customer Who Visited but Did Not Make Any Transactions

## Objective

Find customers who visited but never completed a transaction.

Return the number of visits for each such customer.

### Tables

#### Visits

| Column | Type |
|---------|------|
| visit_id | int |
| customer_id | int |

#### Transactions

| Column | Type |
|---------|------|
| transaction_id | int |
| visit_id | int |
| amount | int |

---

## My Solution

```sql

```

---

## Explanation

```

```

---

# 009. Rising Temperature

## Objective

Find dates where the recorded temperature is higher than the previous day's temperature.

### Tables

#### Weather

| Column | Type |
|---------|------|
| id | int |
| recordDate | date |
| temperature | int |

---

## My Solution

```sql

```

---

## Explanation

```

```

---

# 010. Average Time of Process per Machine

## Objective

Calculate the average processing time for each machine.

### Tables

#### Activity

| Column | Type |
|---------|------|
| machine_id | int |
| process_id | int |
| activity_type | enum |
| timestamp | float |

---

## My Solution

```sql

```

---

## Explanation

```

```
# LeetCode SQL 50 — Problems 011–020

---

# 011. Employee Bonus

## Question

Return the name and bonus of every employee whose bonus is less than `1000`.

Employees who have not received a bonus should also be included.

## Tables

### `Employee`

| Column | Type |
|---|---|
| `empId` | int |
| `name` | varchar |
| `supervisor` | int |
| `salary` | int |

### `Bonus`

| Column | Type |
|---|---|
| `empId` | int |
| `bonus` | int |

---

## My Solution

```sql

```

---

## Explanation



---

# 012. Students and Examinations

## Question

Return every possible student–subject combination and the number of examinations that the student attended for that subject.

Order the results by `student_id` and then by `subject_name`.

## Tables

### `Students`

| Column | Type |
|---|---|
| `student_id` | int |
| `student_name` | varchar |

### `Subjects`

| Column | Type |
|---|---|
| `subject_name` | varchar |

### `Examinations`

| Column | Type |
|---|---|
| `student_id` | int |
| `subject_name` | varchar |

---

## My Solution

```sql

```

---

## Explanation



---

# 013. Managers with at Least 5 Direct Reports

## Question

Return the names of managers who have at least five employees reporting directly to them.

## Tables

### `Employee`

| Column | Type |
|---|---|
| `id` | int |
| `name` | varchar |
| `department` | varchar |
| `managerId` | int |

---

## My Solution

```sql

```

---

## Explanation



---

# 014. Confirmation Rate

## Question

Calculate the confirmation rate for every registered user.

A user's confirmation rate is:

```text
Number of confirmed requests ÷ Total confirmation requests
```

Return `0` for users who did not make any confirmation requests. Round the rate to two decimal places.

## Tables

### `Signups`

| Column | Type |
|---|---|
| `user_id` | int |
| `time_stamp` | datetime |

### `Confirmations`

| Column | Type |
|---|---|
| `user_id` | int |
| `time_stamp` | datetime |
| `action` | enum('confirmed', 'timeout') |

---

## My Solution

```sql

```

---

## Explanation



---

# 015. Not Boring Movies

## Question

Return movies that meet both conditions:

- The movie has an odd-numbered ID.
- Its description is not `boring`.

Order the results from highest to lowest rating.

## Tables

### `Cinema`

| Column | Type |
|---|---|
| `id` | int |
| `movie` | varchar |
| `description` | varchar |
| `rating` | float |

---

## My Solution

```sql

```

---

## Explanation



---

# 016. Average Selling Price

## Question

Calculate the average selling price for every product.

The calculation should account for the number of units sold at each price. Round the result to two decimal places.

Return an average price of `0` for products with no sales.

## Tables

### `Prices`

| Column | Type |
|---|---|
| `product_id` | int |
| `start_date` | date |
| `end_date` | date |
| `price` | int |

### `UnitsSold`

| Column | Type |
|---|---|
| `product_id` | int |
| `purchase_date` | date |
| `units` | int |

---

## My Solution

```sql

```

---

## Explanation



---

# 017. Project Employees I

## Question

Calculate the average number of years of employee experience for each project.

Round the average to two decimal places.

## Tables

### `Project`

| Column | Type |
|---|---|
| `project_id` | int |
| `employee_id` | int |

### `Employee`

| Column | Type |
|---|---|
| `employee_id` | int |
| `name` | varchar |
| `experience_years` | int |

---

## My Solution

```sql

```

---

## Explanation



---

# 018. Percentage of Users Attended a Contest

## Question

Calculate the percentage of all users who registered for each contest.

Round the percentage to two decimal places.

Order the results by:

1. Percentage from highest to lowest
2. Contest ID from lowest to highest when percentages are tied

## Tables

### `Users`

| Column | Type |
|---|---|
| `user_id` | int |
| `user_name` | varchar |

### `Register`

| Column | Type |
|---|---|
| `contest_id` | int |
| `user_id` | int |

---

## My Solution

```sql

```

---

## Explanation



---

# 019. Queries Quality and Percentage

## Question

For each query name, calculate:

- **Quality:** the average of `rating / position`
- **Poor query percentage:** the percentage of queries with a rating below `3`

Round both results to two decimal places.

## Tables

### `Queries`

| Column | Type |
|---|---|
| `query_name` | varchar |
| `result` | varchar |
| `position` | int |
| `rating` | int |

---

## My Solution

```sql

```

---

## Explanation



---

# 020. Monthly Transactions I

## Question

For each month and country, return:

- Total number of transactions
- Number of approved transactions
- Total transaction amount
- Total amount from approved transactions

Represent each month using the `YYYY-MM` format.

## Tables

### `Transactions`

| Column | Type |
|---|---|
| `id` | int |
| `country` | varchar |
| `state` | enum('approved', 'declined') |
| `amount` | int |
| `trans_date` | date |

---

## My Solution

```sql

```

---

## Explanation

# LeetCode SQL 50 — Problems 021–030

---

# 021. Immediate Food Delivery II

## Question

For each customer, identify their first order.

Calculate the percentage of customers whose first order was immediate, meaning the preferred delivery date was the same as the order date.

Round the result to two decimal places.

## Tables

### `Delivery`

| Column | Type |
|---|---|
| `delivery_id` | int |
| `customer_id` | int |
| `order_date` | date |
| `customer_pref_delivery_date` | date |

---

## My Solution

```sql

```

---

## Explanation



---

# 022. Game Play Analysis IV

## Question

Calculate the fraction of players who logged in again exactly one day after their first login.

Round the result to two decimal places.

## Tables

### `Activity`

| Column | Type |
|---|---|
| `player_id` | int |
| `device_id` | int |
| `event_date` | date |
| `games_played` | int |

---

## My Solution

```sql

```

---

## Explanation



---

# 023. Number of Unique Subjects Taught by Each Teacher

## Question

Return each teacher and the number of distinct subjects they teach.

A teacher may teach the same subject in more than one department, but that subject should only be counted once.

## Tables

### `Teacher`

| Column | Type |
|---|---|
| `teacher_id` | int |
| `subject_id` | int |
| `dept_id` | int |

---

## My Solution

```sql

```

---

## Explanation



---

# 024. User Activity for the Past 30 Days I

## Question

Return the number of active users for each day during the 30-day period ending on `2019-07-27`.

A user is active on a day when they performed at least one recorded activity.

Do not include dates with no active users.

## Tables

### `Activity`

| Column | Type |
|---|---|
| `user_id` | int |
| `session_id` | int |
| `activity_date` | date |
| `activity_type` | enum |

---

## My Solution

```sql

```

---

## Explanation



---

# 025. Product Sales Analysis III

## Question

For each product, identify the earliest year in which it was sold.

Return the product ID, first year, quantity, and price from that year.

## Tables

### `Sales`

| Column | Type |
|---|---|
| `sale_id` | int |
| `product_id` | int |
| `year` | int |
| `quantity` | int |
| `price` | int |

---

## My Solution

```sql

```

---

## Explanation



---

# 026. Classes With at Least 5 Students

## Question

Return the classes that have at least five distinct students enrolled.

## Tables

### `Courses`

| Column | Type |
|---|---|
| `student` | varchar |
| `class` | varchar |

---

## My Solution

```sql

```

---

## Explanation



---

# 027. Find Followers Count

## Question

Return each user together with the number of followers they have.

Order the results by `user_id` from lowest to highest.

## Tables

### `Followers`

| Column | Type |
|---|---|
| `user_id` | int |
| `follower_id` | int |

---

## My Solution

```sql

```

---

## Explanation



---

# 028. Biggest Single Number

## Question

A single number is a value that appears exactly once in the table.

Return the largest single number.

Return `NULL` when no single number exists.

## Tables

### `MyNumbers`

| Column | Type |
|---|---|
| `num` | int |

---

## My Solution

```sql

```

---

## Explanation



---

# 029. Customers Who Bought All Products

## Question

Return the IDs of customers who purchased every product listed in the `Product` table.

## Tables

### `Customer`

| Column | Type |
|---|---|
| `customer_id` | int |
| `product_key` | int |

### `Product`

| Column | Type |
|---|---|
| `product_key` | int |

---

## My Solution

```sql

```

---

## Explanation



---

# 030. Number of Employees Reporting to Each Employee

## Question

For each employee who manages at least one other employee, return:

- Their employee ID
- Their name
- The number of employees who report directly to them
- The average age of their direct reports

Round the average age to the nearest integer.

Order the results by employee ID.

## Tables

### `Employees`

| Column | Type |
|---|---|
| `employee_id` | int |
| `name` | varchar |
| `reports_to` | int |
| `age` | int |

---

## My Solution

```sql

```

---

## Explanation

# LeetCode SQL 50 — Problems 031–040

---

# 031. Primary Department for Each Employee

## Question

Return the primary department for every employee.

If an employee belongs to only one department, return that department even if it is not marked as primary.

### Tables

#### Employee

| Column | Type |
|---------|------|
| employee_id | int |
| department_id | int |
| primary_flag | enum('Y','N') |

---

## My Solution

```sql

```

---

## Explanation



---

# 032. Triangle Judgement

## Question

Determine whether each set of three side lengths can form a valid triangle.

Return the original values together with the result.

### Tables

#### Triangle

| Column | Type |
|---------|------|
| x | int |
| y | int |
| z | int |

---

## My Solution

```sql

```

---

## Explanation



---

# 033. Consecutive Numbers

## Question

Return every number that appears at least three times consecutively in the log.

### Tables

#### Logs

| Column | Type |
|---------|------|
| id | int |
| num | int |

---

## My Solution

```sql

```

---

## Explanation



---

# 034. Product Price at a Given Date

## Question

Return the price of every product on a specified date.

If a product has never had its price updated before that date, return the default price.

### Tables

#### Products

| Column | Type |
|---------|------|
| product_id | int |
| new_price | int |
| change_date | date |

---

## My Solution

```sql

```

---

## Explanation



---

# 035. Last Person to Fit in the Bus

## Question

Passengers board a bus in queue order.

The bus has a maximum weight capacity.

Return the name of the last passenger who can board without exceeding the limit.

### Tables

#### Queue

| Column | Type |
|---------|------|
| person_id | int |
| person_name | varchar |
| weight | int |
| turn | int |

---

## My Solution

```sql

```

---

## Explanation



---

# 036. Count Salary Categories

## Question

Classify accounts into salary categories and return the number of accounts in each category.

### Tables

#### Accounts

| Column | Type |
|---------|------|
| account_id | int |
| income | int |

---

## My Solution

```sql

```

---

## Explanation



---

# 037. Employees Whose Manager Left the Company

## Question

Return employees whose manager no longer exists in the employee table.

Only include employees whose salary meets the required condition.

Order the results by employee ID.

### Tables

#### Employees

| Column | Type |
|---------|------|
| employee_id | int |
| name | varchar |
| manager_id | int |
| salary | int |

---

## My Solution

```sql

```

---

## Explanation



---

# 038. Exchange Seats

## Question

Swap the seat IDs of every pair of consecutive students.

If the number of students is odd, leave the final student unchanged.

### Tables

#### Seat

| Column | Type |
|---------|------|
| id | int |
| student | varchar |

---

## My Solution

```sql

```

---

## Explanation



---

# 039. Movie Rating

## Question

Determine:

- The user who rated the greatest number of movies.
- The movie with the highest average rating during the specified month.

Return both results.

### Tables

#### Movies

| Column | Type |
|---------|------|
| movie_id | int |
| title | varchar |

#### Users

| Column | Type |
|---------|------|
| user_id | int |
| name | varchar |

#### MovieRating

| Column | Type |
|---------|------|
| movie_id | int |
| user_id | int |
| rating | int |
| created_at | date |

---

## My Solution

```sql

```

---

## Explanation



---

# 040. Restaurant Growth

## Question

For every day beginning with the seventh recorded day, calculate:

- The total revenue over the previous seven days (inclusive).
- The average daily revenue over the same seven-day period.

Round the average to two decimal places.

### Tables

#### Customer

| Column | Type |
|---------|------|
| customer_id | int |
| name | varchar |
| visited_on | date |
| amount | int |

---

## My Solution

```sql

```

---

## Explanation

# LeetCode SQL 50 — Problems 041–050

---

# 041. Friend Requests II: Who Has the Most Friends

## Question

Determine which user has the greatest number of friends.

Return the user's ID together with the total number of friends.

### Tables

#### RequestAccepted

| Column | Type |
|---------|------|
| requester_id | int |
| accepter_id | int |
| accept_date | date |

---

## My Solution

```sql

```

---

## Explanation



---

# 042. Investments in 2016

## Question

Calculate the total investment value in 2016 for policyholders who satisfy the required investment and location conditions.

Round the result to two decimal places.

### Tables

#### Insurance

| Column | Type |
|---------|------|
| pid | int |
| tiv_2015 | float |
| tiv_2016 | float |
| lat | float |
| lon | float |

---

## My Solution

```sql

```

---

## Explanation



---

# 043. Department Top Three Salaries

## Question

Return the three highest distinct salaries from every department.

Include the employee name, department name, and salary.

### Tables

#### Employee

| Column | Type |
|---------|------|
| id | int |
| name | varchar |
| salary | int |
| departmentId | int |

#### Department

| Column | Type |
|---------|------|
| id | int |
| name | varchar |

---

## My Solution

```sql

```

---

## Explanation



---

# 044. Fix Names in a Table

## Question

Capitalize the first letter of each customer's name and convert all remaining letters to lowercase.

Return the results ordered by user ID.

### Tables

#### Users

| Column | Type |
|---------|------|
| user_id | int |
| name | varchar |

---

## My Solution

```sql

```

---

## Explanation



---

# 045. Patients With a Condition

## Question

Return patients whose list of conditions contains the required diagnosis code.

### Tables

#### Patients

| Column | Type |
|---------|------|
| patient_id | int |
| patient_name | varchar |
| conditions | varchar |

---

## My Solution

```sql

```

---

## Explanation



---

# 046. Delete Duplicate Emails

## Question

Delete duplicate email records while keeping the record with the smallest ID for each email address.

### Tables

#### Person

| Column | Type |
|---------|------|
| id | int |
| email | varchar |

---

## My Solution

```sql

```

---

## Explanation



---

# 047. Second Highest Salary

## Question

Return the second highest distinct salary.

If a second highest salary does not exist, return `NULL`.

### Tables

#### Employee

| Column | Type |
|---------|------|
| id | int |
| salary | int |

---

## My Solution

```sql

```

---

## Explanation



---

# 048. Group Sold Products By The Date

## Question

For each selling date, return:

- The number of unique products sold
- A comma-separated list of those product names in alphabetical order

### Tables

#### Activities

| Column | Type |
|---------|------|
| sell_date | date |
| product | varchar |

---

## My Solution

```sql

```

---

## Explanation



---

# 049. List the Products Ordered in a Period

## Question

Return products that were ordered at least the required number of times during the specified month.

### Tables

#### Products

| Column | Type |
|---------|------|
| product_id | int |
| product_name | varchar |
| product_category | varchar |

#### Orders

| Column | Type |
|---------|------|
| product_id | int |
| order_date | date |
| unit | int |

---

## My Solution

```sql

```

---

## Explanation



---

# 050. Find Users With Valid E-Mails

## Question

Return users whose email addresses satisfy the required formatting rules.

### Tables

#### Users

| Column | Type |
|---------|------|
| user_id | int |
| name | varchar |
| mail | varchar |

---

## My Solution

```sql

```

---

## Explanation
