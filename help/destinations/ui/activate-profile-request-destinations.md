---
keywords: 激活配置檔案請求目標；激活資料；配置檔案請求目標
title: 激活受眾資料以配置檔案請求目標(Beta)
type: Tutorial
seo-title: Activate audience data to profile request destinations
description: 瞭解如何通過將段映射到配置檔案請求目標來激活您在Adobe Experience Platform擁有的受眾資料。
seo-description: Learn how to activate the audience data you have in Adobe Experience Platform by mapping segments to profile request destinations.
exl-id: cd7132eb-4047-4faa-a224-47366846cb56
source-git-commit: dd9493077706b102467493e90b363ac202550eee
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 0%

---

# 將受眾資料激活到配置檔案請求目標

## 總覽 {#overview}

本文介紹在Adobe Experience Platform配置檔案請求目標中激活受眾資料所需的工作流。 配置檔案請求目標的示例包括 [Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) 和 [自定義個性化](../../destinations/catalog/personalization/custom-personalization.md) 連接。

## 先決條件 {#prerequisites}

要將資料激活到目標，必須已成功 [連接到目標](./connect-destination.md)。 如果尚未執行此操作，請轉至 [目標目錄](../catalog/overview.md)，瀏覽支援的目標，並配置要使用的目標。

### 段合併策略 {#merge-policy}

當前，配置檔案請求目標僅支援激活使用 [預設合併策略](../../segmentation/ui/segment-builder.md#merge-policies)。

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

## 驗證段激活 {#verify}

檢查 [目標監控文檔](../../dataflows/ui/monitor-destinations.md) 有關如何監視資料流到目標的詳細資訊。
