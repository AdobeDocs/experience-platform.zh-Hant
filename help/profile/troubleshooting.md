---
keywords: Experience Platform；設定檔；即時客戶設定檔；疑難排解；API
title: 即時客戶設定檔疑難排解指南
type: Documentation
description: 本檔案提供即時客戶個人檔案常見問題的解答，以及使用Adobe Experience Platform處理個人檔案資料時常見錯誤的疑難排解指南。
exl-id: 0b340025-093b-41e4-8053-969a8e80e889
source-git-commit: dde38e230a6bcb10cd38a12f644f2dd03f0cebaf
workflow-type: tm+mt
source-wordcount: '964'
ht-degree: 0%

---

# 即時客戶個人檔案疑難排解指南

本檔案提供即時客戶個人檔案常見問題的解答，以及常見錯誤的疑難排解指南。 如需Adobe Experience Platform中其他服務的相關問題和疑難排解，請參閱 [Experience Platform疑難排解指南](../landing/troubleshooting.md).

替換為 [!DNL Real-Time Customer Profile]，您能透過合併來自多個管道（包括線上、離線、CRM和協力廠商）的資料，檢視每個個別客戶的整體檢視。 這可讓行銷人員跨多個管道為客戶推動協調、一致且相關的體驗。

## 常見問題集

以下是有關Real-Time Customer Profile常見問題的解答清單。

### 即時客戶個人檔案可接受哪些型別的資料？

設定檔接受兩者 **記錄** 和 **時間序列** 資料，只要相關資料包含至少一個身分值，可將資料與不重複個人建立關聯。

和所有Platform服務一樣，設定檔需要其資料在Experience Data Model (XDM)結構描述下語義結構化。 反過來，此結構描述必須有 **主要身分** 已定義並啟用以便在設定檔中使用。

如果您不熟悉XDM，請從 [XDM概覽](../xdm/home.md) 以進一步瞭解。 接下來，請參閱XDM使用手冊，以瞭解操作步驟 [設定身分欄位](../xdm/tutorials/create-schema-ui.md#identity-field) 和 [為設定檔啟用結構描述](../xdm/tutorials/create-schema-ui.md#profile).

### 設定檔資料會儲存在哪裡？

即時客戶個人檔案會維護自己的資料存放區（稱為「個人檔案存放區」），與包含其他內嵌Platform資料的資料湖分開。

### 如果我已經將資料內嵌至Platform，可以在設定檔存放區中使用嗎？

如果資料已內嵌至非設定檔資料集，您必須將該資料重新內嵌至已啟用設定檔的資料集，才能使其在設定檔存放區中使用。 可以為設定檔啟用現有資料集，但是在該設定之前擷取的任何資料仍將不會顯示在設定檔存放區中。

如果您想要將先前擷取的資料新增至設定檔存放區，請遵循 [資料集設定教學課程](./tutorials/dataset-configuration.md) 建立新資料集或轉換要啟用設定檔的現有資料集，然後將所需資料重新內嵌至該資料集。

### 如何檢視我內嵌的設定檔資料？

檢視設定檔資料的方法有很多種，視您使用的是API還是UI而定。

#### 使用 API

如果您知道要存取之設定檔實體的ID，則可以使用 `/entities` （設定檔存取）設定檔API中的端點來查詢這些實體。 請參閱以下小節： [實體](./api/entities.md) 詳細資訊，請參閱開發人員指南。

您也可以使用Adobe Experience Platform Segmentation Service API來存取已符合受眾會籍資格的客戶的個別設定檔。 請參閱 [Segmentation Service概述](../segmentation/home.md) 以取得詳細資訊。

#### 使用UI

在Experience Platform UI中， **[!UICONTROL 瀏覽]** 索引標籤中的 **[!UICONTROL 設定檔]** 工作區可讓您檢視設定檔總數，並依其身分值搜尋個別設定檔。 請參閱 [設定檔使用手冊](./ui/user-guide.md) 以取得詳細資訊。

您也可以在「 」下方檢視對象清單 **[!UICONTROL 瀏覽]** 索引標籤中的 **[!UICONTROL 受眾]** 工作區。 選取對象後，畫面會顯示符合該對象資格的設定檔範例。 然後，您可以選取這些列出的設定檔之一，以檢視其詳細資訊。 請參閱 [區段UI總覽](../segmentation/ui/overview.md) 以取得詳細資訊。

## 錯誤代碼

以下是您在使用Real-time Customer Profile API時可能會遇到的錯誤訊息清單。 如果您遇到的錯誤未在此處列出，您可能會在一般情況下找到它 [平台疑難排解指南](../landing/troubleshooting.md) 而非。

### 無法查詢所提供路徑之計算屬性的結構描述

```json
{
  "code": "400",
  "message": "Could not lookup schema of the computed attribute for the provided path"
}
```

建立新的計算屬性時，如果系統找不到要求裝載中提供的結構描述，就會發生此錯誤。 確認您已在裝載中提供正確的租使用者ID `path` 屬性，而且其值 `schema.name` 是有效的結構描述名稱。

如果您不知道租使用者ID，可以依照以下檔案中的步驟擷取之 [Schema Registry開發人員指南](../xdm/api/getting-started.md).

### 指定的結構描述或definedOn已經存在相同名稱的函式

```json
{
  "code": "400",
  "message": "Function with the same name already exists for the specified schema or definedOn"
}
```

建立新的計算屬性時，如果提供的是 `name` 屬性已用於 `schema.name`. 在重試之前，以唯一名稱取代值。

### 運算式的傳回結構描述與XDM結構描述中運算屬性的結構描述不同

```json
{
  "code": "400",
  "message": "Return schema of the expression is not same as the schema of the computed attribute in the XDM schema"
}
```

建立新的計算屬性時，如果提供的是 `name` 屬性已用於 `schema.name`. 在重試之前，以唯一名稱取代值。

### 無效的刪除請求（設定檔系統作業）

```json
{
  "code": "400",
  "message": "Invalid delete request (Profile System Job)"
}
```

為刪除系統作業提供無效的裝載時，就會發生此錯誤。 確保您在裝載的底下提供有效的資料集或批次ID `dataSetID` 或 `batchID` 屬性。 請參閱以下小節： [建立刪除請求](./api/profile-system-jobs.md#create-a-delete-request) 詳細資訊，請參閱個人資料開發人員指南。

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

### 不支援的媒體型別

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
