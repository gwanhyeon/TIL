# function collate()

sql문에서 정렬시에 한글을 정렬하고 싶은 경우가 생긴다. 하지만, 모든 데이터가 정렬되지 않고, 일부 데이터만 정렬되는 현상이 생길 수 있습니다.

> 무엇이 문제인가?

Collation의 종류중에는 en_US.UTF-8 같은 설정이 존재한다. 즉, 언어에 따른 collation 설정을 뜻합니다. 한국어 설정(ko_KR.UTF-8)을 활용해도, 정렬 문제는 해결되지 않을 수 있습니다. 이것은 근본적으로 collate 'C' 옵션을 통해서 해결해 나갈 수 있습니다.

요약하자면, collation은 정렬에 활용되며 OS default 방식을 채택하여 정렬의 기준을 잡게 됩니다. 정렬의 기준의 방식은 C, POSIX 등이 있습니다. C, POSIX 방식은 character code byte의 값으로 정렬을 하기 때문에 한글 인코딩문제에 대해서 대응해나갈 수 있다.

### 직접 설정을 바꾸는 다른 방법으로는, 

DEFAULT로 COLLATE가 C가 되도록 하려면, initdb 로 데이터베이스 생성 COLLATE를 지정해주면 될 것 같네요.

`initdb -E UTF-8 --lc-collate=C -W -D <위치>`
혹은 LC_COLLATE=C 로 환경변수가 설정된 상태로 postgresql 서버가 동작하면 가능하다.

1. 데이터베이스를 DUMP 합니다.
2. 새 데이터베이스를 위와 같이 lc-collate를 지정하여 생성합니다.
3. DUMP한 데이터를 새 데이터베이스에 로딩하면 됩니다.

```sql
default_scope { order('name collate "C" asc') }
SELECT "categories".* FROM "categories"  ORDER BY name collate "C" asc
```

다음과 같이 한글 정렬 문제를 해결할 수 있다.
