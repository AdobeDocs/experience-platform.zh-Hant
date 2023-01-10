---
keywords: Experience Platform；首頁；熱門主題；流程服務；刪除帳戶；刪除；API
solution: Experience Platform
title: 使用流量服務API刪除帳戶
type: Tutorial
description: 了解如何使用流量服務API刪除帳戶。
exl-id: 3d07ab7d-c012-472e-8db4-b19e3936dcba
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 2%

---

# 使用流量服務API刪除帳戶

您可以刪除包含錯誤或已使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

請參閱下列教學課程，了解如何使用API刪除帳戶的步驟。

## 快速入門

本教學課程要求您具備有效的連線ID。 如果您沒有有效的連線ID，請從 [來源概觀](../../home.md) 並遵循在嘗試本教學課程之前概述的步驟。

本教學課程也需要您妥善了解下列Adobe Experience Platform元件：

* [來源](../../home.md): [!DNL Experience Platform] 可讓您從各種來源擷取資料，同時使用來建構、加標籤及增強傳入資料 [!DNL Platform] 服務。
* [沙箱](../../../sandboxes/home.md): [!DNL Experience Platform] 提供可分割單一沙箱的虛擬沙箱 [!DNL Platform] 例項放入個別的虛擬環境，以協助開發及改進數位體驗應用程式。

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱 [Platform API快速入門](../../../landing/api-guide.md).

## 刪除帳戶

>[!TIP]
>
>在刪除源帳戶之前，必須先刪除與源帳戶關聯的任何現有資料流。 要刪除現有資料流，請參閱 [刪除源資料流](./delete-dataflows.md).

若要刪除帳戶，請向 [!DNL Flow Service] API，同時提供與您要刪除之帳戶對應的基本連線ID。

**API格式**

```http
DELETE /connections/{BASE_CONNECTION_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 要刪除的源帳戶的基本連接ID。 |

**要求**

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/flowservice/connections/dd3631cd-d0ea-4fea-b631-cdd0ea6fea21' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態204（無內容）和空白內文。

您可以嘗試對連線進行查詢(GET)以確認刪除。

## 後續步驟

依照本教學課程，您已成功使用 [!DNL Flow Service] 刪除現有帳戶的API。

有關如何使用用戶介面執行這些操作的步驟，請參閱 [刪除UI中的帳戶](../../tutorials/ui/delete-accounts.md).
