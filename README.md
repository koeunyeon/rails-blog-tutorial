# reference
https://guides.rubyonrails.org/getting_started.html

# 루비 설치
https://www.ruby-lang.org/en/downloads/

## windows
https://rubyinstaller.org/
2021.04.05 기준 추천 버전 [Ruby+DevKit 2.7.2-1 (x64)](https://github.com/oneclick/rubyinstaller2/releases/download/RubyInstaller-2.7.2-1/rubyinstaller-devkit-2.7.2-1-x64.exe)

## 설치 확인
`cmd`
```
ruby --version
```

`ruby 2.7.2p137`

# sqlite3 설치
https://www.sqlite.org/download.html

Precompiled Binaries for Windows => sqlite-tools-win32-x86-3350400.zip
D:\_my\ror_blog\sqlite3\sqlite3.exe 가 있으면 됨.

```
sqlite3 --version
```


# nodejs 설치
https://nodejs.org/en/download/
2021.04.05 기준 14.16.0 임. msi 64-bit 받음.

# yarn 설치
npm install --global yarn

```
yarn --version
```

# rails 설치
```
gem install rails
```
```
rails --version
```
`Rails 6.1.3.1`

# blog 어플리케이션 생성
```
rails new blog
```

# 어플리케이션으로 이동
```
cd /blog
```

# 웹서버 실행
```
ruby bin\rails server
```

http://localhost:3000/


# 라우팅 설정
`/blog/config/routes.rb`
```
Rails.application.routes.draw do
  # For details on the DSL available within this file, see https://guides.rubyonrails.org/routing.html
  get "/articles", to: "articles#index"
end
```

# articles 컨트롤러 생성
```
ruby bin\rails generate controller Articles index --skip-routes
```

아래 내용 자동 생성 (컨트롤러)
`app/controllers/articles_controller.rb`
```
class ArticlesController < ApplicationController
  def index
  end
end
```

아래 내용 자동 생성 (뷰)
`app/views/articles/index.html.erb`
```
<h1>Articles#index</h1>
<p>Find me in app/views/articles/index.html.erb</p>
```

이렇게 바꾼다.
```

```

http://localhost:3000/articles


