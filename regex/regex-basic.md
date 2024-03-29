# 정규표현식

특정한 규칙을 가진 문자열의 집합을 표혆기 위해 쓰이는 형식언어

# 정규표현식의 종류

vim / posix 정규식

# 정규표현식의 기본 문법

1. 패턴 그대로 매칭하는 경우: 단어그대로 패턴으로 사용하여 매치하는 영역을 찾는다.
2. 메타문자 및 수량 한정자를 적용하는 경우: 정규식 패턴에 쓰이는 문자중에서 특별한 의미를 가지는 메타문자들이 있는데, 이들을 사용하여 보다 폭 넓은 패턴에 매치할 수 있다.
3. 그룹 및 look around 기능: 패턴의 일부를 그룹으로 묶거나 특정 패턴의 앞 뒤로 다른 패턴이 오는 조건을 더하는 경우

# 정규표현식의 메타 문자 

> ^

문자열의 시작을 표현한다.[....] 내부에서 쓰이는 경우라면 뒤의 패턴에 일치하지 않는것을 선택한다.
^http: 문자열이 http로 시작하는 경우에만 매치, 중간에 나타난 http에는 매치 X
ab[^0-9]: ab뒤에 숫자가 아닌것이 오는것에만 매치한다.(abc)


> $

문자열의 끝을 표현한다.

> \b

단어의 경계, 문자열 시작과 끝, 공백, 개행, 탭, 콤마, 구두점, 대시문자 등이 올 수 있다.

> \B

\b가 아닌것 정규식 메타문자에서는 흔히 대문자로 표현한 것을 소문자로 표현한 문자의 반대를 의미한다.

\bplay\B

> \s

공백 문자 및 탭 문자에 매치한다.

> \S

공백 문자가 아닌 한 글자에 매치한다.

> \d

숫자에 매치한다.[0-9]

> \D

숫자가 아닌 문자에 매치한다. [^0-9

> \w

단어를 만들 수 있는 글자, 알파벳 대소문자, 숫자, 언더스코어를 포함한다. [A-Z-a-z0-9_]

> \W

\w에 포함되지 않는 문자들

> \n

개행문자, \r은 캐리지 리턴이다.

> \

이스케이프용 문자, 정규식상의 특별한 의미가 있는 문자들을 문자 그대로 쓸때 앞에 붙인다. \^ 라고 쓰면 문자 ^만 의미한다.

> .

아무문자 1개에 대응딘다. 공백 역시 문자 1개로 취급된다.

# 선택 패턴

| 문자를 이용하면 A | B 패턴(A or B)

ex) tomato|potato

선택 패턴은 이후에 등장하는 그룹 패턴과 관련하여 보다 강력하게 쓰일 수 있다.

선택 패턴으로는 [....], 대괄호속에 넣은 문자 중에서 하나에 매칭하는것


ex) [cfh]all 패턴 -> call, fall, hall 모두 매칭 가능

특히, 선택패턴은 특정 범위를 표현하는것도 가능하다.
`[A-Z] [0-9] [a-z] [ㄱ_힣]`

선택 패턴내에서 ^이 쓰이면 not의 의미를 갖는다. 선택 패턴이 아닌경우에는 (시작점을 뜻한다 ^)


# 그룹

괄호로 둘러싼 단위는 그룹을 나타낸다.
그룹은 전체 패턴 내에서 다시 하나로 묶여지는 패턴 조각을 나타낸다. 특히 `|`나 뒤에 나오는 수량 한정자를 그룹에 붙이는 형태로 많이 사용되며, 한 번 매치한 그룹이 다시 반복되어 나타나는 경우에도 사용할 수 있다.

ex) (tom|pot)ato: tomato, potato 모두 매치되는 패턴을 그룹을 써서 줄이기 
(a|i){3}bc: a혹은 i가 3개 온 후에 bc가 오는 패턴(aaabc, iiibc, aiabc, iiabc) 등에 매치 된다.

괄호를 써서 묶은 부분은 1번부터 시작하는 그룹으로 참조 가능하다

tomato -> to ma to -> (to)ma\1 (\1은 1번그룹을 재사용한다는것을 뜻한다.)

> 응용

(a|b|c){2}ma\1

이 패턴은 a혹은 b혹은 c중에서 매치되는 두 글자를 그룹으로 캡쳐하고 ma 뒤에 동일한 글자가 반복되는 패턴.

aamaaa, bcmabc, abmaab등에 매치되지만,

캡쳐된 그룹의 패턴이 아닌 캡쳐된 내용에 매치하므로 aamabb에는 매치되지 않는다.

# 비캡쳐링 그룹 

(?: ) 을 사용하면 그룹으로 묶어는 주지만 캡쳐는 하지 않는 비 캡쳐링 그룹이 된다. 이는 특정한 수량 한정자등을 적용은 하려 하지만 최종 결과에서 따로 구분하여 사용할 필요가 없는 경우에 적용한다. (사실 캡쳐만 해놓고 사용하지 않아도 무방하다.)
> 수량 한정자

동일한 글자 혹은 동일한 족이 n개 만큼 나오는 경우 수량한정자를 뒤에 붙일 수 있다.

> ?

바로 앞의 글자혹은 그룹이 1개 혹은 0개이다

> *

0개 이상이다

> +

1개 이상이다

> {n}

N개가 있다

> {n, m}

N개 이상, M개 이하가 있다.

> 해커랭크 참고 문제 

 https://www.hackerrank.com/challenges/matching-anything-but-new-line

[^\n]{3}(?:\.[^\n]{3}){3}
---------------------------------------------------
[^\n]               # 개행문자가 아닌 글자
     {3}            # 가 3개 있고
(?:                 # 캡쳐하지 않는 그룹이 시작
 \.                 # . 이 온 후
   [^\n]{3}         # . 다음에 다시 개행이 아닌 문자가 3개
){3}                # 이 그룹이 다시 3회 반복

> reference

[reference](https://soooprmx.com/%EC%A0%95%EA%B7%9C%ED%91%9C%ED%98%84%EC%8B%9D%EC%9D%98-%EA%B0%9C%EB%85%90%EA%B3%BC-%EA%B8%B0%EC%B4%88-%EB%AC%B8%EB%B2%95/)