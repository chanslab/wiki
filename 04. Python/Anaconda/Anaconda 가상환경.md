# 가상환경 설정

#### Anaconda와 pycharm 활용

Anaconda를 설치하면 conda 가상환경을 사용 할 수 있다

pycharm에서 가상환경을 만들면서 작업한다 

또는 만들어 놓은 가상환경을 사용해도 된다



## Anaconda 가상환경 

#### 가상환경 생성

###### 인터넷에 연결되어 있어야 생성된다

```python
conda create -n <가상환경명>
conda create -n <가상환경명> python
conda create -n <가상환경명> python=3.10
```

#### 가상환경 삭제

```python
conda remove -n <가상환경명> --all
```

#### 가상환경 확인

```python
conda info -e
```

#### 가상환경 Activate, Deactivate

```python
conda activate <가상환경명>
conda deactivate
```

#### 가상환경에 라이브러리 설치

##### 라이브러리 검색

```python
conda search <라이브러리명>
conda search --full-name <라이브러리명>
```

##### 라이브러리 설치/삭제

```python
conda install <라이브러리명>
conda uninsall <라이브러리명>
```

##### 라이브러리 목록 확인

```python
conda list
```

#### Anaconda  update

```shell
conda update -n base conda		
```

