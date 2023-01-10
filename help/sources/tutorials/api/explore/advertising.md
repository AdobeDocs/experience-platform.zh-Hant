---
keywords: Experience Platform；首頁；熱門主題；廣告系統；廣告系統
solution: Experience Platform
title: 使用流量服務API探索廣告系統
description: 流量服務用於收集和集中Adobe Experience Platform內各種不同來源的客戶資料。 該服務提供用戶介面和RESTful API，所有受支援的源都可從中連接。 本教學課程使用流量服務API來探索廣告系統。
exl-id: 3016ce1e-12e6-47ce-a4c5-52f8d440f515
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 2%

---

# 使用 [!DNL Flow Service] API

建立基本連線後，您現在可以使用唯一的基本連線ID來導覽及探索來源的資料結構和內容。 這可讓您在建立資料流並將其帶入Adobe Experience Platform之前，先識別特定項目及其各自的資料類型和格式。

本教學課程使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/) 探索廣告系統。

## 快速入門

>[!IMPORTANT]
>
>本教學課程要求您擁有廣告來源的唯一基本連線ID。 如果您沒有此ID，請參閱 [將廣告來源連接到Platform](../../api/create/advertising/ads.md) 教學課程。

本指南需要妥善了解下列Adobe Experience Platform元件：

* [來源](../../../home.md): [!DNL Experience Platform] 可讓您從各種來源擷取資料，同時使用來建構、加標籤及增強傳入資料 [!DNL Platform] 服務。
* [沙箱](../../../../sandboxes/home.md): [!DNL Experience Platform] 提供可分割單一沙箱的虛擬沙箱 [!DNL Platform] 例項放入個別的虛擬環境，以協助開發及改進數位體驗應用程式。

以下章節提供您需要知道的其他資訊，以便成功連線至使用 [!DNL Flow Service] API。

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱 [Platform API快速入門](../../../../landing/api-guide.md).

## 探索資料表

使用廣告系統的基本連線，您可以執行GET請求來探索資料表。 使用以下調用查找要檢查或將其嵌入的表的路徑 [!DNL Platform].

**API格式**

```https
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| 參數 | 說明 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 廣告系統的基本連線ID。 |

**要求**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/2484f2df-c057-4ab5-84f2-dfc0577ab592/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應是從到廣告系統的一組表格。 找到要放進的桌子 [!DNL Platform] 並注意 `path` 屬性，因為您必須在下一個步驟中提供屬性，以檢查其結構。

```json
[
    {
        "type": "table",
        "name": "v201809.ACCOUNT_PERFORMANCE_REPORT",
        "path": "v201809.ACCOUNT_PERFORMANCE_REPORT",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "v201809.ADGROUP_PERFORMANCE_REPORT",
        "path": "v201809.ADGROUP_PERFORMANCE_REPORT",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "v201809.AD_CUSTOMIZERS_FEED_ITEM_REPORT",
        "path": "v201809.AD_CUSTOMIZERS_FEED_ITEM_REPORT",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "v201809.AD_PERFORMANCE_REPORT",
        "path": "v201809.AD_PERFORMANCE_REPORT",
        "canPreview": true,
        "canFetchSchema": true
    }
]
```

## Inspect表的結構

若要從廣告系統檢查表格的結構，請在指定表格路徑作為查詢參數時執行GET要求。

**API格式**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| 參數 | 說明 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 廣告系統的連線ID。 |
| `{TABLE_PATH}` | 廣告系統內的表格路徑。 |

**要求**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/2484f2df-c057-4ab5-84f2-dfc0577ab592/explore?objectType=table&object=v201809.AD_PERFORMANCE_REPORT' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回表格的結構。 有關表格各欄的詳細資訊位於 `columns` 陣列。

```json
{
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "CallOnlyPhoneNumber",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "AdGroupId",
                "type": "long",
                "xdm": {
                    "type": "integer",
                    "minimum": -9007199254740992,
                    "maximum": 9007199254740991
                }
            },
            {
                "name": "AdGroupName",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Date",
                "type": "string",
                "meta:xdmType": "date-time",
                "xdm": {
                    "type": "string",
                    "format": "date-time"
                }
            },
        ]
    }
}
```

## 後續步驟

依照本教學課程，您已探索廣告系統，並找到您要帶入的表格路徑 [!DNL Platform]，並取得其結構的相關資訊。 您可以在下一個教學課程中使用此資訊，以 [從您的廣告系統收集資料並匯入Platform](../collect/advertising.md).
