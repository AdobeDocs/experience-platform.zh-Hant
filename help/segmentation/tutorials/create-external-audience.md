---
title: 建立及啟用外部對象
type: Tutorial
description: 瞭解如何使用Experience Platform API在Adobe Experience Platform中建立外部受眾。
source-git-commit: 0a37ef2f5fc08eb515c7c5056936fd904ea6d360
workflow-type: tm+mt
source-wordcount: '892'
ht-degree: 3%

---


# 使用API建立及啟用外部對象

本教學課程將逐步解說使用Adobe Experience Platform API建立外部受眾所需的步驟。

## 快速入門

若要取得本教學課程，請先實際瞭解建立外部受眾所涉及的各種Experience Platform服務。 在開始本教學課程之前，請先閱讀以下服務的檔案：

- [來源](../../sources/home.md)： Experience Platform允許從各種來源擷取資料，同時讓您能夠使用Experience Platform服務來建構、加標籤以及增強傳入的資料。
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md)：可讓您從外部資料建立對象。
- [目的地](../../destinations/home.md)：目的地是預先建置的與常用應用程式的整合，可讓您順暢地從Experience Platform啟用資料，用於跨管道行銷活動、電子郵件行銷活動、目標定位廣告等。

### 必要的標頭

此教學課程也要求您完成[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)，才能成功呼叫[!DNL Experience Platform] API。 完成驗證教學課程會提供所有 [!DNL Experience Platform] API 呼叫中每個必要標頭的值，如下所示：

- 授權：持有人`{ACCESS_TOKEN}`
- x-api-key： `{API_KEY}`
- x-gw-ims-org-id： `{ORG_ID}`

[!DNL Experience Platform]中的所有資源都與特定的虛擬沙箱隔離。 對[!DNL Experience Platform] API的請求需要一個標頭，該標頭會指定將在其中執行操作的沙箱的名稱：

- x-sandbox-name： `{SANDBOX_NAME}`

>[!NOTE]
>
>如需[!DNL Experience Platform]中沙箱的詳細資訊，請參閱[沙箱概觀檔案](../../sandboxes/home.md)。

所有POST、PUT和PATCH請求都需要額外的標頭：

- Content-Type： application/json

## 準備外部對象 {#prepare}

您必須先準備包含對象資料的檔案，才能在Experience Platform中建立外部對象。

在此範例中，您應使用CSV檔案。 請確認您的CSV檔案包含&#x200B;**至少**&#x200B;個具有身分值（例如ECID、電子郵件ID或CRM ID）的資料行。 此外，請確定包含細分和啟動所需的所有擴充屬性。

您也必須確認檔案符合Experience Platform結構描述的要求。 如需建立結構描述的詳細資訊，請閱讀使用API[建立結構描述的](/help/xdm/tutorials/create-schema-api.md)教學課程，或使用UI[建立結構描述的](/help/xdm/tutorials/create-schema-ui.md)教學課程。

在您確認CSV檔案包含您所需的所有資訊並符合結構描述後，您需要將CSV檔案上傳至雲端儲存提供者，以便使用來源將資料擷取到Experience Platform。 如需使用雲端儲存空間來源的詳細資訊，請參閱使用API[探索雲端儲存空間選項的](/help/sources/tutorials/api/explore/cloud-storage.md)教學課程或[來源概觀](/help/sources/home.md#cloud-storage)。

## 建立外部對象 {#create}

準備CSV檔案後，您現在可以開始建立外部對象的程式。

您可以對`/external-audience/`端點發出POST要求，以建立外部對象。

提出此請求時，您需要指定下列資訊：

- 對象名稱
- 對象的說明
- CSV和結構描述之間的對應欄位
- 來源規格資訊
   - 這包括要擷取的CSV檔案的檔案路徑
      - 檔案路徑&#x200B;**不能**&#x200B;包含任何空格。 例如，如果您的路徑是`activation/sample-source/Example CSV File.csv`，請將路徑設定為`activation/sample-source/ExampleCSVFile.csv`。

如需如何使用此端點的詳細資訊，請閱讀[外部對象端點指南](/help/segmentation/api/external-audiences.md#create-audience)。

+++請求

```shell
curl -X POST https://platform.adobe.io/data/core/ais/external-audience/ \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "name": "Sample external audience",
        "description": "A sample version of an external audience",
        "fields": [
            {
                "name": "ppid",
                "type": "string",
                "identityNs": "email"
            },
            {
                "name": "list_id",
                "type": "string",
                "labels": ["core/C2", "custom/deep"]
            },
            {
                "name": "delete",
                "type": "number"
            },
            {
                "name": "process_consent",
                "type": "string"
            }
        ],
        "sourceSpec": {
            "params": {
                "path": "activation/sample-source/example.csv",
                "type": "file",
                "sourceType": "Cloud Storage",
                "baseConnectionId": "1d1d4bc5-b527-46a3-9863-530246a61b2b"
            }
        },
        "ttlInDays": "40",
        "labels": ["core/C1"],
        "audienceType": "people",
        "originName": "CUSTOM_UPLOAD"
    }'
```

+++

提出此要求後，請務必記下您從回應中收到的`operationId`，以便擷取對象ID。

## 擷取對象ID {#retrieve-audience-id}

現在您已建立外部對象，您需要取得對象ID，才能將對象擷取至Experience Platform。

您可以向`/external-audiences/operations`端點發出GET要求，並提供您先前從建立外部對象回應中收到的作業ID，藉此擷取對象ID。

如需如何使用此端點的詳細資訊，請閱讀[外部對象端點指南](/help/segmentation/api/external-audiences.md#retrieve-status)。

+++ 請求

```shell
curl -X GET https://platform.adobe.io/data/core/ais/external-audience/operations/{OPERATION_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

提出此要求後，請務必記下您從回應中收到的`audienceId`，以便觸發對象的擷取工作。

## 開始對象內嵌 {#start-ingestion}

由於您已取得`audienceId`，因此現在可以觸發將外部對象擷取至Experience Platform。

您可以在提供對象ID時，透過向下列端點發出POST請求來開始對象擷取。 此外，您必須指定開始時間，以決定要處理的檔案。

如需如何使用此端點的詳細資訊，請閱讀[外部對象端點指南](/help/segmentation/api/external-audiences.md#start-audience-ingestion)

+++ 請求

```shell
curl -X POST https://platform.adobe.io/data/core/ais/external-audience/{AUDIENCE_ID}/runs \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
    "dataFilterStartTime": 764245635
 }' 
```

+++

提出此要求後，請務必記下您從回應中收到的`runId`，以便監視擷取狀態。

## 監視擷取狀態 {#monitor-ingestion}

觸發對象擷取後，您現在可以監視擷取進度，以確認擷取是否成功，並驗證對象是否可用於下游啟用。

您可以在提供對象和執行ID的同時，透過向以下端點發出GET請求來擷取對象擷取狀態。

如需如何使用此端點的詳細資訊，請閱讀[外部對象端點指南](/help/segmentation/api/external-audiences.md#retrieve-ingestion-status)。

+++ 請求

```shell
curl -X GET https://platform.adobe.io/data/core/ais/external-audience/{AUDIENCE_ID}/runs/{RUN_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

## 後續步驟 {#next-steps}

>[!IMPORTANT]
>
>為了使用外部產生的對象，您&#x200B;**必須**&#x200B;等到每日細分工作完成為止。

在您確認外部對象已成功內嵌後，即可在對象入口網站中看到該對象，並用於下游服務，例如目的地。

如需對象入口網站的詳細資訊，請參閱[對象入口網站UI指南](/help/segmentation/ui/audience-portal.md)。 如需有關目的地的詳細資訊，請閱讀[目的地概觀](/help/destinations/home.md)。

