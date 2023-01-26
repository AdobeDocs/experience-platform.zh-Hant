---
title: 將Adobe Journey Optimizer與Platform Web SDK搭配使用
description: 了解如何使用Adobe Journey Optimizer透過Experience PlatformWeb SDK轉譯個人化內容
keywords: ajo;ajo web;adobe journey optimizer;renderDecisions；曲面；決策；主張；範圍；結構
exl-id: e608952c-9598-11ed-b382-d72064651cac
source-git-commit: 1b0f1e2e1625f6994a6e09bd086e4b63a3e8d4ab
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 0%

---

# 使用 [!DNL Adobe Journey Optimizer] 和 [!DNL Platform Web SDK]

[!DNL Adobe Experience Platform] [!DNL Web SDK] 可提供及呈現管理的個人化體驗 [!DNL Adobe Journey Optimizer] 至網頁頻道。 您可以使用WYSIWYG編輯器， [!DNL Adobe Journey Optimizer] [網頁行銷活動UI](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html)，建立、啟用和傳遞 [!DNL Journey Optimizer Web] 行銷活動和個人化體驗。

>[!IMPORTANT]
>
>閱讀 [Adobe Journey Optimizer網路頻道檔案](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/get-started-web.html) 如需快速入門的資訊 [!DNL Journey Optimizer Web] 體驗製作和報告。

## 術語 {#terminology}

**[!UICONTROL 曲面]**:Web曲面是由URL識別的Web屬性，其中 [!DNL Adobe Journey Optimizer] 體驗內容將會傳送。

**[!UICONTROL 主張]**:在 [!DNL Adobe Journey Optimizer]，建議與從 [!DNL Journey Optimizer Campaign].

## 啟用 [!DNL Adobe Journey Optimizer] {#enable-ajo}

若要開始使用 [!DNL Adobe Journey Optimizer]，請遵循下列步驟。

1. 瀏覽 [必要條件](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html#prerequesites) 從 [!DNL Adobe Journey Optimizer] [網頁體驗指南](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html)，具體說明：
   * 設定 [!DNL Adobe Experience Cloud Visual Editing Helper].
   * 啟用 [!DNL Adobe Journey Optimizer] 在 [資料流](../../datastreams/overview.md).
   * 啟用 [!UICONTROL 邊緣活動合併策略] 選項。

2. 新增 `renderDecisions` 選項。 設定 `renderDecisions` to `true` 以在您的網頁表面上自動呈現已傳送的Journey Optimizer內容主張。

   ```javascript
   alloy("sendEvent", {
       ...,
       "renderDecisions": true
   })
   ```

3. （可選）在事件中指定其他曲面。 依預設，Web SDK會自動產生目前網頁的網頁表面，並將其納入向邊緣網路發出的請求中。 如有需要，可在請求中納入其他曲面，方法是在 `personalization.surfaces` 選項 `sendEvent` ，或 **[!UICONTROL 曲面]** [[!UICONTROL 傳送事件] 動作](../../extension/action-types.md#send-event) Web SDK擴充功能的設定。

   ```javascript
   alloy("sendEvent", {
       ...
       "personalization": {
       "surfaces": [ "web://my.site.com/about.html", "web://my.site.com/contact.html" ]
       }
   })
   ```

   ![extension-add-surface](./assets/extension-add-surface.png)

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

4. 與其他個人化功能類似，您可以新增 **[預先隱藏程式碼片段](../manage-flicker.md)** 以在擷取體驗時僅隱藏頁面的某些部分。

## 建立Adobe Journey Optimizer Web體驗 {#create-ajo-web-experiences}

關注 [網站行銷活動製作](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html#create-web-campaign) 中的說明 [!DNL Adobe Journey Optimizer] [網頁體驗指南](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html) 建立 [!DNL Journey Optimizer Web] 行銷活動和體驗。

## 轉譯個人化內容 {#rendering-personalized-content}

請參閱 [呈現個人化內容](../rendering-personalization-content.md) 以取得更多資訊。

Adobe Journey Optimizer Web曲面命題的處理方式與 `__view__` 決策範圍主張。 具體來說，當 `renderDecisions` 選項設為 `true` 在 `sendEvent` 命令，Web SDK會自動呈現這些內容。

範例Journey Optimizer內容主張：

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

若要對Adobe Journey Optimizer個人化實作除錯，請使用 [[!DNL Web SDK] 偵錯](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/debugging.html). [!DNL Adobe Journey Optimizer] 使用進行疑難排解時，可使用除錯追蹤 [[!DNL Adobe Experience Platform Assurance]](https://developer.adobe.com/client-sdks/documentation/platform-assurance/). 檢查事件 `AJO:` 前置詞。

![assurance-ajo-trace](./assets/assurance-ajo-trace.png)


