---
keywords: Experience Platform；配置；即時客戶配置；故障排除；API
title: 即時客戶概要資訊故障排除指南
type: Documentation
description: 本文檔提供有關即時客戶概要檔案的常見問題解答，以及使用Adobe Experience Platform處理概要檔案資料時常見錯誤的故障排除指南。
exl-id: 0b340025-093b-41e4-8053-969a8e80e889
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '1007'
ht-degree: 0%

---

# 即時客戶概要資訊故障排除指南

本文檔提供有關即時客戶概要檔案的常見問題解答，以及常見錯誤的故障排除指南。 有關Adobe Experience Platform其他服務的問題和故障排除，請參閱 [Experience Platform故障排除指南](../landing/troubleshooting.md)。

與 [!DNL Real-Time Customer Profile]，通過組合來自多個渠道（包括線上、離線、CRM和第三方）的資料，您可以看到每個客戶的整體視圖。 這使營銷人員能夠跨多個渠道為客戶提供協調、一致和相關的體驗。

## 常見問題集

以下是有關即時客戶概要資訊的常見問題解答的清單。

### Real-Time Customer Profile接受哪些類型的資料？

配置檔案接受兩者 **記錄** 和 **時間序列** 資料，只要有關資料包含至少一個標識值，該標識值將資料與唯一的個人相關聯。

與所有平台服務一樣，Profile要求其資料在經驗資料模型(XDM)架構下進行語義結構化。 而此架構必須具有 **主身份** 定義並啟用以在配置檔案中使用。

如果您不熟悉XDM，請從 [XDM概述](../xdm/home.md) 來瞭解更多資訊。 接下來，請參見XDM使用手冊，瞭解如何 [設定標識欄位](../xdm/tutorials/create-schema-ui.md#identity-field) 和 [為配置檔案啟用方案](../xdm/tutorials/create-schema-ui.md#profile)。

### 配置檔案資料儲存在何處？

Real-Time Customer Profile維護其自己的資料儲存（稱為「配置檔案儲存」），與包含其他接收的平台資料的Data Lake分開。

### 如果我已將資料接收到平台，是否可以在配置檔案儲存中將其提供？

如果資料已被攝取到非配置檔案資料集中，則必須將該資料重新攝取到啟用配置檔案的資料集中，以便在配置檔案儲存中可用。 可以為配置檔案啟用現有資料集，但在配置檔案儲存中仍不會顯示在配置檔案之前所攝取的所有資料。

如果要將以前攝取的資料添加到配置檔案儲存，請按照 [資料集配置教程](./tutorials/dataset-configuration.md) 建立新資料集或轉換要為配置檔案啟用的現有資料集，然後將所需資料重新插入該資料集。

### 如何查看所攝取的配置檔案資料？

查看配置檔案資料有多種方法，具體取決於您是使用API還是UI。

#### 使用 API

如果您知道要訪問的配置檔案實體的ID，則可以使用 `/entities` 配置檔案API中的（配置檔案訪問）終結點，用於查找這些實體。 請參閱 [實體](./api/entities.md) 中。

您還可以使用Adobe Experience Platform分段服務API訪問符合段成員資格的客戶的單個配置檔案。 查看 [分段服務概述](../segmentation/home.md) 的子菜單。

#### 使用UI

在Experience PlatformUI中， **[!UICONTROL 瀏覽]** 的 **[!UICONTROL 配置檔案]** 工作區允許您查看配置檔案總數並按其標識值搜索單個配置檔案。 查看 [配置檔案使用手冊](./ui/user-guide.md) 的子菜單。

也可以在 **[!UICONTROL 瀏覽]** 的 **[!UICONTROL 段]** 工作區。 選擇段後，將顯示符合該段的配置檔案示例。 然後，您可以選擇其中任何列出的配置檔案以查看其詳細資訊。 查看 [分段UI概述](../segmentation/ui/overview.md) 的子菜單。

## 錯誤代碼

以下是使用Real-Time Customer Profile API時可能遇到的錯誤消息清單。 如果此處未列出您遇到的錯誤，則在常規 [平台故障排除指南](../landing/troubleshooting.md) 的雙曲餘切值。

### 無法查找所提供路徑的計算屬性的架構

```json
{
  "code": "400",
  "message": "Could not lookup schema of the computed attribute for the provided path"
}
```

建立新計算屬性時，當系統找不到請求負載中提供的架構時，會出現此錯誤。 確保在負載中提供了正確的租戶ID `path` 屬性，以及 `schema.name` 是有效的架構名稱。

如果您不知道您的租戶ID，則可以按照 [架構註冊表開發人員指南](../xdm/api/getting-started.md)。

### 指定架構或definedOn已存在同名的函式

```json
{
  "code": "400",
  "message": "Function with the same name already exists for the specified schema or definedOn"
}
```

建立新計算屬性時，當提供 `name` 屬性已用於下面所示的架構 `schema.name`。 在重試之前，請用唯一名稱替換值。

### 表達式的返回架構與XDM架構中計算屬性的架構不同

```json
{
  "code": "400",
  "message": "Return schema of the expression is not same as the schema of the computed attribute in the XDM schema"
}
```

建立新計算屬性時，當提供 `name` 屬性已用於下面所示的架構 `schema.name`。 在重試之前，請用唯一名稱替換值。

### 刪除請求無效（配置檔案系統作業）

```json
{
  "code": "400",
  "message": "Invalid delete request (Profile System Job)"
}
```

當為刪除系統作業提供無效的負載時，會發生此錯誤。 確保在負載下提供有效的資料集或批ID `dataSetID` 或 `batchID` 屬性。 請參閱 [建立刪除請求](./api/profile-system-jobs.md#create-a-delete-request) 的子菜單。

### 找不到配置檔案資料集的批處理

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

當嘗試為配置檔案資料建立刪除請求時找不到有效批時，會發生此錯誤。 再次嘗試之前，請檢查是否為啟用了配置檔案的資料集輸入了正確的ID。

### 尚未建立投影目標

```json
{
  "status":404,
  "title":"The projection destination has not yet been created.",
  "type":"http://ns.adobe.com/adobecloud/problem/missing-entity"
}
```

當 `destinationId` 在 `POST /config/projections` 請求無效。 再次嘗試之前，請仔細檢查您是否提供了有效的目標ID。 要建立新目標，請按照 [配置式開發人員指南](./api/edge-projections.md#create-a-destination)。

### 不支援的媒體類型

```json
{
  "status": 415,
  "title": "HTTP 415 Unsupported Media Type",
  "type": "http://ns.adobe.com/adobecloud/problem/unsupported-media-type"
}
```

在發送具有無效內容類型標頭的POST或PUT請求時，會發生此錯誤。 按兩下檢查您是否正在為正在使用的終結點提供有效的內容類型值。

大多數配置檔案終結點接受其內容類型標頭的「application/json」，但有以下例外：

| 端點 | Content-Type |
| --- | --- |
| `/config/projections` | application/vnd.adobe.platform.projectionConfig+json;版本=1 |
| `/config/destinations` | application/vnd.adobe.platform.projectionDestination+json;版本=1 |
