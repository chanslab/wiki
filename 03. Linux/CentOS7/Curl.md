## 주요 옵션
| short | long | Comments |
|:---:|:---:|:---|
| -k | --insecure | https 사이트를 SSL certificate 검증없이 연결 |
|-l|--head|HTTP 헤더만 출력(바디는 출력하지 않음) |
|-L|--location|redirection(301, 302코드) 인 경우, 해당 urㅣ을 추적하여 실행, 디폴트 50회|
|-d|--data|HTTP Post Data를 출력함, HTTP Post 메소드, JSON 데이터 등 추적할 때 사용|
|-v|--verbose|상세하게 출력|
|-o|--output FILE|표준 출력대신에 해당 FILE에 출력함. 다운로드시에 유용하게 사용|
|-O|--remote-name|-o와 유사하나, 원격 파일 이름으로 저장|
|-s|--silent|진행 내용 등을 출력하지 않음. 응답코드 정도 확인 시에 유용함|
|-S|--show-error|Show error even when -s is used|
|-X|--request|Request시 사용할 method(GET,POST,PUT,PATCH,DELTE) 기술|

```shell
$ curl -X GET "localhost:9200/?pretty"
# pretty는 가독성을 좋게 해줌
```


## 사용예제
```shell
$ curl -o response.txt https://www.example.net  # 결과를 "지정된" 이름으로 파일에 저장
$ curl -O https://www.example.net/index.html    # 결과를 파일이름으로 저장
$ curl -k https://www.example.net   # SSL증명서 에러 무시
$ curl -s -o response.txt http://www.example.net    # 진행상황을 표시 하지 않기, 에러도 표시되지 않음
$ curl -sS -o response.txt http://www.example.net   # 에러메시지는 보고 싶을때
$ curl -* -O http://www.example.net/index.html  # progress bar로 진척상황표시
$ curl -x <proxyip>:<port> --proxy-user <username>:<password> http://www.example.net    # proxy이용시
$ curl -x <username>:<password>@<proxyip>:<port> http://www.example.net    # proxy이용시
$ curl -L http://www.example.net    #301/302등의 redirect를 자동인식
$ curl -X [PUT|GET|POST] http://www.example.net # http의 메소드를 지정
$ curl -w '\n' 'http://www.example.net/posturl' -X POST --data 'name=myname&mode=create'    # parameter를 POST로 송신 
$ curl -sS -w '%{http_code}\n' http://www.example.net # status code만 출력
$ curl -I http://www.example.net    # 헤더만 출력, -i는 body도 출력
http 자세한 정보를 볼때, request header를 확인 할 때 필요
$ curl -v http://www.example.net    # request header를 확인할때
$ curl -sS http://www.example.net -X POST -F "test=data" --trace.log trace.log -o /dev/null # --trace는 binary, --trace-ascii는 텍스트, --trace-time은 시간표시
$ curl -sS http://www.example.net -X POST -v -F "test=data" --trace-ascii trace-ascii.log -o /dev/null
$ curl -s http://www.example.net -o /dev/null -w '%{http_code}¥n' # reqeust의 결과만 확인
$ for((;;)) { curl -v --header "Connection: keep-alive" "http://www.example.net";}  # DDoS 부하시험
$ curl --limit-rate [10k|1m,1g] http://www.example.net  # 전송속도 제한 (k, m, g등을 이용)
$ curl -c cookie.txt http://www.example.net # 수신한 쿠키를 저장
$ curl -b cookie.txt http://www.example.net # 저장한 쿠키를 송신
$ curl --connect-timeout 600 http://www.example.net # 최대접속시간제한을 설정
$ curl -s -w '%{http_code}\n' https://www.amazon.co.jp/dp/B00JEYPPOE/ -o /dev/null
503 # User-Agent를 지정
$ curl -s -w '%{http_code}\n' https://www.amazon.co.jp/dp/B00JEYPPOE/ -o /dev/null  -A ''
200 # User-Agent를 지정
$ curl -H "Host: www.example.net" -k https://<IP address>   # Header를 지정
```

### (예제) 연속된 URL로 요청하고 결과 파일로 저장
여러개의 url로 되어 있는 동영상을 다운로드 할 때
```shell
$ curl "https://example_url/[0000001-000188].m4s" -o "#1.m4s" # [0000001-000188]까지 연속으로 접속해서,  [0000001-000188].m4s 파일로 저장
```
### (예제) redirect을 따라가는 명령어
예를 들어 https://example.com/url_org 가 https://example_com/url_redirect로 연결될 경우
```shell
$ curl -L https://example.com/url_org 
```