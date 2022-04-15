# capstone22

팀명: bit<br>
이름: 김도현(팀원 Web)<br>
졸업작품 소개사이트:<br>
포트폴리오 소개 사이트:<br>


졸업 작품 소개
- 작품명 : EVCAR
- 개발환경 : react
- 작품소개 : 전기차 충전소위치/ 전기차소개
- 작품의 특징

***
[ 개발일지 ]
## 4월 13일

-백그라운드 영상 넣기
```jsx
  <video autoPlay muted loop width="100%">
    <source src={bgImage} type="video/mp4"/>
  </video>
```
-Navbar 디자인
```jsx
const Navbar = () => {
  return (
    <Nav>
      <Logo src={Logoimg} />
      <Menu>
        <MenuLink href="">전기차소개</MenuLink>
        <MenuLink href="">보조금지원</MenuLink>
        <MenuLink href="">충전소찾기</MenuLink>
        <MenuLink href="">전기차추천</MenuLink>
      </Menu>
    </Nav>
  );
};

const Nav = styled.div`
  background-color: white;
  width: 100%;
  height: 80px;
  text-transform:uppercase;
  padding: 0 2rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-wrap: wrap;
  opacity: 50px;
  position: fixed;
  box-shadow: 0px 0px 10px 0px #000 ;
  z-index: 1;
`;

const Logo = styled.img`
  width: 170px;
  height: 40px;
  margin-left: 10em;
`

const MenuLink = styled.a`
  margin-right: 10em;
  padding: 0;
  cursor: pointer;
  text-decoration: none;
  color: gray;
`;

const Menu = styled.div`
  display:flex;
  justify-content: space-between;
  align-items: center;
  position: relative;
` ;
```
![home](https://blogfiles.pstatic.net/MjAyMjA0MTVfMTUg/MDAxNjUwMDMzOTY2Nzg0.aF0Vnj1zttP9xX2lojHmy1FpFrQ5LtohTI8SCnZsg8wg.XIJ5bVRcwNztRqFC1IC4p9sx_EnfctG4-m4964TIYkgg.JPEG.alsl970/dee.JPG)
***
## 4월 06일

- [XD 페이지 디자인] (https://xd.adobe.com/view/a9de9c2c-8ce8-43a6-85c0-9913bf38e068-fc8d/)
- 카카오지도 api
```jsx
const options = {
  center: new window.kakao.maps.LatLng(37.512259196344, 126.72065257372), //지도의 중심좌표.
  level: 3,
};

function App() {
  const container = useRef(null);

  useEffect(() => {
    new window.kakao.maps.Map(container.current, options); 
    return () => {};
  }, []);
```
![evcar](https://user-images.githubusercontent.com/89895926/162460055-5c7be7c1-f69e-4ff2-bcf8-7c9edf6cb1d6.png)

***
## 3월 30일

- css 공부
- styled-components 공부
- react hook 공부

```jsx
import React, { useState, useEffect } from "react";
import styled, { createGlobalStyle } from "styled-components";
import axios from "axios";

function Home() {
  const [posts, setPosts] = useState([]);
  useEffect(() => {
    axios
      .get("https://jsonplaceholder.typicode.com/posts")
      .then(({ data }) => setPosts(data));
  });
  return (
    <Container>
      <GlobalStyle />
      {posts.map((post, index) => (
        <Post key={index}>
          <Title>{post.title}</Title>
          <Body>{post.body}</Body>
        </Post>
      ))}
    </Container>
  );
}
const GlobalStyle = createGlobalStyle`
body {
  margin: 0;
}
`;
const Container = styled.div`
  min-height: 100vh;
  padding: 200px 0;
  display: grid;
  grid-template-columns: repeat(4, 300px);
  grid-template-rows: repeat(auto-fit, 300px);
  grid-auto-rows: 300px;
  grid-gap: 30px 20px;
  justify-content: center;
  background: #55efc4;
  box-sizing: border-box;
`;

const Post = styled.div`
  border: 1px solid black;
  border-radius: 20px;
  background: white;
  box-shadow: 10px 5px 5px #7f8fa6;
`;

const Title = styled.div`
  height: 20%;
  display: flex;
  justify-content: center;
  align-items: center;
  border-bottom: 1px solid black;
  font-weight: 600;
`;

const Body = styled.div`
  height: 80%;
  padding: 11px;
  border-radius: 20px;
`;

export default Home;
```
***
## 3월 23일

- 아이디어 정리 
- 작품 기술서 작성
- 참고 사이트 찾기
- 전기차충전소 오픈api 찾기
- 지도api 가져와보기



매주 금요일까지
