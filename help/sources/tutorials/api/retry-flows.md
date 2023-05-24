---
keywords: Experience Platform；首頁；熱門主題；流式服務；
title: 重試失敗的資料流運行
description: 本教程介紹如何使用流服務API重試失敗的資料流運行的步驟
exl-id: b9abc737-9a57-47e6-98ab-6d6c44f38d17
source-git-commit: a9887535b12b8c4aeb39bb5a6646da88db4f0308
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 2%

---

# 重試失敗的資料流運行

>[!IMPORTANT]
>
>批處理源支援重試失敗的資料流運行。 您只能重試失敗的資料流運行。

本教程介紹如何使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)。

## 快速入門

本教程要求您對以下Adobe Experience Platform元件有一定的瞭解：

* [源](../../home.md): [!DNL Experience Platform] 允許從各種源接收資料，同時讓您能夠使用 [!DNL Platform] 服務。
* [沙箱](../../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙箱，將單個沙箱 [!DNL Platform] 實例到獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

### 使用平台API

有關如何成功調用平台API的資訊，請參見上的指南 [平台API入門](../../../landing/api-guide.md)。

## 重試失敗的資料流運行

要重試失敗的資料流運行，請向 `/runs` 端點，同時提供資料流和 `re-trigger` 作為查詢參數的一部分。

**API格式**

```http
POST /runs/{RUN_ID}/action?op=re-trigger
```

| 參數 | 說明 |
| --- | --- |
| `{RUN_ID}` | 與要重試的資料流運行相對應的運行ID。 |
| `op` | 確定要執行的操作的操作。 要重試失敗的資料流運行，必須指定 `re-trigger` 作為你的行動。 |

**要求**

以下請求將重試運行ID的資料流運行 `4fb0418e-1804-45d6-8d56-dd51f05c0baf`。

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/runs/4fb0418e-1804-45d6-8d56-dd51f05c0baf/action?op=re-trigger' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json'
```

**回應**

成功的響應返回新建立的流運行ID及其相應的etag版本。

```json
{
    "id": "3fb0418e-1804-45d6-8d56-dd51f05c0baf",
    "etag": "\"1100c53e-0000-0200-0000-627138980000\""
}
```
