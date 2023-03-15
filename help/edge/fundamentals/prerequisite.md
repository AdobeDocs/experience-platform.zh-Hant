---
title: 使用Adobe Experience Platform Web SDK的必要條件
description: 了解使用Adobe Experience Platform Web SDK的必要條件。
keywords: 第一方網域；CNAME；結構；建立結構；launch;aep web sdk擴充功能；擴充功能；組態ID；組態工具；資料元素；建立資料元素；XDM物件；sendEvent；傳送事件；
exl-id: 98ae69db-bc87-4ea3-b101-664ac53e7ae0
source-git-commit: 6a9882224cba08718c81a3aead237107b3e47726
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 0%

---

# 使用Adobe Experience Platform Web SDK的必要條件

若要使用Adobe Experience Platform Web SDK，您必須先：

- 為您組織中的使用者設定正確的權限。 所有Experience Cloud客戶都能存取資料收集工具，您組織中的每位使用者只需要結構、身分和資料流的權限。 若要深入了解如何設定這些權限，請參閱 [資料收集權限管理](https://experienceleague.adobe.com/docs/experience-platform/collection/permissions.html?lang=en).
- 建議啟用第一方網域(CNAME)。 如果您已有Adobe Analytics的CNAME，則應使用該CNAME。 在開發中進行測試沒有CNAME，但Adobe建議您先有CNAME，再投入生產。 雖然CNAME實作不會提供Cookie存留期的任何優點，但可防止特定廣告封鎖程式和較不常見的瀏覽器封鎖SDK請求。 在這些情況下，使用CNAME可能會防止使用這些工具的使用者中斷資料收集作業。

>[!IMPORTANT]
>
>**請注意，自11/10/20起，第一方CNAME實作的所有Safari瀏覽器和行動iOS裝置都有7天的到期日。**

- 如果您的網站已使用 [Experience CloudID服務](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html) 在您的網站上(透過Adobe Experience Platform Launch中的訪客API或Experience CloudID服務擴充功能)，而且您想在移轉至Adobe Experience Platform Web SDK時繼續使用，則必須使用最新版的訪客API或Experience CloudID服務擴充功能。 請參閱 [ID移轉](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en#identity) 以取得更多資訊。
