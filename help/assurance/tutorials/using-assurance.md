---
title: 使用 Adobe Experience Platform Assurance
description: 本指南會說明在安裝並實作 Adob​​e Experience Platform Assurance 之後如何使用。
exl-id: 872c83d1-82e8-40d8-9b66-3e51a91a955f
source-git-commit: f8576e7f7e1da7351f7860cba27d5d09d0161132
workflow-type: tm+mt
source-wordcount: '674'
ht-degree: 28%

---

# 使用 Adobe Experience Platform Assurance

本教學課程會說明如何使用 Adob&#x200B;&#x200B;e Experience Platform Assurance。如需有關如何安裝和實作 Adob&#x200B;&#x200B;e Experience Platform Assurance 擴充功能的說明，請閱讀有關[實作 Assurance 擴充功能](./implement-assurance.md)的教學課程。

## 建立工作階段

登入[Assurance UI](https://experience.adobe.com/assurance)後，您可以選取&#x200B;**[!UICONTROL Create Session]**&#x200B;開始建立工作階段。

![建立工作階段按鈕會反白顯示，向您顯示可以在哪裡建立工作階段。](./images/using-assurance/create-session.png)

**[!UICONTROL Create New Session]**&#x200B;對話方塊會出現，其中包含兩個建立工作階段的選項：

### 深層連結連線

選取此選項可產生唯一的工作階段URL、QR碼和PIN。 掃描二維碼或手動開啟應用程式中的工作階段連結，然後輸入PIN碼以建立連線。

選取&#x200B;**[!UICONTROL Deep link connect]**&#x200B;並選取&#x200B;**[!UICONTROL Start]**&#x200B;以繼續。

![已選取[建立新工作階段]對話方塊，其中顯示[深層連結連線]選項。](./images/using-assurance/create-new-session-deep-link.png)

您現在可以輸入名稱來識別工作階段，然後提供&#x200B;**[!UICONTROL Base URL]** （您應用程式的深層連結URL）。 提供這些詳細資料後，請選取&#x200B;**[!UICONTROL Next]**。

>[!INFO]
>
>基礎 URL 是用於從 URL 啟動應用程式的根定義。會產生一個工作階段 URL，您可藉以啟動 Assurance 工作階段。範例值可能如下所示： `myapp://default`在&#x200B;**[!UICONTROL Base URL]**&#x200B;欄位中，輸入應用程式的基礎深層連結定義。

![顯示工作階段名稱和基本URL輸入欄位。](./images/using-assurance/create-session-form-deep-link.png)

### 快速連線

觸發來自應用程式的連線，而您的裝置會出現在可用裝置清單中。 選取&#x200B;**[!UICONTROL Quick connect]**&#x200B;以建立Assurance工作階段。

#### 先決條件

使用「快速連線」之前，請確認您的應用程式具備必要的SDK版本和實作：

**Android SDK需求：**

- Mobile Core v3.1.0 或更新版本
- Adobe Journey Optimizer v3.1.0 或更新版本
- Adobe Experience Platform Assurance v3.0.4或更新版本

**iOS SDK需求：**

- Mobile Core v5.2.0 或更新版本
- Adobe Journey Optimizer v5.1.1 或更新版本
- Adobe Experience Platform Assurance v5.0.0或更新版本

**實作：**

您的應用程式必須實作[`startSession` API](https://developer.adobe.com/client-sdks/home/base/assurance/api-reference/#startsession-quick-connect)才能觸發Assurance連線。 此API呼叫通常包含在動作集中或是在應用程式中觸發。

#### 建立快速連線工作階段

![已選取顯示[快速連線]選項的[建立新工作階段]對話方塊。](./images/using-assurance/create-new-session-quick-connect.png)

選取「**[!UICONTROL Quick connect]**」並選取「**[!UICONTROL Start]**」以繼續，您將會看到裝置選擇器介面：

1. **觸發Assurance連線** — 在您的行動應用程式或實作中，觸發使用`startSession` API起始Assurance連線的動作。 這會讓您的裝置可供探索。

2. **選取並連線您的裝置** — 一旦您的裝置出現在可用裝置清單中，請選取並按一下&#x200B;**[!UICONTROL Connect]**。

![顯示可用裝置的[快速連線]裝置選擇器介面。](./images/using-assurance/quick-connect-device-picker.png)

## 連線到工作階段

連線的步驟取決於您使用的作業階段型別：

### 深層連結連線工作階段

針對以&#x200B;**[!UICONTROL Deep Link Connect]**&#x200B;建立的工作階段：

1. 導覽至您的工作階段詳細資訊頁面（針對現有工作階段），或繼續建立工作階段，以檢視連結、QR碼和PIN
2. 使用裝置的相機應用程式來掃描二維碼，或複製連結並在應用程式中開啟
3. 當您的應用程式啟動時，您會看到PIN輸入畫面重疊。 輸入PIN並按&#x200B;**[!UICONTROL Connect]**

![顯示連線到 Assurance 工作階段的選項的對話框會隨即顯示。](./images/using-assurance/deep-link-connection.png)

### 快速連線工作階段

對於以&#x200B;**[!UICONTROL Quick Connect]**&#x200B;建立的工作階段（可由以`adobeassurance://`開頭的工作階段URL識別），連線會透過裝置選擇器介面自動進行：

1. 導覽至您的階段作業詳細資訊頁面（針對現有階段作業），或從建立階段作業繼續進行
2. 在&#x200B;**[!UICONTROL Connect Device]**&#x200B;區段中，您會看到裝置選擇器介面
3. 觸發應用程式中設定的動作，讓裝置可供探索
4. 從清單中選取您的裝置，然後按一下&#x200B;**[!UICONTROL Connect]**

![裝置選擇器介面顯示可連線的可用裝置。](./images/using-assurance/quick-connect-device-picker.png)

### 正在驗證連線

您的應用程式上顯示 Adob&#x200B;&#x200B;e Experience Platform 圖示 (紅色的 Adob&#x200B;&#x200B;e「A」) 時，您可以驗證您的應用程式是否已和 Assurance 連線。

## 匯出工作階段

若要匯出Assurance工作階段，請在應用程式的工作階段詳細資訊頁面上，選取工作階段中的&#x200B;**[!UICONTROL Export to JSON]**：

![匯出一個工作階段](./images/using-assurance/export-session.png)

匯出選項會遵守搜尋篩選結果，並且只會匯出顯示在事件檢視中的事件。例如，如果您搜尋「track」事件，然後選取「**[!UICONTROL Export to JSON]**」，則只會匯出「track」事件結果。