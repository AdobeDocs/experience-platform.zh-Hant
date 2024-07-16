---
keywords: Experience Platform；首頁；熱門主題；流程服務；刪除帳戶；刪除；API
solution: Experience Platform
title: 使用流程服務API刪除帳戶
type: Tutorial
description: 瞭解如何使用Flow Service API刪除帳戶。
exl-id: 3d07ab7d-c012-472e-8db4-b19e3936dcba
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 2%

---

# 使用流程服務API刪除帳戶

您可以使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)刪除包含錯誤或已過時的來源帳戶。

請參閱下列教學課程，以瞭解如何使用API刪除帳戶的步驟。

## 快速入門

本教學課程要求您具備有效的連線ID。 如果您沒有有效的連線ID，請從[來源概觀](../../home.md)中選取您選擇的連線器，並依照在嘗試本教學課程之前概述的步驟進行。

本教學課程也要求您實際瞭解下列Adobe Experience Platform元件：

* [來源](../../home.md)： [!DNL Experience Platform]允許從各種來源擷取資料，同時讓您能夠使用[!DNL Platform]服務來建構、加標籤以及增強傳入的資料。
* [沙箱](../../../sandboxes/home.md)： [!DNL Experience Platform]提供可將單一[!DNL Platform]執行個體分割成個別虛擬環境的虛擬沙箱，以利開發及改進數位體驗應用程式。

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱[Platform API快速入門](../../../landing/api-guide.md)的指南。

## 刪除帳戶

>[!TIP]
>
>在刪除來源帳戶之前，您必須先刪除與來源帳戶關聯的任何現有資料流。 若要刪除現有的資料流，請參閱有關[刪除來源資料流](./delete-dataflows.md)的教學課程。

若要刪除帳戶，請提供與您要刪除的帳戶對應的基礎連線ID時，向[!DNL Flow Service] API提出DELETE要求。

**API格式**

```http
DELETE /connections/{BASE_CONNECTION_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 您要刪除之來源帳戶的基本連線ID。 |

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

成功的回應會傳回HTTP狀態204 （無內容）和空白內文。

您可以嘗試對連線進行查詢(GET)來確認刪除。

## 後續步驟

依照此教學課程，您已成功使用[!DNL Flow Service] API刪除現有帳戶。

如需有關如何使用使用者介面執行這些操作的步驟，請參閱有關在UI](../../tutorials/ui/delete-accounts.md)中刪除帳戶[的教學課程。
