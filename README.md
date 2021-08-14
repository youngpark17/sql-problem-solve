# sql-problem-solve

## leetcode 181.(easy)

![](https://i.imgur.com/W7v5lx9.png)

--- 

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