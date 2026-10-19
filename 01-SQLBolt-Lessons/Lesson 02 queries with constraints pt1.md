# SQL Lesson 2: Queries with constraints (Pt. 1)

## 1. Problem kya hai?

Lesson 1 mein `SELECT` se columns chunna seekha. Lekin agar table mein **10 crore rows** hon, toh saari rows padhna slow bhi hai aur kaam ka bhi nahi. Humein sirf **kaam ki rows** chahiye.

**Solution: `WHERE` clause.** Yeh **har row ko check** karta hai: "Kya yeh row meri condition poori karti hai?" Haan toh result mein aayegi, nahi toh bahar.

**Real-life example:** Class ke register mein se sirf wo students dhoondhna jinke marks 70 se zyada hain.

---

## 2. Formula

```sql
SELECT column1, column2
FROM table_name
WHERE condition
  AND / OR another_condition;
```

| Keyword | Kaam |
|---|---|
| `SELECT` | **Kaun se columns** |
| `FROM` | **Kaunsa table** |
| `WHERE` | **Kaun si rows** (filter) |

**Technical term:** `WHERE` ek **clause** hai, aur jo condition likhte hain use **predicate** ya **constraint** kehte hain.

---

## 3. Operators (numbers ke liye)

| Operator | Matlab | Example |
|---|---|---|
| `=` | Barabar | `marks = 80` |
| `!=` ya `<>` | Barabar nahi | `marks != 80` |
| `<` , `<=` | Chhota, chhota ya barabar | `marks < 70` |
| `>` , `>=` | Bada, bada ya barabar | `marks >= 70` |
| `BETWEEN a AND b` | a aur b ke beech (**dono shamil**) | `marks BETWEEN 60 AND 80` |
| `NOT BETWEEN a AND b` | Range ke **bahar** | `marks NOT BETWEEN 60 AND 80` |
| `IN (...)` | List mein se koi ek | `marks IN (40, 70, 90)` |
| `NOT IN (...)` | List mein se koi nahi | `marks NOT IN (40, 70, 90)` |
| `AND` | **Dono** conditions true | `A AND B` |
| `OR` | **Koi ek** condition true | `A OR B` |

⚠️ SQL mein barabar ke liye **single `=`** hota hai, `==` nahi (jo C/Java/Python mein hota hai).

---

## 4. Examples

Table `students`:

| id | name | dept | marks |
|---|---|---|---|
| 1 | Rahul | CSE | 80 |
| 2 | Priya | ECE | 90 |
| 3 | Amit | CSE | 70 |
| 4 | Neha | ME | 60 |
| 5 | Karan | ECE | 40 |

### A. Simple condition

```sql
SELECT name, marks
FROM students
WHERE marks > 70;
```
Har row check hui: 80 > 70 ✅, 90 > 70 ✅, 70 > 70 ❌ (barabar hai, bada nahi), 60 ❌, 40 ❌.

| name | marks |
|---|---|
| Rahul | 80 |
| Priya | 90 |

### B. AND (dono sahi hone chahiye)

```sql
SELECT name
FROM students
WHERE dept = 'CSE' AND marks >= 70;
```
Rahul (CSE, 80) ✅, Amit (CSE, 70) ✅. Priya CSE nahi hai ❌.

| name |
|---|
| Rahul |
| Amit |

> Text (`'CSE'`) ko **single quotes** mein likhte hain. Numbers ko quotes nahi chahiye. Text ka detail Lesson 3 mein.

### C. OR (koi ek sahi ho)

```sql
SELECT name
FROM students
WHERE dept = 'ECE' OR marks >= 80;
```
Rahul (marks 80 ✅), Priya (ECE ✅), Karan (ECE ✅).

| name |
|---|
| Rahul |
| Priya |
| Karan |

### D. BETWEEN (dono ends shamil)

```sql
SELECT name, marks
FROM students
WHERE marks BETWEEN 60 AND 80;
```
60 aur 80 dono **include** hote hain.

| name | marks |
|---|---|
| Rahul | 80 |
| Amit | 70 |
| Neha | 60 |

`BETWEEN 60 AND 80` bilkul `marks >= 60 AND marks <= 80` ke barabar hai.

### E. NOT BETWEEN

```sql
SELECT name, marks
FROM students
WHERE marks NOT BETWEEN 60 AND 80;
```
Jo range ke **bahar** hain: 90 aur 40. (60 aur 80 range mein the, isliye wo nahi aate.)

| name | marks |
|---|---|
| Priya | 90 |
| Karan | 40 |

### F. IN aur NOT IN

```sql
SELECT name FROM students WHERE marks IN (40, 70, 90);
```
Result: Priya (90), Amit (70), Karan (40).

```sql
SELECT name FROM students WHERE marks NOT IN (40, 70, 90);
```
Result: Rahul (80), Neha (60).

`IN` ek chhota shortcut hai. `marks IN (40, 70, 90)` ka matlab `marks = 40 OR marks = 70 OR marks = 90`.

### G. Not equal

```sql
SELECT name FROM students WHERE dept != 'CSE';
```
Result: Priya, Neha, Karan.

---

## 5. 🚨 Sabse important: AND aur OR ki priority

SQL mein **AND pehle chalta hai, OR baad mein** (jaise math mein × pehle, + baad mein). Isliye brackets zaroori ho jaate hain.

**Query 1 (bina bracket):**
```sql
SELECT name FROM students
WHERE dept = 'CSE' OR dept = 'ECE' AND marks >= 80;
```
SQL ise aise padhta hai: `dept = 'CSE'` **OR** `(dept = 'ECE' AND marks >= 80)`

- CSE wale sab: Rahul, Amit
- ECE aur marks >= 80: Priya

**Result: Rahul, Amit, Priya**

**Query 2 (bracket ke saath):**
```sql
SELECT name FROM students
WHERE (dept = 'CSE' OR dept = 'ECE') AND marks >= 80;
```
Pehle bracket: CSE ya ECE (Rahul, Priya, Amit, Karan), phir unme se marks >= 80.

**Result: Rahul, Priya**

Dono ka result alag hai. **Jab AND aur OR saath ho, toh bracket lagao.** Interview aur MCQ dono mein yeh trap aata hai.

**Priority order:** `NOT` > `AND` > `OR`

---

## 6. Query kaise solve karein (step by step)

1. **Table kaunsa?** → `FROM`
2. **Kaun se columns dikhane hain?** → `SELECT`
3. **Kaun si rows chahiye?** → `WHERE` mein condition likho
4. Condition mein **AND/OR** hai? Toh bracket socho.
5. "Range" hai toh `BETWEEN`, "list" hai toh `IN`.

**Query ka execution order (basic):** pehle `FROM` (table uthao), phir `WHERE` (rows filter karo), phir `SELECT` (columns nikalo). Isliye `WHERE` mein wo column bhi use kar sakte ho jo `SELECT` mein nahi hai.

---

## 7. Common mistakes 🚨

| Galti | Galat | Sahi |
|---|---|---|
| `==` use karna | `WHERE marks == 80` ❌ | `WHERE marks = 80` ✅ |
| BETWEEN mein order ulta | `BETWEEN 80 AND 60` ❌ (khaali result) | `BETWEEN 60 AND 80` ✅ |
| Bracket bhoolna (AND/OR mix) | Galat result milta hai | Bracket lagao |
| BETWEEN ko exclusive samajhna | 60 aur 80 nahi aayenge sochna ❌ | Dono **include** hote hain |
| `NOT BETWEEN` mein ends | Ends include maan lena ❌ | Ends **bahar** hote hain, `BETWEEN` mein the |
| Text par quotes na lagana | `WHERE dept = CSE` ❌ | `WHERE dept = 'CSE'` ✅ |

---

## 8. Interview / MCQ traps

1. **`BETWEEN` inclusive hai** (dono ends shamil). Yeh MCQ mein bahut aata hai.
2. **`BETWEEN 80 AND 60`** (bada pehle) khaali result deta hai, error nahi.
3. **AND ki priority OR se zyada hai**, isliye bracket ka use.
4. **`NOT IN` aur NULL:** agar list mein `NULL` ho, toh `NOT IN` koi row nahi deta. Aur `col != 4` wali condition mein jinki value `NULL` hai wo rows bhi nahi aati. Iska detail **Lesson 8 (NULLs)** mein aayega, abhi bas yaad rakho.
5. `!=` aur `<>` dono "not equal" hain (`<>` standard SQL hai, `!=` zyada tar DBs mein chalta hai).
6. **`WHERE` rows filter karta hai.** Groups par condition `HAVING` se lagti hai (aage padhenge).

---

## 9. SQLBolt Exercise 2: tareeka (movies table)

Columns: `id, title, director, year, length_minutes`

| Task | Soch |
|---|---|
| Row id 6 wali movie | Ek column (`id`) par barabar ki condition |
| 2000 se 2010 ke beech ki movies | `year` par range. Dono ends shamil hain |
| 2000 se 2010 ke beech **nahi** | Upar wale ka ulta. Ends ka dhyan rakho |
| Pehli 5 movies aur unka year | Sirf `title`, `year` columns. `id` par ek condition (pehli 5 movies ki id kya hain?) |

**Pehle khud likhke SQLBolt mein try karo.**

---

## 10. Quick revision

1. `WHERE` = **rows ka filter**.
2. `BETWEEN` = **dono ends shamil**.
3. `IN` = list mein se koi ek. Yeh `OR` ka shortcut hai.
4. **AND pehle, OR baad mein.** Mix ho toh bracket lagao.
5. Text par single quotes, equals ke liye single `=`.

---

## 11. Quick quiz

**Q1.** `students` table se un students ke naam dikhao jinke marks 60 se zyada hain. Query likho.

**Q2.** `marks BETWEEN 60 AND 80` mein kya 60 aur 80 aate hain?

**Q3.** `marks IN (40, 70, 90)` ko `OR` se likho.

**Q4.** Table: `students` (upar wala). Is query ka output kya hoga?
```sql
SELECT name FROM students
WHERE dept = 'ECE' AND marks > 50;
```

**Q5.** In dono mein farak kya hai aur result kya aayega?
```sql
-- (i)
WHERE dept = 'CSE' OR dept = 'ECE' AND marks >= 80
-- (ii)
WHERE (dept = 'CSE' OR dept = 'ECE') AND marks >= 80
```

**Q6.** `WHERE marks NOT BETWEEN 60 AND 80` ko `>` / `<` aur `OR` se likho.
