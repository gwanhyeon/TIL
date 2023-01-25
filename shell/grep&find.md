# grep & find 특정문자 대소문자 구분없이 사용하기

```shell
$grep -i "word" words.txt
``` 

> grep

하위폴더를 포함하여 존재하는 모든 파일에서 원하는 단어를 찾아주는 명령어 입니다.

*$grep -rni [검색어] [경로명 또는 파일명]*

r :  하위디렉토리까지 검색
n:  파일의 몇번째 라인에 있는지 표시
i :  검색어를 대소 문자 구분없이 검색

검색어 내에 공백문자가 있을경우는 "  " 를 사용하시면 됩니다.

예)
```shell   
$grep -rn test ./kernel/-
$grep -rni "test board" ./kernel/-
$grep -rn test *
```

git이나 svn을 사용하시는 분들은 .git .svn 폴더로 인해  불필요하게 검색시간이 늘어납니다.
아래와 같이 특정 Directory를 제외 할 수 있습니다

--exclude-dir=디렉토리

예)
```shell
$grep -rn --exclude-dir=\.git test ./kernel/-
```

.bashrc 파일에 아래 내용을 추가 하시면 더 편하게 사용하실 수 있습니다. 
```shell
$alias grp='grep -rn --exclude-dir=\.git'
$grp test ./kernel/-
```
과 같이 사용하실 수 있습니다.

> tip
     
구조체의 정의(definition)부분 검색 일반적으로 정의 부분은  이름뒤에 { 가 위치합니다.
```shell
struct input_dev {
    ...
$grep -rn "input_dev\s*{" *
$grep -rn "input_dev\s\+{" *
```
로 검색하시면 됩니다.
- \s 는 space를 의미합니다.
- * 는 개수가 0 개 이상을 의미합니다.  따라서 공백이 0개 이상 존재해야 합니다.
- \+  1개 이상을 의미합니다. 따라서 공백이 적어도 1개는 존재해야 합니다.

> find

하위폴더에 존재하는 파일을 찾아주는 명령어 입니다.

```shell
find [검색 디렉토리] -iname [파일명]
-name    :  대소문자 구분하여 파일명 검색
-iname   :  대소문자 구분하지 않고 파일명 검색

$find ./kernel -iname mcs*
$find . -name mcs*
```

> Tip

특정 확장자에서 문자열 검색
```shell    
find . -iname "*.h" | xargs grep -n "input_dev"
```
find로 파일검색후  파일내에 특정 문자열 검색

> keyboard로 붙여넣기

일반적으로 마우스로 문자열을 긁어다가 오른쪽 버턴을 누르면 프롬프트에 복사가 되는데
마우스로 문자열을 잘라내어 Clipboard에 저장된 내용을 Command 창에서 다시 쓰려면
Shift + Insert 키를 누르게 되면 Clipboard에 저장된 내용이 프롬프트에 붙여넣기가 됩니다.

> dev/null이 무엇일까?

dev/null은 shell에서 출력을 버리는 용도로 사용한다.
dev/null 파일은 항상 비어있으며, dev/null에 전송된 데이터는 버려집니다. 따라서, 특정 명령어를 실행 후 출력이 필요 없는 경우는 /dev/null에 출력을 지정하는것이 좋습니다.

```shell
파일 설명자    설명
0    표준 입력
1    표준 출력
2    표준 오류(진단) 출력
```

예시) 
```shell
find . -iname '*.sh' 2>dev/null
```

> 정리: 다음의 명령어는 무엇을 의미할까?
 
1. .은 현재 디렉터리에서부터 찾고, /는 root에서부터 찾는다.
2. iname은 대소문자를 상관없이 찾는다.
3. name은 *. 소문자만 찾는다.
4. *를 사용하여 모든 sh파일 형식을 찾는다.
5. 2>dev/null을 사용하여 오류가 발생한 출력은 버린다.(표준 오류 출력)
6. 와일드 카드의 의미는 "*" : "모든"이란 의미를 가지고 있습니다.
'ade*' = ade로 시작하는 모든 파일
'*ade' = ade로 끝나는 모든 파일
'a*b' = a로 시작해서 b로 끝나는 모든 파일
7. find -name에서 이 ' '를 이용해 리눅스에서 문장을 감쌀 시, 감싸진 문자들은 모두 
쉘에서 "아무런 의미도 없는 일반 문자 취급"합니다 ex) '*abv' : 그냥 이름이 *abv란 파일


> reference

find 완전 정복
https://mamu2830.blogspot.com/2019/12/find.html 
