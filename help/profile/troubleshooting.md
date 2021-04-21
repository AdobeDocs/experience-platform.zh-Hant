---
keywords: Experience Platform；配置檔案；即時客戶配置檔案；故障排除；API
title: 即時客戶個人檔案疑難排解指南
topic-legacy: guide
type: Documentation
description: 本檔案提供有關即時客戶個人檔案的常見問題解答，以及使用Adobe Experience Platform使用個人檔案資料時常見錯誤的疑難排解指南。
exl-id: 0b340025-093b-41e4-8053-969a8e80e889
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1003'
ht-degree: 0%

---

# 即時客戶個人檔案疑難排解指南

本檔案提供即時客戶個人檔案常見問題的解答，以及常見錯誤的疑難排解指南。 有關Adobe Experience Platform其他服務的問題和故障排除，請參閱[Experience Platform故障排除指南](../landing/troubleshooting.md)。

透過[!DNL Real-time Customer Profile]，您可以結合來自多個通道（包括線上、離線、CRM和協力廠商）的資料，全面瞭解每個客戶。 這可讓行銷人員跨多個通道為客戶提供協調、一致且相關的體驗。

## 常見問題集

以下是有關即時客戶個人檔案的常見問題解答清單。

### 「即時客戶個人檔案」接受哪些資料？

只要相關資料包含至少一個將資料與唯一個人相關聯的標識值，配置檔案接受&#x200B;**record**&#x200B;和&#x200B;**time-series**&#x200B;資料。

和所有平台服務一樣，描述檔要求其資料在體驗資料模型(XDM)架構下以語義結構化。 而此方案必須定義&#x200B;**主標識**，並啟用該標識以便在配置檔案中使用。

如果您不熟悉XDM，請從[XDM概觀](../xdm/home.md)開始瞭解詳細內容。 接下來，請參閱XDM使用手冊，瞭解如何[設定身份欄位](../xdm/tutorials/create-schema-ui.md#identity-field)和[啟用配置檔案](../xdm/tutorials/create-schema-ui.md#profile)模式的步驟。

### 描述檔資料儲存在何處？

即時客戶個人檔案會維護其專屬的資料存放區（稱為「個人檔案存放區」），與包含其他收錄平台資料的資料存放區分開。

### 如果我已將資料擷取到Platform中，我是否可將它提供至Profile商店？

如果資料已收錄至非描述檔資料集，您必須將該資料重新收錄至啟用描述檔的資料集，才能在描述檔儲存中使用。 雖然可以啟用現有資料集的描述檔，但是在設定之前所擷取的任何資料仍不會出現在描述檔儲存中。

如果您想要將先前擷取的資料新增至描述檔儲存，請依照[資料集設定教學課程](./tutorials/dataset-configuration.md)建立新資料集或轉換要啟用描述檔的現有資料集，然後將所需資料重新擷取至該資料集。

### 如何檢視我所攝取的描述檔資料？

檢視描述檔資料有多種方法，視您使用的是API或UI而定。

#### 使用API

如果您知道要存取的描述檔實體的ID，可使用描述檔API中的`/entities`（描述檔存取）端點來尋找這些實體。 如需詳細資訊，請參閱開發人員指南中[entities](./api/entities.md)一節。

您也可以使用Adobe Experience Platform區段服務API來存取符合區段會籍資格之客戶的個人個人檔案。 如需詳細資訊，請參閱[分段服務概觀](../segmentation/home.md)。

#### 使用UI

在Experience PlatformUI中，**[!UICONTROL Profiles]**&#x200B;工作區中的&#x200B;**[!UICONTROL Browse]**&#x200B;標籤允許您查看配置檔案總數，並按其標識值搜索單個配置檔案。 如需詳細資訊，請參閱[Profile使用指南](./ui/user-guide.md)。

您也可以在&#x200B;**[!UICONTROL Segments]**&#x200B;工作區的&#x200B;**[!UICONTROL Browse]**&#x200B;標籤下檢視區段清單。 選取區段後，會顯示符合該區段的描述檔範例。 然後，您可以選取其中任何列出的描述檔來檢視其詳細資訊。 如需詳細資訊，請參閱[區段UI概觀](../segmentation/ui/overview.md)。

## 錯誤代碼

以下是您使用即時客戶設定檔API時可能會遇到的錯誤訊息清單。 如果此處未列出您遇到的錯誤，您可在一般的[平台疑難排解指南](../landing/troubleshooting.md)中找到。

### 無法查找所提供路徑的計算屬性的模式

```json
{
  "code": "400",
  "message": "Could not lookup schema of the computed attribute for the provided path"
}
```

當建立新的計算屬性時，當系統找不到請求裝載中提供的架構時，就會發生此錯誤。 請確定您已在裝載的`path`屬性中提供正確的租用戶ID，且`schema.name`的值是有效的架構名稱。

如果您不知道您的租用戶ID，可依照[架構註冊表開發人員指南](../xdm/api/getting-started.md)中的步驟來擷取該租用戶ID。

### 對於指定的架構或definedOn，已存在具有相同名稱的函式

```json
{
  "code": "400",
  "message": "Function with the same name already exists for the specified schema or definedOn"
}
```

建立新計算屬性時，當提供的`name`屬性已用於`schema.name`下所指示的模式時，會發生此錯誤。 請先以唯一名稱取代值，再再試一次。

### 表達式的返回模式與XDM模式中計算屬性的模式不同

```json
{
  "code": "400",
  "message": "Return schema of the expression is not same as the schema of the computed attribute in the XDM schema"
}
```

建立新計算屬性時，當提供的`name`屬性已用於`schema.name`下所指示的模式時，會發生此錯誤。 請先以唯一名稱取代值，再再試一次。

### 刪除請求無效（配置檔案系統作業）

```json
{
  "code": "400",
  "message": "Invalid delete request (Profile System Job)"
}
```

當為刪除系統作業提供無效的裝載時，會發生此錯誤。 請確定您是分別在裝載的`dataSetID`或`batchID`屬性下提供有效的資料集或批次ID。 如需詳細資訊，請參閱「設定檔開發人員指南」中有關建立刪除要求的章節。[](./api/profile-system-jobs.md#create-a-delete-request)

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

當`POST /config/projections`請求中提供的`destinationId`無效時，會發生此錯誤。 再次嘗試之前，請再次檢查您是否已提供有效的目標ID。 要建立新目標，請遵循[Profile developer guide](./api/edge-projections.md#create-a-destination)中概述的步驟。

### 不支援的介質類型

```json
{
  "status": 415,
  "title": "HTTP 415 Unsupported Media Type",
  "type": "http://ns.adobe.com/adobecloud/problem/unsupported-media-type"
}
```

傳送具有無效「內容類型」標題的POST或PUT請求時，會發生此錯誤。 再次檢查您是否為您使用的端點提供有效的「內容類型」值。

大部分描述檔端點會接受「應用程式/json」做為其「內容類型」標題，但有下列例外：

| 端點 | Content-Type |
| --- | --- |
| `/config/projections` | application/vnd.adobe.platform.projectionConfig+json;version=1 |
| `/config/destinations` | application/vnd.adobe.platform.projectionDestination+json;version=1 |
