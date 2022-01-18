
# String_AGG 함수

여러행의 컬럼을 하나로 합치는 함수

`STRING_AGG("합칠컬럼명", "구분자") WITHIN GROUP(ORDER BY "컬럼명")`


### 기본 사용법
SELECT age
     , STRING_AGG(name, ',') name
  FROM user
 WHERE job IN ('A', 'B')
 GROUP BY age
 

### 컬럼 값을 정렬하여 합치는 방법
SELECT age
     , STRING_AGG(ename, ',') WITHIN GROUP(ORDER BY name) name
  FROM user
 WHERE job IN ('A', 'B')
 GROUP BY age