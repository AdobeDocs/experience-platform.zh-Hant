---
title: 瀏覽資料衛生工作單
description: 瞭解如何在Adobe Experience Platform用戶介面中查看和管理現有資料衛生工作單。
exl-id: 76d4a809-cc2c-434d-90b1-23d88f29c022
source-git-commit: 49ba5263c6dc8eccac2ffe339476cf316c68e486
workflow-type: tm+mt
source-wordcount: '481'
ht-degree: 2%

---

# 瀏覽資料衛生工作單 {#browse-work-orders}

>[!CONTEXTUALHELP]
>id="platform_hygiene_workorders"
>title="工作單ID"
>abstract="當向系統發送資料衛生請求時，建立工作單以執行所請求的任務。 換句話說，工作單代表特定的資料衛生過程，包括其當前狀態和其他相關細節。 每個工作單在建立時自動分配其唯一的ID。"
>text="See the data hygiene UI guide to learn more."

>[!IMPORTANT]
>
>Adobe Experience Platform的資料衛生功能目前僅適用於已購買Healthcare Shield的組織。

當向系統發送資料衛生請求時，建立工作單以執行所請求的任務。 工作單表示特定資料衛生處理，例如計畫資料集過期，其包括其當前狀態和其他相關詳細資訊。

本指南介紹如何查看和管理Adobe Experience Platform用戶介面中的現有工作單。

## 列出和篩選現有工作單

當您首次訪問 **[!UICONTROL 資料衛生]** 工作區中，將顯示現有工作單的清單及其基本詳細資訊。

![顯示 [!UICONTROL 資料衛生] 平台UI中的工作區](../images/ui/browse/work-order-list.png)

<!-- The list only shows work orders for one category at a time. Select **[!UICONTROL Consumer]** to view a list of consumer deletion tasks, and **[!UICONTROL Dataset]** to view a list of scheduled dataset expirations.

![Image showing the [!UICONTROL Dataset] tab](../images/ui/browse/dataset-tab.png) -->

選擇漏斗表徵圖(![漏斗表徵圖的影像](../images/ui/browse/funnel-icon.png))以查看顯示的工作單的篩選器清單。

![顯示的工作單濾鏡的影像](../images/ui/browse/filters.png)

| 篩選 | 說明 |
| --- | --- |
| [!UICONTROL 狀態] | 根據工作單的當前狀態篩選：<ul><li>**[!UICONTROL 已完成]**:作業已完成。</li><li>**[!UICONTROL 待定]**:作業已建立，但尚未執行。 A [資料集過期請求](./dataset-expiration.md) 在計畫刪除日期之前假定此狀態。 刪除日期到達後，狀態將更新為 [!UICONTROL 正在執行] 除非事先取消。</li><li>**[!UICONTROL 正在執行]**:資料集過期請求已啟動，當前正在處理。</li><li>**[!UICONTROL 已取消]**:作為手動用戶請求的一部分，已取消作業。</li></ul> |
| [!UICONTROL 建立日期] | 根據下達工作單的時間進行篩選。 |
| [!UICONTROL 到期日] | 根據有關資料集的計畫刪除日期篩選資料集過期請求。 |
| [!UICONTROL 更新日期] | 根據上次更新工作單的時間篩選資料集過期請求。 建立和到期被計為更新。 |

{style=&quot;table-layout:auto&quot;}

## 查看工作單的詳細資訊

選擇列出的工作單的ID以查看其詳細資訊。

![顯示正在選擇的工作單ID的影像](../images/ui/browse/select-work-order.png)

<!-- Depending on the type of work order selected, different information and controls are provided. These are covered in the sections below.

### Consumer delete details

>[!CONTEXTUALHELP]
>id="platform_hygiene_responsemessages"
>title="Consumer delete response"
>abstract="When a consumer deletion process receives a response from the system, these messages are displayed under the **[!UICONTROL Result]** section. If a problem occurs while a work order is processing, any relevant error messages will appear in this section to help you troubleshoot the issue. To learn more, see the data hygiene UI guide."


The details of a consumer delete request are read-only, displaying its basic attributes such as its current status and the time elapsed since the request was made.

![Image showing the details page for a consumer delete work order](../images/ui/browse/consumer-delete-details.png)

### Dataset expiration details -->

資料集到期的詳細資訊頁面提供有關其基本屬性的資訊，包括刪除發生前剩餘天數的計畫到期日。 在右欄中，可以使用控制項編輯或取消過期。

![顯示資料集到期工作單詳細資訊頁的影像](../images/ui/browse/ttl-details.png)

## 後續步驟

本指南介紹了如何查看和管理平台UI中的現有資料衛生工作單。 有關建立您自己的工作單的資訊，請參閱上的指南 [調度資料集過期](./dataset-expiration.md)。
