## 웹 사이트 요청 처리

- 웹브라우저를 통해서 웹사이트에 대한 요청을 할 경우, 

- Django에서는 요청 주소와 연결된 뷰를 호출한다

- 뷰를 호출할 때에는 기본적으로 request 변수를 사용하여 요청을 받는다

  ```python
  def board_list(request):
  	...
  ```

  - FBV에서는 파라미터로 request 변수가 있다

  - CBV에서는 request 변수가 명시되어 있지 않다

    - Generic View에 내장된 get(), post(), dispatch() 등의 메소드를 통해서 정보를 받는다

      ```python
      class BoardListView(ListView):
      	def dispatch(self, request):
      		...
      ```

  > 웹 사이트 요청은 FBV, CBV 상관없이 클래스 및 함수를 호출 했을 경우, 
  >
  > 요청에 사용되는 **request 변수를 파라미터로 지정하여 요청 정보를 받는다**

### POST 방식

- HTML의 Form으로 부터 데이터를 전송할 때 사용되는 방식

- request 변수의 method 변수에 'POST' 값이 저장

- Form에서 입력받은 데이터는 POST라는 이름의 딕셔너리형 변수로 저장됨

  ```python
  def board_list_page(request):
  	if request.method == 'POST':
  		name = request.POST['title']    # title은 form에서 입력받은 요소 변수
  ```

### GET 방식

- URL에 변수와 값을 입력하여 전송하는 형태

  ```python
  https://localhost:8080/boardapp/board_list/?page=3
  
  def board_list(request):
  	page = int(request.GET["page"])
  ```



> POST, GET 방식 모두 request.POST['key'], request.GET['key']로 요청 정보를 받을때 'key' 라는 이름의 데이터가 존재하지 않으면 에러가 발생

#### try-catch를 사용해 처리 한다

```python
try:
	page = int(request.GET('page'))
except:
	page = 1
```

#### 또는 get() 메소드를 사용한다

```python
title = request.POST.get('title')
page = int(request.GET.get('page'))
```



### File 및 Image 전송

- 이미지 또는 파일은 POST 방식으로 전송하도록 되어 있다

- **View에서는 전송 받은 파일을 처리 할 때 request.POST 가 아닌 request.FILE 변수를 사용한다**

  ```python
  dev board_list_page(request):
  	if request.method == 'POST':
  		name = request.POST['title']
  		image = request.FILE['img_file']
  ```



### CSRF(Cross Site Request Forgery) 방지 설정

- 사이트 간 요청 위조 공격

- CSRF 방지를 위한 규격 설정이 가능하다

  - View에서 CSRF 방지 설정을 위한 패키지를 호출
  - 폼을 사용하는 모든 View에서 CSRF 방지 설정을 사용하고 해당 값을 템플릿 변수로 반환한다
  - 템플릿 파일은 View에서 반환한 CSRF 방지 설정을 사용하기 위해서 CSRF Token을 본문에 지정한다
  - 폼 전송시 csrfmiddlewaretoken 변수 값을 올바르게 전송할 수 있도록 구성한다

  ```python
  from django.shortcuts import render
  from django.template.context_processors import csrf
  
  def memberRegisterFromPage(request):
  	args = {}
  	args.update(csrf(request))
  	
  	return render(request, 'member_register_form.html', args)
  ```

- POST 요청에 대해서 GET 요청보다 높은 보안 수준을 적용한다

- 핵심은 로그인한 사용자가 의도하지 않은 POST 요청을 거부 하는 것

- Django는 해커가 임의 POST 요청을 할 수 없도록 한다

  - Django는 새로운 요청을 하는 브라우저마다 구분되는 값을 서버에 저장한다
  - POST 요청을 하는 form이 브라우저별로 구분되는 값을 가지지 않는다면, 요청을 거부한다
  - 브라우저별로 구분되는 값은 서버에 저장
    - 브라우저를 사용하는 사람은 값을 알 수 없다
      - 실 사용자의 POST 요청도 거부되게 된다
    - 그래서, Django는 실 사용자가 해당 값을 사용할 수 있는 기능을 제공한다
    - template에서 {% csrf_token %} 태그를 사용하면, 이 영역은 브라우저별로 구분되는 값으로 치환된다
    - 이 값을 확인할 수 있는 시점은 HTML 파일이 사용자에게 전달되어 브라우저에 그려진 다음이며, 해커는 이 값을 미리 알 방법이 없다
    - Django는 form 요청에 브라우저별로 구분되는 값이 포함되어 있는것을 확인하고, POST 요청을 수락한다
    - 브라우저별로 구분되는 값을 Django에서는 CSRF token 이라고 부른다
  
- template에서는 {% csrf_token %} 이라는 구문을 명시, 해당 부분이 input 태그의 hidden 속성을 가진 태그로 변경되며, 암호화된 값을 가진다

- 특정 뷰에서는 csrf 방지 설정 기능을 이미 내장하고 있다

  - 뷰에서 csrf(request)를 생략해도 템플릿에서 즉시 사용할 수 있다
  - 특정 뷰는 다음과 같다
    - 함수 형태의 뷰(FBV)에서 render를 사용하여 응답을 전송할 경우
    - Generic View 로부터 상속받은 클래스 형태의 뷰(CBV)를 사용할 경우
  - django.contrib 패키지를 사용하여 뷰를 구현할 경우