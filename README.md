# ⛄ 202230133 정지호

## 9월 25일 강의

### Next.js 기초와 내장 컴포넌트

- Next는 서버사이드 렌더링 외에도 많은 내장 컴포넌트와 함수를 제공.
- React의 React Router, Reach Router 등은 **클라이언트 라우팅**만 구현 가능.
- Next는 파일시스템 기반 페이지와 라우팅을 함.
- 페이지는 /pages 디렉토리 안의 _.js, _.jsx, *ts, *tsx 파일에서 export한 react 컴포넌트

#### 만일 블로그와 같이 컨텐츠를 분리해야 한다면 어떻게 해야할까?

**=> /pages 아래 디렉토리를 만들고 라우팅 규칙을 만들면 됨.**<br/>
**=> /pages 디렉토리 내부에는 계층적 구조로 라우팅 규칙을 만들 수 있음.**<br/>
**=> /pages/ports 안에 index.jsdhk [slug].js를 만들어 jsx를 반환.**<br/>

- /pages/ports/디렉토리 내에 Index.js만 간단히 만들면 O

### 페이지에서 경로 매개변수 사용하기

- 경로 매개변수를 사용해 동적 페이지 쉽게 만들기 가능.
- page/greet/[name].js 파일을 만들어 보겠습니다.
- 내장 getServerSideProps 함수를 통해 URL에서 동적으로 [name] 변수 값을 가져오는 것.
- greet/Mitch 주소로 가면 'HELLO MITCH'라는 문구가 렌더링 됩니다.

#### pages 밖에서는 getServerSideprops나 getStaticProps 함수를 사용치 못하는데, 어떻게 경로 매개변수를 컴포넌트 안에서 사용할 수 있을까요?

**=> useRouter Hook을 이용하면 컴포넌트 안에서 경로 매개변수를 사용할 수 있음**<br/>
**=> useRouter은 next/router에서 가져올 수 있음**<br/>
**=> useRouter Hook을 사용해 query 매개변수를 가져옴**<br/>
**=> 콘솔에 로그를 출력하면 매개 변수와 쿼리 문자열들을 어떻게 전달하는 지 알 수 있음**<br/>

## 9월 11일 강의

- 개발 시 타입스크립트를 주 언어로 사용하고 싶다면 타입스크립트 전용 플러그인 설치 후 설정 변경.

- 웹팩은 특정 라이브러리, 페이지, 기능에 대해 컴파일된 코드를 **전부 포함하는 번들**을 만들어줌.
- SASS, LESS 같은 CSS 전처리기를 사용해 개발하고 싶다면, **웹팩 설정을 수정**해주면 됨.

#### BUT...

설정을 바꿀 일은 많지 않으며, 꼭 수정해야 한다해도 대부분 next.config.js 파일의 기본값을 변경하는 것으로 충분.

### Transpile

- Babel은 ECMAScript와 같은 자바스크립트 최신 버전이나, TypeScript 이전 버전의 코드로 변환시켜 주는 Transplie 도구임.
- 개발자가 작성한 코드 -> Parse -> Transform -> Generate -> 이전버전의 코드
- Babel의 **parser**는 JS를 컴퓨터가 이해할 수 있는 코드 구조인 Abstract Syntax Tree(AST)로 변환하는 역할.
- Babel의 **traverse** 모듈은 전체 트리 상태를 유지하며 노드 교체, 제거, 추가 담당.
- **generator**가 수정된 AST를 일반 코드로 변환해줌.
- **SWC**도 Babel과 같은 JS 트랜스 컴파일러임.
- Next 12 이후 부터 Babel에 SWC교체 되었음.
- SWC는 Rust로 작성되어 있어 Babel에 비해 속도가 훨씬 빠름.

### SWC 적용 방법

- 새로운 프로젝트에 적용하는 것은 다음 명령으로 프로젝트를 생성하면 바로 사용할 수 있음 <br>
  `$npx create-next-app@latest` or `$npx create-next-app@12`
- Next 12 이전 버전의 프로젝트에 적용하려면 다음과 같이 업그레이드 필요 <br>
  `$npm install next@12` <br>
  Babel을 설정했다면 설정 파일(babelrc 또는 babel.config.js)를 삭제해 줌.

### 렌더링 전략

- 렌더링 전략: 웹 페이지 or 웹 애플리케이션을 웹 브라우저에 제공하는 방법
- 정적인 페이지 제작에는 **Gatsby** 를 추천함.
- 서버 사이드 렌더링 전략을 원한다면 다른 프레임워크를 검토
  <br><br>
- Nest.js는 이 모든 방법을 새로운 수준으로 제공
- 빌드 시점에 정적으로, 동적으로 실행할 지 쉽게 정할 수 있음.
- 요청이 있을 때마다 페이지 다시 생성 가능
- 반드시 클라이언트에서 렌더링해야 할 컴포넌트 지정 가능.

### 서버 사이드 렌더링 (SSR)

- 웹 페이지를 제공하는 가장 흔한 방법.
- APM을 이용하는 일반적 웹 페이지 생성
- JS 코드가 적재되면 동적으로 렌더링.
  <br><br>
- Next.js도 이와 같이 동적페이지 렌더링 가능
- 여기에 스크립트 코드를 집어 넣어 나중에 웹 페이지를 동적으로 처리할 수도 있는데 이를 **하이드레이션**이라함.
  <br><br>
  즉, 어떤 사람이 작성한 블로그 글을 한 페이지에 모아 작성해야 한다면 SSR을 이용하는 것이 적당.
- 서버 사이드 렌더링 -> 자바스크립트가 하이드레이션된 페이지를 전송 -> 클라이언트에서 DOM위에 각 스크립트 코드를 하이드레이션: 페이지 새로고침없이 사용자와 웹 페이지 간 상호작용을 가능케함.
- 리액트 하이드레이션 덕에 웹 앱은 싱글 페이지 애플리케이션(SPA)처럼 작동가능.
- CSR과 SSR 장점 모두 갖음.

#### SSR의 장점

- 더 안전한 웹 애플리케이션: 쿠키 관리, 주요 API, 데이터 검증 등과 같은 작업을 서버에서 처리하기에 중요한 데이터를 노출할 필요X
- 더 뛰어난 웹 사이트 호환성: 클라이언트 환경이 자바스크립트를 사용하지 못하거나 오래된 브라우저를 사용하더라도 서비스 제공.
- 더 뛰어난 SEO: 서버가 렌더링한 HTML을 받기에 봇이나 웹 크롤러가 페이지를 렌더링할 필요가 없음.

#### SSR이 최적의 렌더링 전략이 아닌 경우

- 클라이언트가 페이지를 요청할 때마다 페이지를 다시 렌더링할 수 있는 서버 필요.
- 다른 방식에 비해 SSR이 더 많은 자원을 소모하고, 더 많은 부하를 보이며 유지 보수 비용도 증가함.
- 페이지에 대한 요청을 처리하는 시간 증가.
- 페이지가 외부 API 또는 데이터 소스에 접근해야 한다면, 해당 페이지를 렌더링할 때마다 이들 다시 요청해야 함.
- 페이지 간의 이동은 CSR에 비해 느림.
- 중요한 것은 Next.js가 기본적으로 빌드 시점에 정적으로 페이지를 만든다는 것.
  <BR><BR>
  페이지에서 외부 API를 호출하거나 데이터베이스에 접근하는 등 동적 작업을 해야 한다면 해당하는 함수를 페이지에 export해야 합니다.

## 9월 4일 강의

### 프로젝트 생성 방법

- 프로젝트 생성<br>
  ` $ npx create-next-app@latest`
- 안되면 해당 코드 작성 후 재실행 <br>
  `$ npm i -g create-react-app`
- pages를 사용하고 싶다면, App Router를 NO로 설정
- 프로젝트가 생성되면 프로젝트 디렉토리로 이동하여 `npm run dev` 명령어 실행
- 리액트처럼 바로 실행되지 않기에 `http://localhost:3000`으로 접속 (`ctrl+해당 localhost` 클릭)

### Chocolatey 설치

1. chocolatey 페이지에서 chocolatey 설치
2. powershell에 복붙 `https://chocolatey.org/install#individual`
3. powershell에서 GIT도 다운 `https://community.chocolatey.org/packages?q=git`

#### + PLUS

- pages/ 의 index.js 파일을 복사해서, about.js로 이름ㅇ르 바꾸면, `http://localhost:3000/about` 으로 접속 가능

- `ctrl+해당 localhost` 클릭 하면 바로 들어갈 수 있음.
- `ctrl+c` 누르면 워킹디렉토리에서 빠져나올 수 있음.

- 바벨이나 웹팩의 설정도 커스터마이징 가능
- 바벨 : 자바스크립트 트랜스컴파일, 최신 자바스크립트 코드를 하위 호환성을 보장하는 스크립트 코드로 변환하는 일을 담당.
- 하위 호환성이 보장되면 어떤 js코드도 실행할 수 있음.
- 바벨 사용 시 브라우저나 Node.js 등에서 지원하지 않는 기능을 사용가능.

## 8월 28일 강의

### npm vs yarn

- yarn 설치: `$ npm i -g yarn`
- yarn 확인: `$ yarn -v`
- yarn 삭제: `$ npm uni -g yarn`

### Pages Router vs App Router

- React로 개발하다 처음 Next를 사용하면 제일 먼저 놀라는 기능.
- Next.js **13.4**에서부터 **App Router**가 **stable**하게 지원하기 시작.

### [ Pages Router ]

- **pages 디렉토리**가 **root**이고, **index.js**가 **index page**가 됨.
- about.js는 /about, team.js는 /team 경로로 라우팅
- **클라이언트 중심**의 라우팅입니다.

### [ App Router ] => 강의 진행

- **app 디렉토리**가 **root**이고, **page.js**가 **index page**가 됨.
- /about/page.js는 /about, /login/page.js는 /page 경로로 라우팅.
- **서버 중심**의 라우팅입니다.
- 번들 사이즈가 작음.

### Next.js 13 vs 14

- Pages Router -> App Router
- Date Fetching: 13까지는 getServerSideProps, getStaticProps 메소드를 이용해 구현했으나,
  14에서는 SSG(정적 사이트 생성), SSR(서버 측 렌더링) 및 ISR(증분적 정적 재생성)에서 **하나의 API**만을 사용해 구현할 수 있게됨.
- **이미지 최적화**: 13까지는 **도구**를 사용했으나, 14부터는 **자체적**으로 지원하기 시작
- **보안 강화**: XSS 공격에 대한 보호 기능이 강화되고, 보안 관련 헤더 설정을 더욱 쉽게 만듦.

### Ch01. Next.js 알아보기

- Next.js는 리액트를 위해 만든 오픈소스 **자바스크립트 웹 프레임워트**
- 리액트에는 없는 **다양한 기능 제공**
  - 서버 사이드 렌더링(SSR: Server Side Rendering)
  - 정적 사이트 생성(SSG: Static Site Generation)
  - 증분 정적 재생성(ISR: Incremental Static Regeneration)

```html
SSG(정적 페이지 생성) 미리 만들어 놓은 페이지를 서비스 하기에 속도는 빠르나, 한
번 생성 후엔 수정이 불가능. 이러한 단점을 보완하고자 나온 것이 ISR(증분 정적
재생성). 이미 생성된 페이지를 일정 시간이 지난 후에 다시 생성.(최신 데이터로
업데이트)
```

#### [CH01의 주요 내용]

- Next.js.소개 / 다른 프레임워크와의 비교 / 리액트와의 차이점
- 기본 구조 타입 스크립트를 사용하는 방법
- 바벨과 웹팩 설정 커스터 마이징 ( Next.js 14는 Webpack에서 Tubopack으로 바뀜)

### 1.1 준비하기

- Node.js와 npm을 설치하거나, codesandbox.io 혹은 repl.it 등의 사이트를 이용.
  <br>
  **잠시 확인을 위한 것이면 사이트 이용도 괜찮으나, 그렇지 않다면 local에 환경설정하는 것이 BEST**

### 1.2 Next.js란?

Angular, React, Vue와 같은 프레임워크가 등장하며 웹 개발 분야는 급속도로 변화함.

- 리액트는 메타(페이스북)의 조던 발케가 만들어, 2013년 오픈소스를 발표.

#### [ Next.js가 제공하는 새로운 기능들 ]

- **코드 분할(Splitting):** 페이지를 로딩 할 때 번들을 여러 조각으로 나누어 필요한 부분만 전송.
  <br><br>
- 파일 기반 라우팅 (React에서는 React-Router-Dom사용)
  <br><br>
- 경로 기반 **프리페칭(Prefetching):** 사용자가 다음에 이동할 수 있는 페이지를 미리 가져오는 기술.
  <br><br>
- **서버 사이드 렌더링(SSR):** 페이지 요청이 올때 마다 사전 렌더링. (페이지 요청 시 Fetching 요소 적용하여 렌더링)
  <br><br>
- **정적 사이트 생성(SSG):** 빌드하는 동안 페이지를 사전 생성. (Fetching 요소 적용하려면 재 빌드 해야함.)
  <br><br>
- **증분 정적 콘텐츠 생성(ISR)** 배포 후에도 재 배포 없이 계속 없데이트 (일정 시간마다 SSG를 재렌더링)
  <br><br>
- 타입스크립트 기본 지원
  <br><br>
- **자동 폴리필(Polyfill)적용:** 이전 브라우저에서 최신 기능을 제공하는 데 필요한 코드를 제공.
  <br><br>
- **이미지 최적화:** Next/image 컴포넌트로 제공하는 이미지 최적화 기술 ( laxy loading-지연, 이미지 사이즈 최적화-webp 변환, placeholder-영역 확보)
  <br><br>
- 웹 애플리케이션의 국제화 지원: **다국어 지원** (local에 맞는 URL로 라우팅)
  <br><br>
- Next.js는 현재 넷플릭스, 트위치, 틱톡, 나이키, 우버, 엘라스틱 등 사이트에서 사용 중임.

### 1.3 Next.js와 비슷한 프레임워크

#### [ Gatsby ]

- 정적 웹 사이트를 만들 수 있는 프레임워크
- 정적 사이트 생성만 지원
- 클라이언트 사이드 렌더링만 지원
- 동적으로 변하는 복잡한 웹 사이트 제작 불가

#### [ Razzle ]

- 서버 사이드 랜더링이 가능한 자바스크립트 애플리케이션 개발 가능
- CRA와 유사하게 프로젝트를 구성할 수 있다는 장점 (create-razzle-app)
- React, Preact, Reason-React, Angular 및 Vue와 함께 사용O

#### [ Nuxt.js ]

- Vue를 사용한 웹 애플리케이션 개발에서 리액트의 Next.js에 해당하는 프레임워크
- Nuxt.js나 Next.js 모두 같은 목표를 갖는 프레임워크지만 Nuxt.js는 더 많은 설정 필요
- 만약 Vue 개발자가 서버 사이드 렌더링이 필요하다면 Nuxt.js도 추천함.

#### [ Angular Universal]

- 정적 사이트 생성과 서버 사이드 렌더링 지원
- Nuxt나 Next와는 달리 대기업 Google에서 만듦.
- Angular로 개발하는 경우 Angular Universal을 사용하는 것이 대부분.
