# merge, rebase, squash 차이

- 어떤것이 가장 매력적인가?

### **1. merge, rebase, squash 차이**

- **merge**: 두 개의 branch를 합치는 과정입니다. 만약 'feature' branch에서 작업을 완료하고 이를 'main' branch에 합치려면 merge를 사용하게 됩니다.
  merge를 할 때, 'feature'와 'main' branch의 변경 사항들을 합치고, 그 결과를 새로운 커밋으로 저장합니다.
  
  <img width="500" alt="스크린샷 2023-10-12 오후 3 39 55" src="https://github.com/MojitoBar/iOS-DeepDive/assets/16567811/80e47d82-deb2-44c2-8c55-f0f1b8647864">
      
  ```swift
  // 현재 브랜치에 {test} 브랜치를 합치겠다는 뜻
  git merge test
  ```

- **rebase**: 한 branch의 변경 사항을 다른 branch 위에 "재배치"하는 과정입니다. 예를 들어 'feature' branch에서 작업하던 중 'main' branch에 새로운 커밋이 추가됐다면, 'feature' branch를 rebase하여 'main'의 최신 커밋 위에 'feature'의 커밋을 다시 적용할 수 있습니다. 이는 커밋 히스토리를 깔끔하게 한 줄로 유지하는 데 도움이 됩니다.

  <img width="500" alt="스크린샷 2023-10-12 오후 3 09 58" src="https://github.com/MojitoBar/iOS-DeepDive/assets/16567811/4db0be7a-ec3f-4ecb-acff-89b652d3330f">

  ```swift
  // 현재 브랜치의 변경 사항을 {main} 브랜치 밑으로 합치겠다는 뜻
  git rebase main

  // 이후에 {main} 브랜치에서 merge를 fast-forward가 적용되어,
  // test와 같은 노드를 가르킬 수 있다.
  git checkout main
  git merge test
  ```

- **squash**: 여러 커밋을 하나의 커밋으로 합치는 과정입니다. git merge의 옵션으로 —squash를 이용하여 사용할 수 있습니다.
  원래 merge의 명령어의 경우 합치고자하는 브랜치에 기록된 모든 커밋을 가져오지만 —squash의 경우 여러 커밋을 합친 새로운 커밋을 현재 브랜치에 반영합니다.
  rebase에서도 squash를 사용할 수 있습니다.
  ```swift
  // merge --squash 예제
  git checkout main
  git merge --squash test

  // 합친 커밋이 반영될 메시지를 작성
  git commit -m "commit 0~3"

  // rebase & squash 예제
  // HEAD 기준으로 최근 커밋 3개를 rebase 하겠다는 뜻
  git rebase -i HEAD~3
  ```
<img width="400" alt="Untitled" src="https://github.com/MojitoBar/iOS-DeepDive/assets/16567811/3f922c94-8619-45b3-b208-f068b8dcd540">

<img width="400" alt="Untitled" src="https://github.com/MojitoBar/iOS-DeepDive/assets/16567811/53df0e6b-7616-4f6d-bc13-e541ef6100fa">

왼쪽처럼 창이 뜨면 앞에 ‘pick’ 부분을 원하는 명령어로 변경한 후 저장하면 됩니다.

오른쪽은 ‘squash’로 변경하고 저장했을 때 뜨는 화면. 여기서 합칠 커밋 메시지를 작성하면 된다.

## 어떨 때 사용하면 좋을까?

- **merge**: 간단하게 브랜치를 합치고 그 과정을 명시적으로 남기고 싶을 때 사용합니다.
- **rebase**: 커밋 히스토리를 한 줄로 깔끔하게 유지하고 싶을 때 사용합니다.
- **squash**: 여러 변경 사항을 하나의 의미 있는 커밋으로 합칠 때 사용합니다.

개인적으로는 squash가 매력적이었습니다. 브랜치를 따서 작업하다보면 의미있는 커밋만 하려해도 굳이 전부 반영될 필요가 없는 커밋이 있는 경우가 있었습니다.

또는 main에 반영될 것을 생각해서 의미있는 커밋만을 하려다보니 너무 잘게 커밋하게 되거나 한번에 diff가 큰 커밋을 하게 되는 경우가 있었습니다.

이럴 때 squash를 이용해서 main에 변경사항을 훨씬 깔끔하고 단위도 어느정도 일정하게 나눠서 반영할 수 있을 것 같았습니다.
