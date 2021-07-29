---
title: 使用Adobe Experience Platform Debugger測試內嵌程式碼
description: 了解如何使用Platform Debugger在本機測試網站上不同Adobe Experience Platform的內嵌程式碼。
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 57%

---

# 使用 Adobe Experience Platform Debugger 測試內嵌程式碼

>[!NOTE]
>
>Adobe Experience Platform Launch在Adobe Experience Platform中已重新命名為一套資料收集技術。 因此，產品檔案中已推出數個術語變更。 有關術語更改的綜合參考，請參閱以下[document](../../term-updates.md)。

當您在Adobe Experience Platform中變更標籤程式庫組建時，應先測試這些變更，再將組建部署至生產環境。 如果您的網站沒有專用的測試或開發環境，您可以使用 Adobe Experience Platform Debugger 在本機測試網站中不同的內嵌程式碼。

## 先決條件

本教學課程需要妥善了解如何在資料收集UI中使用環境和內嵌程式碼。 如需詳細資訊，請參閱[環境概觀](./environments.md)。

此外，使用本教學課程前，您需先安裝 Platform Debugger 瀏覽器擴充功能。Platform Debugger 僅適用於 Chrome 和 Firefox 瀏覽器。開始教學課程之前，請先透過下列任一連結安裝擴充功能：

* [Chrome 版 Platform Debugger](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)
* [Firefox 版 Platform Debugger](https://addons.mozilla.org/zh-TW/firefox/addon/adobe-experience-platform-dbg/)

## 在網站上開啟 Platform Debugger

使用您選擇的瀏覽器導覽至您的網站，並開啟 Platform Debugger 擴充功能。Platform Debugger 所連線的網站會顯示在視窗底部。如果標籤目前在您的網站上執行，則會列在[!UICONTROL 摘要]標籤中。

![](./images/embed-code-testing/summary.png)

>[!NOTE]
>
>如果 Platform Debugger 一開始未能順利連線，您可能需要重新載入顯示您網站的瀏覽器索引標籤，才能再次嘗試連線。

## 更換內嵌程式碼

Platform Debugger連線至您的網站後，請在左側導覽中選取&#x200B;**[!UICONTROL Launch]**。 您可在此處查看網站上目前所執行程式庫組建的相關資訊，包括其環境和關聯的擴充功能。從此處，選擇&#x200B;**[!UICONTROL Configuration]**&#x200B;以顯示管理內嵌代碼的控制項。

![](./images/embed-code-testing/launch-tab.png)

在「[!UICONTROL 頁面內嵌程式碼]」下方會顯示您網站目前使用的內嵌程式碼。 在內嵌程式碼的右側選取「**[!UICONTROL 動作]**」，然後選取「**[!UICONTROL 取代]**」。

![](./images/embed-code-testing/replace.png)

此時畫面會顯示彈出視窗，提示您提供內嵌程式碼，以取代目前的程式碼。請注意，使用 Platform Debugger 取代內嵌程式碼不會變更網站上已部署的內嵌程式碼。相反地，這只會變更本機所執行的內嵌程式碼，以利您測試內嵌程式碼實作與偵測錯誤。

將您要測試的內嵌程式碼貼到提供的文字方塊中，然後選取&#x200B;**[!UICONTROL Apply]**。

![](./images/embed-code-testing/paste-code.png)

會重新顯示&#x200B;**[!UICONTROL Configuration]**&#x200B;標籤，指出即時內嵌程式碼已取代為您提供的程式碼。 您現在可以使用網頁瀏覽器，查看您測試的內嵌程式碼能否正常運作。

![](./images/embed-code-testing/code-replaced.png)

## 後續步驟

本教學課程說明如何使用 Platform Debugger 在本機上測試不同內嵌程式碼。如需 Platform Debugger 各項功能的詳細資訊，請參閱 [Platform Debugger 文件](https://experienceleague.adobe.com/docs/debugger/using-v2/experience-cloud-debugger.html)。
