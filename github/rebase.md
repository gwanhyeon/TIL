# Git rebase란?

Git rebase는 두 개의 공통 Base를 가진 Branch에서 한 Branch의 Base를 다른 Branch의 최신 커밋으로 branch의 base를 옮기는 작업입니다. 용어 그대로 베이스를 다시 설정하는 작업입니다.

 

Git rebase의 장점
1. 공유 branch의 최신 변경사항을 즉각 반영할 수 있다.
git merge는 공유 branch에 대한 변경사항을 즉각 대응하기 어렵습니다.

 

반면에 Git rebase를 사용한다면, 동료 개발자들이 올린 commit들의 수정사항을 내가 작업하고 있는 branch에 즉각 반영할 수 있습니다.

즉, 공유 branch에 대한 최신 commit을 반영하면서 작업을 해야할 때 git rebase를 사용한다면 작업 branch에서 항상 최신 변경사항을 적용한 commit을 유지할 수 있습니다. 

2. rebase는 커밋이력을 남기지 않으므로 commit History가 깔끔해진다.
git merge를 사용하여 최신 이력을 가져올 경우, 복잡하고 어지러운 커밋 History가 됩니다.

반면, git rebase로 만들어진 History는 두, 세 줄의 깔끔하고 직관적인 History로 프로젝트를 관리 할 수 있습니다.

 

특히, git-flow를 사용할 때 Rebase and Merge 전략으로 깔끔한 History로 작업할 수 있습니다.

git-flow에서는 develop 브랜치를 생성하고 개발자들이 각각 기능별로 feature를 생성하고 개발이 완료되면 develop에 merge를 합니다.

위 처럼 git-flow를 적용하여 자신은 feature/b에서 작업을 하는 중이고, 동료 개발자가 feature/a에서 작업을 하고 develop에 merge를 하였다고 가정을 해 봅시다.

merge 했을 때의 그래프
feature/b에서 작업을 모두 끝냈다거나, feature/a에서 작업한 내용들을 가져오고 싶어서 feature/b를 develop에 merge를 한다고 가정하면 위와 같은 커밋 그래프가 형성됩니다.

위의 commit history는 feature가 두개라서 그나마 보기에는 편할 것 같지만 feature가 10개 이상 된다면 어떨까요?

극단적으로 Merge만 할 경우 엄청나게 복잡한 Commit History가 생길 수 있다.. ㄷㄷ
위처럼, 조금 극단적이긴 하지만 feature가 많다면 엄청 복잡한 History가 생길 가능성이 있습니다.

저런 그래프를 관리하면서 이전 버전에서 버그가 났을 경우 커밋을 추적할 수 있을까요?
Commit History 관리도 프로젝트 관리에서 중요한 작업이라고 생각합니다.

그렇다면 rebase 후에 merge를 해보도록 하겠습니다.

$ git checkout feature/b
$ git rebase develop
명령어를 입력한 후에 feature 브랜치를 develop에 merge 하도록 하겠습니다.

rebase 후 merge 했을 때 그래프
feature/b의 base를 develop의 최신 commit으로 옮겼습니다.

그리하여 두 줄의 Commit History로 훨씬 간결하고 보기좋은 그래프로 바뀌었습니다.

또한, feature/b의 커밋들에도 최신 변경사항들이 반영 된 커밋들로 존재하게 됩니다.

Git rebase의 단점 아닌 단점
내 작업 branch의 각각 commit마다 conflict를 해결해야 한다.
merge는 충돌이 발생하면 한번만 처리하면 되지만 rebase는 나의 branch의 각각의 commit마다 충돌처리를 해주어야 합니다.

즉, 오래전에 수정했던 커밋을 rebase 과정에서 또 다시 conflict를 해결해줘야 할 수도 있습니다.

그래서, 각각의 커밋마다 충돌을 해결하고 Resolve Confilct와 Continue rebase를 해주어야 하는 번거로움이 있을 수 있습니다.

하지만, 이것이 단점이 아닌 장점이다.
오히려 회사에서 git-flow를 오래 사용하면서 느낀 결과, develop의 이전 커밋들과 내 브랜치의 커밋들을 어느 커밋에서 충돌이 난건지도 모른채로 하나의 커밋에서 충돌을 해결하는 것은 바람직한 방법은 아니라고 생각합니다.

오히려 feature 브랜치의 모든 커밋이 전부 정상적으로 동작하도록 각각의 커밋마다 충돌을 해결하는 것이 코드 에러를 줄이고 품질을 높이는 방법이라고 생각하기 때문에 더 좋은 방법이라고 생각하고, 회사에서도 위에 나열한 장점들 때문에 Rebase and Merge를 사용하고 있습니다.

 
