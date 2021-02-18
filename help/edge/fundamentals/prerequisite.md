---
title: 使用Adobe Experience Platform Web SDK的必要條件
description: 瞭解使用Adobe Experience Platform Web SDK的必要條件。
keywords: 第一方域；CNAME;schema;create schema;launch;aep web sdk extension;extension;configuration id;configuration tool;data element;create data element;XDM Object;sendEvent;sendEvent;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 0%

---


# 使用Adobe Experience Platform Web SDK的必要條件

若要使用平台網頁SDK，您必須先：

- 為您的組織布建此功能。 (如果您想要取得存取權，可免費存取平台網頁SDK，請聯絡您的客戶成功經理(CSM)。
- 啟用第一方網域(CNAME)。 如果您已擁有Adobe Analytics的CNAME，則應使用該CNAME。 在開發中進行測試沒有CNAME，但您在投入生產前需要CNAME。

>[!IMPORTANT]
>
>**請注意，自11/10/20起，第一方CNAME實作在所有Safari瀏覽器和行動iOS裝置上都有7天的到期日。**

- 取得Adobe Experience Platform的權益。 如果您尚未購買Adobe Experience Platform,Adobe將提供您必要的存取權，讓您以有限的方式使用SDK，毋需額外付費。
- 如果您的網站已在您的網站上使用[Experience Cloud ID服務](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html)（透過Adobe Experience Platform Launch內的訪客API或Experience Cloud ID服務擴充功能），而您想要在移轉至Adobe Experience Platform Web SDK時繼續使用它，則必須使用最新版的訪客API或體驗雲端ID服務擴充功能。 如需詳細資訊，請參閱[ID移轉](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en#identity)。
