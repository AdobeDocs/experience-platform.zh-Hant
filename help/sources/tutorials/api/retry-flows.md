---
keywords: Experience Platform；首頁；熱門主題；流量服務；
title: 重試失敗的資料流運行
description: 本教學課程涵蓋如何使用流服務API重試失敗的資料流運行的步驟
source-git-commit: dfb95f457d7ddb730950159165ed85b2f532f9ab
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 2%

---

# 重試失敗的資料流運行

>[!IMPORTANT]
>
>批處理源可支援重試失敗的資料流運行。 您只能重試失敗的資料流運行。

本教學課程涵蓋如何使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入門

本教學課程需要您妥善了解下列Adobe Experience Platform元件：

* [來源](../../home.md): [!DNL Experience Platform] 可讓您從各種來源擷取資料，同時使用來建構、加標籤及增強傳入資料 [!DNL Platform] 服務。
* [沙箱](../../../sandboxes/home.md): [!DNL Experience Platform] 提供可分割單一沙箱的虛擬沙箱 [!DNL Platform] 例項放入個別的虛擬環境，以協助開發及改進數位體驗應用程式。

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱 [Platform API快速入門](../../../landing/api-guide.md).

## 重試失敗的資料流運行

要重試失敗的資料流運行，請向 `/runs` 端點，同時提供資料流和 `re-trigger` 作為查詢參數的一部分。

**API格式**

```http
POST /runs/{RUN_ID}/action?op=re-trigger
```

| 參數 | 說明 |
| --- | --- |
| `{RUN_ID}` | 與要重試的資料流運行對應的運行ID。 |
| `op` | 決定要執行的動作的操作。 要重試失敗的資料流運行，必須指定 `re-trigger` 作為您的操作。 |

**要求**

以下請求重試運行ID的資料流運行 `4fb0418e-1804-45d6-8d56-dd51f05c0baf`.

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

成功的回應會傳回新建立的流程執行ID及其對應的etag版本。

```json
{
    "id": "3fb0418e-1804-45d6-8d56-dd51f05c0baf",
    "etag": "\"1100c53e-0000-0200-0000-627138980000\""
}
```
