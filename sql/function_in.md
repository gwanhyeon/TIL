# where in 절

### in 절
WHERE 포함하고 싶은 컬럼명 IN (조건1, 조건2, 조건3...조건 N)

조건에 일치하는 모든 내용을 조회
```sql
SELECT 
     , NAME
     , AGE
  FROM USER
  WHERE NAME IN ('KGH', 'KIM') 
```

### not in 절
WHERE 포함하고 싶지 않은 컬럼명 IN (조건1, 조건2, 조건3... 조건 N)

조건에 일치하지 않는 모든 내용을 조회

```sql
SELECT 
     , NAME
     , AGE
  FROM USER
  WHERE NAME NOT IN ('KGH', 'KIM') 
```

번외로, IN절안에 LIKE절 사용은 할 수는 없다고합니다.
