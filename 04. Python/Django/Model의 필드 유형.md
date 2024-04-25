## 유형별 모델 필드


|  구분  |        명        | 비고 |
| :----: | :--------------: | :--: |
| 숫자형 |   IntegerField   |      |
|        |    FloatField    |      |
| 문자형 |    CharField     |      |
|        |    EmailField    |      |
|        |    TextField     |      |
|        |     URLField     |      |
| 날짜형 |  DateTimeFiled   |      |
|        |    DateFiled     |      |
|        |    TimeFiled     |      |
|  기타  |  BlooleanFiled   |      |
|        |    ImageFiled    |      |
|        | NullBooleanFiled |      |
|        |    SlugFiled     |      |

## 필드 속성

| 필드명         | 내용                                       | 비고 |
| -------------- | ------------------------------------------ | ---- |
| primary_key    | 모델의 키 값으로 사용할 필드               |      |
| max_length     | 최대 길이 설정                             |      |
| blank, null    | 공백 허용 여부, 미존재 값 여부             |      |
| default        | 기본값                                     |      |
| upload_to      | 파일 업로드 시 경로를 지정하는 용도록 사용 |      |
| 함수 인자 없음 | 모델 필드의 기본값을 그대로 사용할 때      |      |

