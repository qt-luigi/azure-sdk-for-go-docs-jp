# Go用のAzure リソース マネージャー パッケージの紹介

`github.com/Azure/azure-sdk-for-go/arm` パッケージはAzure リソース マネージャー (ARM)を使用して操作を実行するために使用されます。
詳細については [Azure リソース マネージャー vs クラシック環境](https://azure.microsoft.com/documentation/articles/resource-manager-deployment-model/) をご覧ください。
Azure サービス管理またはクラシック環境のパッケージは [management](https://github.com/Azure/azure-sdk-for-go/tree/master/management) フォルダーにあります。

## どうやってここに来たのか？

Azureは急速に成長しており、定期的に新しいサービスと機能を追加しています。
急成長はユーザーにとっては良いことですが、SDKでは厳しいです。
新しいサービスと新しい機能ごとに、誰かが詳細を学び、必要なコードをSDKに追加する必要があります。
その結果、[Azure SDK for Go](https://github.com/Azure/azure-sdk-for-go) はAzureよりも遅れています。
それはサービス全体を欠いており、機能を最新に保っていません。
手書きのSDKを維持するには変更が多すぎます。

このため、[Azure SDK for Go](https://github.com/Azure/azure-sdk-for-go) は、Azure リソース マネージャー (ARM) パッケージのリリースで、生成コードモデルに移行しています。
他のAzure SDK、特に [Azure SDK for .NET](https://github.com/Azure/azure-sdk-for-net) は、生成コード戦略をうまく採用しています。
最近、マイクロソフトはこれらのSDKの作成に使用された [AutoRest](https://github.com/Azure/autorest) ツールを公開し、Goのサポートを追加しています。
ARMパッケージはこの新しいツールチェーンを使用して生成された最初のセットです。
AutoRestの入力は [Azure REST API 仕様](https://github.com/Azure/azure-rest-api-specs) で、SwaggerのJSON形式のファイルです。

注意すべき項目がいくつかあります。
ひとつめに、ツールと基になるサポートパッケージの両方が新しいため、本コードはまだ "本番準備完了" ではありません。
これらのパッケージを ***ベータ版*** として扱います。
これはコードを信じていないと言っているわけではなく、公式の最初のリリースに落ち着く前に、他の人が何を考え、何がどれくらいうまくさまざまな環境で動作するかを確認したいためです。
問題を見つけたり提案がある場合は、何を見つけたのかを文書にしてプルリクエストを送ってください。
ただし、コードが生成されるので、プルリクエストを使用してプルリクエスト自体をマージするのではなく、基となるジェネレーターに対して変更した内容を反映します。

ふたつめの注意すべき項目は、生成されたコードをクリーンで信頼できるものにするために、別の新しいパッケージ [go-autorest](https://github.com/Azure/go-autorest) に依存するということです。
SDKの一部ではありますが、バージョン管理をより適切に制御し、俊敏性を維持するためにコードを分離しました。
[go-autorest](https://github.com/Azure/go-autorest) は手作業で作成されているため、他のリポジトリーと同じ方法でプルリクエストを受け取ります。

これらのパッケージが "本番準備完了" になるまで急速に改善するつもりです。
そのため、これらを試してみて、私たちにあなたの考えを伝えてください。

## 私たちは何をしたのか？

新しいフレームワークを作成するのは難しく、しばしば "崖" に導かれます:
コードは、特殊なケースや調整が行われるまでは使いやすく、その後は行き詰まってしまいます。
多くの場合、要件のわずかな違いは、コードをフォークし、多くの時間を費やすことにつながります。
崖は生成されたコードでさらに頻繁に発生します。
私たちはそれらを回避することを望み、新しいモデルはそうであると信じています。
私たちの最初の目標は:

* 簡単に使用できる。 簡単に使用するためには "clone したら go" でなければなりません。
* 複雑なケースの大多数を処理するための簡単な構成。
* 既存のフレームワークとの統合が簡単で、チャンネルにうまくフィットし、ファンアウト/ファンインの設定をサポートしている。

これらは一連の例で最もよく示されていて、すべては [examples](https://github.com/Azure/azure-sdk-for-go/blob/master/arm/examples) サブフォルダーに含まれています。

## SDKはどのようにテストされているのか？

SDKのテストは現在進行中の作業です。 それには3つの異なる点があります:

* API自体に対して [Azure REST API 仕様](https://github.com/Azure/azure-rest-api-specs) をテストします。 この方法で仕様がAPIの動作に正しく反映しているかどうかを見つけることができます。 すべてのAzure SDKはこのテストの恩恵を受けることができます。
* AutoRestに [受け入れテスト](https://github.com/Azure/autorest/blob/master/docs/developer/guide/writing-tests.md) を追加します。
* 生成されたSDKをコードサンプルでテストします。 これは以前のテストを逃れたバグを捕まえ、いくつかのドキュメントを提供します。

## 注記: 認証とAzure リソース マネージャー

Azure リソース マネージャー パッケージを使用する前に、リクエストを認証および承認する方法を理解する必要があります。
Azure リソース マネージャーのリクエストは、[OAuth2](http://oauth.net) を通じて承認されます。
OAuth2は証明書よりも多くの利点を提供しますが、ヘッドレスサーバーのスクリプトなどのプログラムによる使用には、1つまたは複数の*サービス プリンシパル*を理解して作成する必要があります。

Azure-SDK-for-Nodeには、どちらもGoに適用可能である、ポータルにサービス プリンシパルを作成する方法と、Azure CLIを使用する方法に関する説明が含まれている優れたチュートリアルがあります。
そのドキュメントをここで見つけてください: [Authenticaion, Azure/azure-sdk-for-node](https://github.com/Azure/azure-sdk-for-node/blob/master/Documentation/Authentication.md)

さらに、これが何を意味するのかを記述した
[サービスプリンシパルを使用してCIサーバーでAzureを自動化する](http://blog.davidebbo.com/2014/12/azure-service-principal.html)
や
[Microsoft Azure REST API + OAuth 2.0](https://ahmetalpbalkan.com/blog/azure-rest-api-with-oauth2/)
など、いくつかの優れたブログ記事があります。
サービス プリンシパルの作成と認可の詳細については、MSDNの記事
[Azure API 管理 REST API 認証](https://msdn.microsoft.com/library/azure/5b13010a-d202-4af5-aabf-7ebc26800b3d)
や
[Azure ポータルを使用して新しいAzure サービス プリンシパルを作成する](https://azure.microsoft.com/documentation/articles/resource-group-create-service-principal-portal/)
を参照してください。
Azure Active Directoryのシニア プログラム マネージャーであるDushyant Gillは
[Azure リソース マネージャー APIで認証するための開発者ガイド](http://www.dushyantgill.com/blog/2015/05/23/developers-guide-to-auth-with-azure-resource-manager-api/)
という幅広いブログ記事を書いていて、これもまた非常に有用です。

### 完全なソースコード

[証明書またはデバイス認証を経由してAzureに認証する](https://github.com/Azure/go-autorest/tree/master/autorest/azure/example) の完全な例のコードを入手してください。

## 簡単な例: Azure ストレージ内の名前の可用性を確認する

[Azure Storage](http://azure.microsoft.com/documentation/services/storage/)
や
[Azure Compute](https://azure.microsoft.com/documentation/services/virtual-machines/)
などの各ARMプロバイダーには、独自のパッケージがあります。
まず、必要なプロバイダーのパッケージをインポートします。
次に、ほとんどのパッケージは、名前の衝突を避けて使いやすさを向上させるために、複数のクライアント間でAPIを分割します。
たとえば、
[Azure Storage](http://azure.microsoft.com/documentation/services/storage/)
パッケージには
[storage.AccountsClient](https://godoc.org/github.com/Azure/azure-sdk-for-go/arm/storage#AccountsClient)
と
[storage.UsageOperationsClient](https://godoc.org/github.com/Azure/azure-sdk-for-go/arm/storage#UsageOperationsClient)
の2つのクライアントがあります。
名前が使用可能かどうかを確認するには、
[storage.AccountsClient](https://godoc.org/github.com/Azure/azure-sdk-for-go/arm/storage#AccountsClient).
を使用します。

各ARMクライアントは [autorest.Client](https://godoc.org/github.com/Azure/go-autorest/autorest#Client) で構成されます。
[autorest.Client](https://godoc.org/github.com/Azure/go-autorest/autorest#Client) を使用すると、
[go-autorest](https://github.com/Azure/go-autorest) のデコレーター パターンを利用してAPI呼び出しの動作を変更できます。
たとえば、上記のコードでは、
[azure.ServicePrincipalToken](https://godoc.org/github.com/Azure/go-autorest/autorest/azure#ServicePrincipalToken)
には、OAuth2 認証 トークンをリクエストに適用する
[WithAuthorization](https://godoc.org/github.com/Azure/go-autorest/autorest#Client.WithAuthorization)
[autorest.PrepareDecorator](https://godoc.org/github.com/Azure/go-autorest/autorest#PrepareDecorator)
が含まれています。
必要に応じて、提供された資格情報を使用してトークンをリフレッシュします。

デコレートされた
[autorest.Sender](https://godoc.org/github.com/Azure/go-autorest/autorest#Sender)
を提供するか、
[autorest.Client](https://godoc.org/github.com/Azure/go-autorest/autorest#Client)
にカスタムの
[autorest.PrepareDecorator](https://godoc.org/github.com/Azure/go-autorest/autorest#PrepareDecorator)
または
[autorest.RespondDecorator](https://godoc.org/github.com/Azure/go-autorest/autorest#RespondDecorator)
を設定することで、より多くの制御が可能になります。
詳細については、付属のサンプルファイル
[check.go](https://github.com/Azure/azure-sdk-for-go/blob/master/arm/examples/check/check.go)
を参照してください。
これらを介することで、発信要求を修正したり、着信応答を検査したり、予期しない待ち時間からサービスを保護する
[サーキット ブレーカー](https://msdn.microsoft.com/library/dn589784.aspx)
を提供することさえできます。

最後に、すべてのAzure ARM API呼び出しは
[autorest.DetailedError](https://godoc.org/github.com/Azure/go-autorest/autorest#DetailedError)
のインスタンスを返します。
DetailedErrorはオリジナルの
[error](http://golang.org/ref/spec#Errors)
への匿名アクセスを提供するだけでなく、パッケージタイプ（
[storage.AccountsClient](https://godoc.org/github.com/Azure/azure-sdk-for-go/arm/storage#AccountsClient)
など）、失敗したメソッド（
[CheckNameAvailability](https://godoc.org/github.com/Azure/azure-sdk-for-go/arm/storage#AccountsClient.CheckNameAvailability)
など）、詳細なエラーメッセージを提供します。

### 完全なソースコード

この例の完全なソースコードは [check.go](https://github.com/Azure/azure-sdk-for-go/blob/master/arm/examples/check/check.go) で見つけられます。

1. [サービス プリンシパル](https://azure.microsoft.com/documentation/articles/resource-group-authenticate-service-principal-cli/) を作成します。 [認証](#first-a-sidenote-authentication-and-the-azure-resource-manager) にはテナントID、クライアントID、クライアント シークレットが必要で、それらを取得したらすぐに保持してください。
2. 以下に記載されたいずれかの方法を使用してあなたのAzure サブスクリプションIDを取得してください:
  - サブスクリプション セクションの [ポータル](portal.azure.com) を通じて取得する。
  - [Azure CLI](https://azure.microsoft.com/documentation/articles/xplat-cli-install/) でコマンド `azure account show` を使用して取得する。
  - [Azure Powershell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/) でコマンドレット `Get-AzureRmSubscription` を使用して取得する。
3. 環境変数 `AZURE_TENANT_ID = <TENANT_ID>`、`AZURE_CLIENT_ID = <CLIENT_ID>`、`AZURE_CLIENT_SECRET = <CLIENT_SECRET>` および `AZURE_SUBSCRIPTION_ID = <SUBSCRIPTION_ID>` を設定します。
4. 次のコマンドでサンプルを実行します:

```
$ cd arm/examples/check
$ go run check.go
```

## より複雑なもの: 新しいAzure ストレージ アカウントを作成する

ローカルおよびリージョン間の冗長性、およびサービスの負荷はサービスの応答性に影響します。
任意のAPI呼び出しはリクエストを完了する前に返されます。
Azure ARM API呼び出しは、HTTP ステータスコード '202 Accepted' を返すことで、リクエストが不完全である（何らかの理由でリクエストが失敗したのに対して）ことを示します。
すべてのAzure ARMクライアントに組み込まれた
[autorest.Client](https://godoc.org/github.com/Azure/go-autorest/autorest#Client)
は、基本的なリクエスト ポーリングをサポートします。
デフォルトでは、指定された期間が経過するまでポーリングを行います（レスポンスの
HTTP [Retry-After](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.37)
ヘッダーで指定されたポーリング頻度で）。
[autorest.Client](https://godoc.org/github.com/Azure/go-autorest/autorest#Client)
の設定を変更することで、固定数をポーリングするか、まったくポーリングしないようにすることができます。

ポーリングするかどうかにかかわらず、すべてのAzure ARMクライアントのレスポンスは、
[autorest.Response](https://godoc.org/github.com/Azure/go-autorest/autorest#Response)
のインスタンスで構成されます。
現在のところ、
[autorest.Response](https://godoc.org/github.com/Azure/go-autorest/autorest#Response)
は、標準の
[http.Response](https://golang.org/pkg/net/http/#Response)
オブジェクト（より多くの機能を実装するにつれて変更される可能性があります）に対してのみ構成されます。
コードがAzure ARM API呼び出しからエラーを受け取った時、返された
[autorest.Response](https://godoc.org/github.com/Azure/go-autorest/autorest#Response)
に含まれているHTTP ステータスコードを調べると便利です。
たとえば、HTTP 202の場合は、
[GetPollingLocation](https://godoc.org/github.com/Azure/go-autorest/autorest#Response.GetPollingLocation)
レスポンス メソッドを使用してポーリングを続行するURLを抽出できます。
同様に、
[GetPollingDelay](https://godoc.org/github.com/Azure/go-autorest/autorest#Response.GetPollingDelay)
レスポンス メソッドは、
[time.Duration](http://golang.org/pkg/time/#Duration)
として、サービスが提案した最小ポーリング遅延を返します。

新しいAzure ストレージ アカウントを作成することは、これらの概念を理解するのに簡単な方法です。

[storage.AccountsClient](https://godoc.org/github.com/Azure/azure-sdk-for-go/arm/storage#AccountsClient)
の
[autorest.Client](https://godoc.org/github.com/Azure/go-autorest/autorest#Client)
部分は、設定された期間（デフォルト）のポーリングに対して一定数の試行でポーリングします。
ストレージ アカウントの作成中にエラーが発生した場合、コードはHTTP ステータスコードを検査し、ポーリングのために
[Azure Storage](http://azure.microsoft.com/documentation/services/storage/)
サービスが返したURLを出力します。

### 例の完全なソース

作成されたアカウントの削除を含む詳細は、サンプルコードファイルの [create.go](https://github.com/Azure/azure-sdk-for-go/blob/master/arm/examples/create/create.go) にあります。

1. [サービス プリンシパル](https://azure.microsoft.com/documentation/articles/resource-group-authenticate-service-principal-cli/) を作成します。 [認証](#first-a-sidenote-authentication-and-the-azure-resource-manager) にはテナントID、クライアントID、クライアント シークレットが必要で、それらを取得したらすぐに保持してください。
2. 以下に記載されたいずれかの方法を使用してあなたのAzureサブスクリプションIDを取得してください:
  - サブスクリプション セクションの [ポータル](portal.azure.com) を通じて取得する。
  - [Azure CLI](https://azure.microsoft.com/documentation/articles/xplat-cli-install/) でコマンド `azure account show` を使用して取得する。
  - [Azure Powershell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/) でコマンドレット `Get-AzureRmSubscription` を使用して取得する。
3. 環境変数 `AZURE_TENANT_ID = <TENANT_ID>`、`AZURE_CLIENT_ID = <CLIENT_ID>`、`AZURE_CLIENT_SECRET = <CLIENT_SECRET>` および `AZURE_SUBSCRIPTION_ID = <SUBSCRIPTION_ID>` を設定します。
4. リソース グループを作成し、main関数の最初の行にその名前を追加します。
5. 次のコマンドでサンプルを実行します:

```
$ cd arm/examples/create
$ go run create.go
```


## 非同期リクエストの作成

Goの多くの強みの1つは、ゴルーチンを用いて非同期リクエストを送信および管理することがどれほど自然なのかです。
ARMパッケージには、Goコードで使用されるさまざまな非同期パターンに自然に適合することを望んでいましたが、単純なユースケースでは簡単に使用できます。
私たちは、すべてのAPIにパターンを適用することで両方を達成しました。
各パッケージ APIには（少なくとも）4つのメソッドが含まれます（APIがページされた結果セットを返す場合はさらに多く）。
たとえば、`Foo` という名前のAPI呼び出しの場合、パッケージは次のように定義します:

- `FooPreparer`: このメソッドは、APIの引数を受け取り、準備された `http.Request` を返します。
- `FooSender`: このメソッドは、準備された `http.Request` を送信します。 可能なステータスコードを処理し、[autorest.Client](https://godoc.org/github.com/Azure/go-autorest/autorest#Client) で無効にされていない限り、ポーリングを処理します。
- `FooResponder`: このメソッドは、送信者によって返された `http.Response` を受け取って処理し、もしあればJSONを結果に非整列化します。
- `Foo`: このメソッドはAPIの引数を受け取り、その結果を返します。`FooPreparer`、` FooSender`、および `FooResponder` のラッパーです。

preparer、sender、およびresponderメソッドを使用することにより、パッケージ ユーザーは必要に応じてゴルーチン間でリクエストとレスポンスの処理を分散できます。
さらに、キャンセル チャネルを `http.Response` に追加すると（
[PrepareDecorator](https://godoc.org/github.com/Azure/go-autorest/autorest#PrepareDecorator)
を通じてより簡単に）、送信されたリクエストをキャンセルすることができます（詳細については
[http.Request](https://golang.org/pkg/net/http/#Request)
のドキュメントを参照）。

## ページされた結果セット

一部のAPI呼び出しは部分的な結果を返します。 通常、そうする時、結果構造は `Value` 配列と `NextLink` URLを含みます。
`NextLink` URLは、次のページまたは結果のブロックを取得するために使用されます。

パッケージには、ページされた結果を自然に処理して取得するための2つのメソッドが追加されています。
はじめに、ページされた結果構造上のパッケージは、次の結果セットのための `http.Request` を返すpreparerメソッドを含みます。
`FooResults` という名前の構造体に返される結果セットに対して、パッケージには `FooResultsPreparer` という名前のメソッドが含まれます。
`NextLink` が `nil` または空の場合、メソッドは `nil` を返します。

対応するAPI（通常、名前に "List" が含まれる）には、結果セットが与えられたときに次の結果セットを取得するのを容易にするメソッドがあります。
たとえば、`FooList` という名前のAPIでは、パッケージには最後の呼び出しの結果を受け取って、次のセットを返す `FooListNextResults` が含まれます。

## 要約

Azure SDK for Goの新しいAzure リソース マネージャー パッケージは、Azureの急速な成長に伴ってSDKを最新の状態に保つための大きな一歩です。
前述したように、私たちは本番で使用できるようにこれらのパッケージを迅速に安定させるつもりです。
また、
[Azure Resource Manager Templates](https://msdn.microsoft.com/library/azure/dn790568.aspx)
と他のプロバイダーのハイライトを含んでいる、いくつかの例を追加します。

そのため、パッケージを試してみて、さまざまなARMプロバイダーを探索して、あなたの考えを伝えてください。

あなたからの声をお待ちしています！

## ライセンス

Azure SDK for GoのLICENSEファイルを参照してください。
