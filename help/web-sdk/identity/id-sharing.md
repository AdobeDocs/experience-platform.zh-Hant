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

一家服裝公司想要根據客戶的興趣來打造個人化體驗，並在同時載入WebViews的行動應用程式中維持個人化的準確性。 透過使用行動裝置對網頁的ID共用功能，他們可確保在應用程式和行動網站內容中使用相同的訪客識別碼，傳遞 [!DNL ECID] 移至行動網頁URL。

### 跨網域提供一致的個人化

一家擁有多個線上商店的零售商想要根據客戶興趣，在其網域間個人化購物者體驗。 零售商使用Web SDK跨網域ID共用功能，可依據客戶興趣在所有網域中提供正確的優惠。

### 增強訪客活動報告功能

技術零售商想要改善訪客活動報表，提供訪客從行動應用程式移至其行動網站或其他網域的相關資訊。 使用Web SDK跨網域ID共用功能，行銷團隊可以準確地追蹤訪客的網頁屬性並產生活動報表。

## 先決條件 {#prerequisites}

若要使用行動裝置對網頁和跨網域的ID共用，您必須使用 [!DNL Web SDK] 2.11.0版或更新版本。

若為Edge Network行動實作，此功能在 [邊緣網路的身分識別](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/) 擴充功能從1.1.0版(iOS和Android)開始。

此功能也與 [!DNL VisitorAPI.js] 1.7.0版或更新版本。

## 行動裝置對網頁ID共用 {#mobile-to-web}

使用 `getUrlVariables` 來自的API [邊緣網路的身分識別](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/api-reference/#geturlvariables) 擴充功能可將識別碼擷取為查詢引數，並在開啟時附加至URL [!DNL webViews].

Web SDK不需額外設定即可接受 `ECID` 查詢字串中的值。

查詢字串引數包括：

* `MCID`：Experience CloudID (`ECID`)
* `MCORGID`：Experience Cloud `orgID` 必須與 `orgID` 設定於 [!DNL Web SDK].
* `TS`：時間戳記引數不能超過五分鐘。


行動裝置對網頁的ID共用會使用 `adobe_mc` 引數。 當 `adobe_mc` 引數存在且有效， `ECID` 來自查詢字串的，會自動新增至在第一次向Edge Network提出要求時的身分對應。 所有後續的Edge Network互動都會使用 `ECID`.

如需如何將訪客ID從行動應用程式傳遞至WebView的詳細資訊，請參閱以下檔案： [處理WebView](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/app-implementation/web-views.html#implementation).

## 實作跨網域ID共用 {#cross-domain-sharing}

請參閱 [`appendIdentityToUrl`](../commands/appendidentitytourl.md) 使用Web SDK標籤擴充功能和Web SDK JavaScript程式庫的實作指示命令。
