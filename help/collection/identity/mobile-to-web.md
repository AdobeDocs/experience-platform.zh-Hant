---
title: 從行動應用程式分享身分到行動網頁/網頁檢視
description: 從行動應用程式將身分傳遞至行動網站內容或WebView，以便報告和個人化可在Web內容中繼續。
source-git-commit: bf0bb72777cacd822fd6e887ac3ef71764784214
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 0%

---

# 從行動應用程式分享身分到行動網頁/網頁檢視

當訪客從行動應用程式移至WebView或行動網頁時，應用程式和網頁內容會各自維持自己的身分識別。 如果沒有明確的移交，網頁體驗會將訪客視為新的不明人員，這會使報表產生片段並重新啟動個人化。

行動裝置對網頁的身分共用可解決此問題，方法是透過[查詢字串引數，將訪客的](./overview.md)Experience Cloud ID (ECID)`adobe_mc`從行動應用程式傳遞至Web目的地。 引數包含ECID、您的Experience Cloud組織ID和時間戳記。 當Web目的地載入有效的`adobe_mc`引數時，Web SDK會自動讀取該引數，並將傳遞的身分套用至其第一個Edge Network請求，讓兩個內容共用相同的訪客。

當您的行動應用程式開啟組織控制的WebView或行動網頁，而您希望應用程式活動和網頁活動保持繫結至相同訪客時，請使用此模式。 如果您的目標是不同網域上的網站之間的身分連續性，請改用[跨網域共用](cross-domain-sharing.md)。

## 先決條件

開始之前，請確定您的實作符合下列需求：

* **行動應用程式**： Adobe Experience Platform Mobile SDK具有[適用於Edge Network](https://developer.adobe.com/client-sdks/edge/identity-for-edge-network/)的身分識別延伸功能版本&#x200B;**1.1.0或更新版本** （iOS和Android）。
* **Web目的地**： [Web SDK](/help/collection/js/js-overview.md)版本&#x200B;**2.11.0或更新版本**，或Web SDK標籤延伸。
* **URL控制項**：您的程式碼會控制應用程式傳遞給WebView或瀏覽器的URL，以便您能附加查詢字串引數。
* **符合的設定**：在行動裝置和網頁實作中設定了相同的Experience Cloud組織識別碼。

## 從行動應用程式擷取身分 {#retrieve-identity}

使用Edge Network識別擴充功能中的[`getUrlVariables`](https://developer.adobe.com/client-sdks/edge/identity-for-edge-network/api-reference/#geturlvariables) API，以查詢字串形式擷取訪客的識別身分。 接著，您可以在開啟WebView或瀏覽器之前，將該字串附加至URL。

傳回的字串包含下列URL編碼的引數：

| 參數 | 說明 |
| --- | --- |
| `MCID` | Experience Cloud ID (ECID)。 |
| `MCORGID` | 您的Experience Cloud組織ID。 此引數必須符合目的地頁面上Web SDK中設定的組織。 |
| `TS` | 時間戳記。 目的地必須在&#x200B;**5分鐘**&#x200B;內收到此值，否則移交會被拒絕。 |

下列程式碼範例說明移交在行動應用程式中會如何呈現：

>[!BEGINTABS]

>[!TAB Swift (iOS)]

```swift
Identity.getUrlVariables { (urlVariables, error) in
    if let error = error {
        // Handle the error
        return
    }

    guard let urlVariables = urlVariables else { return }

    // Construct the full URL by appending the identity query string
    if let url = URL(string: "https://example.com/webapp?\(urlVariables)") {
        // Open the URL in a WebView or browser
        let request = URLRequest(url: url)
        webView.load(request)
    }
}
```

>[!TAB Kotlin (Android)]

```kotlin
Identity.getUrlVariables { urlVariables ->
    if (urlVariables != null) {
        // Construct the full URL by appending the identity query string
        val url = "https://example.com/webapp?$urlVariables"

        // Open the URL in a WebView or browser
        webView.loadUrl(url)
    }
}
```

>[!ENDTABS]

## 在網頁端接收身分 {#receive-identity}

Web目的地不需要其他程式碼。 當網頁上出現Web SDK，且URL包含有效的`adobe_mc`引數時，SDK會自動擷取ECID，並在第一個Edge Network請求時將它套用至訪客的身分對應。

如果您的Web目的地使用Web SDK標籤延伸模組，而您需要將訪客重新導向至另一個頁面，同時保留身分，請使用具有身分的[重新導向](/help/tags/extensions/client/web-sdk/actions/redirect-with-identity.md)動作，將`adobe_mc`引數轉送至下一個頁面。

>[!NOTE]
>
>`adobe_mc`引數會在&#x200B;**5分鐘**&#x200B;後到期。 請確定Web目的地會在URL開啟後立即載入並傳送其第一個Edge Network要求。
