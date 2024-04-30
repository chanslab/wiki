### 가상환경 활성화

- [mac] source env_name/bin/activate
- [window]     env_name/Scripts/activate

###### *✓* *맥의* *경우**,* *~/.zshrc* *에* *alias**를* *등록해서* *사용하면* *편리함*
###### *...*
###### *alias activate="source /Users/jcs/workspace/langchain/venv_langchain/bin/activate"*
###### *...*

###  **가상환경** **비활성화**
- deactivate
! conda list 처럼 가상환경 목록을 확인하는 메뉴는 없음

### python venv 다른 파이썬 버전으로 만들기

원래 사용하는 것은 환경변수 path 에있는 파이썬 기본 값으로 만든다.

```
python -m venv venv
```

 
특정버전으로 하고 싶으면 아래와 같이 하면 된다.

```
py -[버전] -m venv [venv명]
```

 

3.6버전으로 하고 싶으면 이렇게

```
py -3.6 -m venv venv36
```

 

## Why venv?

Python Application 개발 시 Standard Library가 아닌 Package와 Module을 사용하여 개발할 경우가 많습니다. 특정 버그가 수정된 버전이 필요하거나, 다른 버전의 Library Interface를 사용하여 프로그램을 개발 할 경우가 있습니다.

즉, 특정 버전의 파이썬 설치만으로 프로그램의 요구 사항을 충족시키는 것이 불가능 할 수도 있다는 뜻입니다. 프로그램_A는 1.0 Version의 Module이 필요하지만, 프로그램_B는 2.0 Version의 Module이 필요할 때, Version 1.0이나 2.0만 설치되면 하나의 프로그램은 실행할 수 없게 됩니다.

이러한 문제의 해결하기 위하여 `Virtual Environment`를 구성합니다.

> - 가상 환경 적용으로 특정 버전의 파이썬과 개발하려는 프로그램에 적용되는 패키지로 독립된 파이썬 환경 구성 가능
> - 의존성과 버전문제 차이로 인한 어플리케이션간 충돌 문제 해결

앞의 예시에서, 프로그램A는 Version 1.0의 파이썬과 관련 라이브러리가 적용된 가상 환경으로 구성하고, 프로그램B는 Version 2.0의 파이썬과 관련 라이브러리가 적용된 가상환경으로 구성할 수 있습니다. 프로그램B에서 라이브러리를 업그레이드 하거나 추가 설치되어도 프로그램A에 영향을 끼치지 않습니다.

![img](https://images.velog.io/images/jbbang/post/463b0353-f6f0-4f5e-a5f3-a2fd02ea1813/%EA%B7%B8%EB%A6%BC1.png)

## 가상환경 구성

virtualenv나 venv 모듈을 이용하여 가상환경을 생성합니다.

- virtualenv : 별도로 설치 필요
- venv : python 3.4 버전부터 기본적으로 내장됨

가상환경을 만드는데 3.5버전부터는 venv를 권장합니다.

**1. venv 옵션 확인**

> ```null
> ￦> python -m venv –help
> ```
>
> > **-m** : python에 -m 옵션을 지정해서 pip를 실행할 수도 있습니다. -m 옵션은 모듈을 실행하는 옵션이며 pip도 모듈입니다.

**2. 가상환경 생성**

> ```null
> ￦> py -3.8 -m venv program_a_venv
> ```
>
> > **-3.8** : python 버전 선택 시(python 3.8 version)
> > **program_a_venv** : 가상환경 구성할 폴더명

명령을 실행하면 `program_a_venv` 폴더가 생성되고, Python 바이너리/바이너리의 복사/심볼릭 링크를 포함 하는 하위 디렉토리를 생성합니다.

**3. 가상환경 활성화**

> ```null
> ￦> venv\Scripts\activate
> ```

실행 시 아래와 같이 커맨드 앞에 (program_a_venv)가 붙음

> ```null
> (program_a_venv)￦>
> ```

**4. pip 모듈 설치(test)**

> ```null
> (program_a_venv)￦> pip install numpy==1.21.4
> ```

**5. 비활성화**

> ```null
> (program_a_venv)￦> deactivate
> ```

실행 시 아래와 같이 복귀

> ```null
> ￦>
> ```

## 가상환경 구성 테스트

처음 예시로 들었던 내용과 같은 형태의 가상환경을 구성합니다.

> - Program A
>   - python version : 3.8
>   - numpy version : 1.21.4
>   - venv 폴더명 : program_a_venv
> - Program B
>   - python version : 3.9
>   - numpy version : 1.22.0
>   - venv 폴더명 : program_b_venv

결과

> - Program A
>   ![img](https://velog.velcdn.com/images%2Fjbbang%2Fpost%2F5f8b4483-0a1f-408e-826c-608377bf9817%2Fimage.png)

> - Program B
>   ![img](https://velog.velcdn.com/images%2Fjbbang%2Fpost%2Ffea2df5a-8718-44a0-9422-dcb77af6209c%2Fimage.png)

각각 프로그램 환경에 대하여 python version, pip list로 버전을 확인해 보았습니다.

## Reference

> - https://docs.python.org/3/tutorial/venv.html
> - https://docs.python-guide.org/dev/virtualenvs/
> - https://virtualenv.pypa.io/en/latest/
> - https://www.baylor.edu/library/index.php?id=972719





