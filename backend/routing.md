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