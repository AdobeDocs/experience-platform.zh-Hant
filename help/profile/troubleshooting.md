---
keywords: Experience Platform；設定檔；即時客戶設定檔；疑難排解；API
title: 即時客戶個人檔案疑難排解指南
type: Documentation
description: 本檔案提供關於即時客戶設定檔常見問題的解答，以及使用Adobe Experience Platform處理設定檔資料時常見錯誤的疑難排解指南。
exl-id: 0b340025-093b-41e4-8053-969a8e80e889
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '1007'
ht-degree: 0%

---

# 即時客戶個人檔案疑難排解指南

本檔案提供關於即時客戶設定檔常見問題的解答，以及常見錯誤的疑難排解指南。 如需Adobe Experience Platform中其他服務的相關問題和疑難排解，請參閱 [Experience Platform疑難排解指南](../landing/troubleshooting.md).

使用 [!DNL Real-Time Customer Profile]，您可結合來自多個管道的資料，包括線上、離線、CRM和協力廠商，全面了解每個客戶。 這可讓行銷人員跨多個管道為客戶提供協調一致的相關體驗。

## 常見問題集

以下是關於即時客戶設定檔常見問題的解答清單。

### 「即時客戶設定檔」接受哪種資料？

設定檔接受兩者 **記錄** 和 **時間序列** 只要相關資料包含至少一個將資料與不重複個人建立關聯的身分值，資料即可。

與所有Platform服務一樣，設定檔要求其資料在Experience Data Model(XDM)架構下進行語義結構化。 而此結構必須具有 **主要身分** 定義，並啟用以在設定檔中使用。

若您不熟悉XDM，請從 [XDM概觀](../xdm/home.md) 了解更多。 接下來，請參閱XDM使用指南，了解如何執行 [設定身分欄位](../xdm/tutorials/create-schema-ui.md#identity-field) 和 [為配置檔案啟用架構](../xdm/tutorials/create-schema-ui.md#profile).

### 設定檔資料會儲存在何處？

即時客戶設定檔會維護其專屬的資料存放區（稱為「設定檔存放區」），與包含其他擷取之平台資料的Data Lake不同。

### 如果我已將資料內嵌至Platform，可以在設定檔存放區中使用嗎？

如果資料已內嵌至非設定檔資料集，您必須將該資料重新內嵌至啟用設定檔的資料集，才能在設定檔存放區中使用。 您可以為「設定檔」啟用現有資料集，但在該設定前擷取的任何資料仍不會顯示在「設定檔」存放區中。

如果您想要將先前擷取的資料新增至設定檔存放區，請遵循 [資料集設定教學課程](./tutorials/dataset-configuration.md) 若要建立新資料集或轉換要啟用「設定檔」的現有資料集，然後將所需資料重新內嵌至該資料集。

### 如何檢視擷取的設定檔資料？

根據您是使用API還是UI，有多種檢視設定檔資料的方法。

#### 使用 API

如果您知道要存取之設定檔實體的ID，則可使用 `/entities` （設定檔存取）設定檔API中的端點來尋找這些實體。 請參閱 [實體](./api/entities.md) （位於開發人員指南中）以取得詳細資訊。

您也可以使用Adobe Experience Platform細分服務API來存取符合區段成員資格之客戶的個別設定檔。 請參閱 [區段服務概觀](../segmentation/home.md) 以取得更多資訊。

#### 使用UI

在Experience PlatformUI中， **[!UICONTROL 瀏覽]** 標籤 **[!UICONTROL 設定檔]** 工作區可讓您檢視設定檔總數，並依其身分值搜尋個別設定檔。 請參閱 [設定檔使用手冊](./ui/user-guide.md) 以取得更多資訊。

您也可以在 **[!UICONTROL 瀏覽]** 標籤 **[!UICONTROL 區段]** 工作區。 選取區段後，會顯示符合該區段資格的設定檔範例。 然後，您可以選取這些列出的設定檔中的任何一個，以檢視其詳細資訊。 請參閱 [區段UI概觀](../segmentation/ui/overview.md) 以取得更多資訊。

## 錯誤代碼

以下是使用即時客戶設定檔API時可能遇到的錯誤訊息清單。 如果此處未列出您遇到的錯誤，則可在一般 [平台疑難排解指南](../landing/troubleshooting.md) 。

### 無法查找提供路徑的計算屬性的架構

```json
{
  "code": "400",
  "message": "Could not lookup schema of the computed attribute for the provided path"
}
```

建立新的計算屬性時，當系統找不到請求裝載中提供的架構時，就會發生此錯誤。 請確定您已在裝載的 `path` 屬性，以及 `schema.name` 是有效的架構名稱。

如果您不知道租用戶ID，可依照 [Schema Registry開發人員指南](../xdm/api/getting-started.md).

### 指定的架構或definedOn已存在同名的函式

```json
{
  "code": "400",
  "message": "Function with the same name already exists for the specified schema or definedOn"
}
```

建立新的計算屬性時，當提供 `name` 屬性已用於 `schema.name`. 請先以唯一名稱取代值，然後再重試。

### 運算式的傳回架構與XDM架構中計算屬性的架構不同

```json
{
  "code": "400",
  "message": "Return schema of the expression is not same as the schema of the computed attribute in the XDM schema"
}
```

建立新的計算屬性時，當提供 `name` 屬性已用於 `schema.name`. 請先以唯一名稱取代值，然後再重試。

### 刪除請求無效（配置檔案系統作業）

```json
{
  "code": "400",
  "message": "Invalid delete request (Profile System Job)"
}
```

為刪除系統作業提供無效的有效負載時，會發生此錯誤。 請確定您在裝載的 `dataSetID` 或 `batchID` 屬性。 請參閱 [建立刪除請求](./api/profile-system-jobs.md#create-a-delete-request) ，取得詳細資訊。

### 找不到設定檔資料集的批次

```json
{
  "requestId":"LlTmQkhgHKFGHGHnIkmUxcIL4YTFSpQw",
  "errors":{
    "400":[
      {
        "code":"400",
        "message":"Batch not found for profile dataset '5da688d2c4e60518ad25b7b1'"
      }
    ]
  }
}
```

嘗試為設定檔資料建立刪除請求時，找不到有效的批次時，即會發生此錯誤。 請先確認輸入的資料集ID正確，然後再試一次。

### 尚未建立投影目標

```json
{
  "status":404,
  "title":"The projection destination has not yet been created.",
  "type":"http://ns.adobe.com/adobecloud/problem/missing-entity"
}
```

此錯誤發生於 `destinationId` 在 `POST /config/projections` 請求無效。 再次嘗試之前，請再次檢查您是否提供了有效的目標ID。 若要建立新目的地，請遵循 [設定檔開發人員指南](./api/edge-projections.md#create-a-destination).

### 不支援的媒體類型

```json
{
  "status": 415,
  "title": "HTTP 415 Unsupported Media Type",
  "type": "http://ns.adobe.com/adobecloud/problem/unsupported-media-type"
}
```

傳送POST或PUT要求時，會發生此錯誤，且內容類型標題無效。 再次檢查您是否為正在使用的端點提供有效的內容類型值。

大部分的設定檔端點接受其「內容類型」標題的「application/json」，但有下列例外：

| 端點 | Content-Type |
| --- | --- |
| `/config/projections` | application/vnd.adobe.platform.projectionConfig+json;版本=1 |
| `/config/destinations` | application/vnd.adobe.platform.projectionDestination+json;版本=1 |
