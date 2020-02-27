
26.1.3 제킬(JekyII) 설치
루비가 정상적으로 설치가 잘 된 상태에서 제킬을 설치해 보도록 하겠습니다.
먼저 제킬을 설치할 폴더를 하나 생성후에 이동을 합니다.

c:\>mkdir jekyll
c:\>cd jekyll

루비의 페키지 메니저인 gem 툴을 이용하여 제킬을 설치합니다.

c:\jekyll>gem install jekyll
Fetching: public_suffix-3.0.0.gem (100%)
Successfully installed public_suffix-3.0.0
Fetching: addressable-2.5.2.gem (100%)
… 중간생략
Installing ri documentation for jekyll-3.6.0
Done installing documentation for public_suffix, addressable, colorator, rb-fsevent, ffi, rb-inotify, sass-listen, sass, jekyll-sass-converter, listen, jekyll-watch, kramdown, liquid, mercenary, forwardable-extended, pathutil, rouge, safe_yaml, jekyll after 54 seconds
19 gems installed

c:\jekyll>

자동으로 제킬 파일들을 다운로드하여 설치하여 줍니다.


26.2 프로젝트
루비와 지킬 패키지가 설치가 되었다면, 새로운 지킬 웹사이트를 생성해야 합니다.

26.2.1 프로젝트 생성
현재의 폴더에 제킬 프로젝트 사이트 하나를 생성해 봅니다.

제킬을 위한 새로운 템플릿 사이트를 생성할 수 있는 명령을 제공합니다.

c:\jekyll>jekyll new 폴더명

현재의 프로젝트(.)에 제킬 템플릿 사이트 파일들을 생성해 보도록 하겠습니다.

c:\jekyll>jekyll new .
Could not load Bundler. Bundle install skipped.
New jekyll site installed in c:/jekyll.

c:\jekyll>dir/w
 C 드라이브의 볼륨: windows
 볼륨 일련 번호: 447E-0DB0

 c:\jekyll 디렉터리

[.]           [..]          .gitignore    404.html      about.md      Gemfile       index.md      _config.yml
[_posts]
               6개 파일               3,801 바이트
               3개 디렉터리  18,317,680,640 바이트 남음

처음에는 비어있는 폴더에 몇 개의 파일들과 폴더들이 생성이 되었습니다.

26.2.2 서버실행
루비로 개발된 제킬(Jekyll)은 깃허브 저장소로 푸시(push)하기 전에 작성한 정적사이트를 로컬 컴퓨터에서 확인을 할 수 있도록 웹서버 데몬을 지원합니다.

c:\jekyll>jekyll serve
Configuration file: c:/jekyll/_config.yml
            Source: c:/jekyll
       Destination: c:/jekyll/_site
 Incremental build: disabled. Enable with --incremental
      Generating...
                    done in 0.631 seconds.
  Please add the following to your Gemfile to avoid polling for changes:
    gem 'wdm', '>= 0.1.0' if Gem.win_platform?
 Auto-regeneration: enabled for 'c:/jekyll'
    Server address: http://127.0.0.1:4000/
  Server running... press ctrl-c to stop.

이와 같이 출력되면 콘솔을 닫지 말고 표기된 IP주소와 포트로 브라우저 접속을 해봅니다.

http://127.0.0.1:4000/

제킬(Jekyll)로 생성된 정적 웹페이지를 확인해 보실 수 있습니다. 
 

26.2.3 오류해결
만일 지킬 내장 웹서버를 실행시 다음과 같은 오류가 발생할 수 있습니다.

C:/Ruby24-x64/lib/ruby/2.4.0/rubygems/core_ext/kernel_require.rb:55:in `require': cannot load such file -- bundler (LoadError)
        from C:/Ruby24-x64/lib/ruby/2.4.0/rubygems/core_ext/kernel_require.rb:55:in `require'
        from C:/Ruby24-x64/lib/ruby/gems/2.4.0/gems/jekyll-3.6.0/lib/jekyll/plugin_manager.rb:48:in `require_from_bundler'
        from C:/Ruby24-x64/lib/ruby/gems/2.4.0/gems/jekyll-3.6.0/exe/jekyll:11:in `<top (required)>'
        from C:/Ruby24-x64/bin/jekyll:23:in `load'
        from C:/Ruby24-x64/bin/jekyll:23:in `<main>'

이런경우 추가 패키지를 설치하고 다시 실행을 해보면 문제를 해결 할 수 있습니다.

c:\jekyll>gem install bundler
Fetching: bundler-1.20.4.gem (100%)
Successfully installed bundler-1.20.4
Parsing documentation for bundler-1.20.4
Installing ri documentation for bundler-1.20.4
Done installing documentation for bundler after 16 seconds
1 gem installed

c:\jekyll>bundle install
Fetching gem metadata from https://rubygems.org/...........
Fetching version metadata from https://rubygems.org/..
Fetching dependency metadata from https://rubygems.org/.
Resolving dependencies...
Using public_suffix 3.0.0
… 중간생략
Installing minima 2.1.1
Bundle complete! 4 Gemfile dependencies, 25 gems now installed.
Use `bundle info [gemname]` to see where a bundled gem is installed.

다시 jekyll serve 를 실행해 봅니다.


26.3 정적 사이트
제칼을 통하여 정적 사이트를 제작해고 깃허브와 연동하여 페이지를 운영해 보도록 하겠습니다.

26.3.1 생성
제칼을 통하여 쉽게 프로젝트를 생성할 수 있습니다. 

jekyll new 폴더명

명령을 수행하면 지정한 폴더에 제킬 초기 템플릿 파일들이 자동으로 생성을 합니다. 만일 현재의 디렉토리에 생성을 할때는 폴더명 대신에 현재의 디렉토리를 표시하는 점(.) 을 넣으면 됩니다.

26.3.2 마크다운
깃 페이지는 정적 html 파일을 웹페이지로 호스팅을 합니다. 직접 웹페이지 내용을 HTML로 작성이 가능하지만, 일부 컨덴츠의 경우 마크다운으로 작성이 되는 경우가 많이 있습니다.

루비로 만들어진 JekyII 협업 툴은 마크다운으로 생성된 문서들을 html 형태로 출력할 수 있도록 변환 작업을 지원합니다. 또한, 정적 페이지의 사이트를 운영하기 위한 다양한 테마와 처리 기능들을 지원합니다.

깃허브는 깃페이지와 같이 정적 페이지를 생성할 수 있는 JekyII 툴을 지원합니다.

26.3.3 빌드
제칼은 사이트의 내용을 정적 HTML로 자동으로 생성해 줍니다. 생성을 위한 명령어는 콘솔을 통하여 실행됩니다.

Jekyll build

기본값으로 현재의 폴더의 내용을 ./_site에 생성을 합니다. 만일, 다른 폴더에 html 결과물을 생성을 하고자 할때 는 --destination 옵션을 사용하시면 됩니다.

Jekyll build --destnation 출력폴더

또는 현재의 폴더의 컨덴츠 말고 다른 폴더에 컨덴츠가 저장되어 있는 경우 --source 옵션을 이용하여 직접 지정을 할 수도 있습니다.

Jekyll build --source 원본내용 --destnation 출력폴더

매번 html 생성을 하는것과 달리, 원본의 소스가 수정이 되거나 할 때 자동으로 감지하여 자동생성 할 수도 있습니다.

Jekyll build –warch

단, 감지상태에서 자동빌드를 할 때 환경설정파일(_config.yml)파일은 자동으로 적용이 되지 않습니다. _config.yml 파일은 build 명령을 통하여 완전하게 전체 생성을 할할 때 적용이 됩니다.

빌드 생성을 할 때 --source 와 --destnation 은 _config.yml 파일에 설정을 하여 실행을 할 수도 있습니다.

환경파일: _config.yml
source: _source
destination: _depoly


26.4 구조
지킬(jekll)의 주요 기능은 마크다운, 텍스트로 구성된 컨덴츠를 레이아웃과 결합하여보기좋게 정적 HTML 파일을 생성하는 것입니다.

26.4.1 디렉토리 구조
c:\jekyll>tree /f
windows 볼륨에 대한 폴더 경로의 목록입니다.
볼륨 일련 번호가 000000B4 447E:0DB0입니다.
C:.
│  .gitignore
│  404.html
│  about.md
│  Gemfile
│  Gemfile.lock
│  index.md
│  _config.yml
│
├─.sass-cache
│  ├─15209a447bbac67844d817c14c82736f5528653b
│  │      _base.scssc
│  │      _layout.scssc
│  │      _syntax-highlighting.scssc
│  │
│  └─a18dbbb8f958a9c4ec61fca2edd10d7d156591ba
│          minima.scssc
│
├─_posts
│      2017-10-18-welcome-to-jekyll.markdown
│
└─_site
    │  404.html
    │  feed.xml
    │  index.html
    │
    ├─about
    │      index.html
    │
    ├─assets
    │      main.css
    │
    └─jekyll
        └─update
            └─2017
                └─10
                    └─18
                            welcome-to-jekyll.html

26.4.2 _config.yml
제칼의 환경정보를 담고 있는 파일입니다. Jekyll의 옵션을 환경설정 파일에 저장하여 실행을 할 수도 있습니다. 

26.4.3 _drafts
초안이란 아직 게시하지 않은 포스트를 말한다. 파일명 형식에 날짜가 없다: title.MARKUP. 사용 방법은  초안 활용하기를 참고하라. 

26.4.4 _includes
재사용하기 위한 파일을 담는 디렉토리로서, 필요에 따라 포스트나 레이아웃에 손쉽게 삽입할 수 있다. {% include file.ext %} 와 같이 Liquid 태그를 사용하면 _includes/file.ext 파일에 담긴 코드가 삽입된다. 

26.4.5 _layouts
포스트를 포장할 때 사용하는 템플릿이다. 각 포스트 별로 레이아웃을 선택하는 기준은 YAML 머리말이며, 자세한 내용은 다음 섹션에서 설명한다. {{ content }} 와 같이 Liquid 태그를 사용하면 페이지에 컨텐츠가 주입된다. 

26.4.6 _posts
 한마디로 말하면, 당신의 컨텐츠다. 중요한 것은 파일들의 명명규칙인데, 반드시 다음 형식을 따라야 한다: YEAR-MONTH-DAY-title.MARKUP. 고유주소는 포스트 별로 각각 정의할 수 있지만, 날짜와 마크업 언어 종류는 오로지 파일명에 의해 결정된다.

26.4.7 _data
사이트에 사용할 데이터를 적절한 포맷으로 정리하여 보관하는 디렉토리. Jekyll 엔진은 이 디렉토리에 있는 (확장자와 포맷이 .yml 또는 .yaml, .json, .csv 인) 모든 YAML 파일을 자동으로 읽어들여 `site.data` 로 사용할 수 있도록 만든다. 만약 이 디렉토리에 members.yml 라는 파일이 있다면, site.data.members 라고 입력하여 그 컨텐츠를 사용할 수 있다. 

26.4.8 _site
Jekyll 이 변환 작업을 마친 뒤 생성된 사이트가 저장되는 (디폴트) 경로이다. 대부분의 경우, 이 경로를 .gitignore 에 추가하는 것은 괜찮은 생각이다. 

26.4.9 .jekyll-metadata
Jekyll 은 이 파일을 참고하여, 마지막으로 빌드한 이후에 한번도 수정되지 않은 파일은 어떤 것인지, 다음 빌드 때 어떤 파일을 다시 생성해야 하는지 판단할 수 있다. 생성된 사이트에 이 파일이 복사되지는 않는다. 대부분의 경우, 이 파일을 .gitignore 에 추가하는 것은 괜찮은 생각이다. 

26.4.10 index.html 및 다른 HTML, Markdown, Textile 파일
Jekyll 은 YAML 머리말 섹션을 가진 모든 파일을 찾아 변환 작업을 수행한다. 위에서 언급하지 않은 다른 디렉토리나 사이트의 루트 디렉토리에 있는 모든 .html, .markdown, .md, .textile 이 여기에 해당한다. 

26.4.11 다른 파일/폴더
css 나 images 폴더, favicon.ico 파일같이 앞서 언급하지 않은 다른 모든 디렉토리와 파일들은 있는 그대로 생성된 사이트에 복사한다. 다른 사람들이 만든 사이트는 어떤식으로 생겼는지 궁금하다면, Jekyll 을 사용하는 사이트들이 이미 많이 있으니 살펴보도록 한다. 

--////
http://jekyllrb-ko.github.io/docs/posts/

26.4.12 머리말
사이트에 공동적으로 적용되는 머리말을 만들어 삽입을 할 수 있습니다.

26.4.13 포스트작성
마크다운과 리퀴드 템플릿을 응용하여 게시판과 같은 포스트를 생성할 수 있습니다.

26.5 리퀴드 템플릿
지킬은 리퀴드 탬플릿 언어를 지원합니다. 리퀴드는 다양한 프레임워크에서도 이미 사용을 하고 있는 대중적인 템플릿 언어 입니다.

리퀴드를 이용하면 다수의 페이지를 생성 관리하는데, 변수를 사용하고 동적으로 페이지를 빌드 할 수 있습니다.

26.6 정리
깃허브는 정적인 페이지만을 호스팅 서비스 할 수 있는 기능을 제공합니다. 페이지의 수정 및 동적인 처리는 지킬을 통하여 대신 수행하여, 빌드가 됩니다.

지킬을 활용하면 보다 보기 좋은 깃허브 페이지 웹사이트를 생성할 수 있습니다.


