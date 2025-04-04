---
keywords: Experience Platform；設定檔；即時客戶設定檔；疑難排解；API
title: 即時客戶設定檔疑難排解指南
type: Documentation
description: 本檔案提供即時客戶個人檔案常見問題的解答，以及使用Adobe Experience Platform處理個人檔案資料時常見錯誤的疑難排解指南。
exl-id: 0b340025-093b-41e4-8053-969a8e80e889
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '968'
ht-degree: 1%

---

# 即時客戶個人檔案疑難排解指南

本檔案提供即時客戶個人檔案常見問題的解答，以及常見錯誤的疑難排解指南。 如需Adobe Experience Platform中其他服務的相關問題和疑難排解，請參閱[Experience Platform疑難排解指南](../landing/troubleshooting.md)。

透過[!DNL Real-Time Customer Profile]，您可以透過合併來自多個管道（包括線上、離線、CRM和協力廠商）的資料，檢視每個個別客戶的整體檢視。 這可讓行銷人員跨多個管道為客戶推動協調、一致且相關的體驗。

## 常見問題集

以下是有關Real-Time Customer Profile常見問題的解答清單。

### 即時客戶個人檔案可接受哪些型別的資料？

設定檔接受&#x200B;**記錄**&#x200B;和&#x200B;**時間序列**&#x200B;資料，只要有關資料至少包含一個識別值，可將資料與不重複的個人建立關聯。

和所有Experience Platform服務一樣，設定檔需要其資料在Experience Data Model (XDM)結構描述下進行語義結構化。 反過來，此結構描述必須已定義&#x200B;**主要身分**，而且必須啟用才能在設定檔中使用。

如果您不熟悉XDM，請從[XDM總覽](../xdm/home.md)開始瞭解更多。 接下來，請參閱XDM使用手冊，瞭解如何[設定身分識別欄位](../xdm/tutorials/create-schema-ui.md#identity-field)和[為設定檔](../xdm/tutorials/create-schema-ui.md#profile)啟用結構描述。

### 設定檔資料會儲存在哪裡？

即時客戶個人檔案會維護自己的資料存放區（稱為「個人檔案存放區」），與包含其他已擷取Experience Platform資料的資料湖分開。

### 如果我已經將資料內嵌至Experience Platform，可以在設定檔存放區中使用嗎？

如果資料已內嵌至非設定檔資料集，您必須將該資料重新內嵌至已啟用設定檔的資料集，才能使其在設定檔存放區中使用。 可以為設定檔啟用現有資料集，但是在該設定之前擷取的任何資料仍將不會顯示在設定檔存放區中。

如果您想要將先前擷取的資料新增至設定檔存放區，請依照[資料集組態教學課程](./tutorials/dataset-configuration.md)中的指示來建立新資料集，或將現有資料集轉換為可啟用設定檔的資料集，然後將想要的資料重新擷取至該資料集。

### 如何檢視我內嵌的設定檔資料？

檢視設定檔資料的方法有很多種，視您使用的是API還是UI而定。

#### 使用 API

如果您知道要存取之設定檔實體的ID，則可以使用設定檔API中的`/entities` （設定檔存取）端點來尋找這些實體。 如需詳細資訊，請參閱開發人員指南中[entities](./api/entities.md)的相關章節。

您也可以使用Adobe Experience Platform Segmentation Service API來存取已符合受眾會籍資格的客戶的個別設定檔。 如需詳細資訊，請參閱[分段服務總覽](../segmentation/home.md)。

#### 使用UI

在Experience Platform UI中，**[!UICONTROL 設定檔]**&#x200B;工作區中的&#x200B;**[!UICONTROL 瀏覽]**&#x200B;索引標籤可讓您檢視設定檔總計數，並依其身分值搜尋個別設定檔。 如需詳細資訊，請參閱[設定檔使用手冊](./ui/user-guide.md)。

您也可以在&#x200B;**[!UICONTROL 對象]**&#x200B;工作區的&#x200B;**[!UICONTROL 瀏覽]**&#x200B;標籤下檢視對象清單。 選取對象後，畫面會顯示符合該對象資格的設定檔範例。 然後，您可以選取這些列出的設定檔之一，以檢視其詳細資訊。 如需詳細資訊，請參閱[區段UI總覽](../segmentation/ui/overview.md)。

## 錯誤代碼

以下是您在使用Real-time Customer Profile API時可能會遇到的錯誤訊息清單。 如果此處未列出您遇到的錯誤，您可以在一般[Experience Platform疑難排解指南](../landing/troubleshooting.md)中找到。

### 無法查詢所提供路徑之計算屬性的結構描述

```json
{
  "code": "400",
  "message": "Could not lookup schema of the computed attribute for the provided path"
}
```

建立新的計算屬性時，如果系統找不到要求裝載中提供的結構描述，就會發生此錯誤。 確定您已提供有效負載`path`屬性中的正確租使用者ID，且`schema.name`的值為有效的結構描述名稱。

如果您不知道您的租使用者ID，可以按照[Schema Registry開發人員指南](../xdm/api/getting-started.md)中的步驟擷取它。

### 指定的結構描述或definedOn已經存在相同名稱的函式

```json
{
  "code": "400",
  "message": "Function with the same name already exists for the specified schema or definedOn"
}
```

建立新的計算屬性時，當提供的`name`屬性已用於`schema.name`下指示的結構描述時，就會發生此錯誤。 在重試之前，以唯一名稱取代值。

### 運算式的傳回結構描述與XDM結構描述中運算屬性的結構描述不同

```json
{
  "code": "400",
  "message": "Return schema of the expression is not same as the schema of the computed attribute in the XDM schema"
}
```

建立新的計算屬性時，當提供的`name`屬性已用於`schema.name`下指示的結構描述時，就會發生此錯誤。 在重試之前，以唯一名稱取代值。

### 無效的刪除請求（設定檔系統作業）

```json
{
  "code": "400",
  "message": "Invalid delete request (Profile System Job)"
}
```

為刪除系統作業提供無效的裝載時，就會發生此錯誤。 請確定您分別在承載的`dataSetID`或`batchID`屬性下提供有效的資料集或批次ID。 如需詳細資訊，請參閱設定檔開發人員指南中有關[建立刪除請求](./api/profile-system-jobs.md#create-a-delete-request)的章節。

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

當嘗試為設定檔資料建立刪除請求時找不到有效的批次時，就會發生此錯誤。 在重試之前，請檢查您已為啟用設定檔的資料集輸入正確的ID。

### 不支援的媒體類型

```json
{
  "status": 415,
  "title": "HTTP 415 Unsupported Media Type",
  "type": "http://ns.adobe.com/adobecloud/problem/unsupported-media-type"
}
```

傳送具有無效Content-Type標頭的POST或PUT請求時，會發生此錯誤。 仔細檢查您是否為使用的端點提供有效的Content-Type值。

大部分的設定檔端點都接受「application/json」做為其Content-Type標頭，但下列為例外：

| 端點 | Content-Type |
| --- | --- |
| `/config/projections` | application/vnd.adobe.platform.projectionConfig+json； version=1 |
| `/config/destinations` | application/vnd.adobe.platform.projectionDestination+json； version=1 |
