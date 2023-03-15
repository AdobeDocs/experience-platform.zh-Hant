---
title: 行動對網頁和跨網域ID共用
description: 了解如何跨網域將訪客ID從行動裝置保留至Web屬性
keywords: 身分；行動；ID；共用；網域；跨網域； SDK；平台；
exl-id: b9bb236f-52cf-4615-96d8-1137d957de8c
source-git-commit: 3b65143e33804b251f888dbe2a69d238b3f4cda3
workflow-type: tm+mt
source-wordcount: '901'
ht-degree: 1%

---

# 行動對網頁和跨網域ID共用

## 總覽

Adobe Experience Platform Web SDK支援訪客ID共用功能，讓客戶能更精確、在行動應用程式、行動網站內容以及各網域之間提供個人化體驗。

## 使用案例 {#use-cases}

### 在行動應用程式和行動網站之間提供一致的個人化內容

服裝公司想要根據客戶的興趣來個人化其客戶體驗，並在同時載入WebViews的行動應用程式中確保個人化正確。 透過使用行動對網頁ID共用功能，客戶可透過傳遞 [!DNL ECID] 至行動網頁URL。

### 跨網域提供一致的個人化

具有多個線上商店的零售商想要根據客戶興趣，在其網域間個人化購物者體驗。 使用Web SDK跨網域ID共用功能，零售商可根據客戶興趣，在其所有網域中提供準確的優惠方案。

### 增強訪客活動報表

技術零售商想要透過其訪客何時從行動應用程式移至行動網站或其他網域的相關資訊，來改善其訪客活動報表。 使用Web SDK跨網域ID共用功能，行銷團隊就可以在其Web屬性上準確追蹤訪客，並產生活動報表。

## 先決條件 {#prerequisites}

若要使用行動對網頁和跨網域ID共用，您必須使用 [!DNL Web SDK] 2.11.0版或更新版本。

若為邊緣網路行動實作，此功能在 [邊緣網路的標識](https://aep-sdks.gitbook.io/docs/foundation-extensions/identity-for-edge-network) 擴充功能從1.1.0版開始(iOS和Android)。

此功能也與 [!DNL VisitorAPI.js] 1.7.0版或更新版本。

## 行動對網頁ID共用 {#mobile-to-web}

使用 `getUrlVariables` 來自 [邊緣網路的標識](https://aep-sdks.gitbook.io/docs/foundation-extensions/identity-for-edge-network/api-reference#geturlvariables) 擴充功能，以擷取識別碼作為查詢參數，並在開啟 [!DNL webViews].

Web SDK無需額外設定即可接受 `ECID` 值。

查詢字串參數包括：

* `MCID`:Experience CloudID(`ECID`)
* `MCORGID`:Experience Cloud `orgID` 必須符合 `orgID` 在 [!DNL Web SDK].
* `TS`:時間戳記參數不得早於5分鐘。


行動對網頁ID共用使用 `adobe_mc` 參數。 當 `adobe_mc` 參數存在且有效， `ECID` 系統會自動從查詢字串新增至Edge Network第一個要求中的身分對應。 後續的所有邊緣網路互動都會使用 `ECID`.

如需如何將訪客ID從行動應用程式傳遞至WebView的詳細資訊，請參閱 [處理WebViews](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/app-implementation/web-views.html#implementation).

## 跨網域ID共用 {#cross-domain-sharing}

為了跨網域ID共用，Web SDK 2.11.0版新增了 `appendIdentityToUrl` 命令。 使用時，此命令將生成 `adobe_mc` 查詢字串參數。

命令接受一個屬性的對象， `url`，並傳回具有屬性的物件 `url`.

此命令不等待任何同意更新。 如果未提供同意，則會傳回URL不變。

若 `ECID` 未提供，則 `/acquire` 會呼叫端點來產生 `ECID`.

以下是客戶如何在其網站上實作跨網域ID共用的範例。

此程式碼會針對頁面上的所有點按新增事件接聽程式，如果點按是連結至相符網域（在此例中為） `adobe.com` 或 `behance.com`)、將身分新增至URL，並將使用者重新導向至該處。

```js
document.addEventListener("click", event => {
  const anchor = event.target.closest("a");
  if (!anchor || !anchor.href) {
    return;
  }
  const url = new URL(anchor.href);
  if (!url.hostname.endsWith("adobe.com") && !url.hostname.endsWith("behance.com")) {
    return;
  }
  event.preventDefault();
  alloy("appendIdentityToUrl", { url: anchor.href }).then(result => {
    document.location = result.url;
  });
});
```

## 使用標籤擴充功能 {#tags-extension}

類似於使用 [!DNL Web SDK]，則無須進行其他設定 [!DNL Tags] 擴充功能，以使用透過URL傳遞的身分。

若要透過「標籤」擴充功能使用行動對網頁和跨網域ID共用，您必須使用「標籤」擴充功能2.12.0版或更新版本。

若要將身分從目前頁面共用至其他網域，可在 [!DNL Web SDK] [!DNL Tags] 擴充功能。 此動作的設計用途為搭配 **[!UICONTROL 核心 — 按一下]** 事件類型和值比較條件。

請遵循所述步驟 [此處](../../tags/ui/managing-resources/rules.md) 若要建立具有下列設定的規則：

* [!UICONTROL 事件設定]:
   * **[!UICONTROL 擴充功能：核心]**
   * **[!UICONTROL 事件類型：按一下]**
   * 選擇 **[!UICONTROL 使用者點按>特定元素時]**
   * 在 **[!UICONTROL 選取器]**: `a[href]`. 每當錨點標籤點按於具有 `href` 屬性。

      ![顯示事件設定的UI影像，以及上述設定](assets/id-sharing-event-configuration.png)

* [!UICONTROL 條件設定]
   * **[!UICONTROL 邏輯類型]**: [!UICONTROL 一般]
   * **[!UICONTROL 擴充功能]**: [!UICONTROL 核心]
   * **[!UICONTROL 條件類型]**: [!UICONTROL 值比較]
   * **[!UICONTROL 左操作數]**: [!UICONTROL `%this.hostname%`]. 這是可搭配使用的特殊資料元素 [!UICONTROL 核心 — 按一下] 事件，並解析至所點按連結的主機名稱。
   * **[!UICONTROL 運算元]**: [!UICONTROL 符合Regex]
   * **[!UICONTROL 右操作數]**:輸入符合您要共用身分之網域的規則運算式。 例如，若要比對主機名稱結尾為的連結 `adobe.com` 或 `behance.com`，請使用此規則運算式： `behance.com$|adobe.com$`. 連結的頁面必須具有 [!DNL Web SDK] 或 [!DNL Visitor ID] 安裝以接受身分。

      ![顯示條件組態的UI影像，以及上述設定](assets/id-sharing-condition-configuration.png)

* [!UICONTROL 動作設定]
   * **[!UICONTROL 擴充功能]**: [!UICONTROL Adobe Experience Platform Web SDK]
   * **[!UICONTROL 動作類型]**: [!UICONTROL 使用身分重新導向]
   * **[!UICONTROL 例項]**:選取您的執行個體。 在大多數情況下，您只會設定一個執行個體。 如果您有多個執行個體，請選取一個具有您要共用之身分的執行個體。

      ![顯示動作組態的UI影像，以及上述設定](assets/id-sharing-action-configuration.png)

此 **[!UICONTROL 使用身分重新導向]** 動作會阻止瀏覽器瀏覽至連結。 然後，它會將 `appendIdentityToUrl` 方法 [!DNL Web SDK] 例項。

最後，它會將使用者重新導向至 [!DNL URL] 和 `adobe_mc` 已附加查詢字串參數。
