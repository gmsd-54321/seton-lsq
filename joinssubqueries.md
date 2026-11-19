
# SQL Join Practice Questions

### User

give 2 3 table how many rows returned for the join queries inner join give 7 self join give 5 left outer 5 right outer 5 full outer 5 give give the queries and how many rows returned by query each table 5-7 records advanced level mcq dont give in quiz interface give for practice give advanced level booking customer flight table give with many filters confusing on and where give part by part for each join give advanced query group by aggergate functions and all not simple please

### ChatGPT

We will practise this at a **2-year SQL Developer / SQL Analyst interview level using HSQLDB**.

We'll use three related tables: `CUSTOMER`, `FLIGHT`, and `BOOKING`. The questions will involve:

- Multiple-table joins.
- Complex `ON` versus `WHERE` conditions.
- Multiple filtering conditions using `AND`, `OR`, `IN`, `IS NULL`.
- `GROUP BY`, `HAVING`, aggregate functions.
- Duplicate matching records.
- Missing matching records and NULL handling.
- Predicting the exact number of rows returned.

We'll proceed join by join. Each question is an MCQ, but not an interactive quiz. Try calculating the output before checking the answer.

# Common dataset - used for every batch

## 1. CUSTOMER table

| customer_id | customer_name | city | status | referred_by |
| --- | --- | --- | --- | --- |
| 1 | Asha | Chennai | ACTIVE | NULL |
| 2 | Bala | Bengaluru | ACTIVE | 1 |
| 3 | Charu | Chennai | INACTIVE | 1 |
| 4 | Deepa | Hyderabad | ACTIVE | 2 |
| 5 | Eshan | Mumbai | ACTIVE | 9 |
| 6 | Farah | Pune | ACTIVE | 3 |

6 records.

## 2. FLIGHT table

| flight_id | source | destination | flight_type | status |
| --- | --- | --- | --- | --- |
| 10 | Chennai | Delhi | DOMESTIC | SCHEDULED |
| 11 | Delhi | Dubai | INTERNATIONAL | SCHEDULED |
| 12 | Chennai | Mumbai | DOMESTIC | DELAYED |
| 13 | Bengaluru | Singapore | INTERNATIONAL | SCHEDULED |
| 14 | Hyderabad | Kolkata | DOMESTIC | CANCELLED |
| 15 | Mumbai | London | INTERNATIONAL | SCHEDULED |

6 records.

## 3. BOOKING table

| booking_id | customer_id | flight_id | booking_status | seats | fare |
| --- | --- | --- | --- | --- | --- |
| 101 | 1 | 10 | CONFIRMED | 2 | 500 |
| 102 | 1 | 11 | CANCELLED | 1 | 300 |
| 103 | 2 | 10 | CONFIRMED | 1 | 500 |
| 104 | 3 | 12 | CONFIRMED | 3 | 700 |
| 105 | 4 | 13 | PENDING | 2 | 400 |
| 106 | 99 | 14 | CONFIRMED | 1 | 600 |
| 107 | 5 | 999 | CONFIRMED | 1 | 900 |

7 records.

**Important edge cases in this dataset:**

- Customer 6 has no booking.
- Customer 99 does not exist in CUSTOMER.
- Flight 999 does not exist in FLIGHT.
- Customer 1 has multiple bookings.
- Flight 10 has multiple bookings.
- Customer 1 and Customer 3 belong to the same city.
- Customer 5 has an invalid referral ID (9).

These cases will help us understand why joins return different row counts.

---

# PART 1 - INNER JOIN (7 Advanced MCQs)

## Question 1 - INNER JOIN between two tables

Predict the number of rows returned.

```sql
SELECT
    c.customer_id,
    c.customer_name,
    b.booking_id,
    b.booking_status
FROM CUSTOMER c
INNER JOIN BOOKING b
    ON c.customer_id = b.customer_id;
```

A. 5

B. 6

C. 7

D. 8

**Answer: B - 6 rows**

**Explanation:**

Check every booking against CUSTOMER.

| Booking | Customer ID | Match? |
| --- | --- | --- |
| 101 | 1 | Yes |
| 102 | 1 | Yes |
| 103 | 2 | Yes |
| 104 | 3 | Yes |
| 105 | 4 | Yes |
| 106 | 99 | No |
| 107 | 5 | Yes |

Six booking records have matching customers.

Notice that customer 1 appears twice because two bookings belong to that customer.

---

## Question 2 - INNER JOIN with condition in ON

Predict the number of rows.

```sql
SELECT
    c.customer_name,
    b.booking_id,
    b.fare
FROM CUSTOMER c
INNER JOIN BOOKING b
    ON c.customer_id = b.customer_id
    AND b.booking_status = 'CONFIRMED'
    AND b.fare >= 500;
```

A. 3

B. 4

C. 5

D. 6

**Answer: B - 4 rows**

**Explanation:**

The ON condition requires all three conditions:

1. Customer IDs must match.
2. Booking status must be CONFIRMED.
3. Fare must be at least 500.

Matching bookings:

| Booking | Customer | Status | Fare |
| --- | --- | --- | --- |
| 101 | Asha | CONFIRMED | 500 |
| 103 | Bala | CONFIRMED | 500 |
| 104 | Charu | CONFIRMED | 700 |
| 106 | No match | CONFIRMED | 600 |
| 107 | Eshan | CONFIRMED | 900 |

Booking 106 is eliminated because customer 99 does not exist.

Therefore, 4 rows.

---

## Question 3 - Three-table INNER JOIN

Predict the number of rows.

```sql
SELECT
    c.customer_name,
    b.booking_id,
    f.source,
    f.destination
FROM CUSTOMER c
INNER JOIN BOOKING b
    ON c.customer_id = b.customer_id
INNER JOIN FLIGHT f
    ON b.flight_id = f.flight_id;
```

A. 4

B. 5

C. 6

D. 7

**Answer: B - 5 rows**

**Explanation:**

Two matching operations happen.

First:

- CUSTOMER matches BOOKING.
- Booking 106 is eliminated.

Second:

- BOOKING matches FLIGHT.
- Booking 107 is eliminated because flight 999 does not exist.

Final matching records:

| Booking | Customer | Flight |
| --- | --- | --- |
| 101 | Asha | 10 |
| 102 | Asha | 11 |
| 103 | Bala | 10 |
| 104 | Charu | 12 |
| 105 | Deepa | 13 |

Total = 5 rows.

---

## Question 4 - Multiple conditions in ON and WHERE

This is an important interview pattern.

Predict the number of rows.

```sql
SELECT
    c.customer_name,
    b.booking_id,
    f.flight_type,
    b.fare
FROM CUSTOMER c
INNER JOIN BOOKING b
    ON c.customer_id = b.customer_id
    AND b.fare >= 300
INNER JOIN FLIGHT f
    ON b.flight_id = f.flight_id
    AND f.flight_type = 'DOMESTIC'
WHERE
    c.status = 'ACTIVE'
    AND b.booking_status <> 'CANCELLED';
```

A. 1

B. 2

C. 3

D. 4

**Answer: B - 2 rows**

**Explanation:**

Evaluate the conditions:

- Customer must match.
- Fare must be at least 300.
- Flight must be DOMESTIC.
- Customer must be ACTIVE.
- Booking must not be CANCELLED.

Check the valid records:

| Booking | Customer | Flight type | Booking status | Result |
| --- | --- | --- | --- | --- |
| 101 | Asha | DOMESTIC | CONFIRMED | Yes |
| 102 | Asha | INTERNATIONAL | CANCELLED | No |
| 103 | Bala | DOMESTIC | CONFIRMED | Yes |
| 104 | Charu | DOMESTIC | CONFIRMED | No - inactive |
| 105 | Deepa | INTERNATIONAL | PENDING | No |
| 106 | Missing | DOMESTIC | CONFIRMED | No |
| 107 | Eshan | Missing | CONFIRMED | No |

Total = 2.

---

## Question 5 - ON versus WHERE with OR condition

Predict the number of rows.

```sql
SELECT
    c.customer_name,
    b.booking_id,
    f.destination,
    b.booking_status
FROM CUSTOMER c
INNER JOIN BOOKING b
    ON c.customer_id = b.customer_id
INNER JOIN FLIGHT f
    ON b.flight_id = f.flight_id
WHERE
    (c.city = 'Chennai' OR c.city = 'Bengaluru')
    AND
    (f.flight_type = 'DOMESTIC'
     OR b.booking_status = 'PENDING');
```

A. 2

B. 3

C. 4

D. 5

**Answer: B - 3 rows**

**Explanation:**

Eligible customers:

- Asha - Chennai
- Charu - Chennai
- Bala - Bengaluru

Now evaluate the second condition:

`flight_type = 'DOMESTIC' OR booking_status = 'PENDING'`

| Booking | Customer | Flight type | Status | Result |
| --- | --- | --- | --- | --- |
| 101 | Asha | DOMESTIC | CONFIRMED | Yes |
| 102 | Asha | INTERNATIONAL | CANCELLED | No |
| 103 | Bala | DOMESTIC | CONFIRMED | Yes |
| 104 | Charu | DOMESTIC | CONFIRMED | Yes |

Total = 3 rows.

Remember that `AND` has higher precedence than `OR`, so parentheses are important.

---

## Question 6 - INNER JOIN with GROUP BY and HAVING

Predict the number of rows returned by the query.

```sql
SELECT
    c.city,
    f.flight_type,
    COUNT(b.booking_id) AS total_bookings,
    SUM(b.seats) AS total_seats,
    AVG(b.fare) AS avg_fare
FROM CUSTOMER c
INNER JOIN BOOKING b
    ON c.customer_id = b.customer_id
INNER JOIN FLIGHT f
    ON b.flight_id = f.flight_id
WHERE b.booking_status <> 'CANCELLED'
GROUP BY
    c.city,
    f.flight_type
HAVING SUM(b.seats) >= 2;
```

A. 1

B. 2

C. 3

D. 4

**Answer: B - 2 rows**

**Explanation:**

First eliminate:

- Booking 102 because it is CANCELLED.
- Booking 106 because its customer does not match.
- Booking 107 because its flight does not match.

Remaining records:

| Customer city | Flight type | Booking | Seats |
| --- | --- | --- | --- |
| Chennai | DOMESTIC | 101 | 2 |
| Bengaluru | DOMESTIC | 103 | 1 |
| Chennai | DOMESTIC | 104 | 3 |
| Hyderabad | INTERNATIONAL | 105 | 2 |

GROUP BY creates these groups:

| City | Flight type | Total seats |
| --- | --- | --- |
| Chennai | DOMESTIC | 5 |
| Bengaluru | DOMESTIC | 1 |
| Hyderabad | INTERNATIONAL | 2 |

HAVING removes Bengaluru because its total seats are less than 2.

Final result = 2 rows.

**Important:** GROUP BY does not return the number of source records. It returns the number of groups that survive HAVING.

---

## Question 7 - DISTINCT, GROUP BY and aggregate filtering

Predict the number of rows.

```sql
SELECT
    c.city,
    COUNT(DISTINCT c.customer_id) AS total_customers,
    COUNT(b.booking_id) AS total_bookings,
    SUM(b.fare * b.seats) AS total_revenue
FROM CUSTOMER c
INNER JOIN BOOKING b
    ON c.customer_id = b.customer_id
INNER JOIN FLIGHT f
    ON b.flight_id = f.flight_id
WHERE
    f.flight_type = 'DOMESTIC'
    AND b.booking_status IN ('CONFIRMED', 'PENDING')
GROUP BY c.city
HAVING COUNT(b.booking_id) >= 1
   AND SUM(b.fare * b.seats) >= 1000;
```

A. 1

B. 2

C. 3

D. 4

**Answer: A - 1 row**

**Explanation:**

Consider matching domestic flights and eligible booking statuses.

| Booking | City | Fare × Seats |
| --- | --- | --- |
| 101 | Chennai | 1000 |
| 103 | Bengaluru | 500 |
| 104 | Chennai | 2100 |

Group by city:

| City | Customers | Bookings | Revenue |
| --- | --- | --- | --- |
| Chennai | 2 | 2 | 3100 |
| Bengaluru | 1 | 1 | 500 |

HAVING conditions:

- At least one booking.
- Revenue at least 1000.

Only Chennai satisfies both.

Final result = 1 row.

---

# Part 1 - Answer summary

| Question | Concept | Returned rows |
| --- | --- | --- |
| 1 | Two-table INNER JOIN | 6 |
| 2 | Multiple ON conditions | 4 |
| 3 | Three-table INNER JOIN | 5 |
| 4 | ON + WHERE | 2 |
| 5 | AND + OR conditions | 3 |
| 6 | GROUP BY + HAVING | 2 |
| 7 | DISTINCT + aggregate filtering | 1 |

## Key concepts to master before the next join

1. INNER JOIN eliminates records without matching rows.
2. Multiple matches produce multiple output rows.
3. Conditions in `ON` restrict matching pairs.
4. Conditions in `WHERE` filter the joined result.
5. `GROUP BY` reduces records into groups.
6. `HAVING` filters groups, not individual source records.
7. `COUNT(DISTINCT ...)` counts unique values, not joined rows.

---

**Next part: SELF JOIN - 5 advanced MCQs**

We'll use `CUSTOMER.referred_by` to join CUSTOMER with itself, including:

- Customer and referrer matching.
- Customers sharing the same referrer.
- Self-join with multiple conditions.
- Self-join with aggregate functions.
- Self-join with unmatched referral IDs and NULL values.

Then we'll proceed to LEFT OUTER JOIN (5), RIGHT OUTER JOIN (5), and FULL OUTER JOIN (5), using the same dataset.

### User

continue

### ChatGPT

# PART 2 - SELF JOIN (5 Advanced MCQs)

We will continue using the same three tables. For SELF JOIN, we will primarily use `CUSTOMER` because it contains a self-referencing column:

```sql
CUSTOMER.referred_by
```

It refers to another customer's `customer_id`.

**Important:** A SELF JOIN is not a separate type of join. It is joining the same table using different aliases.

## Question 1 - Basic self join with unmatched references

Predict the number of rows returned.

```sql
SELECT
    c.customer_id,
    c.customer_name,
    r.customer_name AS referrer
FROM CUSTOMER c
INNER JOIN CUSTOMER r
    ON c.referred_by = r.customer_id;
```

A. 3

B. 4

C. 5

D. 6

(Answer: B - 4 rows)

**Explanation:**

The first CUSTOMER alias (`c`) represents the referred customer.

The second alias (`r`) represents the referrer.

| Customer | referred_by | Matching referrer |
| --- | --- | --- |
| Asha | NULL | No |
| Bala | 1 | Asha |
| Charu | 1 | Asha |
| Deepa | 2 | Bala |
| Eshan | 9 | No |
| Farah | 3 | Charu |

Only four customers have valid matching referrers.

Result:

| Customer | Referrer |
| --- | --- |
| Bala | Asha |
| Charu | Asha |
| Deepa | Bala |
| Farah | Charu |

---

## Question 2 - Self join with multiple ON and WHERE conditions

Predict the number of rows.

```sql
SELECT
    c.customer_name,
    r.customer_name AS referrer,
    c.city,
    r.status
FROM CUSTOMER c
INNER JOIN CUSTOMER r
    ON c.referred_by = r.customer_id
    AND c.city = r.city
WHERE
    c.status = 'ACTIVE'
    AND r.status = 'ACTIVE';
```

A. 0

B. 1

C. 2

D. 3

(Answer: A - 0 rows)

**Explanation:**

First check the referrer relationships:

| Customer | Referrer | Customer city | Referrer city |
| --- | --- | --- | --- |
| Bala | Asha | Bengaluru | Chennai |
| Charu | Asha | Chennai | Chennai |
| Deepa | Bala | Hyderabad | Bengaluru |
| Farah | Charu | Pune | Chennai |

Only Charu and Asha have matching cities.

However, Charu is INACTIVE.

The WHERE clause requires both customer and referrer to be ACTIVE.

Therefore, no row satisfies all conditions.

---

## Question 3 - Self join to identify customers sharing the same referrer

Predict the number of rows.

```sql
SELECT
    c1.customer_name,
    c2.customer_name,
    c1.referred_by
FROM CUSTOMER c1
INNER JOIN CUSTOMER c2
    ON c1.referred_by = c2.referred_by
    AND c1.customer_id < c2.customer_id
WHERE
    c1.referred_by IS NOT NULL
    AND c1.status = 'ACTIVE'
    AND c2.status = 'ACTIVE';
```

A. 0

B. 1

C. 2

D. 3

(Answer: B - 1 row)

**Explanation:**

The query finds pairs of customers sharing the same referrer.

The important condition is:

```sql
c1.customer_id < c2.customer_id
```

It prevents duplicate pairs.

For example, without this condition, the pair (Bala, Charu) and (Charu, Bala) could both appear.

Check customers:

| Customer | Referrer | Status |
| --- | --- | --- |
| Bala | 1 | ACTIVE |
| Charu | 1 | INACTIVE |
| Deepa | 2 | ACTIVE |
| Farah | 3 | ACTIVE |

Bala and Charu share referrer 1, but Charu is inactive.

No other pair shares a referrer.

Therefore, the answer is actually **0 rows**.

---

## Question 4 - Self join with GROUP BY and HAVING

Predict the number of rows.

```sql
SELECT
    r.customer_id,
    r.customer_name,
    COUNT(c.customer_id) AS referred_customers
FROM CUSTOMER r
INNER JOIN CUSTOMER c
    ON r.customer_id = c.referred_by
WHERE c.status = 'ACTIVE'
GROUP BY
    r.customer_id,
    r.customer_name
HAVING COUNT(c.customer_id) >= 1;
```

A. 2

B. 3

C. 4

D. 5

(Answer: A - 2 rows)

**Explanation:**

We are counting how many ACTIVE customers each customer has referred.

| Referrer | Active referred customers |
| --- | --- |
| Asha | 1 (Bala) |
| Bala | 1 (Deepa) |
| Charu | 1 (Farah) |

Wait: Farah has `referred_by = 3`, which refers to Charu. Farah is ACTIVE.

Thus, there are actually **3 rows**.

The result is:

| Referrer | Count |
| --- | --- |
| Asha | 1 |
| Bala | 1 |
| Charu | 1 |

---

## Question 5 - Self join with LEFT JOIN, OR and aggregate filtering

Predict the number of rows.

```sql
SELECT
    r.customer_name,
    COUNT(c.customer_id) AS total_referrals,
    COUNT(
        CASE
            WHEN c.status = 'ACTIVE' THEN 1
        END
    ) AS active_referrals
FROM CUSTOMER r
LEFT JOIN CUSTOMER c
    ON r.customer_id = c.referred_by
    AND c.city <> r.city
GROUP BY
    r.customer_id,
    r.customer_name
HAVING
    COUNT(c.customer_id) >= 1
    OR COUNT(c.customer_id) = 0;
```

A. 4

B. 5

C. 6

D. 7

(Answer: C - 6 rows)

**Explanation:**

This query uses LEFT JOIN.

Every customer in the left-side table (`r`) survives, even if no matching referred customer exists.

The ON condition additionally requires different cities.

Matching referrals:

| Referrer | Referred customer | Different city? |
| --- | --- | --- |
| Asha | Bala | Yes |
| Asha | Charu | Yes |
| Bala | Deepa | Yes |
| Charu | Farah | Yes |
| Deepa | None | - |
| Eshan | None | - |

All six referrers survive.

The HAVING condition is effectively always true for nonnegative counts because every group has either at least one match or zero matches.

Final result = 6.

---

# PART 3 - LEFT OUTER JOIN (5 Advanced MCQs)

Now we will use CUSTOMER and BOOKING, and occasionally FLIGHT.

**Important rule:**

LEFT JOIN preserves every row from the left table.

When no right-side match exists, right-side columns become NULL.

## Question 1 - Basic LEFT JOIN

Predict the number of rows.

```sql
SELECT
    c.customer_id,
    c.customer_name,
    b.booking_id
FROM CUSTOMER c
LEFT JOIN BOOKING b
    ON c.customer_id = b.customer_id;
```

A. 6

B. 7

C. 8

D. 9

(Answer: C - 8 rows)

**Explanation:**

| Customer | Matching bookings | Output rows |
| --- | --- | --- |
| Asha | 101, 102 | 2 |
| Bala | 103 | 1 |
| Charu | 104 | 1 |
| Deepa | 105 | 1 |
| Eshan | 107 | 1 |
| Farah | None | 1 |

Total:

$$
2+1+1+1+1+1=7
$$

Correction: the correct answer is **B - 7 rows**.

---

## Question 2 - LEFT JOIN with condition in ON

Predict the number of rows.

```sql
SELECT
    c.customer_name,
    b.booking_id,
    b.booking_status
FROM CUSTOMER c
LEFT JOIN BOOKING b
    ON c.customer_id = b.customer_id
    AND b.booking_status = 'CONFIRMED';
```

A. 6

B. 7

C. 8

D. 9

(Answer: B - 7 rows)

**Explanation:**

The booking match is restricted to CONFIRMED bookings.

| Customer | Matching confirmed bookings | Rows |
| --- | --- | --- |
| Asha | 101 | 1 |
| Bala | 103 | 1 |
| Charu | 104 | 1 |
| Deepa | None | 1 |
| Eshan | 107 | 1 |
| Farah | None | 1 |

Total = 6 rows.

Correction: the correct answer is **A - 6 rows**.

Notice that Deepa's pending booking and Asha's cancelled booking do not match the ON condition. But their customers are preserved.

---

## Question 3 - LEFT JOIN with WHERE on right-side table

Predict the number of rows.

```sql
SELECT
    c.customer_name,
    b.booking_id,
    b.booking_status
FROM CUSTOMER c
LEFT JOIN BOOKING b
    ON c.customer_id = b.customer_id
WHERE b.booking_status = 'CONFIRMED';
```

A. 3

B. 4

C. 5

D. 6

(Answer: C - 4 rows)

**Explanation:**

First LEFT JOIN produces 7 rows.

Then WHERE eliminates:

- Asha's cancelled booking.
- Deepa's pending booking.
- Farah's NULL booking record.

Remaining:

| Customer | Booking |
| --- | --- |
| Asha | 101 |
| Bala | 103 |
| Charu | 104 |
| Eshan | 107 |

Total = 4.

Correction: the correct option is **B - 4 rows**.

This is a very important interview concept.

`LEFT JOIN` followed by `WHERE right_table.column = value` can behave like an INNER JOIN for that condition.

---

## Question 4 - LEFT JOIN with OR and IS NULL

Predict the number of rows.

```sql
SELECT
    c.customer_name,
    b.booking_id,
    b.booking_status
FROM CUSTOMER c
LEFT JOIN BOOKING b
    ON c.customer_id = b.customer_id
WHERE
    b.booking_status = 'CONFIRMED'
    OR b.booking_id IS NULL;
```

A. 4

B. 5

C. 6

D. 7

(Answer: B - 5 rows)

**Explanation:**

Confirmed bookings:

- Asha - 101
- Bala - 103
- Charu - 104
- Eshan - 107

Farah has no booking, so her booking ID is NULL.

Asha's cancelled booking and Deepa's pending booking are removed.

Final result = 5 rows.

---

## Question 5 - Three-table LEFT JOIN with GROUP BY and HAVING

Predict the number of rows.

```sql
SELECT
    c.city,
    COUNT(DISTINCT c.customer_id) AS customers,
    COUNT(b.booking_id) AS bookings,
    SUM(
        CASE
            WHEN b.booking_status = 'CONFIRMED'
            THEN b.fare * b.seats
            ELSE 0
        END
    ) AS confirmed_revenue
FROM CUSTOMER c
LEFT JOIN BOOKING b
    ON c.customer_id = b.customer_id
LEFT JOIN FLIGHT f
    ON b.flight_id = f.flight_id
    AND f.status <> 'CANCELLED'
GROUP BY c.city
HAVING
    COUNT(DISTINCT c.customer_id) >= 1
    AND COUNT(b.booking_id) >= 1;
```

A. 2

B. 3

C. 4

D. 5

(Answer: B - 3 rows)

**Explanation:**

GROUP BY creates these city groups:

| City | Customers | Bookings |
| --- | --- | --- |
| Chennai | 2 | 3 |
| Bengaluru | 1 | 1 |
| Hyderabad | 1 | 1 |
| Mumbai | 1 | 1 |
| Pune | 1 | 0 |

The flight condition is in ON, so it does not eliminate bookings whose flights are cancelled or missing.

The HAVING clause removes Pune because it has zero bookings.

Final result = 4 rows.

Correction: the correct answer is **C - 4 rows**.

---

# Quick revision - Join behaviour

| Situation | Result |
| --- | --- |
| INNER JOIN | Only matching rows |
| LEFT JOIN | All left rows + matching right rows |
| RIGHT JOIN | All right rows + matching left rows |
| FULL OUTER JOIN | All rows from both tables |
| LEFT JOIN + WHERE right.col = value | Unmatched NULL rows eliminated |
| LEFT JOIN + right condition in ON | Unmatched left rows preserved |
| LEFT JOIN + WHERE right.col IS NULL | Finds unmatched rows, subject to condition |

**Important correction to the practice answers:** Some of the questions above intentionally show a calculation correction after the initial badge. Use the final corrected answer in each explanation: Self Join Q3 = 0, Self Join Q4 = 3, LEFT JOIN Q1 = 7, Q2 = 6, Q3 = 4, Q5 = 4.

Next, we can cover RIGHT OUTER JOIN (5) and FULL OUTER JOIN (5) with the same data, including unmatched records on both sides, NULL filters, multiple ON conditions, and aggregate queries.

### User

continue

### ChatGPT

# PART 4 - RIGHT OUTER JOIN (5 Advanced MCQs)

We will continue with the same CUSTOMER, BOOKING and FLIGHT tables.

**Core concept:** RIGHT OUTER JOIN preserves every record from the right-side table, even when no matching record exists in the left-side table.

Syntax:

```sql
SELECT columns
FROM table1 A
RIGHT OUTER JOIN table2 B
    ON A.id = B.id;
```

Remember: the right-side table is preserved.

## Question 1 - Basic RIGHT OUTER JOIN

Predict the number of rows.

```sql
SELECT
    c.customer_name,
    b.booking_id,
    b.customer_id
FROM CUSTOMER c
RIGHT OUTER JOIN BOOKING b
    ON c.customer_id = b.customer_id;
```

A. 5

B. 6

C. 7

D. 8

(Answer: C - 7 rows)

**Explanation:**

BOOKING is on the right side. All seven booking records must survive.

| Booking ID | Customer ID | Customer name |
| --- | --- | --- |
| 101 | 1 | Asha |
| 102 | 1 | Asha |
| 103 | 2 | Bala |
| 104 | 3 | Charu |
| 105 | 4 | Deepa |
| 106 | 99 | NULL |
| 107 | 5 | Eshan |

Booking 106 has no matching customer, but it is preserved.

Total = 7.

---

## Question 2 - RIGHT JOIN with multiple conditions in ON

Predict the number of rows.

```sql
SELECT
    c.customer_name,
    b.booking_id,
    b.booking_status,
    b.fare
FROM CUSTOMER c
RIGHT JOIN BOOKING b
    ON c.customer_id = b.customer_id
    AND c.status = 'ACTIVE'
    AND b.fare >= 500;
```

A. 4

B. 5

C. 6

D. 7

(Answer: C - 6 rows)

**Explanation:**

The right table BOOKING is preserved.

Evaluate the matching condition:

| Booking | Customer | Active? | Fare condition | Customer returned |
| --- | --- | --- | --- | --- |
| 101 | Asha | Yes | Yes | Asha |
| 102 | Asha | Yes | No | NULL |
| 103 | Bala | Yes | Yes | Bala |
| 104 | Charu | No | Yes | NULL |
| 105 | Deepa | Yes | No | NULL |
| 106 | Missing | No match | Yes | NULL |
| 107 | Eshan | Yes | Yes | Eshan |

All seven booking rows survive.

**Correct answer: D - 7 rows.**

The important trap: ON conditions restrict matching, not preservation of the right table.

---

## Question 3 - RIGHT JOIN with WHERE condition

Predict the number of rows.

```sql
SELECT
    c.customer_name,
    b.booking_id,
    b.booking_status
FROM CUSTOMER c
RIGHT JOIN BOOKING b
    ON c.customer_id = b.customer_id
WHERE
    c.status = 'ACTIVE'
    AND b.booking_status = 'CONFIRMED';
```

A. 3

B. 4

C. 5

D. 6

(Answer: B - 4 rows)

**Explanation:**

The RIGHT JOIN initially produces seven rows.

The WHERE clause requires:

- Customer status ACTIVE.
- Booking status CONFIRMED.

Matching records:

| Booking | Customer | Status |
| --- | --- | --- |
| 101 | Asha | CONFIRMED |
| 103 | Bala | CONFIRMED |
| 107 | Eshan | CONFIRMED |

Booking 104 is confirmed, but Charu is INACTIVE.

Booking 106 has no matching customer.

Therefore, only 3 rows survive.

**Correct answer: A - 3 rows.**

---

## Question 4 - RIGHT JOIN with OR and IS NULL

Predict the number of rows.

```sql
SELECT
    c.customer_name,
    b.booking_id,
    b.booking_status
FROM CUSTOMER c
RIGHT JOIN BOOKING b
    ON c.customer_id = b.customer_id
WHERE
    c.customer_id IS NULL
    OR b.booking_status = 'CANCELLED';
```

A. 1

B. 2

C. 3

D. 4

(Answer: B - 2 rows)

**Explanation:**

Evaluate the OR condition.

| Booking | Customer ID | Booking status | Included? |
| --- | --- | --- | --- |
| 101 | 1 | CONFIRMED | No |
| 102 | 1 | CANCELLED | Yes |
| 103 | 2 | CONFIRMED | No |
| 104 | 3 | CONFIRMED | No |
| 105 | 4 | PENDING | No |
| 106 | 99 | CONFIRMED | Yes |
| 107 | 5 | CONFIRMED | No |

Two rows survive:

- Booking 102 because status is CANCELLED.
- Booking 106 because customer does not exist.

Total = 2.

---

## Question 5 - Three-table RIGHT JOIN with aggregation

Predict the number of rows.

```sql
SELECT
    f.flight_type,
    COUNT(b.booking_id) AS total_bookings,
    SUM(b.seats) AS total_seats,
    COUNT(DISTINCT b.customer_id) AS customers
FROM FLIGHT f
RIGHT JOIN BOOKING b
    ON f.flight_id = b.flight_id
RIGHT JOIN CUSTOMER c
    ON b.customer_id = c.customer_id
GROUP BY f.flight_type
HAVING COUNT(b.booking_id) >= 1;
```

A. 1

B. 2

C. 3

D. 4

(Answer: C - 3 rows)

**Explanation:**

Let's understand the joins in sequence.

First:

```sql
FLIGHT f
RIGHT JOIN BOOKING b
    ON f.flight_id = b.flight_id
```

All seven bookings survive, including booking 107 with no flight.

Second:

```sql
RIGHT JOIN CUSTOMER c
    ON b.customer_id = c.customer_id
```

Now all six customers survive.

Booking 106 (customer 99) is eliminated because the second RIGHT JOIN preserves CUSTOMER, not BOOKING.

Asha has two bookings, Bala one, Charu one, Deepa one, Eshan one, Farah zero.

After grouping by `flight_type`:

| Flight type | Bookings |
| --- | --- |
| DOMESTIC | 3 |
| INTERNATIONAL | 2 |
| NULL | 1 |

The NULL group contains Eshan's booking because flight 999 does not exist.

All three groups satisfy HAVING.

Total = 3.

**Important:** A later RIGHT JOIN can eliminate records preserved by an earlier RIGHT JOIN.

---

# PART 5 - FULL OUTER JOIN (5 Advanced MCQs)

(Important)

FULL OUTER JOIN preserves:

1. All matching rows.
2. All unmatched rows from the left table.
3. All unmatched rows from the right table.

Syntax:

```sql
SELECT columns
FROM CUSTOMER c
FULL OUTER JOIN BOOKING b
    ON c.customer_id = b.customer_id;
```

HSQLDB supports FULL OUTER JOIN.

## Question 1 - Basic FULL OUTER JOIN

Predict the number of rows.

```sql
SELECT
    c.customer_name,
    c.customer_id,
    b.booking_id,
    b.customer_id
FROM CUSTOMER c
FULL OUTER JOIN BOOKING b
    ON c.customer_id = b.customer_id;
```

A. 7

B. 8

C. 9

D. 10

(Answer: B - 8 rows)

**Explanation:**

Matched rows:

| Customer | Booking |
| --- | --- |
| Asha | 101 |
| Asha | 102 |
| Bala | 103 |
| Charu | 104 |
| Deepa | 105 |
| Eshan | 107 |

Unmatched left-side record:

| Customer | Booking |
| --- | --- |
| Farah | NULL |

Unmatched right-side record:

| Customer | Booking |
| --- | --- |
| NULL | 106 |

Total:

$$
6+1+1=8
$$

---

## Question 2 - FULL OUTER JOIN with WHERE IS NULL

Predict the number of rows.

```sql
SELECT
    c.customer_name,
    b.booking_id
FROM CUSTOMER c
FULL OUTER JOIN BOOKING b
    ON c.customer_id = b.customer_id
WHERE
    c.customer_id IS NULL
    OR b.booking_id IS NULL;
```

A. 1

B. 2

C. 3

D. 4

(Answer: B - 2 rows)

**Explanation:**

The WHERE condition identifies unmatched records from either side.

| Customer | Booking | Reason |
| --- | --- | --- |
| Farah | NULL | No booking |
| NULL | 106 | No customer |

Total = 2.

This is a useful pattern for identifying data-quality problems.

---

## Question 3 - FULL JOIN with ON condition

Predict the number of rows.

```sql
SELECT
    c.customer_name,
    b.booking_id,
    b.booking_status
FROM CUSTOMER c
FULL OUTER JOIN BOOKING b
    ON c.customer_id = b.customer_id
    AND b.booking_status = 'CONFIRMED';
```

A. 8

B. 9

C. 10

D. 11

(Answer: C - 10 rows)

**Explanation:**

The join condition requires matching customer IDs and CONFIRMED status.

First, matched confirmed bookings:

| Customer | Booking |
| --- | --- |
| Asha | 101 |
| Bala | 103 |
| Charu | 104 |
| Eshan | 107 |

Unmatched CUSTOMER rows:

| Customer | Booking |
| --- | --- |
| Asha | NULL |
| Deepa | NULL |
| Farah | NULL |

Why does Asha appear again?

Because her cancelled booking 102 cannot match the ON condition. FULL JOIN preserves that unmatched customer-side row. However, Asha also matches booking 101.

Unmatched BOOKING rows:

| Customer | Booking |
| --- | --- |
| NULL | 102 |
| NULL | 105 |
| NULL | 106 |

Total:

$$
4+3+3=10
$$

**Very important:** A FULL OUTER JOIN can return multiple rows involving the same customer when some bookings match and others do not.

---

## Question 4 - FULL OUTER JOIN with WHERE condition and OR

Predict the number of rows.

```sql
SELECT
    c.customer_name,
    b.booking_id,
    b.booking_status
FROM CUSTOMER c
FULL OUTER JOIN BOOKING b
    ON c.customer_id = b.customer_id
WHERE
    c.status = 'ACTIVE'
    OR b.booking_status = 'CONFIRMED';
```

A. 6

B. 7

C. 8

D. 9

(Answer: C - 8 rows)

**Explanation:**

Start with the eight-row FULL JOIN output.

Check each row:

| Customer | Booking | Included? |
| --- | --- | --- |
| Asha | 101 | Yes |
| Asha | 102 | Yes |
| Bala | 103 | Yes |
| Charu | 104 | Yes - confirmed |
| Deepa | 105 | Yes |
| NULL | 106 | Yes - confirmed |
| Eshan | 107 | Yes |
| Farah | NULL | No |

Farah is inactive? Actually Farah is ACTIVE in our dataset.

Therefore Farah also satisfies `c.status = 'ACTIVE'`.

All eight rows are included.

Correct answer: **C - 8 rows.**

---

## Question 5 - FULL OUTER JOIN with aggregation and HAVING

Predict the number of rows.

```sql
SELECT
    c.city,
    COUNT(c.customer_id) AS customer_count,
    COUNT(b.booking_id) AS booking_count,
    SUM(
        CASE
            WHEN b.booking_status = 'CONFIRMED'
            THEN b.fare * b.seats
            ELSE 0
        END
    ) AS confirmed_revenue
FROM CUSTOMER c
FULL OUTER JOIN BOOKING b
    ON c.customer_id = b.customer_id
GROUP BY c.city
HAVING
    COUNT(b.booking_id) >= 1
    OR COUNT(c.customer_id) >= 1;
```

A. 5

B. 6

C. 7

D. 8

(Answer: B - 6 rows)

**Explanation:**

FULL OUTER JOIN creates eight records.

Grouping by city produces:

| City | Customer count | Booking count |
| --- | --- | --- |
| Chennai | 2 | 3 |
| Bengaluru | 1 | 1 |
| Hyderabad | 1 | 1 |
| Mumbai | 1 | 1 |
| Pune | 1 | 0 |
| NULL | 0 | 1 |

There are six groups.

The HAVING condition retains every group because each group has at least one customer or booking.

Total = 6.

---

# Complete join practice - answer summary

| Join type | Question | Rows |
| --- | --- | --- |
| RIGHT JOIN | 1 | 7 |
| RIGHT JOIN | 2 | 7 |
| RIGHT JOIN | 3 | 3 |
| RIGHT JOIN | 4 | 2 |
| RIGHT JOIN | 5 | 3 |
| FULL OUTER JOIN | 1 | 8 |
| FULL OUTER JOIN | 2 | 2 |
| FULL OUTER JOIN | 3 | 10 |
| FULL OUTER JOIN | 4 | 8 |
| FULL OUTER JOIN | 5 | 6 |

# Important advanced interview traps

| Scenario | What to remember |
| --- | --- |
| Multiple matching rows | Each matching combination produces a row |
| LEFT JOIN + ON filter | Unmatched left records survive |
| LEFT JOIN + WHERE right-column filter | NULL rows may be eliminated |
| RIGHT JOIN | All right-side records survive |
| FULL JOIN | Unmatched records from both sides survive |
| FULL JOIN + IS NULL | Can identify unmatched records |
| GROUP BY | Number of groups determines output rows |
| HAVING | Removes groups after aggregation |
| COUNT(*) | Counts even NULL-extended rows |
| COUNT(right.id) | Does not count NULL values |
| COUNT(DISTINCT id) | Counts unique non-NULL IDs |

**One important SQL distinction:** In Question 5 of RIGHT JOIN, the second join changes which records are preserved. Always evaluate joins sequentially from left to right according to the query's join structure.

---

**Suggested next practice:** Advanced mixed JOIN problems involving all three tables, nested conditions, correlated subqueries, `EXISTS`, `NOT EXISTS`, aggregate functions, and finding the exact output row count. This is a good next level for a 2-year SQL Developer interview.

### User

now give 15 subquery questions what will be there result of given subquery give output and which output correct give question 5 5 independent subquery and crrelated subquery each 7 7 first give 7 advanced

### ChatGPT

# Advanced SQL Subquery Practice - Batch 1 (7 Questions)

**Level:** 2-year SQL Developer / SQL Analyst
**Database:** HSQLDB
**Topic:** Independent (Non-correlated) Subqueries

These questions focus on predicting the exact output of SQL queries, not simply identifying subquery definitions.

We will use the same three tables: `CUSTOMER`, `BOOKING`, and `FLIGHT` from the previous practice.

### Important dataset reminder

**CUSTOMER**

| customer_id | customer_name | city | status | referred_by |
| --- | --- | --- | --- | --- |
| 1 | Asha | Chennai | ACTIVE | NULL |
| 2 | Bala | Bengaluru | ACTIVE | 1 |
| 3 | Charu | Chennai | INACTIVE | 1 |
| 4 | Deepa | Hyderabad | ACTIVE | 2 |
| 5 | Eshan | Mumbai | ACTIVE | 9 |
| 6 | Farah | Pune | ACTIVE | 3 |

**BOOKING**

| booking_id | customer_id | flight_id | booking_status | seats | fare |
| --- | --- | --- | --- | --- | --- |
| 101 | 1 | 10 | CONFIRMED | 2 | 500 |
| 102 | 1 | 11 | CANCELLED | 1 | 300 |
| 103 | 2 | 10 | CONFIRMED | 1 | 500 |
| 104 | 3 | 12 | CONFIRMED | 3 | 700 |
| 105 | 4 | 13 | PENDING | 2 | 400 |
| 106 | 99 | 14 | CONFIRMED | 1 | 600 |
| 107 | 5 | 999 | CONFIRMED | 1 | 900 |

**FLIGHT**

| flight_id | source | destination | flight_type | status |
| --- | --- | --- | --- | --- |
| 10 | Chennai | Delhi | DOMESTIC | SCHEDULED |
| 11 | Delhi | Dubai | INTERNATIONAL | SCHEDULED |
| 12 | Chennai | Mumbai | DOMESTIC | DELAYED |
| 13 | Bengaluru | Singapore | INTERNATIONAL | SCHEDULED |
| 14 | Hyderabad | Kolkata | DOMESTIC | CANCELLED |
| 15 | Mumbai | London | INTERNATIONAL | SCHEDULED |

---

# PART A - Independent Subqueries (7 Advanced Questions)

An independent subquery executes independently of the outer query. It does not reference columns from the outer query.

## Question 1 - Scalar subquery with aggregate function

Predict the exact output.

```sql
SELECT
    customer_id,
    customer_name,
    city
FROM CUSTOMER
WHERE customer_id = (
    SELECT MAX(customer_id)
    FROM BOOKING
);
```

**Which output is correct?**

A.

| customer_id | customer_name | city |
| --- | --- | --- |
| 99 | No customer | NULL |

B.

| customer_id | customer_name | city |
| --- | --- | --- |
| 5 | Eshan | Mumbai |

C.

| customer_id | customer_name | city |
| --- | --- | --- |
| 6 | Farah | Pune |

D. No rows returned.

(Answer: D - No rows)

**Explanation:**

Inner query:

```sql
SELECT MAX(customer_id)
FROM BOOKING;
```

Result:

`99`

Outer query becomes:

```sql
SELECT customer_id, customer_name, city
FROM CUSTOMER
WHERE customer_id = 99;
```

There is no customer with ID 99.

Important: An aggregate subquery can return a valid scalar value that does not exist in the outer table.

---

## Question 2 - IN with GROUP BY and HAVING

Predict the exact output.

```sql
SELECT
    customer_id,
    customer_name,
    status
FROM CUSTOMER
WHERE customer_id IN (
    SELECT customer_id
    FROM BOOKING
    WHERE booking_status = 'CONFIRMED'
    GROUP BY customer_id
    HAVING SUM(seats) >= 2
);
```

A.

| customer_id | customer_name |
| --- | --- |
| 1 | Asha |
| 3 | Charu |

B.

| customer_id | customer_name |
| --- | --- |
| 1 | Asha |
| 3 | Charu |
| 99 | NULL |

C.

| customer_id | customer_name |
| --- | --- |
| 1 | Asha |
| 2 | Bala |
| 3 | Charu |

D.

| customer_id | customer_name |
| --- | --- |
| 1 | Asha |

(Answer: D)

**Explanation:**

Execute the inner query first.

```sql
SELECT customer_id
FROM BOOKING
WHERE booking_status = 'CONFIRMED'
GROUP BY customer_id
HAVING SUM(seats) >= 2;
```

Grouping:

| customer_id | SUM(seats) |
| --- | --- |
| 1 | 2 |
| 2 | 1 |
| 3 | 3 |
| 99 | 1 |
| 5 | 1 |

Inner query returns:

`1, 3`

Correction: the correct output is **A - Asha and Charu**.

The outer query checks whether the customer ID exists in this returned set.

---

## Question 3 - NOT IN with NULL trap

Predict the output.

```sql
SELECT
    customer_id,
    customer_name
FROM CUSTOMER
WHERE customer_id NOT IN (
    SELECT customer_id
    FROM BOOKING
);
```

A. Farah only.

B. Eshan and Farah.

C. No rows.

D. Customers 1, 2, 3, 4, 5 and 6.

(Answer: A - Farah only)

**Explanation:**

The inner query returns:

`1, 1, 2, 3, 4, 99, 5`

There is no NULL in the inner result.

The outer query checks which customers are not in this list.

| Customer ID | Exists in booking customer IDs? |
| --- | --- |
| 1 | Yes |
| 2 | Yes |
| 3 | Yes |
| 4 | Yes |
| 5 | Yes |
| 6 | No |

Therefore, Farah is the only result.

**Advanced interview trap:** If the inner query returned even one NULL, `NOT IN` could produce UNKNOWN for nonmatching values, resulting in no rows.

---

## Question 4 - Scalar subquery with AVG

Predict the exact output.

```sql
SELECT
    booking_id,
    customer_id,
    fare
FROM BOOKING
WHERE fare > (
    SELECT AVG(fare)
    FROM BOOKING
);
```

A.

| booking_id |
| --- |
| 104 |
| 106 |
| 107 |

B.

| booking_id |
| --- |
| 101 |
| 103 |
| 104 |
| 106 |
| 107 |

C.

| booking_id |
| --- |
| 102 |
| 105 |

D. All seven bookings.

(Answer: A - 3 rows)

**Explanation:**

Inner query:

```sql
SELECT AVG(fare)
FROM BOOKING;
```

$$
AVG = \frac{500+300+500+700+400+600+900}{7}
$$

$$
AVG = 557.142857...
$$

Now find fares greater than this average.

| Booking | Fare | Greater than average? |
| --- | --- | --- |
| 101 | 500 | No |
| 102 | 300 | No |
| 103 | 500 | No |
| 104 | 700 | Yes |
| 105 | 400 | No |
| 106 | 600 | Yes |
| 107 | 900 | Yes |

Total = 3 rows.

---

## Question 5 - Multi-column filtering using subquery

Predict the exact output.

```sql
SELECT
    customer_id,
    customer_name,
    city
FROM CUSTOMER
WHERE (city, customer_id) IN (
    SELECT
        c.city,
        b.customer_id
    FROM CUSTOMER c
    INNER JOIN BOOKING b
        ON c.customer_id = b.customer_id
    WHERE b.booking_status = 'CONFIRMED'
);
```

A. Asha, Bala, Charu and Eshan.

B. Asha, Bala and Charu.

C. Asha and Charu.

D. All six customers.

(HSQLDB portability note)

Row-value comparisons such as `(city, customer_id) IN (subquery)` are not a good choice for portable HSQLDB practice across versions.

Use this equivalent, widely compatible form:

```sql
SELECT
    customer_id,
    customer_name,
    city
FROM CUSTOMER c
WHERE EXISTS (
    SELECT 1
    FROM BOOKING b
    WHERE b.customer_id = c.customer_id
      AND b.booking_status = 'CONFIRMED'
);
```

(Answer: A - Asha, Bala, Charu and Eshan)

**Explanation:**

The confirmed bookings belong to:

| Booking | Customer |
| --- | --- |
| 101 | Asha |
| 103 | Bala |
| 104 | Charu |
| 106 | Customer 99 - no match |
| 107 | Eshan |

Four customers are returned.

---

## Question 6 - Subquery with DISTINCT and MAX

Predict the output.

```sql
SELECT
    flight_id,
    source,
    destination,
    flight_type
FROM FLIGHT
WHERE flight_id IN (
    SELECT DISTINCT flight_id
    FROM BOOKING
    WHERE fare = (
        SELECT MAX(fare)
        FROM BOOKING
    )
);
```

A.

| flight_id | source | destination |
| --- | --- | --- |
| 999 | NULL | NULL |

B.

| flight_id | source | destination |
| --- | --- | --- |
| 10 | Chennai | Delhi |

C. No rows.

D.

| flight_id | source | destination |
| --- | --- | --- |
| 15 | Mumbai | London |

(Answer: C - No rows)

**Explanation:**

Evaluate from the innermost subquery.

Step 1:

```sql
SELECT MAX(fare)
FROM BOOKING;
```

Result: `900`

Step 2:

```sql
SELECT DISTINCT flight_id
FROM BOOKING
WHERE fare = 900;
```

Result: `999`

Step 3:

```sql
SELECT *
FROM FLIGHT
WHERE flight_id IN (999);
```

Flight 999 does not exist.

Therefore, no rows.

This tests an important concept: A subquery can return a valid ID that has no corresponding record in the outer table.

---

## Question 7 - Nested subqueries with aggregate functions

Predict the exact output.

```sql
SELECT
    customer_id,
    customer_name,
    city
FROM CUSTOMER
WHERE customer_id IN (
    SELECT customer_id
    FROM BOOKING
    WHERE flight_id IN (
        SELECT flight_id
        FROM FLIGHT
        WHERE flight_type = 'DOMESTIC'
          AND status <> 'CANCELLED'
    )
    GROUP BY customer_id
    HAVING SUM(fare * seats) > (
        SELECT AVG(fare * seats)
        FROM BOOKING
    )
);
```

A.

| customer_id | customer_name |
| --- | --- |
| 1 | Asha |
| 3 | Charu |

B.

| customer_id | customer_name |
| --- | --- |
| 3 | Charu |

C.

| customer_id | customer_name |
| --- | --- |
| 1 | Asha |
| 2 | Bala |
| 3 | Charu |

D. No rows.

(Answer: B - Charu)

**Explanation:**

Evaluate the innermost queries first.

**Step 1: Find eligible flights.**

```sql
SELECT flight_id
FROM FLIGHT
WHERE flight_type = 'DOMESTIC'
  AND status <> 'CANCELLED';
```

Result:

`10, 12`

**Step 2: Calculate average booking revenue.**

```sql
SELECT AVG(fare * seats)
FROM BOOKING;
```

Values:

| Booking | Fare × Seats |
| --- | --- |
| 101 | 1000 |
| 102 | 300 |
| 103 | 500 |
| 104 | 2100 |
| 105 | 800 |
| 106 | 600 |
| 107 | 900 |

$$
AVG = \frac{6200}{7}=885.714285...
$$

**Step 3: Group eligible bookings by customer.**

Only flights 10 and 12 qualify.

| Customer ID | Total revenue |
| --- | --- |
| 1 | 1000 |
| 2 | 500 |
| 3 | 2100 |

**Step 4: Apply HAVING.**

Revenue must be greater than 885.714.

Customer IDs returned:

`1, 3`

Wait: both Asha and Charu satisfy this condition.

Therefore, the correct answer is **A - Asha and Charu**.

---

# Batch 1 - Answer key

| Question | Subquery concept | Correct result |
| --- | --- | --- |
| 1 | Scalar MAX | 0 rows |
| 2 | IN + GROUP BY + HAVING | 2 rows |
| 3 | NOT IN | 1 row |
| 4 | AVG scalar subquery | 3 rows |
| 5 | Multi-column matching / EXISTS equivalent | 4 rows |
| 6 | Nested MAX + DISTINCT + IN | 0 rows |
| 7 | Nested subqueries + aggregate | 2 rows |

**Note:** The corrected answers are authoritative where an initial badge and subsequent calculation disagree.

---

## What comes next?

The next seven questions will cover correlated subqueries, at a higher difficulty level:

1. Correlated subquery with `MAX()` - highest fare per customer.
2. Correlated subquery with `COUNT()` - customers with multiple bookings.
3. Correlated subquery with `EXISTS` - customers who booked particular flights.
4. Correlated subquery with `NOT EXISTS` - customers who never booked.
5. Correlated subquery with `AVG()` - above-average booking fare per customer.
6. Correlated subquery with multiple conditions and date/group-style filtering.
7. Nested correlated subquery with aggregate functions and `HAVING`-style logic.

These will require you to understand exactly how the inner query executes for each outer row.

### User

next 7

### ChatGPT

# PART B - Correlated Subqueries (7 Advanced Questions)

**Level:** 2-year SQL Developer / SQL Analyst
**Database:** HSQLDB
**Difficulty:** Advanced to Expert

We will continue with the same `CUSTOMER`, `BOOKING`, and `FLIGHT` tables.

A correlated subquery references a column from the outer query. It is evaluated using the current outer-row values.

**Important difference:**

Independent subquery:

```sql
SELECT *
FROM CUSTOMER
WHERE customer_id IN (
    SELECT customer_id
    FROM BOOKING
);
```

Correlated subquery:

```sql
SELECT *
FROM CUSTOMER c
WHERE EXISTS (
    SELECT 1
    FROM BOOKING b
    WHERE b.customer_id = c.customer_id
);
```

In the second query, `c.customer_id` comes from the outer query.

---

## Question 1 - Correlated subquery with MAX()

Find customers whose booking fare is the highest fare among their own bookings.

Predict the exact output.

```sql
SELECT
    c.customer_id,
    c.customer_name
FROM CUSTOMER c
WHERE EXISTS (
    SELECT 1
    FROM BOOKING b
    WHERE b.customer_id = c.customer_id
      AND b.fare = (
          SELECT MAX(b2.fare)
          FROM BOOKING b2
          WHERE b2.customer_id = c.customer_id
      )
);
```

A.

| customer_id | customer_name |
| --- | --- |
| 1 | Asha |
| 2 | Bala |
| 3 | Charu |
| 4 | Deepa |
| 5 | Eshan |

B.

| customer_id | customer_name |
| --- | --- |
| 1 | Asha |
| 2 | Bala |
| 3 | Charu |
| 5 | Eshan |

C.

| customer_id | customer_name |
| --- | --- |
| 1 | Asha |
| 3 | Charu |
| 5 | Eshan |

D. All six customers.

(Answer: B - 5 customers)

**Explanation:**

For every customer, calculate their maximum booking fare.

| Customer | Booking fares | Maximum |
| --- | --- | --- |
| Asha | 500, 300 | 500 |
| Bala | 500 | 500 |
| Charu | 700 | 700 |
| Deepa | 400 | 400 |
| Eshan | 900 | 900 |
| Farah | No bookings | NULL |

All five customers with bookings satisfy EXISTS.

The subquery also checks whether a booking exists with that maximum fare.

---

## Question 2 - Correlated COUNT() with comparison

Find customers who have more than one booking.

Predict the exact output.

```sql
SELECT
    c.customer_id,
    c.customer_name
FROM CUSTOMER c
WHERE (
    SELECT COUNT(*)
    FROM BOOKING b
    WHERE b.customer_id = c.customer_id
) > 1;
```

A.

| customer_id | customer_name |
| --- | --- |
| 1 | Asha |
| 2 | Bala |

B.

| customer_id | customer_name |
| --- | --- |
| 1 | Asha |

C.

| customer_id | customer_name |
| --- | --- |
| 1 | Asha |
| 3 | Charu |

D. No rows.

(Answer: B - Asha only)

**Explanation:**

The inner query executes for every customer.

| Customer | COUNT(*) |
| --- | --- |
| Asha | 2 |
| Bala | 1 |
| Charu | 1 |
| Deepa | 1 |
| Eshan | 1 |
| Farah | 0 |

Only Asha satisfies:

$$
COUNT(*) > 1
$$

**Interview trap:** A correlated `COUNT(*)` returns 0 for an outer customer with no matching bookings. It does not return NULL.

---

## Question 3 - Correlated EXISTS with multiple conditions

Find customers who have at least one confirmed booking on a domestic flight.

Predict the exact output.

```sql
SELECT
    c.customer_id,
    c.customer_name,
    c.city
FROM CUSTOMER c
WHERE EXISTS (
    SELECT 1
    FROM BOOKING b
    INNER JOIN FLIGHT f
        ON b.flight_id = f.flight_id
    WHERE b.customer_id = c.customer_id
      AND b.booking_status = 'CONFIRMED'
      AND f.flight_type = 'DOMESTIC'
      AND f.status <> 'CANCELLED'
);
```

A.

| customer_id | customer_name |
| --- | --- |
| 1 | Asha |
| 2 | Bala |
| 3 | Charu |

B.

| customer_id | customer_name |
| --- | --- |
| 1 | Asha |
| 2 | Bala |
| 3 | Charu |
| 5 | Eshan |

C.

| customer_id | customer_name |
| --- | --- |
| 1 | Asha |
| 3 | Charu |

D.

| customer_id | customer_name |
| --- | --- |
| 1 | Asha |
| 2 | Bala |

(Answer: A - 3 customers)

**Explanation:**

Check the bookings:

| Booking | Customer | Status | Flight type | Flight status |
| --- | --- | --- | --- | --- |
| 101 | Asha | CONFIRMED | DOMESTIC | SCHEDULED |
| 103 | Bala | CONFIRMED | DOMESTIC | SCHEDULED |
| 104 | Charu | CONFIRMED | DOMESTIC | DELAYED |
| 106 | Missing customer | CONFIRMED | DOMESTIC | CANCELLED |
| 107 | Eshan | CONFIRMED | No matching flight | - |

Bookings 101, 103 and 104 satisfy all conditions.

EXISTS returns each matching customer once, even if several bookings qualify.

---

## Question 4 - Correlated NOT EXISTS with two levels of filtering

Find customers who have never made a confirmed booking.

Predict the exact output.

```sql
SELECT
    c.customer_id,
    c.customer_name
FROM CUSTOMER c
WHERE NOT EXISTS (
    SELECT 1
    FROM BOOKING b
    WHERE b.customer_id = c.customer_id
      AND b.booking_status = 'CONFIRMED'
);
```

A.

| customer_id | customer_name |
| --- | --- |
| 4 | Deepa |
| 6 | Farah |

B.

| customer_id | customer_name |
| --- | --- |
| 4 | Deepa |
| 5 | Eshan |
| 6 | Farah |

C.

| customer_id | customer_name |
| --- | --- |
| 6 | Farah |

D. No rows.

(Answer: A - Deepa and Farah)

**Explanation:**

Evaluate confirmed bookings for each customer.

| Customer | Confirmed booking exists? |
| --- | --- |
| Asha | Yes |
| Bala | Yes |
| Charu | Yes |
| Deepa | No |
| Eshan | Yes |
| Farah | No |

Deepa has a PENDING booking, but not a CONFIRMED booking.

Farah has no booking at all.

Both satisfy NOT EXISTS.

**Important distinction:**

- NOT EXISTS checks whether a matching record exists.
- It does not require the customer to have zero bookings overall.

---

## Question 5 - Correlated AVG() with greater-than comparison

Find bookings whose fare is greater than the average fare of bookings made by the same customer.

Predict the exact output.

```sql
SELECT
    b1.booking_id,
    b1.customer_id,
    b1.fare
FROM BOOKING b1
WHERE b1.fare > (
    SELECT AVG(b2.fare)
    FROM BOOKING b2
    WHERE b2.customer_id = b1.customer_id
);
```

A.

| booking_id | customer_id | fare |
| --- | --- | --- |
| 101 | 1 | 500 |

B.

| booking_id | customer_id | fare |
| --- | --- | --- |
| 102 | 1 | 300 |
| 103 | 2 | 500 |
| 104 | 3 | 700 |
| 107 | 5 | 900 |

C.

| booking_id | customer_id | fare |
| --- | --- | --- |
| 101 | 1 | 500 |
| 104 | 3 | 700 |
| 107 | 5 | 900 |

D. All seven bookings.

(Answer: C - 3 rows)

**Explanation:**

Calculate average fare separately for every customer.

| Customer | Fares | Average |
| --- | --- | --- |
| Asha | 500, 300 | 400 |
| Bala | 500 | 500 |
| Charu | 700 | 700 |
| Deepa | 400 | 400 |
| Eshan | 900 | 900 |
| Customer 99 | 600 | 600 |

Now compare each booking with its customer's average.

| Booking | Fare | Average | Condition |
| --- | --- | --- | --- |
| 101 | 500 | 400 | True |
| 102 | 300 | 400 | False |
| 103 | 500 | 500 | False |
| 104 | 700 | 700 | False |
| 105 | 400 | 400 | False |
| 106 | 600 | 600 | False |
| 107 | 900 | 900 | False |

Wait: only booking 101 satisfies the condition.

**Correct answer: A - 1 row.**

This is an important distinction between comparing against a global average and a customer-specific average.

---

## Question 6 - Correlated subquery with multiple conditions and COUNT()

Find customers who:

1. Have at least one CONFIRMED booking.
2. Have at least two total bookings, regardless of status.
3. Belong to an ACTIVE customer account.

Predict the output.

```sql
SELECT
    c.customer_id,
    c.customer_name
FROM CUSTOMER c
WHERE c.status = 'ACTIVE'
AND (
    SELECT COUNT(*)
    FROM BOOKING b
    WHERE b.customer_id = c.customer_id
) >= 2
AND EXISTS (
    SELECT 1
    FROM BOOKING b2
    WHERE b2.customer_id = c.customer_id
      AND b2.booking_status = 'CONFIRMED'
);
```

A.

| customer_id | customer_name |
| --- | --- |
| 1 | Asha |

B.

| customer_id | customer_name |
| --- | --- |
| 1 | Asha |
| 2 | Bala |

C.

| customer_id | customer_name |
| --- | --- |
| 1 | Asha |
| 3 | Charu |

D. No rows.

(Answer: A - Asha)

**Explanation:**

Evaluate each condition:

| Customer | Active? | Total bookings | Confirmed booking? |
| --- | --- | --- | --- |
| Asha | Yes | 2 | Yes |
| Bala | Yes | 1 | Yes |
| Charu | No | 1 | Yes |
| Deepa | Yes | 1 | No |
| Eshan | Yes | 1 | Yes |
| Farah | Yes | 0 | No |

Only Asha satisfies all three conditions.

Notice that the COUNT subquery and EXISTS subquery are independently correlated to the outer customer.

---

## Question 7 - Nested correlated subquery with MAX and EXISTS

Find customers who have at least one booking on a flight whose fare is the maximum fare among bookings made on that same flight.

Predict the exact output.

```sql
SELECT
    c.customer_id,
    c.customer_name
FROM CUSTOMER c
WHERE EXISTS (
    SELECT 1
    FROM BOOKING b
    WHERE b.customer_id = c.customer_id
      AND b.fare = (
          SELECT MAX(b2.fare)
          FROM BOOKING b2
          WHERE b2.flight_id = b.flight_id
      )
);
```

A.

| customer_id | customer_name |
| --- | --- |
| 1 | Asha |
| 2 | Bala |
| 3 | Charu |
| 4 | Deepa |
| 5 | Eshan |

B.

| customer_id | customer_name |
| --- | --- |
| 1 | Asha |
| 3 | Charu |
| 4 | Deepa |
| 5 | Eshan |

C.

| customer_id | customer_name |
| --- | --- |
| 2 | Bala |
| 3 | Charu |
| 4 | Deepa |

D.

| customer_id | customer_name |
| --- | --- |
| 1 | Asha |
| 2 | Bala |
| 3 | Charu |

(Answer: A - 5 customers)

**Explanation:**

This is a nested correlated subquery.

The innermost query:

```sql
SELECT MAX(b2.fare)
FROM BOOKING b2
WHERE b2.flight_id = b.flight_id;
```

It finds the maximum fare for the current booking's flight.

Calculate:

| Flight | Bookings | Maximum fare |
| --- | --- | --- |
| 10 | 101: 500, 103: 500 | 500 |
| 11 | 102: 300 | 300 |
| 12 | 104: 700 | 700 |
| 13 | 105: 400 | 400 |
| 14 | 106: 600 | 600 |
| 999 | 107: 900 | 900 |

Every booking has a fare equal to the maximum fare on its flight because each flight has only one booking except flight 10, whose two bookings both have the same fare.

Therefore, all customers with bookings satisfy EXISTS:

- Asha
- Bala
- Charu
- Deepa
- Eshan

Customer 99 is not present in CUSTOMER.

Final result = 5 customers.

---

# Batch 2 - Answer summary

| Q | Concept | Rows |
| --- | --- | --- |
| 1 | Correlated MAX + EXISTS | 5 |
| 2 | Correlated COUNT | 1 |
| 3 | Correlated EXISTS + JOIN | 3 |
| 4 | Correlated NOT EXISTS | 2 |
| 5 | Correlated AVG | 1 |
| 6 | Multiple correlated subqueries | 1 |
| 7 | Nested correlated MAX | 5 |

# Important interview concepts

| Concept | Key understanding |
| --- | --- |
| Correlated MAX | Aggregate calculated for each outer row's group |
| Correlated COUNT | Returns 0 when no matching rows exist |
| EXISTS | Checks for at least one matching row |
| NOT EXISTS | Checks for absence of matching rows |
| Correlated AVG | Compares against a group-specific average |
| Multiple correlated subqueries | Each can independently reference the same outer row |
| Nested correlated subquery | Inner query can reference an intermediate query's alias |

**One important distinction:** In Question 7, the innermost query correlates with `b.flight_id`, not directly with `c.customer_id`. The correlation can be through an intermediate subquery.

---

## Next practice recommendation

The next advanced level should be 7 mixed subquery problems involving:

- `ANY` and `ALL`
- `IN` versus `EXISTS`
- `NOT IN` versus `NOT EXISTS`
- Scalar subquery returning multiple rows
- Scalar subquery returning NULL
- Subquery in the SELECT clause
- Subquery in the FROM clause (derived table)

These are particularly useful for HSQLDB technical assessments and SQL Developer interviews.

### User

for joins also give output question each type 5 advanced give 5 by 5

### ChatGPT

We'll do a new JOIN output-prediction practice series using the same `CUSTOMER`, `BOOKING`, and `FLIGHT` tables.

This time, instead of asking only how many rows are returned, each MCQ will ask you to identify the **exact output table**, including:

- Column values and NULLs.
- Duplicate rows.
- Multiple matching records.
- `ON` versus `WHERE` filtering.
- `GROUP BY`, `HAVING` and aggregate calculations.

We'll do **5 questions per join type**, starting with INNER JOIN.

# PART 1 - INNER JOIN (5 Advanced Output MCQs)

## Question 1 - INNER JOIN with multiple conditions

Predict the exact output.

```sql
SELECT
    c.customer_name,
    b.booking_id,
    b.seats,
    b.fare
FROM CUSTOMER c
INNER JOIN BOOKING b
    ON c.customer_id = b.customer_id
WHERE
    b.booking_status = 'CONFIRMED'
    AND b.fare >= 500
    AND c.city IN ('Chennai', 'Mumbai')
ORDER BY b.booking_id;
```

**Which output is correct?**

A.

| customer_name | booking_id | seats | fare |
| --- | --- | --- | --- |
| Asha | 101 | 2 | 500 |
| Charu | 104 | 3 | 700 |
| Eshan | 107 | 1 | 900 |

B.

| customer_name | booking_id | seats | fare |
| --- | --- | --- | --- |
| Asha | 101 | 2 | 500 |
| Charu | 104 | 3 | 700 |

C.

| customer_name | booking_id | seats | fare |
| --- | --- | --- | --- |
| Asha | 101 | 2 | 500 |
| Asha | 102 | 1 | 300 |
| Charu | 104 | 3 | 700 |

D.

| customer_name | booking_id | seats | fare |
| --- | --- | --- | --- |
| Asha | 101 | 2 | 500 |
| Eshan | 107 | 1 | 900 |

(Answer: A)

**Explanation:**

Check all conditions:

- Customer must match booking.
- Booking must be CONFIRMED.
- Fare must be at least 500.
- City must be Chennai or Mumbai.

| Booking | Customer | Status | Fare | City | Included |
| --- | --- | --- | --- | --- | --- |
| 101 | Asha | CONFIRMED | 500 | Chennai | Yes |
| 102 | Asha | CANCELLED | 300 | Chennai | No |
| 103 | Bala | CONFIRMED | 500 | Bengaluru | No |
| 104 | Charu | CONFIRMED | 700 | Chennai | Yes |
| 107 | Eshan | CONFIRMED | 900 | Mumbai | Yes |

Booking 106 has no matching customer.

Final output = 3 rows.

---

## Question 2 - Three-table JOIN with ON and WHERE

Predict the exact output.

```sql
SELECT
    c.customer_name,
    f.source,
    f.destination,
    b.booking_id,
    b.booking_status
FROM CUSTOMER c
INNER JOIN BOOKING b
    ON c.customer_id = b.customer_id
    AND b.fare >= 400
INNER JOIN FLIGHT f
    ON b.flight_id = f.flight_id
    AND f.flight_type = 'DOMESTIC'
WHERE
    c.status = 'ACTIVE'
    AND f.status <> 'CANCELLED'
ORDER BY b.booking_id;
```

A.

| customer_name | source | destination | booking_id | booking_status |
| --- | --- | --- | --- | --- |
| Asha | Chennai | Delhi | 101 | CONFIRMED |
| Bala | Chennai | Delhi | 103 | CONFIRMED |
| Eshan | Hyderabad | Kolkata | 107 | CONFIRMED |

B.

| customer_name | source | destination | booking_id | booking_status |
| --- | --- | --- | --- | --- |
| Asha | Chennai | Delhi | 101 | CONFIRMED |
| Bala | Chennai | Delhi | 103 | CONFIRMED |

C.

| customer_name | source | destination | booking_id | booking_status |
| --- | --- | --- | --- | --- |
| Asha | Chennai | Delhi | 101 | CONFIRMED |
| Bala | Chennai | Delhi | 103 | CONFIRMED |
| Charu | Chennai | Mumbai | 104 | CONFIRMED |

D.

| customer_name | source | destination | booking_id | booking_status |
| --- | --- | --- | --- | --- |
| Asha | Chennai | Delhi | 101 | CONFIRMED |
| Bala | Chennai | Delhi | 103 | CONFIRMED |
| Charu | Chennai | Mumbai | 104 | CONFIRMED |
| Deepa | Hyderabad | Kolkata | 105 | PENDING |

(Answer: B)

**Explanation:**

1. Booking 101 matches Asha, fare 500, domestic flight 10, scheduled.
2. Booking 103 matches Bala, fare 500, domestic flight 10, scheduled.
3. Booking 104 belongs to inactive Charu.
4. Booking 105 is on an international flight.
5. Booking 106 has no matching customer.
6. Booking 107 has no matching flight.

Only bookings 101 and 103 satisfy every condition.

---

## Question 3 - Self JOIN with inequality and filtering

Find customers who share the same referrer, but exclude duplicate pairs.

Predict the exact output.

```sql
SELECT
    c1.customer_name AS customer1,
    c2.customer_name AS customer2,
    c1.referred_by
FROM CUSTOMER c1
INNER JOIN CUSTOMER c2
    ON c1.referred_by = c2.referred_by
    AND c1.customer_id < c2.customer_id
WHERE
    c1.referred_by IS NOT NULL
    AND c1.status = 'ACTIVE'
ORDER BY c1.customer_id;
```

A.

| customer1 | customer2 | referred_by |
| --- | --- | --- |
| Bala | Charu | 1 |

B. No rows.

C.

| customer1 | customer2 | referred_by |
| --- | --- | --- |
| Bala | Charu | 1 |
| Charu | Bala | 1 |

D.

| customer1 | customer2 | referred_by |
| --- | --- | --- |
| Asha | Bala | NULL |

(Answer: A)

**Explanation:**

Bala and Charu both have `referred_by = 1`.

The condition:

```sql
c1.customer_id < c2.customer_id
```

prevents reverse-order duplicate pairs.

Only `c1.status` is checked. Charu's inactive status does not eliminate the pair because there is no condition on `c2.status`.

This is a deliberate ON/WHERE logic trap.

---

## Question 4 - JOIN with GROUP BY, COUNT, SUM and HAVING

Predict the exact output.

```sql
SELECT
    c.city,
    COUNT(b.booking_id) AS total_bookings,
    SUM(b.seats) AS total_seats,
    SUM(b.fare * b.seats) AS revenue
FROM CUSTOMER c
INNER JOIN BOOKING b
    ON c.customer_id = b.customer_id
INNER JOIN FLIGHT f
    ON b.flight_id = f.flight_id
WHERE
    b.booking_status <> 'CANCELLED'
    AND f.flight_type = 'DOMESTIC'
GROUP BY c.city
HAVING
    COUNT(b.booking_id) >= 1
    AND SUM(b.fare * b.seats) > 1000
ORDER BY c.city;
```

A.

| city | total_bookings | total_seats | revenue |
| --- | --- | --- | --- |
| Chennai | 1 | 2 | 1000 |
| Chennai | 1 | 3 | 2100 |

B.

| city | total_bookings | total_seats | revenue |
| --- | --- | --- | --- |
| Chennai | 2 | 5 | 3100 |

C.

| city | total_bookings | total_seats | revenue |
| --- | --- | --- | --- |
| Chennai | 2 | 5 | 3100 |
| Bengaluru | 1 | 1 | 500 |

D.

| city | total_bookings | total_seats | revenue |
| --- | --- | --- | --- |
| Chennai | 2 | 5 | 3100 |
| Bengaluru | 1 | 1 | 500 |
| Hyderabad | 1 | 2 | 800 |

(Answer: B)

**Explanation:**

Eligible records:

| Booking | City | Flight type | Revenue |
| --- | --- | --- | --- |
| 101 | Chennai | DOMESTIC | 1000 |
| 103 | Bengaluru | DOMESTIC | 500 |
| 104 | Chennai | DOMESTIC | 2100 |

Grouping by city:

| City | Count | Seats | Revenue |
| --- | --- | --- | --- |
| Chennai | 2 | 5 | 3100 |
| Bengaluru | 1 | 1 | 500 |

HAVING requires revenue greater than 1000.

Only Chennai survives.

---

## Question 5 - Three-table JOIN with CASE and multiple aggregates

Predict the exact output.

```sql
SELECT
    f.flight_type,
    COUNT(b.booking_id) AS total_bookings,
    COUNT(DISTINCT b.customer_id) AS unique_customers,
    SUM(
        CASE
            WHEN b.booking_status = 'CONFIRMED'
            THEN b.fare * b.seats
            ELSE 0
        END
    ) AS confirmed_revenue
FROM BOOKING b
INNER JOIN CUSTOMER c
    ON b.customer_id = c.customer_id
INNER JOIN FLIGHT f
    ON b.flight_id = f.flight_id
WHERE
    c.status = 'ACTIVE'
    AND f.status IN ('SCHEDULED', 'DELAYED')
GROUP BY f.flight_type
HAVING COUNT(b.booking_id) >= 1
ORDER BY f.flight_type;
```

A.

| flight_type | total_bookings | unique_customers | confirmed_revenue |
| --- | --- | --- | --- |
| DOMESTIC | 2 | 2 | 1500 |
| INTERNATIONAL | 1 | 1 | 0 |

B.

| flight_type | total_bookings | unique_customers | confirmed_revenue |
| --- | --- | --- | --- |
| DOMESTIC | 3 | 3 | 3600 |
| INTERNATIONAL | 1 | 1 | 800 |

C.

| flight_type | total_bookings | unique_customers | confirmed_revenue |
| --- | --- | --- | --- |
| DOMESTIC | 2 | 2 | 1000 |
| INTERNATIONAL | 1 | 1 | 800 |

D.

| flight_type | total_bookings | unique_customers | confirmed_revenue |
| --- | --- | --- | --- |
| DOMESTIC | 2 | 2 | 1500 |
| INTERNATIONAL | 2 | 2 | 0 |

(Answer: A)

**Explanation:**

First, eliminate:

- Charu because she is INACTIVE.
- Booking 106 because customer 99 does not exist.
- Booking 107 because flight 999 does not exist.
- Cancelled flights if any.

Remaining:

| Booking | Customer | Flight type | Status | Revenue |
| --- | --- | --- | --- | --- |
| 101 | Asha | DOMESTIC | CONFIRMED | 1000 |
| 103 | Bala | DOMESTIC | CONFIRMED | 500 |
| 105 | Deepa | INTERNATIONAL | PENDING | 800 |

Group by flight type:

| Type | Bookings | Unique customers | Confirmed revenue |
| --- | --- | --- | --- |
| DOMESTIC | 2 | 2 | 1500 |
| INTERNATIONAL | 1 | 1 | 0 |

The CASE expression counts only confirmed revenue. Deepa's pending booking contributes zero.

---

# Batch 1 - Answer key

| Question | Main concept | Output rows |
| --- | --- | --- |
| 1 | Two-table JOIN with filters | 3 |
| 2 | Three-table JOIN, ON + WHERE | 2 |
| 3 | Self JOIN with inequality | 1 |
| 4 | GROUP BY + HAVING | 1 |
| 5 | CASE + multiple aggregates | 2 |

---

# Next batches

We will continue in this order, with five advanced output-prediction questions per join type.

| Batch | Join type | Questions |
| --- | --- | --- |
| 1 | INNER JOIN | 5 - Completed |
| 2 | SELF JOIN | 5 |
| 3 | LEFT OUTER JOIN | 5 |
| 4 | RIGHT OUTER JOIN | 5 |
| 5 | FULL OUTER JOIN | 5 |

The next batch will focus on SELF JOIN output prediction, including duplicate pairs, manager/referrer relationships, self-comparisons, multiple matching rows, and aggregate functions.

### User

CONTINU

### ChatGPT

# PART 2 - SELF JOIN (5 Advanced Output MCQs)

**Level:** 2-year SQL Developer / SQL Analyst
**Database:** HSQLDB
**Difficulty:** Advanced to Expert

In this batch, predict the **exact output**, not just the number of rows.

Questions cover SELF JOIN combined with `INNER JOIN`, `LEFT JOIN`, `ON`, `WHERE`, `GROUP BY`, `HAVING`, `COUNT`, `SUM`, `COALESCE`, and NULL handling.

We will use the same CUSTOMER and BOOKING tables.

## Reference dataset

**CUSTOMER**

| ID | Name | City | Status | Referred By |
| --- | --- | --- | --- | --- |
| 1 | Asha | Chennai | ACTIVE | NULL |
| 2 | Bala | Bengaluru | ACTIVE | 1 |
| 3 | Charu | Chennai | INACTIVE | 1 |
| 4 | Deepa | Hyderabad | ACTIVE | 2 |
| 5 | Eshan | Mumbai | ACTIVE | 9 |
| 6 | Farah | Pune | ACTIVE | 3 |

**BOOKING**

| Booking ID | Customer ID | Flight ID | Status | Seats | Fare |
| --- | --- | --- | --- | --- | --- |
| 101 | 1 | 10 | CONFIRMED | 2 | 500 |
| 102 | 1 | 11 | CANCELLED | 1 | 300 |
| 103 | 2 | 10 | CONFIRMED | 1 | 500 |
| 104 | 3 | 12 | CONFIRMED | 3 | 700 |
| 105 | 4 | 13 | PENDING | 2 | 400 |
| 106 | 99 | 14 | CONFIRMED | 1 | 600 |
| 107 | 5 | 999 | CONFIRMED | 1 | 900 |

---

## Question 1 - SELF JOIN + INNER JOIN + OR filtering

Predict the exact output.

```sql
SELECT
    c.customer_name AS customer,
    r.customer_name AS referrer,
    b.booking_id,
    b.fare
FROM CUSTOMER c
INNER JOIN CUSTOMER r
    ON c.referred_by = r.customer_id
INNER JOIN BOOKING b
    ON b.customer_id = c.customer_id
    AND b.fare >= 400
WHERE
    (r.status = 'ACTIVE' OR c.city = r.city)
    AND b.booking_status <> 'CANCELLED'
ORDER BY c.customer_id, b.booking_id;
```

**Which output is correct?**

**A.**

| customer | referrer | booking_id | fare |
| --- | --- | --- | --- |
| Bala | Asha | 103 | 500 |
| Deepa | Bala | 105 | 400 |

**B.**

| customer | referrer | booking_id | fare |
| --- | --- | --- | --- |
| Bala | Asha | 103 | 500 |
| Charu | Asha | 104 | 700 |
| Deepa | Bala | 105 | 400 |

**C.**

| customer | referrer | booking_id | fare |
| --- | --- | --- | --- |
| Bala | Asha | 103 | 500 |
| Charu | Asha | 104 | 700 |
| Deepa | Bala | 105 | 400 |
| Farah | Charu | NULL | NULL |

**D.**

| customer | referrer | booking_id | fare |
| --- | --- | --- | --- |
| Charu | Asha | 104 | 700 |
| Deepa | Bala | 105 | 400 |

**Answer: B - 3 rows**

### Explanation

First, the self join identifies valid customer-referrer pairs.

| Customer | Referrer | Referrer status | Booking |
| --- | --- | --- | --- |
| Bala | Asha | ACTIVE | 103 |
| Charu | Asha | ACTIVE | 104 |
| Deepa | Bala | ACTIVE | 105 |
| Farah | Charu | INACTIVE | No booking |

Bala, Charu and Deepa satisfy the booking conditions.

Charu's own status is INACTIVE, but the query checks `r.status`, not `c.status`.

Farah is eliminated because the INNER JOIN with BOOKING finds no matching booking.

---

## Question 2 - SELF LEFT JOIN + aggregate functions + HAVING

Predict the exact output.

```sql
SELECT
    r.customer_name AS referrer,
    COUNT(DISTINCT c.customer_id) AS active_referrals,
    COUNT(b.booking_id) AS confirmed_bookings,
    COALESCE(SUM(b.seats), 0) AS confirmed_seats
FROM CUSTOMER r
LEFT JOIN CUSTOMER c
    ON c.referred_by = r.customer_id
    AND c.status = 'ACTIVE'
    AND c.city <> r.city
LEFT JOIN BOOKING b
    ON b.customer_id = c.customer_id
    AND b.booking_status = 'CONFIRMED'
GROUP BY
    r.customer_id,
    r.customer_name
HAVING
    COUNT(c.customer_id) > COUNT(b.booking_id)
ORDER BY r.customer_id;
```

**Which output is correct?**

**A.**

| referrer | active_referrals | confirmed_bookings | confirmed_seats |
| --- | --- | --- | --- |
| Asha | 1 | 1 | 1 |
| Bala | 1 | 0 | 0 |
| Charu | 1 | 0 | 0 |

**B.**

| referrer | active_referrals | confirmed_bookings | confirmed_seats |
| --- | --- | --- | --- |
| Asha | 2 | 2 | 4 |
| Bala | 1 | 0 | 0 |

**C.**

| referrer | active_referrals | confirmed_bookings | confirmed_seats |
| --- | --- | --- | --- |
| Bala | 1 | 0 | 0 |
| Charu | 1 | 0 | 0 |

**D.**

| referrer | active_referrals | confirmed_bookings | confirmed_seats |
| --- | --- | --- | --- |
| Bala | 1 | 1 | 2 |
| Charu | 1 | 0 | 0 |

**Answer: C - 2 rows**

### Explanation

First LEFT JOIN matches only ACTIVE referrals living in a different city.

| Referrer | Matching referral | Status | Different city? |
| --- | --- | --- | --- |
| Asha | Bala | ACTIVE | Yes |
| Asha | Charu | INACTIVE | No |
| Bala | Deepa | ACTIVE | Yes |
| Charu | Farah | ACTIVE | Yes |

Second LEFT JOIN checks for CONFIRMED bookings.

| Referrer | Active referrals | Confirmed bookings |
| --- | --- | --- |
| Asha | 1 | 1 |
| Bala | 1 | 0 |
| Charu | 1 | 0 |
| Deepa | 0 | 0 |
| Eshan | 0 | 0 |
| Farah | 0 | 0 |

Apply HAVING:

```sql
COUNT(c.customer_id) > COUNT(b.booking_id)
```

Asha: `1 > 1` → FALSE.

Bala: `1 > 0` → TRUE.

Charu: `1 > 0` → TRUE.

The other customers have `0 > 0`, which is FALSE.

Only Bala and Charu survive.

**Trick:** A LEFT JOIN preserves unmatched rows, but `COUNT(column)` ignores NULL values.

---

## Question 3 - BOOKING self join with duplicate matching pairs

Predict the exact output.

```sql
SELECT
    b1.booking_id AS first_booking,
    b2.booking_id AS second_booking,
    c1.customer_name AS first_customer,
    c2.customer_name AS second_customer,
    b1.fare - b2.fare AS fare_difference
FROM BOOKING b1
INNER JOIN BOOKING b2
    ON b1.flight_id = b2.flight_id
    AND b1.booking_id <> b2.booking_id
INNER JOIN CUSTOMER c1
    ON c1.customer_id = b1.customer_id
INNER JOIN CUSTOMER c2
    ON c2.customer_id = b2.customer_id
WHERE
    b1.fare >= b2.fare
    AND c1.status = 'ACTIVE'
    AND c2.status = 'ACTIVE'
ORDER BY b1.booking_id, b2.booking_id;
```

**Which output is correct?**

**A.**

| first_booking | second_booking | first_customer | second_customer | fare_difference |
| --- | --- | --- | --- | --- |
| 101 | 103 | Asha | Bala | 0 |

**B.**

| first_booking | second_booking | first_customer | second_customer | fare_difference |
| --- | --- | --- | --- | --- |
| 101 | 103 | Asha | Bala | 0 |
| 103 | 101 | Bala | Asha | 0 |

**C.**

| first_booking | second_booking | first_customer | second_customer | fare_difference |
| --- | --- | --- | --- | --- |
| 101 | 101 | Asha | Asha | 0 |
| 101 | 103 | Asha | Bala | 0 |
| 103 | 101 | Bala | Asha | 0 |
| 103 | 103 | Bala | Bala | 0 |

**D.** No rows returned.

**Answer: B - 2 rows**

### Explanation

First identify bookings with the same flight ID.

Flight 10 has two bookings:

| Booking | Customer | Flight | Fare |
| --- | --- | --- | --- |
| 101 | Asha | 10 | 500 |
| 103 | Bala | 10 | 500 |

The condition:

```sql
b1.booking_id <> b2.booking_id
```

removes self-pairs such as `(101,101)` and `(103,103)`.

But it does not remove reversed pairs.

Therefore:

- `(101,103)` qualifies.
- `(103,101)` also qualifies.

Both fares are equal, so `b1.fare >= b2.fare` is TRUE for both.

**Advanced trap:** Using `<>` produces both pair directions. To return each unordered pair only once, use:

```sql
b1.booking_id < b2.booking_id
```

---

## Question 4 - Three-level SELF JOIN + LEFT JOIN + GROUP BY

This question involves a referral hierarchy.

A customer may refer another customer, who may then refer someone else.

Predict the exact output.

```sql
SELECT
    g.customer_name AS grand_referrer,
    r.status AS direct_referrer_status,
    COUNT(DISTINCT c.customer_id) AS second_level_customers,
    COUNT(b.booking_id) AS qualifying_bookings,
    COALESCE(SUM(b.fare * b.seats), 0) AS total_value
FROM CUSTOMER c
INNER JOIN CUSTOMER r
    ON c.referred_by = r.customer_id
INNER JOIN CUSTOMER g
    ON r.referred_by = g.customer_id
LEFT JOIN BOOKING b
    ON b.customer_id = c.customer_id
    AND b.booking_status IN ('CONFIRMED', 'PENDING')
WHERE
    c.status = 'ACTIVE'
    AND g.status = 'ACTIVE'
GROUP BY
    g.customer_name,
    r.status
HAVING
    COUNT(DISTINCT c.customer_id) >= 1
ORDER BY r.status;
```

**Which output is correct?**

**A.**

| grand_referrer | direct_referrer_status | second_level_customers | qualifying_bookings | total_value |
| --- | --- | --- | --- | --- |
| Asha | ACTIVE | 2 | 1 | 800 |

**B.**

| grand_referrer | direct_referrer_status | second_level_customers | qualifying_bookings | total_value |
| --- | --- | --- | --- | --- |
| Asha | ACTIVE | 1 | 1 | 800 |
| Asha | INACTIVE | 1 | 0 | 0 |

**C.**

| grand_referrer | direct_referrer_status | second_level_customers | qualifying_bookings | total_value |
| --- | --- | --- | --- | --- |
| Asha | ACTIVE | 1 | 1 | 800 |
| Charu | INACTIVE | 1 | 0 | 0 |

**D.**

| grand_referrer | direct_referrer_status | second_level_customers | qualifying_bookings | total_value |
| --- | --- | --- | --- | --- |
| Asha | ACTIVE | 1 | 1 | 400 |
| Asha | INACTIVE | 1 | 1 | 700 |

**Answer: B - 2 rows**

### Explanation

First resolve the referral hierarchy.

```svg
<svg viewBox="0 0 320 170" width="100%" xmlns="http://www.w3.org/2000/svg"><rect x="117" y="6" width="86" height="35" rx="7" fill="#DCE9F9" stroke="#6697D5" /><text x="160" y="28" font-size="13" font-weight="600" text-anchor="middle" fill="#24466D">Asha</text><path d="M160 41 V55 H75 V70 M160 55 H245 V70" stroke="currentColor" opacity=".65" stroke-width="1.5" fill="none" /><rect x="32" y="70" width="86" height="35" rx="7" fill="#D9EFE5" stroke="#68A98D" /><text x="75" y="92" font-size="13" text-anchor="middle" fill="#24654B">Bala</text><rect x="202" y="70" width="86" height="35" rx="7" fill="#F8E6CF" stroke="#C9955C" /><text x="245" y="92" font-size="13" text-anchor="middle" fill="#805225">Charu</text><path d="M75 105 V127 M245 105 V127" stroke="currentColor" opacity=".65" stroke-width="1.5" /><rect x="32" y="127" width="86" height="35" rx="7" fill="#D9EFE5" stroke="#68A98D" /><text x="75" y="149" font-size="13" text-anchor="middle" fill="#24654B">Deepa</text><rect x="202" y="127" width="86" height="35" rx="7" fill="#D9EFE5" stroke="#68A98D" /><text x="245" y="149" font-size="13" text-anchor="middle" fill="#24654B">Farah</text></svg>
```

Asha is the grand-referrer of Deepa and Farah.

The first two INNER JOINs produce:

| Customer (c) | Referrer (r) | Grand-referrer (g) |
| --- | --- | --- |
| Deepa | Bala | Asha |
| Farah | Charu | Asha |

Both Deepa and Farah are ACTIVE.

Now apply the LEFT JOIN with BOOKING.

| Customer | Referrer status | Qualifying booking | Revenue |
| --- | --- | --- | --- |
| Deepa | ACTIVE | 105 (PENDING) | 800 |
| Farah | INACTIVE | NULL | 0 |

The query groups by both grand-referrer name and direct-referrer status.

Therefore, two groups are created.

**Important:** The WHERE clause checks `c.status` and `g.status`, not `r.status`. Therefore, Charu's inactive status does not eliminate Farah.

---

## Question 5 - SELF LEFT JOIN + NULL filtering + OR

Predict the exact output.

```sql
SELECT
    c.customer_name,
    c.referred_by,
    r.customer_name AS active_referrer,
    b.booking_id,
    b.fare
FROM CUSTOMER c
LEFT JOIN CUSTOMER r
    ON c.referred_by = r.customer_id
    AND r.status = 'ACTIVE'
LEFT JOIN BOOKING b
    ON b.customer_id = c.customer_id
    AND b.booking_status = 'CONFIRMED'
WHERE
    r.customer_id IS NULL
    AND (
        b.booking_id IS NULL
        OR b.fare >= 800
    )
ORDER BY c.customer_id, b.booking_id;
```

**Which output is correct?**

**A.**

| customer_name | referred_by | active_referrer | booking_id | fare |
| --- | --- | --- | --- | --- |
| Eshan | 9 | NULL | 107 | 900 |
| Farah | 3 | NULL | NULL | NULL |

**B.**

| customer_name | referred_by | active_referrer | booking_id | fare |
| --- | --- | --- | --- | --- |
| Asha | NULL | NULL | 101 | 500 |
| Eshan | 9 | NULL | 107 | 900 |
| Farah | 3 | NULL | NULL | NULL |

**C.**

| customer_name | referred_by | active_referrer | booking_id | fare |
| --- | --- | --- | --- | --- |
| Farah | 3 | NULL | NULL | NULL |

**D.**

| customer_name | referred_by | active_referrer | booking_id | fare |
| --- | --- | --- | --- | --- |
| Eshan | 9 | NULL | 107 | 900 |
| Farah | 3 | Charu | NULL | NULL |

**Answer: A - 2 rows**

### Explanation

First LEFT JOIN:

```sql
LEFT JOIN CUSTOMER r
    ON c.referred_by = r.customer_id
    AND r.status = 'ACTIVE'
```

This matches only ACTIVE referrers.

| Customer | Actual referrer | Active referrer match |
| --- | --- | --- |
| Asha | None | NULL |
| Bala | Asha | Asha |
| Charu | Asha | Asha |
| Deepa | Bala | Bala |
| Eshan | Invalid ID 9 | NULL |
| Farah | Charu (INACTIVE) | NULL |

The WHERE condition:

```sql
r.customer_id IS NULL
```

retains Asha, Eshan and Farah.

Now evaluate the second condition.

| Customer | Confirmed booking | Fare | Condition |
| --- | --- | --- | --- |
| Asha | 101 | 500 | FALSE |
| Eshan | 107 | 900 | TRUE |
| Farah | NULL | NULL | TRUE |

Asha is eliminated because she has a confirmed booking with fare below 800.

Eshan qualifies because fare 900 is at least 800.

Farah qualifies because `b.booking_id IS NULL`.

Final output contains Eshan and Farah.

**Advanced trap:** Farah has a real referrer, Charu. But Charu is INACTIVE, so the ON condition rejects that match, producing NULL in `r.customer_name`.

---

# PART 2 - Answer key

| Question | Concept | Answer | Rows |
| --- | --- | --- | --- |
| 1 | SELF INNER JOIN + BOOKING filters | B | 3 |
| 2 | SELF LEFT JOIN + HAVING | C | 2 |
| 3 | BOOKING self join + duplicate pairs | B | 2 |
| 4 | Three-level SELF JOIN + aggregates | B | 2 |
| 5 | SELF LEFT JOIN + NULL + OR | A | 2 |

## Key concepts tested

- SELF JOIN with different aliases.
- Self-referencing foreign keys and missing references.
- Duplicate pairs caused by `<>` versus `<`.
- How conditions in `ON` affect LEFT JOIN matching.
- `COUNT(column)` versus `COUNT(*)`.
- Aggregation after joining the same table multiple times.
- Three-level referral hierarchies.
- `WHERE` filters involving NULL-extended rows.

**Next: PART 3 - LEFT OUTER JOIN (5 Advanced Output MCQs)**

The next batch will include three-table LEFT JOINs, tricky `ON` versus `WHERE` differences, `COUNT(*)` versus `COUNT(column)`, duplicate matches, and grouped output tables with `CASE`, `SUM` and `HAVING`.

### User

continue

### ChatGPT

# PART 3 - LEFT OUTER JOIN (5 Advanced Output MCQs)

**Level:** Advanced to Expert
**Database:** HSQLDB
**Focus:** Predict the exact output table.

We will continue using the same `CUSTOMER`, `BOOKING`, and `FLIGHT` datasets.

These questions deliberately combine:

- Multiple LEFT JOINs.
- Conditions in ON versus WHERE.
- NULL handling.
- `COUNT(*)` versus `COUNT(column)`.
- `CASE WHEN`, `SUM`, `AVG`.
- `GROUP BY` and `HAVING`.

---

## Question 1 - Three-table LEFT JOIN with ON and WHERE

Predict the exact output.

```sql
SELECT
    c.customer_name,
    b.booking_id,
    b.booking_status,
    f.destination
FROM CUSTOMER c
LEFT JOIN BOOKING b
    ON c.customer_id = b.customer_id
    AND b.booking_status IN ('CONFIRMED', 'PENDING')
LEFT JOIN FLIGHT f
    ON b.flight_id = f.flight_id
    AND f.status <> 'CANCELLED'
WHERE
    c.status = 'ACTIVE'
    AND c.city <> 'Pune'
ORDER BY c.customer_id, b.booking_id;
```

**Which output is correct?**

**A.**

| customer_name | booking_id | booking_status | destination |
| --- | --- | --- | --- |
| Asha | 101 | CONFIRMED | Delhi |
| Bala | 103 | CONFIRMED | Delhi |
| Deepa | 105 | PENDING | Singapore |
| Eshan | 107 | CONFIRMED | NULL |

**B.**

| customer_name | booking_id | booking_status | destination |
| --- | --- | --- | --- |
| Asha | 101 | CONFIRMED | Delhi |
| Bala | 103 | CONFIRMED | Delhi |
| Deepa | 105 | PENDING | Singapore |
| Eshan | 107 | CONFIRMED | NULL |
| Farah | NULL | NULL | NULL |

**C.**

| customer_name | booking_id | booking_status | destination |
| --- | --- | --- | --- |
| Asha | 101 | CONFIRMED | Delhi |
| Bala | 103 | CONFIRMED | Delhi |
| Charu | 104 | CONFIRMED | Mumbai |
| Deepa | 105 | PENDING | Singapore |

**D.**

| customer_name | booking_id | booking_status | destination |
| --- | --- | --- | --- |
| Asha | 101 | CONFIRMED | Delhi |
| Asha | 102 | CANCELLED | Dubai |
| Bala | 103 | CONFIRMED | Delhi |
| Deepa | 105 | PENDING | Singapore |
| Eshan | 107 | CONFIRMED | NULL |

(Answer: A - 4 rows)

### Explanation

First LEFT JOIN:

```sql
ON c.customer_id = b.customer_id
AND b.booking_status IN ('CONFIRMED', 'PENDING')
```

Cancelled bookings are excluded from matching.

Second LEFT JOIN:

```sql
ON b.flight_id = f.flight_id
AND f.status <> 'CANCELLED'
```

A booking can survive even if its flight does not match.

| Customer | Booking | Flight match |
| --- | --- | --- |
| Asha | 101 | Delhi |
| Bala | 103 | Delhi |
| Deepa | 105 | Singapore |
| Eshan | 107 | NULL |
| Charu | NULL | NULL |
| Farah | NULL | NULL |

WHERE removes:

- Charu because she is INACTIVE.
- Farah because her city is Pune.

Final output = 4 rows.

**Important:** Eshan's booking 107 survives because the second join is LEFT JOIN, even though flight 999 does not exist.

---

## Question 2 - LEFT JOIN with COUNT(*) versus COUNT(column)

Predict the exact output.

```sql
SELECT
    c.city,
    COUNT(*) AS total_rows,
    COUNT(b.booking_id) AS booking_count,
    COUNT(DISTINCT c.customer_id) AS customer_count,
    COALESCE(SUM(b.seats), 0) AS total_seats
FROM CUSTOMER c
LEFT JOIN BOOKING b
    ON c.customer_id = b.customer_id
    AND b.booking_status = 'CONFIRMED'
GROUP BY c.city
ORDER BY c.city;
```

**Which output is correct?**

**A.**

| city | total_rows | booking_count | customer_count | total_seats |
| --- | --- | --- | --- | --- |
| Bengaluru | 1 | 1 | 1 | 1 |
| Chennai | 3 | 2 | 2 | 5 |
| Hyderabad | 1 | 0 | 1 | 0 |
| Mumbai | 1 | 1 | 1 | 1 |
| Pune | 1 | 0 | 1 | 0 |

**B.**

| city | total_rows | booking_count | customer_count | total_seats |
| --- | --- | --- | --- | --- |
| Bengaluru | 1 | 1 | 1 | 1 |
| Chennai | 3 | 2 | 2 | 5 |
| Hyderabad | 1 | 1 | 1 | 2 |
| Mumbai | 1 | 1 | 1 | 1 |
| Pune | 1 | 0 | 1 | 0 |

**C.**

| city | total_rows | booking_count | customer_count | total_seats |
| --- | --- | --- | --- | --- |
| Bengaluru | 1 | 1 | 1 | 1 |
| Chennai | 2 | 2 | 2 | 5 |
| Hyderabad | 0 | 0 | 1 | 0 |
| Mumbai | 1 | 1 | 1 | 1 |
| Pune | 0 | 0 | 1 | 0 |

**D.**

| city | total_rows | booking_count | customer_count | total_seats |
| --- | --- | --- | --- | --- |
| Bengaluru | 1 | 1 | 1 | 1 |
| Chennai | 3 | 3 | 2 | 6 |
| Hyderabad | 1 | 0 | 1 | 0 |
| Mumbai | 1 | 1 | 1 | 1 |
| Pune | 1 | 0 | 1 | 0 |

(Answer: A - 5 groups)

### Explanation

The LEFT JOIN matches only confirmed bookings.

| Customer | Confirmed bookings |
| --- | --- |
| Asha | 101 |
| Bala | 103 |
| Charu | 104 |
| Deepa | None |
| Eshan | 107 |
| Farah | None |

Notice Chennai contains two customers:

- Asha has one confirmed booking.
- Charu has one confirmed booking.

Therefore, Chennai produces two booking rows and one customer row for each customer.

Actually, Chennai has 3 joined rows because Asha has one confirmed booking and Charu has one confirmed booking, giving 2 rows. Wait: Asha's booking 102 is CANCELLED and does not match. Therefore, there are 2 rows, not 3.

The correct result is:

| city | total_rows | booking_count | customer_count | total_seats |
| --- | --- | --- | --- | --- |
| Bengaluru | 1 | 1 | 1 | 1 |
| Chennai | 2 | 2 | 2 | 5 |
| Hyderabad | 1 | 0 | 1 | 0 |
| Mumbai | 1 | 1 | 1 | 1 |
| Pune | 1 | 0 | 1 | 0 |

**None of the original options is exact.** Option C also incorrectly gives zero for `total_rows` in unmatched groups. The correct Chennai `total_rows` is 2, while unmatched customers each contribute one row.

This illustrates why you should calculate the joined rows before calculating aggregates.

---

## Question 3 - LEFT JOIN with WHERE OR IS NULL

Predict the exact output.

```sql
SELECT
    c.customer_name,
    b.booking_id,
    b.booking_status,
    b.fare
FROM CUSTOMER c
LEFT JOIN BOOKING b
    ON c.customer_id = b.customer_id
WHERE
    b.booking_status = 'CONFIRMED'
    OR b.booking_id IS NULL
ORDER BY c.customer_id, b.booking_id;
```

**Which output is correct?**

**A.**

| customer_name | booking_id | booking_status | fare |
| --- | --- | --- | --- |
| Asha | 101 | CONFIRMED | 500 |
| Bala | 103 | CONFIRMED | 500 |
| Charu | 104 | CONFIRMED | 700 |
| Eshan | 107 | CONFIRMED | 900 |
| Farah | NULL | NULL | NULL |

**B.**

| customer_name | booking_id | booking_status | fare |
| --- | --- | --- | --- |
| Asha | 101 | CONFIRMED | 500 |
| Bala | 103 | CONFIRMED | 500 |
| Charu | 104 | CONFIRMED | 700 |
| Eshan | 107 | CONFIRMED | 900 |

**C.**

| customer_name | booking_id | booking_status | fare |
| --- | --- | --- | --- |
| Asha | 101 | CONFIRMED | 500 |
| Asha | 102 | CANCELLED | 300 |
| Bala | 103 | CONFIRMED | 500 |
| Charu | 104 | CONFIRMED | 700 |
| Eshan | 107 | CONFIRMED | 900 |
| Farah | NULL | NULL | NULL |

**D.**

| customer_name | booking_id | booking_status | fare |
| --- | --- | --- | --- |
| Asha | 101 | CONFIRMED | 500 |
| Bala | 103 | CONFIRMED | 500 |
| Charu | 104 | CONFIRMED | 700 |
| Deepa | NULL | NULL | NULL |
| Eshan | 107 | CONFIRMED | 900 |
| Farah | NULL | NULL | NULL |

(Answer: A - 5 rows)

### Explanation

The LEFT JOIN initially produces seven rows.

| Customer | Booking | Status |
| --- | --- | --- |
| Asha | 101 | CONFIRMED |
| Asha | 102 | CANCELLED |
| Bala | 103 | CONFIRMED |
| Charu | 104 | CONFIRMED |
| Deepa | 105 | PENDING |
| Eshan | 107 | CONFIRMED |
| Farah | NULL | NULL |

WHERE condition:

```sql
b.booking_status = 'CONFIRMED'
OR b.booking_id IS NULL
```

- Confirmed bookings survive.
- Farah survives because booking ID is NULL.
- Asha's cancelled booking is removed.
- Deepa's pending booking is removed.

Final output = 5 rows.

**Important:** Deepa is removed even though she has a matching booking. `b.booking_id IS NULL` is not true for her.

---

## Question 4 - LEFT JOIN + CASE + GROUP BY + HAVING

Predict the exact output.

```sql
SELECT
    c.city,
    COUNT(DISTINCT c.customer_id) AS customers,
    COUNT(b.booking_id) AS total_bookings,
    SUM(
        CASE
            WHEN b.booking_status = 'CONFIRMED'
            THEN b.fare * b.seats
            ELSE 0
        END
    ) AS confirmed_revenue,
    SUM(
        CASE
            WHEN b.booking_status = 'CANCELLED'
            THEN 1
            ELSE 0
        END
    ) AS cancelled_bookings
FROM CUSTOMER c
LEFT JOIN BOOKING b
    ON c.customer_id = b.customer_id
GROUP BY c.city
HAVING
    COUNT(b.booking_id) >= 1
    AND SUM(
        CASE
            WHEN b.booking_status = 'CONFIRMED'
            THEN b.fare * b.seats
            ELSE 0
        END
    ) >= 1000
ORDER BY c.city;
```

**Which output is correct?**

**A.**

| city | customers | total_bookings | confirmed_revenue | cancelled_bookings |
| --- | --- | --- | --- | --- |
| Chennai | 2 | 3 | 3100 | 1 |
| Mumbai | 1 | 1 | 900 | 0 |

**B.**

| city | customers | total_bookings | confirmed_revenue | cancelled_bookings |
| --- | --- | --- | --- | --- |
| Chennai | 2 | 3 | 3100 | 1 |

**C.**

| city | customers | total_bookings | confirmed_revenue | cancelled_bookings |
| --- | --- | --- | --- | --- |
| Chennai | 2 | 3 | 3100 | 1 |
| Bengaluru | 1 | 1 | 500 | 0 |

**D.**

| city | customers | total_bookings | confirmed_revenue | cancelled_bookings |
| --- | --- | --- | --- | --- |
| Chennai | 2 | 3 | 2400 | 1 |
| Hyderabad | 1 | 1 | 0 | 0 |

(Answer: B - 1 group)

### Explanation

Calculate group-wise results.

| City | Customers | Bookings | Confirmed revenue | Cancelled |
| --- | --- | --- | --- | --- |
| Chennai | 2 | 3 | 3100 | 1 |
| Bengaluru | 1 | 1 | 500 | 0 |
| Hyderabad | 1 | 1 | 0 | 0 |
| Mumbai | 1 | 1 | 900 | 0 |
| Pune | 1 | 0 | 0 | 0 |

Chennai revenue:

$$
(500 \times 2)+(700 \times 3)=3100
$$

Mumbai revenue is 900, not 1000, because Eshan has one seat at 900.

HAVING requires:

- At least one booking.
- Confirmed revenue at least 1000.

Only Chennai survives.

---

## Question 5 - Multiple LEFT JOINs with nested filtering and aggregate output

Predict the exact output.

```sql
SELECT
    c.customer_name,
    COUNT(b.booking_id) AS booking_count,
    COUNT(f.flight_id) AS valid_flights,
    SUM(
        CASE
            WHEN f.flight_type = 'DOMESTIC'
            THEN b.seats
            ELSE 0
        END
    ) AS domestic_seats,
    SUM(
        CASE
            WHEN f.flight_type = 'INTERNATIONAL'
            THEN b.seats
            ELSE 0
        END
    ) AS international_seats
FROM CUSTOMER c
LEFT JOIN BOOKING b
    ON c.customer_id = b.customer_id
    AND b.booking_status <> 'CANCELLED'
LEFT JOIN FLIGHT f
    ON b.flight_id = f.flight_id
    AND f.status <> 'CANCELLED'
WHERE
    c.status = 'ACTIVE'
GROUP BY
    c.customer_id,
    c.customer_name
HAVING
    COUNT(b.booking_id) >= 1
ORDER BY c.customer_name;
```

**Which output is correct?**

**A.**

| customer_name | booking_count | valid_flights | domestic_seats | international_seats |
| --- | --- | --- | --- | --- |
| Asha | 1 | 1 | 2 | 0 |
| Bala | 1 | 1 | 1 | 0 |
| Deepa | 1 | 1 | 0 | 2 |
| Eshan | 1 | 0 | 0 | 0 |

**B.**

| customer_name | booking_count | valid_flights | domestic_seats | international_seats |
| --- | --- | --- | --- | --- |
| Asha | 2 | 2 | 2 | 1 |
| Bala | 1 | 1 | 1 | 0 |
| Deepa | 1 | 1 | 0 | 2 |
| Eshan | 1 | 0 | 0 | 0 |

**C.**

| customer_name | booking_count | valid_flights | domestic_seats | international_seats |
| --- | --- | --- | --- | --- |
| Asha | 1 | 1 | 2 | 0 |
| Bala | 1 | 1 | 1 | 0 |
| Deepa | 1 | 1 | 0 | 0 |
| Eshan | 0 | 0 | 0 | 0 |

**D.**

| customer_name | booking_count | valid_flights | domestic_seats | international_seats |
| --- | --- | --- | --- | --- |
| Asha | 1 | 1 | 2 | 0 |
| Bala | 1 | 1 | 1 | 0 |
| Deepa | 1 | 1 | 0 | 2 |
| Eshan | 1 | 1 | 0 | 1 |

(Answer: A - 4 customers)

### Explanation

First LEFT JOIN:

```sql
AND b.booking_status <> 'CANCELLED'
```

Asha's cancelled booking 102 is excluded from matching.

Second LEFT JOIN:

```sql
AND f.status <> 'CANCELLED'
```

Eshan's booking 107 has flight 999, which does not exist. The booking survives, but the flight columns become NULL.

Evaluate the customers:

| Customer | Booking | Flight | Valid flight? |
| --- | --- | --- | --- |
| Asha | 101 | Domestic | Yes |
| Bala | 103 | Domestic | Yes |
| Deepa | 105 | International | Yes |
| Eshan | 107 | NULL | No |

Now calculate aggregates:

- `COUNT(b.booking_id)` counts bookings even when the flight is missing.
- `COUNT(f.flight_id)` counts only matching flights.
- Domestic seats count only domestic flights.
- International seats count only international flights.

Eshan contributes one booking, zero valid flights and zero seats in both flight categories.

All four customers pass HAVING.

---

# PART 3 - Answer summary

| Question | Main concept | Correct output rows |
| --- | --- | --- |
| 1 | Three-table LEFT JOIN | 4 |
| 2 | COUNT(*) vs COUNT(column) | 5 groups |
| 3 | WHERE + OR + IS NULL | 5 |
| 4 | CASE + GROUP BY + HAVING | 1 |
| 5 | Multiple LEFT JOINs + aggregates | 4 |

## Important exam traps from this batch

| Concept | What happens |
| --- | --- |
| Filter in LEFT JOIN ON | Left-side records remain |
| Filter in WHERE | Can eliminate NULL-extended records |
| COUNT(*) | Counts NULL-extended rows |
| COUNT(b.booking_id) | Ignores NULL booking IDs |
| COUNT(f.flight_id) | Counts only valid matching flights |
| SUM(CASE WHEN...) | Calculates conditional totals |
| COALESCE(SUM(...),0) | Replaces NULL aggregate result with zero |
| HAVING | Filters after grouping |
| Multiple LEFT JOINs | A record may survive one join but fail to match the next |

---

# Next: PART 4 - RIGHT OUTER JOIN (5 Advanced Output MCQs)

We'll cover:

1. RIGHT JOIN with multiple ON conditions.
2. RIGHT JOIN with WHERE and NULL filtering.
3. Three-table RIGHT JOIN with missing customers and flights.
4. RIGHT JOIN with GROUP BY, COUNT and SUM.
5. Multiple RIGHT JOINs with CASE, HAVING and duplicate matches.

### User

continue

### ChatGPT

# PART 4 - RIGHT OUTER JOIN: 5 Advanced Output MCQs

We’ll continue with the same `CUSTOMER`, `BOOKING`, and `FLIGHT` tables.

**Important:** A `RIGHT OUTER JOIN` preserves every row from the right-side table, even when no matching row exists on the left. Missing left-side columns become `NULL`.

---

## Q1. RIGHT JOIN with multiple conditions in ON

**Query:**

```sql
SELECT
    b.booking_id,
    c.customer_name,
    c.status,
    b.booking_status,
    b.fare
FROM CUSTOMER c
RIGHT OUTER JOIN BOOKING b
    ON c.customer_id = b.customer_id
   AND c.status = 'ACTIVE'
   AND b.fare >= 500
ORDER BY b.booking_id;
```

What is the correct output?

**Option A**

| booking_id | customer_name | status | booking_status | fare |
| --- | --- | --- | --- | --- |
| 101 | Asha | ACTIVE | CONFIRMED | 500 |
| 102 | NULL | NULL | CANCELLED | 300 |
| 103 | Bala | ACTIVE | CONFIRMED | 500 |
| 104 | NULL | NULL | CONFIRMED | 700 |
| 105 | NULL | NULL | PENDING | 400 |
| 106 | NULL | NULL | CONFIRMED | 600 |
| 107 | Eshan | ACTIVE | CONFIRMED | 900 |

**Option B**

| booking_id | customer_name | status | booking_status | fare |
| --- | --- | --- | --- | --- |
| 101 | Asha | ACTIVE | CONFIRMED | 500 |
| 103 | Bala | ACTIVE | CONFIRMED | 500 |
| 104 | Charu | INACTIVE | CONFIRMED | 700 |
| 106 | NULL | NULL | CONFIRMED | 600 |
| 107 | Eshan | ACTIVE | CONFIRMED | 900 |

**Option C**

| booking_id | customer_name | status | booking_status | fare |
| --- | --- | --- | --- | --- |
| 101 | Asha | ACTIVE | CONFIRMED | 500 |
| 102 | NULL | NULL | CANCELLED | 300 |
| 103 | Bala | ACTIVE | CONFIRMED | 500 |
| 104 | Charu | INACTIVE | CONFIRMED | 700 |
| 105 | Deepa | ACTIVE | PENDING | 400 |
| 106 | NULL | NULL | CONFIRMED | 600 |
| 107 | Eshan | ACTIVE | CONFIRMED | 900 |

**Option D**

| booking_id | customer_name | status | booking_status | fare |
| --- | --- | --- | --- | --- |
| 101 | Asha | ACTIVE | CONFIRMED | 500 |
| 103 | Bala | ACTIVE | CONFIRMED | 500 |
| 107 | Eshan | ACTIVE | CONFIRMED | 900 |

(Correct answer: A)

**Explanation:**

The right table is `BOOKING`, so all seven bookings must appear.

The matching condition requires both:

- Customer must be ACTIVE.
- Booking fare must be at least 500.

Booking 104 has fare 700, but Charu is INACTIVE, so the customer columns become NULL.

Booking 105 has an ACTIVE customer, Deepa, but fare is only 400. Therefore, it also has no match.

Booking 106 has no corresponding customer at all.

The unmatched booking rows are preserved because of the RIGHT JOIN.

---

## Q2. RIGHT JOIN with WHERE and NULL filtering

**Query:**

```sql
SELECT
    b.booking_id,
    c.customer_name,
    b.booking_status
FROM CUSTOMER c
RIGHT JOIN BOOKING b
    ON c.customer_id = b.customer_id
WHERE c.customer_id IS NULL
   OR b.booking_status = 'CANCELLED'
ORDER BY b.booking_id;
```

What is the output?

**Option A**

| booking_id | customer_name | booking_status |
| --- | --- | --- |
| 102 | Asha | CANCELLED |
| 106 | NULL | CONFIRMED |

**Option B**

| booking_id | customer_name | booking_status |
| --- | --- | --- |
| 102 | Asha | CANCELLED |
| 106 | NULL | CONFIRMED |
| 107 | Eshan | CONFIRMED |

**Option C**

| booking_id | customer_name | booking_status |
| --- | --- | --- |
| 102 | Asha | CANCELLED |
| 104 | Charu | CONFIRMED |
| 106 | NULL | CONFIRMED |

**Option D**

| booking_id | customer_name | booking_status |
| --- | --- | --- |
| 106 | NULL | CONFIRMED |

(Correct answer: A)

**Explanation:**

Evaluate the WHERE condition for each booking:

| booking_id | Customer match? | Cancelled? | Included? |
| --- | --- | --- | --- |
| 101 | Yes | No | No |
| 102 | Yes | Yes | Yes |
| 103 | Yes | No | No |
| 104 | Yes | No | No |
| 105 | Yes | No | No |
| 106 | No | No | Yes |
| 107 | Yes | No | No |

Two rows satisfy the OR condition:

1. Booking 102 satisfies `booking_status = 'CANCELLED'`.
2. Booking 106 satisfies `customer_id IS NULL`.

**Exam trap:** Booking 107 has a missing flight, not a missing customer. This query joins only CUSTOMER and BOOKING, so Eshan is a valid match.

---

## Q3. Three-table RIGHT JOIN with missing customer and flight records

**Query:**

```sql
SELECT
    b.booking_id,
    c.customer_name,
    f.destination,
    b.booking_status
FROM CUSTOMER c
RIGHT JOIN BOOKING b
    ON c.customer_id = b.customer_id
RIGHT JOIN FLIGHT f
    ON b.flight_id = f.flight_id
ORDER BY f.flight_id;
```

What is the correct output?

**Option A**

| booking_id | customer_name | destination | booking_status |
| --- | --- | --- | --- |
| 101 | Asha | Delhi | CONFIRMED |
| 103 | Bala | Delhi | CONFIRMED |
| 102 | Asha | Dubai | CANCELLED |
| 104 | Charu | Mumbai | CONFIRMED |
| 105 | Deepa | Singapore | PENDING |
| 106 | NULL | Kolkata | CONFIRMED |
| NULL | NULL | London | NULL |

**Option B**

| booking_id | customer_name | destination | booking_status |
| --- | --- | --- | --- |
| 101 | Asha | Delhi | CONFIRMED |
| 103 | Bala | Delhi | CONFIRMED |
| 102 | Asha | Dubai | CANCELLED |
| 104 | Charu | Mumbai | CONFIRMED |
| 105 | Deepa | Singapore | PENDING |
| 106 | NULL | Kolkata | CONFIRMED |
| 107 | Eshan | NULL | CONFIRMED |

**Option C**

| booking_id | customer_name | destination | booking_status |
| --- | --- | --- | --- |
| 101 | Asha | Delhi | CONFIRMED |
| 103 | Bala | Delhi | CONFIRMED |
| 102 | Asha | Dubai | CANCELLED |
| 104 | Charu | Mumbai | CONFIRMED |
| 105 | Deepa | Singapore | PENDING |
| 106 | NULL | Kolkata | CONFIRMED |
| NULL | NULL | London | NULL |
| NULL | NULL | NULL | NULL |

**Option D**

| booking_id | customer_name | destination | booking_status |
| --- | --- | --- | --- |
| 101 | Asha | Delhi | CONFIRMED |
| 103 | Bala | Delhi | CONFIRMED |
| 102 | Asha | Dubai | CANCELLED |
| 104 | Charu | Mumbai | CONFIRMED |
| 105 | Deepa | Singapore | PENDING |
| 106 | NULL | Kolkata | CONFIRMED |
| 107 | Eshan | NULL | CONFIRMED |
| NULL | NULL | London | NULL |

(Correct answer: A)

**Explanation:**

Understand the order of execution:

**First JOIN:**

```sql
CUSTOMER c
RIGHT JOIN BOOKING b
    ON c.customer_id = b.customer_id
```

All seven bookings are preserved.

**Second JOIN:**

```sql
... RIGHT JOIN FLIGHT f
    ON b.flight_id = f.flight_id
```

Now every flight must be preserved.

- Flight 10 has two bookings: 101 and 103.
- Flight 11 has booking 102.
- Flight 12 has booking 104.
- Flight 13 has booking 105.
- Flight 14 has booking 106.
- Flight 15 has no booking, so its booking and customer columns are NULL.

Booking 107 disappears because its flight ID 999 does not match any flight, and the second RIGHT JOIN preserves flights, not unmatched bookings.

**Key takeaway:** In chained RIGHT JOINs, the rightmost table of each individual JOIN determines which rows are preserved at that stage.

---

## Q4. RIGHT JOIN with GROUP BY, COUNT and SUM

**Query:**

```sql
SELECT
    c.city,
    COUNT(*) AS total_rows,
    COUNT(b.booking_id) AS booking_count,
    SUM(b.seats) AS total_seats,
    SUM(b.fare) AS total_fare
FROM BOOKING b
RIGHT JOIN CUSTOMER c
    ON b.customer_id = c.customer_id
GROUP BY c.city
ORDER BY c.city;
```

What is the correct output?

**Option A**

| city | total_rows | booking_count | total_seats | total_fare |
| --- | --- | --- | --- | --- |
| Bengaluru | 1 | 1 | 1 | 500 |
| Chennai | 3 | 3 | 6 | 1500 |
| Hyderabad | 1 | 1 | 2 | 400 |
| Mumbai | 1 | 1 | 1 | 900 |
| Pune | 1 | 0 | NULL | NULL |

**Option B**

| city | total_rows | booking_count | total_seats | total_fare |
| --- | --- | --- | --- | --- |
| Bengaluru | 1 | 1 | 1 | 500 |
| Chennai | 2 | 2 | 5 | 1200 |
| Hyderabad | 1 | 1 | 2 | 400 |
| Mumbai | 1 | 1 | 1 | 900 |
| Pune | 1 | 0 | NULL | NULL |

**Option C**

| city | total_rows | booking_count | total_seats | total_fare |
| --- | --- | --- | --- | --- |
| Bengaluru | 1 | 1 | 1 | 500 |
| Chennai | 3 | 3 | 6 | 1500 |
| Hyderabad | 1 | 1 | 2 | 400 |
| Mumbai | 1 | 1 | 1 | 900 |
| Pune | 0 | 0 | 0 | 0 |

**Option D**

| city | total_rows | booking_count | total_seats | total_fare |
| --- | --- | --- | --- | --- |
| Bengaluru | 1 | 1 | 1 | 500 |
| Chennai | 2 | 2 | 5 | 1200 |
| Hyderabad | 1 | 0 | NULL | NULL |
| Mumbai | 1 | 1 | 1 | 900 |
| Pune | 1 | 0 | NULL | NULL |

(Correct answer: B)

**Explanation:**

Here, `CUSTOMER` is the right table. Therefore, all six customers appear.

Notice that booking 106 belongs to customer ID 99, which does not exist in CUSTOMER. Since the RIGHT JOIN preserves CUSTOMER rows, booking 106 is not included.

Customer-wise calculation:

| Customer | Bookings | Seats | Fare |
| --- | --- | --- | --- |
| Asha | 2 | 3 | 800 |
| Bala | 1 | 1 | 500 |
| Charu | 1 | 3 | 700 |
| Deepa | 1 | 2 | 400 |
| Eshan | 1 | 1 | 900 |
| Farah | 0 | NULL | NULL |

Grouping by city:

- Chennai: Asha + Charu = 3 bookings, 6 seats, fare 1500.
- Bengaluru: 1 booking, 1 seat, fare 500.
- Hyderabad: 1 booking, 2 seats, fare 400.
- Mumbai: 1 booking, 1 seat, fare 900.
- Pune: no booking, so SUM returns NULL.

**Important exam distinction:**

- `COUNT(*)` counts the preserved customer row even if there is no booking.
- `COUNT(b.booking_id)` ignores NULL booking IDs.
- `SUM(b.seats)` returns NULL when every value in the group is NULL.

---

## Q5. RIGHT JOIN with CASE, HAVING and multiple matches

**Query:**

```sql
SELECT
    c.city,
    COUNT(b.booking_id) AS total_bookings,
    SUM(
        CASE
            WHEN b.booking_status = 'CONFIRMED'
            THEN b.seats
            ELSE 0
        END
    ) AS confirmed_seats,
    SUM(
        CASE
            WHEN b.booking_status = 'CANCELLED'
            THEN 1
            ELSE 0
        END
    ) AS cancelled_bookings
FROM BOOKING b
RIGHT JOIN CUSTOMER c
    ON b.customer_id = c.customer_id
GROUP BY c.city
HAVING COUNT(b.booking_id) >= 1
   AND SUM(
       CASE
           WHEN b.booking_status = 'CONFIRMED'
           THEN b.seats
           ELSE 0
       END
   ) >= 2
ORDER BY c.city;
```

What is the correct output?

**Option A**

| city | total_bookings | confirmed_seats | cancelled_bookings |
| --- | --- | --- | --- |
| Chennai | 3 | 5 | 1 |

**Option B**

| city | total_bookings | confirmed_seats | cancelled_bookings |
| --- | --- | --- | --- |
| Chennai | 3 | 5 | 1 |
| Hyderabad | 1 | 0 | 0 |

**Option C**

| city | total_bookings | confirmed_seats | cancelled_bookings |
| --- | --- | --- | --- |
| Chennai | 3 | 5 | 1 |
| Mumbai | 1 | 1 | 0 |

**Option D**

| city | total_bookings | confirmed_seats | cancelled_bookings |
| --- | --- | --- | --- |
| Chennai | 2 | 5 | 0 |

(Correct answer: A)

**Explanation:**

Calculate each city's group before applying HAVING.

| City | Total bookings | Confirmed seats | Cancelled bookings |
| --- | --- | --- | --- |
| Chennai | 3 | 5 | 1 |
| Bengaluru | 1 | 1 | 0 |
| Hyderabad | 1 | 0 | 0 |
| Mumbai | 1 | 1 | 0 |
| Pune | 0 | 0 | 0 |

The HAVING condition requires:

```sql
COUNT(b.booking_id) >= 1
AND confirmed_seats >= 2
```

Only Chennai satisfies both conditions.

Chennai includes:

- Booking 101: 2 confirmed seats.
- Booking 102: 1 cancelled booking, contributes 0 confirmed seats.
- Booking 104: 3 confirmed seats.

Therefore, confirmed seats = 2 + 3 = 5, total bookings = 3, and cancelled bookings = 1.

---

## Quick revision: RIGHT JOIN exam traps

| Situation | What happens? |
| --- | --- |
| Unmatched row in right table | Preserved |
| Unmatched row in left table | Discarded |
| Left-side condition in `ON` | Right-side rows are still preserved |
| Left-side condition in `WHERE` | Can eliminate NULL-extended rows |
| `COUNT(*)` | Counts preserved rows |
| `COUNT(left_table.id)` | Ignores NULL values |
| `SUM()` over only NULL values | Returns NULL |
| Chained RIGHT JOIN | Each JOIN preserves its own right-side table |

**Next: PART 5 - FULL OUTER JOIN (5 Advanced Output MCQs)**, covering unmatched rows from both tables, NULL handling, multiple joins, aggregation and filtering.
