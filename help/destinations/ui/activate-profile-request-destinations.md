---
keywords: 激活配置檔案請求目標；激活資料；配置檔案請求目標
title: 將受眾資料激活到配置檔案請求目標
type: Tutorial
description: 瞭解如何通過將段映射到配置檔案請求目標來激活您在Adobe Experience Platform擁有的受眾資料。
exl-id: cd7132eb-4047-4faa-a224-47366846cb56
source-git-commit: a6fe0f5a0c4f87ac265bf13cb8bba98252f147e0
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 0%

---

# 將受眾資料激活到配置檔案請求目標

>[!IMPORTANT]
> 
>要激活資料，您需要 **[!UICONTROL 管理目標]**。 **[!UICONTROL 激活目標]**。 **[!UICONTROL 查看配置檔案]**, **[!UICONTROL 查看段]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

## 總覽 {#overview}

本文介紹在Adobe Experience Platform配置檔案請求目標中激活受眾資料所需的工作流。 配置檔案請求目標的示例包括 [Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) 和 [自定義個性化](../../destinations/catalog/personalization/custom-personalization.md) 連接。

## 先決條件 {#prerequisites}

要將資料激活到目標，必須已成功 [連接到目標](./connect-destination.md)。 如果尚未執行此操作，請轉至 [目標目錄](../catalog/overview.md)，瀏覽支援的目標，並配置要使用的目標。

### 段合併策略 {#merge-policy}

當前，配置檔案請求目標僅支援激活使用 [活動邊緣合併策略](../../segmentation/ui/segment-builder.md#merge-policies) 設定為預設值。

## 選擇目標 {#select-destination}

1. 轉到 **[!UICONTROL 連接>目標]**，然後選擇 **[!UICONTROL 目錄]** 頁籤。

   ![目標目錄頁籤](../assets/ui/activate-segment-streaming-destinations/catalog-tab.png)

1. 選擇 **[!UICONTROL 激活段]** 在與要激活段的目標相對應的卡上，如下圖所示。

   ![激活按鈕](../assets/ui/activate-profile-request-destinations/activate-segments-button.png)

1. 選擇要用於激活段的目標連接，然後選擇 **[!UICONTROL 下一個]**。

   ![選擇目標](../assets/ui/activate-profile-request-destinations/select-destination.png)

1. 移至下一節 [選擇段](#select-segments)。

## 選擇段 {#select-segments}

使用段名稱左側的複選框選擇要激活到目標的段，然後選擇 **[!UICONTROL 下一個]**。

![選擇段](../assets/ui/activate-profile-request-destinations/select-segments.png)

## 計畫段導出 {#scheduling}

預設情況下， [!UICONTROL 段計畫] 頁只顯示在當前激活流中選擇的新選定段。

![新段](../assets/ui/activate-profile-request-destinations/new-segments.png)

要查看激活到目標的所有段，請使用篩選選項並禁用 **[!UICONTROL 僅顯示新段]** 的子菜單。

![所有段](../assets/ui/activate-profile-request-destinations/all-segments.png)

在 **[!UICONTROL 段計畫]** 頁，選擇每個段，然後使用 **[!UICONTROL 開始日期]** 和 **[!UICONTROL 結束日期]** 選擇器，用於配置將資料發送到目標的時間間隔。

![段計畫](../assets/ui/activate-profile-request-destinations/segment-schedule.png)

選擇 **[!UICONTROL 下一個]** 轉到 [!UICONTROL 審閱] 的子菜單。

## 審閱 {#review}

在 **[!UICONTROL 審閱]** 的子菜單。 選擇 **[!UICONTROL 取消]** 分解流， **[!UICONTROL 後退]** 修改設定，或 **[!UICONTROL 完成]** 確認選擇並開始向目標發送資料。

>[!IMPORTANT]
>
>在此步驟中，Adobe Experience Platform檢查資料使用策略違規。 下面顯示的示例違反了策略。 在解決違規之前，無法完成段激活工作流。 有關如何解決策略違規的資訊，請參見 [策略執行](../../rtcdp/privacy/data-governance-overview.md#enforcement) 資料治理文檔部分。

![資料策略違規](../assets/common/data-policy-violation.png)

如果未檢測到任何策略違規，請選擇 **[!UICONTROL 完成]** 確認選擇並開始向目標發送資料。

![審閱](../assets/ui/activate-profile-request-destinations/review.png)

<!--

Commenting out this part since destination monitoring is not available currently for the Adobe Target and Custom Personalization destinations.

## Verify segment activation {#verify}

Check the [destination monitoring documentation](../../dataflows/ui/monitor-destinations.md) for detailed information on how to monitor the flow of data to your destinations.

-->