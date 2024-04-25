## MTV(Model-Template-View) 

### Model

- Django와 데이터베이스를 연결시켜주는 코드

- 데이터의 형태를 나타냄

- 모든 Model 클래스는 django.db.models.Model클래스를 상속

- 각각의 모델은 테이블과 매핑, 모델의 속성은 테이블의 필드를 나타냄

- 파일명은 기본적으로 models.py 를 사용

  ```python
  class DjangoModel(models.Model):
  	name = models.CharField("이름")
  ```

### Template

- 웹 브라우저로 돌려줄 코드, 사용자에게 제공될 결과물의 형태

- HTML을 사용

- Templates 디렉토리 내에 HTML 파일을 사용

  ```html
  <!DOCTYPE html>
  <html lang="ko">
  	<body>
  		<h1>DjangoTemplate</h1>
  	</body>
  </html>
  ```

### View

- 사용자의 요청을 받아 처리하는 웹 사이트의 로직

- 함수(Function)를 사용

- 파일명은 기본적으로 views.py를 사용

  ```python
  def django_view(request):
  	return HttpResponse("Django View")
  ```
