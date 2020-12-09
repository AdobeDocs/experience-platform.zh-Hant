---
keywords: Experience Platform;home;popular topics;flow service;API;api;delete;delete dataflows
solution: Experience Platform
title: 使用流服務API刪除資料流
topic: overview
type: Tutorial
description: 本教學課程涵蓋使用Flow Service API刪除批次和串流資料流的步驟。
translation-type: tm+mt
source-git-commit: b63b17f2a7271fc673abc8245a4917c0daca4ef3
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 1%

---


# 使用流服務API刪除資料流

您可以使用 [[!DNL Flow Service] API刪除包含錯誤或已過時的批處理和流資料流](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml)。

本教程介紹使用批處理源和流源刪除資料流的步驟 [!DNL Flow Service]。

## 快速入門

本教學課程要求您必須擁有有效的流程ID。 如果您沒有有效的流程ID，請從來源概觀中選取您選擇的連 [接器](../../home.md) ，並依照本教學課程前所述的步驟進行。

本教學課程也要求您對Adobe Experience Platform的下列元件有正確的認識：

* [來源](../../home.md): [!DNL Experience Platform] 允許從各種來源接收資料，同時提供使用服務構建、標籤和增強傳入資料的 [!DNL Platform] 能力。
* [沙盒](../../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙盒，可將單一執行個體分 [!DNL Platform] 割為不同的虛擬環境，以協助開發和發展數位體驗應用程式。

以下各節提供您需要知道的其他資訊，以便使用 [!DNL Flow Service] API成功刪除資料流。

### 讀取範例API呼叫

本教學課程提供範例API呼叫，以示範如何設定請求的格式。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱疑難排解指 [南中有關如何讀取範例API呼叫的](../../../landing/troubleshooting.md#how-do-i-format-an-api-request)[!DNL Experience Platform] 章節。

### 收集必要標題的值

若要呼叫API，您必 [!DNL Platform] 須先完成驗證教 [學課程](../../../tutorials/authentication.md)。 完成驗證教學課程後，將提供所有 [!DNL Experience Platform] API呼叫中每個必要標題的值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

中的所有資 [!DNL Experience Platform]源(包括屬於這些資源 [!DNL Flow Service])都隔離到特定的虛擬沙盒。 對API的所 [!DNL Platform] 有請求都需要一個標題，該標題會指定要在中執行的操作的沙盒名稱：

* `x-sandbox-name: {SANDBOX_NAME}`

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的媒體類型標題：

* `Content-Type: application/json`

## 刪除資料流

使用現有流ID，您可以通過對 [!DNL Flow Service] API執行DELETE請求來刪除資料流。

**API格式**

```http
DELETE /flows/{FLOW_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{FLOW_ID}` | 要刪除 `id` 的資料流的唯一值。 |

**請求**

```shell
curl -X DELETE \
    'https://platform-int.adobe.io/data/foundation/flowservice/flows/20c115bc-46e3-40f3-bfe9-fb25abe4ba76' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態204（無內容）和空白的內文。 您可以嘗試對資料流執行查找(GET)請求，以確認刪除。 API將返回HTTP 404（找不到）錯誤，表示資料流已被刪除。

## 後續步驟

按照本教程，您已成功使用 [!DNL Flow Service] API刪除現有資料流。

有關如何使用用戶介面執行這些操作的步驟，請參閱UI中有關刪 [除資料流的教程](../../tutorials/ui/delete.md)
