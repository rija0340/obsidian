## sql joins types

https://www.programiz.com/sql/left-join, query et image ensemble dans l'explication donc il est plus simple d’appréhender le concept.


le colonne itovizana , zan oe le clé etrangére sy primaire ao anatin'le table roa no mapifandray azy fa ilay directive Join no mitondra ny affichage anle resultat.

### inner join  = join

jointure entre deux table et le résultat est seulement les éléments de la table 1 qui ont des correspondances (des ids ) dans la tables2 


![[Pasted image 20230609081504.png]]

### left join 

Here, the SQL command selects the `customer_id` and `first_name` columns (from the `Customers` table) and the `amount` column (from the `Orders` table).

The result set will contain those rows where there is a match between `customer_id` (of the `Customers` table) and `customer` (of the `Orders` table), along with all the remaining rows from the `Customers` table.

![[Pasted image 20230609082833.png]]

### right join 

Here, the SQL command selects the `customer_id` and `first_name` columns (from the `Customers` table) and the `amount` column (from the `Orders` table).

And, the result set will contain those rows where there is a match between `customer_id` (of the `Customers` table) and `customer` (of the `Orders` table), along with all the remaining rows from the `Orders` table.

![[Pasted image 20230609083301.png]]

### sql full outer join 

The SQL `FULL OUTER JOIN` statement joins two tables based on a common column. It selects records that have matching values in these columns and the remaining rows from both of the tables.

![[Pasted image 20230609084843.png]]