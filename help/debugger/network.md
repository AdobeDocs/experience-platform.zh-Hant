---
title: 網路標籤
description: 瞭解如何使用Adobe Experience Platform Debugger中的「網路」標籤。
keywords: Debugger；Experience Platform Debugger 擴充功能；Chrome；擴充功能；網路；資訊
seo-description: Experience Platform Debugger Network screen
seo-title: Network Tab
uuid: 839686c9-6e4f-4661-acf6-150ea24dc47f
exl-id: ed0579ef-ec26-43df-9453-a395c105038a
source-git-commit: df1a67e4b6f3d2eaeaba2b8d3c9b1588ee0b1461
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 62%

---

# 網路標籤

**網路**&#x200B;索引標籤會彙總頁面上發出的所有Adobe Experience Cloud解決方案呼叫，並依從左到右的順序顯示。 標準參數會自動加上好記名稱的標示，並將相同角色的常見參數編排為分組顯示。

![](images/network.jpg)

若要比較不同點擊數的索引鍵值組，此畫面相當實用。您可確認整合時所使用的參數 (例如 Experience Cloud 訪客 ID 或補充資料 ID)，在各整合作業之間是否一致。

>[!NOTE]
>
>目前並非解決方案呼叫中傳遞的所有參數 (例如 Analytics 內容變數、Target 自訂參數或 Experience Cloud ID 服務客戶 ID) 都會顯示在網路畫面中。

若要依解決方案變更資訊，請從左側導覽的清單中選取您要檢視的解決方案。篩選下列範例以僅顯示 Analytics：

![](images/network-analytics.jpg)

若要返回顯示所有解決方案，請選取&#x200B;**[!UICONTROL 網路]**

選取「網路」檢視中的專案以檢視展開檢視。 從展開的視圖視窗中，您可以將顯示的資訊複製到剪貼簿。

![](images/network-expand.jpg)

<!--Use the icon at the top of each column to copy the server call URL to your clipboard, where you can paste it into another document for reference or debugging purposes.

![](images/copy.jpg)-->

若要清除清單，請選取&#x200B;**[!UICONTROL 移除事件]**。

若要下載包含此熒幕上資訊的Excel檔案，請選取&#x200B;**[!UICONTROL 下載]**。
