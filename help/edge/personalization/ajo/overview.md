---
title: 將Adobe Journey Optimizer與平台Web SDK配合使用
description: 瞭解如何使用Experience PlatformWeb SDK使用Adobe Journey Optimizer呈現個性化內容
keywords: ajo;ajo web;adobe journey optimizer;renderDecisions;surfaces;decisions;spatitions;scope;schema
exl-id: 3f28e2bc-2c4b-4400-8f69-c7316449ff4f
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 0%

---

# 使用 [!DNL Adobe Journey Optimizer] 和 [!DNL Platform Web SDK]

[!DNL Adobe Experience Platform] [!DNL Web SDK] 可以提供和呈現管理的個性化體驗 [!DNL Adobe Journey Optimizer] 到Web頻道。 你可以使用WYSIWYG編輯器， [!DNL Adobe Journey Optimizer] [Web市場活動UI](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html)，建立、激活和交付 [!DNL Journey Optimizer Web] 市場活動和個性化體驗。

>[!IMPORTANT]
>
>閱讀 [Adobe Journey OptimizerWeb渠道文檔](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/get-started-web.html) 有關入門的資訊 [!DNL Journey Optimizer Web] 體驗創作和報告。

## 術語 {#terminology}

**[!UICONTROL 曲面]**:Web曲面是由URL標識的Web屬性， [!DNL Adobe Journey Optimizer] 將提供體驗內容。

**[!UICONTROL 命題]**:在 [!DNL Adobe Journey Optimizer]，命題與從 [!DNL Journey Optimizer Campaign]。

## 啟用 [!DNL Adobe Journey Optimizer] {#enable-ajo}

開始使用 [!DNL Adobe Journey Optimizer]，請執行以下步驟。

1. 通過 [先決條件](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html#prerequesites) 從 [!DNL Adobe Journey Optimizer] [Web體驗指南](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html)，具體為：
   * 設定 [!DNL Adobe Experience Cloud Visual Editing Helper]。
   * 啟用 [!DNL Adobe Journey Optimizer] 在 [資料流](../../datastreams/overview.md)。
   * 啟用 [!UICONTROL 活動 — 邊緣合併策略] 的雙曲餘切值。

2. 添加 `renderDecisions` 頁籤 設定 `renderDecisions` 至 `true` 用於在您的網頁表面上自動呈現已傳遞的Journey Optimizer內容陳述。

   ```javascript
   alloy("sendEvent", {
       ...,
       "renderDecisions": true
   })
   ```

3. （可選）在事件中指定附加曲面。 預設情況下，Web SDK將自動為當前網頁生成Web曲面，並將其包含在向邊緣網路的請求中。 如果需要，可通過在 `personalization.surfaces` 選項 `sendEvent` 或 **[!UICONTROL 曲面]** [[!UICONTROL 發送事件] 動作](../../extension/action-types.md#send-event) Web SDK擴展的配置。

   ```javascript
   alloy("sendEvent", {
       ...
       "personalization": {
       "surfaces": [ "web://my.site.com/about.html", "web://my.site.com/contact.html" ]
       }
   })
   ```

   ![擴展加曲面](./assets/extension-add-surface.png)

   事件曲面包含在 `query.personalization.surfaces` 請求欄位：

   ```json
   {
   "events": [
       {
           "query": {
               "personalization": {
               "schemas": [
                   ...
               ],
               "decisionScopes": [
                   "__view__"
               ],
               "surfaces": [
                   "web://ajostage.weebly.com/"
               ]
               }
           },
           ...
       }
   ]
   }
   ```

4. 與其他個性化功能類似，您可以添加 **[預隱藏代碼](../manage-flicker.md)** 只隱藏頁面的某些部分，同時獲取體驗。

## 建立Adobe Journey OptimizerWeb體驗 {#create-ajo-web-experiences}

關注 [Web活動編輯](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html#create-web-campaign) 說明 [!DNL Adobe Journey Optimizer] [Web體驗指南](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html) 建立 [!DNL Journey Optimizer Web] 活動和經驗。

## 呈現個性化內容 {#rendering-personalized-content}

請參閱 [呈現個性化內容](../rendering-personalization-content.md) 的子菜單。

對網面的Adobe Journey Optimizer命題的處理方式與 `__view__` 決策範圍建議。 具體來說，當 `renderDecisions` 選項設定為 `true` 的 `sendEvent` 命令這些命令將由Web SDK自動呈現。

示例Journey Optimizer內容陳述：

```json
{
    "scope": "web://ajostage.weebly.com/",
    "scopeDetails": {
        "correlationID": "ccfaf19c-6360-4aea-b464-0cf924db5da7",
        "characteristics": {
            "eventToken": "eyJtZXNzYWdlRXhlY3V0aW9uIjp7Im1lc3NhZ2VFeGVjdXRpb25JRCI6ImEzNDYxYTMzLTc5MjktNGQyNS1hNmMxLTVkYzM2YWY1NzRmMyIsIm1lc3NhZ2VJRCI6ImNjZmFmMTljLTYzNjAtNGFlYS1iNDY0LTBjZjkyNGRiNWRhNyIsIm1lc3NhZ2VUeXBlIjoibWFya2V0aW5nIiwiY2FtcGFpZ25JRCI6IjEzN2JmMzllLWM1ODgtNGI1My1iODQxLTJiMWZiZDYxM2JkYiIsImNhbXBhaWduVmVyc2lvbklEIjoiMTA1NzY1MmEtZWYwNS00YjE3LWExMmUtY2FlOTQyOTFhMWFjIiwiY2FtcGFpZ25BY3Rpb25JRCI6ImViNTlmODQ4LTk5ZDYtNGE1OC05YmU4LTk4MjIxODU0NmYzNiIsIm1lc3NhZ2VQdWJsaWNhdGlvbklEIjoiYzg2NzFjZmItNDdjYS00YTVjLTg4Y2YtNzYwZDFlZjU1MzQyIn0sIm1lc3NhZ2VQcm9maWxlIjp7ImNoYW5uZWwiOnsiX2lkIjoiaHR0cHM6Ly9ucy5hZG9iZS5jb20veGRtL2NoYW5uZWxzL3dlYiIsIl90eXBlIjoiaHR0cHM6Ly9ucy5hZG9iZS5jb20veGRtL2NoYW5uZWwtdHlwZXMvd2ViIn0sIm1lc3NhZ2VQcm9maWxlSUQiOiI2YTViY2I3ZC02MmYxLTQ5NDItODRkMC02MzE5ZjM5Zjk1ZGUifX0="
        },
        "decisionProvider": "AJO",
        "activity": {
            "id": "137bf39e-c588-4b53-b841-2b1fbd613bdb#eb59f848-99d6-4a58-9be8-982218546f36"
        }
    },
    "id": "002321c0-dff5-4153-b171-a9dfb70b9750",
    "items": [
        {
            "schema": "https://ns.adobe.com/personalization/dom-action",
            "data": {
                "uiData": {
                    "tagType": "Text",
                    "actionType": "changed"
                },
                "content": "Welcome AJO!",
                "prehidingSelector": "#wsite-content > DIV:nth-of-type(2) > DIV:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(3) > FONT:nth-of-type(1) > SPAN:nth-of-type(1)",
                "type": "setHtml",
                "selector": "#wsite-content > DIV.wsite-section-wrap:eq(1) > DIV.wsite-section:eq(0) > DIV.wsite-section-content:eq(0) > DIV.container:eq(0) > DIV.wsite-section-elements:eq(0) > DIV.paragraph:eq(0) > FONT:nth-of-type(1) > SPAN:nth-of-type(1)"
            },
            "id": "0a522f66-9e6a-4ded-b1d0-e9167f103290"
        },
        {
            "schema": "https://ns.adobe.com/personalization/dom-action",
            "data": {
                "uiData": {
                    "tagType": "Text",
                    "actionType": "changed"
                },
                "content": {
                    "font-weight": "bold"
                },
                "prehidingSelector": "#wsite-content > DIV:nth-of-type(2) > DIV:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(3) > FONT:nth-of-type(1) > SPAN:nth-of-type(1)",
                "type": "setStyle",
                "selector": "#wsite-content > DIV.wsite-section-wrap:eq(1) > DIV.wsite-section:eq(0) > DIV.wsite-section-content:eq(0) > DIV.container:eq(0) > DIV.wsite-section-elements:eq(0) > DIV.paragraph:eq(0) > FONT:nth-of-type(1) > SPAN:nth-of-type(1)"
            },
            "id": "66216ca5-5d0f-4239-a8c8-6bc4a5a7cbdb"
        }
    ]
}
```

## 為  除錯 {#debugging}

要調試Adobe Journey Optimizer個性化設定，請使用 [[!DNL Web SDK] 調試](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/debugging.html)。 [!DNL Adobe Journey Optimizer] 排除故障時，使用 [[!DNL Adobe Experience Platform Assurance]](https://developer.adobe.com/client-sdks/documentation/platform-assurance/)。 使用 `AJO:` 前置詞。

![保證 — 跟蹤](./assets/assurance-ajo-trace.png)
