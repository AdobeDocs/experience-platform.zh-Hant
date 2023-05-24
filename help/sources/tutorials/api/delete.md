---
keywords: Experience Platform；首頁；熱門主題；流式服務；刪除帳戶；delete;api
solution: Experience Platform
title: 使用流服務API刪除帳戶
type: Tutorial
description: 瞭解如何使用流服務API刪除帳戶。
exl-id: 3d07ab7d-c012-472e-8db4-b19e3936dcba
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 2%

---

# 使用流服務API刪除帳戶

您可以使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)。

有關如何使用API刪除帳戶的步驟，請參見以下教程。

## 快速入門

本教程要求您具有有效的連接ID。 如果您沒有有效的連接ID，請從 [源概述](../../home.md) 在嘗試本教程之前，請按照上述步驟操作。

本教程還要求您對以下Adobe Experience Platform元件有一定的瞭解：

* [源](../../home.md): [!DNL Experience Platform] 允許從各種源接收資料，同時讓您能夠使用 [!DNL Platform] 服務。
* [沙箱](../../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙箱，將單個沙箱 [!DNL Platform] 實例到獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

### 使用平台API

有關如何成功調用平台API的資訊，請參見上的指南 [平台API入門](../../../landing/api-guide.md)。

## 刪除帳戶

>[!TIP]
>
>在刪除源帳戶之前，必須先刪除與源帳戶關聯的任何現有資料流。 要刪除現有資料流，請參閱上的教程 [刪除源資料流](./delete-dataflows.md)。

要刪除帳戶，請向 [!DNL Flow Service] API，同時提供與要刪除的帳戶對應的基本連接ID。

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

成功的響應返回HTTP狀態204（無內容）和空白正文。

您可以通過嘗試查找(GET)連接請求來確認刪除。

## 後續步驟

按照本教程，您已成功使用 [!DNL Flow Service] 用於刪除現有帳戶的API。

有關如何使用用戶介面執行這些操作的步驟，請參閱上的教程 [刪除UI中的帳戶](../../tutorials/ui/delete-accounts.md)。
