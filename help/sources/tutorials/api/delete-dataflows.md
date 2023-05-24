---
keywords: Experience Platform；首頁；熱門主題；流服務；API;api;delete;delete dataflows
solution: Experience Platform
title: 使用流服務API刪除資料流
type: Tutorial
description: 瞭解如何使用流服務API刪除批處理和流資料流。
exl-id: ea9040b1-3a40-493d-86f0-27deef09df07
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 2%

---

# 使用流服務API刪除資料流

您可以使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)。

本教程介紹了刪除使用批處理源和流式處理源建立的資料流的步驟 [!DNL Flow Service]。

## 快速入門

本教程要求您具有有效的流ID。 如果沒有有效的流ID，請從 [源概述](../../home.md) 在嘗試本教程之前，請按照上述步驟操作。

本教程還要求您對以下Adobe Experience Platform元件有一定的瞭解：

* [源](../../home.md): [!DNL Experience Platform] 允許從各種源接收資料，同時讓您能夠使用 [!DNL Platform] 服務。
* [沙箱](../../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙箱，將單個沙箱 [!DNL Platform] 實例到獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

### 使用平台API

有關如何成功調用平台API的資訊，請參見上的指南 [平台API入門](../../../landing/api-guide.md)。

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回HTTP狀態204（無內容）和空白正文。 您可以通過嘗試對資料流進行查找(GET)請求來確認刪除。 API將返回HTTP 404（未找到）錯誤，表示資料流已被刪除。

## 後續步驟

按照本教程，您已成功使用 [!DNL Flow Service] 刪除現有資料流的API。

有關如何使用用戶介面執行這些操作的步驟，請參閱上的教程 [刪除UI中的資料流](../../tutorials/ui/delete.md)
