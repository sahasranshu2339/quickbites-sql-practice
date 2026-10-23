# QuickBites: SQL Practice Project

A beginner-to-intermediate MySQL project built around a food-delivery database. It creates a three-table schema, loads sample data, and answers 10 practice questions using filtering, sorting, aggregation, subqueries and joins.

## What this project covers

- Creating a database and tables with primary keys, foreign keys, defaults and `NOT NULL` constraints
- Inserting sample data
- Filtering with `WHERE`, sorting with `ORDER BY`
- Aggregate functions: `SUM`, `AVG`, `COUNT`
- Grouping with `GROUP BY`
- Subqueries (in `WHERE` and with `IN`)
- `INNER JOIN` across two and three tables

## Database schema

```
customers                restaurants               orders
-----------              -------------             ---------------
customer_id (PK)         restaurant_id (PK)        order_id (PK)
first_name               name                      customer_id (FK) -> customers
last_name                cuisine_type              restaurant_id (FK) -> restaurants
city                     rating                    order_date
join_date                                          total_amount
                                                   status
```

One customer can place many orders, and one restaurant can receive many orders.

| Table | Rows | Purpose |
|---|---|---|
| `customers` | 5 | People who place orders |
| `restaurants` | 5 | Restaurants with cuisine and rating |
| `orders` | 10 | Orders linking a customer to a restaurant, with amount and status (`Delivered`, `Cancelled`, `Pending`) |

## Getting started

**Requirements:** MySQL 8.x (or MySQL Workbench / any MySQL client).

1. Clone this repository.
2. Open the `.sql` file in MySQL Workbench, or run it from the terminal:

   ```bash
   mysql -u your_username -p < quickbites.sql
   ```

3. The script creates the `quickbites_db` database, the tables and the sample data, then runs the practice queries.

> **Warning:** the script starts with `DROP DATABASE IF EXISTS quickbites_db;`. Running it deletes any existing database with that name. Don't run it against a database you want to keep.

## The 10 practice queries

| # | Question | Concepts |
|---|---|---|
| 1 | Restaurants with a rating of 4.5 or higher | `WHERE` |
| 2 | All orders from most to least expensive | `ORDER BY` |
| 3 | Delivered orders costing more than $20 | `WHERE` with `AND` |
| 4 | Total revenue and average order value from delivered orders | `SUM`, `AVG` |
| 5 | Number of customers in each city | `COUNT`, `GROUP BY` |
| 6 | Total sales per restaurant, highest first | `SUM`, `GROUP BY`, `ORDER BY` |
| 7 | Orders more expensive than the overall average | Subquery |
| 8 | Customers who have at least one cancelled order | `IN` with subquery |
| 9 | Customer names alongside their order details | `INNER JOIN` |
| 10 | Full picture: customer, restaurant and amount per order | Multi-table `INNER JOIN` |

## Sample results

**Query 1: restaurants rated 4.5 or higher**

| name | cuisine_type | rating |
|---|---|---|
| Pizza Planet | Italian | 4.5 |
| Wok Express | Asian | 4.7 |

**Query 4: delivered orders summary**

| total_revenue | average_order_value |
|---|---|
| 246.25 | about 30.78 |

**Query 5: customers per city**

| city | total_customers |
|---|---|
| New York | 2 |
| Los Angeles | 2 |
| Chicago | 1 |

**Query 7: orders above the overall average (27.375)**

Orders 3, 6, 8 and 10.

**Query 8: customers with a cancelled order**

Alice Smith.

## Notes and possible improvements

- Query 6 groups by `restaurant_id`. Joining to `restaurants` would show restaurant names instead of IDs.
- Query 6 includes cancelled and pending orders in sales totals. Adding `WHERE status = 'Delivered'` would count only completed sales.
- Possible next steps: `LEFT JOIN` to find customers with no orders, window functions (`RANK`, running totals), `HAVING`, views, and indexes.

## Author

**Sahasranshu Srichandan**
GitHub: [sahasranshu2339](https://github.com/sahasranshu2339)
Email: sahasranshu2329@gmail.com
