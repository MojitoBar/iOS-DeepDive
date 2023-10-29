# reflog란?

### reflog란

1. 로컬 기록: `git reflog`는 로컬 저장소에서의 작업 히스토리를 추적한다. 이 히스토리는 `git push`와 같은 원격 저장소에 관한 작업과는 관련이 없다. (commit, rebase, reset, checkout 등이 추적됨)
2. HEAD의 이동 기록: reflog는 HEAD와 브랜치 포인터가 어떻게 이동했는지에 대한 기록이다.
   예를 들어, 커밋, 체크아웃, 리베이스, 리셋과 같은 명령어로 인해 HEAD의 위치가 바뀌면 이를 기록한다.
3. 복구 도구: 만약 실수로 커밋을 삭제하거나, 브랜치를 잘못 변경한 경우 `reflog`를 사용하여 이전 상태로 되돌릴 수 있다.

### 기본 사용법:

1. reflog 보기: 단순히 `git reflog` 명령어를 입력하면 HEAD의 최근 변경 내역을 볼 수 있다. 결과는 아래와 같은 형태로 표시된다.

   ```
   [hash] HEAD@{n}: [action]: [description]
   ```

   ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/35feff1a-b00e-45d2-8e8b-157f74dde233/581341fe-6315-40cc-aa5b-bfbd7b932686/Untitled.png)

2. 특정 항목으로 돌아가기: `git reflog`의 출력에서 원하는 항목의 해시 또는 `HEAD@{n}` 참조를 사용하여 `git reset` 또는 `git checkout` 명령을 실행해 해당 상태로 되돌릴 수 있습니다.

   ```
   git reset --hard HEAD@{n}
   ```

### 주의사항:

- `git reflog`는 로컬 히스토리만을 기록한다. 원격 저장소에서의 작업은 기록되지 않는다.
- `git reflog`는 일정 시간이 지나면 오래된 항목들이 자동으로 정리된다. 따라서 무한정 복구할 수는 없다.
