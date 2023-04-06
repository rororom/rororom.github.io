---
title: 첫 깃허브 블로그 만들기
author: 개롱이
date: 2023-04-6 16-13-00 +0900
categories: [Github, Blog]
tags: [github blog]
pin: true
---

> 들어가기 앞서, 사용 기기는 **m1 macbook** 입니다. 운영 체제에 따라 Terminal 언어 등에 차이가 있을 수 있어요!

# Generate

## 1. 깃허브에 새로운 Repository 생성

[GitHub: Let’s build from here](https://github.com/)

![1_make new repository](/CzNzhYH/github-beginning-1.png)

repository name은 `username.github.io` 형식으로 적어준다.

**public, add a README file** 체크해주고 생성
<br/>
<br/>

## 2. 로컬 저장소에 Repository clone

![2_repository clone](/TgYNbLx/github-beginning-2.png)

https 링크를 복사하고 terminal 오픈
<br/>
<br/>

```shell
mkdir git_blog
cd git_blog
git clone 복사한 url
```
git_blog 폴더를 새로 만들어준 다음 폴더 안에 git clone을 해주었다.
- *mkdir : 폴더 생성*
- *cd : 폴더 이동*
<br/>
<br/>

![3_check folder](/ZNhK3Rd/github-beginning-3.png){:.w-75 .normal}

ls 명령어를 통해 생성된 폴더를 확인할 수 있다.
<br/>
<br/>

## 3. Clone 폴더에 index.html 생성

```shell
cd username.github.io
echo "Hello World" > index.html
```
- *echo : 파일 생성*
<br/>
<br/>

## 4. 파일을 원격 저장소로 Push

```shell
git add .
git commit -m "커밋 메세지"
git push -u origin main
```
<br/>

## 5. 생성된 홈페이지 확인

브라우저 주소창에 username.github.io 입력

![4_check index](/vzBvwnN/github-beginning-4.png)

웹페이지가 만들어졌다.
<br/>
<br/>

# Jekyll

## 1. Jekyll install

```shell
gem install bundler
gem install jekyll
```
terminal에 위 명령 실행
<br/>

<details>
<summary><b>❗️error : Gem::FilePermissionError</b></summary>
<div markdown="1">
![5_error message](/Np7hFsH/github-beginning-5.png)

>_ERROR: While executing gem ... (Gem::FilePermissionError) You don't have write permissions for the /Library/Ruby/Gems/2.6.0 directory._

### **- 발생 이유**
- 시스템 ruby를 이용하고 있기 때문에 **권한이 없어** gem 설치가 되지 않는 것
- sudo를 통해 root 권한으로 실행하면 설치 가능하지만 <u>보안상의 이유로 권장하지 않는다.</u>

### **- rbenv를 통한 문제 해결**

```shell
brew update
brew installl rbenv ruby-build
```
brew를 통해 **rbenv** 설치
<br/>
<br/>

```shell
rbenv versions
```
![6_rbenv check](/qMFnPjR/github-beginning-6.png){:.w-75 .normal}

rbenv 설치가 되었는지 위 명령어를 통해 확인해보면 현재 **system ruby**를 쓰고 있다는 걸 알 수 있다.
<br/>
<br/>

```shell
rbenv install -l
```
![Untitled](/ryxdNxp/github-beginning-7.png){:.w-75 .normal}

`rbenv install -l` 명령어로 설치할 수 있는 ruby 버전 확인

<u>rbenv로 관리되는 ruby</u>를 설치해야 한다.

현재 기준 가장 최신 버전인 3.2.1 ver 선택
<br/>
<br/>

```shell
rbenv install 3.2.1
```
- rbenv 3.2.1 ver 설치 명령
<br/>

<details>
<summary><b>❗️error : BUILD FAILED (macOS 13.0.1 using ruby-build 20230309)</b></summary>
<div markdown="1">
### **rbenv 설치 명령어를 입력하자 해당 에러가 발생했다.**
-   구글링을 해보니 'brew install readline openssl' 명령 후 install 진행하여 해당 오류를 해결한 경우가 있지만, 나는 계속 같은 오류가 떴다.
-   스택오버플로우에서 같은 오류에 대한 글을 발견했고, 조언에 따라 `CFLAGS="-Wno-error=implicit-function-declaration" RUBY_CONFIGURE_OPTS='--with-readline-dir=/usr/local/opt/readline/' arch -x86_64 rbenv install 3.1.2` 명령을 입력하였다. 결과는 또 다시 오류…
-   여기서 로그를 다시 읽어보았다.
<br/>
<br/>

```
Last 10 log lines:
Check ext/psych/mkmf.log for more details.
*** Fix the problems, then remove these directories and try again if you want.
Generating RDoc documentation
/private/var/folders/0w/r8w9x4sn1n36v2bqbbwwg71w0000gn/T/ruby-build.20230329101927.39565.eCr3PI/ruby-3.2.1/lib/yaml.rb:3: warning: It seems your ruby installation is missing psych (for YAML output).
To eliminate this warning, please install libyaml and reinstall your ruby.
uh-oh! RDoc had a problem:
cannot load such file -- psych
```

`To eliminate this warning, please install libyaml and reinstall your ruby.` 이 경고를 없애려면 **libyaml를 설치**하고 **ruby를 재설치**하라는 문구가 있었다.
<br/>

## 진짜 해결
>
-   `brew install libyaml`
-   `brew upgrade ruby-build`
-   `rbenv install 3.2.1`

libyaml 설치하고 ruby를 업데이트 해주니 rbenv가 정상적으로 설치되었다.

</div>
</details>
<br/>

```shell
rbenv versions
```
![8_rbenv version check](/1MZmQ3Z/github-beginning-8.png){:.w-75 .normal}

다시 버전을 확인해보면, 여전히 system으로 되어 있지만 신규 추가된 3.2.1 버전도 함께 보인다.
<br/>
<br/>

```shell
rbenv global 3.2.1
```
- rbenv 글로벌 버전을 3.2.1로 변경
<br/>
<br/>

![9_rbenv version change](/82Kwwzm/github-beginning-9.png){:.w-75 .normal}

다시 버전을 확인해보면 3.2.1이 선택되어있다.

마지막으로 **rbenv PATH를 추가**하기 위해 쉘 설정 파일을 열어 아래 코드를 추가한다.

나는 zsh 사용하므로 zshrc 에 추가해줬다.

```shell
vim ~/.zshrc
```

```shell
[[ -d ~/.rbenv  ]] && \\
export PATH=${HOME}/.rbenv/bin:${PATH} && \\
eval "$(rbenv init -)"
```

코드를 추가했다면 `source` 로 코드를 적용해준다.

```shell
source ~/.zchrc
```

이후 다시 `gem install` 실행하면 정상작동 된다.
</div>
</details>
<br/>

## 2. 기존에 만들었던 index.html 삭제

```shell
rm -f index.html
```
<br/>

## 3. 다운받은 jekyll 이용하여 홈페이지의 기본 틀 생성

```shell
jekyll new ./
```

<u>github 원격 저장소에 연결된 root directory</u>로 이동한 다음 위 명령어를 실행해준다.

처음에 생성했던 git_blog/username.gihub.io 폴더에 실행해주면 된다.
<br/>
<br/>

## 4. 번들 설치

```shell
bundle install
```
<br/>

## 5. jekyll 로컬 서버에 띄우기

```shell
bundle exec jekyll serve
```

![10_jekyll serve](/PWfdKNw/github-beginning-10.png)

[<http://127.0.0.1:4000/>](<http://127.0.0.1:4000/>) 을 브라우저에 입력해보면 서버가 작동하는 것을 볼 수 있다.

![11_blog on jekyll](/4W0jqWh/github-beginning-11.png)
<br/>
<br/>

## 6. Push

```shell
git add .
git commit -m "커밋 메세지"
git push -u origin main
```
변경된 내용을 github 원격 저장소에 저장해준다.
<br/>
<br/>


# jekyll theme 적용

## 1. 테마 다운로드

구글에 *jekyll themes*를 검색하면 여러 템플릿이 뜬다.

나에게는 공부 기록 겸 일지처럼 사용할 웹페이지가 필요해서 미디어 중심보다 글 중심의 디자인을 찾아봤다.

그 중에서도 카테고리 별로 글을 정리할 수 있고, 태그 별 모아보기 기능이 있는 [**Chirpy**](https://github.com/cotes2020/jekyll-theme-chirpy.git) 템플릿을 선택
<br/>

![12_download chirpy zip](/T8yhHMp/github-beginning-12.png)

Download ZIP을 눌러 다운받은 zip 파일의 압축을 풀고, 모든 파일을 복사한 후 **username.github.io** 폴더에 붙여넣는다.

겹치는 파일은 전부 replace 해준다.
<br/>
<br/>

```shell
bundle install
bundle exec jekyll serve
```

명령어를 재차 실행해 서버를 띄워주고 서버 주소로 접속하면 템플릿이 적용된 나의 웹사이트가 나타난다.
<br/>
<br/>

![13_apply chirpy](/Gn58RHm/github-beginning-13.png)

귀엽죠?
<br/>
<br/>

## 2. 블로그 설정

github에 push하기 전 웹페이지의 정보를 수정해주자.

먼저 **username.github.io** 폴더 안에 있는 **_config.yml** 파일을 열어준다.
<br/>
<br/>

![14_open config](/1d6YF5L/github-beginning-14.png)

웹페이지에 대한 설정이 나온다.

timezone도 서울로 바꿔주고, 타이틀과 사진 등을 내 정보대로 수정했다.
<br/>
<br/>

![15_update profile](/PQTVhH4/github-beginning-15.png)

![16_cdn](/QnYmzRT/github-beginning-16.png)

=> Chirpy 템플릿은 폴더 내의 이미지를 사용하는 것이 아니라 CDN을 통해 외부 서버에서 이미지를 가져오는 방식을 사용했다. 무료 이미지 호스팅 사이트인 [https://imgbb.com/](https://imgbb.com/) 에 사용할 이미지를 올려놓고, 다이렉트 링크를 복사해 붙여넣어줬다.
<br/>
<br/>

## 3. 포스팅

포스팅은 _posts 폴더에 markdown 형식으로 작성하면 된다.

markdown은 처음이라 조금 어색했지만 Chirpy 템플릿 제작자분이 사용법을 하나하나 적어주셔서 금방 적응할 수 있었다.
<br/>
<br/>

![17_check posting](/nj0cy6F/github-beginning-17.png)

포스팅이 잘 되는 걸 확인했으니 다시 git에 push
<br/>
<br/>

```shell
git add .
git commit -m "apply jekyll"
git push
```
<br/>

## 4. 웹 호스팅

[GitHub Pages 설명서 - GitHub Docs](https://docs.github.com/ko/pages)

깃허브를 통해 웹 사이트를 호스팅 하는 방법은 공식 사이트를 읽고 따랐다.

먼저 생성한 repository의 setting으로 들어가 **pages** 탭을 클릭해준다.
<br/>
<br/>

![18_find pages](/wWV6vW0/github-beginning-18.png){: .normal}

pages는 사이드바 code and automation 구역의 맨 아래 있다.
<br/>
<br/>

![19_change branch](/1vMfyDZ/github-beginning-19.png)

Branch를 **main**으로 선택해주고 (브랜치 이름이 다를 수 있어요) Save
<br/>
<br/>

![20_custom domain](/NVKswzm/github-beginning-20.png)

이쪽에서 커스텀 도메인을 만들 수도 있는 모양이다.
<br/>

>❗  root 선택 시 jekyll 템플릿을 찾지 못하고, docs 선택 시 docs directory를 못 찾는 에러가 발생했다. Source를 **Github Actions**로 바꿔준 후 적용하니 웹페이지가 정상적으로 호스팅됐다.
{: .prompt-danger }

<br/>
<br/>

![21_hosted page](/LgRgX60/github-beginning-21.png)

브라우저 주소창에 username.github.io 를 입력하면 정상적으로 웹페이지에 접속된다.

이렇게 인생 첫 깃허브 블로그를 만들어 봤다.

나도 이제 깃허브 블로그 있는 개롱이다.
