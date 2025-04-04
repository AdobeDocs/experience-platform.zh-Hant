---
keywords: Experience Platform；首頁；熱門主題；流程服務；API；API；刪除；刪除資料流程
solution: Experience Platform
title: 使用流程服務API刪除資料流
type: Tutorial
description: 瞭解如何使用流量服務API刪除批次和串流資料流。
exl-id: ea9040b1-3a40-493d-86f0-27deef09df07
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 2%

---

# 使用流程服務API刪除資料流

您可以使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)刪除含有錯誤或已作廢的批次和串流資料流。

本教學課程涵蓋刪除使用[!DNL Flow Service]的批次和串流來源資料流的步驟。

## 快速入門

本教學課程要求您具備有效的流量ID。 如果您沒有有效的流量ID，請從[來源概觀](../../home.md)中選取您選擇的聯結器，並依照在嘗試本教學課程之前概述的步驟進行。

本教學課程也要求您實際瞭解下列Adobe Experience Platform元件：

* [來源](../../home.md)： [!DNL Experience Platform]允許從各種來源擷取資料，同時讓您能夠使用[!DNL Experience Platform]服務來建構、加標籤以及增強傳入的資料。
* [沙箱](../../../sandboxes/home.md)： [!DNL Experience Platform]提供可將單一[!DNL Experience Platform]執行個體分割成個別虛擬環境的虛擬沙箱，以利開發及改進數位體驗應用程式。

### 使用Experience Platform API

如需如何成功呼叫Experience Platform API的詳細資訊，請參閱[Experience Platform API快速入門](../../../landing/api-guide.md)指南。

## 刪除資料流

使用現有的流量ID，您可以透過對[!DNL Flow Service] API執行DELETE請求來刪除資料流。

**API格式**

```http
DELETE /flows/{FLOW_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{FLOW_ID}` | 您要刪除之資料流的唯一`id`值。 |

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

成功的回應會傳回HTTP狀態204 （無內容）和空白內文。 您可以嘗試對資料流進行查詢(GET)請求以確認刪除。 此API將傳回HTTP 404 （找不到）錯誤，這表示資料流已刪除。

## 後續步驟

依照此教學課程，您已成功使用[!DNL Flow Service] API刪除現有的資料流。

如需有關如何使用使用者介面執行這些操作的步驟，請參閱有關[在UI中刪除資料流](../../tutorials/ui/delete.md)的教學課程
