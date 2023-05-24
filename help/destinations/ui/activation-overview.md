---
keywords: 激活目標；激活資料
title: Activation 總覽
type: Tutorial
description: 瞭解如何將您在Adobe Experience Platform擁有的受眾資料激活到各種類型的目標。
exl-id: 987af401-2d93-45b4-a8f9-191e6058e4da
source-git-commit: a6fe0f5a0c4f87ac265bf13cb8bba98252f147e0
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 1%

---

# Activation 總覽

>[!IMPORTANT]
> 
>要激活資料，您需要 **[!UICONTROL 管理目標]**。 **[!UICONTROL 激活目標]**。 **[!UICONTROL 查看配置檔案]**, **[!UICONTROL 查看段]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

Adobe Experience Platform支援各種目的地。 受眾激活工作流根據其支援的受眾資料類型和資料導出的頻率在目標之間有所不同。

## 激活方法 {#activation-methods}

在你之後 [配置目標](connect-destination.md)，可以通過多種方式激活受眾段：

### 從目標目錄激活受眾

有關從目標目錄激活受眾到目標的詳細資訊，請參閱以下指南：

* [將受眾資料激活到流段導出目標](activate-segment-streaming-destinations.md)
* [激活受眾資料以流式處理配置檔案導出目標](activate-streaming-profile-destinations.md)
* [將受眾資料激活到批配置檔案導出目標](activate-batch-profile-destinations.md)

### 從 [!UICONTROL 瀏覽] 頁

按照以下步驟將資料從 **[!UICONTROL 瀏覽]** 的子菜單。

1. 轉到 **[!UICONTROL 連接>目標]**，然後選擇 **[!UICONTROL 瀏覽]** 頁籤。

   ![「瀏覽」頁籤](../assets/ui/activation-overview/browse-tab.png)

1. 查找要用於激活段的目標連接，選擇 [!UICONTROL 名稱] 列，然後選擇 **[!UICONTROL 激活段]**。

   ![「激活段」按鈕](../assets/ui/activation-overview/activate-segments.png)

1. 根據所選目標，請遵循以下文章中描述的步驟，從 **[!UICONTROL 選擇段]** 步驟，完成激活工作流：

   * [將受眾資料激活到流段導出目標](activate-segment-streaming-destinations.md)
   * [激活受眾資料以流式處理配置檔案導出目標](activate-streaming-profile-destinations.md)
   * [將受眾資料激活到批配置檔案導出目標](activate-batch-profile-destinations.md)

### 從段詳細資訊頁面激活受眾 {#activate-segment-details}

您可以從段詳細資訊頁面將段激活到目標。 請參閱 [段詳細資訊](../../segmentation/ui/overview.md#segment-details) 的子菜單。

根據所選目標，按照以下文章中描述的步驟完成激活工作流：

* [將受眾資料激活到流段導出目標](activate-segment-streaming-destinations.md)
* [激活受眾資料以流式處理配置檔案導出目標](activate-streaming-profile-destinations.md)
* [將受眾資料激活到批配置檔案導出目標](activate-batch-profile-destinations.md)
