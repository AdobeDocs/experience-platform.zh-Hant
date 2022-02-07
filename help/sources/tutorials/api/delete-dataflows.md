---
keywords: Experience Platform；首頁；熱門主題；流服務；API;api;delete;delete dataflows
solution: Experience Platform
title: 使用流服務API刪除資料流
topic-legacy: overview
type: Tutorial
description: 瞭解如何使用流服務API刪除批處理和流資料流。
exl-id: ea9040b1-3a40-493d-86f0-27deef09df07
source-git-commit: a51c878bbfd3004cb597ce9244a9ed2f2318604b
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 1%

---

# 使用流服務API刪除資料流

您可以使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)。

本教程介紹了刪除使用批處理源和流式處理源建立的資料流的步驟 [!DNL Flow Service]。

## 快速入門

本教程要求您具有有效的流ID。 如果沒有有效的流ID，請從 [源概述](../../home.md) 在嘗試本教程之前，請按照上述步驟操作。

本教程還要求您對以下Adobe Experience Platform元件有一定的瞭解：

* [源](../../home.md): [!DNL Experience Platform] 允許從各種源接收資料，同時讓您能夠使用 [!DNL Platform] 服務。
* [沙箱](../../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙箱，將單個沙箱 [!DNL Platform] 實例到獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

以下各節提供了需要瞭解的其他資訊，以便使用 [!DNL Flow Service] API。

### 讀取示例API調用

本教程提供了示例API調用，以演示如何格式化請求。 這些包括路徑、必需的標頭和正確格式化的請求負載。 還提供了API響應中返回的示例JSON。 有關示例API調用文檔中使用的約定的資訊，請參見上的 [如何讀取示例API調用](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) 的 [!DNL Experience Platform] 疑難解答指南。

### 收集所需標題的值

為了呼叫 [!DNL Platform] API，必須首先完成 [驗證教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份驗證教程將提供所有中每個必需標頭的值 [!DNL Experience Platform] API調用，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

中的所有資源 [!DNL Experience Platform]包括那些 [!DNL Flow Service]，與特定虛擬沙箱隔離。 所有請求 [!DNL Platform] API需要一個標頭，該標頭指定操作將在以下位置進行的沙盒的名稱：

* `x-sandbox-name: {SANDBOX_NAME}`

所有包含負載(POST、PUT、PATCH)的請求都需要附加的媒體類型報頭：

* `Content-Type: application/json`

## 刪除資料流

使用現有流ID，可以通過執行對的DELETE請求來刪除資料流 [!DNL Flow Service] API。

**API格式**

```http
DELETE /flows/{FLOW_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{FLOW_ID}` | 獨特 `id` 要刪除的資料流的值。 |

**要求**

```shell
curl -X DELETE \
    'https://platform.adobe.io/data/foundation/flowservice/flows/20c115bc-46e3-40f3-bfe9-fb25abe4ba76' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回HTTP狀態204（無內容）和空白正文。 您可以通過嘗試對資料流進行查找(GET)請求來確認刪除。 API將返回HTTP 404（未找到）錯誤，表示資料流已被刪除。

## 後續步驟

按照本教程，您已成功使用 [!DNL Flow Service] 刪除現有資料流的API。

有關如何使用用戶介面執行這些操作的步驟，請參閱上的教程 [刪除UI中的資料流](../../tutorials/ui/delete.md)
