# 웹 사이트 요청 응답 처리

[TOC]



## django.shortcuts 패키지의 render, redirect 함수



### render

```python
render(request, template_name, context=None, content_type=None, status=None, using=None)
```

- 웹 사이트 요청 응답 시 웹페이지로 사용할 Template에 대한 파일 이름과 템플릿 파일내에서 사용할 변수를 지정할 때 사용
- views.py 파일이 초기 생성될 때 기본으로 가지고 오는 함수

```python
from django.shortcuts import render


def BoardsView(request):
	boardList = Boards.objects.all()
	return render(request, 'boardsview.html', {'board': board})
```



### redirect

```python
redirect(to, permanent=false, *args, **kwargs)
```

- 웹 사이트 요청 응답에 대해서 특정 URL로 페이지를 이동할 때 사용
- render는 요청 응답을 위한 웹 페이지 파일을 반환하고, redirect는 웹 사이트의 다른 URL로 이동하는 기능을 수행

```python
from django.shortcuts import redirect


def board_delete_result(request):
	if referer == "board":
		redirection_page = '/boardapp/board_list/' + article.category.category_code + '/'
	else:
		redirection_page = '/boardapp/comm_list/' + article.catetory.category_code + '/'
  
  return redirect(redirection_page)
```



## django.http 패키지의 HttpResponse, JsonResponse 함수



### HttpResponse

```python
HttpResponse(content, content_type=None, status=200, reason=None, charset=None)
```

- 웹 사이트 요청 시 간단한 응답을 위한 객체
- render와 달리 Template으로 사용할 웹 페이지 파일을 사용하지 않는다
- 대신, 응답을 위한 문자열 값을 반환한다

```python
from django.http import HttpResponse

def user_register_idcheck(request):
	...
	msg = "<font color='red'>경고</font>"
	return HttpResponse(msg)
```



### JsonResponse

```python
JsonResponse(data, encoder=DjangoJSONEncoder, safe=True, json_dumps_params=None, **kwargs)
```

- HttpResponse와 유사한 응답 처리 방식으로, 웹페이지에 사용할 데이터를 JSON 방식으로 통신하기 위해 사용
- JSON 형태의 배열, 리스트, 딕셔너리 형태의 변수를 전달한다

```python
from django.http import JsonResonse

def board_like_result(request):
	args = {}  # 딕셔너리 초기화
	args.update({"like_err_msg":"본인의 게시물에는 추천할 수 없습니다"})
	args.update({"article_id":articel_id})
	
	return JsonResponse(args)
```

