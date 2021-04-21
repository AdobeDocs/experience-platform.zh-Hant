---
keywords: Experience Platform;home；熱門主題；流服務；API;api;delete；刪除資料流
solution: Experience Platform
title: 使用流服務API刪除資料流
topic-legacy: overview
type: Tutorial
description: 瞭解如何使用Flow Service API刪除批處理和流資料流。
exl-id: ea9040b1-3a40-493d-86f0-27deef09df07
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 1%

---

# 使用流服務API刪除資料流

使用[[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml)可以刪除包含錯誤或已過時的批處理和流資料流。

本教程介紹使用[!DNL Flow Service]刪除批處理源和流源所建立的資料流的步驟。

## 快速入門

本教學課程要求您必須擁有有效的流程ID。 如果您沒有有效的流ID，請從[來源概觀](../../home.md)中選取您選擇的連接器，然後依照本教學課程嘗試前所述的步驟進行。

本教學課程還要求您對Adobe Experience Platform的以下部分有切實的瞭解：

* [來源](../../home.md): [!DNL Experience Platform] 允許從各種來源接收資料，同時提供使用服務構建、標籤和增強傳入資料的 [!DNL Platform] 能力。
* [沙盒](../../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙盒，可將單一執行個體分 [!DNL Platform] 割為不同的虛擬環境，以協助開發和發展數位體驗應用程式。

以下各節提供了使用[!DNL Flow Service] API成功刪除資料流所需的其他資訊。

### 讀取範例API呼叫

本教學課程提供範例API呼叫，以示範如何設定請求的格式。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱[!DNL Experience Platform]疑難排解指南中[如何讀取範例API呼叫](../../../landing/troubleshooting.md#how-do-i-format-an-api-request)一節。

### 收集必要標題的值

若要呼叫[!DNL Platform] API，您必須先完成[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)。 完成驗證教學課程後，所有[!DNL Experience Platform] API呼叫中每個所需標題的值都會顯示在下面：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

[!DNL Experience Platform]中的所有資源（包括屬於[!DNL Flow Service]的資源）都隔離到特定的虛擬沙盒。 對[!DNL Platform] API的所有請求都需要一個標題，該標題指定要在中執行操作的沙盒的名稱：

* `x-sandbox-name: {SANDBOX_NAME}`

所有包含裝載(POST、PUT、PATCH)的請求都需要附加的媒體類型標題：

* `Content-Type: application/json`

## 刪除資料流

使用現有流ID，您可以通過對[!DNL Flow Service] API執行DELETE請求來刪除資料流。

**API格式**

```http
DELETE /flows/{FLOW_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{FLOW_ID}` | 要刪除的資料流的唯一`id`值。 |

**要求**

```shell
curl -X DELETE \
    'https://platform-int.adobe.io/data/foundation/flowservice/flows/20c115bc-46e3-40f3-bfe9-fb25abe4ba76' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態204（無內容）和空白的內文。 您可以嘗試對資料流進行查找(GET)請求，以確認刪除。 API將返回HTTP 404（找不到）錯誤，表示資料流已被刪除。

## 後續步驟

按照本教程，您已成功使用[!DNL Flow Service] API刪除現有資料流。

有關如何使用用戶介面執行這些操作的步驟，請參閱有關在UI](../../tutorials/ui/delete.md)中刪除資料流的[教程
