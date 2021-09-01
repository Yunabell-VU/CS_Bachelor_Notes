# Database SQL

----------

## Basic SQL Syntax

```SQL
select Attribute1, ..., AttributeN
from   Table1, ..., TableM
where  Condition
```

![image_1f6nk72r9eguqbn1qou17ik11pk9.png-7.8kB](http://yunabell-image-repository.oss-cn-shanghai.aliyuncs.com/img/image_1f6nk72r9eguqbn1qou17ik11pk9.png)  

> Write your first SQL query

```SQL
select address
from   Students
```

> Last names of all students with first name George

```SQL
select last
from   Students
where  first = 'George'
```

### Attribute References

The first name of students with last name "Orwell":

```SQL
select first
from   Students S
where  S.last = 'Orwell'

select Students.first
from   Students
where  Students.last = 'Simpson'
```


----------

## Joins of multiple tables

```SQL
select *
from   Table1 X, Table2 Y
where  X.attributeA = Y.attributeB
```

**Joining three tables**

We now query all results of George Orwell. In addition, for each exercise we want the maximum number of points that was possible for each exercise. To this end we need to join the tables Students, Results and Exercises.

```SQL
select S.first, S.last, E.category, E.number, R.points, E.maxPoints
from   Students S, Results R, Exercises E
where  S.sid = R.sid                                   -- join condition for S-R
   and R.category = E.category and R.number = E.number -- join condition for R-E
   and S.first = 'George' and S.last = 'Orwell'
```

> **Persons who take classes**  
![image_1f6nknhhc1i3ripicl41bp8g8um.png-42.1kB](http://yunabell-image-repository.oss-cn-shanghai.aliyuncs.com/img/image_1f6nknhhc1i3ripicl41bp8g8um.png)  

```SQL
select P.name, C.kind
from Persons P, Classes C, TakesClasses T
where P.id = T.person_id and C.id = T.class_id
```


----------

### Self-joins

> **All students that have 9 points in homework 1 and 2**

```SQL
select S.first, S.last
from   Students S, Results R1, Results R2
where  S.sid = R1.sid
   and S.sid = R2.sid
   and R1.category = 'homework' AND R1.number = 1
   and R2.category = 'homework' AND R2.number = 2
   and R1.points >= 9 AND R2.points >= 9
```

> **All students that have solved at least two exercises**

```SQL
select S.first, S.last
from   Students S, Results R1, Results R2
where  S.sid = R1.sid
   and S.sid = R2.sid
   and (R1.category <> R2.category OR R1.number <> R2.number)
```

> **Persons who like someone with blue eyes**  

![image_1f6nl5msq1s71osp1p031plfvip13.png-26.8kB](http://yunabell-image-repository.oss-cn-shanghai.aliyuncs.com/img/image_1f6nl5msq1s71osp1p031plfvip13.png)  

```SQL
select distinct Pa.name
from Persons Pa, Persons Pb, Likes L
where Pb.eyeColor = 'blue'
    and L.personB_id = Pb.id 
    and Pa.id = L.personA_id
```

> **Persons who like two people with green eyes**

```SQL
select distinct Pa.name
from Persons Pa, Likes L1, Likes L2
where Pa.id = L1.personA_id
    and Pa.id = L2.personA_id
    and L1.personB_id IN (select Pb.id from Persons Pb where Pb.eyeColor = 'green')
    and L2.personB_id IN (select Pb.id from Persons Pb where Pb.eyeColor = 'green')
    and L1.personB_id <> L2.personB_id
```

> **Men that play soccer in mixed teams**  

![image_1f6nm1h031h2e2ua10me12u1fao1g.png-50.6kB](http://yunabell-image-repository.oss-cn-shanghai.aliyuncs.com/img/image_1f6nm1h031h2e2ua10me12u1fao1g.png)  

```SQL
select distinct Pm.name
from Persons Pm, Persons Pf, SportTogether S1
where Pm.gender = 'male'
    and Pf.gender = 'female'
    and S1.sport = 'soccer'
    and ((S1.personA_id = Pm.id and S1.personB_id = Pf.id ) or (S1.personA_id = Pf.id and S1.personB_id = Pm.id))
```


----------

### Duplicate elimination

```SQL
select distinct address
from   Students
```

> **Last names without duplicates**

```SQL
select distinct last
from Students
```


----------

### Inner and outer joins

When joining two tables in SQL, by default only those rows will be returned that participate in some match.

For the case that we also want to include all students in the result, SQL offers special join operations:

- left [outer] join: preserves rows of left table

- right [outer] join: preserves rows of right table

- full [outer] join: preserves rows of both tables

- [inner] join: the usual join (rows without match are not included)

- cross join: Cartesian product (all combinations)

**For example:**
```SQL
SELECT A.name, B.name
FROM   TableA A LEFT JOIN TableB B
    ON A.id = B.id
```

> **All students and their results**

```SQL
SELECT first, last, points
FROM   Students S LEFT JOIN Results R
    ON S.sid = R.sid
```

> **People that do not like anyone**  
![image_1f6nno0s31ivs51u1nm23qr1e321t.png-34kB](http://yunabell-image-repository.oss-cn-shanghai.aliyuncs.com/img/image_1f6nno0s31ivs51u1nm23qr1e321t.png)  

```SQL
select Pa.name 
from Persons Pa left outer join Likes L
on Pa.id = L.personA_id 
where personA_id IS NULL
// group by Pa.name
```

----------

## Monotonic and non-monotonic queries

> **all students who have not submitted any homework**

```SQL
SELECT first, last
FROM   Students S
WHERE  S.sid NOT IN (SELECT sid FROM Results)
```

### IN and NOT IN

```SQL
SELECT ...
FROM   Table
WHERE  attributeX IN (SELECT attributeY FROM ...)

SELECT ...
FROM   Table
WHERE  attributeX NOT IN (SELECT attributeY FROM ...)

//SQL also allows to check whether a tuple occurs (or does not occur) in a subquery:

WHERE (A,B) NOT IN (SELECT C,D FROM . . . )
```

> **Students without any homework result**

```SQL
SELECT first, last
FROM   Students
WHERE  sid NOT IN (SELECT sid
                   FROM   Results
                   WHERE  category = "homework")
```

> **All persons that do not take any classes**  
![image_1f6noak9n2np1qv31dnr1i9c1sdc2q.png-28.6kB](http://yunabell-image-repository.oss-cn-shanghai.aliyuncs.com/img/image_1f6noak9n2np1qv31dnr1i9c1sdc2q.png)  

```SQL
select Pa.name
from Persons Pa
where Pa.id NOT IN (select person_id from TakesClasses)
```

>**All persons that do not know anyone who takes classes**  
![image_1f6noc0ottvt1rf9lse1d3nst537.png-40.3kB](http://yunabell-image-repository.oss-cn-shanghai.aliyuncs.com/img/image_1f6noc0ottvt1rf9lse1d3nst537.png)  

```SQL
select Pa.name
from Persons Pa
where Pa.id NOT IN (select personA_id from Knows where personB_id IN (select person_id from TakesClasses) )
```


----------


### EXISTS and NOT EXISTS

The construct EXISTS and NOT EXISTS enables the main (or outer) query to check whether the subquery result is empty:

- `EXISTS` is true if the subquery is **not empty**

- `NOT EXISTS` is true if the subquery is **empty**

> **Students that have submitted any homework**

```SQL
SELECT first, last
FROM   Students S
WHERE  EXISTS (SELECT *
               FROM   Results R
               WHERE  R.category = "homework"
               AND    R.sid = S.sid)
```

> **The oldest people**  
![image_1f6np3qhc1fs11og3qj683g1bb53k.png-24.6kB](http://yunabell-image-repository.oss-cn-shanghai.aliyuncs.com/img/image_1f6np3qhc1fs11og3qj683g1bb53k.png)  

```SQL
SELECT Pa.name
FROM   Persons Pa
WHERE  NOT EXISTS (SELECT *
               FROM   Persons Pb
               WHERE  Pb.age > Pa.age)
```

>**People that like everyone they know**  
![image_1f6np7orbs6ej6c1plg16pd109r41.png-35.7kB](http://yunabell-image-repository.oss-cn-shanghai.aliyuncs.com/img/image_1f6np7orbs6ej6c1plg16pd109r41.png)  

```SQL
select P.name
from Persons P
where not exists (select K.personA_id
                    from Knows K
                    where K.personB_id not in (select L.personB_id
                                                from Likes L
                                                where L.personA_id = K.personA_id)
                    and K.personA_id = P.id)
```

----------

### For All

SQL does not offer a universal quantifier ∀, thus, one cannot use "for all” directly in a query.

However, as we have seen in the logic recap, `FOR ALL` can be expressed using the existential quantifier `EXISTS`.

> **Who got the best result for homework 1?**  
![image_1f6nps9kb1qsn1q2c7v61m5s1lvr4e.png-24kB](http://yunabell-image-repository.oss-cn-shanghai.aliyuncs.com/img/image_1f6nps9kb1qsn1q2c7v61m5s1lvr4e.png)  

```SQL
SELECT   first, last, points
FROM     Students S, Results X
WHERE    S.sid = X.sid
AND      X.category = "homework" AND X.number = 1
AND      NOT EXISTS
         (SELECT *
          FROM   Results Y
          WHERE  Y.category = "homework" AND Y.number = 1
          AND    Y.points > X.points)
```

> **People that are older than everybody they know **  
>
> ![image_1f6npuq4t3u9dd2leapqses4r.png-26kB](http://yunabell-image-repository.oss-cn-shanghai.aliyuncs.com/img/image_1f6npuq4t3u9dd2leapqses4r.png)  
> 

```SQL
select name
from Persons
where name not in
    (select Pa.name
    from Persons Pb, Persons Pa, Knows K
    where K.personA_id = Pa.id
    and Pb.id = K.personB_id 
    and (Pa.age - Pb.age) <= 5)

//NOT EXISTS
select P.name
from Persons P
where NOT EXISTS
    (select Pa.name
    from Persons Pb, Persons Pa, Knows K
    where K.personA_id = Pa.id
    and Pb.id = K.personB_id 
    and (Pa.age - Pb.age) <= 5
    and Pa.name = P.name)
```


#### Implication

![image_1f6nq7imq1tks9c119q6l6jklf58.png-53kB](http://yunabell-image-repository.oss-cn-shanghai.aliyuncs.com/img/image_1f6nq7imq1tks9c119q6l6jklf58.png)  

----------

### All, Any, Some

```SQL
SELECT ...
FROM ...
WHERE attribute COMPARISON ALL/SOME (select ...)
```

Here `COMPARISON` is a comparison operator; for example `>`, `>=`, `=`…​

The `ALL` comparison is universal, while `ANY` is existential. For example:

- `nr > ALL (select …​)` is true if nr is > than all values returned by the subquery

- `nr > ANY (select …​)` is true if nr is > than at least one value returned by the subquery

> Which student(s) got the maximum points for homework 1?

```SQL
SELECT    S.first, S.last, X.points
FROM      Students S, Results X
WHERE     S.sid = X.sid AND X.category = "homework" AND X.number = 1
AND       X.points >= ALL (SELECT  Y.points
                           FROM    Results Y
                           WHERE   Y.category  = "homework"
                           AND     Y.number = 1)
                           
//or use ANY

SELECT    S.first, S.last, X.points
FROM      Students S, Results X
WHERE     S.sid = X.sid AND X.category = "homework" AND X.number = 1
AND       NOT X.points < ANY (SELECT  Y.points
                              FROM    Results Y
                              WHERE   Y.category = "homework"
                              AND     Y.number = 1)
```

----------

## More nested subqueries

> **List the students who solved all homework assignments**

```SQL
SELECT   first, last
FROM     Students S
WHERE    NOT EXISTS
         (SELECT *
          FROM   Results E
          WHERE  category = "homework"
          AND    NOT EXISTS
                 (SELECT *
                  FROM   Exercises R
                  WHERE  R.sid = S.sid
                  AND    R.number = E.number
                  AND    R.category = "homework"))
```

> **Who got full points for homework 1? ** 
![image_1f6nqv67q1jf09i61jlobcn6e15l.png-24.7kB](http://yunabell-image-repository.oss-cn-shanghai.aliyuncs.com/img/image_1f6nqv67q1jf09i61jlobcn6e15l.png)  

```SQL
SELECT   S.first, S.last
FROM     Students S, Results R
WHERE    S.sid = R.sid AND R.category = "homework" AND R.number = 1
AND      R.points = (SELECT  maxPoints
                     FROM    Exercises
                     WHERE   category = "homework" AND number = 1)
```

> **Points (in %) achieved in homework exercise 1**

```SQL
SELECT  X.sid, (X.points * 100 / X.maxPoints) AS percent
FROM    (SELECT E.category, E.number, R.sid,
                R.points, E.maxPoints
         FROM   Exercises E, Results R
         WHERE  E.category = R.category AND E.number = R.number) X
WHERE   X.category = "homework" AND X.number = 1
```

----------

## Aggregations

We compute minimum of the set of integers {42,57,5,13,27}:

    min{42,57,5,13,27} = 5

SQL defines the five main aggregation functions:

- `COUNT`, computes the number of elements,
- `SUM`, computes the sum over all elements,
- `AVG`, computes the average over all elements,
- `MAX`, computes the maximum of the elements, and
- `MIN`, computes the minimum of the elements.

> **How many students are in the database?**
```SQL
SELECT  COUNT(*)
FROM    Students
```

Keep in mind, the following exceptions:

- COUNT(*) counts null values
- COUNT(*) counts rows, not attribute values

>**Homework points for student 101 plus 3 bonus points.**

```SQL
SELECT  SUM(points) + 3 AS "total points + bonus"
FROM    Results
WHERE   sid = 101 AND category = "homework"
```

>**Best and average result for homework 1?**

```SQL
SELECT  MAX(points), AVG(points)
FROM    Results
WHERE   category = "homework" AND number = 1
```

>**How many students have submitted a homework?**

```SQL
SELECT COUNT(DISTINCT sid)
FROM   Results
WHERE  category = "homework"
```


----------

### GROUP BY

In SQL, the GROUP BY construct partitions the rows (tuples) of a table into disjoint groups.

The syntax is as follows:

```SQL
SELECT    (group by attributes and aggregation functions)
FROM      ...
WHERE     ...
GROUP BY  attributes
```

The execution of the query is as follows:

1. First, the FROM and WHERE clause is evaluated.

2. Afterwards, the GROUP BY partitions the rows/tuples into disjoint groups based on value equality for the GROUP BY attributes. More precisely, all rows that have the same value for all attributes in the GROUP BY clause form one group.

>**Average points for each homework**

```SQL
SELECT    number, AVG(points)
FROM      Results
WHERE     category = "homework"
GROUP BY  number
```

>**Number of classes that a person takes**  
![image_1f6nrtnmcmrr4k216861c0o1amm62.png-27.2kB](http://static.zybuluo.com/Yunabell/rbt82fkq9j6t4h5351j6z4w9/image_1f6nrtnmcmrr4k216861c0o1amm62.png)  

```SQL
select P.name, count(T.person_id) as "nrOfClasses"
from Persons P, TakesClasses T
where P.id = T.person_id
group by P.name
```


----------
### HAVING

> **Only groups of size greater than n tuples**
```SQL
SELECT ...            -- output columns
FROM ...              -- what tuples
WHERE ...             -- filter tuples
GROUP BY ...          -- group tuples
HAVING COUNT(*) > n   -- filter groups
```

**The condition in the HAVING clause may (only) involve aggregation functions.**

> **Which students got at least 18 homework points?**

```SQL
SELECT    first, last
FROM      Students S, Results R
WHERE     S.sid = R.sid AND R.category = "homework"
GROUP BY  S.sid, first, last
HAVING    SUM(points) >= 18
```

> **Rich people**  
![image_1f6ns6fp71u0619vi16ho1gi3et46f.png-29.6kB](http://yunabell-image-repository.oss-cn-shanghai.aliyuncs.com/img/image_1f6ns6fp71u0619vi16ho1gi3et46f.png)  

```SQL
select P.name
from Persons P, AccountOf A, BankAccounts B
where P.id = A.person_id and B.id = A.account_id
group by P.name
having sum(B.balance) >= 1000000
```

>**People that know old people**  
![image_1f6nsbbc19hh1k9r4ur18t91l416s.png-26.3kB](http://yunabell-image-repository.oss-cn-shanghai.aliyuncs.com/img/image_1f6nsbbc19hh1k9r4ur18t91l416s.png)  

```SQL
select Pa.name
from Persons Pa, Knows K, Persons Pb
where Pa.id = K.personA_id and K.personB_id = Pb.id and Pb.age > 60
group by Pa.name
having count(personB_id) = 2
```

>**The poor**  
![image_1f6nsf3pk1q93fne196lqa34h79.png-33.8kB](http://static.zybuluo.com/Yunabell/1z46yujiqzzdudnkotbpg1t5/image_1f6nsf3pk1q93fne196lqa34h79.png)  

```SQL
select P.name
from Persons P left join (AccountOf A left join BankAccounts B on B.id = A.account_id )on P.id = A.person_id
group by P.name
having sum(B.balance) IS NULL 
        or sum(B.balance)*2 
        < (select max(X.bankBalance)
            from (select sum(B.balance) as bankBalance
                        from Persons P, AccountOf A, BankAccounts B
                        where P.id = A.person_id and B.id = A.account_id
                        group by P.name) X)
```


----------

## Sorting output

>**Homework results sorted by exercise (best result first). In case of a tie, sort alphabetically by student name.**

```SQL
SELECT    R.number, R.points, S.first, S.last
FROM      Students S, Results R
WHERE     S.sid = R.sid AND R.category = "homework"
ORDER BY  R.number, R.points DESC, S.last, S.first
```

----------