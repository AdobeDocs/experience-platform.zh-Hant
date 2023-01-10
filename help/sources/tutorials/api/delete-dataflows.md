---
keywords: Experience Platform；首頁；熱門主題；流程服務；API;API；刪除；刪除資料流
solution: Experience Platform
title: 使用流服務API刪除資料流
type: Tutorial
description: 了解如何使用流服務API刪除批處理資料流和流資料流。
exl-id: ea9040b1-3a40-493d-86f0-27deef09df07
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 2%

---

# 使用流服務API刪除資料流

您可以刪除包含錯誤或已使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

本教學課程涵蓋使用批次和串流來源刪除資料流的步驟 [!DNL Flow Service].

## 快速入門

本教學課程需要您具備有效的流程ID。 如果您沒有有效的流量ID，請從 [來源概觀](../../home.md) 並遵循在嘗試本教學課程之前概述的步驟。

本教學課程也需要您妥善了解下列Adobe Experience Platform元件：

* [來源](../../home.md): [!DNL Experience Platform] 可讓您從各種來源擷取資料，同時使用來建構、加標籤及增強傳入資料 [!DNL Platform] 服務。
* [沙箱](../../../sandboxes/home.md): [!DNL Experience Platform] 提供可分割單一沙箱的虛擬沙箱 [!DNL Platform] 例項放入個別的虛擬環境，以協助開發及改進數位體驗應用程式。

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱 [Platform API快速入門](../../../landing/api-guide.md).

## 刪除資料流

使用現有流ID，您可以通過執行DELETE請求來刪除資料流 [!DNL Flow Service] API。

**API格式**

```http
DELETE /flows/{FLOW_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{FLOW_ID}` | 唯一 `id` 值。 |

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

成功的回應會傳回HTTP狀態204（無內容）和空白內文。 您可以嘗試對資料流執行查閱(GET)請求以確認刪除。 API會傳回HTTP 404（找不到）錯誤，指出資料流已刪除。

## 後續步驟

依照本教學課程，您已成功使用 [!DNL Flow Service] 刪除現有資料流的API。

有關如何使用用戶介面執行這些操作的步驟，請參閱 [刪除UI中的資料流](../../tutorials/ui/delete.md)
