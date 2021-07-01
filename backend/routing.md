ルーティング - routing
---
## 一般的な用法
ネットワークで送信相手までの経路を決定すること

## Webアプリケーションフレームワークにおいて
リクエストされたURLとそのURLで行いたい処理を結びつけること

## 実例
### Ruby on Rails
```rb
get '/patients/:id', to: 'patients#show'
```

このとき、 `GET /patients/1`と`PatientsController`の`show`メソッドが呼び出され、引数として`id = 1`が渡る。

参考: https://railsguides.jp/routing.html

Railsの場合では `patients` というキーワードでModel, View, Controllerが自動的に決まるようになっているためこのような書き方ができる。

### Flask
```py
from flask import Flask
app = Flask(__name__)

@app.route('/')
def hello_world():
    return "Hello World!"

if __name__ == '__main__':
    app.run()
```

`@app.route('/')`という[アノテーション](/programming/annotation.md)により、`/`と`hello_world()`が紐づくようになっている。

参考: https://a2c.bitbucket.io/flask/quickstart.html#id2

### Django
プロジェクト名をSite、プロジェクトに含まれるアプリをAppとして
Site/urls.py
```py
from django.contrib import admin
from django.urls import path, include
from .views import HogeView
from . import Fuga

urlpattarn = [
    path('admin/', admin.site.urls),
    # 関数型ビューパターン
    path('', views.hoge, name="hoge"),
    # アプリへの接続
    path('app/', include("App.urls")),
]
```
Site/views.py
```py
from django.shortcuts import HttpResponse

def hoge(request):
    return HttpResponse("Hallo World!!")
```
Site/settings.py
```py
~~
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'App.apps.appConfig',
]

MIDDLEWARE = [
    'django.middleware.security.SecurityMiddleware',
    'django.contrib.sessions.middleware.SessionMiddleware',
    'django.middleware.common.CommonMiddleware',
    'django.middleware.csrf.CsrfViewMiddleware',
    'django.contrib.auth.middleware.AuthenticationMiddleware',
    'django.contrib.messages.middleware.MessageMiddleware',
    'django.middleware.clickjacking.XFrameOptionsMiddleware',
]

ROOT_URLCONF = 'Site.urls'
~~
```
App/urls.py
```py
from django.urls import path
from . import App

urlpattarn = [
    path('admin/', admin.site.urls),
     # クラスベースビューパターン
    path('home', Views.home, name="home"),
]
```
App/views.py
```py
from django.shortcuts import HttpResponse

def home(request):
    return HttpResponse("App Home Page!!")
```
ROOT_URLCONFで指定しているディレクトリ内のurls.pyを第一とする。<br/>
URLを`''`にすると、Site/views.pyの`hoge`が表示される。
INSTALLED_APPSに'App.apps.appConfig'を入力し、Site/urls.pyの`path('app/', include("App.urls"))`によりURLが`app/~`のときはAppのurls.pyに接続される。
例えば、URLを`app/home`とすると、App/views.pyの`home`が呼び出され処理が行われる。

参考: https://docs.djangoproject.com/ja/3.1/intro/tutorial03/
