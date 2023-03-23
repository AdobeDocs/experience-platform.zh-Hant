---
title: 瀏覽資料衛生工作單
description: 了解如何在Adobe Experience Platform使用者介面中檢視及管理現有的資料衛生工作單。
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
>Adobe Experience Platform中的資料衛生功能目前僅適用於已購買的組織 **Adobe醫療保健盾** 或 **Adobe隱私與安全防護**.

將資料檢疫要求傳送到系統時，會建立工單以執行要求的任務。工作單代表特定資料衛生程式，例如排程的資料集有效期，包括其目前狀態和其他相關詳細資訊。

本指南說明如何在Adobe Experience Platform UI中檢視及管理現有工作單。

## 列出並篩選現有工作單

當您首次存取 **[!UICONTROL 資料衛生]** 工作區中，會顯示現有工作單的清單及其基本詳細資訊。

![顯示 [!UICONTROL 資料衛生] 平台UI中的工作區](../images/ui/browse/work-order-list.png)

清單一次只顯示一個類別的工作單。 選擇 **[!UICONTROL 消費者]** 查看記錄刪除任務清單，以及 **[!UICONTROL 資料集]** 檢視排程資料集過期時間清單。

![顯示 [!UICONTROL 資料集] 標籤](../images/ui/browse/dataset-tab.png)

選取漏斗圖示(![漏斗圖示的影像](../images/ui/browse/funnel-icon.png))，查看所顯示工作單的篩選器清單。

![顯示的工作單篩選器的影像](../images/ui/browse/filters.png)

根據您正在查看的工作單類型，可以使用不同的篩選選項。

### 記錄刪除的篩選器

下列篩選條件適用於記錄刪除請求：

| 篩選 | 說明 |
| --- | --- |
| [!UICONTROL 狀態] | 根據工作單的當前狀態進行篩選：<ul><li>**[!UICONTROL 已完成]**:作業已完成。</li><li>**[!UICONTROL 失敗]**:作業遇到錯誤，無法完成。</li><li>**[!UICONTROL 處理]**:請求已啟動，目前正在處理中。</li></ul> |
| [!UICONTROL 建立日期] | 根據下工作單的時間進行篩選。 |
| [!UICONTROL 更新日期] | 根據上次更新工作單的時間進行篩選。 將建立計為更新。 |

### 資料集有效期的篩選器

下列篩選條件適用於資料集的有效期請求：

| 篩選 | 說明 |
| --- | --- |
| [!UICONTROL 狀態] | 根據工作單的當前狀態進行篩選：<ul><li>**[!UICONTROL 已完成]**:作業已完成。</li><li>**[!UICONTROL 待定]**:作業已建立，但尚未執行。 A [資料集過期請求](./dataset-expiration.md) 會在排程的刪除日期之前假設此狀態。 刪除日期到達後，狀態會更新為 [!UICONTROL 執行中] 除非事先取消。</li><li>**[!UICONTROL 執行中]**:資料集過期請求已開始，目前正在處理中。</li><li>**[!UICONTROL 已取消]**:作業已作為手動用戶請求的一部分被取消。</li></ul> |
| [!UICONTROL 建立日期] | 根據下工作單的時間進行篩選。 |
| [!UICONTROL 到期日] | 根據相關資料集的排程刪除日期，篩選資料集到期請求。 |
| [!UICONTROL 更新日期] | 根據上次更新工作單的時間進行篩選。 建立和過期均計為更新。 |

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

![顯示所選工作單ID的影像](../images/ui/browse/select-work-order.png)

根據所選工作單的類型，提供不同的資訊和控制。 以下各節將介紹這些內容。

### 記錄刪除詳細資訊 {#record-delete}

記錄刪除請求的詳細資訊包括其當前狀態和自請求發出以來經過的時間。 每個請求也包含 **[!UICONTROL 按服務列出的狀態]** 一節，提供刪除中涉及的每個下游服務的個別狀態詳細資訊。 在右側邊欄中，您可以使用控制項來更新工作單的名稱和說明。

![顯示記錄刪除工作單詳細資訊頁面的影像](../images/ui/browse/record-delete-details.png)

### 資料集過期詳細資訊 {#dataset-expiration}

資料集過期的詳細資訊頁面會提供基本屬性的相關資訊，包括刪除前剩餘日期的排程到期日。 在右側邊欄中，您可以使用控制項來編輯或取消過期。

![顯示資料集過期工作單詳細資訊頁面的影像](../images/ui/browse/ttl-details.png)

## 後續步驟

本指南說明如何在Platform UI中檢視及管理現有的資料衛生工作單。 有關建立自己的工作單的資訊，請參閱以下文檔：

* [管理資料集過期時間](./dataset-expiration.md)
<!-- * [Manage record deletes](./record-delete.md) -->
