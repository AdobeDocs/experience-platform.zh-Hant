---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: 即時客戶個人檔案疑難排解指南
topic: guide
translation-type: tm+mt
source-git-commit: 94fd6ee324b35acb7ef1185f7851d76d76f3e91c
workflow-type: tm+mt
source-wordcount: '983'
ht-degree: 0%

---


# 即時客戶個人檔案疑難排解指南

本檔案提供即時客戶個人檔案常見問題的解答，以及常見錯誤的疑難排解指南。 如需Adobe Experience Platform中其他服務的相關問題和疑難排解，請參閱 [Experience Platform疑難排解指南](../landing/troubleshooting.md)。

即時客戶描述檔是一般查閱實體儲存，可合併來自各種企業資料資產的資料，然後以個別客戶描述檔和相關時間系列事件的形式提供對該資料的存取。 此功能可讓行銷人員跨多個通道，推動與受眾之間協調、一致且相關的體驗。

## 常見問題集

以下是有關即時客戶個人檔案的常見問題解答清單。

### 「即時客戶個人檔案」接受哪些資料？

只要相關資 **料包含至少一個識別值，將資料與獨特個人關聯，描述檔就會同****** 時接受記錄和時間系列資料。

和所有平台服務一樣，描述檔要求其資料在體驗資料模型(XDM)架構下以語義結構化。 而此方案必須定義主 **要身份** ，並啟用以在配置式中使用。

如果您不熟悉XDM，請從 [XDM概觀開始](../xdm/home.md) ，以瞭解更多。 接下來，請參閱XDM使用指南，瞭解如何設 [定身分欄位](../xdm/tutorials/create-schema-ui.md#identity-field)[並啟用描述檔架構的步驟](../xdm/tutorials/create-schema-ui.md#profile)。

### 描述檔資料儲存在何處？

即時客戶個人檔案會維護其專屬的資料存放區（稱為「個人檔案存放區」），與包含其他收錄平台資料的資料存放區分開。

### 如果我已將資料擷取到Platform中，我是否可將它提供至Profile商店？

如果資料已收錄至非描述檔資料集，您必須將該資料重新收錄至啟用描述檔的資料集，才能在描述檔儲存中使用。 可以為描述檔啟用現有資料集，但是在該設定之前所擷取的任何資料仍不會出現在描述檔儲存中。

如果您想要將先前擷取的資料新增至描述檔存放區，請依照資料集設定教學課程 [](./tutorials/dataset-configuration.md) ，建立新的資料集或轉換要啟用描述檔的現有資料集，然後將所需的資料重新收錄至該資料集。

### 如何檢視我所攝取的描述檔資料？

檢視描述檔資料有多種方法，視您使用的是API或UI而定。

#### 使用API

如果您知道要存取的描述檔實體ID，可以使用描述檔API中的 `/entities` （描述檔存取）端點來尋找這些實體。 如需詳細資訊，請 [參閱](./api/entities.md) 「開發人員指南」中有關實體的章節。

您也可以使用Adobe Experience Platform Segmentation Service API來存取符合區段會籍資格之客戶的個人個人檔案。 See the [Segmentation Service overview](../segmentation/home.md) for more information.

#### 使用UI

在Experience Platform UI中，「描述檔 ******** 」工作區中的「瀏覽」標籤可讓您檢視描述檔總計數，並依個別描述檔的識別值來搜尋個別描述檔。 如需詳細 [資訊，請參閱Profile使用指南](./ui/user-guide.md) 。

您也可以在「區段」工作區的「瀏覽」 **[!UICONTROL 標籤下]** ，檢視區段 **[!UICONTROL 清單]** 。 選取區段後，會顯示符合該區段的描述檔範例。 然後，您可以選取其中任何列出的描述檔來檢視其詳細資訊。 See the [Segmentation UI overview](../segmentation/ui/overview.md) for more information.

## 錯誤代碼

以下是您使用即時客戶設定檔API時可能會遇到的錯誤訊息清單。 如果您遇到的錯誤未列於此處，則可在一般的平台疑難排解指南中 [找到](../landing/troubleshooting.md) 。

### 無法查找所提供路徑的計算屬性的模式

```json
{
  "code": "400",
  "message": "Could not lookup schema of the computed attribute for the provided path"
}
```

當建立新的計算屬性時，當系統找不到請求裝載中提供的架構時，就會發生此錯誤。 請確定您已在裝載的屬性中提供正確的租用戶ID `path` ，且其值 `schema.name` 是有效的架構名稱。

如果您不知道您的租用戶ID，可依照「架構註冊表」開發人員指南中的步驟來 [擷取該租用戶ID](../xdm/api/getting-started.md)。

### 對於指定的架構或definedOn，已存在具有相同名稱的函式

```json
{
  "code": "400",
  "message": "Function with the same name already exists for the specified schema or definedOn"
}
```

建立新計算屬性時，如果提供的屬性已用於 `name` 下面所指示的模式，則會發生此錯誤 `schema.name`。 請先以唯一名稱取代值，再再試一次。

### 表達式的返回模式與XDM模式中計算屬性的模式不同

```json
{
  "code": "400",
  "message": "Return schema of the expression is not same as the schema of the computed attribute in the XDM schema"
}
```

建立新計算屬性時，如果提供的屬性已用於 `name` 下面所指示的模式，則會發生此錯誤 `schema.name`。 請先以唯一名稱取代值，再再試一次。

### 刪除請求無效（配置檔案系統作業）

```json
{
  "code": "400",
  "message": "Invalid delete request (Profile System Job)"
}
```

當為刪除系統作業提供無效的裝載時，會發生此錯誤。 請確定您分別在裝載的或屬性下提供有效的資料集 `dataSetID` 或 `batchID` 批次ID。 如需詳細資訊，請 [參閱「設定檔開發人員指南](./api/profile-system-jobs.md#create-a-delete-request) 」中有關建立刪除要求的章節。

### 找不到描述檔資料集的批次

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

當嘗試建立描述檔資料的刪除請求時，找不到有效的批次時，就會發生此錯誤。 在再次嘗試之前，請檢查您是否已為啟用設定檔的資料集輸入正確的ID。

### 尚未建立投影目標

```json
{
  "status":404,
  "title":"The projection destination has not yet been created.",
  "type":"http://ns.adobe.com/adobecloud/problem/missing-entity"
}
```

當請求中提供的 `destinationId` 內容無效時，就 `POST /config/projections` 會發生此錯誤。 再次嘗試之前，請再次檢查您是否已提供有效的目標ID。 若要建立新目標，請依照「設定檔開發人員指南」中 [的步驟進行](./api/edge-projections.md#create-a-destination)。

### 不支援的介質類型

```json
{
  "status": 415,
  "title": "HTTP 415 Unsupported Media Type",
  "type": "http://ns.adobe.com/adobecloud/problem/unsupported-media-type"
}
```

傳送具有無效內容類型標題的POST或PUT請求時，會發生此錯誤。 再次檢查您是否為您使用的端點提供有效的「內容類型」值。

大部分描述檔端點會接受「應用程式/json」做為其「內容類型」標題，但有下列例外：

| 端點 | 內容類型 |
| --- | --- |
| `/config/projections` | application/vnd.adobe.platform.projectionConfig+json; version=1 |
| `/config/destinations` | application/vnd.adobe.platform.projectionDestination+json; version=1 |