---
keywords: 連接目標；目標連接；如何連接目標
title: 建立新的目的地連線
type: Tutorial
description: 本教學課程列出連線至Adobe Experience Platform中目的地的步驟
exl-id: 56d7799a-d1da-4727-ae79-fb2c775fe5a5
source-git-commit: f4721d3f114357b25517e4e66f1f626f82621c34
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%

---

# 建立新的目的地連線

## 概覽 {#overview}

您必須先設定與目的地平台的連線，才能將受眾資料傳送至目的地。 本文說明如何使用Adobe Experience Platform使用者介面來設定新目的地。

## 建立新的目的地連線 {#setup}

1. 前往&#x200B;**[!UICONTROL 連線]** > **[!UICONTROL 目的地]**，然後選取&#x200B;**[!UICONTROL 目錄]**&#x200B;標籤。

   ![目錄頁面](../assets/ui/connect-destinations/catalog.png)

1. 視您是否擁有與目的地的現有連線而定，您可以在目的地卡片上看到&#x200B;**[!UICONTROL 設定]**&#x200B;或&#x200B;**[!UICONTROL 啟用區段]**&#x200B;按鈕。 如需&#x200B;**[!UICONTROL 啟用區段]**&#x200B;與&#x200B;**[!UICONTROL 設定]**&#x200B;之間差異的詳細資訊，請參閱目標工作區檔案的[目錄](../ui/destinations-workspace.md#catalog)區段。

   選取「**[!UICONTROL 設定]**」或「**[!UICONTROL 啟用區段]**」，視您可使用的按鈕而定。

   ![目錄頁面](../assets/ui/connect-destinations/set-up.png)

   ![啟用區段](../assets/ui/connect-destinations/activate-segments.png)

1. 如果選擇了&#x200B;**[!UICONTROL Set up]**，請跳到下一步。

   如果您選取了&#x200B;**[!UICONTROL 啟用區段]**，您現在可以看到現有目的地連線清單。

   選擇&#x200B;**[!UICONTROL 配置新目標]**。

   ![配置新目標](../assets/ui/connect-destinations/configure-new-destination.png)

1. 輸入目標平台連接詳細資訊，然後選擇&#x200B;**[!UICONTROL 連接到目標]**。

   >[!NOTE]
   >
   >下圖僅供圖例之用。 目的地的連線詳細資訊因目的地而異。 如需您目的地的連線詳細資訊，請參閱每個[目的地目錄](../catalog/overview.md)頁面中的&#x200B;**連線參數**&#x200B;區段（例如[Google Customer Match](..//catalog/advertising/google-customer-match.md#parameters)）。

   ![連接到目標](../assets/ui/connect-destinations/connect-destination.png)

1. 選取&#x200B;**[!UICONTROL 「下一步」]**。

   ![連接到目標](../assets/ui/connect-destinations/next.png)

1. 選取適用於您要匯出至目的地之資料的行銷動作。 行銷動作會指出要將資料匯出至目的地的目的。 您可以從Adobe定義的行銷動作中選取，或者您可以建立自己的行銷動作。 如需行銷動作的詳細資訊，請參閱[資料使用原則概述](../../data-governance/policies/overview.md)頁面。

   ![選取行銷動作](../assets/ui/connect-destinations/governance.png)

1. 選取&#x200B;**[!UICONTROL 儲存並退出]**&#x200B;以儲存目的地設定，或選取&#x200B;**[!UICONTROL 下一個]**&#x200B;以繼續處理對象資料[啟動流程](activation-overview.md)。