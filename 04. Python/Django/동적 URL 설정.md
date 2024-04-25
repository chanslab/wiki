# 동적 URL 설정

### app_name

* 동적으로 URL을 생성해서 사용하기 위해서는 app 별로 분리된 하위 urls.py에 app_name 속성이 필요
* app의 패키지명(디렉터리명)을 사용한다

```python
# users/urls.py
...
app_name = "users"
urlpatterns = [
	...
]
```

```python
# posts/urls.py
...
app_name = "posts"
urlpatterns = [
	...
]
```



### Template을 위한 {% url %} 태그 : URL pattern name

**{% url "URL pattern name"%}** 태그는 Template에서 urls.py의 내용을 이용해 동적으로 URL을 생성 한다

```python
{urls.py에 있는 app_name}:{path()에 지정된 name}
```

```python
# users/urls.py

...
app_name = "users"
urlpatterns = [
	path("login/", login_view, name="login"),
	path("logout/", logout_view, name="logout"),
	path("signup/", signup, name="signup"),
]
```

```html
# templates/users/signup.html

<a href="{% url 'users:login' %}"> 로그인 페이지로 이동 </a>
```

