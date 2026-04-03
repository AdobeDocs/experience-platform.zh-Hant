---
title: 跨網域共用身分
description: 維護組織擁有之網域的身分連續性，以改善個人化和報告。
source-git-commit: bf0bb72777cacd822fd6e887ac3ef71764784214
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 0%

---

# 跨網域共用身分

當訪客在您組織擁有的網域之間移動時，依預設每個網域都會維護自己的訪客身分。 如果沒有明確的移交，訪客從您的一個網域點按到另一個網域，會在目的地網站上被視為新的未知人員。 此型別的實作片段會報告並重新啟動個人化。

跨網域身分共用可在訪客點按連結或被重新導向時，將`adobe_mc`查詢字串引數附加至目的地URL以解決此問題。 此引數包含訪客的[Experience Cloud ID (ECID)](./overview.md)、您的組織ID以及時間戳記。 當目的地頁面載入有效的`adobe_mc`引數時，Web SDK會自動讀取該引數，並將已傳遞的身分套用至其第一個Edge Network請求，讓兩個網域共用相同的訪客。 `adobe_mc`引數會在五分鐘後到期，因此目的頁面必須在重新導向後立即載入。

此使用案例涵蓋不同網域上網站之間的身分共用。 如果您想要將身分從行動應用程式傳遞至WebView或行動網頁，請改用[行動對網頁身分共用](./mobile-to-web.md)。

## 先決條件

開始之前，請確定您的實作符合下列需求：

* **網頁SDK**： [網頁SDK](/help/collection/js/js-overview.md)版本&#x200B;**2.11.0或更新版本**，或Web SDK標籤延伸模組已同時安裝在來源和目的地網域上。
* **符合設定**：在設定網頁SDK時，所有參與網域都使用相同的[`orgId`](../js/commands/configure/orgid.md)。
* **URL控制項**：您的程式碼會控制網域之間的連結或重新導向，以便您可以將查詢字串引數附加至目的地URL。

## 實作跨網域共用

您必須在充當跨網域移交來源的每個網域上設定身分共用。 如果訪客可以在兩個網域之間雙嚮導覽，請將兩個網域設定為來源。

>[!BEGINTABS]

>[!TAB JavaScript資料庫]

使用[`appendIdentityToUrl`](/help/collection/js/commands/appendidentitytourl.md)命令將`adobe_mc`引數附加至輸出連結。 以下範例會監聽對錨點元素的點按，並將身分附加至指向所需網域的任何連結：

```js
document.addEventListener("click", event => {
  // Check if the click was a link
  const anchor = event.target.closest("a");
  if (!anchor || !anchor.href) return;

  // Check if the link points to a domain you want to share identity with
  const url = new URL(anchor.href);
  if (!url.hostname.endsWith(".example.com") && !url.hostname.endsWith(".example.org")) return;

  // Append the identity to the URL, then navigate
  event.preventDefault();
  alloy("appendIdentityToUrl", { url: anchor.href }).then(result => {
    window.open(result.url, anchor.target || "_self");
  });
});
```

>[!TAB Web SDK標籤延伸模組]

使用[**[!UICONTROL Redirect with identity]**](/help/tags/extensions/client/web-sdk/actions/redirect-with-identity.md)動作將`adobe_mc`引數附加至輸出連結。 您可以建立包含下列條件的規則，以達成所需的行為：

1. **事件**：將擴充功能設為&#x200B;**[!UICONTROL Core]**，並將事件型別設為&#x200B;**[!UICONTROL Click]**。 在&#x200B;**[!UICONTROL Elements matching the CSS selector]**&#x200B;底下，輸入`a[href]`。
2. **條件**：將擴充功能設為&#x200B;**[!UICONTROL Core]**，並將條件型別設為&#x200B;**[!UICONTROL Value Comparison]**。 將&#x200B;**[!UICONTROL Left Operand]**&#x200B;設定為`%this.hostname%`，**[!UICONTROL Operator]**&#x200B;設定為&#x200B;**[!UICONTROL Matches Regex]**，以及&#x200B;**[!UICONTROL Right Operand]**&#x200B;設定為符合您目的地網域的規則運算式（例如`example\.com$|example\.org$`）。
3. **動作**：將擴充功能設為&#x200B;**[!UICONTROL Adobe Experience Platform Web SDK]**，並將動作型別設為&#x200B;**[!UICONTROL Redirect with identity]**。

>[!ENDTABS]

## 在目的地網域上接收身分

目的地網域不需要其他程式碼。 當網頁上出現Web SDK，且URL包含有效的`adobe_mc`引數時，SDK會自動擷取ECID，並將其套用至訪客在其第一個Edge Network要求上的身分對應。

請確定目的地網域符合下列條件：

* Web SDK或Web SDK標籤延伸已安裝，並已設定為使用與來源網域相同的[`orgId`](../js/commands/configure/orgid.md)。 您可以在網域之間交換使用JavaScript資料庫和Web SDK標籤擴充功能，只要它們共用相同的`orgId`即可。
* 頁面會在&#x200B;**引數到期前的重新導向的** 5分鐘`adobe_mc`內載入並傳送其第一個Edge Network要求。
