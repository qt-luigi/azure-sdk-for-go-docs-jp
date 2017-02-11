# 本リポジトリーについて

[Azure/azure-sdk-for-go](https://github.com/Azure/azure-sdk-for-go) のドキュメントを日本語に翻訳してみました。
Google翻訳を使用して翻訳した後に自分でチェックして修正しています。
翻訳時のバージョンは [v8.0.1-beta](https://github.com/Azure/azure-sdk-for-go/tree/v8.0.1-beta) です。

# Microsoft Azure SDK for Go

このプロジェクトはMicrosoft Azure REST APIの操作を実行するためのさまざまなGoパッケージを提供します。

[![GoDoc](https://godoc.org/github.com/Azure/azure-sdk-for-go?status.svg)](https://godoc.org/github.com/Azure/azure-sdk-for-go) [![Build Status](https://travis-ci.org/Azure/azure-sdk-for-go.svg?branch=master)](https://travis-ci.org/Azure/azure-sdk-for-go) [![Go Report Card](https://goreportcard.com/badge/github.com/Azure/azure-sdk-for-go)](https://goreportcard.com/report/github.com/Azure/azure-sdk-for-go)

> **注意:**
このリポジトリーは継続的な開発が進行中であり時間が経つと破綻する可能性があります。
現時点でまだリリースはありません。
本リポジトリーの使用を予定している場合は、プロジェクト内でパッケージをベンダリングすることを検討し、安定したタグがないときにそれらを更新してください。

# パッケージ

## Azure リソース マネージャー (ARM)

[ARMについて](/arm/README.md)

- [analysisservices](/arm/analysisservices)
- [authorization](/arm/authorization)
- [batch](/arm/batch)
- [cdn](/arm/cdn)
- [cognitiveservices](/arm/cognitiveservices)
- [commerce](/arm/commerce)
- [compute](/arm/compute)
- [containerregistry](/arm/containerregistry)
- [containerservice](/arm/containerservice)
- [datalake-analytics/account](/arm/datalake-analytics/account)
- [datalake-store/account](/arm/datalake-store/account)
- [devtestlabs](/arm/devtestlabs)
- [dns](/arm/dns)
- [documentdb](/arm/documentdb)
- [eventhub](/arm/eventhub)
- [intune](/arm/intune)
- [iothub](/arm/iothub)
- [keyvault](/arm/keyvault)
- [logic](/arm/logic)
- [machinelearning/commitmentplans](/arm/machinelearning/commitmentplans)
- [machinelearning/webservices](/arm/machinelearning/webservices)
- [mediaservices](/arm/mediaservices)
- [mobileengagement](/arm/mobileengagement)
- [network](/arm/network)
- [notificationhubs](/arm/notificationhubs)
- [powerbiembedded](/arm/powerbiembedded)
- [recoveryservices](/arm/recoveryservices)
- [redis](/arm/redis)
- [resources/features](/arm/resources/features)
- [resources/links](/arm/resources/links)
- [resources/locks](/arm/resources/locks)
- [resources/policy](/arm/resources/policy)
- [resources/resources](/arm/resources/resources)
- [resources/subscriptions](/arm/resources/subscriptions)
- [scheduler](/arm/scheduler)
- [search](/arm/search)
- [servermanagement](/arm/servermanagement)
- [servicebus](/arm/servicebus)
- [sql](/arm/sql)
- [storage](/arm/storage)
- [trafficmanager](/arm/trafficmanager)
- [web](/arm/web)

## Azure サービス管理 (ASM)、いわゆるクラシック環境

[ASMについて](/management/README.md)

- [affinitygroup](/management/affinitygroup)
- [hostedservice](/management/hostedservice)
- [location](/management/location)
- [networksecuritygroup](/management/networksecuritygroup)
- [osimage](/management/osimage)
- [sql](/management/sql)
- [storageservice](/management/storageservice)
- [virtualmachine](/management/virtualmachine)
- [virtualmachinedisk](/management/virtualmachinedisk)
- [virtualmachineimage](/management/virtualmachineimage)
- [virtualnetwork](/management/virtualnetwork)
- [vmutils](/management/vmutils)

## Azure Storage SDK for Go

[ストレージについて](/storage/README.md)

- [storage](/storage)

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
