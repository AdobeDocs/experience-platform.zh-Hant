---
title: 使用Adobe Experience Platform Assurance
description: 本指南說明在安裝及實作Adobe Experience Platform Assurance後，如何使用它。
source-git-commit: 24f452bdb923179eefe53fdb28d3a92d43e533cd
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---


# 使用Adobe Experience Platform Assurance

本教學課程說明如何使用Adobe Experience Platform Assurance。 如需安裝與實作Adobe Experience Platform Assurance擴充功能的指示，請參閱以下的教學課程： [實作保證延伸](./implement-assurance.md).

## 建立工作階段

登入 [保證UI](https://experience.adobe.com/assurance)，您可以選取 **[!UICONTROL 建立工作階段]** 以開始建立工作階段。

![系統會反白顯示「建立工作階段」按鈕，顯示您可在何處建立工作階段。](./images/using-assurance/create-session.png)

此 **[!UICONTROL 建立新工作階段]** 對話框。 請檢閱指示，然後選取 **[!UICONTROL 開始]**.

![隨即顯示「建立新工作階段」對話方塊，其中顯示如何使用「保證」的指示。](./images/using-assurance/create-new-session.png)

您現在可以輸入名稱以識別工作階段，然後提供 **[!UICONTROL 基本URL]** （應用程式的深層連結URL）。 提供這些詳細資訊後，請選取 **[!UICONTROL 下一個]**.

>[!INFO]
>
>基礎URL是用來從URL啟動應用程式的根定義。 會產生工作階段URL，您可借此啟動「保證」工作階段。 範例值看起來可能像： `myapp://default` 在 **[!UICONTROL 基本URL]** 欄位，輸入應用程式的基礎深層連結定義。

![隨即顯示建立新工作階段的完整工作流程。](./images/using-assurance/create-session.gif)

## 連接到會話

建立工作階段後，請確定您會看到 **[!UICONTROL 建立新工作階段]** 對話框現在會顯示一個連結、QR碼和PIN碼。

![畫面上會顯示對話方塊，顯示連線至您的保證工作階段的選項。](./images/using-assurance/create-new-session-pin.png)

如果出現此對話方塊，您可以使用裝置的相機應用程式掃描QR碼，以及開啟應用程式，或複製連結並在應用程式中開啟。 當您的應用程式啟動時，應該會看到PIN項目畫面重疊。 從上一步輸入PIN，然後按 **[!UICONTROL Connect]**.

當應用程式上顯示Adobe Experience Platform圖示(紅色Adobe「A」)時，您可以確認您的應用程式已連線至「保證」。

![將顯示將應用程式連接到保證會話的完整工作流。](./images/using-assurance/connect-session.gif)

## 匯出工作階段

若要匯出「保證」工作階段，請在應用程式的工作階段詳細資訊頁面上，選取 **[!UICONTROL 匯出至JSON]** 在工作階段中：

![匯出工作階段](./images/using-assurance/export-session.png)

匯出選項會遵循搜尋篩選結果，而只匯出事件檢視中顯示的事件。 例如，如果您搜尋「track」事件，然後選取 **[!UICONTROL 匯出至JSON]**，只會匯出「track」事件結果。
