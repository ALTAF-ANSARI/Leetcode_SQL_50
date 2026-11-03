# Select

This folder contains the solutions for the **Select** section of the LeetCode SQL 50 study plan.

## Problem List

| # | Problem | Difficulty | Solution |
|---:|---|---|---|
| 1757 | [Recyclable and Low Fat Products](https://leetcode.com/problems/recyclable-and-low-fat-products/) | Easy | [SQL Solution](./1757-Recyclable-and-Low-Fat-Products.sql) |
| 584 | [Find Customer Referee](https://leetcode.com/problems/find-customer-referee/) | Easy | Coming soon |
| 595 | [Big Countries](https://leetcode.com/problems/big-countries/) | Easy | Coming soon |
| 1148 | [Article Views I](https://leetcode.com/problems/article-views-i/) | Easy | Coming soon |
| 1683 | [Invalid Tweets](https://leetcode.com/problems/invalid-tweets/) | Easy | Coming soon |

---

# 1757. Recyclable and Low Fat Products

<sub>Difficulty: Easy · Topic: SELECT + WHERE · LeetCode SQL 50</sub>

**[Open problem on LeetCode](https://leetcode.com/problems/recyclable-and-low-fat-products/)**

## 1. Problem Statement

You are given a table named `Products` containing information about products. Your task is to return the IDs of all products that satisfy **both** of these conditions:

1. The product is low fat (`low_fats = 'Y'`).
2. The product is recyclable (`recyclable = 'Y'`).

Return only the `product_id` column. The order of the returned rows does not matter.

## 2. Table Schema

### Products

| Column | Type | Description |
|---|---|---|
| product_id | int | Unique identifier for each product; primary key |
| low_fats | enum ('Y', 'N') | Whether the product is low fat |
| recyclable | enum ('Y', 'N') | Whether the product is recyclable |

## 3. Example

**Input: Products**

| product_id | low_fats | recyclable |
|---:|:---:|:---:|
| 0 | Y | N |
| 1 | Y | Y |
| 2 | N | Y |
| 3 | Y | Y |
| 4 | N | N |

**Output**

| product_id |
|---:|
| 1 |
| 3 |

**Explanation:** Products with IDs **1** and **3** have `low_fats = 'Y'` and `recyclable = 'Y'`. Every other product fails at least one of the two conditions, so it is excluded.

## 4. SQL Solution

```sql
SELECT product_id
FROM Products
WHERE low_fats = 'Y'
  AND recyclable = 'Y';
```

## 5. Concept Used: SELECT, WHERE, AND

### A. SELECT

`SELECT product_id` specifies the column we want in the result. We do not need all columns, only the product identifier.

### B. FROM

`FROM Products` tells SQL which table to read records from.

### C. WHERE

`WHERE` filters rows. Only records satisfying the condition are included in the result.

### D. AND (Logical Operator)

The `AND` operator combines two conditions. **Both conditions must be TRUE** for a row to be returned.

- `low_fats = 'Y'` checks whether the product is low fat.
- `recyclable = 'Y'` checks whether the product is recyclable.

If either condition is false (or does not evaluate to true), that row is not selected.

## 6. Visualize the Filtering

| Product ID | Low fat? | Recyclable? | Selected? |
|---:|:---:|:---:|:---:|
| 0 | Y | N | ❌ No |
| 1 | Y | Y | ✅ Yes |
| 2 | N | Y | ❌ No |
| 3 | Y | Y | ✅ Yes |
| 4 | N | N | ❌ No |

Think of `AND` as an intersection: a product must belong to **both** groups (low-fat products and recyclable products).

## 7. AND vs OR

This problem specifically requires `AND`, not `OR`.

| Operator | Meaning | Row is returned when |
|---|---|---|
| AND | Both conditions must be true | Low fat **and** recyclable |
| OR | At least one condition must be true | Low fat **or** recyclable |

Using `OR` would return extra products that satisfy only one condition, which would be incorrect for this problem.

## 8. Complexity

Let **n** be the number of rows in the Products table.

- **Time:** Typically O(n), because the query may need to examine each row to evaluate the filters. An optimizer may use an appropriate index if available.
- **Auxiliary space:** O(1) for the logical query itself; actual execution memory is database-engine dependent.

## 9. Key Takeaways

- Use `SELECT` to choose the required output columns.
- Use `WHERE` to filter rows based on conditions.
- Use `AND` when every condition must be satisfied.
- Put string/enum values such as `'Y'` inside single quotes.
- Select only the columns requested by the problem.

## 10. Interview Practice

1. What is the difference between `AND` and `OR` in SQL?
2. Does `WHERE` filter rows or columns?
3. What happens if one condition joined by `AND` is false?
4. How would you find products that are low fat **or** recyclable?
5. Why do we write `'Y'` in single quotes?

---

**Status:** ✅ Solved

**Next problem:** [Find Customer Referee](https://leetcode.com/problems/find-customer-referee/)

[← Back to repository](../README.md)
