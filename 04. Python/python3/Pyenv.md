### https://www.daleseo.com/python-pyenv/

## 여러 버전의 파이썬 관리하기 (pyenv)

macOS에 내장된 파이썬의 정확한 버전과 바이너리 파일의 위치는 다음과 같이 확인하실 수 있습니다.

```bash
$ python -V
Python 2.7.15
$ which python
/usr/bin/python

# Mac에서 파이썬 3 설치
# Mac의 패키지 매니저인 Homebrew를 이용하면 터미널에서 간편하게 파이썬 3를 설치할 수 있습니다.
$ brew install python

# 설치한 파이썬 3의 정확한 버전과 바이너리 파일의 위치는 다음과 같이 확인하실 수 있습니다.
$ python3 -V
Python 3.7.6
$ which python3
/usr/bin/python3
```

이제부터 Mac에 내장된 파이썬 2가 사용해야 할 때는 python, 직접 설치한 파이썬 3를 사용해야 할 때는 python3 커맨드를 사용하면 됩니다. 마찬가지 방식으로 파이썬 2 패키지를 설치할 때는 pip, 파이썬 3 패키지를 설치할 때는 pip3 커맨드를 사용합니다.

#### 오직 파이썬 3만 쓰기

파이썬 2의 지원이 공식 중단 됨에 따라 앞으로 파이썬 2를 사용하는 프로젝트는 줄어들 것이고 그에 따라 점점 파이썬 2를 사용할 일이 적어질 것입니다. 저처럼 파이썬 2를 사용할 일이 거의 없는 분이라면, 위와 같이 굳이 2개의 커맨드를 사용할 이유가 없을 것입니다.

이럴 경우, 다음과 같이 python과 pip 커맨드가 파이썬 3 바이너리를 바라보도록 별칭(alias)를 설정해주면 됩니다.

```bash
$ echo "alias python=/usr/local/bin/python3" >> ~/.bash_profile
$ echo "alias pip=/usr/local/bin/pip3" >> ~/.bash_profile
# Zsh를 사용하시는 분들은 .bash_profile 파일 대신에 .zshrc를 사용하면 됩니다.

$ echo "alias python=/usr/local/bin/python3" >> ~/.zshrc
$ echo "alias pip=/usr/local/bin/pip3" >> ~/.zshrc
# .bash_profile(또는 .zshrc) 파일의 변경 사항을 적용하고 python 커맨드를 날리면 파이썬 3 런타임이 실행되는 것을 볼 수 있습니다.

$ exec "$SHELL"
$ python -V
Python 3.7.6
$ which python
pip: aliased to /usr/local/bin/python3
```

#### pyenv로 여러 파이썬 버전 변경하기

파이썬 3만을 쓰더라도, 하나의 Mac에서 3.5, 3.6, 3.7, 3.8 등 여러 마이너 버전의 파이썬을 사용하고 싶을 때가 있습니다. 이럴 경우, pyenv 패키지를 사용하면, 좀 더 쉽게 여러 버전의 파이썬을 설치하고 변경할 수 있습니다.

먼저 Homebrew를 이용해서 pyenv 패키지를 설치합니다.

```bash
$ brew install pyenv
# 그 다음, .bash_profile(또는 .zshrc) 파일에 pyenv가 활성화 되도록 관련 스크립트를 추가해줍니다.

$ echo -e 'if command -v pyenv 1>/dev/null 2>&1; then\n  eval "$(pyenv init -)"\nfi' >> ~/.bash_profile
# 그리고 .bash_profile(또는 .zshrc) 파일의 변경 사항을 적용해줍니다.

$ exec "$SHELL"
# 자 이제, pyenv를 사용할 준비가 끝이 났습니다! 👍 pyenv install 커맨드로 여러 버전의 파이썬 3를 설치해봅니다.

$ pyenv install 3.7.6
$ pyenv install 3.8.1
# 드디어, pyenv global 커맨드를 이용해서 두 개 버전의 파이썬 사이를 자유롭게 넘나들 수 있게 되었습니다. 🎉

$ pyenv global 3.8.1
$ python -V
Python 3.8.1
➜  new-blog git:(new-contents) ✗ pyenv global 3.7.6
➜  new-blog git:(new-contents) ✗ python -V
Python 3.7.6


# pyenv versions 커맨드를 통해서 Mac에 어떤 버전의 파이썬이 설치되어 있고, 이 중 현재 어떤 버전이 활성화되어 있는지 확인할 수 있습니다.

$ pyenv versions
  system

* 3.7.6 (set by /Users/dale/.pyenv/version)
  3.8.1
```

