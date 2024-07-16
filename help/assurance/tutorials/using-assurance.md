---
title: 使用 Adobe Experience Platform Assurance
description: 本指南會說明在安裝並實作 Adob​​e Experience Platform Assurance 之後如何使用。
exl-id: 872c83d1-82e8-40d8-9b66-3e51a91a955f
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 100%

---

# 使用 Adobe Experience Platform Assurance

本教學課程會說明如何使用 Adob&#x200B;&#x200B;e Experience Platform Assurance。如需有關如何安裝和實作 Adob&#x200B;&#x200B;e Experience Platform Assurance 擴充功能的說明，請閱讀有關[實作 Assurance 擴充功能](./implement-assurance.md)的教學課程。

## 建立工作階段

登入 [Assurance UI](https://experience.adobe.com/assurance) 後，您可選取「**[!UICONTROL 建立工作階段]**」，即可開始建立工作階段。

![建立工作階段按鈕會反白顯示，向您顯示可以在哪裡建立工作階段。](./images/using-assurance/create-session.png)

「**[!UICONTROL 建立新工作階段]**」對話框會隨即顯示。請檢閱規定的說明，然後選取「**[!UICONTROL 開始]**」以繼續進行。

![「建立新工作階段」對話框會隨即顯示，其中會顯示有關如何使用 Assurance 的說明。](./images/using-assurance/create-new-session.png)

您現在可以輸入名稱以識別工作階段，然後提供&#x200B;**[!UICONTROL 基礎 URL]** (您的應用程式的深度連結 URL)。提供這些詳細資料後，請選取「**[!UICONTROL 下一步]**」。

>[!INFO]
>
>基礎 URL 是用於從 URL 啟動應用程式的根定義。會產生一個工作階段 URL，您可藉以啟動 Assurance 工作階段。範例值可能如下所示：`myapp://default`在&#x200B;**[!UICONTROL 基礎 URL]** 欄位中，輸入您的應用程式的基礎深度連結定義。

![建立新工作階段的完整工作流程即會顯示。](./images/using-assurance/create-session.gif)

## 連線到工作階段

建立工作階段後，請確保您看到「**[!UICONTROL 建立新工作階段]**」對話框現在顯示一個連結、一個 QR 碼和一個 PIN。

![顯示連線到 Assurance 工作階段的選項的對話框會隨即顯示。](./images/using-assurance/create-new-session-pin.png)

如果顯示此對話框，您可以使用裝置的相機應用程式掃描 QR 碼並開啟您的應用程式，或者將連結複製並在您的應用程式中開啟。您的應用程式啟動時，您應該會看到 PIN 登入畫面重疊。請輸入上一步中的 PIN，然後按下「**[!UICONTROL 連線]**」。

您的應用程式上顯示 Adob&#x200B;&#x200B;e Experience Platform 圖示 (紅色的 Adob&#x200B;&#x200B;e「A」) 時，您可以驗證您的應用程式是否已和 Assurance 連線。

![將您的應用程式和 Assurance 工作階段連線的完整工作流程會隨即顯示。](./images/using-assurance/connect-session.gif)

## 匯出工作階段

若要匯出 Assurance 工作階段，請在應用程式的工作階段詳細資料頁面上，在工作階段中選取「**[!UICONTROL 匯出為 JSON]**」：

![匯出一個工作階段](./images/using-assurance/export-session.png)

匯出選項會遵守搜尋篩選結果，並且只會匯出顯示在事件檢視中的事件。例如，如果您搜尋「追蹤」事件，然後選取「**[!UICONTROL 匯出為 JSON]**」，則只會匯出「追蹤」事件的結果。
