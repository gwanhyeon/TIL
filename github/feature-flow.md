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



### Git-flow 작업 처리 과정(rebase로 그래프를 단순하게 만들자)
```shell
1. upstream/feature-user 브랜치에서 작업 브랜치(bfm-100_login_layout)를 생성합니다.
(feature-user)]$ git fetch upstream
(feature-user)]$ git checkout -b bfm-100_login_layout –track upstream/feature-user

2. 작업 브랜치에서 소스코드를 수정합니다. (뚝딱뚝딱 :hammer:)
3. 작업 브랜치에서 변경사항을 커밋합니다. (보통은 vi editor에서 커밋 메세지를 작성 함)
(bfm-100_login_layout)]$ git commit -m "BFM-100 로그인 화면 레이아웃 생성"

4. 만약 커밋이 불필요하게 어려 개로 나뉘어져 있다면 squash를 합니다. (커밋 2개를 합쳐야 한다면)
(bfm-100_login_layout)]$ git rebase -i HEAD~2

5. 작업 브랜치를 upstream/feature-user에 rebase합니다.
(bfm-100_login_layout)]$ git pull –rebase upstream feature-user

6. 작업 브랜치를 origin에 push합니다.
(bfm-100_login_layout)]$ git push origin bfm-100_login_layout

7. Github에서 bfm-100_login_layout 브랜치를 feature-user에 merge하는 Pull Request를 생성합니다.
8. 같은 feature를 개발하는 동료에게 리뷰 승인을 받은 후 자신의 Pull Request를 merge합니다. 만약 혼자 feature를 개발한다면 1~2명의 동료에게 리뷰 승인을 받은 후 Pull Request를 merge합니다.
```

### 2. develop 변경사항을 feature로 가져오기 (Optional)
작업을 할 때 브랜치의 수명은 되도록 짧게 가져가는 게 좋지만, feature 브랜치에서 기능을 완료하는데 해야 할 작업들이 많아서 오래 걸리는 경우 들이 있습니다. 그러다 보면 develop에 추가된 기능들이 필요한 경우가 종종 생기게 됩니다. 그럴 때는 feature 브랜치에 develop의 변경사항들을 가져와야 합니다.
```shell
feature-user 브랜치에 upstream/develop 브랜치를 merge 합니다.
(feature-user)]$ git fetch upstream
(feature-user)]$ git merge –no-ff upstream/develop

upstream/develop의 변경사항이 merge된 feature-user를 upstream에 push 합니다.
(feature-user)]$ git push upstream feature-user
```

### 3. 완료된 기능을 이번 출시 버전에 포함시키기
드디어 feature-user 브랜치에서 작업하던 기능이 완료되었습니다. 이젠 feature 브랜치를 이번 출시 버전에 포함시키기 위해서 develop에 merge 해야 합니다.

develop 브랜치에 upstream/feature-user 브랜치를 merge 합니다.
```shell
(develop)]$ git fetch upstream
(develop)]$ git merge –no-ff upstream/feature-user

upstream/feature-user 기능이 merge된 develop를 upstream에 push 합니다.
(develop)]$ git push upstream develop
```

> reference 

[우아한 형제들 Git-flow](https://techblog.woowahan.com/2553/)
