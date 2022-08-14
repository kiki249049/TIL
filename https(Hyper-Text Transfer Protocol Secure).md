### 1. https(Hyper-Text Transfer Protocol Secure)

요새 사이트를 보면 전부 사이트주소앞에 https가 붙어있는 것을 볼 수 있다.

ex) https://www.google.com

https의 s를 보면 알 수 있다시피 Secure즉, **보안**에 대한 규약이다



https의 좋은점은 크게 2가지로 나뉜다.

1. 내가 어떤 웹사이트에 보내는 정보를 다른 누군가가 훔쳐보지 못하게한다.

- 예를 들어 우리 ssokdam.com 사이트에서 로그인을 하게 되면 ssokdam.com의 백엔드서버로 정보가 가게 되는데({id: test, pw : test}) http로 보내게 되면 누구든 그냥 알아볼 수 있는 형식으로 보내지게 된다.(중간에 누군가가 인터셉트 가능 => 정보 털림)
- https로 보내게 되면 우리가 보낸정보(id: test, pw: test)를 뒤죽박죽된 텍스트로 변경해서 보낸다. ^$%^@$@^!@$!@$ 이런식으로 ssokdam.com서버만 알아볼 수 있는 상태로 정보를 보내게 된다.

2. 신뢰할 수 있는 사이트인지를 판별해 준다.

- 예를들면 네이버링크를 클릭했는데 이상한 피싱사이트로 연결된 경우 http형식으로 돼 있기때문에 주소창에 "안전하지 않다"라는 문구와 함께 주의창이 나타나게 된다.(https는 기관으로부터 검증된 사이트만 주소에 사용할 수 있기 때문)

=> http보다 https보다 안전한 이유!



그렇다면 http는 무엇일까?

=> 인터넷상의 커뮤니케이션에 사용되는 형식들 중 하나!

예를 들어

```http
:authority : www.naver.com
:method : GET
:path: /
:scheme: https
...
```

이런형식을 서버에 보낸다 했을때 어떤 형식인지 기재를 안해주었을 경우 서버에서 알아먹지를 못한다.

그렇기때문에 http(s)라는 형식이라고 주소창 앞에 기재를 해줌으로써 http형식인지 서버에서 알아먹고 그 형식으로 읽어 페이지를 보내주는 것



https에서 조금 더 깊게 들어가 보면 대칭키 & 비대칭키에 대해서 알아야한다.

### 2. 대칭키 방식  

=> 주는쪽과 받는쪽이 같은 방식으로 암호화하고 복호화를 한다.

ex) 클라이언트 : A => X라는 key를 사용해서 암호화 => !@#$%^&로 변환

​	   서버 : !@#$%^&를 받고 => X라는 key를 사용해서 복호화 => A

여기서 대칭키의 약점! 만약에 X라는 key누군가 훔쳐가버린다면? 보안은 뚫리게 된다.

![img](https://velog.velcdn.com/images%2Fminj9_6%2Fpost%2Fd5082238-3853-4523-bae9-44f83a1dc0e9%2Fimage.png)

### 3. 비대칭키(공개키) 방식  

대칭키 방식의 보완책 

ex) 클라이언트 : A => X(공개키)라는 key를 사용해서 암호화 => !@#$%^&로 변환

​	   서버 : !@#$%^&를 받고 => Y(개인키)라는 key를 사용해서 복호화 => A

X를 누구나 볼 수 있는 키(공개키)로 설정하고 Y키를 개인키로 서버에 숨겨둔다.

X라는 공개키를 중간에 가로채도 Y라는 개인키가 없기때문에 다른사람이 볼 수 없음

반대 방향으로 서버에서 Y(개인키)키로 암호화된 정보로 클라이언트단으로 보내는건 X(공개키)로만 복호화할 수 있기 때문에 정보를 받은 서버가 올바른 서버인지 특정 할 수 있다.



더 깊게 들어가보자. Https가 구현되는 과정?

처음에 말했듯이 https가 신뢰할 수 있는 사이트라는 것을 증명해준다는 것은 공인된 민간기업이 "인증"을 해주었기 때문이다. => 그럼 어떻게 인증을 하는건가?

### 4. CA(Certificate Authority)

를 통해서 인증한다.

CA를 해줄수 있는 회사는 다음과 같다.

| 1    | [코모도](https://ko.wikipedia.org/wiki/코모도_그룹)          | 6.1%   | 41.0% |
| ---- | ------------------------------------------------------------ | ------ | ----- |
| 2    | [시만텍](https://ko.wikipedia.org/wiki/시만텍)               | 5%     | 30.2% |
| 3    | [고 대디](https://ko.wikipedia.org/wiki/고_대디)             | 2.2%   | 13.3% |
| 4    | [글로벌사인](https://ko.wikipedia.org/w/index.php?title=글로벌사인&action=edit&redlink=1) | 1.7%   | 10.4% |
| 5    | [DigiCert](https://ko.wikipedia.org/w/index.php?title=DigiCert&action=edit&redlink=1) | 0.5%   | 3.1%  |
| 6    | [StartCom](https://ko.wikipedia.org/w/index.php?title=StartCom&action=edit&redlink=1) | 0.4%   | 2.2%  |
| 7    | [Entrust](https://ko.wikipedia.org/w/index.php?title=Entrust&action=edit&redlink=1) | 0.1%   | 0.8%  |
| 8    | [버라이즌](https://ko.wikipedia.org/wiki/버라이즌_커뮤니케이션스) | 0.1%   | 0.7%  |
| 9    | [Trustwave](https://ko.wikipedia.org/w/index.php?title=Trustwave_Holdings&action=edit&redlink=1) | 0.1%   | 0.6%  |
| 10   | [세콤](https://ko.wikipedia.org/wiki/세콤)                   | 0.1%   | 0.6%  |
| 11   | Unizeto                                                      | 0.1%   | 0.4%  |
| 12   | [Buypass](https://ko.wikipedia.org/w/index.php?title=Buypass&action=edit&redlink=1) | 0.1%   | 0.1%  |
| 13   | QuoVadis                                                     | < 0.1% | 0.1%  |
| 14   | [도이체 텔레콤](https://ko.wikipedia.org/wiki/도이체_텔레콤) | < 0.1% | 0.1%  |
| 15   | [네트워크 솔루션스](https://ko.wikipedia.org/w/index.php?title=네트워크_솔루션스&action=edit&redlink=1) | < 0.1% | 0.1%  |
| 16   | [SwissSign](https://ko.wikipedia.org/w/index.php?title=SwissSign&action=edit&redlink=1) | < 0.1% | 0.1%  |

아무회사나 될 수 있는게 아니라 엄격한 인증과정을 거쳐서 CA를 할 수 있는 회사가 될 수 있다고한다. 

각 브라우저에 CA를 해줄 수 있는 회사 목록이 있다고한다.

그럼 구체적으로 브라우저에서 사이트에 접속을 할 때 어떤과정을 거치는지 알아보자

1. 처음 클라이언트는 서버를 신뢰하지 못하기때문에 랜덤데이터를 생성해서 서버에 보내게 된다.
2. 랜덤데이터를 받은 서버는 답변으로 서버측에서 생성한 무작위 데이터와 "인증서"를 같이 실어 보낸다.

--- 여기까지의 과정을 handshake(악수)를 했다고 표현을 한다. ----

3. 그러면 이제 클라이언트에서는 이 인증서가 진짜인지 브라우저에 내장된 CA들의 정보를 통해 확인한다.

인증서들은 CA의 개인키로 암호화돼 있기때문에 CA의 공개키로 복호화시켜 진짜인지 가짜인지 판별가능(비대칭키 방식으로 검증한다.) => 이 과정에서 통과를 못하면 주소창에 ! "주의"표시가 뜨게 된다.

![img](https://mblogthumb-phinf.pstatic.net/MjAyMDA0MTdfNDcg/MDAxNTg3MTA2MjcxMDI4.izNFUi6s0ANinrGCEQZlsgk2DfUAVorDuwASVf0lAu4g.cdpthwXpHs4EjY8OvnG7GgJ9Qjqxp2hrVEor3_xE9iUg.PNG.wincert/SE-ad36a241-4f43-4b65-96c2-1955ba4ecfc0.png?type=w800)

4. 이렇게 인증절차가 완료되면 인증서에 "서버의 공개키"가 있고 "대칭키"방식으로 데이터 통신을 하게 된다. 

=> 여기서 좋은 비대칭키 방식을 냅두고 대칭키 방식으로 통신하는 이유는 비대칭키는 컴퓨터에 부하가 많이 가기 때문에 대칭키 방식으로 통신을한다. 

=> 대칭키 방식은 탈취할 수 있어서 보안에 취약하다 하지 않았나? => 대칭키를 공유할때 비대칭키 방식을 사용하기 때문에 탈취할 수 없음