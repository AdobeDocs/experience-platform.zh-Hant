---
title: 移動到Web和跨域ID共用
description: 瞭解如何跨域將訪問者ID從移動屬性保留到Web屬性
keywords: 標識；移動；id；共用；域；跨域；sdk；平台；
exl-id: b9bb236f-52cf-4615-96d8-1137d957de8c
source-git-commit: 3b65143e33804b251f888dbe2a69d238b3f4cda3
workflow-type: tm+mt
source-wordcount: '901'
ht-degree: 1%

---

# 移動到Web和跨域ID共用

## 總覽

Adobe Experience Platform網路軟體開發工具包支援訪問者身份共用功能，使客戶能夠更準確地在移動應用和移動網路內容之間以及跨域提供個性化體驗。

## 使用案例 {#use-cases}

### 在移動應用和移動網站之間提供一致的個性化

一家服裝公司希望根據客戶的興趣個性化客戶體驗，並在一個同時載入WebView的移動應用程式中保持個性化的準確性。 通過使用移動到Web ID共用功能，他們可以通過傳遞應用程式和移動Web內容中使用相同的訪問者標識符來確保向客戶提供最準確的服務 [!DNL ECID] 的子菜單。

### 跨域提供一致的個性化

一個擁有多個線上商店的零售商希望根據顧客的興趣，對顧客的購物體驗進行個性化設定。 使用Web SDK跨域ID共用功能，零售商可以根據客戶興趣在其所有域中提供準確的服務。

### 增強訪問者活動報告

一家技術零售商希望利用訪問者何時從移動應用程式移動到移動網站或移動其他域的資訊來改進訪問者活動報告。 使用Web SDK跨域ID共用功能，營銷團隊可以準確跟蹤訪問者的Web屬性並生成活動報告。

## 先決條件 {#prerequisites}

要使用移動到Web和跨域ID共用，必須使用 [!DNL Web SDK] 2.11.0版或更高版本。

對於邊緣網路移動實現，在 [邊緣網路的標識](https://aep-sdks.gitbook.io/docs/foundation-extensions/identity-for-edge-network) 擴展從1.1.0版(iOS和Android)開始。

此功能還與 [!DNL VisitorAPI.js] 1.7.0版或更高版本。

## 移動到Web的ID共用 {#mobile-to-web}

使用 `getUrlVariables` 來自 [邊緣網路的標識](https://aep-sdks.gitbook.io/docs/foundation-extensions/identity-for-edge-network/api-reference#geturlvariables) 擴展，以作為查詢參數檢索標識符，並在開啟時將其附加到URL [!DNL webViews]。

Web SDK接受不需要其他配置 `ECID` 查詢字串中的值。

查詢字串參數包括：

* `MCID`:Experience CloudID(`ECID`)
* `MCORGID`:Experience Cloud `orgID` 必須與 `orgID` 在 [!DNL Web SDK]。
* `TS`:時間戳參數不能早於5分鐘。


移動到Web的ID共用使用 `adobe_mc` 的下界。 當 `adobe_mc` 參數存在且有效， `ECID` 在向邊緣網路發出的第一個請求中，自動將查詢字串添加到標識映射。 所有後續邊緣網路交互都將使用 `ECID`。

有關如何將訪問者ID從移動應用傳遞到WebView的詳細資訊，請參閱上的文檔 [處理WebView](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/app-implementation/web-views.html#implementation)。

## 跨域ID共用 {#cross-domain-sharing}

對於跨域ID共用，Web SDK 2.11.0版為 `appendIdentityToUrl` 的子菜單。 使用時，此命令將生成 `adobe_mc` 查詢字串參數。

該命令接受具有一個屬性的對象， `url`，並返回具有屬性的對象 `url`。

此命令不等待任何同意更新。 如果未提供同意，則返回URL時未更改。

如果 `ECID` 未提供， `/acquire` 將調用終結點以生成 `ECID`。

下面是客戶如何在其網站上實現跨域ID共用的示例。

此代碼為頁面上的所有按一下添加事件偵聽器，如果按一下的連結指向匹配的域（在本例中） `adobe.com` 或 `behance.com`)，將標識添加到URL並重定向用戶。

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

## 使用標籤擴展 {#tags-extension}

與使用 [!DNL Web SDK]，在 [!DNL Tags] 使用通過URL傳遞的身份的擴展。

要通過「標籤」擴展使用移動到Web和跨域ID共用，必須使用2.12.0版或更高版本的「標籤」擴展。

要將標識從當前頁面共用到其他域，請在 [!DNL Web SDK] [!DNL Tags] 擴展。 此操作旨在與 **[!UICONTROL 核心 — 按一下]** 事件類型和值比較條件。

按照說明的步驟操作 [這裡](../../tags/ui/managing-resources/rules.md) 建立具有以下配置的規則：

* [!UICONTROL 事件配置]:
   * **[!UICONTROL 擴充功能：核心]**
   * **[!UICONTROL 事件類型：按一下]**
   * 選擇 **[!UICONTROL 當用戶按一下>特定元素時]**
   * 鍵入 **[!UICONTROL 選擇器]**: `a[href]`。 此事件將隨時觸發錨點標籤在頁面上的 `href` 屬性。

      ![使用上述設定顯示事件配置的UI影像](assets/id-sharing-event-configuration.png)

* [!UICONTROL 條件配置]
   * **[!UICONTROL 邏輯類型]**: [!UICONTROL 常規]
   * **[!UICONTROL 擴展]**: [!UICONTROL 核心]
   * **[!UICONTROL 條件類型]**: [!UICONTROL 值比較]
   * **[!UICONTROL 左操作數]**: [!UICONTROL `%this.hostname%`]。 這是一個特殊的資料元素 [!UICONTROL 核心 — 按一下] 事件並解析為按一下的連結的主機名。
   * **[!UICONTROL 運算子]**: [!UICONTROL 匹配規則運算式]
   * **[!UICONTROL 右操作數]**:鍵入與要與共用標識的域匹配的規則運算式。 例如，要匹配以結尾為主機名的連結 `adobe.com` 或 `behance.com`，使用此規則運算式： `behance.com$|adobe.com$`。 連結的頁面需要 [!DNL Web SDK] 或 [!DNL Visitor ID] 安裝以接受身份。

      ![顯示具有上述設定的條件配置的UI影像](assets/id-sharing-condition-configuration.png)

* [!UICONTROL 動作設定]
   * **[!UICONTROL 擴展]**: [!UICONTROL Adobe Experience PlatformWeb SDK]
   * **[!UICONTROL 操作類型]**: [!UICONTROL 使用標識重定向]
   * **[!UICONTROL 實例]**:選擇實例。 在大多數情況下，您只配置了一個實例。 如果有多個實例，請選擇要共用標識的實例。

      ![顯示具有上述設定的操作配置的UI影像](assets/id-sharing-action-configuration.png)

的 **[!UICONTROL 使用標識重定向]** 操作將阻止瀏覽器導航到連結。 然後，它會 `appendIdentityToUrl` 方法 [!DNL Web SDK] 實例。

最後，它將用戶重定向到 [!DNL URL] 和 `adobe_mc` 查詢字串參數已附加。
