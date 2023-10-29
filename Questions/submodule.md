# submodule이란?

[Git - Submodules](https://git-scm.com/book/en/v2/Git-Tools-Submodules)

프로젝트를 작업하다보면 그 안에서 다른 프로젝트를 사용해야하는 경우가 종종 있다.

타사에서 개발한 라이브러리거나 별도로 개발하여 여러 상위 프로젝트에서 사용하고 있는 라이브러리일 수도 있다.

Git의 서브모듈을 사용하면 Git 레포지토리를 다른 Git 레포지토리의 하위 디렉토리로 유지할 수 있다.

## 주요 명령어

**submodule 추가**: 특정 URL에서 하위 모듈을 현재 저장소에 추가한다.

```
git submodule add [URL] [path/to/submodule]
```

**하위 모듈과 함께 저장소 클론**: 저장소와 그 안의 모든 하위 모듈을 동시에 클론한다.

```
git clone [URL] --recurse-submodules
```

**submodule 초기화 및 업데이트**: 만약 `--recurse-submodules` 옵션을 빼고 서브모듈이 포함된 저장소를 클론하게되면 하위 모듈이 빈 폴더로 클론된다. 이때 submodule의 설정을 초기화하고 업데이트 하는 명령어이다.

```
git submodule init
git submodule update
```

**하위 모듈 업데이트**: 모든 하위 모듈을 최신 상태로 업데이트한다.

```
git submodule update --remote
```

## Git Submodule 특징

- **독립적인 저장소**: 하위 모듈은 슈퍼 프로젝트와 독립된 저장소로 작동한다. 따라서 하위 모듈에서 변경사항을 커밋하면 해당 변경사항은 슈퍼 프로젝트에 바로 반영되지 않는다.
- **하위 모듈의 특정 커밋 참조**: 슈퍼 프로젝트는 하위 모듈의 특정 커밋을 참조한다. 따라서 하위 모듈을 업데이트하면 슈퍼 프로젝트에서 해당 하위 모듈의 참조를 업데이트해야 한다.
- **변경사항의 추적**: 슈퍼 프로젝트에서는 하위 모듈의 내용 자체를 추적하지 않고, 오직 하위 모듈의 커밋 해시만을 추적한다.

서브모듈을 추가하면 사진처럼 프로젝트 명 뒤에 참조하는 커밋이 붙어있는 것을 확인할 수 있다.

따라서 하위 프로젝트에 변경사항이 생겼다면 상위 프로젝트에서 업데이트를 꼭 해주어야한다.

![Untitled](https://github.com/MojitoBar/iOS-DeepDive/assets/16567811/e4990960-4f3c-4d56-8a7d-c8df56b5f45a)

그리고 서브모듈을 추가하게되면 .gitmodules라는 파일이 생기는데 여기에 서브모듈의 정보가 들어있다.

```
[submodule "pin"]
	path = pin
	url = git@github.com:MojitoBar/pins-light.git
```

---

여러 블로그를 찾아보니 서브모듈을 공개되면 안되는 환경변수를 저장하는 용으로도 사용하는 사람들이 있는 것 같았는데, 이런 방법은 처음 알게되어 흥미로웠다.
