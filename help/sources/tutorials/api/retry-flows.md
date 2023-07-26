---
title: 重試失敗的資料流執行
description: 瞭解如何使用流程服務API重試失敗的資料流執行。
exl-id: b9abc737-9a57-47e6-98ab-6d6c44f38d17
source-git-commit: d4dba26a151619a555a69287e182ff8398cca7b4
workflow-type: tm+mt
source-wordcount: '273'
ht-degree: 2%

---

# 重試失敗的資料流執行

>[!IMPORTANT]
>
>批次來源可支援重試失敗的資料流執行。 您只能重試失敗的資料流執行。

本教學課程涵蓋如何使用重試失敗的資料流執行的步驟。 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入門

本教學課程需要您實際瞭解下列Adobe Experience Platform元件：

* [來源](../../home.md)：Experience Platform可讓您從各種來源擷取資料，同時能夠使用來建構、加標籤及增強傳入資料 [!DNL Platform] 服務。
* [沙箱](../../../sandboxes/home.md)：Experience Platform提供對單一區域進行分割的虛擬沙箱 [!DNL Platform] 將執行個體整合至個別的虛擬環境中，協助開發及改進數位體驗應用程式。

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱以下指南： [Platform API快速入門](../../../landing/api-guide.md).

## 重試失敗的資料流執行

若要重試失敗的資料流執行，請向以下發出POST請求： `/runs` 端點，同時提供資料流的執行ID和 `re-trigger` 作業作為查詢引數的一部分。

**API格式**

```http
POST /runs/{RUN_ID}/action?op=re-trigger
```

| 參數 | 說明 |
| --- | --- |
| `{RUN_ID}` | 與您要重試的資料流執行對應的執行ID。 |
| `op` | 決定要執行之動作的作業。 若要重試失敗的資料流執行，您必須指定 `re-trigger` 作為您的作業。 |

**要求**

>[!NOTE]
>
>您可以使用 `re-trigger` 在成功的資料流執行沒有擷取記錄的情況下，重試成功的資料流執行的作業。

以下要求會重試針對執行ID執行的資料流 `4fb0418e-1804-45d6-8d56-dd51f05c0baf`.

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

成功的回應會傳回新建立的資料流執行ID及其對應的etag版本。

```json
{
    "id": "3fb0418e-1804-45d6-8d56-dd51f05c0baf",
    "etag": "\"1100c53e-0000-0200-0000-627138980000\""
}
```
