##  RAILS
### 1. 기본 설치
* C9에서 사용하기 위해 cd ..로 최상위로 이동한다.
    * 설치
        - gem install rails -v 5.0.6 : rails 5.0.6버젼 설치
        - rvm install 2.4.1 : version manager를 이용해 ruby 2.4.1설치
        - rvm default 2.4.1 로 기본 버젼 지정 가능
        - rails _5.0.6_ new test_app : 프로젝트 생성(test_app이름으로)
* 서버 동작시
    - 우상단의 Run Project는 workspace를 기반으로 되어 있음
    - `rails s -b $PORT -o $IP` : 실행
### 2. 기본
* 변수
    - 지역, 인스턴스 변수 : `@`를 사용하거나 사용하지 않음. 사용시에는 view에서 사용가능
    - 클래스 변수 : `@@` 사용
* 상속
    - ex) `class Users::SessionsController < Devise::SessionsController`
        > Devise의 SessionsController를 상속한다.

* gem
        - ruby가 사용하는 library
* bundler : 설치 --> gem install bundler
    - 내 프로젝트에 사용될 모든 gem을 자동으로 설치함
    - 해당 gem은 Gemfile에 명시한다.
    - Gemfile에 사용할 gem을 명시한 이후 터미널에 다음 명령어 입력
        - `bundle install`
        - 해당 명령어는 사용할 라이브러리를 추가한 이후에도 반드시 해당 명령어를 실행
        - 사용할 gem을 지우더라도 해당 명령어를 다시 수행해야 한다. 그래야 삭제됨
* rails 파일
    - 실행되는 것이 모두 분리되어 있음.
    - test_app/app
        - models, views, controllers
    - config/routes.rb : action에 따른 어떤 logic을 수행할지 명시함
        - 클라이언트의 요청이 들어오면 어떤 controller의 action을 수행할지 지정함.
        - 아래와 같이 설정이 된다.
-<pre><code>
            class __controller
                def action_name
                    end
end
</code></pre>
        - routing의 경우 scaffold방식으로 지정되면 resources를 통해 RESTful API가 만들어지며, devise는 devise for를 통해 생성한다.
        * nested route
            - resources 안에 또다시 resources를 넣을 수 있다.(<a href="https://github.com/hongjw1991/watcha_app">참조</a>)
    - config/initializers : 서버 동작시 처음에 다 읽어들인다.
    - db/ : ORM이용해 db 설정
        - seeds.rb : 다른 db 혹은 csv파일의 내용을 바로 로컬 db에 넣을 수 있다.
            - `rake db:seed` 를 통해 적용 가능(seed는 drop, migrate, seed가 합쳐진 것)
    - log : 로그파일. 각종 로그가 저장됨
    - public : 외부에서 모두가 접근가능한 폴더
    - test : rails의 프레임워크는 TDD(Test Driven Development)에 최적화되어 있음. 즉, test에 어떤 기능을 구현할지 명시할 수 있다.
    - tmp : 임시파일 저장
    - vendor : template 지정
    - Gemfile : gem관리
        - `gem 'gem이름', '~> version'`과 같이 입력한다.
        - `group :development do` 여기에 사용하는 경우 실행시에만 작동하는 gem file을 줄 수 있다.
    - Gemfile.lock : 설치된 dependencies 확인
* rails client - server 요청 관계
    - 하단 이미지 확인
        - Routes는 config/routes.rb
        - DBMS --> db/
* cf)ORM
    - ORM : db에 만들 table의 column등의 설정진행
    - ORM : Object Relational Mapping : 객체와 관계형 DBMS간의 매핑을 지원해주는 Framework
* rails mode
    - Development
        - 변경사항이 자동적으로 확인되고, 모든 로그가 찍힌다.
    - Test
    - Productionr
        - 변경사항이 자동적으로 저장되지 않음. 로그도 일부만 찍힌다.(낮은 level). `$ rails s`로 서버를 실행하지 않는다.
* gems
    * toastr_rails
        - js파일을 이용한 flash를 사용할 수 있다.
        - <a href="https://medium.com/@shilpikayal/toastr-js-with-rails-5-b7677bd56b52">참조</a>
        - 위 참조 링크를 통해 js file에서 어떻게 implementation이 가능한지 알 수 있다.
        - application.js 파일에서 수정가능
    * bootstrap
        - getbootstrap.com에서 bootstrap gem을 사용하기 위한 방법이 설명되어 있다.
            - `class`를 이용하여 css를 입힐 수 있음.
        - gemfile에 `gem 'bootstrap', '~> 4.1.1'`과 같이 하고 command에 bundle install을 하면 설치된다.
        - 이후, app/assets/stylesheets/application.scss에서 `@import "bootstrap";`으로 import할 수 있다.
        - 만약 scss가 아니고 css면 단순히 rename할 것
        - 이 부트스트랩을 통해 Grid system을 이용하면 반응형 웹(사이즈에 따라 자동으로 조정)을 쉽게 구현할 수 있다.
            - app/views/layouts/application.html.erb에 다음 코드를 추가한다.
            - `<meta="viewport" content="width=devide-width, initial-scale=1, shrink-to-fit=no">`
        * Grid System
            - 12부분으로 나누어서 화면을 조정할 수 있다.
    - <a href="http://getbootstrap.com/docs/4.1/getting-started/download/">부트스트랩 정보 참조</a>
    * geocoder
        - ip를 기반으로 위치를 알려주는 gem
        - Gemfile에 gem 'geocoder'로 설치 가능
        - request.location : 위치 정보, request.location.region : 지역 정보
    * rails db gem 
        - database viewer를 지원하는 gem이다.
    * Faker gem
        - <pre><code><a href="https://github.com/stympy/faker">참조</a></code></pre>
        - Fake 데이터를 generate
    * bcrypt
        - 비밀번호를 암호화 해주는 gem
        - gem file에 기본으로 주석처리된 상태로 존재.
        - authenticate method : 암호화된 비밀번호가 일치하는지 확인함.
        - rb파일에 `has_secure_password`를 추가하여 사용할 수 있다.
    * carrierwave
        - file upload를 하면 해당 파일을 볼 수 있게 해준다.
        - This gem provides a simple and extremely flexible way to upload files from Ruby applications. It works well with Rack based web applications, such as Ruby on Rails.
        - `rails g uploader 이름` 으로 사용가능 => app폴더 밑에 폴더가 만들어진다.
    * mini_magick
        - uploader에서 resizing을 위해 설치해야 하는 gem
    * fog-aws
        - Amazon S3를 지원하는 gem file
    * figaro
        - 손쉽게 환경변수를 만들고 사용할 수 있는 rails gem
        - gem file에 추가한 후, `bundle install`, `bundle exec figaro install`를 한다.
        - configuration의 파일은 종종 매우 sensitive하기 때문에 자동으로 이를 통해 .gitignore에 추가할 수 있다.
    * devise
        - `gem devise` 로 설치한다.
        - *dependency*가 매우 많은 `gem`이다.
    * turbolink
        - js 파일을 읽어들이는데 도움을 주는 `gem`
        - application.js에서 `require`를 통해 turbolink를 사용하고 application.html.erb에서 head부분에 `, 'data-turbolinks-track': 'reload'` 부분을 통해 로직을 작성한다.
        - *asset/javascripts*아래에 있는 모든 js를 읽어들여 application.js로 합치는 역할을 한다.
* HTTP method
    * get
    * post
    * put : 수정시 사용, 일부 브라우저에서는 지원하지 않음. 따라서 patch와 같이 route시킴, 전체 데이터를 교체함. 모든 필드를 항상 새로운 값으로
    * patch : 수정시 사용, 부분 데이터를 업데이트 함.
    * delete : 서버에 리소스 삭제 요청
* ruby code
    - `p / puts`
        - `p` : 내부 구조까지 전부 보여줌
        - `puts` : 객체를 보여줌
* rails c
    * rails command를 불러오는 명령어
    * 코드
        - 객체 존재여부, 내용이 비어있는지 여부 확인하려면?
            - `nil?`
            - `present?`
            - `empty?`
        - 객체 일치여부
            - `eql?`
* rails method
    > class method
        > 사용 방법 : <pre><code>def 메소드명(매개변수)
                                        로직안에서 self 쓸수 없음   
        >                        end</code></pre>

    > instance method
        > 사용 방법 : <pre><code>def self.메소드명(매개변수)
                                        로직안에서 self를 쓸 수 있음
                                        self==현재 자신 객체
        >                        end</code></pre>
        
    - cf) 아래의 !, ?와 같은 경우는 필수는 아니고, 명시적인 표시를 할 때 사용한다.
        - 특정 메소드의 경우에는 작동은 같으나 결과가 다를 수 있다!(ex- gsub)
    - ?
        - return 값이 `true`, `false`인 경우에 이와 같이 명명한다.
        - `def user_signed_in?`
           `end`
    - !(bang)
        - 의도하지 않은 액션이 발생할 수 있는 메소드에 붙여준다.
    - private
        - controller의 특정 구간에 private을 써놓으면 그 아래 쪽 method는 전체가 private으로 다른 곳에서 호출할 수 없다.
    - db 입력
        1. new : 새로운 객체 생성.
        2. update : 객체 내용 update(save필요 없음)
            - 만약 rollback되면 false리턴, 저장 되었으면 true리턴
        3. create : 객체 생성. new, save가 모두 실행됨.
        4. save : 저장. create, update시에는 필요 없음
        5. destroy : 객체를 삭제함. -> frozen 상태가 된다.
        6. frozen? : destroy한 경우 true, 새로 만들었거나 기존 상태 유지의 경우 false
    - errors
        - transaction이 rollback되었을 때 해당 error를 볼 수 있다.
* view
    - action명.html.erb : 루비코드가 포함된 html
    - action명.js.erb : 루비코드가 포함된 js
* render와 redirect
    - redirect는 301코드를 반환하여 다른 url로 이동시킨다.
    - render는 그대로 코드가 끝난다. `js: jscode` 와 같이 즉각적으로 js code를 사용할 수 있다.(코드 자체가 응답이 된다.)
* other rails basic
    - require
        - parameter가 존재하는지 확신시킴.
        - 만약 parameter가 존재하면, 해당 parameter의 key에 대한 value를 return. 없으면 에러
* hash type(3가지 방법이 있음) - 아래 코드를 중괄호로 묶어야 함.
    1. `"key" => "value"`
    2. `:key => "value"`
    3. `key: "value"`
* respond_to do |format| 형식(<a href="https://github.com/hongjw1991/watcha_app">사용참조<a/>)
    - 원하는 js 파일로 응답시킬 수 있다.(기존에는 action명에 일치하는 파일로 알아서 찾아가도록 했다.)
    - 그러나 이를 사용시에 분기를 사용하여 서로 다른 js파일로 render시킬 수가 있다.
    - format.html과 format.json
        > 일반적인 요청시 html로 보내고, json으로 요청시 json으로 보낸다.

### 3. MVC
- ![이미지](./readme_img/mvc.JPG)
* Controller
    - 역할?
        - 서비스 로직을 가짐.
        - 모델과 뷰를 연결해준다.
    - 규칙
        - 모델, 뷰에 대해 알고 있어야 한다. 모델과 뷰는 서로에 대해서 알 수 없다.
        - 모델, 뷰의 변경에 대해 인지하고 있어야 한다.
    - app.rb에서 작성한 모든 내용이 `Controller`에 들어간다.
    - `Controller`는 하나의 서비스에 대해서만 작성함.
    - `Controller`를 만들 때에는 `$ rails g controller 컨트롤러명` 을 이용한다.(복수형으로 할 것)
        - ex) 아래 스샷 참조
            `$rails g controller home`
            `# app/controllers/home_controller.rb 파일 생성됨`
            `class HomeController < ApplicationController >> 상속`
        - 모든 `Controller`는 `ApplicationController`를 상속받는다. (상단의 코드는 상속 코드)
        - `HomeController`에서 액션(`def`)를 작성하면 해당 액션명과 일치하는 `view`파일을 *app/views/home*폴더 밑에 작성한다.
        - 사용자의 요청을 받는 url설정은 *config/routes.rb*에서 수행된다.(아래 이미지 참조)
        - 이제는 erb :xxx 와 같은 코드는 필요가 없다. 자동 매핑
    - routes.rb
        - get/post방식을 간단히 mapping가능함.
        - root keyword를 통해 root디렉토리로 연결시 매핑을 할 수 있다.
        - as keyword를 통해 prefix를 지정할 수 있다.
    - parameter 사용
        - `params[:parameter명]`으로 parameter value를 인식할 수 있다.
        * find함수로 db 검색(약 4가지)
            - 특정 column을 사용해 찾기를 원하는 경우 : `find_by_user_name(params[:parameter명])`과 같이 찾을 수 있다.
            1. `Model.find(id)`
                -  이 방식은 인덱싱이 되어 있는 컬럼을 이용하는 것. 검색속도가 매우 빠르며 항상 고유한 값을 가진다.
                - `find`함수를 사용하여 db에서 검색할 parameter지정 가능
            2. `Model.find_by_컬럼명(value)` | `Model.find_by(컬럼명: value)`
                - 사용자가 입력했던 값으로 검색해야 하는 경우
                - 게시글 검색시, 작성자, 제목 등으로 검색하는 경우
                - `find_by`의 특징 : `1개만 검색된다.
            3. `Model.where(컬럼명: 검색어값)`
                - ex) `User.where(user_name: "hello")`
                - 결과 값이 여러개. 배열형태. 일치하는 값이 없는 경우에도 빈 배열이 나옴(실제 배열이 아니라 duck typing)
                - 따라서 `nil?`로 검색하면 `false`값을 얻을 수 있다.
            4. `Model.where("컬럼명 LIKE ?", "%#{value}%")`
                - ex) `User.where("user_name LIKE ?", "%h%")`
                - `Model.where("컬럼명 LIKE '%#(value)%'")` : 가능한 방식이지만 사용해선 안된다.
                    - 사용하면 안되는 이유??
                        - 즉각적인 SQL Injection이 가능해진다.(보안에 취약한 구조). 즉, 사용자가 SQL문을 통해 직접 쿼리가 가능해진다.
                - 텍스트(string, text type)가 특정 단어, 문장을 포함하고 있는가를 검색
                - 다만, 이 방식은 Full table scan으로 오래 걸리는 방식이다.
                - 이에 따라, Full text search라는 방식을 사용하기도 함.(찾아볼것)
    - DB에 입력(두 가지 방법)
        1. 위와 같이 `params[:parameter명]`을 통해 new method를 사용하여 입력(save method 사용해야 함)
        2. update method사용(save필요 없음)
        3. create method사용(new, save를 모두 실행해줌.)
## Controller----------------------            
![이미지](./readme_img/after_command.JPG)            
![이미지](./readme_img/home_controller.JPG)            
![이미지](./readme_img/route_file.JPG)
* Model(아래 스샷 참조)
    - 생성
        - `$ rails g model 모델명`
        - *app/models*아래에 파일이 생성된다.
        - 생성된시간_create_모델명s.rb로 파일이 생성되고 여기에 table을 생성하기 위한 코드를 작성할 수 있다.
    - 역할
        - 데이터를 가진 객체
    - 규칙
        - 사용자가 편집하고자 하는 모든 데이터를 가지고 있어야 한다.
        - 뷰 또는 컨트롤러에 대해 어떠한 정보도 알지 못한다.
        - 변경이 일어나면, 변경에 대해 통지할 수 있는 방법을 구현해야 한다.
    - command
        - `rake db:migrate` : 스키마 및 sql문장 생성. 모델명에 맞는 table이 생성된다.(`rake db:reset`하면 내용만 지움)
        - `rails c`를 통해 rails command를 불러올 수 있다.
        - migrate가 된 이후에 Users라는 클래스 객체를 생성할 수 있고, 이를 변수에 저장할 수 있다.
        - 해당 변수에 저장하는 방식은 `u1 = User.new`와 같이 생성(row추가)하며, `u1.save`하면 자동으로 table에 user가 추가된다.
        - `u1.user_name = ""`처럼 table내의 column value를 지정할 수 잇으며 ORM방식에 의해 자동적으로 SQL문을 생성하여 table에 저장된다.
        - `u1.save`를 통해 sql문 실행 가능.
        - 만약 table에 추가적으로 schema를 수정하고 싶은 경우 rb파일에 `t.string = "email"` 과 같이 가능할 것이다.
        - 이 경우 수정을 위해서 `rake db:drop`을 통해 drop하고 다시 migrate해야 한다.(이전의 데이터는 모두 날아간다.)
        - 따라서 부득이하게 db를 수정해야 할 경우에는 add_column, add_index등의 명령을 통해서 추가해야 한다.
        - *app/models/모델명.rb*에는 아무런 내용이 없지만 ApplicationRecord를 상속함으로써 기능을 사용할 수 있다.
    - column
        - string : 256자까지 가능
        - text : 대략 12000자 까지 가능
    - 모델 코딩
        - 메소드 추가하기(daum_cafe부분 daum.rb참조)
            - 모델에 특정 메소드를 직접 추가하여 사용할 수 있다.
            - 어느 컨트롤러에서든 사용할 수 있다. 그러나 만약 인스턴스 메소드인 경우에는 특정 객체가 요구될 경우 반드시 그를 통해 사용해야 한다.
        - validation
            - 중복 불가 속성 : `uniqueness: true`
            - nil값 불가 속성 : `presence: true`
## Model---------------------------
![이미지](./readme_img/make_model.JPG)
![이미지](./readme_img/ORM_model.JPG)
* View
    - 생성
        - touch
    - 역할
        - Client에게 보여줄 Front page
    - 규칙
        - 액션과 뷰 파일의 이름은 반드시 일치시켜야 한다.
### 4. 유저등록 및 유저정보 가져오기
* 진행
    - user controller생성 : `rails g controller user`
    - controller에 함수 생성 후 action을 연결(routes.rb에 mapping)
    - controller에는 create, new, users등 각 로직을 구성
        * 로직
            - index에는 모델명.all을 통해 전체 row의 정보를 읽어올 수 있다.
            - show에는 모델명.find를 통해 하나의 row의 정보를 찾아 읽어올 수 있다.
            - create에는 new, save등으로 유저 정보를 생성할 수 있다.(개인 유저 정보를 볼 수 있는 곳으로 redirect : redirect_to사용)
                - redirect_to 에 notice를 줄 수 있다. notice가 flash의 key가 되며, 내용이 value가 된다.
                - `redirect_to @post, flash: {success: 'Post was successfully created.'}`와 같이 현재는 변경되었다.
    - POST방식 rails 요청시
        - POST방식으로 정보를 요청하게 되면 단순히 요청시에 rails에서는 오류가 난다.
        - 안정성 및 보안을 높이기 위해서 특정한 토큰을 정보 요청시 같이 전달해야만 한다.
        - `<input type="hidden" name="authenticity_token" value="<%= form_authenticity_token %>">`
        - 해당 token의 경우도 전달될 때마다 지속하여 변경된다.
        - 물론 application_controller에서 protect부분을 주석처리해도 되지만 그 경우 보안이 나빠진다.
* 요청 정보 확인 하기
    - controller에 `p request`와 같이 작성하면 action이 실행될 때 유저의 요청 정보를 서버로그에 나타낼 수 있다.
        - `request`객체를 써내려갈 수 있다. .연산자를 이용해 속성을 뽑아낼 수 있다.
        - 만약 IP정보를 뽑아내고 싶다면 `p request.ip`로 하면 된다.
* 요청 정보 삭제하기
    - find함수를 이용해 parameter로 전달되는 value에 맞는 객체를 찾는다.
    - destroy메소드로 삭제 가능
* 수정하기
    - find로 찾은 다음 다른 내용으로 변경한 다음 save한다.
### 5. form helper 
* 개념
    - *ruby tag*로 *html*코드를 작성할 수 있는 코드
    - view helper의 일종
    - 참조 : http://guides.rubyonrails.org/form_helpers.html
* 예시
    - input 태그
        * submit
            - `<%= submit_tag("tweet") %>`
            - `<input type="submit" value="tweet">`
        * password
            - `<%= password_field_tag(:password) %>`
    - textarea 태그
        - `<%= text_area_tag(:contents, params[:contents], placeholder: "What's happening?", size: "24x6") %>`
        - `<textarea placeholder="What's happening?"></textarea>`
    - a 태그
        - `<%= link_to "새글 쓰기", :method => 'get'%>`
    - form 태그
        - `<%= form_tag("/경로", method: "put")`
        - form helper에서 form태그는 post가 default이다.
### 6. cookie / session
* cookie
    - 서버와 클라이언트가 요청하는 정보는 독립적으로 작용한다.
    - 이 독립적인 부분을 보완하기 위한 것이 cookie(특정 정보는 저장하여 유지할 필요가 있다.)
    - cookie에는 서버 및 클라이언트가 삭제하거나 브라우저가 종료되기 전에는 정보가 유지된다.(웹 브라우저가 저장한다)
    - 쿠키는 사용자가 웹 사이트를 처음 방문할 때 웹 사이트에서 사용자 컴퓨터의 하드 디스크에 저장해 놓는 작은 파일.
    - *웹 서버는 웹 브라우저가 전송한 쿠키를 사용해 필요한 데이터를 읽을 수 있다.*
    - *HTTP 쿠키란 서버가 사용자에 웹 브라우저에 전송하는 작은 데이터 조각으로, 브라우저는 그 데이터 조각을 저장할 수 있고 동일한 서버로 다음 요청 시 함께 전송한다.*
        - 이에 따라, 동일한 유저인지 아닌지 확인할 수 있다.
        - 쿠키는 상태가 없는(statless) HTTP 프로토콜에서 상태 기반 정보를 기억한다.
    - flash정보 또한 cookie. : 휘발성이므로 정보가 전달된 이후에는 사라짐.
    * 목적  
        - 세션 관리
        - 개인화
        - 트래킹
    * 사용
        - `cookies` hash 타입을 사용해 설정 가능
        - `flash` hash 타입을 사용해 설정 가능
* session
    - session id를 생성하여 server memory에 저장.
    - F12 - application에 보면 암호화되어 저장되어 있는 것을 확인 가능
    - 즉, 클라이언트 및 서버 양단에서 저장한다.(cookie는 클라이언트에서 저장)
    - 독립적인 request, response가 전달되는 웹 환경에서 정보를 지속적으로 저장하기 위해 쿠키를 사용했으나 이는 위조가 가능하고 안전하지 않다.
    - 따라서, 서버에 정보를 저장하고 해당 위치, 즉 session ID를 생성해 client에 저장하여 정보를 유지한다.
    - `session` hash 타입을 사용해 설정 가능 : `session[:user_id]`
    - `session` hash 타입은 매우 방대한 정보를 저장하고 있음.
    - 구현한 내용은 daum_cafe_app 부분 참조
### 7. daum_cafe_app 만들기
* rails app 생성
    - rails _5.0.6_ new name
    * 모델 생성
        - rails g model post
    * controller 생성
        - rails g controller board index show new edit
        - 뒤의 parameter를 주면 view파일도 동시에 생성가능
* route 지정
    - RESTful 한 방식으로 지정할 것.
    - 수정 : put, patch
    - 삭제 : delete
* 세션을 이용한 로그인 시스템 만들기
    - `session[:지정hash]` : 이를 이용해 특정 hash key에 value를 저장할 수 있다.
    - 일반적으로 고유한 id를 찾을 수 없으므로 login을 구현시, id를 이용해 찾아야 한다.
        - 유저가 존재하는지 확인하기 위해 `nil?`을 사용. 비밀번호 일치 여부 확인을 위해 `eql?`사용
        - 검색한 내용을 활용시 `empty?`를 사용해 비어있는지 확인할 수 있다.
        - 존재여부를 묻는 경우 `present?`를 사용할 수도 있다.
        `user.present?`
        - `find_by_column명(params[:parameter명])`으로 찾는다.
    - id를 찾아서 db에 저장된 객체를 찾았으면 해당 id에 따른 고유한 값을 `session[:current_name]`과 같이 hash타입에 저장한다.
    - 이에 따라 현재 로그인된 유저 정보를 index에 보여줄 수 있다.
        - `model명.find(session[:current_name]) if session[:current_name]`으로 찾고 변수에 저장해 사용할 수 있다.
* 코드 줄이기
    - 동일한 코드의 반복을 줄일 필요가 있다. 하나의 메소드로 관리
        - `def set_post`
               `@post = Post.find(params[:id])`
            `end`
        - 위와 같이 하나의 메소드로 코드를 지정하면 하나의 요청에서는 해당 값이 유지되어 사용된다.
        - 이러한 사용방식을 택할 경우, 변수는 다른 곳에서도 반드시 일치시켜야 한다.
        - 그러나 코드 중복 자체는 줄일 수 없음.
        - 따라서, filter를 사용해 코드 중복을 줄일 수 있다.
    - filter??
        - Filters are methods that are run "before", "after" or "around" a controller action.
        - `before_action :require_login`와 같이 사용할 수 있다.
        - 그러나 모든 action에 대해 지정하면 오류가 날 수 있으므로, 특정 경우에만 사용토록 해야 한다.(only)
        - `before_action :set_post, only: [:show, :edit, :update, :destroy]`
        - `before_action :set_post, except: [:index, :new, :create]` : 이와 같이 제외하는 방식으로 사용해도 된다.
    - application_controller이용
        - 현재 로그인된 유저 확인, 로그인 상태 확인 메소드 생성
        - 어디서든 메소드를 불러 즉각적으로 사용할 수 있음.
        - 따라서 해당 코드를 다른 컨트롤러에서 사용 가능.
        - 이를 통해 특정 액션의 경우 로그인된 상태에서만 입장할 수 있게 하려면?
            `def authenticate_user!`
            `   unless user_signed_in?`
            `    redirect_to '/sign_in'`
     
            `    end`
            `end`
        - 위와 같이 메소드를 지정한 다음 board_controller에 filter를 사용
            `before_action :authenticate_user!, except: [:index, :show]`
        - View file에서 controller에 있는 action을 사용하기 위해 시도하는 경우
            - 단순히 사용하면 선언되지 않은 메소드라고 오류를 내보낸다.
            - Cycle상, controller에 있던 메소드를 거쳐서 view로 넘어온 것이기 때문에 다시 돌아가서 확인할 수가 없는 것이다.
            - 따라서, helper_method를 사용한다.
            - `helper_method :메소드명` 과 같이 사용할 수 있다.
* 한명의 유저가 여러 글을 작성(1:n 구조 구현)
    - 유저가 1이고 글(post)가 n이다. 따라서 다음과 같이 rb file에 작성할 수 있다.
        - user.rb에 넣을 코드 : `has_many :posts` : 반드시 복수형으로 지정해야 한다.
        - post.rb에 넣을 코드 : `belongs_to :user`
        - posts와 user는 메소드 처럼 사용할 수 있다.
    - db를 변경한다. 모델명_id를 통해 foreign key를 지정할 수 있다.
        - `t.integer :user_id`
        - 위와 같이 posts table에 칼럼을 추가하여 외래키를 지정할 수 있다.
        - 외래키 지정시에는 `:foreign_key true`로 속성을 줄 수 있지만, 만약 table이 post가 먼저 만들어지고 user가 이후에 만들어지는 경우에는 불가능.
        - rails c를 통해 command하고 특정 유저를 만들고 post객체를 만든 다음 post를 채워넣고
            - `u.posts`, `p.user`를 통해 user가 작성한 post들, post를 작성한 user 정보를 확인할 수 있다.
    - 이에 따라 controller에서 post를 create할 때마다 user의 id를 저장해야 한다.
        - `post.user_id = current_user.id`로 application_controller에 있는 current_user메소드를 호출하고
        - 세션에 저장된 user_id를 통해 User모델에서 객체를 찾고 고유한 해당 id값을 저장한다.
    - 위 과정으로 외래키를 지정할 수 있으며, user / post를 연결해 각각에 대해 쿼리할 수 있다.
* Rendering
    - 참조 : <pre><code><a href="http://guides.rubyonrails.org/layouts_and_rendering.html">내용참조</a></code></pre>
    - 특정 내용을 다른 페이지에 위치시킬 수 있다.(렌더링)
    - 파일을 분해하여 파편화하고 관리가 편해지도록 만들 수 있다. 이 경우 사용
    - 방법
        - _file명.html.erb로 파일을 만들고 내용을 채워넣는다.(각 내용을 파편화)
        - 실제 보여줄 페이지에서 `<%= render '파일명(_제외됨)' %>`와 같이 사용하면 된다.
        - 만약 렌더링할 페이지를 특정 위치에 놓은 경우, 해당 resource uri를 주면 된다.
        - 보통 여러 view에서 공유할 렌더링 페이지는 shared라고 폴더를 만들고 해당 내용을 관리함.
        - `<%= render '파일명', 분해된 파일에서 사용코자 하는 변수명: 실제 변수명 %>` : 이와 같이 parameter를 줄 수 있다.
            - 이 경우에는 해당 변수를 이용하여 rendering 시킬 수 있다.
### 8. Scaffold
* 생성
    - `rails g scaffold 이름 title:string contents:text`
    - 위 명령어를 실행하면, scaffold가 생성되며 자동으로 RESTful형식으로 route가 추가된다.(`resources :scaffold명`)
        - `rake routes`명령을 통해 확인할 수 있다. 
* form_for
    - 기존 form_tag의 경우
        - 기존의 경우 `<%= form_tag("url") do %> <% end %> `와 같이 작성하고 내부에 `text_area_tag, text_field_tag`를 사용했다.
        - 문제는, 이 형태를 사용하게 되면 `edit`과 같은 부분에서 중복해서 사용할 수 없다.
        - 그러나, 모델과 관련 없는 parameter도 넘길 수 있다.(보안 이슈 발생 가능)
    - form_for의 경우
        - 특정한 parameter를 넘기는 것이 불가능. 즉, model과 관련없는 input tag는 설정 불가하다.
        - 또한 `edit`과 `new`와 같이 코드가 다른 경우에도 스스로 인식하여 value를 채우거나 없으면 채워넣지 않는 방식으로 작동함.
        - 그 이유는 SQL Injection과 같은 공격에서 보안 이슈를 해결하기 위함이다.
        - 예시 <pre><code><%= form_for(@post) do |f| %>
                        <%= f.text_field(:title) %>
                        <%= f.text_area(:contents) %>
                        <%= f.text_field(:description) %>  <-- 불가능 </code></pre>
        - 이에 따라, scaffold는 tag에서 전달하는 name도 이중으로 전달된다. ex) `name="post[title]"`
        - hidden input tag의 경우 : `hidden_field`
        - file upload : `file_field`
    - form_for url
        - `form_for(변수)`에서 변수가 비어있는지 채워져있는지에 따라서 자동으로 new / edit으로 지정된다.
        - 따라서, 객체가 비어있는지, 저장되어 있는 값을 불러온건지가 중요!
        - 따라서, view파일 까지 naming을 명확하게 일치시켜주지 않으면 오류가 난다.
    - form_for html class 입히기
        - `<%= form_for(post, html: {class: 'text-center'}) do |f| %>` 와 같이 설정.
* scaffold 의 post_params
    - <pre><code>def post_params
                    params.require(:post).permit(:title, :contents)
                end</code></pre>
    - `require`에 의해 parameter가 존재하는지 확인하고 permit으로 형태 조정
    - `{title: params[:post][:title], contents: [:post][:contents]}`와 같다.
* link_to
    - 링크를 지정시에 route에 지정된 prefix를 사용할 수 있다.
    - `지정된prefix_path`를 이용해 지정 가능
        - ex) `<%= link_to '글보기', post_path(post) %>`
    - 알아서 필요한 key를 뽑아서 링크를 지정할 수 있다.
    - method 또한 지정 가능.
        - ex) `<%= link_to '삭제', post_path(@post), method: 'DELETE', class: 'btn btn-danger' %>`
        - 위에서 `@post`처럼 객체를 전달하면 RESTful한 URL이 생성되었기에 해당 id를 전달하게 된다.
### 9. 댓글 기능 만들기(daum_cafe 참조)
* 모델
    - `rails g model comment content post_id: interger`
* 관계(post와 comment 모델)
    - 한 게시글에 여러 댓글(1 : n)
    - 따라서, comment.rb 모델에는 `belongs_to :post`, post.rb 모델에는 `has_many :comments`
* route
    * 생성
        - 어떤 게시글에 속할지 알아야 하므로 게시글의 id가 필요
            - `post 'post/:id/comments/create' => "comments#create` : 특정 post(게시글)에 댓글을 만든다.
    * 삭제
        - 어떤 게시글에 들어가 있는지는 명확함. 댓글의 id만 필요
            - `delete 'comments/:id' => 'comments#destroy'`
* controller
    - `rails g controller comments create destroy` : 우선 댓글 controller는 만들고 삭제할 수만 있게 하기 위해 action 설정
    - 액션
        - create
            - 이 경우에는 특정 게시글에 댓글을 달아야 하므로 게시글의 id를 저장해야 한다.
        - destroy
            - 이 경우에는 댓글의 id만 있으면 삭제할 수 있다. 따라서 댓글의 id로 찾는다
* view
    - show
        - 게시글이 show되는 부분에서 댓글이 삽입되고 삭제되어야 한다.
### 10. M:N 관계 구현(daum_cafe참조)
* 생성
    - cafe와 user는 서로 M:N 관계이다. 유저는 여러 카페에 가입할 수 있으며, 카페는 여러 유저를 가질 수 있다.
    - 모델링
        - 1번 유저가 1,2,3번 카페에 가입
            - `u1.dames => [1, 2, 3]`
        - 2번 유저가 2,3번 카페에 가입
        - 3번 유저는 1,3번 카페에 가입
        - -------------------------
        - 1번 카페에는 1,3번 유저가 가입했다.
            - `c1.users => [1, 3]`
        - 2번 카페에는 1,2번 유저가 가입했다.
        - 3번 카페에는 1,2,3번 유저가 가입했다.
* join table
    - M:N의 관계를 가지는 Table관계에서 서로를 연결해주기 위해서 join table이 필요함
    - 해당 table은 양 테이블의 id를 갖고 있음.
    - 따라서, 양 쪽 id에 종속되므로 `belongs_to`를 2개 추가한다.
* daum 및 user table
    - memberships라는 join table을 통해서 각자의 객체를 여럿 가질 수 있다.
    - 따라서, 기본적으로 `has_many :memberships`를 포함하며
    - 추가적으로 `has_many :users | daums through: :memberships`를 통해 양 단을 연결할 수 있다.
    - 여기 까지 완성하면, rails command에서 `reload!`로 load를 한 후에(필요시), `u1 = User.first`, `u1.daums`를 하면 u1이 가입한 카페를 확인할 수 있다.
* parameter전달 method
    - <pre><code>def daum_params
          params.require(:daum).permit(:title, :contents)
      end</code></pre>
    - 위와 같이 parameter를 전달하게 하는 method를 따로 구성하면 코드를 줄일 수 있다. `require`에 들어가는 simbol은 모델명을 사용한다.
    - 특정 parameter만 전달할 수 있도록 지정할 수 있다.
### 11. 전체 카페 구현(daum_cafe)
* 기본 내용
    - 모델
        - daum(cafe를 의미), user, post(게시글 - 각 카페에 저장됨), membership(카페와 유저 M:N관계 join table), comment(댓글)
    - 컨트롤러
        - cafe, user, authenticate(회원가입, 로그인 등), comment, post
    - view
        - 
* rails 설정
    - route
        - resources 사용시 각 RESTful URL이 생성됨.
    - gem
        - bootstrap : 부트스트랩의 UI 사용
        - bcrypt : 비밀번호 암호화하여 사용하는 gem
        - Faker : 테스트용으로 seed파일을 이용하여 무작위 데이터 입력시 사용
        - fog-aws : Amazon S3를 지원하는 file uploader gem
        - mini_magick : file resizing등에 사용
        - carrierwave : file upload시 사용
        - figaro : credential하게 프로젝트를 관리할 수 있다.(application.yml 파일이 .gitignore에 추가됨)
    - seeds
    - JS and Stylesheete
        - `@import 'bootstrap';`으로 부트스트랩 import
        - `popper, bootstrap require`
    - app
        - uploader(carrierwave gem 필요)
            - 만들기
                > `rails g uploader uploader이름`

            - uploader를 mount 시킨다
                > `mount_uploader :image_path, ImageUploader` : 해당 내용을 post.rb로 마운트시킨다.

            - 이미지를 업로드시에 리사이징(용량, 크기) 할 수 있다.
                > ubuntu환경 : `sudo apt-get update`를 한 다음 `sudo apt-get install imagemagick`
                
                > MacOS : `brew install imagemagick`
                
                > uploader.rb에서 `include CarrierWave::MiniMagick`를 주석해제 하고, mini_magick gem을 설치한다.
                
                * resize_to_fill / resize_to_fit
                    - uploader파일에서 주석 처리되어 있는 부분을 해제 하고 사이즈를 지정한다.
                    - fill은 지정사이즈에 맞춰 resizing하고 남는 부분을 자른다.
                    - fit은 가로 세로 비율을 맞추어서 fitting해준다.
                    - 사용시에는 해당 versioning된 `method.url`을 이용하여 사용한다.(*posts/show.html.erb*참조)
            - 특정 확장자만 가능하도록 지정할 수 있다.(`extension_whitelist`)
                - 다른 종류의 파일을 올리게 되면 transaction이 진행되지 않는다.
                - 이미지외에 다른 파일을 리사이징하게되면 문제가 될 수 있다.
                - 만약 다른 파일을 업로드 하고 싶은 경우에는 다른 colomn 및 Uploader(`rails g uploader 이름`으로 새로 생성)를 이용하여 mount해야 한다.
            - filename
                - upload시에 `model.id`가 아닌 original_filename으로 업로드할 수 있다.
    - config
        - initializer
            - fog.rb : <a href="https://github.com/carrierwaveuploader/carrierwave">fog</a>에 있는 fog부분을 copy paste한다.
                - *application.yml*에 amazon key, secret key를 지정하고 개발 단계에서만 사용(development:)
                - fog.rb에서 모든 key, endpoint등을 지정하고 uploader.rb에서 storage를 fog로 변경하면 된다.
                - 이에 따라, 이미지를 업로드 하면 이제 경로가 S3의 경로로 되며, 버킷을 살펴보면 변화가 있는 것을 알 수 있다.
* 전체
    - controller(application_controller) : 추가 필요
        - `helper_method` : 뷰에서 해당 메소드를 직접 사용할 수 있도록 지정할 수 있다.
            > user_signed_in? 과 current_user를 지정

        - user_signed_in? : 현재 로그인한 유저가 있는지 확인
            > `session[sign_in_user].present?` 로직으로 현재 로그인한 유저 여부 확인 및 `true | false`반환

        - authenticate_user : 유저가 로그인하지 않았다면 로그인 페이지로 이동시킨다.
            > cafe 개설, 수정, 가입시에 로그인 되어있는지 확인한다.
            
        - current_user : 로그인을 했다면 현재 유저의 정보를 가져온다.
            > `@current_user = User.find(session[:sign_in_user]) if user_signed_in?`
            
    - view(views/layouts, views/shared) : 추가 필요
* 카페
    - route : `resources`를 사용해 RESTful URL 설정.(destroy제와)
        - 가입 : 가입하는 경우는 `resources`로 지정되어 있지 않으므로 따로 지정한다.
            > `post '/join_cafe/:cafe_id' => 'cafes#join_cafe', as: 'join_cafe'` : prefix를 지정할 수 있다.

    - 관계
        - 한 명의 유저는 여러 카페를 가질 수 있고, 하나의 카페는 여러 유저를 회원으로 갖는다(유저와 M:N관계)
            > Membership으로 Join Table을 만들어 관계설정

        - 한 카페는 다수의 Post를 가질 수 있으며, 하나의 Post는 하나의 Cafe(daum)만 갖는다.(게시글과 1:N관계)
    - 모델(daum.rb)
        - db에는 카페의 title, description, 개설한 user의 name(master_name)을 저장한다.
    - 컨트롤러
        - 액션
            * before_action : 카페에 대한 정보 요청시, 카페 개설, 수정, 가입 등은 인증된 사용자만 가능하다.
                > `authenticate_user`로 확인
                
            * index : 카페의 전체 목록을 보여준다.(`@cafe`)에 저장
            * show : 특정 카페의 정보를 보여준다.(`@cafe`)에 저장, find함수 사용
                > 관계에서 한 카페는 다수의 Post를 가질 수 있다. 따라서, Post작성 시, 어떤 카페에서 작성되었는지 정보가 필요하다.
                
                > 카페의 id를 저장해서 hash로 알 필요가 있다. 이곳에서 `session[:current_cafe]`를 이용해 미리 아이디를 저장하고
                해당 내용을 전달하는 방식을 사용할 수 있다.
                
            * new : 새로운 카페를 개설할 때 사용한다.
                > `authenticate_user`로 인증된 유저인지 확인 후 개설해야 한다.
                
            * create : 실제로 카페를 개설하는 로직을 작성한다.(post방식)
                > `daum_paras`를 통해 `form_for`로 전달된 parameter를 확인하여 저장.
                
                > 카페 개설자의 id는 master_name으로 저장한다. 현재 유저는 session에 의해 application_controller에서 찾는 로직을 구성
                
                > 카페 개설에 성공했을 경우, Membership을 추가하고 redirect
                
                > 만약 실패했다면 실패 로그를 서버에 저장. `errors`메소드를 사용
            
            * edit : 카페 정보를 수정할 수 있는 페이지로 이동
                > id를 통해 해당 카페의 정보를 모델에서 찾아온다.
            
            * join_cafe : 카페에 실제로 가입하는 로직
                > 중복 가입을 막기 위해 Model코딩을 한다.(메소드를 추가하거나, Validation을 이용한다.) : ex)daum.rb의 `is_member`인스턴스 메소드
                
                > 예를 들어, 인스턴스 메소드 is_member를 추가하면 해당 메소드로 카페에 유저가 추가되어 있는지 확인할 수 있다.
                
                > 따라서, 메소드의 리턴값을 사용해 로직을 구성하여 가입 성공 실패를 결정한다.
                
                > 또는, join table인 Membership 모델에 `validate` keyword를 이용하여 제약을 추가할 수 있다.
                
            * daum_params(private) : model에서 쿼리하고 객체를 반환할 때 parameter를 전달하기 위한 메소드
                > `params.require(model_name).permit(parameters)`를 통해 모델에 지정된 parameter를 전달할 수 있다.
                
    - 뷰
        - index : 개설된 카페 리스트를 보여주며 새로운 카페를 개설할 수 있다.
        - new : `form_for`를 통해 새로 개설할 카페의 title, description을 지정한다.
        - show : 카페에 가입할 수 있으며, 카페의 정보가 보인다. 새 글을 작성할 수 있다.(기가입 여부에 따라 다른 로직)
            > 새 글을 작성시에는 카페의 id를 전달하여 어느 카페에서 전달했는지 확인할 수 있다.(혹은 세션을 사용)
            
* 유저
    - 관계
        - `has_secure_password`를 통해 password를 check할 수 있다.
        - 하나의 유저는 여러 카페를 가입할 수 있고, 카페는 여러 명의 유저를 회원으로 갖는다.
        - 따라서, join table인 membership을 통해 서로를 연결한다.(`has_many`, `through`)
    - 모델
        - 회원의 정보를 저장하는 id, password(*bcrypt gem*을 이용해 암호화)를 요구
    - 컨트롤러(authenticate_controller) : 회원가입, 로그인, 로그아웃 로직을 작성한다.
        - sign_up : 실제 회원가입을 할 수 있는 페이지로 이동
        - user_sign_up : *password*와 *password_confirmation*이 같은 경우에만 가능. *bcrypt* 버전에 따라 내용이 달라짐. 추가 필요
            > 성공한 경우 저장하고 페이지를 이동. 실패시 transaction오류를 확인하기 위해 서버에 로그를 저장한다.

        - sign_in : 로그인 페이지로 이동시킨다.
        - user_sign_in : 실제 로그인을 진행하는 로직을 구현한다.
            > id로 찾을 수 없으므로 `user_name`으로 find_by하여 객체를 찾는다. 찾으면 해당 유저의 존재여부, 비밀번호 일치 여부 확인(`authenticate`메소드)
            
            > 비밀번호까지 일치하는 경우, session에 hash를 추가하여 저장, 실패시 이동 및 서버로그를 찍는다.
            
        - sign_out : 로그아웃 로직을 작성한다.
            > 세션을 `delete`한다.
            
    - 뷰
        - authenticate/sign_in
            > 로그인에 필요한 아이디, 비밀번호를 입력받는다.
            
        - authenticate/sign_up
            > 회원가입에 필요한 아이디, 비밀번호, 비밀번호 확인을 입력받는 페이지
            
* 게시글(post)
    - 관계
        - 한 유저는 여러 포스트를 작성하며, 하나의 포스트는 한명의 유저에 의해 작성된다.(유저와 1:n 관계)
        - 한 카페는 여러 포스트를 가지며, 하나의 포스트는 하나의 카페에 종속된다.(카페와 1:n 관계)
        - 한 포스트는 여러 댓글을 가지며, 한 댓글은 하나의 포스트에 종속된다.(댓글과 1:n 관계)
    - 모델
        - 게시글 제목, content, 이미지 경로를 가지며, 관계에 의해 `user_id`, `daum_id`를 가진다.
        * ImageUploader : 이미지를 업로드하기 위해서 사용하는 uploader
    - 컨트롤러
        - before_action : 코드를 줄이기 위해 Post객체를 찾는 set_post를 show, edit, destroy, update액션 이전에 수행
        - index : 게시글 전체를 보여주는 action
        - show : 특정 게시글만 보여준다.(set_post를 before_action으로 수행하여 해당 객체를 불러옴)
        - new : 새로운 게시글 객체 생성.
        - create : 게시글을 실제 작성하는 로직. 
            > 이 부분에서, 카페와 post의 관계를 이어주기 위해 어떤 카페에서 작성된 글인지 확인하고 싶은 경우 `session`객체를 이용할 수 있다.

            > ex) `@post.daum_id = session[:current_cafe]`
            
        - edit : 수정하는 페이지로 이동
        - update : 실제 게시글을 수정하는 action
            > `update` method를 이용하여 코드를 줄일 수 있다.
            
        - destroy : 게시글을 삭제함
            > `destroy` 메소드 사용
            
        - set_post(private) : 코드의 중복을 줄이기 위해 작성한 로직. Post객체를 읽어온다.
        - post_params(private) : 게시글 작성 및 수정시 parameter를 전달해준다.
    - 뷰
        - _form : 게시글 작성, 수정시 render시킬 form
        - edit : 수정페이지
        - index : 글 전체 목록 페이지
        - new : 글 작성 페이지
        - show : 글 세부 내용 보여주는 페이지(글, 댓글, 업로드된 이미지 등)
* 댓글(comment)
    - route : 어떤 게시글에서 작성되었는지 RESTful하게 표시해줄 필요가 있다. 따라서,
        > `post '/posts/:id/comments/create' => 'comments#create'` 이와 같이 route시킨다.

    - 관계 
        - 하나의 게시글에는 여러 댓글이 달릴 수 있고, 하나의 댓글은 하나의 포스트에 종속된다.(post와 1:n관계)
    - 모델
        - 댓글 내용, 작성된 post의 id가 필요하다.
    - 컨트롤러
        - create : 댓글을 생성한다.
        - destroy : 댓글을 삭제한다.
    - 뷰
        - _form : 댓글을 작성하기 위한 render form
### 12. 디바이스로 구현하기
* 참조
<a href="">깃허브 참조 사이트</a>
* gem
    - devise 설치
        - `gem devise` -> `bundle install`
    - `rails g devise:install` : initializers에 rb파일과 yml파일을 생성한다.
        > generator로 devise 실행

    - 이 때, 특정 setup을 반드시 진행해야 한다. command에 나온 것을 참조
    - 현재는 개발환경에서 사용할 것이므로 development.rb에 추가한다.
* controller
    - `rails g controller home index` : *home controller*를 만들고 `index` action 생성
    - root route를 `home#index` 로 변경한다.
    - `rails g devise:controllers 컨트롤러 명 ` : 특정 controller에 대한 다양한 controller 파일을 만들어준다.
* model
    - `rails g devise:모델명`으로 생성(복수형으로 지정시 알아서 단수형으로 바꿔줌)
    - *devise*는 기본적으로 email을 id로써 받는다.
* route
    - `devise_for :모델명` : 이를 통해 수많은 route가 생성됨
### 13. 카카오톡 챗봇 API
* 참조
    - <a href="https://github.com/5chang2/kakao_bot_sample">사용방법</a>
    - <a href="https://github.com/plusfriend/auto_reply">API 문서</a>
* API 요청(request / response)
    - request
        - 이용자가 최초로 채팅방에 들어올 때 기본으로 키보드 영역에 표시될 자동응답 명령어의 목록을 호출하는 API.
        - Specification
            > `Method : GET`
            `URL : http(s)://:your_server_url/keyboard`
            `Content-Type : application/json; charset=utf-8`
    - response
        - 사용자가 선택한 명령어를 파트너사 서버로 전달하는 API
        - 사용자가 선택한 명령어는 `content` parameter로 받을 수 있으며, response는 `message, keyboard`로 보낼 수 있다.
        - Specification
            > `Method : POST`
            `URL : http(s)://:your_server_url/message`
            `Content-Type : application/json; charset=utf-8`
* controller 생성
    - *keyboard controller* : `rails g controller keyboard`
        - 이 키보드 컨트롤러에서 Hash 타입으로 값을 전달한다.
* route
    - API request방식이 keyboard로 이루어진다. 따라서 route도 변경한다.
        - `get '/keyboard' => '프로젝트명#keyboard'` : 이와 같이 변경
    - user로부터 받는 명령어를 post 방식으로 전달 받는다.
        - `post '/message' => '프로젝트명#message'`
### 14. JS
* CSS선택자
    - 참조 : <a href="https://www.w3schools.com/cssref/css_selectors.asp">W3S</a>
* 함수
    - 특정 Element 찾기
        - getElementById("id명") : 가장 먼저 찾은 하나만 리턴
        - getElementsByName("name")
        - getElementsByClassName("class명")
        - getElementsByTagName("tag명")
        - querySelector("쿼리선택자") : 가장 먼저 찾은 하나만 리턴
        - querySelectorAll("쿼리선택자")
    - jQuery로 Element 찾기(배열처럼 인식하여 모두 보여줌)
        - `$('.btn')` : btn class를 모두 보여준다.
        - `$('button')` : button을 모두 찾아준다.
        - `$('#title')` : title id를 가진 태그를 찾는다. 하지만 이 경우에도 역시 id는 유일하게 맨 처음 요소 하나만 반환한다.
    - 속성 관련
        - setAttribute("속성명", "속성 값"); : 속성을 변경할 수 있다.
            - attribute는 `console.dir(객체)` 를 통해서 확인해보면 attribute라는 부분이 있다. 이 부분을 활용
* 변수
    - 선언 : var
        - ex) `var btn = document.getElementById("title")`
* 콘솔
    - console.log
    - console.error
    - console.dir(객체) : 해당 객체가 가지는 모든 속성을 반환(변수에 저장한 경우 변수에 저장된 모든 객체에 대해 반환)
* 이벤트(이벤트 감지 후 react)
    - Event Listener : 이벤트 감지
    - 다양한 속성 중, on으로 시작하는 것들이 대부분 event
        > `요소.on이벤트이름 = react행위`와 같이 사용

    - function : Event handler(이벤트 처리)
        - function을 사용해 특정 react를 등록하면 이벤트가 발생시에 해당 함수가 작동한다.
        * 함수 만드는 방법
            1. 변수에 직접적으로 저장한다.(함수 표현식)
                - 실행시에는 `변수명()`으로 실행
                - 선언하기 전에 사용하면 실행되지 않는다.
                > ex) `var func = function() {}`
                
                > `func()`
                
            2. `function function_name() { 실행문 }`(함수 선언식)
                - 실행시에는 `함수명()`으로 실행
                - 선언되기 이전에 사용해도 실행된다.
                - 이와 같이 선언한 함수를 addEventListener로 사용하고 싶으면 이름만으로 넣어야 한다.
                    - 왜냐하면, ()를 사용하면 실행을 의미하기 때문이다.
                    > ex) `btn.addEventListener("mouseover", func2)`
                    
            3. 익명함수 - addEventListener와 같이 지정하는 경우 익명함수를 사용하기도 함
            4. 선언된 함수를 핸들러로 지정 하는 방법
                - 지정시에는 함수의 이름만으로 지정해야 한다.
                - 만약 ()를 포함하는 경우에는 실행을 의미하기 때문에 반영되지 않는다.
    - addEventListener를 사용한 이벤트 등록
        - 해당 경우에는 직접 이벤트를 등록하지 않는다.
        - 이벤트가 계속해서 쌓이는 방식(중첩될 위험이 있으므로 주의한다.)
        - addEventListener를 사용시에는 on을 빼고 넣는다.
        > 첫 번째 인자로 event로 주고, 두 번째 인자로 handler를 준다.
        
        > ex : `btn.addEventListener("mouseover", function() {})`
    
    - jQuery를 사용한 이벤트 적용
        - <pre><code>
            $(.btn).mouseover(function(){
                alert("hahah");  
            })
        </code></pre>
        - <pre><code>
            $(.btn).on('mouseover', function(){
                alert("hahah");  
            })
        </code></pre>
        - 위와 같이 가능하며, 이 경우에 javascript에서 사용했던 방식과 다른 점은, btn이라는 클래스를 가진 모든 경우에 event가 적용된다는 것이다.
        - 한 번에 여러 가지의 이벤트도 인식시킬 수 있다.
        - <pre><code>
        btn.on('mouseenter mouseout', function(){
            if(btn.hasClass('btn-danger')){
                btn.removeClass("btn-danger").addClass('btn-primary');
            } else {
                btn.removeClass('btn-primary').addClass('btn-danger');
            }
        });
        </code></pre>
        - 바로 위 코드를 더 쉽게 작성할 경우
        - <pre><code>
        btn.on('mouseenter mouseout', function(){
            btn.toggleClass('btn-danger').toggleClass('btn-primary');
        });
        </code></pre>
        - 그런데, 위와 같이 작성할 경우 모든 btn에 대해서 해당 이벤트가 작동한다.
        - 따라서, `$(this)`를 사용한다.
        - <pre><code>
        btn.on('mouseenter mouseout', function(){
            $(this).toggleClass('btn-danger').toggleClass('btn-primary');
        });
        </code></pre>
* this 
    - 이벤트가 발생한 자기 자신을 의미한다.
    - `console.dir(this);` : html요소 자체
    - `console.dir($(this));` : jQuery 요소 --> jQuery 함수를 사용할 수 있다.
* Syntax
    - 조건문
        - 자바와 동일
        - if(조건) {} else {} 
    - 반복분
* jQuery 함수
    - hasClass : class를 가졌는지 확인
    - addClass : class 추가
    - removeClass : class 제거
    - toggleClass : class추가 및 제거를 이벤트에 따라 수행(여러 클래스를 한 번에 다 작성해도 된다.)
    - attr : 속성을 추가하거나 속성값을 반환
        - <pre><code>
            btn.on('mouseover', function(){
                $('.card-img-top').attr('style','width:100px');
            });
        </code></pre>
        - 위와 같이, card-img-top클래스를 가진 요소에 style을 추가할 수 있다.
    - text : text value를 변경시킬 수 있다. 값을 넣지 않으면 해당 value를 꺼낸다(val()도 같은 역할)
        - 만약 `$('객체명')`과 같이 사용하게 된다면, `innerHTML, innerText`는 사용할 수 있지만 반환값이 배열형이기 때문에 [0]과 같이 명시를 해야한다.
        - <pre><code>
            btn.on('mouseover', function(){
                $('.card-title').text("Don't Touch me!");
            });
        </code></pre>
        - 만약에 위 코드를 `$(.this)`를 사용해서 하고 싶은 경우, siblings method를 통해 find하여 찾아야만 한다.
    - siblings : 자신과 같은 수준에 있는 요소들을 반환
    - find : 자식 요소들 중에서 선택자로 준 것을 찾아 반환
    - parent : 부모 요소를 반환
    - `$(document).on('ready', function() {})` : document의 load가 끝나면 스크립트를 실행한다는 규정. 
    - append : html elements를 마지막에 추가
    - prepend : html elements를 beginning 부분에 추가
* JS함수
    - innerHTML과 innerText의 차이 : HTML은 span이 있으면 그걸 통째로 뺴오고 Text는 Text만 빼옴. 그리고 인코딩의 차이가 있음.
    - location.href, location.replace : 특정 url로 이동시킬 수 있다.
* 실습
    - 텍스트 변환기를 만들어본다.(일부러 오타를 만든다.)
        - <pre><code>
            <textarea id="input" placeholder="변환할 텍스트를 입력해주세요."></textarea>
            <button class="translate">바꿔줘</button>
            <h3></h3>
        </code></pre>
        - input에 들어있는 텍스트 중에서 '관리' -> '고나리', '확인' -> '호가인', '훤하다' -> '후너하다' 등으로 텍스트를 오타로 바꾸는 이벤트 핸들러 작성
        - <a href="https://github.com/e-/Hangul.js">여기</a>에서 라이브러리를 받고 자음과 모음 분리하여 다시 단어로 합치기
        - npm명령어 `npm install hangul-js`를 통해 읽어오고 js 를 application.js에서 추가한다.
        - 나머지 로직은 아래를 참조
        - <pre><code>
                <script type="text/javascript">
                      var btn = $('.translate');
                      var input_value;
                      btn.on("click", function(){
                        input_value = $('#input').val();
                        //console.log(input_value);
                        
                        var array1;
                        var ch_array = [];
                        var s = input_value.split("");
                        //console.log(s);
                        
                        for (i = 0; i < s.length; i++) {
                          if(Hangul.isComplete(s[i])){
                            array1 = Hangul.disassemble(s[i], true);
                            console.log("array1" + array1);
                            
                            if(Hangul.endsWithConsonant(s[i])){
                              for(j = 0; j < array1[0].length; j++){
                              //console.log(Hangul.isVowel(array1[j]))
                              
                                if(Hangul.isVowel(array1[0][j-1]) && Hangul.isVowel(array1[0][j]) && Hangul.isConsonant(array1[0][j+1])){
                                  ch_array.push(array1[0][j+1]);
                                  ch_array.push(array1[0][j]);
                                  j++;
                                } else {
                                  ch_array.push(array1[0][j]);
                                }
                              
                              }
                            } else {
                              for(j = 0; j < array1[0].length; j++){
                                ch_array.push(array1[0][j]);
                              }
                            }  
                          //console.log(Hangul.assemble(ch_array));  
                        }
                          
                          
                          $('.haha').text(Hangul.assemble(ch_array));
                        }
                      });

                    </script>
        </code></pre>
* Ajax in rails
    - 작동방식
    - <pre><code>
        $.ajax({
            url: 어느 주소로 요청을 보내는가,
            method: 어떤 http method 요청을 보낼것인가,
            data: {
                k: v 어떤 값을 함께 보낼 것인가,
                // 서버에서는 params[k] => v
            }
        })
        </code></pre>
    - 실습(<a href="https://github.com/hongjw1991/watcha_app">참조</a>)
        * 좋아요 기능 구현하기
            - 특정 글에서 영화에 대한 좋아요를 누를 수 있고 눌렀으면 해당 내용을 표시하며, 누른 후에는 좋아요 취소 버튼을 보여준다.
        * 모델
            - `rails g model like`
            - 한 유저는 여러 like를 누를 수 있으며, 하나의 영화는 여러 like를 받을 수 있다.
            - 여기서 문제는, 한 작성자의 경우 movie에 대한 글을 작성했을 수가 있다. 따라서, 1:n과 m:n이 동시에 존재할 수 있다.
                > 방법 : 1:n관계를 끊고 like는 직접 has_many를 통해 1:n으로 연결하고, movies는 like를 통해 연결하는 것(through)
    
        * 로직
            - 좋아요 버튼을 눌렀을 경우, 서버에 요청
                > 현재 유저가 현재 보고 있는 이 영화가 좋다고 하는 요청
            
            - 서버는 응답이 오면 좋아요 버튼의 텍스트를 좋아요 취소로 바꾸고, `btn-info` -> `btn-warning text-white`로 변경한다.
### 14. Kaminari(pagination)
- <a href="https://github.com/kaminari/kaminari">참조</a>
- pagination을 가능하도록 만들어주는 gem
- <a href="https://github.com/hongjw1991/watcha_app">사용참조</a>