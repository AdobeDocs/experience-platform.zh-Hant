---
title: 重試失敗的資料流執行
description: 瞭解如何使用流程服務API重試失敗的資料流執行。
exl-id: b9abc737-9a57-47e6-98ab-6d6c44f38d17
source-git-commit: d4dba26a151619a555a69287e182ff8398cca7b4
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 2%

---

# 重試失敗的資料流執行

>[!IMPORTANT]
>
>批次來源可支援重試失敗的資料流執行。 您只能重試失敗的資料流執行。

本教學課程涵蓋如何使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)重試失敗的資料流執行的步驟。

## 快速入門

本教學課程需要您實際瞭解下列Adobe Experience Platform元件：

* [來源](../../home.md)：Experience Platform允許從各種來源擷取資料，同時讓您能夠使用[!DNL Platform]服務來建構、加標籤以及增強傳入的資料。
* [沙箱](../../../sandboxes/home.md)：Experience Platform提供可將單一[!DNL Platform]執行個體分割成個別虛擬環境的虛擬沙箱，以利開發及改進數位體驗應用程式。

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱[Platform API快速入門](../../../landing/api-guide.md)的指南。

## 重試失敗的資料流執行

若要重試失敗的資料流執行，請在提供資料流的執行ID及`re-trigger`作業作為查詢引數的一部分時，向`/runs`端點提出POST要求。

**API格式**

```http
POST /runs/{RUN_ID}/action?op=re-trigger
```

| 參數 | 說明 |
| --- | --- |
| `{RUN_ID}` | 與您要重試的資料流執行對應的執行ID。 |
| `op` | 決定要執行之動作的作業。 若要重試失敗的資料流執行，您必須指定`re-trigger`作為作業。 |

**要求**

>[!NOTE]
>
>您也可使用`re-trigger`作業重試成功的資料流執行，因為成功的資料流執行沒有擷取的記錄。

下列要求會重試執行ID `4fb0418e-1804-45d6-8d56-dd51f05c0baf`的資料流執行。

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
