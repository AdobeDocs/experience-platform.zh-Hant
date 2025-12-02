---
title: 傳送推播訂閱
description: 註冊、傳送及收集瀏覽器推播訂閱的資料。
source-git-commit: 3abe25a9c538bf4d1b439d48f624d8cad109a99e
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 2%

---

# 傳送推播訂閱

>[!AVAILABILITY]
>
>Web SDK的推播通知目前在&#x200B;**測試版**&#x200B;中。 功能和檔案可能會有所變更。

**[!UICONTROL Send push subscription]**&#x200B;動作會向Adobe Experience Platform註冊推播通知訂閱。 它會處理來自瀏覽器的推送訂閱詳細資訊擷取，並將它們傳送至您設定的資料流。 它適用於Web SDK擴充功能2.32.0版或更新版本。

1. 使用您的Adobe ID憑證登入[experience.adobe.com](https://experience.adobe.com)。
1. 導覽至&#x200B;**[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**。
1. 選取所需的標籤屬性。
1. 導覽至&#x200B;**[!UICONTROL Rules]**，然後選取所需的規則。
1. 在[!UICONTROL Actions]下，選取現有動作或建立動作。
1. 將[!UICONTROL Extension]下拉欄位設定為&#x200B;**[!UICONTROL Adobe Experience Platform Web SDK]**&#x200B;並將[!UICONTROL Action Type]設定為&#x200B;**[!UICONTROL Send push subscription]**。

除了選取SDK執行個體外，動作沒有任何組態設定。

使用此命令之前，在設定擴充功能時，請務必設定有效的[VAPID公開金鑰](../configure/push-notifications.md)。

此動作是等同於[`sendPushSubscription`](/help/collection/js/commands/sendpushsubscription.md)命令的標籤延伸。 如需有關先決條件、建議的執行頻率、命令運作方式和錯誤處理的資訊，請參閱連結頁面。

>[!MORELIKETHIS]
>
>* [設定推播通知](../configure/push-notifications.md)
>* [網頁推播API規格](https://developer.mozilla.org/en-US/docs/Web/API/Push_API)
>* [Service Worker API](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API)
