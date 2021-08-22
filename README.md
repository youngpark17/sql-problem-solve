# sql-problem-solve

## 프로그래머스 우유와 요거트가 담긴 장바구니 - Level4

![](https://i.imgur.com/G31uG0K.png)

```
WITH R AS(
select DISTINCT c.CART_ID as 'id', c.NAME as 'tmp'
from CART_PRODUCTS c
where c.NAME IN ('Yogurt','Milk')
order by id
)
    
select id as "CART_ID" from R
group by id
having count(tmp)>1

```

## 프로그래머스 입양 시각 구하기(2) - Level4

![](https://i.imgur.com/M0aySwJ.png)

테이블에 없는 HOUR 컬럼에 대해서 0으로 select해야해서 임시 테이블 생성 후 처리하였다.


```
with R as(
select hour(DATETIME) as "HOUR",
       count(ANIMAL_ID) as "COUNT"
       from ANIMAL_OUTS
       group by hour(DATETIME)
       order by hour(DATETIME)
    )

,TIME AS(
SELECT 0 AS h
union
SELECT 1 AS h
union
SELECT 2 AS h
union
SELECT 3 AS h
union
SELECT 4 AS h
union
SELECT 5 AS h
union
SELECT 6 AS h
union
SELECT 7 AS h
union
SELECT 8 AS h
union
SELECT 9 AS h
union
SELECT 10 AS h
union
SELECT 11 AS h
union
SELECT 12 AS h
union
SELECT 13 AS h
union
SELECT 14 AS h
union
SELECT 15 AS h
union
SELECT 16 AS h
union
SELECT 17 AS h
union
SELECT 18 AS h
union
SELECT 19 AS h
union
SELECT 20 AS h
union
SELECT 21 AS h
union
SELECT 22 AS h
union
SELECT 23 AS h
)
select t.h as "HOUR",ifnull(R.COUNT,0) as "COUNT" from TIME t
left join R on t.h = R.HOUR;
```

## leetcod 180. Consecutive Numbers(Medium)

![](https://i.imgur.com/GIgHZwI.png)

```
SELECT DISTINCT
    l1.Num AS ConsecutiveNums
FROM
    Logs l1,
    Logs l2,
    Logs l3
WHERE
    l1.Id = l2.Id - 1
    AND l2.Id = l3.Id - 1
    AND l1.Num = l2.Num
    AND l2.Num = l3.Num
;
```

![](https://i.imgur.com/Cn2oAZv.png)

---

## leetcode 184. Department Highest Salary(Medium)

![](https://i.imgur.com/uDhijvD.png)

```

with R as (
select e2.Name, e2.Salary, e2.DepartmentId from (
    select max(e.Salary) as "Salary", e.DepartmentId as "DepartmentId" 
    from Employee e
    group by e.DepartmentId
    )  e1, Employee e2
    where e1.DepartMentId = e2.DepartmentId
    and e1.Salary = e2.Salary
)
select d.Name as "Department", R.Name as "Employee", R.Salary as "Salary"
from R, Department d
where R.DepartmentId = d.Id;

```

![](https://i.imgur.com/QaktOTX.png)

솔루션에 있는 코드는 508초,
위 해당코드의 경우 496초가 나왔다. 실행계획을 봤을때 Type All로 되어있어서 느릴줄 알았는데 생각보다 빠른 코드였다. 조금 더 공부후 최적화를 해볼 예정이다. With 구문은 가독성이 너무 떨어져 사용하였다.

--- 
## leetcode 181.(easy)

![](https://i.imgur.com/W7v5lx9.png)


```
solv1)
select e.name as "Employee"
from Employee e, Employee a
where e.managerId = a.Id
and e.Salary>a.Salary

```

```
solv2)
select e.Name as "Employee"
from Employee e
join Employee a
on e.managerId = a.Id
where   e.Salary>a.Salary

```



self join을 이용한 단순한 문제였다.
뭐가 더 빠를까 궁금해서 두가지 방법으로 조인을 걸어서 돌려봤는데

![](https://i.imgur.com/tnKs35Q.png)

sol1) 풀이가 더 빨리 돌았음을 알 수 있었다. 생각보다 차이가 런타임이 차이가 많이나 찾아봤더니 일반적으로는 속도가 똑같다고 한다. join 구문이 가독성이 더 좋아 보통 join 구문을 권장한다고 한다.