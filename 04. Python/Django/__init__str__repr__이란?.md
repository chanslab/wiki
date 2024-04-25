# __ init __ : initialize (초기화)

객체를 만들 때 제일 처음 실행되는 초기화 메서드

```python
class Test():
	def __init__(self, num1 = None, num2 = None):
		if num1 == None:
			self.num1 = "X"
		if num2 == None:
			self.num2 = "X"
			return 
		self.num1 = num1
		self.num2 = num2
```

 

# __ str __ : string (문자열)

객체 자체를 출력할 때 넘겨주는 형식을 지정해주는 메서드

```python
def __str__(self):
	if self.num1 == "X" or self.num2 == "X":
		return "Has no arguments"
	else:
		return f"print method : num1 + num2 = (self.num1+self.num2)" 
```



# __ repr __ : representation(표현)

사용자가 객체 자체를 이해할 수 있게 표현해 주는 메서드

```python
def __str__(self):
	if self.num1 == "X" or self.num2 == "X":
		return "Has no arguments"
	else:
		return f"print method : num1 + num2 = (self.num1+self.num2)" 
```



# __ str __ 과 __ repr __ 의 차이

__ str __ 은 해당 클래스의 특정 데이터를 **다른 객체들 간에 전달**하고 싶을 때 사용

__ repr __ 은 해당 클래스에 대해 **사용자에게 정보를 전달**하고 싶을때 사용



## 클래스에 __ str __ , __ repr __  정의하지 않을 경우

##### class의 메모리 주소가 출력된다

```python
>>> class Color():
...     def __init__(self, name):
...             self.name = name
...
>>> red = Color('red')
>>> yellow = Color('yellow')
>>>
>>> arr = [red, yellow]
>>> for a in arr:
...     print(a)
...
<__main__.Color object at 0x7fd331b1a460>
<__main__.Color object at 0x7fd331b1ab50>
```

## 정의 했을 경우

```python
>>> class Color():
...     def __init__(self, name):
...             self.name = name
...     def __str__(self):
...             return f'__str__: {self.name=}'
...     def __repr__(self):
...             return f'__str__: {self.name=}'
...
>>> red = Color('red')
>>> yellow = Color('yello')
>>> black = Color('black')
>>>
>>> alist = [red, yellow, black]
>>>
>>> for i in alist:
...     print(i)
...
__str__: self.name='red'
__str__: self.name='yello'
__str__: self.name='black'
```

__ str __ 함수가 호출된다.  __ repr __ 함수 보다 우선 순위가 높다

### repr을 정의하지 않았을때 : 리스트를 출력하면 메모리 주소가 출력된다

```python
>>> class Color():
...     def __init__(self, name):
...             self.name = name
...     def __str__(self):
...             return f'__str__: {self.name}'
...
>>> red = Color('red')
>>> black = Color('black')
>>>
>>> alist = [red, black]
>>> print(alist)
[<__main__.Color object at 0x7fd331b2adc0>, <__main__.Color object at 0x7fd331b2a8e0>]
```

### repr을 정의할 때 : repr 함수가 호출된다

```python
>>> class Color():
...     def __init__(self, name):
...             self.name = name
...     def __str__(self):
...             return f'__str__: {self.name}'
...     def __repr__(self):
...             return f'__repr__: {self.name}'
...
>>> red = Color('red')
>>> black = Color('black')
>>> yellow = Color('yellow')
>>>
>>> alist = [red, yellow, black]
>>>
>>> print(alist)
[__repr__: red, __repr__: yellow, __repr__: black]
```

## f 스트링을 사용할 때 : !r 을 붙히면 repr 함수가 호출된다

```python
>>> from datetime import date
>>> f"오늘은 {date.today()} 입니다."
'오늘은 2023-02-18 입니다.'
>>> f"오늘은 {date.today()!r} 입니다."
'오늘은 datetime.date(2023, 2, 18) 입니다.'
```

### (참고) f스트링 사용할 때 변수명과 변수값을 출력시 변수를 1번만 사용해도 된다

```python
>>> num = 1
# 기존

>>> print(f'num={num}')
num=1

# python 3.8 이상
>>> print(f'{num=}')
num=1
```

