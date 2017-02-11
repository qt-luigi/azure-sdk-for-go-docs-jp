# 本リポジトリーについて

[Azure/azure-sdk-for-go](https://github.com/Azure/azure-sdk-for-go) のドキュメントを日本語に翻訳してみました。
Google翻訳を使用して翻訳した後に自分でチェックして修正しています。
翻訳時のバージョンは [v8.0.1-beta](https://github.com/Azure/azure-sdk-for-go/tree/v8.0.1-beta) です。

**リンクについて:** 
【本リポジトリーの○○に遷移】と記述されているリンクは本リポジトリー内に、何も記述されていないリンクはオリジナルの通り外部および [Azure/azure-sdk-for-go](https://github.com/Azure/azure-sdk-for-go) に遷移します。

# Microsoft Azure SDK for Go

このプロジェクトはMicrosoft Azure REST APIの操作を実行するためのさまざまなGoパッケージを提供します。

[![GoDoc](https://godoc.org/github.com/Azure/azure-sdk-for-go?status.svg)](https://godoc.org/github.com/Azure/azure-sdk-for-go) [![Build Status](https://travis-ci.org/Azure/azure-sdk-for-go.svg?branch=master)](https://travis-ci.org/Azure/azure-sdk-for-go) [![Go Report Card](https://goreportcard.com/badge/github.com/Azure/azure-sdk-for-go)](https://goreportcard.com/report/github.com/Azure/azure-sdk-for-go)

> **注意:**
このリポジトリーは継続的な開発が進行中であり時間が経つと破綻する可能性があります。
現時点でまだリリースはありません。
本リポジトリーの使用を予定している場合は、プロジェクト内でパッケージをベンダリングすることを検討し、安定したタグがないときにそれらを更新してください。

# パッケージ

## Azure リソース マネージャー (ARM)

[ARMについて](/arm/README.md)【本リポジトリーの/arm/README.mdに遷移】

- [analysisservices](https://github.com/Azure/azure-sdk-for-go/blob/master/arm/analysisservices)
- [authorization](https://github.com/Azure/azure-sdk-for-go/blob/master/arm/authorization)
- [batch](https://github.com/Azure/azure-sdk-for-go/blob/master/arm/batch)
- [cdn](https://github.com/Azure/azure-sdk-for-go/blob/master/arm/cdn)
- [cognitiveservices](https://github.com/Azure/azure-sdk-for-go/blob/master/arm/cognitiveservices)
- [commerce](https://github.com/Azure/azure-sdk-for-go/blob/master/arm/commerce)
- [compute](https://github.com/Azure/azure-sdk-for-go/blob/master/arm/compute)
- [containerregistry](https://github.com/Azure/azure-sdk-for-go/blob/master/arm/containerregistry)
- [containerservice](https://github.com/Azure/azure-sdk-for-go/blob/master/arm/containerservice)
- [datalake-analytics/account](https://github.com/Azure/azure-sdk-for-go/blob/master/arm/datalake-analytics/account)
- [datalake-store/account](https://github.com/Azure/azure-sdk-for-go/blob/master/arm/datalake-store/account)
- [devtestlabs](https://github.com/Azure/azure-sdk-for-go/blob/master/arm/devtestlabs)
- [dns](https://github.com/Azure/azure-sdk-for-go/blob/master/arm/dns)
- [documentdb](https://github.com/Azure/azure-sdk-for-go/blob/master/arm/documentdb)
- [eventhub](https://github.com/Azure/azure-sdk-for-go/blob/master/arm/eventhub)
- [intune](https://github.com/Azure/azure-sdk-for-go/blob/master/arm/intune)
- [iothub](https://github.com/Azure/azure-sdk-for-go/blob/master/arm/iothub)
- [keyvault](https://github.com/Azure/azure-sdk-for-go/blob/master/arm/keyvault)
- [logic](https://github.com/Azure/azure-sdk-for-go/blob/master/arm/logic)
- [machinelearning/commitmentplans](https://github.com/Azure/azure-sdk-for-go/blob/master/arm/machinelearning/commitmentplans)
- [machinelearning/webservices](https://github.com/Azure/azure-sdk-for-go/blob/master/arm/machinelearning/webservices)
- [mediaservices](https://github.com/Azure/azure-sdk-for-go/blob/master/arm/mediaservices)
- [mobileengagement](https://github.com/Azure/azure-sdk-for-go/blob/master/arm/mobileengagement)
- [network](https://github.com/Azure/azure-sdk-for-go/blob/master/arm/network)
- [notificationhubs](https://github.com/Azure/azure-sdk-for-go/blob/master/arm/notificationhubs)
- [powerbiembedded](https://github.com/Azure/azure-sdk-for-go/blob/master/arm/powerbiembedded)
- [recoveryservices](https://github.com/Azure/azure-sdk-for-go/blob/master/arm/recoveryservices)
- [redis](https://github.com/Azure/azure-sdk-for-go/blob/master/arm/redis)
- [resources/features](https://github.com/Azure/azure-sdk-for-go/blob/master/arm/resources/features)
- [resources/links](https://github.com/Azure/azure-sdk-for-go/blob/master/arm/resources/links)
- [resources/locks](https://github.com/Azure/azure-sdk-for-go/blob/master/arm/resources/locks)
- [resources/policy](https://github.com/Azure/azure-sdk-for-go/blob/master/arm/resources/policy)
- [resources/resources](https://github.com/Azure/azure-sdk-for-go/blob/master/arm/resources/resources)
- [resources/subscriptions](https://github.com/Azure/azure-sdk-for-go/blob/master/arm/resources/subscriptions)
- [scheduler](https://github.com/Azure/azure-sdk-for-go/blob/master/arm/scheduler)
- [search](https://github.com/Azure/azure-sdk-for-go/blob/master/arm/search)
- [servermanagement](https://github.com/Azure/azure-sdk-for-go/blob/master/arm/servermanagement)
- [servicebus](https://github.com/Azure/azure-sdk-for-go/blob/master/arm/servicebus)
- [sql](https://github.com/Azure/azure-sdk-for-go/blob/master/arm/sql)
- [storage](https://github.com/Azure/azure-sdk-for-go/blob/master/arm/storage)
- [trafficmanager](https://github.com/Azure/azure-sdk-for-go/blob/master/arm/trafficmanager)
- [web](https://github.com/Azure/azure-sdk-for-go/blob/master/arm/web)

## Azure サービス管理 (ASM)、いわゆるクラシック環境

[ASMについて](/management/README.md)【本リポジトリーの/management/README.mdに遷移】

- [affinitygroup](https://github.com/Azure/azure-sdk-for-go/blob/master/management/affinitygroup)
- [hostedservice](https://github.com/Azure/azure-sdk-for-go/blob/master/management/hostedservice)
- [location](https://github.com/Azure/azure-sdk-for-go/blob/master/management/location)
- [networksecuritygroup](https://github.com/Azure/azure-sdk-for-go/blob/master/management/networksecuritygroup)
- [osimage](https://github.com/Azure/azure-sdk-for-go/blob/master/management/osimage)
- [sql](https://github.com/Azure/azure-sdk-for-go/blob/master/management/sql)
- [storageservice](https://github.com/Azure/azure-sdk-for-go/blob/master/management/storageservice)
- [virtualmachine](https://github.com/Azure/azure-sdk-for-go/blob/master/management/virtualmachine)
- [virtualmachinedisk](https://github.com/Azure/azure-sdk-for-go/blob/master/management/virtualmachinedisk)
- [virtualmachineimage](https://github.com/Azure/azure-sdk-for-go/blob/master/management/virtualmachineimage)
- [virtualnetwork](https://github.com/Azure/azure-sdk-for-go/blob/master/management/virtualnetwork)
- [vmutils](https://github.com/Azure/azure-sdk-for-go/blob/master/management/vmutils)

## Azure Storage SDK for Go

[ストレージについて](/storage/README.md)【本リポジトリーの/storage/README.mdに遷移】

- [storage](https://github.com/Azure/azure-sdk-for-go/blob/master/storage)

# インストール

- [Go 1.7をインストールします](https://golang.org/dl/)。

- GoでSDKを取得します:

```
$ go get -d github.com/Azure/azure-sdk-for-go
```

> **重要:**
Azure SDK for Goを依存関係としてベンダリングすることを強くお勧めします。
依存関係をベンダリングするために、Azure SDK for Goは [glide](https://github.com/Masterminds/glide) を使用します。
まだインストールしていない場合、glideをインストールしてください。
プロジェクトディレクトリーに移動し、依存関係をインストールします。

```
$ cd your/project
$ glide create
$ glide install
```

# ドキュメント

[Godoc.org](http://godoc.org/github.com/Azure/azure-sdk-for-go/) にて本リポジトリーのGodocをご覧ください。

# コントリビュート

このプロジェクトへの積極的なコントリビューターになりたい場合、[Microsoft Azure プロジェクト コントリビューション ガイドライン](http://azure.github.io/guidelines/) に記載されている指示に従ってください。

# ライセンス

このプロジェクトは [Apache 2.0 ライセンス](LICENSE) のもとに配布されています。

-----
このプロジェクトは [Microsoft オープンソース 行動規範](https://opensource.microsoft.com/codeofconduct/) を採用しました。
さらなる情報については [行動規範 FAQ](https://opensource.microsoft.com/codeofconduct/faq/) を参照するか、その他に質問や意見があれば [opencode@microsoft.com](mailto:opencode@microsoft.com) に問い合わせてください。
