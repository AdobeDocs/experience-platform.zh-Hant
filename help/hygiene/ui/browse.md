---
title: 瀏覽資料衛生工作單
description: 瞭解如何在Adobe Experience Platform用戶介面中查看和管理現有資料衛生工作單。
exl-id: 76d4a809-cc2c-434d-90b1-23d88f29c022
source-git-commit: a20afcd95d47e38ccdec9fba9e772032e212d7a4
workflow-type: tm+mt
source-wordcount: '862'
ht-degree: 25%

---

# 瀏覽資料衛生工作單 {#browse-work-orders}

>[!CONTEXTUALHELP]
>id="platform_hygiene_workorders"
>title="工單 ID"
>abstract="將資料檢疫要求傳送到系統時，會建立工單以執行要求的任務。換句話說，工單代表特定的資料檢疫流程，包括其目前的狀態和其他相關的詳細資訊。每個工單在建立時都會被自動指派自己的唯一 ID。"
>text="See the data hygiene UI guide to learn more."

>[!IMPORTANT]
>
>Adobe Experience Platform的資料衛生功能目前僅適用於已購買資料的組織 **Adobe醫療保健盾** 或 **Adobe隱私與安全防護**。

將資料檢疫要求傳送到系統時，會建立工單以執行要求的任務。工作單表示特定資料衛生處理，例如計畫資料集過期，其包括其當前狀態和其他相關詳細資訊。

本指南介紹如何查看和管理Adobe Experience Platform用戶介面中的現有工作單。

## 列出和篩選現有工作單

當您首次訪問 **[!UICONTROL 資料衛生]** 工作區中，將顯示現有工作單的清單及其基本詳細資訊。

![顯示 [!UICONTROL 資料衛生] 平台UI中的工作區](../images/ui/browse/work-order-list.png)

該清單一次只顯示一個類別的工作單。 選擇 **[!UICONTROL 消費者]** 查看記錄刪除任務清單，以及 **[!UICONTROL 資料集]** 查看計畫資料集過期的清單。

![顯示 [!UICONTROL 資料集] 頁籤](../images/ui/browse/dataset-tab.png)

選擇漏斗表徵圖(![漏斗表徵圖的影像](../images/ui/browse/funnel-icon.png))以查看顯示的工作單的篩選器清單。

![顯示的工作單濾鏡的影像](../images/ui/browse/filters.png)

根據您正在查看的工作單類型，可以使用不同的篩選選項。

### 記錄刪除的篩選器

以下篩選器應用於記錄刪除請求：

| 篩選 | 說明 |
| --- | --- |
| [!UICONTROL 狀態] | 根據工作單的當前狀態篩選：<ul><li>**[!UICONTROL 已完成]**:作業已完成。</li><li>**[!UICONTROL 失敗]**:作業遇到錯誤，無法完成。</li><li>**[!UICONTROL 處理]**:請求已啟動，當前正在處理。</li></ul> |
| [!UICONTROL 建立日期] | 根據下達工作單的時間進行篩選。 |
| [!UICONTROL 更新日期] | 基於上次更新工作單的時間進行篩選。 建立被計為更新。 |

### 資料集過期的篩選器

以下篩選器適用於資料集過期請求：

| 篩選 | 說明 |
| --- | --- |
| [!UICONTROL 狀態] | 根據工作單的當前狀態篩選：<ul><li>**[!UICONTROL 已完成]**:作業已完成。</li><li>**[!UICONTROL 待定]**:作業已建立，但尚未執行。 A [資料集過期請求](./dataset-expiration.md) 在計畫刪除日期之前假定此狀態。 刪除日期到達後，狀態將更新為 [!UICONTROL 正在執行] 除非事先取消。</li><li>**[!UICONTROL 正在執行]**:資料集過期請求已啟動，當前正在處理。</li><li>**[!UICONTROL 已取消]**:作為手動用戶請求的一部分，已取消作業。</li></ul> |
| [!UICONTROL 建立日期] | 根據下達工作單的時間進行篩選。 |
| [!UICONTROL 到期日] | 根據有關資料集的計畫刪除日期篩選資料集過期請求。 |
| [!UICONTROL 更新日期] | 基於上次更新工作單的時間進行篩選。 建立和到期被計為更新。 |

{style="table-layout:auto"}

## 查看工作單的詳細資訊 {#view-details}

>[!CONTEXTUALHELP]
>id="platform_hygiene_statusbyservice"
>title="服務狀態"
>abstract="資料檢疫要求會由多個 Experience Platform 服務獨立處理。本區段會針對各個服務概述要求目前的處理狀態。若要了解詳細資訊，請參閱資料檢疫 UI 指南。"

>[!CONTEXTUALHELP]
>id="platform_hygiene_numberofidentities"
>title="身分識別的數量"
>abstract="作為此工單的一部分，其記錄被要求更新或刪除的身分識別的數量。計數中包含的身分識別不一定存在於受影響的資料集中。若要了解詳細資訊，請參閱資料檢疫 UI 指南。"

>[!CONTEXTUALHELP]
>id="platform_hygiene_responsemessages"
>title="記錄刪除回應"
>abstract="當記錄刪除流程收到來自系統的回應時，這些訊息會顯示在&#x200B;**[!UICONTROL 結果]**&#x200B;區段下。如果在處理工單時出現問題，任何相關的錯誤訊息都會出現在本區段以協助您對該問題進行疑難排解。若要了解詳細資訊，請查看資料檢疫 UI 指南。"

選擇列出的工作單的ID以查看其詳細資訊。

![顯示正在選擇的工作單ID的影像](../images/ui/browse/select-work-order.png)

根據所選擇的工作單類型，提供不同的資訊和控制。 以下各節將介紹這些內容。

### 記錄刪除詳細資訊 {#record-delete}

記錄刪除請求的詳細資訊包括其當前狀態和自請求發出以來所用的時間。 每個請求還包括 **[!UICONTROL 按服務列出的狀態]** 提供有關刪除中涉及的每個下游服務的各個狀態詳細資訊的部分。 在右滑軌上，您可以使用控制項更新工作單的名稱和說明。

![顯示記錄刪除工作單的詳細資訊頁面的影像](../images/ui/browse/record-delete-details.png)

### 資料集到期詳細資訊 {#dataset-expiration}

資料集到期的詳細資訊頁面提供有關其基本屬性的資訊，包括刪除發生前剩餘天數的計畫到期日。 在右欄中，可以使用控制項編輯或取消過期。

![顯示資料集到期工作單詳細資訊頁的影像](../images/ui/browse/ttl-details.png)

## 後續步驟

本指南介紹了如何查看和管理平台UI中的現有資料衛生工作單。 有關建立您自己的工作單的資訊，請參閱以下文檔：

* [管理資料集過期](./dataset-expiration.md)
<!-- * [Manage record deletes](./record-delete.md) -->
