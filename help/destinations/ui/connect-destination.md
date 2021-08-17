---
keywords: 連接目標；目標連接；如何連接目標
title: 建立新的目的地連線
type: Tutorial
description: 本教學課程列出連線至Adobe Experience Platform中目的地的步驟
exl-id: 56d7799a-d1da-4727-ae79-fb2c775fe5a5
source-git-commit: 3aac1e7c7fe838201368379da8504efc8e316e1c
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 0%

---

# 建立新的目的地連線

## 概覽 {#overview}

您必須先設定與目的地平台的連線，才能將受眾資料傳送至目的地。 本文說明如何使用Adobe Experience Platform使用者介面來設定新目的地。

## 建立新的目的地連線 {#setup}

### 選擇目標 {#select-destination}

1. 前往&#x200B;**[!UICONTROL 連線]** > **[!UICONTROL 目的地]**，然後選取&#x200B;**[!UICONTROL 目錄]**&#x200B;標籤。

   ![目錄頁面](../assets/ui/connect-destinations/catalog.png)

1. 視您是否擁有與目的地的現有連線而定，您可以在目的地卡片上看到&#x200B;**[!UICONTROL Configure]**&#x200B;或&#x200B;**[!UICONTROL Activate]**&#x200B;按鈕。 有關&#x200B;**[!UICONTROL Activate]**&#x200B;和&#x200B;**[!UICONTROL Configure]**&#x200B;之間差異的詳細資訊，請參閱目標工作區檔案的[Catalog](../ui/destinations-workspace.md#catalog)區段。 選擇&#x200B;**[!UICONTROL Configure]**&#x200B;或&#x200B;**[!UICONTROL Activate]**，具體取決於您可用的按鈕。

   ![目錄頁面](../assets/ui/connect-destinations/set-up.png)

   ![啟用區段](../assets/ui/connect-destinations/activate-segments.png)

<!-- 1. If you selected **[!UICONTROL Set up]**, skip this step. If you selected **[!UICONTROL Activate segments]**, you can now see a list of the existing destination connections. Select **[!UICONTROL Configure new destination]**.

   ![Configure new destination](../assets/ui/connect-destinations/configure-new-destination.png) -->

### 帳戶步驟 {#account}

選擇&#x200B;**[!UICONTROL 新帳戶]**&#x200B;以設定到目標的新連接。 或者，如果您先前已設定了到目標的連接，請選擇&#x200B;**[!UICONTROL 現有帳戶]**&#x200B;並選擇現有連接。

您在帳戶步驟中輸入的憑證會依目的地和驗證類型而異。

* 對於雲端儲存目的地，您需要提供Experience Platform憑證以連線至您的儲存位置。

   ![為雲端儲存目的地選取帳戶類型](../assets/ui/connect-destinations/new-account-cloud-storage.png)

* 若為Facebook和其他數個社交和廣告目的地，請選取「**[!UICONTROL 新帳戶]**」 ，然後選取「**[!UICONTROL 連線至目的地]**」 。 這會將您帶往目的地登入頁面，以便將Experience Platform連線至目的地。

   ![選擇社交目的地的帳戶類型](../assets/ui/connect-destinations/new-account.png)

>[!IMPORTANT]
>
>有關此步驟所需參數的詳細資訊（例如[Azure Blob](../catalog/cloud-storage/azure-blob.md#parameters)需要連接字串），請參閱每個目標目錄頁中的&#x200B;**[!UICONTROL 連接參數]**&#x200B;部分。

### 驗證步驟 {#authentication}

輸入目標平台連接詳細資訊，然後選擇&#x200B;**[!UICONTROL 建立目標]**。

1. 選取適用於您要匯出至目的地之資料的行銷動作。 行銷動作會指出要將資料匯出至目的地的目的。 您可以從Adobe定義的行銷動作中選取，或者您可以建立自己的行銷動作。 如需行銷動作的詳細資訊，請參閱[資料使用原則概述](../../data-governance/policies/overview.md)頁面。

   >[!IMPORTANT]
   >
   >下圖僅供圖例之用。 目的地的連線詳細資訊因目的地而異。 如需您目的地的連線詳細資訊，請參閱每個[目的地目錄](../catalog/overview.md)頁面中的&#x200B;**[!UICONTROL 連線參數]**&#x200B;區段（例如[Google Customer Match](../catalog/advertising/google-customer-match.md#parameters)）。

   ![連接到目標](../assets/ui/connect-destinations/connect-destination.png)

1. 選取&#x200B;**[!UICONTROL 儲存並退出]**&#x200B;以儲存目的地設定，或選取&#x200B;**[!UICONTROL 下一個]**&#x200B;以繼續處理對象資料[啟動流程](activation-overview.md)。