### NPM 설치된 내용 확인( --g 를 붙이면, 글로벌로 설치한 내역이 보임)

```bash
➜ vue-node (master) ✔ npm -g ls
/Users/chan/.nvm/versions/node/v16.13.1/lib
├── @vue/cli@4.5.15
├── corepack@0.10.0
└── npm@8.3.0

npm uninstall -g <package>
// 잘안되면, sudo
chown -R "$(whoami)": "$(npm root -g)"
sudo npm uninstall -g <package>
```

  ### NVM 여러버전의 Node.js 관리

[참고 블로그](https://velog.io/@mayinjanuary/NVM-%EC%9D%B4%EB%9E%80-%EB%85%B8%EB%93%9CNode.js-%EB%B2%84%EC%A0%84-%EA%B4%80%EB%A6%AC%ED%95%98%EB%8A%94-%EB%B2%95)

  1. NVM이란?
  Node Version Manager
        2. NVM, 왜 사용해야 하나요?
    협업을 할 때, 또는 다양한 프로젝트를 동시에 진행해야 할 때
    다양한 라이브러리 / 프레임워크 / 개발툴의 버전 호환 문제를 겪어서
        3. 컴퓨터에 다양한 버전의 Node.js 를 설치할 수 있게 해줌
    use 커맨드를 이용해 사용할 Node 버전으로 간단하게 스위칭할수 있게 해줌.
    디폴트 버전을 설정하거나 / 설치한 버전들의 전체 리스트를 확인하거나 / 필요 없는 버전을 삭제하는 등등... 소위 버전 관리가 쉬워짐
    루비의 rvm, rbenv나 파이썬의 pyenv도 같은 역할을 한다고 하네요.


2. NVM 설치하기
    보다 더 자세한 내용을 위해서는 NVM repository(공식 문서) 참고

  ```bash
  $ curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.11/install.sh | bash
  ```

  이 설치 스크립트를 실행하고 나면 두 가지 변화가 생깁니다.

  쉘 설정 파일에 nvm 명령어 스크립트가 추가됩니다.
  전 zsh 쉘을 사용하기 때문에 ~/.zshrc 파일에 스크립트 파일이 추가될 거구요. bash 쉘을 사용하신다면 ~/.bash_profile 에 추가가 됩니다.

3. 다음 커맨드를 통해 확인해보세요.

   ```bash
   $ vi ~/.zshrc
   
   export NVM_DIR="$HOME/.nvm"
   [ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm
   [ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion
   
   #~/.nvm 폴더가 생성됩니다.
   #위 경로에 nvm 레포지토리가 복사됩니다.
   ```

   이제부터는 해당 경로에 nvm 을 이용해 설치한 노드가 버전별로 다운로드됩니다. versions 폴더에서 확인 가능해요.

   아직 어떤 버전의 노드도 설치하지 않았다면, 지금은 비어 있을 겁니다.

4. 설치를 했는데 nvm 커맨드가 실행이 안 돼요.
   가이드대로 설치를 하고 나니 터미널에 이런 문구가 떴습니다.

   ```bash
   npm ERR! peer dep missing: @expo/xdl@54.1.5, required by @expo/dev-tools@0.5.26
   => You currently have modules installed globally with `npm`. These will no
   => longer be linked to the active version of Node when you install a new node
   => with `nvm`; and they may (depending on how you construct your `$PATH`)
   => override the binaries of modules installed with `nvm`:
   
   /usr/local/lib
   ├── create-react-app@3.0.0
   ├── eslint@6.8.0
   ├── expo-cli@2.20.2
   └── serve@11.1.0
   => If you wish to uninstall them at a later point (or re-install them under your
   => `nvm` Nodes), you can remove them from the system Node as follows:
   
        $ nvm use system
        $ npm uninstall -g a_module
   
   => Close and reopen your terminal to start using nvm or run the following to use it now:
   ```

   이미 node 를 설치해 여러 프로젝트를 진행한 바가 있기 때문에 발생한 에러입니다.
   이미 npm (Node Package Manager) 을 사용해 전역으로 설치해둔 패키지들이 있는데,
   nvm 을 사용하여 새로운 node 버전을 설치할 경우
   그 패키지들과의 의존성이 깨진다는 이야기를 하고 있는 것 같아요.

   그러니 애초부터 nvm 을 설치하고, 그 이후에 node 를 깔아서 버전관리를 하는 것이 좋겠죠?
   이 문제는 다른 포스트에서 다루겠습니다.

   마지막 줄을 보시면, Close and reopen your terminal to start using nvm 이라고 써 있는 걸 보실 수 있을 거예요.

   한마디로 nvm 을 사용하려면 쉘을 재시작해야 한다는 소리입니다.
   아무 nvm 커맨드나 한 번 실행해 보시면, 경고 문구가 뜨는 걸 보실 수 있을 거예요.

   ```bash
   $ nvm ls
   zsh: command not found: nvm
   
   ```

5. 따라서 다음 커맨드를 사용해 쉘 환경을 재시작해줍니다.

   - zsh 사용시 

     ```bash
     $ source ~/.zshrc
     ```

     

   - bash 사용시

     ```bash
     $ source ~/.bash_profile
     ```

     

6.  nvm 이 정상적으로 설치되었는지 확인

   ```bash
   $ nvm --version
   ```

   

#### NVM 명령어들

일단 설치 명령어들은 다음과 같습니다.
install, uninstall 뒤에 인자로 오는 문자열은 version-like 이라면 모두 가능합니다. 예를 들면...

##### node.js 버전 설치하기
$ nvm install 0.10
$ nvm install v0.1.2
$ nvm install v8

##### node 최신 버전 설치 (설치 당시 기준)
$ nvm install node

##### node LTS 최신버전 설치
$ nvm install --lts
기타 명령어들은 다음과 같습니다.

##### 설치된 node.js 목록 확인하기
$ nvm ls

##### 설치할 수 있는 모든 Node 버전 조회 (재미삼아 해보지마세요 겁나많음... 황급히 control C 두드리기)
$ nvm ls-remote

##### 특정 버전의 node 사용하기
$ nvm use <version>

##### 현재 사용중인 버전 확인하기
$ nvm current

##### node.js 설치 경로 확인하기
$ which node

##### 필요없는 node 버전 삭제하기
$ nvm uninstall <version>

만일 새로운 쉘을 실행할 경우 node 의 버전이 system 버전으로 리셋되는데요, 이를 고정하기 위한 커맨드는 다음과 같습니다.

$ nvm alias default 8.9.4

##### 설치되어 있는 가장 최신버전의 node를 디폴트로 사용하기
$ nvm alias default node
터미널을 다시 시작해 확인해 보면 디폴트로 설정된 노드가 실행될 거예요.
