# SQL-PLACEMENT-PREP
<div align="center">

# 🧮 SQL Notes: Placement Preparation

### SQLBolt Lessons · Gap Topics · LeetCode SQL 50 · Interview Q&A

![Language](https://img.shields.io/badge/Language-SQL-blue?style=for-the-badge)
![Practice](https://img.shields.io/badge/Practice-LeetCode_SQL_50-orange?style=for-the-badge)
![Style](https://img.shields.io/badge/Notes-Hinglish-green?style=for-the-badge)

*Concept pehle, practice baad mein. Ratta nahi, samajh ke.*

</div>

---

## 📊 Progress Tracker

<!-- PROGRESS:START -->
![Progress](https://img.shields.io/badge/Progress-0%25-red?style=for-the-badge) ![Tasks](https://img.shields.io/badge/Tasks-0%2F0-blue?style=for-the-badge)

**Overall:** `⬜⬜⬜⬜⬜⬜⬜⬜⬜⬜` **0%** (0/0 tasks done)
<!-- PROGRESS:END -->

👉 Tick karne ke liye [📈 Progress Tracker issue](../../issues) kholo aur checkbox par click karo. Bar apne aap update hoga.

---

## 🧭 Study Method (har lesson ke liye)

1. **SQLBolt** par lesson padho aur exercises khud solve karo.
2. Apne shabdon mein **note** likho (`01-SQLBolt-Lessons/`).
3. Us topic ke **LeetCode SQL 50** problems karo.
4. Galtiyan [mistake-log.md](mistake-log.md) mein likho.

**Roz ka routine (2.5-3 ghante):** 30 min concept · 60-90 min problems · 15 min notes + mistake log · 10 min pichhle din ke 2 problems dobara.

---

## 🗓️ 10-Day SQL Roadmap

| Day | Topic | Concept source | Practice (LeetCode SQL 50) |
|---|---|---|---|
| **1** | SELECT, WHERE, ORDER BY, LIMIT, filtering | SQLBolt Lessons 1-5 | Select section |
| **2** | Joins, Outer Joins, NULLs | SQLBolt Lessons 6-8 | Basic Joins |
| **3** | Expressions, Aggregates, GROUP BY, HAVING, execution order | SQLBolt Lessons 9-12 | Basic Aggregate Functions |
| **4** | INSERT, UPDATE, DELETE, CREATE, ALTER, DROP, constraints | SQLBolt Lessons 13-18 | Khud ke tables bana ke practice |
| **5** | Subqueries, EXISTS, correlated, UNION / INTERSECT / EXCEPT | Gap Topics notes | Subqueries |
| **6** | CTE, Window functions | Gap Topics notes | Advanced Select and Joins |
| **7** | String/Date functions, CASE, COALESCE | Gap Topics notes | Advanced String Functions |
| **8** | Views, Indexes, Stored Procedures, interview theory | Gap Topics notes | Mixed revision |
| **9** | Timed practice, weak topics dobara | | Mixed |
| **10** | **Mock test** (5 medium queries, 60 min) | | Mixed |

> LeetCode study plan ka exact section order wahin dekh lena, kyunki wo update hota rehta hai.

---

## 📚 Lesson-wise Notes (SQLBolt)

> Lesson ke naam SQLBolt site se verify kar lena.

| # | Lesson | Notes |
|---|---|---|
| 1 | SELECT queries 101 | [Lesson 1](01-SQLBolt-Lessons/Lesson-01-select-queries-101.md) |
| 2 | Queries with constraints (Pt. 1) | `Lesson-02-...md` |
| 3 | Queries with constraints (Pt. 2) | `Lesson-03-...md` |
| 4 | Filtering and sorting query results | `Lesson-04-...md` |
| 5 | Simple SELECT query review | `Lesson-05-...md` |
| 6 | Multi-table queries with JOINs | `Lesson-06-...md` |
| 7 | OUTER JOINs | `Lesson-07-...md` |
| 8 | A short note on NULLs | `Lesson-08-...md` |
| 9 | Queries with expressions | `Lesson-09-...md` |
| 10 | Queries with aggregates (Pt. 1) | `Lesson-10-...md` |
| 11 | Queries with aggregates (Pt. 2) | `Lesson-11-...md` |
| 12 | Order of execution of a query | `Lesson-12-...md` |
| 13 | Inserting rows | `Lesson-13-...md` |
| 14 | Updating rows | `Lesson-14-...md` |
| 15 | Deleting rows | `Lesson-15-...md` |
| 16 | Creating tables | `Lesson-16-...md` |
| 17 | Altering tables | `Lesson-17-...md` |
| 18 | Dropping tables | `Lesson-18-...md` |

---

## 🧩 Gap Topics (SQLBolt mein nahi hain, lekin interviews mein aate hain)

| Topic | Folder |
|---|---|
| Subqueries, EXISTS, correlated subquery | `02-Gap-Topics/subqueries.md` |
| UNION, UNION ALL, INTERSECT, EXCEPT | `02-Gap-Topics/set-operations.md` |
| CTE (`WITH`) | `02-Gap-Topics/cte.md` |
| Window functions (ROW_NUMBER, RANK, DENSE_RANK, LAG, LEAD) | `02-Gap-Topics/window-functions.md` |
| String, Date functions, CASE, COALESCE | `02-Gap-Topics/functions.md` |
| Views, Indexes, Stored Procedures | `02-Gap-Topics/views-indexes-procedures.md` |

---

## ✅ Topic Checklist

- [ ] SELECT, DISTINCT, WHERE, LIKE, IN, BETWEEN, IS NULL
- [ ] ORDER BY, LIMIT / TOP
- [ ] Constraints (PK, FK, UNIQUE, NOT NULL, CHECK, DEFAULT)
- [ ] DDL / DML
- [ ] Aggregates + GROUP BY + HAVING + WHERE vs HAVING
- [ ] Joins: INNER, LEFT, RIGHT, SELF, CROSS
- [ ] LEFT JOIN + `IS NULL` (unmatched rows)
- [ ] Subqueries, EXISTS, correlated
- [ ] UNION vs UNION ALL, INTERSECT, EXCEPT
- [ ] CASE, COALESCE / IFNULL
- [ ] String aur Date functions
- [ ] Window functions
- [ ] CTE
- [ ] Views, Indexes, Stored Procedures

## 🔥 Classic Interview Questions

- 2nd / Nth highest salary
- Duplicate rows dhoondna
- Department-wise max salary
- Employee jo manager se zyada kamata hai (self join)
- Customer jisne kabhi order nahi kiya (LEFT JOIN + `IS NULL`)
- Top N per group (window function)
- Running total aur month-wise growth

---

## 🔀 MySQL vs SQL Server (syntax farak)

| | MySQL | SQL Server |
|---|---|---|
| Rows limit | `LIMIT 5` | `SELECT TOP 5` |
| Current time | `NOW()` | `GETDATE()` |
| Null replace | `IFNULL(col, 0)` | `ISNULL(col, 0)` |
| Start transaction | `START TRANSACTION;` | `BEGIN TRANSACTION;` |
| Savepoint | `SAVEPOINT sp1;` | `SAVE TRANSACTION sp1;` |

LeetCode par MySQL select karke practice karo. Interview mein jo DB bole, uska syntax use karo.

---

## 🗂️ Repo Structure

```
sql-notes/
├── README.md
├── mistake-log.md
├── 01-SQLBolt-Lessons/
├── 02-Gap-Topics/
├── 03-LeetCode-SQL-50/
├── 04-Interview-QA/
└── .github/            # progress automation
```

## 🔗 Resources

| Purpose | Link |
|---|---|
| Interactive concept | [SQLBolt](https://sqlbolt.com) |
| Practice | [LeetCode SQL 50](https://leetcode.com/studyplan/top-sql-50/) |
| Syntax reference | [W3Schools SQL](https://www.w3schools.com/sql/) |
| Window functions | [Mode SQL Tutorial](https://mode.com/sql-tutorial/) |
| Theory + MCQs | [GFG SQL Tutorial](https://www.geeksforgeeks.org/sql/sql-tutorial/) |

---

<div align="center">

⭐ **Consistency > Intensity** · Roz ek lesson, roz kuch problems ⭐

</div>
