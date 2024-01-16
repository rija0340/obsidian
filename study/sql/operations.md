### modification de 3 rows

```sql
UPDATE employees
SET salary = 5000
WHERE id IN (1, 2, 3);
```



### modification 3 rows using 3 values 

```sql
UPDATE employees
SET salary = 
    CASE 
        WHEN id = 1 THEN 5000
        WHEN id = 2 THEN 6000
        WHEN id = 3 THEN 7000
    END
WHERE id IN (1, 2, 3);

```

### modification structure d'une table ajout de column 

```sql 
ALTER TABLE employees
ADD COLUMN salary FLOAT(8, 2);
```
