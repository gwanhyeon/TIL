# 로컬 저장소와 github remote 저장소 브랜치 동기화 명령어


```xml
$git flow init
```

명령어를 사용하여 git flow의 형식대로 만들어주거나, intellj에서 제공하는 git flow plugin을 추가하여 해당되는 git flow 를 세팅해준다.

`git flow init` 명령어를 실행하면 `main / develop / feature / hotfix ..` 등등 git flow와 관련된 브랜치를 생성시켜준다. 하지만, 현재 github remote 원격저장소에는 해당 브랜치가 업데이트 되어있지 않다. 

```xml
$git fetch origin
$git remote update
$git push -u origin develop
```

따라서, 다음과 같은 명령어로 `remote` 원격지를 `fetch` 시켜준 후에 `remote` 업데이트를 진행한다. 그리고 해당 `develop` 브랜치를 강제로 `origin remote` 원격지에 push를 시켜주면 해당 `develop` 브랜치가 업데이트되어 `main / develop` 를 확인할 수 있다.




