---
title: Adobe Analytics ExperienceEvent完整擴充功能結構欄位群組
description: 本檔案概述Adobe Analytics ExperienceEvent完整擴充功能結構欄位群組。
exl-id: b5e17f4a-a582-4059-bbcb-435d46932775
source-git-commit: fb0d8aedbb88aad8ed65592e0b706bd17840406b
workflow-type: tm+mt
source-wordcount: '888'
ht-degree: 9%

---

# [!UICONTROL Adobe Analytics ExperienceEvent完整擴充功能] 方案欄位組

[!UICONTROL Adobe Analytics ExperienceEvent完整擴充功能] 是的標準架構欄位組 [[!DNL XDM ExperienceEvent] 類](../../classes/experienceevent.md)，會擷取Adobe Analytics所收集的通用量度。

本檔案說明Analytics擴充功能欄位群組的結構和使用案例。

>[!NOTE]
>
>由於此欄位組中重複元素的大小和數量，本指南中顯示的許多欄位已折疊，以節省空間。 要探索此欄位組的完整結構，您可以 [在Platform UI中查詢 ](../../ui/explore.md) 或在 [公用XDM存放庫](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/analytics/experienceevent-all.schema.json).

## 欄位群組結構

欄位群組提供單一 `_experience` 對象，其本身包含單個 `analytics` 物件。

![Analytics欄位群組的頂層欄位](../../images/field-groups/analytics-full-extension/full-schema.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `customDimensions` | 物件 | 擷取Analytics追蹤的自訂維度。 請參閱 [下文](#custom-dimensions) 以取得此物件內容的詳細資訊。 |
| `endUser` | 物件 | 擷取觸發事件之一般使用者的網路互動詳細資料。 請參閱 [下文](#end-user) 以取得此物件內容的詳細資訊。 |
| `environment` | 物件 | 擷取觸發事件之瀏覽器和作業系統的相關資訊。 請參閱 [下文](#environment) 以取得此物件內容的詳細資訊。 |
| `event1to100`<br><br>`event101to200`<br><br>`event201to300`<br><br>`event301to400`<br><br>`event401to500`<br><br>`event501to100`<br><br>`event601to700`<br><br>`event701to800`<br><br>`event801to900`<br><br>`event901to1000` | 物件 | 欄位群組提供物件欄位，可擷取最多1000個自訂事件。 請參閱 [下文](#events) 以取得這些欄位的詳細資訊。 |
| `session` | 物件 | 擷取觸發事件之工作階段的相關資訊。 請參閱 [下文](#session) 以取得此物件內容的詳細資訊。 |

{style="table-layout:auto"}

## `customDimensions` {#custom-dimensions}

`customDimensions` 擷取自訂 [維度](https://experienceleague.adobe.com/docs/analytics/components/dimensions/overview.html) 由Analytics追蹤。

![customDimensions欄位](../../images/field-groups/analytics-full-extension/customDimensions.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `eVars` | 物件 | 擷取最多250個轉換變數的物件([eVar](https://experienceleague.adobe.com/docs/analytics/components/dimensions/evar.html?lang=zh-Hant))。 此對象的屬性已被輸入 `eVar1` to `eVar250` 並只接受字串作為其資料類型。 |
| `hierarchies` | 物件 | 擷取最多五個自訂階層變數的物件([海耶](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/hier.html))。 此對象的屬性已被輸入 `hier1` to `hier5`，它們本身是具有下列子屬性的對象：<ul><li>`delimiter`:用來產生下方提供清單的原始分隔字元 `values`.</li><li>`values`:階層層級名稱的分隔清單，以字串表示。</li></ul> |
| `listProps` | 物件 | 擷取最多75個物件 [清單屬性](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/prop.html#list-props). 此對象的屬性已被輸入 `prop1` to `prop75`，它們本身是具有下列子屬性的對象：<ul><li>`delimiter`:用來產生下方提供清單的原始分隔字元 `values`.</li><li>`values`:prop的分隔值清單，以字串表示。</li></ul> |
| `lists` | 物件 | 擷取最多3個物件 [清單](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/list.html?lang=zh-Hant). 此對象的屬性已被輸入 `list1` to `list3`. 這些屬性中的每個都包含 `list` 陣列 [[!UICONTROL 索引鍵值組]](../../data-types/key-value-pair.md) 資料類型。 |
| `props` | 物件 | 擷取最多75個物件 [prop](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/prop.html). 此對象的屬性已被輸入 `prop1` to `prop75` 並只接受字串作為其資料類型。 |
| `postalCode` | 字串 | 用戶端提供的郵遞區號。 |
| `stateProvince` | 字串 | 客戶端提供的州或省位置。 |

{style="table-layout:auto"}

## `endUser` {#end-user}

`endUser` 擷取觸發事件之一般使用者的網路互動詳細資料。

![endUser欄位](../../images/field-groups/analytics-full-extension/endUser.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `firstWeb` | [[!UICONTROL 網路資訊]](../../data-types/web-information.md) | 來自此使用者第一個體驗事件的網頁、連結和反向連結相關資訊。 |
| `firstTimestamp` | 整數 | 此一般使用者第一個ExperienceEvent的Unix時間戳記。 |

## `environment` {#environment}

`environment` 擷取觸發事件之瀏覽器和作業系統的相關資訊。

![環境欄位](../../images/field-groups/analytics-full-extension/environment.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `browserIDStr` | 字串 | 使用的瀏覽器Adobe Analytics識別碼(又稱為 [瀏覽器類型維度](https://experienceleague.adobe.com/docs/analytics/components/dimensions/browser-type.html?lang=zh-Hant))。 |
| `operatingSystemIDStr` | 字串 | 使用的作業系統的Adobe Analytics識別碼(又稱為 [作業系統類型維](https://experienceleague.adobe.com/docs/analytics/components/dimensions/operating-system-types.html?lang=zh-Hant))。 |

## 自訂事件欄位 {#events}

Analytics擴充功能欄位群組提供10個物件欄位，最多可擷取100個 [自訂事件量度](https://experienceleague.adobe.com/docs/analytics/components/metrics/custom-events.html?lang=zh-Hant) 每個，欄位群組總共1000個。

每個頂級事件對象包含各自範圍內的個別事件對象。 例如， `event101to200` 包含中輸入的事件 `event101` to `event200`.

每個偶數物件都使用 [[!UICONTROL 測量]](../../data-types/measure.md) 資料類型，提供唯一識別碼和可量化的值。

![自訂事件欄位](../../images/field-groups/analytics-full-extension/event-vars.png)

## `session` {#session}

`session` 擷取觸發事件之工作階段的相關資訊。

![工作階段欄位](../../images/field-groups/analytics-full-extension/session.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `search` | [[!UICONTROL 搜尋]](../../data-types/search.md) | 擷取與工作階段項目的網頁或行動搜尋相關的資訊。 |
| `web` | [[!UICONTROL 網路資訊]](../../data-types/web-information.md) | 擷取工作階段項目之連結點按、網頁詳細資料、反向連結資訊和瀏覽器詳細資料的相關資訊。 |
| `depth` | 整數 | 一般使用者的目前工作階段深度（例如頁碼）。 |
| `num` | 整數 | 最終用戶的當前會話編號。 |
| `timestamp` | 整數 | 會話項的Unix時間戳。 |

## 後續步驟

本檔案說明Analytics擴充功能欄位群組的結構和使用案例。 如需欄位群組本身的詳細資訊，請參閱 [公用XDM存放庫](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/analytics/experienceevent-all.schema.json).

如果您使用此欄位群組來使用Adobe Experience Platform Web SDK收集Analytics資料，請參閱 [設定資料流](../../../edge/datastreams/overview.md) 了解如何將資料對應至伺服器端的XDM。
