backend - サーバサイドアプリケーション, mBaaS等
--
## Webアプリケーションフレームワーク
### 共通
- [ルーティング](routing.md)
- [マイグレーション](migration.md)

## API
「Application Programming Interface」の略。
従来は、APIといえばOSがアプリケーションソフト向けに提供していた機能を指していたが、
現在はWebサービスがアプリ開発者向けに公開している機能を **Web API** と呼んでいるほか、
気象情報、グルメ紹介、テレビ番組表、交通データ、観光情報などのさまざまなAPIがある。


### APIの例(銀行口座に入金する場合)
- 銀行口座へのアクセスを許可する認可機能
- 現在残高の確認機能
- 入金額と現在残高を合算する機能
- 合算後の残高を表示する機能


## gRPC
### gRPCについて比較しながら理解してみる
[Data Streaming via GRPC vs MQTT vs](https://medium.com/@msmechatronics/data-streaming-via-grpc-vs-mqtt-vs-5c30dd205193)

HTTP1.1とHTTP2の比較

![https://miro.medium.com/max/1400/1*SXr17zrmh5Lpya6OFZpuTA.png](https://miro.medium.com/max/1400/1*SXr17zrmh5Lpya6OFZpuTA.png)

MQTT, Websocket, gRPCのパフォーマンス比較

![https://miro.medium.com/max/1312/1*WD0PmKxTh5n0TcUAVetLPw.png](https://miro.medium.com/max/1312/1*WD0PmKxTh5n0TcUAVetLPw.png)


## gRPCでのエラーレスポンスについて
### 参考文献

[gRPC status codeの一覧 - Qiita](https://qiita.com/Hiraku/items/0549e4cf7079d22b27e8)

[gRPCでエラー詳細を渡す方法 - Carpe Diem](https://christina04.hatenablog.com/entry/grpc-error-details)


### gRPC→HTTP 対応表
[gRPC→HTTP 対応表](https://www.notion.so/0c094f31f9254f59829b539c52a660a0)


- gRPCの標準エラー＝エラーコード＋エラーメッセージ

## エラー詳細情報を追加したい場合

[errdetails - GoDoc](https://godoc.org/google.golang.org/genproto/googleapis/rpc/errdetails)

```go
st := status.New(codes.InvalidArgument, "some error occurred")
v := &errdetails.BadRequest{
        FieldViolations: []*errdetails.BadRequest_FieldViolation{
                {
                        Field:       "username",
                        Description: "should not empty",
                },
        },
}
dt, _ := st.WithDetails(v)
return nil, dt.Err()
```

```go
st := status.New(dataflowError.ErrorCode, "some error occurred")
errResJP := &errdetails.LocalizedMessage{
	Locale:  "ja-JP",
	Message: dataflowError.ErrorMessageJP,
}
errResEN := &errdetails.LocalizedMessage{
	Locale:  "en-US",
	Message: dataflowError.ErrorMessageEN,
}
detailsErr, _ := st.WithDetails(errResJP, errResEN)
```

#### web APIの例
- GoogleMapsのMap表示
- Amazonの売れ筋や価格の表示
- TwitterやFacebookなどのSNSの投稿記事との連携

## バッチスクリプト

## mBaaS
- [Firebase](firebase/README.md)
