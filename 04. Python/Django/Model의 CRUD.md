## Model 데이터 처리

### 1. 삽입(Insert), 수정(Update)

- #### save() 메소드 사용

  ```python
  board = Boards(id=1, title="제목", content="내용")
  board.save()
  ```

  - id 값이 있으면 수정, 없으면 삽입

### 2. 삭제(Delete)

- #### delete() 메소드 사용

  ```python
  board = Boards.objects.filter(id=1)
  board.delete()
  ```

### 3. 조회(Select)

| 함수       | 내용                              | 비고                                |
| ---------- | --------------------------------- | ----------------------------------- |
| all()      | 테이블상의 모든 데이터셋          |                                     |
| filter()   | 특정 조건에 부합하는 데이터셋     |                                     |
| exclude()  | 특정 조건을 제외한 데이터셋       |                                     |
| get()      | 특정 조건에 부합하는 1개의 데이터 |                                     |
| count()    | 데이터의 개수                     |                                     |
| first()    | 첫 번째 데이터                    |                                     |
| last()     | 가장 마지막 데이터                |                                     |
| exists()   | 데이터 유/무                      |                                     |
| order_by() | 순서대로 정렬                     | Boards.objects.all().order_by('id') |

