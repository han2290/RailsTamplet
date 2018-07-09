# Day 21

- 레일즈 프로젝트에서 ajax를 구현하기 위해서는 다음과 같은 순서를 갖는다.

> 1. ajax 코드를 작성한다. (`$.ajax({})`)
> 2. url 을 지정한다.
> 3. 해당 url을 *config/routes.rb*에서 controller#action을 지정한다.
> 4. controller#action을 자성한다.
> 5. *app/views/controller_name*에 action명과 일치하는 `js.erb` 파일을 작성한다.

- 항상 잘 기억해두고 각 순서에 맞춰 구현하도록한다.

------

#### 오늘 할 일

* 템플릿
* pusher(채팅방, 채팅방에 join)
* 별점 달기(가능하다면)

------

horizontal/index.html

* 캐싱이란?
* 웹팩
* Ajax 돌아가는 방식을 알아야 함



### 템플릿

> Gemfile
>
> ```ruby
> #bootstrap 4
> gem 'bootstrap', '~> 4.1.1'
> 
> #font-awesome-rails
> gem 'font-awesome-rails'
> 
> #gem 'turbolinks', '~> 5' #주석처리
> ```



> home 컨트롤러 생성
>
> root route 설정



> ****
>
> **필요없는 require지우고 필수 요소 추가하기**
>
> application.js
>
> ```js
> //맨 밑의 두 개 지우고 두 개 추가하기
> //bootstrap 3버전은 bootstrap만 추가하고
> //4버전은 popper과 boostrap 두 개 전부 추가한다.
> //= require popper
> //= require bootstrap
> ```
>
> 추가



> **css 파일명 변경 및 다운로드한 gem import**
>
> application.css => application.scss
>
> ```scss
> //전 내용 다 지우고
> @import 'bootstrap';
> @import 'font-awesome';
> ```



> **css 가져오기 위한 명령어 명시**
>
> import할 css 가져오기
>
> main page에서 css 파일 이름을 복사해 scss 파일에서 import 해준다.
>
> : assets/stylesheets/home.scss
>
> ```scss
> @import 'morris';
> @import 'icons';
> @import 'style';
> ```



> **템플릿의 css 파일 인식할 수 있게 옮기기**
>
> import할 css의 파일들을 vendor/assets/javascript에 옮겨준다.



> **필수 meta tag 복사**
>
> layouts/application.html.erb
>
> ```erb
> <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no" />
> 
> <%= stylesheet_link_tag 'application', media: 'all' %>
> <%= stylesheet_link_tag  params[:controller], media: 'all'%>
> <%= javascript_include_tag 'application' %>
> ```
>
>  css를 정상 동작시키기 위해 viewport를 추가한다.
>
> 
>
> 각 페이지 마다 모든 css를 가져오는 것은 자원 낭비다. 따라서 필요한 css만 가져올 수 있도록 파라메터로 컨트롤러를 받아온다. 그렇다면, 컨트롤러에 맞는 css만 가져오게 될 것이다.



> **index 분리하여 가져오기**
>
> index.html을 보면 코드가 너무 길다. 따라서 이것들을 분리하여 랜더링해서 가져올 것이다.



> **js 가져오기**
>
> `<%= javascript_include_tag 'application' %>`를 이용해 js를 가져온다. 'application'이라는 파일에 명시된 js 파일을 자동으로 가져오게 된다.



> **javascript 코드 옮기기**
>
>  만약 javascript 코드가 별도로 작성되어 있다면, 그것을 body 영역의 맨 아래에 복사한다.



> **image 파일 옮기기**
>
> 'assets/images/'에 탬플릿/images/ 내부의 것들을 옮겨준다.
>
> 현재 html의 img는 assets/images로 경로가 잡혀있다. 하지만 rails는 이미지 경로를 어떤 식으로 바꾸므로 ruby tag를 이용하여 형식을 맞추어 줄 필요가 있다.
>
> ```ruby
> <img src = "assets/images/logo.png"....>
>     =>
> <img src = "<%= asset_path 'logo.png' %>....>"
> ```



> font 적용시키기
>
> 



### 기타

#### precompile: scss 에러 찾기

 scss나 css같은 경우는 rails에서 오류를 찾기가 힘들다. 따라서 다음과 같이 precompile을 통해서 에러를 쉽게 찾을 수 있다.

> `$ rake assets:precompile`
>
> 
>
> `public/assets`
>
> ​	여기에 컴파일 결과 있음
>
> 
>
> `$ rake assets:clobber` 
>
> ​	 `public/assets` 의 파일들을 지운다
>
> 
>
> config/initializers/assets.rb
>
> ```ruby
> # Rails.application.config.assets.precompile += %w( search.js ) 를
> 
> Rails.application.config.assets.precompile += %w( home.js 
> home.scss) #로 변경
> ```



#### turbolink와  tree 지우는 이유



#### 캐싱

