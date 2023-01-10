---
keywords: Experience Platform；首頁；熱門主題；行銷自動化
solution: Experience Platform
title: 使用流程服務API探索行銷自動化系統
description: 本教學課程使用流量服務API來探索行銷自動化系統。
exl-id: 250c1ba0-1baa-444f-ab2b-58b3a025561e
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 2%

---

# 探索行銷自動化系統，使用 [!DNL Flow Service] API

[!DNL Flow Service] 可用來收集和集中Adobe Experience Platform中各種不同來源的客戶資料。 該服務提供用戶介面和RESTful API，所有受支援的源都可從中連接。

本教學課程使用 [!DNL Flow Service] 探索行銷自動化系統的API。

## 快速入門

本指南需要妥善了解下列Adobe Experience Platform元件：

* [來源](../../../home.md): [!DNL Experience Platform] 可讓您從各種來源擷取資料，同時使用來建構、加標籤及增強傳入資料 [!DNL Platform] 服務。
* [沙箱](../../../../sandboxes/home.md): [!DNL Experience Platform] 提供可分割單一沙箱的虛擬沙箱 [!DNL Platform] 例項放入個別的虛擬環境，以協助開發及改進數位體驗應用程式。

以下小節提供您需要知道的其他資訊，以便使用成功連線至行銷自動化系統 [!DNL Flow Service] API。

### 收集所需憑據

本教學課程要求您與您要擷取資料的第三方行銷自動化應用程式建立有效連線。 有效的連接涉及應用程式的連接規範ID和連接ID。 如需建立行銷自動化連線及擷取這些值的詳細資訊，請參閱 [將行銷自動化來源連結至Platform](../../api/create/marketing-automation/hubspot.md) 教學課程。

### 讀取範例API呼叫

本教學課程提供範例API呼叫，以示範如何設定要求格式。 這些功能包括路徑、必要標題和格式正確的請求裝載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所使用慣例的相關資訊，請參閱 [如何閱讀API呼叫範例](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑難排解指南。

### 收集必要標題的值

若要對 [!DNL Platform] API，您必須先完成 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en). 完成驗證教學課程會提供所有 [!DNL Experience Platform] API呼叫，如下所示：

* 授權：承載 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

中的所有資源 [!DNL Experience Platform]，包括 [!DNL Flow Service]，會與特定虛擬沙箱隔離。 所有請求 [!DNL Platform] API需要標頭，以指定要在中執行操作的沙箱名稱：

* x-sandbox-name: `{SANDBOX_NAME}`

所有包含裝載(POST、PUT、PATCH)的請求都需要其他媒體類型標題：

* Content-Type: `application/json`

## 探索資料表

使用行銷自動化系統的基本連線，您可以透過執行GET請求來探索資料表。 使用以下調用查找要檢查或將其嵌入的表的路徑 [!DNL Platform].

**API格式**

```https
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| 參數 | 說明 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 行銷自動化系統的基本連線ID。 |

**要求**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/2fce94c1-9a93-4971-8e94-c19a93097129/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應是從到行銷自動化系統的一系清單格。 找到要放進的桌子 [!DNL Platform] 並注意 `path` 屬性，因為您必須在下一個步驟中提供屬性，以檢查其結構。

```json
[
    {
        "type": "table",
        "name": "Hubspot.All_Deals",
        "path": "Hubspot.All_Deals",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Hubspot.Blog_Authors",
        "path": "Hubspot.Blog_Authors",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Hubspot.Blog_Comments",
        "path": "Hubspot.Blog_Comments",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Hubspot.Contacts",
        "path": "Hubspot.Contacts",
        "canPreview": true,
        "canFetchSchema": true
    },
]
```

## Inspect表的結構

若要從行銷自動化系統檢查表格的結構，請在指定表格路徑作為查詢參數時執行GET請求。

**API格式**

```https
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| 參數 | 說明 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 行銷自動化系統的連線ID。 |
| `{TABLE_PATH}` | 行銷自動化系統內的表格路徑。 |

**要求**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/2fce94c1-9a93-4971-8e94-c19a93097129/explore?objectType=table&object=Hubspot.Contacts' \
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
                "name": "Properties_Firstname_Value",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Properties_Lastname_Value",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Added_At",
                "type": "string",
                "meta:xdmType": "date-time",
                "xdm": {
                    "type": "string",
                    "format": "date-time"
                }
            },
            {
                "name": "Portal_Id",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
        ]
    }
}
```

## 後續步驟

依照本教學課程，您已探索行銷自動化系統，並找到您要帶入的表格路徑 [!DNL Platform]，並取得其結構的相關資訊。 您可以在下一個教學課程中使用此資訊，以 [從您的行銷自動化系統收集資料並匯入Platform](../collect/marketing-automation.md).
