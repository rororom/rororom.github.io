---
title: 구글 검색엔진에 내 블로그 등록하기
author: 개롱이
date: 2023-04-09 12:30:00 +0900
categories: [Github, Blog]
tags: [github blog]
pin: true
---

## 구글엔진 등록 전 필요파일

> 모든 필요 파일들은 블로그가 생성되면 깃허브 측에서 자동으로 만들어주기 때문에, 따로 생성하지 않아도 됩니다.

### 1. sitemap.xml

sitemap.xml은 책의 목차처럼 웹사이트 내의 모든 페이지 목록을 나열한 파일이다.

웹 크롤링 과정에서 발견되지 않는 페이지를 보다 찾기 쉽게 만들어준다.

github.io/_site 경로에서 sitemap.xml 파일을 찾아보자.

> 필요하신 분들은 [sitepam.xml 형식에 대한 문서](http://superkts.pe.kr/upload/helper/file1/siteMapXML.htm)를 참고해도 좋을 것 같습니다!
{: .prompt-tip }
<br/>

### 2. robots.txt

필수 사항은 아니지만, 블로그에 웹 크롤러 등 **<u>로봇의 접근을 막기 위한</u>** 파일이다.

검색엔진에 웹 사이트 내부의 특정 정보가 노출되는 것을 원치 않을 때 robots.txt를 이용하면 된다.

```
User-agent: 제어할 로봇의 User-Agent
Allow: /특정 디렉토리 접근 허가/
Disallow:/특정 디렉토리 접근 차단/
```
<br/>

### 3. feed.xml

마찬가지로 필수 사항은 아니지만 **<u>RSS feed 등록</u>**을 하고 싶다면 feed.xml이 필요하다.

RSS는 *Rich Site Summery* 혹은 *Real Simple Syndication*라고 불린다. 포스트의 제목 또는 전체 내용만 따로 뽑아 하나의 파일로 저장해둔 것이다.

사용자들은 각 사이트에서 제공하는 RSS feed 주소만 모아 보고 싶은 컨텐츠를 쉽게 골라 볼 수 있다.

정적 사이트에서는 잘 사용하지 않고, 보통 새로운 컨텐츠가 주기적으로 올라오는 뉴스 사이트나 블로그 사이트에서 많이 사용된다.
<br/>
<br/>

## 구글 검색 엔진 등록하기

### [구글 서치 콘솔](https://search.google.com/search-console?resource_id=https%3A%2F%2Frororom.github.io%2F&hl=ko)

**시작하기** 버튼을 눌러 작업을 시작해보자.
<br/>
<br/>

![1_choose](/3FbcwL1/ongoogle-1.png)

**URL 접두어** 탭에 본인의 블로그 주소를 입력 - *계속*
<br/>
<br/>

![2_check](/rmhKk46/ongoogle-2.png)

소유권 확인을 위해 해당 HTML 파일을 다운받아 루트 디렉토리에 저장 후 깃허브에 PUSH 해준다.

그 다음 확인 버튼을 누르면 구글에서 인증을 시도하고, 소유권이 확인된다.
<br/>
<br/>

![3_sitemaps](/NTYkQyX/ongoogle-3.png){:.w-75 .normal}

왼쪽 위의 메뉴 탭을 열어 **Sitemaps**로 진입한다.
<br/>
<br/>

![4_insert sitemap.xml](/rwKZB1C/ongoogle-4.png){:.w-75 .normal}

나의 블로그 주소 뒤에 **sitemap.xml** 입력 후 제출 버튼을 눌러준다.
<br/>
<br/>

![5_sitemap list](/D1G4bQZ/ongoogle-5.png)

제출이 완료되면 제출된 사이트맵 목록에 상태와 함께 표시된다.

블로그에 포스트가 하나도 없으면 비정상적 상태를 띄는 것 같다.

데이터를 처리하는 데에 며칠 정도 시간이 걸리기 때문에, 바로 구글 검색창에 노출이 되진 않는다. 블로그의 색인이 성공적으로 생성되었는지 확인하고 싶다면 구글에 `site: example.com` 를 검색해보자.

![add_1_site on google](/MCzN0dG/add-ongoogle-1.png)

블로그가 검색 엔진에 등록이 완료되었다. 내 경우 등록되기까지 sitemap을 제출하고 3일 정도 걸렸다.

만약 블로그가 표시되지 않는다면 아래와 같은 이유일 수 있다.

![6_if there are error](/bWD5qDt/ongoogle-6.png)


[Google 검색결과에 내 웹사이트를 표시하는 방법](https://developers.google.com/search/docs/fundamentals/get-on-google?hl=ko)

구글에서 제공하는 해당 문서에서 웹사이트 등록에 관한 정보를 얻을 수 있다.

이상으로 구글 검색 엔진에 블로그 등록까지 마쳤으니, 이제 내 블로그를 잘 관리할 일만 남았다.

언젠가 댓글과 조회수 기능도 추가하고 싶다.
