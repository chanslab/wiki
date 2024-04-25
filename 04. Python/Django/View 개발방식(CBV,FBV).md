## Class-Based View(CBV)

- 클래스 형태로 구성된 뷰
- Generic View로부터 상속받아서 웹 페이지를 간단히 구성할 때 사용

| Base View    | Generic Display View | Generic Editing View | Generic Date View |
| ------------ | -------------------- | -------------------- | ----------------- |
| view         | ListView             | FormView             | ArchiveIndexView  |
| TemplateView | DetailView           | CreateView           | YearArchiveView   |
| RedirectView |                      | UpdateView           | MonthArchiveView  |
|              |                      | DeleteView           | WeekArchiveView   |
|              |                      |                      | DayArchiveView    |
|              |                      |                      | TodayArchiveView  |
|              |                      |                      | DateDetailView    |

### Base View

- 웹 페이지의 기본적인 형태 구성
- 코드가 다소 복잡
- FBV 사용이 간소화 가독성 측면에서 권장

### Generic Display View

- 게시물 목록, 내용 등을 조회할 떄 사용

### Generic Enditing View

- 양식 전송 및 생성, 수정, 삭제 등의 기능을 수행하는 View
- Display View에 비해 사용빈도 낮음

### Generic Date View

- 년/월/주/일 등 날짜 형태로 게시물 목록을 정렬할 때 사용되는 View

  

## Function Based View

- 사용자 정의 함수에 의해서 웹 페이지를 구성할 때 사용

- HTTP Request를 받으면 함수 내에서 필요한 기능을 수행

- render() 등의 함수를 사용하여 표시하고자 하는 웹 페이지를 반환

  ```python
  from django.shortcuts import render
  from boardapp.models import Boards
  
  def BoadrdsFunctionView(request):
  	boardList = Boards.objects.all()
  	
  	return render(request, 'boardsfunctionview.html', {'boardList':boardList})
  ```

  