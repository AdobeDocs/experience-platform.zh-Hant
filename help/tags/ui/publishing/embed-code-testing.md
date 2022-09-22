---
title: 使用Adobe Experience Platform Debugger測試內嵌程式碼
description: 了解如何使用Platform Debugger在本機測試網站上不同Adobe Experience Platform的內嵌程式碼。
exl-id: ae6183b9-0d25-49d0-b0e9-f8b5ba58ab33
source-git-commit: 0c2ee3bbb4d85bd755b4847a509fc7bd50ba67bc
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 62%

---

# 使用 Adobe Experience Platform Debugger 測試內嵌程式碼

>[!NOTE]
>
>Adobe Experience Platform Launch在Adobe Experience Platform中已重新命名為一套資料收集技術。 因此，所有產品文件中出現了幾項術語變更。 如需術語變更的彙整參考資料，請參閱以下[文件](../../term-updates.md)。

當您在Adobe Experience Platform中變更標籤程式庫組建時，應先測試這些變更，再將組建部署至生產環境。 如果您的網站沒有專用的測試或開發環境，您可以使用 Adobe Experience Platform Debugger 在本機測試網站中不同的內嵌程式碼。

## 先決條件

本教學課程需要妥善了解如何在資料收集UI中使用環境和內嵌程式碼。 如需詳細資訊，請參閱[環境概觀](./environments.md)。

此外，使用本教學課程前，您需先安裝 Platform Debugger 瀏覽器擴充功能。Platform Debugger 僅適用於 Chrome 和 Firefox 瀏覽器。開始教學課程之前，請先透過下列任一連結安裝擴充功能：

* [Chrome 版 Platform Debugger](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)
* [Firefox 版 Platform Debugger](https://addons.mozilla.org/zh-TW/firefox/addon/adobe-experience-platform-dbg/)

## 在網站上開啟 Platform Debugger

使用您選擇的瀏覽器導覽至您的網站，並開啟 Platform Debugger 擴充功能。Platform Debugger 所連線的網站會顯示在視窗底部。如果標籤目前在您的網站上執行，則會列在 [!UICONTROL 摘要] 標籤。

![](./images/embed-code-testing/summary.png)

>[!NOTE]
>
>如果 Platform Debugger 一開始未能順利連線，您可能需要重新載入顯示您網站的瀏覽器索引標籤，才能再次嘗試連線。

## 更換內嵌程式碼

Platform Debugger連線至您的網站後，請選取 **[!UICONTROL Launch]** 的下一頁。 您可在此處查看網站上目前所執行程式庫組建的相關資訊，包括其環境和關聯的擴充功能。從此處，選擇 **[!UICONTROL 設定]** 顯示管理內嵌程式碼的控制項。

![](./images/embed-code-testing/launch-tab.png)

在 [!UICONTROL 頁面內嵌程式碼]，則會顯示您的網站目前使用的內嵌程式碼。 選擇 **[!UICONTROL 動作]** 在內嵌程式碼的右側，選取 **[!UICONTROL 取代]**.

![](./images/embed-code-testing/replace.png)

此時畫面會顯示彈出視窗，提示您提供內嵌程式碼，以取代目前的程式碼。請注意，使用 Platform Debugger 取代內嵌程式碼不會變更網站上已部署的內嵌程式碼。相反地，這只會變更本機所執行的內嵌程式碼，以利您測試內嵌程式碼實作與偵測錯誤。

將您要測試的內嵌程式碼貼到提供的文字方塊，然後選取 **[!UICONTROL 套用]**.

![](./images/embed-code-testing/paste-code.png)

此 **[!UICONTROL 設定]** 標籤，指出即時內嵌程式碼已替換為您提供的程式碼。 您現在可以使用網頁瀏覽器，查看您測試的內嵌程式碼能否正常運作。

![](./images/embed-code-testing/code-replaced.png)

## 後續步驟

本教學課程說明如何使用 Platform Debugger 在本機上測試不同內嵌程式碼。如需 Platform Debugger 各項功能的詳細資訊，請參閱 [Platform Debugger 文件](../../../debugger/home.md)。
