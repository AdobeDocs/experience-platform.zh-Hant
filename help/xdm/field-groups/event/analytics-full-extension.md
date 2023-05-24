---
title: Adobe AnalyticsExperienceEvent完整擴展架構欄位組
description: 此文檔概述了Adobe AnalyticsExperienceEvent完整擴展架構欄位組。
exl-id: b5e17f4a-a582-4059-bbcb-435d46932775
source-git-commit: fb0d8aedbb88aad8ed65592e0b706bd17840406b
workflow-type: tm+mt
source-wordcount: '888'
ht-degree: 9%

---

# [!UICONTROL Adobe AnalyticsExperienceEvent完全擴展] 架構欄位組

[!UICONTROL Adobe AnalyticsExperienceEvent完全擴展] 是標準架構欄位組 [[!DNL XDM ExperienceEvent] 類](../../classes/experienceevent.md)它捕獲Adobe Analytics收集的常用指標。

本文檔介紹分析擴展欄位組的結構和用例。

>[!NOTE]
>
>由於此欄位組中重複元素的大小和數量，本指南中顯示的許多欄位已折疊以節省空間。 要瀏覽此欄位組的完整結構，您可以 [在平台UI中查找 ](../../ui/explore.md) 或查看 [公共XDM儲存庫](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/analytics/experienceevent-all.schema.json)。

## 欄位組結構

欄位組提供單個 `_experience` 對象到方案，該方案本身包含單個 `analytics` 的雙曲餘切值。

![分析欄位組的頂級欄位](../../images/field-groups/analytics-full-extension/full-schema.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `customDimensions` | 物件 | 捕獲分析跟蹤的自定義維。 查看 [下文](#custom-dimensions) 的子菜單。 |
| `endUser` | 物件 | 捕獲觸發事件的最終用戶的Web交互詳細資訊。 查看 [下文](#end-user) 的子菜單。 |
| `environment` | 物件 | 捕獲觸發事件的瀏覽器和作業系統的資訊。 查看 [下文](#environment) 的子菜單。 |
| `event1to100`<br><br>`event101to200`<br><br>`event201to300`<br><br>`event301to400`<br><br>`event401to500`<br><br>`event501to100`<br><br>`event601to700`<br><br>`event701to800`<br><br>`event801to900`<br><br>`event901to1000` | 物件 | 欄位組提供對象欄位，以捕獲最多1000個自定義事件。 查看 [下文](#events) 的子菜單。 |
| `session` | 物件 | 捕獲有關觸發事件的會話的資訊。 查看 [下文](#session) 的子菜單。 |

{style="table-layout:auto"}

## `customDimensions` {#custom-dimensions}

`customDimensions` 捕獲 [尺寸](https://experienceleague.adobe.com/docs/analytics/components/dimensions/overview.html) 由分析跟蹤。

![customDimensions欄位](../../images/field-groups/analytics-full-extension/customDimensions.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `eVars` | 物件 | 捕獲最多250個轉換變數的對象([埃瓦爾](https://experienceleague.adobe.com/docs/analytics/components/dimensions/evar.html?lang=zh-Hant))。 此對象的屬性已鍵控 `eVar1` 至 `eVar250` 只接受其資料類型的字串。 |
| `hierarchies` | 物件 | 捕獲最多五個自定義層次結構變數的對象([海耶](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/hier.html))。 此對象的屬性已鍵控 `hier1` 至 `hier5`，這些對象本身具有以下子屬性：<ul><li>`delimiter`:用於生成下提供的清單的原始分隔符 `values`。</li><li>`values`:層次級名稱的分隔清單，以字串形式表示。</li></ul> |
| `listProps` | 物件 | 捕獲最多75個對象 [清單道具](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/prop.html#list-props)。 此對象的屬性已鍵控 `prop1` 至 `prop75`，這些對象本身具有以下子屬性：<ul><li>`delimiter`:用於生成下提供的清單的原始分隔符 `values`。</li><li>`values`:屬性的分隔值清單，以字串形式表示。</li></ul> |
| `lists` | 物件 | 捕獲最多三個對象 [清單](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/list.html?lang=zh-Hant)。 此對象的屬性已鍵控 `list1` 至 `list3`。 每個屬性都包含 `list` 陣列 [[!UICONTROL 鍵值對]](../../data-types/key-value-pair.md) 資料類型。 |
| `props` | 物件 | 捕獲最多75個對象 [道](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/prop.html)。 此對象的屬性已鍵控 `prop1` 至 `prop75` 只接受其資料類型的字串。 |
| `postalCode` | 字串 | 客戶提供的郵遞區號。 |
| `stateProvince` | 字串 | 客戶端提供的州或省位置。 |

{style="table-layout:auto"}

## `endUser` {#end-user}

`endUser` 捕獲觸發事件的最終用戶的Web交互詳細資訊。

![endUser欄位](../../images/field-groups/analytics-full-extension/endUser.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `firstWeb` | [[!UICONTROL Web資訊]](../../data-types/web-information.md) | 與此最終用戶的第一個體驗事件中的網頁、連結和引用相關的資訊。 |
| `firstTimestamp` | 整數 | 此最終用戶的第一個ExperienceEvent的Unix時間戳。 |

## `environment` {#environment}

`environment` 捕獲觸發事件的瀏覽器和作業系統的相關資訊。

![環境場](../../images/field-groups/analytics-full-extension/environment.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `browserIDStr` | 字串 | 使用的瀏覽器的Adobe Analytics標識符(另稱為 [瀏覽器類型維](https://experienceleague.adobe.com/docs/analytics/components/dimensions/browser-type.html?lang=zh-Hant))。 |
| `operatingSystemIDStr` | 字串 | 所用作業系統的Adobe Analytics標識符(另稱為 [作業系統類型維](https://experienceleague.adobe.com/docs/analytics/components/dimensions/operating-system-types.html?lang=zh-Hant))。 |

## 自定義事件欄位 {#events}

「分析」擴展欄位組提供的對象欄位最多可捕獲100個 [自定義事件度量](https://experienceleague.adobe.com/docs/analytics/components/metrics/custom-events.html?lang=zh-Hant) 每個，為欄位組總計1000。

每個頂級事件對象都包含其各自範圍的各個事件對象。 比如說， `event101to200` 包含鍵入的事件 `event101` 至 `event200`。

每個偶數對象都使用 [[!UICONTROL 度量]](../../data-types/measure.md) 資料類型，提供唯一標識符和可量化值。

![自定義事件欄位](../../images/field-groups/analytics-full-extension/event-vars.png)

## `session` {#session}

`session` 捕獲有關觸發事件的會話的資訊。

![會話欄位](../../images/field-groups/analytics-full-extension/session.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `search` | [[!UICONTROL 搜尋]](../../data-types/search.md) | 捕獲與Web或移動搜索相關的會話條目資訊。 |
| `web` | [[!UICONTROL Web資訊]](../../data-types/web-information.md) | 捕獲有關會話條目的連結按一下、網頁詳細資訊、參考資訊和瀏覽器詳細資訊的資訊。 |
| `depth` | 整數 | 最終用戶的當前會話深度（如頁碼）。 |
| `num` | 整數 | 最終用戶的當前會話編號。 |
| `timestamp` | 整數 | 會話項的Unix時間戳。 |

## 後續步驟

本文檔介紹了分析擴展欄位組的結構和使用案例。 有關欄位組本身的詳細資訊，請參閱 [公共XDM儲存庫](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/analytics/experienceevent-all.schema.json)。

如果您使用此欄位組來使用Adobe Experience PlatformWeb SDK收集分析資料，請參閱上的指南 [配置資料流](../../../edge/datastreams/overview.md) 瞭解如何將資料映射到伺服器端的XDM。
