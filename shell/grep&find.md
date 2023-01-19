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
