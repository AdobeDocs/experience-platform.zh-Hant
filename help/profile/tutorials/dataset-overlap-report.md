---
keywords: Experience Platform；概要檔案；即時客戶概要檔案；故障排除； API；報告；資料集重疊報告；概要檔案資料
title: 產生資料集重疊報表
type: Tutorial
description: 本教學課程概述使用即時客戶設定檔API產生資料集重疊報表的必要步驟。
source-git-commit: f30f87527f5e903c851a140e7cbaad1964a48803
workflow-type: tm+mt
source-wordcount: '888'
ht-degree: 1%

---


# 產生資料集重疊報表

資料集重疊報表揭露對您可定址對象（設定檔）貢獻最大的資料集，讓您能夠洞悉組織[!DNL Profile]商店的構成。

除了提供資料的深入資訊外，此報告還可協助您採取行動以最佳化授權使用，例如設定特定資料的使用期限限制。

本教學課程概述使用[!DNL Real-time Customer Profile] API產生資料集重疊報表並解譯組織結果的必要步驟。

## 快速入門

若要使用Adobe Experience PlatformAPI，您必須先完成[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)，以收集所需標題的值。 若要進一步瞭解Experience PlatformAPI，請參閱[平台API說明檔案](../../landing/api-guide.md)快速入門。

本教學課程中所有API呼叫的必要標題為：

* `Authorization: Bearer {ACCESS_TOKEN}`:標題 `Authorization` 需要字詞前置的存取Token `Bearer`。必須每24小時產生一個新的存取Token值。
* `x-api-key: {API_KEY}`:也 `API Key` 稱為a, `Client ID` 是只需產生一次的值。
* `x-gw-ims-org-id: {IMS_ORG}`:這 `IMS Org` 也稱為，只 `Organization ID` 需產生一次。

完成驗證教學課程並收集必要標題的值後，您就可以開始呼叫即時客戶API。

## 使用命令列產生資料集重疊報表

如果您熟悉使用命令列，可以使用下列cURL請求，透過對`/previewsamplestatus/report/dataset/overlap`執行GET請求來產生資料集重疊報表。

**要求**

下列請求使用`date`參數，傳回指定日期的最新報表。

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset/overlap?date=2021-04-19 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

| 參數 | 說明 |
|---|---|
| `date` | 指定要傳回的報表日期。 如果在該日期執行了多份報表，則會傳回該日期的最新報表。 如果報表在指定日期不存在，則會傳回HTTP狀態404（找不到）錯誤。 如果未指定日期，則會傳回最近的報表。 格式：YYYY-MM-DD。 範例：`date=2024-12-31` |

**回應**

成功的請求會傳回HTTP狀態200（確定）和資料集重疊報表。 該報表包含`data`物件，包含以逗號分隔的資料集清單及其個別的描述檔計數。 如需如何讀取報表的詳細資訊，請參閱本教學課程稍後說明資料集重疊報表資料](#interpret-the-report)的章節。[

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

Postman是API開發的協作平台，對於視覺化API呼叫非常有用。 您可從[Postman網站](https://www.postman.com)免費下載它，並提供簡單易用的UI來執行API呼叫。 以下螢幕擷取畫面使用Postman介面。

**要求**

若要使用Postman請求資料集重疊報表，請完成下列步驟：

* 使用下拉式清單，選取「GET」作為請求類型。
* 在`KEY`欄中輸入所需標題：
   * `Authorization`
   * `x-api-key`
   * `x-gw-ims-org-id`
* 在`VALUE`欄中輸入驗證期間生成的值，替換大括弧(`{{ }}`)和大括弧內的任何內容。
* 輸入具有或不具有可選`date`參數的請求路徑：
   `https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset/overlap`\
   或
   `https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset/overlap?date=YYYY-MM-DD`

| 參數 | 說明 |
|---|---|
| `date` | 指定要傳回的報表日期。 如果在該日期執行了多份報表，則會傳回該日期的最新報表。 如果報表在指定日期不存在，則會傳回HTTP狀態404（找不到）錯誤。 如果未指定日期，則會傳回最近的報表。 <br/>格式：YYYY-MM-DD。範例：`date=2024-12-31` |

完成請求類型、標題、值和路徑後，選擇&#x200B;**Send**&#x200B;以傳送API請求並產生報表。

![](../images/dataset-overlap-report/postman-request.png)

**回應**

成功的請求會傳回HTTP狀態200（確定）和資料集重疊報表。 該報表包含`data`物件，包含以逗號分隔的資料集清單及其個別的描述檔計數。 如需如何讀取報表的詳細資訊，請參閱[解讀資料集重疊報表資料的章節](#interpret-the-report)。

![](../images/dataset-overlap-report/postman-response.png)

## 解譯資料集重疊報表資料{#interpret-the-report}

產生的資料集重疊報表提供顯示報表日期和時間的時間戳記，以及包含資料集ID的唯一組合（以逗號分隔的清單）的資料物件。 以下各節提供有關報表元件的其他資訊。

### 報表時間戳記

`reportTimestamp`符合API請求中提供的日期，或如果未提供日期，則符合最近報表的時間戳記。

### 資料集ID清單

`data`物件包含以逗號分隔的清單形式的資料集ID的唯一組合，以及該資料集組合的個別描述檔計數。

>[!NOTE]
>
>與資料集重疊報表的每一列相關聯的所有描述檔計數總和，應等於您組織中的描述檔總數。

若要解譯報表的結果，請考慮下列範例：

```json
  "5d92921872831c163452edc8,5da7292579975918a851db57,5eb2cdc6fa3f9a18a7592a98": 123,
  "5d92921872831c163452edc8,5eb2cdc6fa3f9a18a7592a98": 454412,
  "5eeda0032af7bb19162172a7": 107
```

此報表提供下列資訊：
* 共有123個描述檔，包括來自下列資料集的資料：`5d92921872831c163452edc8`、`5da7292579975918a851db57`、`5eb2cdc6fa3f9a18a7592a98`。
* 共有454,412個描述檔，由來自這兩個資料集的資料組成：`5d92921872831c163452edc8`和`5eb2cdc6fa3f9a18a7592a98`。
* 有107個描述檔僅包含來自資料集`5eeda0032af7bb19162172a7`的資料。
* 組織中共有454,642個個人檔案。

## 後續步驟

完成本教學課程後，您現在可以使用即時客戶設定檔API產生資料集重疊報表。 若要進一步瞭解如何在API和Experience PlatformUI中使用描述檔資料，請先閱讀[描述檔概述檔案](../home.md)。