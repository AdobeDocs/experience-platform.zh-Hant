---
keywords: Experience Platform；設定檔；即時客戶設定檔；疑難排解；API；報表；資料集重疊報表；設定檔資料
title: 產生資料集重疊報表
type: Tutorial
description: 本教學課程概述使用即時客戶設定檔API產生資料集重疊報表所需的步驟。
exl-id: 90894ed3-b09e-435d-a9e3-18fd6dc8e907
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '884'
ht-degree: 1%

---

# 產生資料集重疊報表

資料集重疊報表可讓您清楚掌握組織的組成 [!DNL Profile] 顯示對可定址對象（設定檔）貢獻最多的資料集來儲存。

除了提供資料的深入分析外，此報表還可協助您採取動作，以最佳化授權使用，例如設定特定資料的有效期限限制。

本教學課程概述使用 [!DNL Real-Time Customer Profile] API和解譯您組織的結果。

## 快速入門

若要使用Adobe Experience Platform API，您必須先完成 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en) 以收集所需標題的值。 若要進一步了解Experience PlatformAPI，請參閱 [Platform API快速入門檔案](../../landing/api-guide.md).

本教學課程中所有API呼叫的必要標題為：

* `Authorization: Bearer {ACCESS_TOKEN}`:此 `Authorization` 標題需要以字詞為前置的存取權杖 `Bearer`. 每24小時必須產生一個新的存取權杖值。
* `x-api-key: {API_KEY}`:此 `API Key` 也稱為 `Client ID` 和值只需產生一次。
* `x-gw-ims-org-id: {ORG_ID}`:組織ID只需產生一次。

完成驗證教學課程並收集所需標題的值後，您就可以開始呼叫即時客戶API。

## 使用命令列產生資料集重疊報表

如果您熟悉使用命令列，則可使用下列cURL要求，透過執行以下GET要求來產生資料集重疊報表 `/previewsamplestatus/report/dataset/overlap`.

**要求**

下列請求會使用 `date` 參數來傳回指定日期的最新報表。

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset/overlap?date=2021-04-19 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

| 參數 | 說明 |
|---|---|
| `date` | 指定要傳回的報表日期。 如果在日期上執行了多個報表，則會傳回該日期的最新報表。 如果指定日期沒有報表，則會傳回HTTP狀態404（找不到）錯誤。 若未指定日期，則會傳回最近的報表。 格式：YYYY-MM-DD。 範例：`date=2024-12-31` |

**回應**

成功的要求會傳回HTTP狀態200（確定）和資料集重疊報表。 報表包含 `data` 物件，包含以逗號分隔的資料集清單及其個別的設定檔計數。 如需如何閱讀報表的詳細資訊，請參閱 [解譯資料集重疊報表資料](#interpret-the-report) 稍後在本教學課程中。

```json
{
    "data": {
        "5d92921872831c163452edc8,5da7292579975918a851db57,5eb2cdc6fa3f9a18a7592a98": 123,
        "5d92921872831c163452edc8,5eb2cdc6fa3f9a18a7592a98": 454412,
        "5eeda0032af7bb19162172a7": 107
    },
    "reportTimestamp": "2021-04-19T19:55:31.147"
}
```

### 使用Postman產生資料集重疊報表

Postman是API開發的協作平台，可用來視覺化API呼叫。 您可以從 [Postman網站](https://www.postman.com) 和提供易於使用的UI，用於執行API呼叫。 下列螢幕擷取畫面使用Postman介面。

**要求**

若要使用Postman請求資料集重疊報表，請完成下列步驟：

* 使用下拉式清單，選取GET作為請求類型。
* 在 `KEY` 欄：
   * `Authorization`
   * `x-api-key`
   * `x-gw-ims-org-id`
* 在 `VALUE` 欄，取代大括弧(`{{ }}`)和大括弧內的任何內容。
* 輸入請求路徑，其中包含或不包含可選 `date` 參數：
   `https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset/overlap`\
   或
   `https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset/overlap?date=YYYY-MM-DD`

| 參數 | 說明 |
|---|---|
| `date` | 指定要傳回的報表日期。 如果在日期上執行了多個報表，則會傳回該日期的最新報表。 如果指定日期沒有報表，則會傳回HTTP狀態404（找不到）錯誤。 若未指定日期，則會傳回最近的報表。 <br/>格式：YYYY-MM-DD。 範例：`date=2024-12-31` |

請求類型、標題、值和路徑完成後，請選取 **傳送** 傳送API請求並產生報表。

![](../images/dataset-overlap-report/postman-request.png)

**回應**

成功的要求會傳回HTTP狀態200（確定）和資料集重疊報表。 報表包含 `data` 物件，包含以逗號分隔的資料集清單及其個別的設定檔計數。 如需如何閱讀報表的詳細資訊，請參閱 [解譯資料集重疊報表資料](#interpret-the-report).

![](../images/dataset-overlap-report/postman-response.png)

## 解譯資料集重疊報表資料 {#interpret-the-report}

產生的資料集重疊報表會提供顯示報表日期和時間的時間戳記，以及包含以逗號分隔清單形式之資料集ID唯一組合的資料物件。 以下各節提供有關報告組成部分的其他資訊。

### 報表時間戳記

此 `reportTimestamp` 符合API請求中提供的日期，或若未提供日期，則為最近報表的時間戳記。

### 資料集ID清單

此 `data` 物件包含以逗號分隔清單的資料集ID不重複組合，以及該資料集組合的個別設定檔計數。

>[!NOTE]
>
>與資料集重疊報表每一列相關聯的所有設定檔計數總和，應與您組織中的設定檔總數相等。

若要解譯報表的結果，請考量下列範例：

```json
  "5d92921872831c163452edc8,5da7292579975918a851db57,5eb2cdc6fa3f9a18a7592a98": 123,
  "5d92921872831c163452edc8,5eb2cdc6fa3f9a18a7592a98": 454412,
  "5eeda0032af7bb19162172a7": 107
```

此報告提供下列資訊：

* 有123個設定檔，由來自下列資料集的資料組成： `5d92921872831c163452edc8`, `5da7292579975918a851db57`, `5eb2cdc6fa3f9a18a7592a98`.
* 來自這兩個資料集的資料共454,412個設定檔： `5d92921872831c163452edc8` 和 `5eb2cdc6fa3f9a18a7592a98`.
* 有107個設定檔僅由資料集的資料組成 `5eeda0032af7bb19162172a7`.
* 組織中共有454,642個設定檔。

## 後續步驟

完成本教學課程後，您現在可以使用即時客戶設定檔API產生資料集重疊報表。 若要進一步了解如何在API和Experience PlatformUI中使用設定檔資料，請先閱讀 [設定檔概述檔案](../home.md).
