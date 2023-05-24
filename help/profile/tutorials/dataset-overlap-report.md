---
keywords: Experience Platform；配置檔案；即時客戶配置檔案；故障排除；API;reporting；資料集重疊報告；配置檔案資料
title: 生成資料集重疊報告
type: Tutorial
description: 本教程概括介紹了使用即時客戶配置檔案API生成資料集重疊報告所需的步驟。
exl-id: 90894ed3-b09e-435d-a9e3-18fd6dc8e907
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '884'
ht-degree: 1%

---

# 生成資料集重疊報告

資料集重疊報告可查看組織的組成 [!DNL Profile] 通過公開對可定址的受眾（配置檔案）貢獻最大的資料集來儲存。

除了提供對資料的洞察力外，此報告還可以幫助您採取措施來優化許可證使用，例如設定某些資料的使用壽命限制。

本教程概括介紹了使用 [!DNL Real-Time Customer Profile] API並解釋組織的結果。

## 快速入門

要使用Adobe Experience PlatformAPI，必須先完成 [驗證教程](https://www.adobe.com/go/platform-api-authentication-en) 以收集所需標題所需的值。 要瞭解有關Experience PlatformAPI的詳細資訊，請參閱 [平台API文檔入門](../../landing/api-guide.md)。

本教程中所有API調用的必需標頭包括：

* `Authorization: Bearer {ACCESS_TOKEN}`:的 `Authorization` 頭需要以單詞為前置詞的訪問令牌 `Bearer`。 必須每24小時生成一個新訪問令牌值。
* `x-api-key: {API_KEY}`:的 `API Key` 也稱為a `Client ID` 並且是只需生成一次的值。
* `x-gw-ims-org-id: {ORG_ID}`:組織ID只需生成一次。

完成身份驗證教程並收集所需標頭的值後，您就可以開始調用即時客戶API。

## 使用命令行生成資料集重疊報告

如果您熟悉使用命令行，可以通過執行GET請求來使用以下cURL請求來生成資料集重疊報告 `/previewsamplestatus/report/dataset/overlap`。

**要求**

以下請求使用 `date` 參數，以返回指定日期的最新報表。

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset/overlap?date=2021-04-19 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

| 參數 | 說明 |
|---|---|
| `date` | 指定要返回的報告的日期。 如果在該日期運行了多個報表，則返回該日期的最新報表。 如果指定日期不存在報告，則返回HTTP狀態404（未找到）錯誤。 如果未指定日期，則返回最近的報告。 格式：YYYY-MM-DD。 範例：`date=2024-12-31` |

**回應**

成功的請求返回HTTP狀態200(OK)和資料集重疊報告。 報告包括 `data` 對象，包含以逗號分隔的資料集清單及其各自的配置檔案計數。 有關如何閱讀報告的詳細資訊，請參閱 [解釋資料集重疊報告資料](#interpret-the-report) 在本教程的後面。

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

### 使用Postman生成資料集重疊報告

Postman是API開發的協作平台，對API調用的可視化非常有用。 可以從 [Postman網站](https://www.postman.com) 並提供了一個易於使用的UI，用於執行API調用。 以下螢幕截圖使用Postman介面。

**要求**

要使用Postman請求資料集重疊報告，請完成以下步驟：

* 使用下拉清單，選擇GET作為請求類型。
* 在 `KEY` 列：
   * `Authorization`
   * `x-api-key`
   * `x-gw-ims-org-id`
* 將驗證期間生成的值輸入到 `VALUE` 列，替換大括弧(`{{ }}`)和大括弧中的任何內容。
* 輸入帶可選路徑或不帶可選路徑的請求路徑 `date` 參數：
   `https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset/overlap`\
   或
   `https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset/overlap?date=YYYY-MM-DD`

| 參數 | 說明 |
|---|---|
| `date` | 指定要返回的報告的日期。 如果在該日期運行了多個報表，則返回該日期的最新報表。 如果指定日期不存在報告，則返回HTTP狀態404（未找到）錯誤。 如果未指定日期，則返回最近的報告。 <br/>格式：YYYY-MM-DD。 範例：`date=2024-12-31` |

請求類型、標頭、值和路徑完成後，選擇 **發送** 發送API請求並生成報告。

![](../images/dataset-overlap-report/postman-request.png)

**回應**

成功的請求返回HTTP狀態200(OK)和資料集重疊報告。 報告包括 `data` 對象，包含以逗號分隔的資料集清單及其各自的配置檔案計數。 有關如何閱讀報告的詳細資訊，請參閱 [解釋資料集重疊報告資料](#interpret-the-report)。

![](../images/dataset-overlap-report/postman-response.png)

## 解釋資料集重疊報表資料 {#interpret-the-report}

生成的資料集重疊報告提供了顯示報告日期和時間的時間戳以及包含資料集ID的唯一組合作為逗號分隔清單的資料對象。 以下各節提供了有關報告各組成部分的補充資訊。

### 報表時間戳

的 `reportTimestamp` 與API請求中提供的日期匹配，或者如果未提供日期，則與最近報告的時間戳匹配。

### 資料集ID清單

的 `data` 對象包括作為逗號分隔清單的資料集ID的唯一組合以及該資料集組合的相應配置檔案計數。

>[!NOTE]
>
>與資料集重疊報告的每一行關聯的所有配置檔案計數的總和應等於組織中配置檔案總數。

要解釋報告結果，請考慮以下示例：

```json
  "5d92921872831c163452edc8,5da7292579975918a851db57,5eb2cdc6fa3f9a18a7592a98": 123,
  "5d92921872831c163452edc8,5eb2cdc6fa3f9a18a7592a98": 454412,
  "5eeda0032af7bb19162172a7": 107
```

此報表提供以下資訊：

* 有123個配置檔案，包括來自以下資料集的資料： `5d92921872831c163452edc8`。 `5da7292579975918a851db57`。 `5eb2cdc6fa3f9a18a7592a98`。
* 共有454,412個配置檔案包含來自這兩個資料集的資料： `5d92921872831c163452edc8` 和 `5eb2cdc6fa3f9a18a7592a98`。
* 有107個配置檔案僅包含來自資料集的資料 `5eeda0032af7bb19162172a7`。
* 該組織共有454 642份檔案。

## 後續步驟

完成本教程後，您現在可以使用Real-Time Customer Profile API生成資料集重疊報告。 要瞭解有關在API和Experience PlatformUI中使用配置檔案資料的更多資訊，請首先閱讀 [概述文檔](../home.md)。
