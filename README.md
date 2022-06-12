# cosmosdb

## コンテナ起動

```
docker compose up -d
```

## 証明書のインストール
1. エミュレーターが実行中になったら、別のターミナルを使用してローカル コンピューターの IP アドレスを変数に読み込みます。
```
ipaddr="`ifconfig | grep "inet " | grep -Fv 127.0.0.1 | awk '{print $2}' | head -n 1`"
```
2. 次に、エミュレーターの証明書をダウンロードします。
```
curl -k https://$ipaddr:8081/_explorer/emulator.pem > emulatorcert.crt
```

## UI を介してエンドポイントを使用する
エミュレーターは、そのエンドポイントへの接続をセキュリティで保護するために自己署名証明書を使用しており、手動で信頼する必要があります。 目的の Web ブラウザーを使用して UI を介してエンドポイントを使用するには、次の手順を使用します。

1. エミュレーターの自己署名証明書がダウンロードされていることを確認してください。  
```
curl -k https://$ipaddr:8081/_explorer/emulator.pem > emulatorcert.crt
```
2. Mac で キーチェーン アクセス アプリを開き、エミュレーター証明書をインポートします。
3. [File] 、 [Import Items] の順に選択し、emulatorcert.crt をインポートします。
4. emulatorcert.crt がキーチェーンに読み込まれたら、localhost 名をダブルクリックし、信頼設定を [Always Trust] に変更します。
5. これで、https://localhost:8081/_explorer/index.html または https://{your_local_ip}:8081/_explorer/index.html を参照して、エミュレーターへの接続文字列を取得できます。

### 参考サイト
* [docker-compose と docker サブコマンドの compose って結局どっち使えばいいのかという話](https://keyno63.hatenablog.com/entry/2021/07/24/231528)
* [ローカルでの開発とテストのために Azure Cosmos DB Emulator をインストールして使用する](https://docs.microsoft.com/ja-jp/azure/cosmos-db/local-emulator?tabs=ssl-netstd21)
* [Docker for Linux 上でエミュレーターを実行する](https://docs.microsoft.com/ja-jp/azure/cosmos-db/linux-emulator?tabs=ssl-netstd21)
* [Azure Cosmos DB Emulator がついに Linux 版に対応したので早速試してみた](https://zenn.dev/ymasaoka/articles/get-started-with-cosmosdb-linux-emulator)
