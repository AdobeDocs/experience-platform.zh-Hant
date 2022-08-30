---
title: 使用Adobe Experience PlatformWeb SDK的先決條件
description: 瞭解使用Adobe Experience PlatformWeb SDK的先決條件。
keywords: 第一方域；CNAME；架構；建立模式；啟動；aep web sdk擴展；擴展；配置ID；配置工具；資料元；建立資料元；XDM對象；sendEvent;send Event;
exl-id: 98ae69db-bc87-4ea3-b101-664ac53e7ae0
source-git-commit: 6a9882224cba08718c81a3aead237107b3e47726
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 0%

---

# 使用Adobe Experience PlatformWeb SDK的先決條件

要使用Adobe Experience PlatformWeb SDK，必須首先：

- 為組織中的用戶配置了正確的權限。 所有Experience Cloud客戶都有權訪問資料收集工具，您組織中的每個用戶只需要對架構、標識和資料流的權限。 要詳細瞭解如何設定這些權限，請參閱我們的文檔 [資料收集權限管理](https://experienceleague.adobe.com/docs/experience-platform/collection/permissions.html?lang=en)。
- 建議啟用第一方域(CNAME)。 如果你已經有Adobe Analytics的CNAME，你應該用那個。 在開發中進行測試沒有CNAME，但Adobe建議在您投入生產前先使用一個。 雖然CNAME實現在Cookie生存期方面沒有提供任何好處，但它可以阻止某些廣告攔截程式和不太常見的瀏覽器阻止SDK請求。 在這些情況下，使用CNAME可能會防止使用這些工具的用戶中斷資料收集。

>[!IMPORTANT]
>
>**請注意，自11/10/20起，第一方CNAME實施在所有Safari瀏覽器和移動iOS設備上都有7天的期限。**

- 如果您的網站已使用 [Experience CloudID服務](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html) 在您的網站上(通過訪問者API或Adobe Experience Platform Launch內的Experience CloudID服務擴展)，並且您希望在遷移到Adobe Experience PlatformWeb SDK時繼續使用它，您必須使用訪問者API的最新版本或Experience CloudID服務擴展。 請參閱 [ID遷移](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en#identity) 的子菜單。
