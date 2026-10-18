# SQL Lesson 1: SELECT queries 101

## 1. Pehle basic terms (technical terms ke saath)

| Term | Matlab | Example |
|---|---|---|
| **Query** | Database se data maangne wala sawaal | "Saare students ke naam dikhao" |
| **Statement** | SQL ka ek poora command | `SELECT ... FROM ...;` |
| **Table** | Ek entity ka data (rows + columns) | `students`, `movies` |
| **Row** (record / tuple) | Table mein ek **instance** (ek item) | Ek student, ek movie |
| **Column** (attribute / field) | Sabhi rows ki **common property** | `name`, `age`, `year` |
| **Entity** | Real duniya ki cheez jise table represent karta hai | Student, Movie, Dog |
| **Result set** | Query ka output, jo khud ek chhota table hota hai | Query chalane ke baad jo dikhta hai |

**Yaad rakhne ka tareeka:** Table ko **Excel sheet** samjho. **Column = heading** (Name, Age), **Row = ek line ka data**.

---

## 2. SELECT ka formula

```sql
SELECT column1, column2
FROM table_name;
```

Isse **do sawaalon** ka jawab milta hai:

| Keyword | Sawaal |
|---|---|
| `SELECT` | **Kya** chahiye? (kaun se columns) |
| `FROM` | **Kahan se** chahiye? (kaun sa table) |

Baat bilkul simple hai: **"SELECT kya, FROM kahan se."**

---

## 3. Examples (alag table par, taaki concept clear ho)

Maan lo yeh `students` table hai:

| id | name | dept | marks |
|---|---|---|---|
| 1 | Rahul | CSE | 80 |
| 2 | Priya | ECE | 90 |
| 3 | Amit | CSE | 70 |

### Example A: Ek column

```sql
SELECT name
FROM students;
```
**Output:**

| name |
|---|
| Rahul |
| Priya |
| Amit |

Sirf `name` column aaya, **saari rows** ke saath.

### Example B: Do columns

```sql
SELECT name, marks
FROM students;
```
**Output:**

| name | marks |
|---|---|
| Rahul | 80 |
| Priya | 90 |
| Amit | 70 |

**Dhyan do:** columns ke beech **comma (,)** lagta hai, lekin **aakhri column ke baad comma nahi**.

### Example C: Saare columns (`*`)

```sql
SELECT *
FROM students;
```
`*` ka matlab **"sab kuch"**. Output poora table jaisa hi hoga: `id, name, dept, marks`, saari rows.

### Example D: Order badal do

```sql
SELECT marks, name
FROM students;
```
**Output:**

| marks | name |
|---|---|
| 80 | Rahul |
| 90 | Priya |
| 70 | Amit |

**Concept:** Output mein columns usi **order** mein aate hain jis order mein aapne `SELECT` mein likhe, table ke order mein nahi.

### Example E: Ek hi column do baar

```sql
SELECT name, name
FROM students;
```
Yeh chalta hai, aur column do baar dikhta hai (kam kaam ka hai, bas jaanne ke liye).

---

## 4. Ek query ko kaise padhein (numerical solve karne ka tareeka)

Har question ke liye yeh **3 sawaal** poocho:

1. **Table kaunsa hai?** → `FROM` mein likho.
2. **Kaun se columns chahiye?** → `SELECT` mein likho.
3. **Saare columns chahiye?** → `*` lagao.

**Practice:** Question: *"Students ke naam aur dept dikhao."*
- Table? `students` → `FROM students`
- Columns? `name`, `dept` → `SELECT name, dept`

```sql
SELECT name, dept
FROM students;
```

---

## 5. Zaroori technical baatein

| Baat | Matlab |
|---|---|
| **Keywords case-insensitive hain** | `SELECT`, `select`, `Select` teeno chalte hain. Convention: keywords **CAPITAL** mein likho. |
| **Semicolon (;)** | Statement ka end batata hai. Zyada tar tools mein lagana achhi habit hai. |
| **Multiple lines** | Query kai lines mein likh sakte ho, SQL ko farak nahi padta. `SELECT` aur `FROM` alag lines par likhna readable hota hai. |
| **Column names spelling** | Table ke column ka naam **bilkul sahi** likhna padta hai, warna error aata hai. |
| **Table name case** | MySQL mein Linux par table names **case-sensitive** ho sakte hain, isliye jaisa banaya waisa likho. |

---

## 6. Common mistakes 🚨

| Galti | Galat | Sahi |
|---|---|---|
| Aakhri column ke baad comma | `SELECT name, FROM students;` ❌ | `SELECT name FROM students;` ✅ |
| Comma bhoolna | `SELECT name marks FROM students;` ❌ (error ya **alias** ban jaata hai, aage padhenge) | `SELECT name, marks FROM students;` ✅ |
| `FROM` bhoolna | `SELECT name;` ❌ | `SELECT name FROM students;` ✅ |
| Column ka spelling galat | `SELECT nam FROM students;` ❌ | `SELECT name FROM students;` ✅ |

---

## 7. Interview traps

1. **`SELECT *` real projects mein achha nahi mana jaata.** Kyunki saara data aata hai (zaroorat se zyada), performance par asar padta hai, aur table mein naya column add ho toh output badal jaata hai. Interview mein bolo: "**Sirf zaroori columns select karne chahiye**."
2. **`SELECT` ek table ko badalta nahi.** Yeh sirf data **padhta** hai (DQL), kuch modify nahi karta.
3. Output ek **result set** hota hai, original table ki copy nahi.

---

## 8. Ab SQLBolt ke exercise ke liye

Aapke SQLBolt mein 5 tasks hain. Mainne unke jawab nahi diye, kyunki khud likhoge toh pakka yaad rahega. Sirf **tareeka** dekho:

| Task | Sawaal khud se poocho |
|---|---|
| Sirf title chahiye | Ek column. Kaunsa? |
| Sirf director chahiye | Ek column. Kaunsa? |
| Title **aur** director | Do columns, beech mein comma |
| Title aur year | Do columns, beech mein comma |
| Saari information | `*` |

Table ka naam `movies` hai, aur columns hain: `id, title, director, year, length_minutes`.

**Pehle khud likhke SQLBolt mein try karo.**

---

## 9. Quick quiz

**Q1.** `students` table se sirf `dept` column dikhane ki query likho.

**Q2.** Table ke saare columns dikhane ke liye kya use karte hain?

**Q3.** Is query mein galti kya hai?
```sql
SELECT name, marks, FROM students;
```

**Q4.** `SELECT marks, name FROM students;` aur `SELECT name, marks FROM students;` mein output ka farak kya hoga?

**Q5.** Row aur column ko ek line mein define karo, apne shabdon mein.
