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



# 루트도 `articles#index` 바라보게 변경
`/blog/config/routes.rb`
```
Rails.application.routes.draw do
  # For details on the DSL available within this file, see https://guides.rubyonrails.org/routing.html
  root "articles#index"
  get "/articles", to: "articles#index"
end
```

# article 모델 생성
```
ruby bin\rails generate model Article title:string body:text
```

결과
```
      invoke  active_record
      create    db/migrate/20210405065742_create_articles.rb
      create    app/models/article.rb
      invoke    test_unit
      create      test/models/article_test.rb
      create      test/fixtures/articles.yml
```

# 데이터베이스 마이그레이션
자동 생성되어 있음.
`/blog/db/migrate/날짜_create_articles.rb`
```
class CreateArticles < ActiveRecord::Migration[6.1]
  def change
    create_table :articles do |t|
      t.string :title
      t.text :body

      t.timestamps
    end
  end
end
```

# 마이그레이션 실행
```
ruby bin\rails db:migrate
```

결과
```
== 20210405065742 CreateArticles: migrating ===================================   
-- create_table(:articles)
   -> 0.0030s
== 20210405065742 CreateArticles: migrated (0.0037s) ==========================  
```

파일은 `/blog/db/development.sqlite3` 에 있음.

# 레일즈 콘솔
```
ruby bin\rails console
```

# 객체 생성
```
article = Article.new(title: "Hello Rails", body: "I am on Rails!")
article.save
```

# 객체 조회
```
article
```

```
#<Article id: 1, title: "Hello Rails", body: "I am on Rails!", created_at: "2021-04-05 07:02:52.692494000 +0000", updated_at: "2021-04-05 07:02:52.692494000 +0000">
```

# 객체 가져오기
```
irb(main):004:0> Article.find(1)
  Article Load (0.2ms)  SELECT "articles".* FROM "articles" WHERE "articles"."id" 
= ? LIMIT ?  [["id", 1], ["LIMIT", 1]]
=> #<Article id: 1, title: "Hello Rails", body: "I am on Rails!", created_at: "2021-04-05 07:02:52.692494000 +0000", updated_at: "2021-04-05 07:02:52.692494000 +0000">
```

# 리스트 가져오기
```
irb(main):005:0> Article.all
  Article Load (0.2ms)  SELECT "articles".* FROM "articles" /* loading for inspect */ LIMIT ?  [["LIMIT", 11]]
=> #<ActiveRecord::Relation [#<Article id: 1, title: "Hello Rails", body: "I am on Rails!", created_at: "2021-04-05 07:02:52.692494000 +0000", updated_at: "2021-04-05 07:02:52.692494000 +0000">]>
```

# 컨트롤러에서 모델 사용
`app/controllers/articles_controller.rb`
```
class ArticlesController < ApplicationController
  def index
    @articles = Article.all
  end
end
```

# 뷰 수정
`app/views/articles/index.html.erb`
```
<h1>Articles</h1>

<ul>
  <% @articles.each do |article| %>
    <li>
      <%= article.title %>
    </li>
  <% end %>
</ul>

```

# 개별 글 보여주기
`/blog/config/routes.rb`
```
Rails.application.routes.draw do
  # For details on the DSL available within this file, see https://guides.rubyonrails.org/routing.html
  root "articles#index"
  get "/articles", to: "articles#index"
  get "/articles/:id", to: "articles#show"
end
```

`/blog/app/articles_controller.rb`
```
class ArticlesController < ApplicationController
  def index
    @articles = Article.all
  end

  def show
    @article = Article.find(params[:id])
  end
end
```

`/blog/app/views/articles/show.html.erb`
```
<h1><%= @article.title %></h1>
<p><%= @article.body %></p>
```

http://localhost:3000/articles/1

`/blog/app/views/articles/index.html.erb`
```
<h1>Articles</h1>

<ul>
  <% @articles.each do |article| %>
    <li>
      <a href="/articles/<%= article.id %>">
        <%= article.title %>
      </a>
    </li>
  <% end %>
</ul>

```

# 