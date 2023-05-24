---
keywords: Experience Platform；家庭；熱門主題；廣告系統；廣告系統
solution: Experience Platform
title: 利用流服務API開發廣告系統
description: Flow Service用於收集和集中Adobe Experience Platform內各種不同來源的客戶資料。 該服務提供了用戶介面和REST風格的API，所有支援的源都可從中連接。 本教程使用Flow Service API來瀏覽廣告系統。
exl-id: 3016ce1e-12e6-47ce-a4c5-52f8d440f515
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 2%

---

# 使用 [!DNL Flow Service] API

建立基本連接後，您現在可以使用唯一的基本連接ID來導航和瀏覽源的資料結構和內容。 這允許您在建立資料流並將其傳送到Adobe Experience Platform之前，確定特定項目及其各自的資料類型和格式。

本教程使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/) 探索廣告系統。

## 快速入門

>[!IMPORTANT]
>
>本教程要求您具有廣告來源的唯一基本連接ID。 如果您沒有此ID，請參見上的教程 [將廣告源連接到平台](../../api/create/advertising/ads.md) 教程。

本指南要求對Adobe Experience Platform的下列組成部分有工作上的理解：

* [源](../../../home.md): [!DNL Experience Platform] 允許從各種源接收資料，同時讓您能夠使用 [!DNL Platform] 服務。
* [沙箱](../../../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙箱，將單個沙箱 [!DNL Platform] 實例到獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

以下各節提供您需要瞭解的其他資訊，以便使用 [!DNL Flow Service] API。

### 使用平台API

有關如何成功調用平台API的資訊，請參見上的指南 [平台API入門](../../../../landing/api-guide.md)。

## 瀏覽資料表

使用廣告系統的基本連接，您可以通過執行GET請求來瀏覽資料表。 使用以下調用查找要檢查或插入的表的路徑 [!DNL Platform]。

**API格式**

```https
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| 參數 | 說明 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 廣告系統的基本連接的ID。 |

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

成功的響應是從廣告系統到廣告系統的一系清單。 查找要放入的表 [!DNL Platform] 並注意到 `path` 屬性，因為在下一步中需要提供該屬性來檢查其結構。

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

## Inspect桌子的結構

要從廣告系統檢查表的結構，請在將表的路徑指定為查詢參數時執行GET請求。

**API格式**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| 參數 | 說明 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 廣告系統的連接ID。 |
| `{TABLE_PATH}` | 廣告系統中表的路徑。 |

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

成功的響應返回表的結構。 有關每個表列的詳細資訊位於 `columns` 陣列。

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

通過學習本教程，您已探索了廣告系統，找到了要導入的表的路徑 [!DNL Platform]並獲取了有關其結構的資訊。 您可以在下一教程中使用此資訊 [從您的廣告系統收集資料並將其導入平台](../collect/advertising.md)。
