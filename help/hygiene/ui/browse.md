---
title: 瀏覽資料衛生工作單
description: 了解如何在Adobe Experience Platform使用者介面中檢視及管理現有的資料衛生工作單。
exl-id: 76d4a809-cc2c-434d-90b1-23d88f29c022
source-git-commit: 83149c4e6e8ea483133da4766c37886b8ebd7316
workflow-type: tm+mt
source-wordcount: '860'
ht-degree: 1%

---

# 瀏覽資料衛生工作單 {#browse-work-orders}

>[!CONTEXTUALHELP]
>id="platform_hygiene_workorders"
>title="工作單ID"
>abstract="當資料衛生請求被發送到系統時，建立工作單以執行所請求的任務。 換言之，工作單代表特定的資料衛生過程，包括其當前狀態和其他相關細節。 每個工作單在建立時都會自動分配其唯一ID。"
>text="See the data hygiene UI guide to learn more."

>[!IMPORTANT]
>
>Adobe Experience Platform中的資料衛生功能目前僅適用於已購買Analytics Healthcare Shield的組織。

當資料衛生請求被發送到系統時，建立工作單以執行所請求的任務。 工作單代表特定資料衛生程式，例如排程的資料集有效期，包括其目前狀態和其他相關詳細資訊。

本指南說明如何在Adobe Experience Platform UI中檢視及管理現有工作單。

## 列出並篩選現有工作單

當您首次存取 **[!UICONTROL 資料衛生]** 工作區中，會顯示現有工作單的清單及其基本詳細資訊。

![顯示 [!UICONTROL 資料衛生] 平台UI中的工作區](../images/ui/browse/work-order-list.png)

清單一次只顯示一個類別的工作單。 選擇 **[!UICONTROL 消費者]** 要查看消費者刪除任務的清單，以及 **[!UICONTROL 資料集]** 檢視排程資料集過期時間清單。

![顯示 [!UICONTROL 資料集] 標籤](../images/ui/browse/dataset-tab.png)

選取漏斗圖示(![漏斗圖示的影像](../images/ui/browse/funnel-icon.png))，查看所顯示工作單的篩選器清單。

![顯示的工作單篩選器的影像](../images/ui/browse/filters.png)

根據您正在查看的工作單類型，可以使用不同的篩選選項。

### 消費者刪除的篩選

下列篩選條件適用於消費者刪除請求：

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

{style=&quot;table-layout:auto&quot;}

## 查看工作單的詳細資訊 {#view-details}

>[!CONTEXTUALHELP]
>id="platform_hygiene_statusbyservice"
>title="按服務列出的狀態"
>abstract="多個Experience Platform服務會獨立處理資料衛生請求。 本節概述每個服務的要求目前處理狀態。 要了解更多資訊，請參閱資料衛生UI指南。"

>[!CONTEXTUALHELP]
>id="platform_hygiene_numberofidentities"
>title="身分數"
>abstract="請求在此工作單中刪除的身份數。 計數中包含的身分不一定存在於受影響的資料集中。 要了解更多資訊，請參閱資料衛生UI指南。"

>[!CONTEXTUALHELP]
>id="platform_hygiene_responsemessages"
>title="消費者刪除回應"
>abstract="消費者刪除程式從系統收到回應時，這些訊息會顯示在 **[!UICONTROL 結果]** 區段。 如果在處理工作單時發生問題，本區段會顯示任何相關錯誤訊息，以協助您疑難排解問題。 若要進一步了解，請參閱資料衛生UI指南。"

選擇列出的工作單的ID以查看其詳細資訊。

![顯示所選工作單ID的影像](../images/ui/browse/select-work-order.png)

根據所選工作單的類型，提供不同的資訊和控制。 以下各節將介紹這些內容。

### 消費者刪除詳細資訊 {#consumer-delete}

消費者刪除請求的詳細資訊包括其目前狀態和自請求提出以來經過的時間。 每個請求也包含 **[!UICONTROL 按服務列出的狀態]** 一節，提供刪除中涉及的每個下游服務的個別狀態詳細資訊。 在右側邊欄中，您可以使用控制項來更新工作單的名稱和說明。

![顯示消費者刪除工作單詳細資訊頁面的影像](../images/ui/browse/consumer-delete-details.png)

### 資料集過期詳細資訊 {#dataset-expiration}

資料集過期的詳細資訊頁面會提供基本屬性的相關資訊，包括刪除前剩餘日期的排程到期日。 在右側邊欄中，您可以使用控制項來編輯或取消過期。

![顯示資料集過期工作單詳細資訊頁面的影像](../images/ui/browse/ttl-details.png)

## 後續步驟

本指南說明如何在Platform UI中檢視及管理現有的資料衛生工作單。 有關建立自己的工作單的資訊，請參閱以下文檔：

* [管理資料集過期時間](./dataset-expiration.md)
* [管理消費者刪除](./delete-consumer.md)
