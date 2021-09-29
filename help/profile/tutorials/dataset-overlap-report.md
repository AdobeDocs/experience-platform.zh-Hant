---
keywords: Experience Platform；設定檔；即時客戶設定檔；疑難排解；API；報表；資料集重疊報表；設定檔資料
title: 產生資料集重疊報表
type: Tutorial
description: 本教學課程概述使用即時客戶設定檔API產生資料集重疊報表所需的步驟。
exl-id: 90894ed3-b09e-435d-a9e3-18fd6dc8e907
source-git-commit: 3b34cf37182ae98545651a7b54f586df7d811f34
workflow-type: tm+mt
source-wordcount: '888'
ht-degree: 1%

---

# 產生資料集重疊報表

資料集重疊報表會顯示對可定址對象（設定檔）貢獻最大的資料集，以顯示貴組織[!DNL Profile]存放區的組成。

除了提供資料的深入分析外，此報表還可協助您採取動作，以最佳化授權使用，例如設定特定資料的有效期限限制。

本教學課程概述使用[!DNL Real-time Customer Profile] API產生資料集重疊報表並解譯組織結果所需的步驟。

## 快速入門

若要使用Adobe Experience Platform API，您必須先完成[authentication教學課程](https://www.adobe.com/go/platform-api-authentication-en)，以收集所需標題的值。 若要深入了解Experience PlatformAPI，請參閱[Platform API說明檔案快速入門](../../landing/api-guide.md)。

本教學課程中所有API呼叫的必要標題為：

* `Authorization: Bearer {ACCESS_TOKEN}`:標 `Authorization` 題需要以字詞為前置的存取權 `Bearer`杖。每24小時必須產生一個新的存取權杖值。
* `x-api-key: {API_KEY}`:也 `API Key` 稱為， `Client ID` 且是只需產生一次的值。
* `x-gw-ims-org-id: {IMS_ORG}`:也 `IMS Org` 稱為，只 `Organization ID` 需產生一次。

完成驗證教學課程並收集所需標題的值後，您就可以開始呼叫即時客戶API。

## 使用命令列產生資料集重疊報表

如果您熟悉使用命令列，可以透過對`/previewsamplestatus/report/dataset/overlap`執行GET要求，使用下列cURL要求來產生資料集重疊報表。

**要求**

下列請求會使用`date`參數，傳回指定日期的最新報表。

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset/overlap?date=2021-04-19 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

| 參數 | 說明 |
|---|---|
| `date` | 指定要傳回的報表日期。 如果在日期上執行了多個報表，則會傳回該日期的最新報表。 如果指定日期沒有報表，則會傳回HTTP狀態404（找不到）錯誤。 若未指定日期，則會傳回最近的報表。 格式：YYYY-MM-DD。 範例: `date=2024-12-31` |

**回應**

成功的要求會傳回HTTP狀態200（確定）和資料集重疊報表。 報表包含`data`物件，包含以逗號分隔的資料集清單及其個別設定檔計數。 如需如何讀取報表的詳細資訊，請參閱本教學課程稍後的[解譯資料集重疊報表資料的區段](#interpret-the-report)。

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

Postman是API開發的協作平台，可用來視覺化API呼叫。 您可從[Postman網站](https://www.postman.com)免費下載此UI，並提供執行API呼叫的簡單易用UI。 以下螢幕截圖使用Postman介面。

**要求**

若要使用Postman請求資料集重疊報表，請完成下列步驟：

* 使用下拉式清單，選取GET作為請求類型。
* 在`KEY`欄中輸入所需標題：
   * `Authorization`
   * `x-api-key`
   * `x-gw-ims-org-id`
* 在`VALUE`欄中輸入驗證期間生成的值，替換大括弧(`{{ }}`)和大括弧內的任何內容。
* 輸入有無可選`date`參數的請求路徑：
   `https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset/overlap`\
   或
   `https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset/overlap?date=YYYY-MM-DD`

| 參數 | 說明 |
|---|---|
| `date` | 指定要傳回的報表日期。 如果在日期上執行了多個報表，則會傳回該日期的最新報表。 如果指定日期沒有報表，則會傳回HTTP狀態404（找不到）錯誤。 若未指定日期，則會傳回最近的報表。 <br/>格式：YYYY-MM-DD。範例: `date=2024-12-31` |

完成請求類型、標題、值和路徑後，選取&#x200B;**Send**&#x200B;以傳送API請求並產生報表。

![](../images/dataset-overlap-report/postman-request.png)

**回應**

成功的要求會傳回HTTP狀態200（確定）和資料集重疊報表。 報表包含`data`物件，包含以逗號分隔的資料集清單及其個別設定檔計數。 如需如何讀取報表的詳細資訊，請參閱[解譯資料集重疊報表資料的區段](#interpret-the-report)。

![](../images/dataset-overlap-report/postman-response.png)

## 解譯資料集重疊報表資料 {#interpret-the-report}

產生的資料集重疊報表會提供顯示報表日期和時間的時間戳記，以及包含以逗號分隔清單形式之資料集ID唯一組合的資料物件。 以下各節提供有關報告組成部分的其他資訊。

### 報表時間戳記

`reportTimestamp`符合API請求中提供的日期，或如果未提供日期，則符合最近報表的時間戳記。

### 資料集ID清單

`data`物件包含以逗號分隔的清單之資料集ID的唯一組合，以及該資料集組合的個別設定檔計數。

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

* 有123個設定檔，由來自下列資料集的資料組成：`5d92921872831c163452edc8`、`5da7292579975918a851db57`、`5eb2cdc6fa3f9a18a7592a98`。
* 來自這兩個資料集的資料共454,412個設定檔：`5d92921872831c163452edc8`和`5eb2cdc6fa3f9a18a7592a98`。
* 有107個設定檔僅由資料集`5eeda0032af7bb19162172a7`中的資料組成。
* 組織中共有454,642個設定檔。

## 後續步驟

完成本教學課程後，您現在可以使用即時客戶設定檔API產生資料集重疊報表。 若要進一步了解如何在API和Experience PlatformUI中使用設定檔資料，請先閱讀[設定檔概述檔案](../home.md)。
