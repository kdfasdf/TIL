- https://github.com/kdfasdf/javawebserver/tree/main
의 요구사항 1-3에서 post 방식의 HTTP 요청 메시지에서
그에 상응하는 기능을 수행하고 response를 보내줘야 하는데 
요청 메시지를 받는 과정에서 header와 body를 구분해야 한다.

<br>

- 이전 요구 과정에서 http response 메시지를 만들 때는 헤더에 "\r\n" CRLF를 두번 연달아 사용하면
헤더와 body를 구분할 수 있다는 것을 알게 되었다. 하지만 CRLF가 연달아 있기에 단순하게 response header를 만들 떄와 달리
서버로 들어오는 request header와 body를 CRLF로 구분하기에는 약간의 문제가 되었다

<br>

구글링을 해보니 보통 반복문에 아래와 같은 조건을 넣어 header와 body를 구분하였다

<br>

```
while(!reqMessage.equals("")
  req=br.readLine();
```

<br>

위 코드를 처음 봤을 때는 header와 body 구분을 못하고 body 끝까지 읽는 코드가 아닌가 생각했다
하지만 이는 readLine와 HTTP 헤더 구조 대한 나의 부족한 이해 떄문이었다.
위의 코드는 header와 body를 구분할 수 있는 코드가 맞으며 위 조건 탈출 후 read()를 한번 더 사용하면 
request message의 body 부분을 읽어낼 수 있다.

<br>

우선 Http request 메시지의 구조는 다음과 같다

<br>

![image](https://github.com/kdfasdf/TIL/assets/96770726/e51682f9-a0dd-4125-98fe-76dca48d8e6d)

<br>

- 그리고 헤더를 읽어들일 BufferedReader의 readLine() 메서드에 대한 설명은 다음과 같은데

BufferedReader.readLine()

<br>

```
Reads a line of text. A line is considered to be terminated by any one of a line feed ('\n'), a carriage return ('\r'), or a carriage return followed immediately by a linefeed.
Returns:
A String containing the contents of the line, not including any line-termination characters, or null if the end of the stream has been reached
```

<br>
<br>

readLine() 메서드는 한 줄이 라인피드(LF) ('\n') 혹은 캐리지 리턴(CR) ('\r') 혹은 캐리지 리턴 뒤에 라인피트가 바로 붙는 CRLF에 의해 종료 되는 것으로 간주하고
CR , LF, CRLF 와 같은 라인 종료 문자들을 포함하지 않은 즉 CR , LF, CRLF을 읽기 전 까지의 문자열을 return 한다 만약 스트림의 끝에 도달하면 null을 return 한다

따라서 while 문 안에서 readLine()이 한줄 씩 읽어서 request message 의 header부분을 읽어나간다 그리고 header부분에 끝에 다다랐을 떄 첫 번째 CRLF를 만나 마지막 
header 메시지가 저장되고 두번째CRLF를 만나면 두번쨰CRLF 바로 이전문자가 CRLF였으므로 읽어들일 문자가 없어 ""인 것이다 따라서 반복문 탈출할 시 더 이상 읽을 헤더정보는 없고
body 정보를 읽을 수 있는 것이다.

결과적으로 request body message를 읽는 코드는 다음과 같이 구현할 수 있다.

```
while(!reqMessage.equals("")
  req=br.readLine();
  if(reqMessage.contains("Content-Length)){
    contentLength = getContentLength)
}
char[] body = new char[contentLength]; 
String bodyMessage = String.copyValueOf(br.read(body,0,contentLength));
```
