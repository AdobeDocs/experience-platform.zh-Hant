---
title: 搭配Platform Web SDK使用Adobe Journey Optimizer
description: 瞭解如何使用Adobe Journey Optimizer以Experience Platform Web SDK呈現個人化內容
keywords: ajo；ajo網頁；adobe journey optimizer；renderDecisions；介面；決定；主張；範圍；結構
exl-id: 3f28e2bc-2c4b-4400-8f69-c7316449ff4f
source-git-commit: ae6c6d21b1eea900d01be3287827296071429d30
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 1%

---

# 使用 [!DNL Adobe Journey Optimizer] 使用 [!DNL Platform Web SDK]

[!DNL Adobe Experience Platform] [!DNL Web SDK] 可以傳遞並轉譯受管理的個人化體驗 [!DNL Adobe Journey Optimizer] 至網路頻道。 您可以使用WYSIWYG編輯器， [!DNL Adobe Journey Optimizer] [網頁管道](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html)或非視覺化介面、 [程式碼型Experience Channel](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/code-based-experience/get-started-code-based) 以建立、啟用及傳遞您的 [!DNL Journey Optimizer Web] 行銷活動和個人化體驗。

>[!IMPORTANT]
>
>閱讀 [Adobe Journey Optimizer Web Channel檔案](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/get-started-web.html?lang=zh-Hant) 以取得關於快速入門的資訊 [!DNL Journey Optimizer Web] 體驗撰寫和報告。

## 術語 {#terminology}

**[!UICONTROL 表面]**：網頁介面是指由URI識別的頁面上的網頁或位置，其中 [!DNL Adobe Journey Optimizer] 將會提供體驗內容。

**[!UICONTROL 主張]**：在 [!DNL Adobe Journey Optimizer]，此主張與從體驗中選取的體驗相關聯 [!DNL Journey Optimizer Campaign].

## 正在啟用 [!DNL Adobe Journey Optimizer] {#enable-ajo}

若要開始使用 [!DNL Adobe Journey Optimizer]，請遵循下列步驟。

1. 瀏覽 [必備條件](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html#prerequesites) 從 [!DNL Adobe Journey Optimizer] [Web體驗指南](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html)，尤其是：
   * 設定 [!DNL Adobe Experience Cloud Visual Editing Helper].
   * 啟用 [!DNL Adobe Journey Optimizer] 在您的 [資料流](../../../datastreams/overview.md).
   * 啟用 [!UICONTROL Active-On-Edge合併原則] 選項。

2. 新增 `renderDecisions` 選項新增至您的事件。 設定 `renderDecisions` 至 `true` ，用於自動呈現網頁表面上傳送的Journey Optimizer內容主張。

   ```javascript
   alloy("sendEvent", {
       ...,
       "renderDecisions": true
   })
   ```

3. 可選擇在事件中指定其他介面。 根據預設，Web SDK會自動產生目前網頁的網頁表面，並將其包含在對Edge Network發出的請求中。 如有需要，可在下列欄位中指定其他曲面，以將其包含在請求中： `personalization.surfaces` 的選項 `sendEvent` 指令，或在 **[!UICONTROL 曲面]** [[!UICONTROL 傳送事件] 動作](../../../tags/extensions/client/web-sdk/action-types.md#send-event) Web SDK擴充功能的設定。

   ```javascript
   alloy("sendEvent", {
       ...
       "personalization": {
           "surfaces": [ "web://my.site.com/about.html", "web://my.site.com/contact.html" ]
       }
   })
   ```

   ![extension-add-surface](./assets/extension-add-surface.png)

   事件介面包含在 `query.personalization.surfaces` 要求欄位：

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

4. 與其他個人化功能類似，您可以新增 **[預先隱藏程式碼片段](../manage-flicker.md)** 只隱藏頁面的某些部分。

## 建立Adobe Journey Optimizer網頁體驗 {#create-ajo-web-experiences}

請遵循 [網站行銷活動製作](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html#create-web-campaign) 說明來自 [!DNL Adobe Journey Optimizer] [Web體驗指南](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html) 以建立 [!DNL Journey Optimizer Web] 行銷活動和體驗。

## 呈現個人化內容 {#rendering-personalized-content}

請參閱以下檔案： [呈現個人化內容](../rendering-personalization-content.md) 以取得詳細資訊。

網路表面的Adobe Journey Optimizer主張的處理方式與以下專案類似： `__view__` 決定範圍主張。 具體來說，當 `renderDecisions` 選項已設為 `true` 在 `sendEvent` 這些命令將由Web SDK自動轉譯。

Journey Optimizer內容主張範例：

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

## 偵錯 {#debugging}

若要針對Adobe Journey Optimizer個人化實作除錯，請使用 [Web SDK除錯](/help/web-sdk/use-cases/debugging.md). [!DNL Adobe Journey Optimizer] 使用進行疑難排解時可以使用偵錯追蹤 [[!DNL Adobe Experience Platform Assurance]](https://developer.adobe.com/client-sdks/documentation/platform-assurance/). 使用檢查事件 `AJO:` 前置詞。

![assurance-ajo-trace](./assets/assurance-ajo-trace.png)
