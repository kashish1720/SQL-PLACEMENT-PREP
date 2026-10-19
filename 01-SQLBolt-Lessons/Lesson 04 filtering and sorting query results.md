# SQL Lesson 4: Filtering and sorting Query results

## 1. Problem kya hai?

Table ka data unique ho sakta hai, lekin **query ka result unique nahi hota**. Aur result ka koi **order** bhi nahi hota. Teen problems:

| Problem | Example | Solution |
|---|---|---|
| Result mein **duplicates** | 100 movies mein se director ke naam repeat | `DISTINCT` |
| Result **bikhra hua** (koi order nahi) | Marks ki list random order mein | `ORDER BY` |
| Result **bahut bada** | Sirf top 5 chahiye, ya page 2 ke results | `LIMIT` aur `OFFSET` |

**Real-life example:** Flipkart pe "price low to high" (ORDER BY), ek page par sirf 20 products (LIMIT), "next page" dabao (OFFSET).

---

## 2. DISTINCT: duplicates hatao

```sql
SELECT DISTINCT column1, column2
FROM table_name
WHERE condition;
```

`DISTINCT` result ki **duplicate rows** hata deta hai. Original table ko badalta nahi, sirf output se hataata hai.

⚠️ Dhyan do: `DISTINCT` **poori row** (jitne columns SELECT mein likhe) ka combination dekhta hai, sirf pehle column ka nahi.

---

## 3. ORDER BY: result sort karo

```sql
SELECT column1, column2
FROM table_name
WHERE condition
ORDER BY column ASC / DESC;
```

| Keyword | Matlab | Numbers | Text |
|---|---|---|---|
| `ASC` | **Ascending** (default, likhna zaroori nahi) | Chhota → Bada (1, 2, 3) | A → Z |
| `DESC` | **Descending** | Bada → Chhota (3, 2, 1) | Z → A |

**Multiple columns se sort:** pehle column se sort hota hai, aur jahan **tie** ho wahan doosre column se.
```sql
ORDER BY marks DESC, name ASC
```

---

## 4. LIMIT aur OFFSET: sirf kuch rows lo

```sql
SELECT column1, column2
FROM table_name
WHERE condition
ORDER BY column ASC / DESC
LIMIT num_limit OFFSET num_offset;
```

| Keyword | Matlab | Yaad rakhne ka tareeka |
|---|---|---|
| `LIMIT n` | **Kitni** rows chahiye | "Maximum n rows do" |
| `OFFSET m` | **Kitni rows chhodni** hain (skip) | "Pehli m rows chhod ke shuru karo" |

**Real-life example:** Kitaab ke pages. `LIMIT 10` = 10 pages padho. `OFFSET 20` = pehle 20 pages chhod do.

### Pagination formula (interview mein puchhta hai)

```
OFFSET = (page_number - 1) × page_size
```
Page size 3 ho toh: Page 1 → `OFFSET 0`, Page 2 → `OFFSET 3`, Page 3 → `OFFSET 6`.

---

## 5. Examples

Table `students`:

| id | name | dept | marks |
|---|---|---|---|
| 1 | Rahul | CSE | 80 |
| 2 | Priya | ECE | 90 |
| 3 | Amit | CSE | 70 |
| 4 | Neha | ME | 60 |
| 5 | Karan | ECE | 70 |
| 6 | Rohan | CSE | 90 |
| 7 | Ankita | ME | 85 |

### A. DISTINCT (ek column)

```sql
SELECT DISTINCT dept FROM students;
```
Bina `DISTINCT` ke 7 rows aati (CSE 3 baar, ECE 2 baar, ME 2 baar). Ab:

| dept |
|---|
| CSE |
| ECE |
| ME |

### B. DISTINCT (do columns ka combination)

```sql
SELECT DISTINCT dept, marks FROM students;
```
Row tabhi duplicate hai jab **dept aur marks dono same** hon. `(CSE, 70)` aur `(ECE, 70)` ka marks same hai lekin dept alag hai, isliye **dono rakhi jaati hain**. Is table mein saari 7 combinations alag hain, isliye 7 rows aati hain.

### C. ORDER BY (descending)

```sql
SELECT name, marks FROM students ORDER BY marks DESC;
```

| name | marks |
|---|---|
| Priya | 90 |
| Rohan | 90 |
| Ankita | 85 |
| Rahul | 80 |
| Amit | 70 |
| Karan | 70 |
| Neha | 60 |

⚠️ Priya aur Rohan dono ke marks 90 hain. Inka **order guaranteed nahi** hai (Rohan pehle bhi aa sakta hai). Ise fix karne ke liye doosra column lagao.

### D. Multiple columns (tie-break)

```sql
SELECT name, marks FROM students ORDER BY marks DESC, name ASC;
```
Pehle marks se (bada → chhota), aur jahan marks same hon wahan naam se (A → Z). Ab **Priya hamesha Rohan se pehle** aayegi, aur **Amit hamesha Karan se pehle**.

### E. LIMIT (top N)

```sql
SELECT name, marks FROM students ORDER BY marks DESC, name LIMIT 3;
```

| name | marks |
|---|---|
| Priya | 90 |
| Rohan | 90 |
| Ankita | 85 |

### F. LIMIT + OFFSET (pagination, page size 3)

```sql
-- Page 2
SELECT name, marks FROM students
ORDER BY marks DESC, name
LIMIT 3 OFFSET 3;
```
Sorted list: Priya, Rohan, Ankita, **Rahul, Amit, Karan**, Neha. Pehle 3 skip, agle 3 lo:

| name | marks |
|---|---|
| Rahul | 80 |
| Amit | 70 |
| Karan | 70 |

Page 3 (`OFFSET 6`) mein sirf **Neha** aayegi (sirf ek row bachi hai).

### G. Sabka combination: 2nd highest marks

```sql
SELECT DISTINCT marks
FROM students
ORDER BY marks DESC
LIMIT 1 OFFSET 1;
```
`DISTINCT marks` → 90, 85, 80, 70, 60 (descending). Pehli 1 skip (90), agli 1 lo → **85**.

Bina `DISTINCT` ke result **90** aata (kyunki 90 do baar hai, doosri row bhi 90). Isliye "2nd highest" mein `DISTINCT` ka dhyan rakho.

---

## 6. SQL Server mein syntax alag hai (aapne use kiya hai, yaad rakho)

SQL Server mein `LIMIT` nahi hota.

| Kaam | MySQL | SQL Server |
|---|---|---|
| Top 3 rows | `... ORDER BY marks DESC LIMIT 3;` | `SELECT TOP 3 name, marks FROM students ORDER BY marks DESC;` |
| Skip 3, agli 3 | `... LIMIT 3 OFFSET 3;` | `... ORDER BY marks DESC OFFSET 3 ROWS FETCH NEXT 3 ROWS ONLY;` |

- SQL Server mein `OFFSET ... FETCH` ke liye **`ORDER BY` zaroori hai**.
- MySQL mein `LIMIT 3, 5` ka matlab **"offset 3, count 5"** hota hai (order ulta lagta hai). Confusion se bachne ke liye `LIMIT 5 OFFSET 3` likhna safe hai.

---

## 7. Query ka execution order (important)

SQL query ko aise **padhta nahi**, jaise likhte ho. Asli order:

```
1. FROM       → table uthao
2. WHERE      → rows filter karo
3. SELECT     → columns nikalo
4. DISTINCT   → duplicates hatao
5. ORDER BY   → sort karo
6. LIMIT/OFFSET → sirf kuch rows lo (sabse last)
```

**Isse kya samajh aata hai:**
- `LIMIT` **sabse aakhir mein** lagta hai, isliye pehle sort hota hai, phir top N milte hain.
- `ORDER BY` `SELECT` ke baad chalta hai, isliye wahan **alias** (jaise `marks AS m`) use kar sakte ho. `WHERE` mein nahi (kyunki `WHERE` SELECT se pehle chalta hai).

(Lesson 12 mein iska poora detail aayega.)

---

## 8. Query solve karne ka tareeka

Question padhke yeh poochho:

| Sawaal | Kya lagana hai |
|---|---|
| "Unique / bina duplicate" bola hai? | `DISTINCT` |
| "Sorted / alphabetically / highest se lowest" bola hai? | `ORDER BY` (+ `ASC`/`DESC`) |
| "Top N / first N / last N" bola hai? | `ORDER BY` + `LIMIT N` |
| "Next N / page 2" bola hai? | `LIMIT` + `OFFSET` |
| "Last N" (jaise last 4 released) | **Ulta sort** (`DESC`) karke `LIMIT N` |

---

## 9. Common mistakes 🚨

| Galti | Galat | Sahi |
|---|---|---|
| `DISTINCT` ko column ke baad likhna | `SELECT director DISTINCT` ❌ | `SELECT DISTINCT director` ✅ (SELECT ke turant baad) |
| `ORDER BY` bina likhe `LIMIT` | `LIMIT 5` ❌ (kaunsi 5 rows? koi guarantee nahi) | `ORDER BY ... LIMIT 5` ✅ |
| `ORDER BY` ko `WHERE` se pehle likhna | `ORDER BY year WHERE ...` ❌ | `WHERE ... ORDER BY year` ✅ |
| Last N ke liye `ASC` use karna | Sabse purani aati hain ❌ | `DESC` + `LIMIT N` ✅ |
| `LIMIT` ko `ORDER BY` se pehle likhna | ❌ Syntax error | `ORDER BY` pehle, `LIMIT` baad mein |

---

## 10. Interview / MCQ traps

1. **`DISTINCT` poori row ke combination par kaam karta hai**, sirf pehle column par nahi. `DISTINCT a, b` ka matlab `(a, b)` ki unique pairs.
2. **`ORDER BY` ke bina result ka order guaranteed nahi hota.** Kabhi lagta hai ki insertion ke order mein aa raha hai, par database kuch bhi order de sakta hai. `LIMIT` ke saath `ORDER BY` hamesha lagao.
3. **Default sorting `ASC` hai.**
4. **NULL ki sorting DB par depend karti hai:** MySQL aur SQL Server mein `ASC` sort mein `NULL` **pehle** aate hain. PostgreSQL aur Oracle mein **baad mein**.
5. **Pagination formula:** `OFFSET = (page - 1) × page_size`.
6. **`DISTINCT` mein `NULL`** ko ek hi value maana jaata hai (do NULL rows mein se ek bachti hai).
7. `ORDER BY` mein **column number** bhi de sakte ho (`ORDER BY 2` = SELECT list ka doosra column), lekin yeh achhi practice nahi mani jaati.
8. **Nth highest salary ka classic answer:**
   ```sql
   SELECT DISTINCT salary FROM employees
   ORDER BY salary DESC
   LIMIT 1 OFFSET N-1;
   ```
   Ismein `DISTINCT` isliye hai ki same salary wale log ek hi rank par ginte hain. (Isko window functions se bhi karte hain, aage aayega.)
9. **`DISTINCT` vs `GROUP BY`:** dono duplicates hata sakte hain, lekin `GROUP BY` aggregates (COUNT, SUM) ke saath use hota hai. SQLBolt kehta hai ki specific columns ke basis par duplicates hataane ke liye aage `GROUP BY` seekhenge.

---

## 11. SQLBolt Exercise 4: tareeka (movies table)

Is lesson mein table ka data **scrambled** hai (random order mein). Columns: `id, title, director, year, length_minutes`.

| Task | Soch (jawab nahi diya, khud likho) |
|---|---|
| Pixar movies ke saare directors, alphabetically, bina duplicate | Kaunsa column? Duplicate hatana hai (`DISTINCT`), A → Z (`ORDER BY`) |
| Last 4 movies released (sabse nayi pehle) | Kis column se sort? Sabse nayi pehle matlab `ASC` ya `DESC`? Phir kitni rows? |
| Alphabetically pehli 5 movies | Kis column se sort? Kitni rows? |
| Alphabetically agli 5 movies | Upar wale ki tarah, lekin pehli 5 **skip** karni hain |

---

## 12. Quick revision

1. `DISTINCT` = duplicates hatao (poori row ke combination par).
2. `ORDER BY` = sort. Default `ASC`.
3. `LIMIT n` = n rows. `OFFSET m` = pehli m rows skip.
4. **Hamesha `ORDER BY` ke saath `LIMIT`** lagao.
5. Clause ka order: `SELECT DISTINCT ... FROM ... WHERE ... ORDER BY ... LIMIT ... OFFSET ...`
6. `LIMIT` sabse aakhir mein chalta hai.
7. SQL Server mein `TOP` ya `OFFSET ... FETCH`, MySQL mein `LIMIT`.

---

## 13. Quick quiz

**Q1.** `students` table se unique departments ki list dikhane ki query likho.

**Q2.** Un 3 students ke naam dikhao jinke marks sabse zyada hain. (Table upar wala hai.)

**Q3.** Page size 5 ho toh page 4 ke liye `OFFSET` kitna hoga?

**Q4.** `SELECT DISTINCT dept, marks FROM students;` mein `(CSE, 70)` aur `(ECE, 70)` duplicate maane jaayenge ya nahi? Kyun?

**Q5.** Is query mein galti kya hai?
```sql
SELECT name FROM students LIMIT 3 ORDER BY marks DESC;
```

**Q6.** "2nd highest marks" nikalne ki query likho. `DISTINCT` kyun lagaya?

---

## ✍️ My Practice: SQLBolt Exercise 4

*(Exercise solve karne ke baad meri queries, mistakes aur improved solutions yahan add karunga.)*
Apni 3 aadatein sudharni hain
Jo columns task mein maange hain, sirf wahi SELECT karo.
DISTINCT tabhi lagao jab duplicates sach mein aa sakte hon, aur uske saath extra column mat jodo.
ORDER BY mein jis column se sort karna hai wahi likho, extra column mat daalo.
