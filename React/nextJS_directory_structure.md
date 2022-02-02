# NextJS 파일 구조

## 1. Public
어플리케이션에 사용되는 정적 폴더, 브라우저에 직접 엑세스함.  
image, video, icon 등등 매체가 포함되며 모든 사람이 페이지에 접근 할 수 있다.

## 2. Pages
nextjs에서는 routing 시스템이 react-route와 다르게 파일시스템으로 이루어져있다.  
페이지를 담당하는 컴포넌트로 url을 결정하며 사용자에게 직접적인 뷰를 띄워준다.  
### _app.tsx
각 페이지별로 공통적으로 쓰는 부분에 대해 리펙토링을 해주는 역할을한다.
```typescript
import '../styles/globals.css'
import type { AppProps } from 'next/app'

function MyApp({ Component, pageProps }: AppProps) {
  return <Component {...pageProps} />
}

export default MyApp
```
- create next-app을 했을때 만들어지는 기본형 _app.tsx이다.  
이곳에서 렌더링하는 값은 모든 페이지에 영향을 준다. (최초 실행 위치 = _app.tsx)  

- props로 컴포넌트와 pageProps를 받는데, 컴포넌트는 사용자가 요청한 페이지가 된다.  
즉, 구성한 컴포넌트가 리턴되어 들어오는곳.  
ex) GET /main 요청을 보낼경우, Component 에는 /pages/main.tsx(jsx) 파일이 내려오게된다.  

- pageProps는 페이지 getInitialProps를 통해 내려받은 props들을 말한다.

- 실행 순서: _app.tsx 랜더링 -> 요청 컴포넌트 리턴 -> _document.tsx 실행  

페이지를 업데이트 하기 전에 원하는 방식으로 페이지를 업데이트 하는 터미널이된다.

