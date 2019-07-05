---
layout: post
title: "jekyll for Windows 멀고도 험한 serve의 길.."
subtitle: "로컬에서 jekyll을 띄울때 마주치는 수 많은 장벽"
date:   2019-06-30 09:01:00 +0900
categories: jekyll
tags: [jekyll, error]
comments: true
---

지킬로 만든 정적블로그의 로컬 빌드는 나같은 루비 초급자에게는 언제나 높은 장벽으로 다가온다. 매번 할 때마다 다르고 새로 적용 해 보려고 해도 다른.. 그리고 도저히 익숙해지지 않는 것 같은 기분이다. 😅 아마도 높은 확률로 나중에 스스로 이 페이지를 찾아 볼 것 같기에 기록으로 남겨 두기로했다.  

아래 나오는 에러내용과 해결방법은 윈도우용 루비 인스톨러 [RubyInstaller for Windows](https://rubyinstaller.org/)를 통해 실행하는 방법이다.

---

**1. 아무튼 뭔가의 에러 내용**  
1차적으로 뭔가 서버에러가 났다면 처음으로 아래 시도를 해보면 좋다.

```HTML
1. 디렉토리의 Gemfile.lock 삭제  
2. jekyll serve -w 재시도
```
---

**2. Gem파일 에러**  
Gem파일을 찾을 수 없다고 한다면  

```ruby
bundle install
# 혹은
gem install [GemName]
```
Gem을 삭제 해야 한다면
```ruby
gem uninstall [GemName] --version [GemVersion]
```
---

**3. 커맨드 창 언어설정 에러**
> Conversion error: Jekyll::Converters::Scss encountered an error while converting 'assets/css/style.scss': Invalid CP949 character "\xE2" on line 5  


아래 명령어로 윈도우 커맨드창의 언어 설정을 utf-8로 바꾸어 주어야 함
```ruby
chcp 65001
```
위 명령어 입력 후 <mark>jekyll serve -w</mark> 재시도  

---

**4. liquid버전 에러**  
> You have already activated liquid 4.0.3, but your Gemfile requires liquid 4.0.0. Prepending `bundle exec` to your com...

```ruby
bundle exec jekyll serve -w
```
---

**5. vendor디렉토리 하위 파일에 대한 에러 메시지**
>  Error: could not read file /Users/.../beautiful-jekyll/vendor/bundle/ruby/2.3.0/gems/jekyll-3.7.4/lib/site_template/_posts/0000-00-00-welcome-to-jekyll.markdown.erb: Invalid date '<%= Time.now.strftime('%Y-%m-%d %H:%M:%S %z') %>': Document 'vendor/bundle/ruby/2.3.0/gems/jekyll-3.7.4/lib/site_template/_posts/0000-00-00-welcome-to-jekyll.markdown.erb' does not have a valid date in the YAML front matter.

<mark>_config.yml</mark> 파일에 `exclude` 항목을 검색한 후 하단에 `vendor/` 를 추가합니다.
``` yml
# Exclude these files from production site
exclude:
  - CHANGELOG.md
  - Gemfile
  - Gemfile.lock
  - LICENSE
  - README.md
  ...
  ...
  - vendor/
```
