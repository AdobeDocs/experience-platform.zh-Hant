---
title: 管理資料集TTL
description: 瞭解如何為Adobe Experience PlatformUI中的資料集安排生存時間(TTL)。
exl-id: 97db55e3-b5d6-40fd-94f0-2463fe041671
source-git-commit: 7f1e4bdf54314cab1f69619bcbb34216da94b17e
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---

# 管理資料集TTL

>[!IMPORTANT]
>
>Adobe Experience Platform的資料衛生功能目前僅適用於已購買Healthcare Shield的組織。

的 [[!UICONTROL 資料衛生] 工作區](./overview.md) 在Adobe Experience PlatformUI中，可以為資料集安排生存時間(TTL)。

本文檔介紹如何在平台UI中安排和管理資料集TTL。

## 計畫TTL

要建立新請求，請選擇 **[!UICONTROL 建立請求]** 的下界。

![顯示 [!UICONTROL 建立請求] 按鈕](../images/ui/ttl/create-request-button.png)

<!-- The request creation dialog appears. Under the **[!UICONTROL Action]** section, select **[!UICONTROL Dataset]** to update the available controls for TTL scheduling-->

### 選擇日期和資料集

此時將出現請求建立對話框。 在 **[!UICONTROL 操作]** 部分，選擇希望資料集刪除的日期。 您可以手動輸入日期(格式為 `mm/dd/yyyy`)或選擇日曆表徵圖(![日曆表徵圖的影像](../images/ui/ttl/calendar-icon.png))以從對話框中選擇日期。

![顯示為TTL設定的到期日期的影像](../images/ui/ttl/select-date.png)

下一個，下 **[!UICONTROL 資料集詳細資訊]**，選擇資料庫表徵圖(![資料庫表徵圖的影像](../images/ui/ttl/database-icon.png))開啟資料集選擇對話框。 從清單中選擇要應用TTL的資料集，然後選擇 **[!UICONTROL 完成]**。

![顯示正在選擇的資料集的影像](../images/ui/ttl/select-dataset.png)

>[!NOTE]
>
>僅顯示屬於當前沙箱的資料集。

### 提交請求

選擇資料集和TTL日期後，選擇 **[!UICONTROL 提交]**。

![顯示 [!UICONTROL 提交] 按鈕](../images/ui/ttl/submit.png)

系統會要求您確認資料集的刪除日期。 選擇 **[!UICONTROL 提交]** 繼續。

提交請求後，將建立工作單，並在 [!UICONTROL 資料衛生] 工作區。 在此處，您可以監視工作單處理請求時的狀態。

## 編輯或取消TTL

要編輯或取消TTL，請選擇 **[!UICONTROL 資料集]** 在工作區的首頁上，然後從清單中選擇TTL。

在TTL的詳細資訊頁面上，右欄顯示了編輯或取消計畫刪除的控制項。

## 後續步驟

本文檔介紹了如何在Experience PlatformUI中調度資料集TTL。 要瞭解如何使用資料衛生API調度資料集TTL，請參閱 [資料集TTL終結點指南](../api/ttl.md)。
