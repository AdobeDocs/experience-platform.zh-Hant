---
keywords: 連接目標；目標連接；連接目標
title: 新建目標連接
type: Tutorial
description: 本教程列出了連接到Adobe Experience Platform目標的步驟
exl-id: 56d7799a-d1da-4727-ae79-fb2c775fe5a5
source-git-commit: 729c0724c7af88bb69c9d68a45d58c3575c90828
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 0%

---

# 新建目標連接

>[!IMPORTANT]
> 
>要連接到目標，您需要 **[!UICONTROL 管理目標]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

## 總覽 {#overview}

在將受眾資料發送到目標之前，必須設定到目標平台的連接。 本文介紹如何使用Adobe Experience Platform用戶介面設定新目標。

## 新建目標連接 {#setup}

1. 轉到 **[!UICONTROL 連接]** > **[!UICONTROL 目標]**，然後選擇 **[!UICONTROL 目錄]** 頁籤。

   ![目錄頁](../assets/ui/connect-destinations/catalog.png)

1. 根據您是否與目標有現有連接，您可以看到 **[!UICONTROL 設定]** 或 **[!UICONTROL 激活段]** 按鈕。 有關兩者之間差異的詳細資訊 **[!UICONTROL 激活段]** 和 **[!UICONTROL 設定]**，請參閱 [目錄](../ui/destinations-workspace.md#catalog) 目標工作區文檔的「 」部分。

   選擇 **[!UICONTROL 設定]** 或 **[!UICONTROL 激活段]**，具體取決於您可以使用的按鈕。

   ![目錄頁](../assets/ui/connect-destinations/set-up.png)

   ![激活段](../assets/ui/connect-destinations/activate-segments.png)

1. 如果已選擇 **[!UICONTROL 設定]**，跳至下一步。

   如果已選擇 **[!UICONTROL 激活段]**，您現在可以看到現有目標連接的清單。

   選擇 **[!UICONTROL 配置新目標]**。

   ![配置新目標](../assets/ui/connect-destinations/configure-new-destination.png)

1. 輸入目標平台連接詳細資訊，然後選擇 **[!UICONTROL 連接到目標]**。

   >[!NOTE]
   >
   >下面的影像僅用於圖示目的。 目標連接詳細資訊因目標而異。 有關目標的連接詳細資訊，請參閱 **連接參數** 的 [目標目錄](../catalog/overview.md) 頁面(例如， [Google客戶匹配](..//catalog/advertising/google-customer-match.md#parameters))。

   ![連接到目標](../assets/ui/connect-destinations/connect-destination.png)

1. （可選）選擇要訂閱的目標資料流警報。 在建立資料流以接收有關流運行狀態、成功或失敗的警報消息時，可以訂閱警報。 請參閱 [訂閱上下文中的目標警報](alerts.md) 有關目標資料流警報的詳細資訊。

   ![顯示上下文目標警報訂閱選項的UI影像](../assets/ui/connect-destinations/subscribe-to-alerts.png)

1. 選取&#x200B;**[!UICONTROL 「下一步」]**。

   ![連接到目標](../assets/ui/connect-destinations/next.png)

1. 選擇適用於要導出到目標的資料的市場營銷操作。 市場營銷操作指明將資料導出到目標的目的。 您可以從Adobe定義的市場營銷活動中進行選擇，也可以建立自己的市場營銷活動。 有關市場營銷活動的詳細資訊，請參閱 [資料使用策略概述](../../data-governance/policies/overview.md) 的子菜單。

   ![選擇市場營銷活動](../assets/ui/connect-destinations/governance.png)

1. 選擇 **[!UICONTROL 保存並退出]** 保存目標配置，或選擇 **[!UICONTROL 下一個]** 繼續訪問受眾資料 [激活流](activation-overview.md)。