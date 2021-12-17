# UNION VS UNION ALL
UNION : 각 쿼리의 결과 합을 반환하는 합집합 (중복제거) - 속도면에서 더 느리다.
UNION ALL : 각 쿼리의 모든 결과를 포함한 합집합 (중복제거 안함) - 속도면에서 더 빠르다.

```sql
SELECT A.NAME FROM A
UNION ALL
SELECT A.NAME FROM A
....
```

### 예시 

가장 좋은 예시는 다양한 게시판에서 가장 최신의 글을 가져오는 경우를 들 수 있다.
A,B,C 의 게시판의 글을 UNION ALL로 묶어서 가져온 후 최신의 글을 뽑아내는 것을  UNION ALL로 처리할 수 있겠다.




