# Azure サービス管理 パッケージ for Go

`github.com/Azure/azure-sdk-for-go/management` パッケージは、Azure サービス管理 (ASM) というクラシック デプロイ モデルを使用して操作を実行するために使われます。
詳細については [Azure リソース マネージャー と クラシック デプロイ](https://azure.microsoft.com/documentation/articles/resource-manager-deployment-model/) をご覧ください。
Azure リソース マネージャーのパッケージは [arm](https://github.com/Azure/azure-sdk-for-go/blob/master/arm) フォルダーにあります。

## 注記: 認証とAzure サービス管理

クライアントは現在、証明書またはAzure `.publishSettings` ファイルを使用したサービス管理 APIへの認証をサポートしています。
サブスクリプションの `.publishSettings` ファイルを [ここ](https://manage.windowsazure.com/publishsettings) からダウンロードできます。

### 例: Linux仮想マシンを作成する

この例の完全なソースコードは [example.go](https://github.com/Azure/azure-sdk-for-go/blob/master/management/examples/example.go) にあります。
この例を試すには、[.publishSettings をダウンロード](https://manage.windowsazure.com/publishsettings) し、そのパスをmain関数の最初の行に追加します。
次のコマンドでこの例を実行します。

```
$ cd management/examples
$ go run example.go
```
