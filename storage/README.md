# Azure Storage SDK for Go (プレビュー)

:exclamation: 重要: このパッケージはメンテナンス中のみであり、将来的に廃止される予定です。
代わりに、次のパッケージのいずれかを使用してください。

| サービス | インポート パス/リポジトリー |
|---------|------------------|
| Storage - Blobs | [github.com/Azure/azure-storage-blob-go](https://github.com/Azure/azure-storage-blob-go) |
| Storage - Files | [github.com/Azure/azure-storage-file-go](https://github.com/Azure/azure-storage-file-go) |
| Storage - Queues | [github.com/Azure/azure-storage-queue-go](https://github.com/Azure/azure-storage-queue-go) |

`github.com/Azure/azure-sdk-for-go/storage` パッケージは、 [Azure Storage](https://docs.microsoft.com/en-us/azure/storage/) データプレーンリソース (コンテナー、BLOB、テーブル、キュー) を管理するために使用されます。

ストレージ *アカウント* を管理するには、 [github.com/Azure/azure-sdk-for-go/services/storage](https://github.com/Azure/azure-sdk-for-go/tree/master/services/storage) のパッケージからAzure Resource Manager (ARM) を使用します。

このパッケージは、 [Azure Storage Emulator](https://azure.microsoft.com/documentation/articles/storage-use-emulator/) もサポートします (Windowsのみ)。

