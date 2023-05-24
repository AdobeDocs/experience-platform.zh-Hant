---
title: Marketo Measure終極目的地
description: 瞭解如何連接和激活資料到Marketo Measure終極目標。
last-substantial-update: 2023-03-07T00:00:00Z
exl-id: b4220841-8908-41ff-b977-dbeebfa787c8
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 1%

---

# Marketo Measure終極目的地 {#mmu-destination}

## 總覽 {#overview}

Marketo Measure（前Bizbile）讓營銷人員瞭解哪些營銷努力在推動收入和最大化公司投資回報方面最有效。 Marketo Measure是一個營銷歸因解決方案，可自動跟蹤和報告渠道效能，讓您能夠瞭解哪些渠道是推動客戶參與最多的渠道，並使您能夠相應地優化您的營銷支出。

目的地使企業對企業(B2B)的資料從Adobe Experience Platform流到Marketo Measure。 該卡僅面向Marketo Measure旗艦店的客戶。

## 使用案例 {#use-cases}

為了幫助您更好地瞭解您應如何以及何時使用Marketo Measure目標，以下是Adobe Experience Platform客戶可通過使用此目標解決的示例使用案例。 此整合：

* 滿足大型企業的複雜資料和效能報告要求。
* 通過多個CRM和營銷自動化系統實現B2B屬性報告。
* 輕鬆引入第三方離線觸點資料。

## 先決條件 {#prerequisites}

請注意Marketo Measure目標的以下先決條件：

* Experience Platform沙盒映射應由管理員在Marketo Measure設定頁中完成。 如果沒有沙盒映射，則無法完成連接到目標保存和激活資料的工作流。
* 只能導出B2B XDM類的資料集（例如，請參見XDM Business Account和XDM Business Opportunity類）。 不能為給定資料源引入同一B2B XDM類的多個資料集。
* 每個資料集只能包含在到Marketo Measure目標的一個資料流中。

## 導出類型和頻率 {#export-type-frequency}

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 導出類型 | **[!UICONTROL 資料集導出]** | 您正在導出未按受眾興趣或資格進行分組或結構化的原始資料集。 閱讀有關 [資料集導出](/help/destinations/destination-types.md#dataset-export-destinations)。 |
| 導出頻率 | **[!UICONTROL 批]** | 此批處理目標每兩小時將檔案導出到Marketo Measure平台。 閱讀有關 [調度資料集導出](/help/destinations/ui/export-datasets.md#scheduling)。 |

{style="table-layout:auto"}

## 連接到目標 {#connect}

>[!IMPORTANT]
> 
>要連接到目標，您需要 **[!UICONTROL 管理目標]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

要連接到此目標，請按照 [目標配置教程](../../ui/connect-destination.md)。 在配置目標工作流中，填寫下節中列出的欄位。

### 填寫目標詳細資訊 {#destination-details}

要配置目標的詳細資訊，請填寫以下必需欄位和可選欄位。 UI中某個欄位旁邊的星號表示該欄位是必需的。

* **[!UICONTROL 名稱]**:您將來識別此目標的名稱。
* **[!UICONTROL 說明]**:將幫助您在將來確定此目標的說明。

![連接到Marketo Measure目標的目標工作流。](/help/destinations/assets/catalog/adobe/marketo-measure-ultimate/marketo-measure-connect-to-destination.png)

### 啟用警報 {#enable-alerts}

您可以啟用警報來接收有關目標資料流狀態的通知。 從清單中選擇要訂閱的警報以接收有關資料流狀態的通知。 有關警報的詳細資訊，請參閱上的指南 [使用UI訂閱目標警報](../../ui/alerts.md)。

完成提供目標連接的詳細資訊後，選擇 **[!UICONTROL 下一個]**。

## 將資料集導出到此目標 {#export-datasets}

>[!IMPORTANT]
> 
>要激活資料，您需要 **[!UICONTROL 管理目標]**。 **[!UICONTROL 激活目標]**。 **[!UICONTROL 查看配置檔案]**, **[!UICONTROL 管理和激活資料集目標]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

閱讀 [(Beta)導出資料集](/help/destinations/ui/export-datasets.md) 有關將資料集導出到此目標的詳細說明的教程。

## 驗證資料導出 {#exported-data}

要驗證成功的資料集導出，您可以檢查您的資料集是否已成功將其導出到 [Snowflake資料倉庫](https://experienceleague.adobe.com/docs/marketo-measure/using/marketo-measure-data-warehouse/data-warehouse-access-reader-account.html?lang=en)。

## 資料使用和治理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目標在處理資料時符合資料使用策略。 有關如何 [!DNL Adobe Experience Platform] 強制實施資料治理，讀取 [資料治理概述](/help/data-governance/home.md)。
