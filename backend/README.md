backend - サーバサイドアプリケーション, mBaaS等
--
## Webアプリケーションフレームワーク
### 共通
- [ルーティング](routing.md)
- [マイグレーション](migration.md)

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


## バッチスクリプト

## mBaaS
- [Firebase](firebase/README.md)
