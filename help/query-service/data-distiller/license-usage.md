---
title: 監視批查詢許可證使用情況
description: Adobe Experience Platform UI提供控制面板，您可透過該控制面板檢視貴組織Data Distiller授權使用情形的重要資訊。
exl-id: a1e365a0-cc65-4fd6-b36f-8d79b7d9ec7c
source-git-commit: a1c5b687108a9fc8729008e2b0e39ec6b1842f54
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 0%

---

# (Alpha)監控批次查詢許可證使用情況 {#monitor-license-usage}

>[!IMPORTANT]
>
>尚無法讓所有使用者透過UI監控批次查詢授權使用情形。 此功能為Alpha版，仍在測試中。 本檔案可能會有所變更。

Adobe Experience Platform使用者介面(UI)提供控制面板，您可透過該控制面板檢視貴組織Query Service授權使用情形的重要資訊。

如需如何存取UI中的授權使用控制面板並與之互動，以及進一步了解控制面板中顯示的可用量度的詳細指示，請造訪 [授權使用控制面板指南](../../dashboards/guides/license-usage.md).

請閱讀 [控制面板概觀](../../dashboards/home.md) 以取得Experience Platform中所有控制面板功能的摘要。

## 介面工具集 {#widgets}

授權使用控制面板由Widget組成，Widget會顯示唯讀量度，提供貴組織授權使用的重要資訊。 可見的量度取決於貴組織的特定授權。

選取選項按鈕以選擇要分析的沙箱，並使用下拉式清單來選取分析的時段。 可用的選項有30天、90天、12個月期間、最後一年、完整合約期間或自訂日期。

## 計算小時數 {#compute-hours}

此 [!UICONTROL 計算小時數] 介面工具集使用折線圖來視覺化您組織的每日批次查詢處理時間。 介面工具集在介面工具集的左上方顯示三個度量，以數字表示。 分別為

- [!UICONTROL 實際]:在概述下拉式清單中選擇的時段的總計計算小時數。 此量度也會在圖形上以實線表示。
- [!UICONTROL 授權]:貴組織的授權合約允許的計算小時數總計。 此量度也會在圖形上以虛線表示。
- [!UICONTROL 使用狀況]:這是您使用量相對於授權同意的最大計算時數的百分比。

>[!IMPORTANT]
>
>此 [!UICONTROL 計算小時數] widget僅適用於擁有批次查詢資料Distiller授權的客戶。

![使用許可證儀表板，突出顯示計算時數小工具。](../images/data-distiller/compute-hours.png)
