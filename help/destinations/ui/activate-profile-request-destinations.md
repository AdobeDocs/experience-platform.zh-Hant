---
keywords: 啟用設定檔要求目的地；啟用資料；設定檔要求目的地
title: 對設定檔請求目的地啟用受眾資料（測試版）
type: Tutorial
seo-title: Activate audience data to profile request destinations
description: 了解如何將區段對應至設定檔要求目的地，以啟動您在Adobe Experience Platform中擁有的對象資料。
seo-description: Learn how to activate the audience data you have in Adobe Experience Platform by mapping segments to profile request destinations.
source-git-commit: 0635828cf3f637e67d2cabda860ca452e61892d4
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 0%

---

# 對設定檔請求目的地啟用受眾資料（測試版）

## 總覽 {#overview}

>[!IMPORTANT]
>
>Adobe Experience Platform中的設定檔要求目的地目前為測試版。 檔案和功能可能會有所變更。

本文說明在Adobe Experience Platform設定檔要求目的地中啟用受眾資料所需的工作流程。 設定檔要求目的地的範例是[Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md)和[自訂個人化](../../destinations/catalog/personalization/custom-personalization.md)連線。

## 先決條件 {#prerequisites}

若要將資料激活到目的地，您必須已成功[連接到目標](./connect-destination.md)。 如果尚未這麼做，請前往[目標目錄](../catalog/overview.md)，瀏覽支援的目標，並設定您要使用的目標。

### 區段合併原則 {#merge-policy}

目前，設定檔要求目的地僅支援啟用使用[預設合併原則](../../segmentation/ui/segment-builder.md#merge-policies)的區段。

## 選取您的目的地 {#select-destination}

1. 前往&#x200B;**[!UICONTROL 連線>目的地]**，然後選取&#x200B;**[!UICONTROL 目錄]**&#x200B;標籤。

   ![目標目錄索引標籤](../assets/ui/activate-segment-streaming-destinations/catalog-tab.png)

1. 在與您要啟用區段的目的地對應的卡片上，選取「啟用區段」**[!UICONTROL ，如下圖所示。]**

   ![激活按鈕](../assets/ui/activate-profile-request-destinations/activate-segments-button.png)

1. 選取您要用來啟用區段的目的地連線，然後選取&#x200B;**[!UICONTROL Next]**。

   ![選擇目標](../assets/ui/activate-profile-request-destinations/select-destination.png)

1. 移至下一個區段至[選取您的區段](#select-segments)。

## 選取您的區段 {#select-segments}

使用區段名稱左側的核取方塊，選取您要啟用至目的地的區段，然後選取&#x200B;**[!UICONTROL Next]**。

![選取區段](../assets/ui/activate-profile-request-destinations/select-segments.png)

## 排程區段匯出 {#scheduling}

依預設，「[!UICONTROL 區段排程]」頁面只會顯示您在目前啟動流程中選取的新區段。

![新區段](../assets/ui/activate-profile-request-destinations/new-segments.png)

若要查看所有要啟動至您目的地的區段，請使用篩選選項並停用&#x200B;**[!UICONTROL 僅顯示新區段]**&#x200B;篩選。

![所有區段](../assets/ui/activate-profile-request-destinations/all-segments.png)

在&#x200B;**[!UICONTROL 區段排程]**&#x200B;頁面上，選取每個區段，然後使用&#x200B;**[!UICONTROL 開始日期]**&#x200B;和&#x200B;**[!UICONTROL 結束日期]**&#x200B;選取器來設定將資料傳送至目的地的時間間隔。

![區段排程](../assets/ui/activate-profile-request-destinations/segment-schedule.png)

選擇&#x200B;**[!UICONTROL Next]**&#x200B;以轉至[!UICONTROL Review]頁。

## 檢閱 {#review}

在&#x200B;**[!UICONTROL 檢閱]**&#x200B;頁面上，您會看到您所選項目的摘要。 選擇&#x200B;**[!UICONTROL 取消]**&#x200B;以分解流，選擇&#x200B;**[!UICONTROL 返回]**&#x200B;以修改設定，或選擇&#x200B;**[!UICONTROL 完成]**&#x200B;以確認您的選擇並開始向目標發送資料。

>[!IMPORTANT]
>
>在此步驟中，Adobe Experience Platform會檢查資料使用政策是否違反。 以下顯示違反原則的範例。 除非您解決違規，否則無法完成區段啟用工作流程。 有關如何解決策略違規的資訊，請參閱資料控管文檔部分中的[策略實施](../../rtcdp/privacy/data-governance-overview.md#enforcement)。

![資料策略違規](../assets/common/data-policy-violation.png)

如果未檢測到任何違反策略的情況，請選擇&#x200B;**[!UICONTROL 完成]**&#x200B;以確認您的選擇並開始向目標發送資料。

![檢閱](../assets/ui/activate-profile-request-destinations/review.png)

## 驗證區段啟用 {#verify}

請查看[目標監視文檔](../../dataflows/ui/monitor-destinations.md)，了解如何監視到目標的資料流的詳細資訊。