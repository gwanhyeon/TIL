# over()

over함수는 언제 사용해야할까?
over함수는 보통 order by, group by에 대한 쿼리를 개선하기 위해 나온 함수

1. 기존에 SQL은 서브쿼리내에서 SUM함수를 사용하는 경우가 많았다.

```sql
SELECT NAME, PRICE
FROM (
    SELECT BRITH, PRICE,
    SUM(TOTAL_PRICE) AS PRICE
    FROM USER
    GROUP BY BRITH
    ORDER BY BIRTH DESC
)
```

2. over()함수를 사용하면 이것들을 손쉽게 사용이 가능하다.

```sql
SELECT NAME, BIRTH, SUM(TOTAL_PRICE) OVER(ORDER BY BIRTH DESC) AS PRICE
FROM USER
```

# OVER() 종류

```SQL
COUNT(*) OVER(): 전체행에 대한 카운트를 가져온다.
COUNT(*) OVER(PARTITION BY [COLUMN]): 그룹 단위로 그룹의 카운트를 가져온다.

MAX([COLUMN]) OVER(): 전체 결과값 중 가장 큰 값
MAX([COLUMN]) OVER(PARTITION BY [COLUMN]): 그룹 결과값 중 가장 큰 값

MIN([COLUMN]) OVER(): 전체 결과값 중 가장 작은 값
MIN([COLUMN]) OVER(PARTITION BY [COLUMN]): 그룹 결과값 중 가장 작은 값

SUM([COLUMN]) OVER() : 전체행 합
SUM([COLUMN]) OVER(PARTITION BY [COLUMN]) : 그룹내 합

AVG([COLUMN]) OVER() : 전체행 평균
AVG([COLUMN]) OVER(PARTITION BY [COLUMN]) : 그룹내 평균

STDDEV([COLUMN]) OVER() : 전체행 표준편차
STDDEV([COLUMN]) OVER(PARTITION BY [COLUMN]) : 그룹내 표준편차

RATIO_TO_REPORT([COLUMN])OVER() : 현재행값/SUM(전체행값) %일 경우 100곱하기
RATIO_TO_REPORT([COLUMN])OVER(PARTITION BY [COLUMN]) : 현재행값 / SUM(그룹행값) %일 경우 100곱하기
```


> Tip!

COUNT(*) OVER()함수는 전체행에 대한 카운트를 진행할때 사용하며, COUNT(*) OVER(PARTITION BY [COLUMN]) 같은 경우는 그룹내에 존재하는 것들의 개수를 확인할 수 있다.

해당되는 테이블이 있다고 가정하고, COUNT(*) OVER(PARTITION BY CONTENT)를 사용한다고 가정해보겠습니다. 

> 조건 단일

|NAME|CONTENT|
|------|---|
|kim|JAVA|
|lee|C++|
|lee|PYTHON|
|kim|JAVA|
|park|PYTHON|

---

|COUNT|
|------|
|2| JAVA의 개수
|1| C++의 개수
|2| PYTHON의 개수
|2| JAVA의 개수
|2| PYTHON의 개수

--- 

> 조건 다중

COUNT(*) OVER(PARTITION BY CONTENT, NAME)

|NAME|CONTENT|
|------|---|
|kim|JAVA|
|lee|C++|
|lee|PYTHON|
|kim|JAVA|
|park|PYTHON|

---

|COUNT|
|------|
|2| kim, JAVA의 개수
|1| lee, C++의 개수
|1| lee, PYTHON의 개수
|2| kim, JAVA의 개수
|1| park, PYTHON의 개수

---

단일 조건과 다중 조건에 따른 결과값이 달라지는것을 확인하셨나요? OVER() 함수는 그룹에 대한 PARTITION BY 의 조건을 맵핑시켜 데이터를 노출시켜주는 것을 알 수 있었습니다.





