# 깃기의 Next.js 세상



### Next.js의 자동라우팅

- App 폴더 안에 폴더를 만들면 해당 폴더명이 `/폴더명` 의 형태로 라우팅이 됨

- 그 폴더 안에 page.js를 넣으면 그 page(컴포넌트)를 렌더링 함

- 폴더 안에 폴더를 넣는 것으로 중첩라우팅이 가능함

- (참고) Link 태그

  - 새로고침 없이 부드러운 페이지 이동을 지원

  - `<a>`태그 처럼 사용 가능

  - import 필요

  - ``` jsx
    import Link from "next/link";
    
    export default function Home() {
      return (
        <main>
          <div className="navbar">
            <Link href="/">home</Link>
            <Link href="/list">list페이지</Link>
          </div>
          <h1 className="title">Programming Log</h1>
          <p className="title-sub">by dev kim</p>
        </main>
      )
    } 



### layout.js

- page.js를 보여줄 때, 항상 layout.jsx로 감싸서 보여줌
- 같은 레벨의 layout.js로 감싸진 이후, 상위 레벨(폴더)의 layout.js로도 감싸짐
- 따라서 내브바 등의 중복되는 html은 layout.js에 구현



### Image

- 기본적으로 `img` 태그 사용

  - ```jsx
    <img src="/port1.png" alt="설명"/>  
    ```

  - public 폴더에 있는 것들은 사이트 발행시 자동으로 사이트 root 경로로 이동 -> 따로 /public 안써도 됨

- 최적화된 이미지 사용

  - lazy loading , 사이즈 최적화, layout shift 방지가 자동으로 적용되는 이미지 태그

  - ```jsx
    import Image from 'next/image'
    import 이미지 from './food0.png'
    
    export default function Home() {
      return(
        <div>
          <Image src={이미지} alt="설명"/>
        <div/>
    )} 
    ```

  - Image 태그 import + 이미지 파일도 경로에서 import해와야 함 (`/public/~~~`)

  - 외부 이미지를 사용하고 싶으면 제약이 있음

    - Width, height 옵션을 줘야 하고 (fill="true"을 주고 부모 div에서 조절해도 됨)
    - https://beta.nextjs.org/docs/optimizing/images#remote-images 에 나온대로 셋팅을 해줘야 외부 URL 이미지를 사용가능



### Client / Server Component

- page.js, layout.js에서 만드는 컴포넌트는 기본적으로 전부 server component
  - 자바스크립트를 넣지 못함(useState, useEffect, onClick 사용 불가)
  - 대신 로딩 속도가 빠르고 검색 엔진에 이점
- 컴포넌트 생성시 페이지(파일) 맨위에 `'use client'` 작성 해 넣으면, 그 밑의 모든 컴포넌트는 client component
  - 자바스크립트로 인해 페이지 용량과 로딩시간이 늘어나고 hydration 때문에 더 느려짐
- 따라서 보통 페이지 단위로는 server component로 작성하고 그 안에 자바스크립트 기능이 필요한 부분만 client component로 채워 넣는 것이 좋음