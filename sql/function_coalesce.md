# coalesce()
coalesce 함수는 영영사전에 `합친다`라는 뜻을 가지고 있습니다. 따라서, 값을 합치는 역할(대체)을 하는 함수라고 생각하시면 됩니다.

--- 

coalesce 함수는 기본 형태는 다음과 같습니다.
```sql

    select 
        COALESCE(PARAM1, PARAM2, ......, PARAM N) 
    from 
```
COALESCE 함수는 처음으로 NULL이 아닌 컬럼이면 해당되는 컬럼값으로 대체합니다.
오라클에서는 NVL(PARAM1, PARAM2, .....), MSSQL에서는 ISNULL(PARAM1, PARAM2, ....) 으로 대체 가능합니다.


# coalesce() 사용 방법

```sql
1. 컬럼값으로 대체
coalesce(orderId, id) as orderId

1. 지정 문자열로 대체
coalesce(orderId, 'target id') as orderId

1. NULL로 대체
coalesce(orderId, null) as orderId

4. JSON OBJECT로 대체
coalesce(orderId, '{}')::json as orderId
```

다음과 같이 사용할 수 있습니다. coalesce() 함수는 실무에서 필수적으로 사용되는 함수이기 때문에 익숙해질 필요가 있다고 생각합니다.