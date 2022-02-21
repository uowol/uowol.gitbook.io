# 태블릿으로 Git Commit하기

### 태블릿에 Termux 앱 설치하기

#### Termux란?

'Termux'는 안드로이드에서 Linux Terminal을 사용할 수 있게 해주는 어플리케이션입니다.

실제로 사용해보면, 우리가 알고 있는 linux 터미널과 조금 차이가 있지만 Google 검색 몇 번이면 어렵지 않게 사용할 수 있습니다.

#### Termux에 우분투(Ubuntu) 설치가 가능한가요?

가능합니다. 실제로 Ubuntu환경이 익숙한 저로서는 Termux의 터미널이 맞지 않아 Ubuntu를 설치하여 사용하고 있습니다.

하지만 이번 포스팅에서는 Termux 터미널에서 시작하고 끝이 나므로 설치 과정은 서술하지 않겠습니다. 따로 궁금하신 분들은 Google에 Termux ubuntu install를 검색하시면 외국 분들이 많이 서술해두었으니 참고 바랍니다.

***

### Termux 저장공간 권한 획득하기

```
Termux 터미널은 기본적으로 /data/data/... 폴더에서 작동하는데, Rooting 되지 않은 기종이라면 접근이 불가능합니다. 
때문에 Git에 커밋하는 폴더에 접근하려면 접근가능한 내부저장공간에 Git환경을 구축하는 것을 추천드립니다.
```

#### 안드로이드

"설정 > 애플리케이션 관리 > Termux > 앱 권한 설정"에 들어가셔서 저장 권한을 주시면 됩니다.

#### Termux

저장공간에 접근하려면 Termux 터미널에도 따로 명령어를 입력해주어야 합니다.

1. `$ termux-setup-storage`
   * `ls` 명령어를 쳐보면 `~(root)`폴더에 `storage`라는 폴더가 생깁니다.\
     \

2. `$ cd storage`
   * `ls` 명령어를 쳐보면 여러가지 폴더가 뜰 텐데요, 저희는 `downloads`폴더에서 진행하도록 하겠습니다.\
     \

3. `$ cd downloads`
   * `ls` 명령어를 쳐보면 태블릿의 `Download`폴더와 연동되어 있는 것을 확인할 수 있습니다.

```
만약, downloads폴더에 진행하고 싶지 않다면 /sdcard/로 접근하는 방법도 있습니다. 이 경우 'cd /sdcard' 명령어를 실행하신 후 4.번부터 진행해주시면 됩니다.
```

1. `$ mkdir works`
   * git repository를 가져올 폴더를 생성합니다.\
     \

2. `$ cd works`
   * 생성했으면 이동해야겠지요?\
     \

3. `$ pwd`
   * 만약 여기까지 잘 진행되었다면, 다음과 같이 나올 것입니다.

```
/data/data/com.termux/files/home/storage/downloads/works
또는,
/sdcard/Download/works
```

이로써 Git repository를 가져올 작업공간까지 이동을 완료했습니다.

다음은 Git 설치를 진행해보겠습니다.

***

### Git 설치하기

#### Git 설치

* `$ apt-get install git`
  * 설치하겠느냐는 문구가 뜬다면 `Y`를 입력해주세요.

#### Github 개인 정보 등록

* `$ git config --global user.name "본인 계정 이름 입력"`
* `$ git config --global user.email "본인 계정 이메일 입력"`

#### Github 저장소 복제

위 작업을 모두 정상적으로 마쳤다면 작업공간까지 무사히 이동했을 것입니다.

이제, 해당 공간으로 Git repository를 복제하여 가져오겠습니다.

* `$ git clone https://github.com/계정이름/복제할_repository_주소`
  * 주소는 다음과 같이 알아낼 수 있습니다.&#x20;

#### 원격 저장소 등록

* `$ git remote add origin https://github.com/계정이름/복제할_repository_주소`
* `$ git fetch origin`

여기까지 실행시키면 복제한 폴더가 Git과 성공적으로 연동되었습니다.

***

### Git Commit하기

다음은 Git에 커밋하기 위한 명령어들을 알아보겠습니다.

#### `$ git status`

* 변경 사항이 있는지 확인하고 알려줍니다.

#### `$ git add "파일이름"`

* 변경된 파일이 있다면 커밋하기 전에 `add`명령어로 추가시켜줘야 합니다.
* `$ git add -A` 명령어로 한번에 모든 변경된 파일을 추가할 수 있습니다.

#### `$ git commit -m "메세지 입력"`

* 위 과정이 마무리되었다면 Git에 해당 메세지로 커밋합니다.

#### `$ git push`

* 저장소에 커밋한 파일을 업로드합니다.
* 계정과 암호를 물어본다면 위에 입력했던 것처럼 입력해주시면 됩니다.

#### `$ git pull`

* 저장소를 업데이트(내려받기)합니다.

다음은 태블릿에서 업로드한 화면 캡처 이미지입니다.&#x20;

정상적으로 작동하는 것을 확인할 수 있습니다.
