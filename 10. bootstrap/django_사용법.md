django에서는 static 디렉토리를 만들어서 css, js 등을 처리한다

책에서는 APP별 static 디렉토리를 만들어서 사용하는데 

전체 사이트의 css, js 를 관리하는 방법은 다음과 같다



![image-20230417093111797](D:\workspace\lab\Assets\image-20230417093111797.png)

* static 디렉토리는 workspace 폴더의 가장 최상윙 위치한다
  * 프로젝트, APP 디렉토리와 같은 위치

```django
<!DOCTYPE html>
{% load static %}
<html lang="ko">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Blog</title>

    <!-- bootstrap -->
    <link rel="stylesheet" href="{% static 'bootstrap5/css/bootstrap.min.css' %}" type="text/css" media="screen">

    <!-- fontawesome -->
    <link href="{% static 'fontawesome6/css/fontawesome.css' %}" rel="stylesheet">
    <link href="{% static 'fontawesome6/css/brands.css' %}" rel="stylesheet">
    <link href="{% static 'fontawesome6/css/solid.css' %}" rel="stylesheet">

    <!-- css-->
    <link rel="stylesheet" href="{% static 'css/blog.css' %}" type="text/css" media="screen">
</head>

<body>
... 생략 ...
</body>

<!-- Bootstrap core JS-->
<script src="{% static 'bootstrap5/js/bootstrap.bundle.min.js' %}"></script>

</html>
```

