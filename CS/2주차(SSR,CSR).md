# CRS & SSR

웹 사이트를 `랜더링`하는 것에는 **서버 사이드(SSR)**와 **클라이언트 사이드(CSR)**라는 두 가지 접근법이 있다.

## 0. 브라우저 랜더링이란?

브라우저가 서버로부터 요청해 받은 내용을 화면(view)에 표시해주는 작업을 의미한다.
즉, 브라우저가 서버로부터 HTML, CSS, JavaScript 문서를 전달받아 브라우저 엔진이 각 문서를 해석해 브라우저 화면을 그려주는 것

## 그러나

그러나 서버 사이드 랜더링, 클라이언트 사이드 랜더링에서의 `랜더링` 의 뜻은 다르게 해석해야한다.
여기서 랜더링의 의미를 정확하게 따지자면, **HTML 파일 내에 내용이 있느냐 없느냐
내용이 있다 → 랜더링 / 내용이 없다 → 랜더링 되지 않음** 
으로 이해하고 넘어가자

## 1. 서버 사이드 랜더링(SSR)

→ **서버쪽에서 랜더링 준비를 마친 상태로 클라이언트에게 전달하는 방식**

서버 사이드 렌더링(SSR)은 웹사이트가 서버에서 렌더링되는 것을 의미합니다. 
**따라서 더 빠른 첫 로딩을 제공할 수 있지만, 페이지간의 이동에서 모든것들을 매번 다운로드해야합니다.** 
브라우저를 넘어 훌륭하게 동작하고 개발 프로세스를 돕는 많은 도구들이 있지만, 각 페이지를 로딩할 때마다 서버를 거쳐야 한다는 점에서 로딩 속도 및 성능으로 인식되는 일반적인 측면에서 어려움이 있습니다.

![Untitled](https://velog.velcdn.com/images/sjc0829/post/31d64940-7711-4fd7-9af8-c17ef6a3c688/image.png)

> 
> 
> 1. User가 Website 요청을 보냄.
> 2. Server는 'Ready to Render'. 즉, 즉시 렌더링 가능한 `html`파일을 만든다.(리소스 체크, 컴파일 후 완성된 HTML 컨텐츠로 만든다.)
> 3. 클라이언트에 전달되는 순간, 이미 렌더링 준비가 되어있기 때문에 HTML은 즉시 렌더링 된다. 
> 그러나 사이트 자체는 조작 불가능하다. (Javascript가 읽히기 전이다.)
> 4. 클라이언트가 자바스크립트를 다운받는다.
> 5. 다운 받아지고 있는 사이에 유저는 컨텐츠는 볼 수 있지만 사이트를 조작 할 수는 없다. 이때의 사용자 조작을 기억하고 있는다.
> 6. 브라우저가 Javascript 프레임워크를 실행한다.
> 7. JS까지 성공적으로 컴파일 되었기 때문에 기억하고 있던 사용자 조작이 실행되고 이제 웹 페이지는 상호작용 가능해진다.

## 더 간단하게(SSR)

클라이언트가 브라우저로 요청을 보냈을 때, 서버는 즉시 실행가능한 HTML 을 클라이언트에게 보내준다.
그 HTML 파일 안에는 내용이 있는 상태라서 javascript 가 다운로드 되기 전에도 클라이언트 쪽에서 HTML 안에 있는 내용을 확인할 수 있음

<aside>
💡 2단계에서 `Viewable`
4단계에서 `Interactable`

</aside>

![Untitled](https://velog.velcdn.com/images/sjc0829/post/e1b5b340-8394-4884-9f69-741db611034c/image.png)

---

## 2. 클라이언트 사이드 랜더링(CSR)

→ **클라이언트 쪽에서 랜더링이 일어나는 것**

클라이언트 사이드 랜더링(CSR)은 웹 사이트가 다른 페이지로 이동할 때 브라우저에서 거의 즉시 업데이트될 수 있도록 해주지만, 시작할 때 더 많은 초기 다운로드와 추가 랜더링이 필요하다.
**첫 방문 시 느리지만, 재차 같은 페이지를 방문할 때 빠른 속도로 로딩된다.**

![Untitled](https://velog.velcdn.com/images/sjc0829/post/ad15f148-01c5-4c66-8e1d-754b3d9a4a76/image.png)

> 
> 
> 1. User가 Website 요청을 보냄.
> 2. CDN이 HTML 파일과 JS로 접근할 수 있는 링크를 클라이언트로 보낸다.
> 
> > * CDN : aws의 cloudflare를 생각하면 됨. 엔드 유저의 요청에 '물리적'으로 가까운 서버에서 요청에 응답하는 방식
> > 
> 1. 클라이언트는 HTML과 JS를 다운로드 받는다.(이때 SSR과 달리 유저는 아무것도 볼 수 없다.😡)
> 2. *생략*
> 3. 다운이 완료된 JS가 실행된다. 데이터를 위한 `API`가 호출된다.(이때 유저들은 `placeholder`를 보게된다. )
> 4. 서버가 API로부터의 요청에 응답한다.
> 5. API로부터 받아온 data를 placeholder 자리에 넣어준다. 이제 페이지는 상호작용이 가능해진다.
> 

## 더 간단하게(CSR)

클라이언트가 서버로 요청을 보냈을 때, 서버는 클라이언트에게 랜더링 준비가 되지 않은 HTML 파일을 보낸다.
즉, HTML 안에 아무런 내용이 없다는 것을 의미한다.
이후 자바스크립트가 다운로드 되어져야 클라이언트는 브라우저의 내용을 확인할 수 있다.
애초에 HTML 의 구성요소를 Javascript 를 통해 생성했기 때문에 Javascript 가 다운로드 되기 전까지는 내용을 확인할 수 없는 것이다. (🤔리액트, 또는 js에서 html tag 를 생성해주는 코드를 떠올려보자)

<aside>
💡 4단계에서 `Viewable`, `Interatable`

</aside>

![Untitled](https://velog.velcdn.com/images/sjc0829/post/db4d7183-adf5-4049-829f-d716b6c14132/image.png)

---

## 3. SSR 과 CSR 장점과 단점

## SSR

- 장점
    - 첫 페이지 로딩 속도가 클라이언트 랜더링에 비해 더 빠르다.(첫 로딩 속도만)
    - 검색엔진최적화 (SEO) 가 가능하다.
- 단점
    - 초기 로딩 이후 페이지 이동 시 속도가 다소 느리다.
        - 페이지 이동 시 마다 클라이언트가 서버에게 필요한 데이터를 요청하다 보니 속도가 느리다.

## CSR

- 장점
    - 빠른 인터랙션을 구현할 수 있다.
        - View 랜더링을 브라우저에게 담당하므로 서버 트래픽을 감소
        - 새로 고침이 발생하지 않아서 사용자가 네이티브 앱과 비슷한 경험을 할 수 있다.
- 단점
    - 첫 페이지 로딩속도가 서버사이드 랜더링에 비해 느리다.(첫 로딩 속도만)
    - 검색엔진최적화 (SEO) 에 대한 추가 보완 작업이 필요하다.
        - 포털사이트 검색엔진 크롤러가 웹 사이트에 대한 데이터를 제대로 수집하지 못하는 경우가 발생할 수 있다. 구글 검색엔진의 경우 자바스크립트 엔진이 내장되어 있어 크롤링이 되지만,
        네이버, 다음 의 경우 검색엔진이 제대로 크롤링하지 못하기 때문에 별도의 보완작업이 필요하다.
    

---

## 4. 각각의 차이점

**1) 가장 큰 차이점은, HTML 파일 안에 내용이 들어 있느냐 없느냐 (SSR / CSR)**

웹 페이지 로딩의 종류는 두 가지고 나눌 수 있다.
가장 첫 페이지 로딩 / 나머지 페이지 로딩

✔️ 첫페이지로딩시간 → SSR 이 더 빠르다.

CSR의 경우 HTML, CSS 와 모든 스크립트를 한 번에 불러온다.
SSR의 경우 필요부분의 HTML 과 스크립트를 불러온다.

✔️나머지로딩시간 → CSR 이 더 빠르다.

CSR 의 경우 첫 페이지 로딩을 할 때 부터 모든 HTML, CSS, 스크립트를 불러오기 때문에
다음 페이지 로딩이 SSR 보다 빠름.
SSR 의 경우 페이지 단위로 서버에서 HTML 과 스크립트를 불러오기 때문에 CSR 보다 느리다.

**2) SEO 대응**

**3) 서버 자원 사용**

SSR은 페이지가 바뀔 때마다 매번 서버에 요청을 해서 HTML,스크립트 받기 때문에 서버 부하가 크다.
반면 CSR 은 한번에 몰아서 받아오기 때문에 서버의 부하가 적다.

---

## 5. 사용 권장 예시

### SSR을 사용하자

- 네트워크가 느릴 때 😓(CSR은 한번에 모든 것을 불러오지만 SSR은 각 페이지마다 나눠불러오기 때문)
- SEO(serach engine optimization : 검색 엔진 최적화)가 필요할 때.
- 최초 로딩이 빨라야하는 사이트를 개발 할 때
- 메인 스크립트가 크고 로딩이 매우 느릴 때
    
    > CSR은 메인스크립트가 로딩이 끝나면 API로 데이터 요청을 보낸다. 하지만 SSR은 한번의 요청에 아예 렌더가 가능한 페이지가 돌아온다.
    > 
- 웹 사이트가 상호작용이 별로 없을 때.

### CSR을 사용하자

- 네트워크가 빠를 때
- 서버의 성능이 좋지 않을 때
- 사용자에게 보여줘야 하는 데이터의 양이 많을 때.(로딩창을 띄울 수 있는 장점이 있다.)
- 메인 스크립트가 가벼울 때
- SEO 따윈 관심 없을 때😤
- 웹 어플리케이션에 사용자와 상호작용할 것들이 많을 때. (아예 렌더링 되지 않아서 사용자의 행동을 막는 것이 경험에 오히려 유리함.)