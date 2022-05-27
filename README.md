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
## 5월 25일
콘솔창 열어서 오류 확인 후 수정
* table 오류수정 <br>
  - Warning: Invalid DOM property `rowspan`. Did you mean `rowSpan`?
  - Warning: Invalid DOM property `colspan`. Did you mean `colSpan`? <br>
rowspan,colspan -> rowSpan,colSpan <br>

테이블데이터 <br>
class방식에서 hook방식으로 변경 <br>
```jsx
const Subsidy = () => {
    const [ postsData, setPosts ] = useState();

useEffect(() => {
  setPosts(postList);
    }, [ ])
```

***

## 5월 18일
보조금페이지 테이블 데이터 json 파일로
```jsx
{
    "data": [
      {
          "type": "승용",
          "jejo": "현대자동차",
          "name": "아이오닉5 2WD 롱레인지 20인치",
          "money": "700"
      },
      {
          "type": "승용",
          "jejo": "현대자동차",
          "name": "아이오닉5 2WD 롱레인지 19인치 빌트인 캠 미적용",
          "money": "700"
      },
      {
          "type": "승용",
          "jejo": "현대자동차",
          "name": "아이오닉5 2WD 롱레인지 19인치",
          "money": "700"
      },
      {
          "type": "승용",
          "jejo": "현대자동차",
          "name": "아이오닉5 AWD 롱레인지 20인치",
          "money": "680"
      },
      {
          "type": "승용",
          "jejo": "현대자동차",
          "name": "아이오닉5 AWD 롱레인지 19인치",
          "money": "696"
      },
      ...
```

map함수 사용해서 table 생성

```jsx
class Subsidy extends Component {
  state = {
    posts: Posts.data,
  };

  componentDidMount() {
    console.log(this.state.posts);
  }

  render() {
    const postsData = this.state.posts;
      return (
        <div>
          <div>
	     <table>
              <thead>
                <tr>
                  <th>구분</th>
                  <th>제조사</th>
                  <th>차종</th>
                  <th>보조금</th>
                </tr>
              </thead>
              <tbody>
                {postsData.map((post, index) => (
                  <tr key={index}>
                    <th scope="row">{post.type}</th>
                    <th>{post.jejo}</th>
                    <th>{post.name}</th>
                    <th>{post.money}</th>
                  </tr>
                ))}
              </tbody>
            </table>
          </div>
        </div>
      );
   }
```

![테이블](https://blogfiles.pstatic.net/MjAyMjA1MjJfMjU0/MDAxNjUzMTk4ODA0OTgx.MyMFcypHn8E8OX_C4bPgFkynh_Vfm23G02UgmSX5m9og.JInBKYWNAEHi5zKi5FFSKJhforFksiwMCqNyIiSvG5sg.JPEG.alsl970/money.JPG)

***

## 5월 11일
- JavaScript 웹 크롤링
- 전기차 구매보조금지원 페이지 크롤링
```jsx
const axios = require("axios");
const cheerio = require("cheerio");

// axios를 활용해 AJAX로 HTML 문서를 가져오는 함수 구현
const getHTML = async () => {
  try {
    return await axios.get("https://www.ev.or.kr/portal/buyersGuide/incenTive");
  } catch (error) {
    console.error(error);
  }
}

getHTML()
  .then((html) => {
    const $ = cheerio.load(html.data);
    const titleList = [];
    const bodyList = $("table:nth-child(2)").children("tbody");

    // bodyList를 순회하며 titleList에 find 내용을 저장
    bodyList.each(function(i, elem) {
      titleList[i] = {
        title: $(this).find("tbody>tr:first-child>td:nth-child(1)").text(),
        maker: $(this).find("tbody>tr:first-child>td:nth-child(2)").text(),
        name: $(this).find("tbody>tr:first-child>td:nth-child(3)").text(),
        money: $(this).find("tbody>tr:first-child>td:nth-child(4)").text()
      };
    });
    return titleList;
  })
  .then(res => console.log(res)); // 저장된 결과를 출력
```

![크롤링](https://blogfiles.pstatic.net/MjAyMjA1MTNfMzQg/MDAxNjUyNDE2MTExMjEz.LCiW-eG7IczA0JxXCO3XVCjf-N47XjtU5-AfPivUNTQg.El1mF2tKI0HB37LaxzV2vLeujDMf4M3SyVLn66EQ514g.JPEG.alsl970/%ED%81%AC%EB%A1%A4%EB%A7%81.JPG)

***
## 5월 04일
- 전기차소개 페이지에 Tab기능넣기
- React hooks로 Tab기능구현
```jsx
const [activeIndex, setActiveIndex] = useState(0);

const tabContArr=[
        {
            tabTitle:(
                <li onClick={()=>tabClickHandler(0)}> 탭1 </li>
            ),
            tabCont:(
                <div>탭1 내용</div>
            )
        },
        {
            tabTitle:(
                <li onClick={()=>tabClickHandler(1)}> 탭2 </li>
            ),
            tabCont:(
                <div>탭2 내용</div>
            )
        }
    ];
    
 const tabClickHandler=(index)=>{
 	setActiveIndex(index)
 }
 
 return (
    <ul className="tabs is-boxed">
	    {tabContArr.map((section, index)=>{
		    return section.tabTitle
	    })}
    </ul>
    
    // activeIndex의 탭콘트만 보여줌!
    <div>
	    { tabContArr[activeIndex].tabCont }
    </div>
);
```
- 전기차 소개페이지 디자인 <br />
![1](https://blogfiles.pstatic.net/MjAyMjA1MDZfMTY5/MDAxNjUxODI3MzExMjY5.vY3-gG-7Lf10F55gVUxGP0cREWixwZ7_sndHW2iD5z0g.mmUJ78lnuumP0aDHcJpja9Sb3UbduZ9Z0FSK_wE0-Xcg.PNG.alsl970/1.png?type=w2)
![2](https://blogfiles.pstatic.net/MjAyMjA1MDZfODcg/MDAxNjUxODI3MzExNTUz.m671B984ZRv0Jwn_CpTdSmM0rSNdf5eBSFpUByRttXMg.NPN4OXHX4JpYegkX6xc7RqA2rKsghntoyr3yCZG16j0g.PNG.alsl970/2.png?type=w2)
![3](https://blogfiles.pstatic.net/MjAyMjA1MDZfNzIg/MDAxNjUxODI3MzExODg4.6hdQx0ySqCObuqivPFPnEA6WiJduo8Ir7quQTRAhbhsg.drKSecd9J0VKPTGyboAey8r5tHhL6fBPvIaKoo_9ZdMg.PNG.alsl970/3.png?type=w2)
***
## 4월 13일

- 백그라운드 영상 넣기
```jsx
  <video autoPlay muted loop width="100%">
    <source src={bgImage} type="video/mp4"/>
  </video>
```
- Navbar 디자인
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

const Menu = styled.div`
  display:flex;
  justify-content: space-between;
  align-items: center;
  position: relative;
` ;

const MenuLink = styled.a`
  margin-right: 10em;
  padding: 0;
  cursor: pointer;
  text-decoration: none;
  color: gray;
`;
```
- 홈화면 틀잡기 <br>

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
