---
title: 行動裝置對網頁和跨網域ID共用
description: 瞭解如何將訪客ID從行動裝置儲存至Web屬性，並儲存在各個網域中
keywords: 身分；行動；ID；共用；網域；跨網域；sdk；平台；
exl-id: b9bb236f-52cf-4615-96d8-1137d957de8c
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 0%

---

# 行動裝置對網頁和跨網域ID共用

## 概觀

Adobe Experience Platform Web SDK支援訪客ID共用功能，可讓客戶在行動應用程式和行動網站內容之間，以及跨網域更準確地提供個人化體驗。

## 使用案例 {#use-cases}

### 在行動應用程式和行動網站之間提供一致的個人化內容

一家服裝公司想要根據客戶的興趣來打造個人化體驗，並在同時載入WebViews的行動應用程式中維持個人化的準確性。 藉由使用行動裝置對網頁的ID共用功能，使用者可將[!DNL ECID]傳遞至行動網頁URL，使用應用程式和行動網頁內容中的相同訪客識別碼，確保向客戶呈現最正確的優惠。

### 跨網域提供一致的個人化

一家擁有多個線上商店的零售商想要根據客戶興趣，在其網域間個人化購物者體驗。 零售商使用Web SDK跨網域ID共用功能，可依據客戶興趣在所有網域中提供正確的優惠。

### 增強訪客活動報告功能

技術零售商想要改善訪客活動報表，提供訪客從行動應用程式移至其行動網站或其他網域的相關資訊。 使用Web SDK跨網域ID共用功能，行銷團隊可以準確地追蹤訪客的網頁屬性並產生活動報表。

## 先決條件 {#prerequisites}

若要使用行動裝置對網頁和跨網域識別碼共用，您必須使用[!DNL Web SDK] 2.11.0版或更新版本。

對於Edge Network行動實作，此功能從1.1.0版(iOS和Android)開始，在[Edge Network身分識別](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/)擴充功能中受到支援。

此功能也與[!DNL VisitorAPI.js] 1.7.0版或更新版本相容。

## 行動裝置對網頁ID共用 {#mobile-to-web}

使用Edge Network](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/api-reference/#geturlvariables)延伸模組[身分識別中的`getUrlVariables` API來擷取識別碼做為查詢引數，並在開啟[!DNL webViews]時將其附加至您的URL。

Web SDK不需額外設定，即可接受查詢字串中的`ECID`值。

查詢字串引數包括：

* `MCID`：Experience Cloud識別碼(`ECID`)
* `MCORGID`：Experience Cloud`orgID`必須符合[!DNL Web SDK]中設定的`orgID`。
* `TS`：時間戳記引數不能超過五分鐘。


行動裝置對網頁識別碼共用使用`adobe_mc`引數。 當`adobe_mc`引數存在且有效時，來自查詢字串的`ECID`會自動新增到對Edge Network發出的第一個要求中的身分對應。 所有後續Edge Network互動都會使用該`ECID`。

有關如何將訪客ID從行動應用程式傳遞至WebView的詳細資訊，請參閱[處理WebViews](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/app-implementation/web-views.html#implementation)的檔案。

## 實作跨網域ID共用 {#cross-domain-sharing}

如需使用Web SDK標籤擴充功能和Web SDK JavaScript程式庫的實作指示，請參閱[`appendIdentityToUrl`](../commands/appendidentitytourl.md)命令。
