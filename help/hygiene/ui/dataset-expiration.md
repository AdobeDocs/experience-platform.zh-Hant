---
title: 管理資料集有效期
description: 了解如何在Adobe Experience Platform UI中排程資料集的有效期。
exl-id: 97db55e3-b5d6-40fd-94f0-2463fe041671
source-git-commit: 5a12c75a54f420b2ca831dbfe05105dfd856dc4d
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 0%

---

# 管理資料集過期時間

>[!IMPORTANT]
>
>Adobe Experience Platform中的資料衛生功能目前僅適用於已購買Healthcare Shield的組織。

此 [[!UICONTROL 資料衛生] 工作區](./overview.md) 在Adobe Experience Platform UI中，可讓您排程資料集的有效期。 當資料集到期日時，資料湖、身分服務和即時客戶設定檔會開始個別的程式，從各自的服務中移除資料集的內容。 從這三項服務中刪除資料後，過期時間就會標示為完成。

>[!WARNING]
>
>如果資料集設為過期，您必須手動變更可能會將資料內嵌至該資料集的任何資料流，以免對下游工作流程造成負面影響。

本檔案說明如何在Platform UI中排程和管理資料集有效期。

## 排程資料集的有效期

若要建立新請求，請選取 **[!UICONTROL 建立請求]** 從工作區的主要頁面。

![顯示 [!UICONTROL 建立請求] 按鈕](../images/ui/ttl/create-request-button.png)

<!-- The request creation dialog appears. Under the **[!UICONTROL Action]** section, select **[!UICONTROL Dataset]** to update the available controls for dataset expiration scheduling-->

### 選取日期和資料集

請求建立對話方塊隨即顯示。 在 **[!UICONTROL 動作]** 區段，選取您要刪除資料集的日期。 您可以手動輸入日期（格式） `mm/dd/yyyy`)或選取日曆圖示(![日曆圖示的影像](../images/ui/ttl/calendar-icon.png))，從對話方塊選取日期。

![顯示資料集所設定到期日的影像](../images/ui/ttl/select-date.png)

下一個，下 **[!UICONTROL 資料集詳細資料]**，請選取資料庫圖示(![資料庫表徵圖的影像](../images/ui/ttl/database-icon.png))開啟資料集選取對話方塊。 從清單中選擇要套用到期日的資料集，然後選取 **[!UICONTROL 完成]**.

![顯示所選資料集的影像](../images/ui/ttl/select-dataset.png)

>[!NOTE]
>
>只會顯示屬於目前沙箱的資料集。

### 提交請求

選取資料集和到期日後，請選取 **[!UICONTROL 提交]**.

![顯示 [!UICONTROL 提交] 按鈕](../images/ui/ttl/submit.png)

系統會要求您確認資料集的刪除日期。 選擇 **[!UICONTROL 提交]** 繼續。

提交請求後，會建立工作單，並顯示在 [!UICONTROL 資料衛生] 工作區。 在此處，您可以在工作單處理請求時監控其狀態。

## 編輯或取消資料集的過期時間

若要編輯或取消資料集的過期時間，請選取 **[!UICONTROL 資料集]** 在工作區的主要頁面上，並從清單中選取資料集過期時間。

在資料集過期的詳細資訊頁面上，右側邊欄會顯示編輯或取消排程刪除的控制項。

## 後續步驟

本檔案說明如何在Experience PlatformUI中排程資料集到期日。 若要了解如何使用資料衛生API排程資料集到期日，請參閱 [資料集過期端點指南](../api/dataset-expiration.md).
