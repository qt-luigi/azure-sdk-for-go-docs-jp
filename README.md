# 本リポジトリーについて

[Azure/azure-sdk-for-go](https://github.com/Azure/azure-sdk-for-go) のドキュメントを日本語に翻訳してみました。
Google翻訳を使用して翻訳した後に自分でチェックして修正しています。
翻訳時のバージョンは [v43.0.0](https://github.com/Azure/azure-sdk-for-go/tree/v43.0.0) です。

# Azure SDK for Go

[![godoc](https://godoc.org/github.com/Azure/azure-sdk-for-go?status.svg)](https://godoc.org/github.com/Azure/azure-sdk-for-go)

[![Build Status](https://travis-ci.org/Azure/azure-sdk-for-go.svg?branch=master)](https://travis-ci.org/Azure/azure-sdk-for-go)

[![Build Status](https://dev.azure.com/azure-sdk/public/_apis/build/status/go/Azure.azure-sdk-for-go?branchName=latest)](https://dev.azure.com/azure-sdk/public/_build/latest?definitionId=640&branchName=latest)

[![Go Report Card](https://goreportcard.com/badge/github.com/Azure/azure-sdk-for-go)](https://goreportcard.com/report/github.com/Azure/azure-sdk-for-go)

azure-sdk-for-goは、Azureサービスを管理および使用するためのGoパッケージを提供します。
Goの直近の2つのメジャーリリースを正式にサポートしています。
Goの古いバージョンは、SDKの外部依存関係の変更により動作しなくなるまで、CIで実行され続けます。
GoのバージョンがCIから削除されると、CHANGELOGが更新されます。

更新と変更について通知を受けるには、 [Azure更新フィード](https://azure.microsoft.com/updates/) を購読してください。

ユーザーは、 [github.com/Azure-Samples/azure-sdk-for-go-samples][samples_repo] にあるサンプルリポジトリーに直接ジャンプすることをお勧めします。

質問やフィードバックがありますか？
[Gophers Slack](https://gophers.slack.com/) の **[#Azure SDK チャンネル](https://gophers.slack.com/messages/CA7HK8EEP)** でチャットしてください。
必要に応じて、まず [ここ](https://invite.slack.golangbridge.org) でサインアップしてください。

## パッケージの更新

SDKのほとんどのパッケージは、 [Azure/autorest.go][] および [Azure/autorest][] を使用して [Azure API 仕様][azure_rest_specs] から生成されます。
これらの生成されたパッケージは、 [Azure/go-autorest][] に実装されたHTTPクライアントに依存します。

[azure_rest_specs]: https://github.com/Azure/azure-rest-api-specs
[azure/autorest]: https://github.com/Azure/autorest
[azure/autorest.go]: https://github.com/Azure/autorest.go
[azure/go-autorest]: https://github.com/Azure/go-autorest

SDKコードベースは [セマンティックバージョニング](https://semver.org) に準拠しているため、メジャー (x.0.0) リリース以外での破壊的な変更を回避できます。
AzureのAPIは頻繁に更新されるため、**毎月末に** 完全な変更ログを含む **新しいメジャーバージョン** をリリースします。
詳細と背景については、 [SDK Update Practices](https://github.com/Azure/azure-sdk-for-go/wiki/SDK-Update-Practices) をご覧ください。

アプリケーションでAzure SDKなどの依存関係をより確実に管理するには、 [golang/dep](https://github.com/golang/dep) をお勧めします。

未だパブリックプレビューのパッケージは、 `./services/preview` ディレクトリーにあります。
これらのパッケージはプレビュー段階にあるため、メジャーバージョンの更新以外での破壊的な変更を含む変更がなされる可能性があることに注意してください。

## その他のAzure Goパッケージ

次に示すように、AzureにはGoでサービスを使用するための他のいくつかのパッケージが用意されています。
必要なパッケージが利用できない場合は、イシューを開いてお知らせください。

| サービス             | インポート パス/リポジトリー                                                                       |
| -------------------- | -------------------------------------------------------------------------------------------------- |
| Storage - Blobs      | [github.com/Azure/azure-storage-blob-go](https://github.com/Azure/azure-storage-blob-go)           |
| Storage - Files      | [github.com/Azure/azure-storage-file-go](https://github.com/Azure/azure-storage-file-go)           |
| Storage - Queues     | [github.com/Azure/azure-storage-queue-go](https://github.com/Azure/azure-storage-queue-go)         |
| Service Bus          | [github.com/Azure/azure-service-bus-go](https://github.com/Azure/azure-service-bus-go)             |
| Event Hubs           | [github.com/Azure/azure-event-hubs-go](https://github.com/Azure/azure-event-hubs-go)               |
| Application Insights | [github.com/Microsoft/ApplicationInsights-go](https://github.com/Microsoft/ApplicationInsights-go) |

# インストールと使用:

## インストール

```sh
$ go get -u github.com/Azure/azure-sdk-for-go/...
```

および、`Gopkg.toml` ファイルで指定されている [`go-autorest`](https://github.com/Azure/go-autorest) の最小バージョンを含めるようにしてください。

また、depを使用する場合は、リポジトリー内で次のように実行します:

```sh
$ dep ensure -add github.com/Azure/azure-sdk-for-go
```

Goをインストールする必要がある場合は、 [公式の指示](https://golang.org/dl/) に従ってください。

## 使用

さらに多くのシナリオと例については、 [Azure-Samples/azure-sdk-for-go-samples][samples_repo] を参照してください。

このリポジトリーでパッケージを使用するには、次の一般的な手順を適用します。
認証と `Authorizer` インターフェースの詳細については、 [次のセクション](#authentication) を参照してください。

1. [services][services_dir] ディレクトリーからパッケージをインポートします。
2. `New*Client` 関数を使用してクライアントを作成および認証します。
   `c := compute.NewVirtualMachinesClient(...)`
3. クライアントを使用してAPIメソッドを呼び出します。
   `res, err := c.CreateOrUpdate(...)`
4. レスポンスとエラーを処理します。

[services_dir]: https://github.com/Azure/azure-sdk-for-go/tree/master/services

たとえば、新しい仮想ネットワークを作成するには (山括弧内の文字列を独自の値に置き換えます):

```go
package main

import (
	"context"

	"github.com/Azure/azure-sdk-for-go/services/network/mgmt/2017-09-01/network"

	"github.com/Azure/go-autorest/autorest/azure/auth"
	"github.com/Azure/go-autorest/autorest/to"
)

func main() {
	// create a VirtualNetworks client
	vnetClient := network.NewVirtualNetworksClient("<subscriptionID>")

	// create an authorizer from env vars or Azure Managed Service Idenity
	authorizer, err := auth.NewAuthorizerFromEnvironment()
	if err == nil {
		vnetClient.Authorizer = authorizer
	}

	// call the VirtualNetworks CreateOrUpdate API
	vnetClient.CreateOrUpdate(context.Background(),
		"<resourceGroupName>",
		"<vnetName>",
		network.VirtualNetwork{
			Location: to.StringPtr("<azureRegion>"),
			VirtualNetworkPropertiesFormat: &network.VirtualNetworkPropertiesFormat{
				AddressSpace: &network.AddressSpace{
					AddressPrefixes: &[]string{"10.0.0.0/8"},
				},
				Subnets: &[]network.Subnet{
					{
						Name: to.StringPtr("<subnet1Name>"),
						SubnetPropertiesFormat: &network.SubnetPropertiesFormat{
							AddressPrefix: to.StringPtr("10.0.0.0/16"),
						},
					},
					{
						Name: to.StringPtr("<subnet2Name>"),
						SubnetPropertiesFormat: &network.SubnetPropertiesFormat{
							AddressPrefix: to.StringPtr("10.1.0.0/16"),
						},
					},
				},
			},
		})
}
```

## 認証

一般的なSDK操作は、認証および承認される必要があります。
_Authorizer_ インターフェースでは、Azure ADから受信したOAuth2 Authorizationヘッダーとbearerトークンの挿入など、リクエストで任意の認証スタイルを使用できます。

SDK自体は、最初に環境変数のOAuthクライアント資格情報を確認し、Azure VMの場合は、利用可能な場合はAzureの [マネージドサービスID]() にフォールバックするauthorizerを取得する簡単な方法を提供します。
[前のセクション](#use) の次のスニペットは、このヘルパーを示しています。

```go
import "github.com/Azure/go-autorest/autorest/azure/auth"

// create a VirtualNetworks client
vnetClient := network.NewVirtualNetworksClient("<subscriptionID>")

// create an authorizer from env vars or Azure Managed Service Idenity
authorizer, err := auth.NewAuthorizerFromEnvironment()
if err == nil {
    vnetClient.Authorizer = authorizer
}

// call the VirtualNetworks CreateOrUpdate API
vnetClient.CreateOrUpdate(context.Background(),
// ...
```

次の環境変数は、認証構成の決定に役立ちます:

- `AZURE_ENVIRONMENT`: 使用するAzure環境を指定します。
  設定されていない場合、デフォルトで `AzurePublicCloud` になります。
  マネージドサービスID (MSI) による認証には適用されません。

- `AZURE_AD_RESOURCE`: 使用するAADリソースIDを指定します。
  設定されていない場合、Azureリソースマネージャーでの操作の場合、デフォルトで `ResourceManagerEndpoint` になります。
  `auth.NewAuthorizerFromEnvironmentWithResource(resource string)` を使用して、プログラムで代替リソースを選択することもできます。

### 認証の詳細

前者は、サービスプリンシパルと [AzureマネージドサービスID][] の両方をシームレスに使用できるため、SDKが提供するいくつかの認証オプションの最初で最も推奨されるものです。
その他のオプションを以下に示します。

> 注: 新しいサービスプリンシパルを作成する必要がある場合は、 [azure-cli](https://github.com/Azure/azure-cli) で `az ad sp create-for-rbac -n "<app_name>"` を実行します。 
> 詳細については、 [これらのドキュメント](https://docs.microsoft.com/cli/azure/create-an-azure-service-principal-azure-cli?view=azure-cli-latest) を参照してください。
> アプリで使用するために新しいプリンシパルのID、シークレット、テナントIDをコピーするか、シリアライズされた出力の `--sdk-auth` パラメーターを検討してください。

[AzureマネージドサービスID]: https://docs.microsoft.com/en-us/azure/active-directory/msi-overview

- 上記の `auth.NewAuthorizerFromEnvironment()` は、次の構成で最初に利用可能なものからauthorizerを作成します。

      1. **クライアント資格情報**: Azure ADアプリケーションIDとシークレット。

          - `AZURE_TENANT_ID`: 認証するテナントを指定します。
          - `AZURE_CLIENT_ID`: 使用するアプリクライアントIDを指定します。
          - `AZURE_CLIENT_SECRET`: 使用するアプリシークレットを指定します。

  	  2. **クライアント証明書**: Azure ADアプリケーションIDとX.509証明書。

          - `AZURE_TENANT_ID`: 認証するテナントを指定します。
          - `AZURE_CLIENT_ID`: 使用するアプリクライアントIDを指定します。
          - `AZURE_CERTIFICATE_PATH`: 使用する証明書パスを指定します。
          - `AZURE_CERTIFICATE_PASSWORD`: 使用する証明書パスワードを指定します。

      3. **リソース所有者のパスワード**: Azure ADのユーザーとパスワード。
         この付与タイプは *非推奨* なので、対話型ログインが必要な場合は、代わりにデバイスログインを使用してください。

          - `AZURE_TENANT_ID`: 認証するテナントを指定します。
          - `AZURE_CLIENT_ID`: 使用するアプリクライアントIDを指定します。
          - `AZURE_USERNAME`: 使用するユーザー名を指定します。
          - `AZURE_PASSWORD`: 使用するパスワードを指定します。

      4. **AzureマネージドサービスID**: 資格情報管理をプラットフォームに委任します。
         VM上では、コードがAzureで実行されている必要があります。
		     すべての構成はAzureによって処理されます。
		     詳細については、[AzureマネージドサービスID](https://docs.microsoft.com/en-us/azure/active-directory/msi-overview) を参照してください。

- `auth.NewAuthorizerFromFile()` メソッドは、 [Azure CLI][] によって作成された認証ファイルの資格情報を使用してauthorizerを作成します。
  以下の手順に従って利用してください。

  1. サービスプリンシパルを作成し、 `az ad sp create-for-rbac --sdk-auth > client_credentials.json` を使用して認証ファイルを出力します。
  2. 環境変数 `AZURE_AUTH_LOCATION` に、保存された出力ファイルのパスを設定します。
  3. 上記のように、クライアントで `auth.NewAuthorizerFromFile()` によって返されたauthorizerを使用します。

- `auth.NewAuthorizerFromCLI()` メソッドは、 [Azure CLI][] を使用して認証情報を取得するauthorizerを作成します。
  この方法を使用するには、次の手順に従います:

  1. [Azure CLI v2.0.12](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) 以降をインストールします。
     以前のバージョンをアップグレードします。
  2. `az login` を使用してAzureにサインインします。

  エラーが発生した場合は、 `az account get-access-token` を使用してアクセスを確認してください。

  Azure CLIがデフォルトディレクトーリにインストールされていない場合、 `az` が見つからないことを報告するエラーが発生することがあります。
  `AzureCLIPath` 環境変数を使用して、Azure CLIインストールフォルダーを定義します。

  複数のアカウントを使用してAzure CLIにサインインしている場合、またはアカウントが複数のサブスクリプションにアクセスできる場合は、使用する特定のサブスクリプションを指定する必要があります。
  これを行うには、以下を使用します:

  ```
  az account set --subscription <subscription-id>
  ```

  現在のアカウント設定を確認するには、次を使用します:

  ```
  az account list
  ```

[azure cli]: https://github.com/Azure/azure-cli

- 最後に、 `auth.NewDeviceFlowConfig()` を呼び出してauthorizerを次のように抽出することにより、OAuthの [デバイスフロー][] を使用できます:

  ```go
  config := auth.NewDeviceFlowConfig(clientID, tenantID)
  a, err := config.Authorizer()
  ```

[デバイスフロー]: https://oauth.net/2/device-flow/

# バージョン管理

azure-sdk-for-goは、すべてのAzure APIに少なくとも基本的なGoバインディングを提供します。
ユーザーに最大限の柔軟性を提供するために、SDKには、まだ使用されている以前のバージョンのAzure APIも含まれています。
これにより、最新版のAzureデータセンター、以前のAPIを備えたリージョンデータセンター、さらにはAzure Stackのオンプレミスインストールのユーザーをサポートできます。

**SDKバージョン** はグローバルに適用され、git [タグ](https://github.com/Azure/azure-sdk-for-go/tags) によって追跡されます。
これらはx.y.z形式であり、通常は [セマンティックバージョニング]](https://semver.org) 仕様に準拠しています。

**サービスAPIバージョン** は通常、日付文字列で表され、バージョンごとに個別のパッケージを提供することで追跡されます。
たとえば、コンピュートとネットワークの最新のAPIバージョンを選択するには、次のインポートを使用します:

```go
import (
    "github.com/Azure/azure-sdk-for-go/services/compute/mgmt/2017-12-01/compute"
    "github.com/Azure/azure-sdk-for-go/services/network/mgmt/2017-09-01/network"
)
```

場合によっては、サービス側の変更により、既存のバージョンに大きな変更が必要になります。
これらのケースは変更ログに記載されているため、 `サービスAPIバージョン` を単独で使用して下位互換性を確保することはできません。

利用可能なすべてのサービスとバージョンは、このリポジトリーと [GoDoc][services_godoc] の `services/` パスの下にリスト化されています。
`find ./services -type d -mindepth 3` を実行して、使用可能なすべてのサービスパッケージを一覧表示します。

[services_godoc]: https://godoc.org/github.com/Azure/azure-sdk-for-go/services

### プロファイル

Azure **APIプロファイル** は、Azure APIとバージョンのサブセットを指定します。 プロファイルは以下を提供できます:

- 特定のAPIバージョンにロックすることによるアプリケーションの **安定性** ; および/または
- アプリケーションとAzure StackおよびリージョンのAzureデータセンターでの **互換性** 。

Go SDKでは、プロファイルは `profiles/` パスで使用でき、それらのコンポーネントAPIバージョンは、 `services/` での実際のサービスパッケージのエイリアスです。
次のように使用できます:

```go
import "github.com/Azure/azure-sdk-for-go/profiles/2017-03-09/compute/mgmt/compute"
import "github.com/Azure/azure-sdk-for-go/profiles/2017-03-09/network/mgmt/network"
import "github.com/Azure/azure-sdk-for-go/profiles/2017-03-09/storage/mgmt/storage"
```

次のプロファイルは、AzureとAzure Stackのハイブリッド環境で使用できます。
- 2017-03-09
- 2018-03-01

バージョン付きプロファイルに加えて、 `latest` および `preview` の2つの特別なプロファイルも提供しています。
`latest` のプロファイルには、プレビューバージョンおよび/またはコンテンツを除く、各サービスの最新のAPIバージョンが含まれています。
`preview` プロファイルは `latest` プロファイルに似ていますが、プレビューAPIバージョンが含まれています。

`latest` と `preview` プロファイルを使用すると、アプリケーションを構築するときにAPIの更新を最新の状態に保つことができます。
ただし、定義上は安定していないため、本番環境のアプリでは使用 **しないでください**。
代わりに、 `services/` パスから最新の特定のAPIバージョン (または必要に応じて古いバージョン) を選択します。

例として、最新のCompute APIを自動的に使用するには、次のいずれかのインポートを使用します:

```go
import "github.com/Azure/azure-sdk-for-go/profiles/latest/compute/mgmt/compute"
import "github.com/Azure/azure-sdk-for-go/profiles/preview/compute/mgmt/compute"
```

### 破壊的な変更の回避

破壊的な変更の回避するには、インポートを指定するときに、 `サービスAPIバージョン` または `プロファイル` を指定し、特定のSDKバージョンにロック ( [dep](https://github.com/golang/dep) を使用するか、まもなく対応する [Go Modules](https://github.com/golang/go/wiki/Modules) で) する必要があります。

たとえば、ソースコードのインポートで、`サービスAPIバージョン` (`2017-12-01`) を使用します:

```go
import "github.com/Azure/azure-sdk-for-go/services/compute/mgmt/2017-12-01/compute"
```

または `プロファイル` バージョン (`2017-03-09`):

```go
import "github.com/Azure/azure-sdk-for-go/profiles/2017-03-09/compute/mgmt/compute"
```

同様に、depの場合、次の内容を含む `Gopkg.toml` ファイル:

```toml
[[constraint]]
  name = "github.com/Azure/azure-sdk-for-go"
  version = "21.0.0"
```

これらの手法を組み合わせると、破壊的な変更が発生しないようにすることができます。
変更に非常に敏感な場合は、SDKバージョンに [バージョンピン](https://golang.github.io/dep/docs/Gopkg.toml.html#version-rules) を追加することでニーズを満たすことができます:

```toml
[[constraint]]
  name = "github.com/Azure/azure-sdk-for-go"
  version = "=21.3.0"
```

## 検査とデバッグ

### 組み込みの基本的なリクエスト/レスポンスロギング

`go-autorest v10.15.0` 以降では、環境変数を設定することで、リクエストとレスポンスの基本的なロギングを有効にできます。
`AZURE_GO_SDK_LOG_LEVEL` を `INFO` に設定すると、ボディなしでリクエスト/レスポンスがログに記録されます。
ボディを含めるには、ログレベルを `DEBUG` に設定します。

デフォルトでは、ロガーは標準エラーに書き込みますが、 `AZURE_GO_SDK_LOG_FILE` で指定されている場合は、標準出力またはファイルに書き込むこともできます。
指定したファイルがすでに存在する場合は、置き換えられることに注意してください。

**重要:** デフォルトでは、ロガーはAuthorizationおよびOcp-Apim-Subscription-Keyヘッダーを編集します。
他のシークレットは編集されま _せん_ 。

### カスタムリクエスト/レスポンスインスペクターの記述

すべてのクライアントはいくつかの便利なフックを実装して、Azureに対して行われる基になるリクエストを検査するのに役立ちます。

- `RequestInspector`: 送信前にGoの `http.Request` を表示および操作します
- `ResponseInspector`: 受信した `http.Response` を表示します

以下は、 `net/http/httputil` でこれらを使用してリクエストとレスポンスを確認する方法の例です。

```go
vnetClient := network.NewVirtualNetworksClient("<subscriptionID>")
vnetClient.RequestInspector = LogRequest()
vnetClient.ResponseInspector = LogResponse()

// ...

func LogRequest() autorest.PrepareDecorator {
	return func(p autorest.Preparer) autorest.Preparer {
		return autorest.PreparerFunc(func(r *http.Request) (*http.Request, error) {
			r, err := p.Prepare(r)
			if err != nil {
				log.Println(err)
			}
			dump, _ := httputil.DumpRequestOut(r, true)
			log.Println(string(dump))
			return r, err
		})
	}
}

func LogResponse() autorest.RespondDecorator {
	return func(p autorest.Responder) autorest.Responder {
		return autorest.ResponderFunc(func(r *http.Response) error {
			err := p.Respond(r)
			if err != nil {
				log.Println(err)
			}
			dump, _ := httputil.DumpResponse(r, true)
			log.Println(string(dump))
			return err
		})
	}
}
```

## トレースとメトリック

すべてのパッケージとランタイムは、 [OpenCensus](https://opencensus.io/) を使用して計測されます。

### 有効化

デフォルトでは、トレースプロバイダーはプログラムにコンパイルされず、 `AZURE_SDK_TRACING_ENABLED` 環境変数を設定する従来のアプローチは有効ではなくなります。

トレースを有効にするには、ソースファイルに次を含める必要があります。

``` go
import _ "github.com/Azure/go-autorest/tracing/opencensus"
```

トレーサーを接続するには、 `tracing.Register()` を呼び出して、 `tracing.Tracer` インターフェースを満たす型を渡します。

**注**: SDKの将来のメジャーリリースでは、トレースがデフォルトで有効になる可能性があります。

### 使用法

有効にすると、すべてのSDK呼び出しがトレースとメトリックを発行し、トレースはSDK呼び出しをAzure APIに対して行われた未加工のhttp呼び出しと関連付けます。
これらのトレースを使用するには、まだ実行していない場合は、 [Azure App Insights](https://docs.microsoft.com/en-us/azure/application-insights/opencensus-local-forwarder) や [Zipkin](https://opencensus.io/quickstart/go/tracing/#exporting-traces) などの任意のエクスポーターを登録する必要があります。

それらの間のSDK呼び出しとコードの残りの部分を関連付けるには、 `trace.Startspan(ctx context.Context, name string, o ...StartOption)` 関数を使用して、 [opencensus-goライブラリー](https://github.com/census-instrumentation/opencensus-go) を使用して開始されたspanを持つコンテキストを渡します。
次に例を示します:

```go
func doAzureCalls() {
	// The resulting context will be initialized with a root span as the context passed to
	// trace.StartSpan() has no existing span.
	ctx, span := trace.StartSpan(context.Background(), "doAzureCalls", trace.WithSampler(trace.AlwaysSample()))
	defer span.End()

	// The traces from the SDK calls will be correlated under the span inside the context that is passed in.
	zone, _ := zonesClient.CreateOrUpdate(ctx, rg, zoneName, dns.Zone{Location: to.StringPtr("global")}, "", "")
	zone, _ = zonesClient.Get(ctx, rg, *zone.Name)
	for i := 0; i < rrCount; i++ {
		rr, _ := recordsClient.CreateOrUpdate(ctx, rg, zoneName, fmt.Sprintf("rr%d", i), dns.CNAME, rdSet{
			RecordSetProperties: &dns.RecordSetProperties{
				TTL: to.Int64Ptr(3600),
				CnameRecord: &dns.CnameRecord{
					Cname: to.StringPtr("vladdbCname"),
				},
			},
		},
			"",
			"",
		)
	}
}
```

## 再試行ポリシーのリクエスト

SDKは、構成可能なデフォルト値を使用して、失敗したリクエストに再試行ポリシーを提供します。
各 [client](https://godoc.org/github.com/Azure/go-autorest/autorest#Client) オブジェクトには、次のフィールドが含まれています。
- `RetryAttempts` - 失敗したリクエストを再試行する回数
- `RetryDuration` - 再試行間の待機時間

非同期操作では、次の値も使用されます。
- `PollingDelay` - ポーリングリクエスト間の待機時間
- `PollingDuration` - タイムアウトする前に非同期リクエストをポーリングする合計時間

使用されるデフォルト値については、 [ドキュメント](https://godoc.org/github.com/Azure/go-autorest/autorest#pkg-constants) を参照してください。

1つ以上の値を変更すると、それ以降のすべてのAPI呼び出しに影響します。

デフォルトのポリシーでは、APIの `Sender` メソッドから `autorest.DoRetryForStatusCodes()` を呼び出します。
例:

```go
func (client OperationsClient) ListSender(req *http.Request) (*http.Response, error) {
	sd := autorest.GetSendDecorators(req.Context(), autorest.DoRetryForStatusCodes(client.RetryAttempts, client.RetryDuration, autorest.StatusCodesForRetry...))
	return autorest.SendWithSender(client, req, sd...)
}
```

`autorest.DoRetryforStatusCodes()` の動作の詳細については、 [ドキュメント](https://godoc.org/github.com/Azure/go-autorest/autorest#DoRetryForStatusCodes) をご覧ください。

`Sender` メソッドで使用される `SendDecorators` のスライスは、コンテキストで内密に受け渡すことにより、API呼び出しごとにカスタマイズできます。
ここに例があります。

```go
ctx := context.Background()
autorest.WithSendDecorators(ctx, []autorest.SendDecorator{
	autorest.DoRetryForStatusCodesWithCap(client.RetryAttempts,
		client.RetryDuration, time.Duration(0),
		autorest.StatusCodesForRetry...)})
client.List(ctx)
```

これにより、 `SendDecorators` のデフォルトスライスが提供されたスライスに置き換えられます。

`PollingDelay` と `PollingDuration` の値は、非同期呼び出しが完了するまでブロックするときに、 [WaitForCompletionRef()](https://godoc.org/github.com/Azure/go-autorest/autorest/azure#Future.WaitForCompletionRef) によって排他的に使用されます。

# リソース

- SDKドキュメントは [godoc.org](https://godoc.org/github.com/Azure/azure-sdk-for-go/) にあります。
- SDKサンプルは、 [Azure-Samples/azure-sdk-for-go-samples](https://github.com/Azure-Samples/azure-sdk-for-go-samples) にあります。
- SDK通知は、 [Azure更新フィード](https://azure.microsoft.com/updates/) を介して公開されます。
- Azure APIドキュメントは [docs.microsoft.com/azure](https://docs.microsoft.com/azure) にあります。
- Azureの一般的なドキュメントは、 [docs.microsoft.com/azure](https://docs.microsoft.com/azure) にあります。

## セキュリティ問題とセキュリティバグの報告

セキュリティの問題やバグは、電子メールでマイクロソフトセキュリティレスポンスセンター (MSRC) の <secure@microsoft.com> に非公開で報告する必要があります。
24時間以内に返信があります。
何らかの理由で連絡が取れない場合は、メールでフォローアップして、元のメッセージが届いたことを確認してください。
MSRC PGPキーを含む詳細情報は、 [セキュリティTechCenter](https://www.microsoft.com/msrc/faqs-report-an-issue) にあります。

## ライセンス

```
   Copyright 2020 Microsoft Corporation

   Licensed under the Apache License, Version 2.0 (the "License");
   you may not use this file except in compliance with the License.
   You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

   Unless required by applicable law or agreed to in writing, software
   distributed under the License is distributed on an "AS IS" BASIS,
   WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
   See the License for the specific language governing permissions and
   limitations under the License.
```

## コントリビュート

[CONTRIBUTING.md](./CONTRIBUTING.md) を参照してください。

[samples_repo]: https://github.com/Azure-Samples/azure-sdk-for-go-samples
