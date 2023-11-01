---
title: Marketo Measure Ultimate目的地
description: 瞭解如何將資料連線並啟用至Marketo Measure Ultimate目的地。
last-substantial-update: 2023-03-07T00:00:00Z
exl-id: b4220841-8908-41ff-b977-dbeebfa787c8
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '652'
ht-degree: 1%

---

# Marketo Measure Ultimate目的地 {#mmu-destination}

## 概觀 {#overview}

Marketo Measure （前身為Bizible）可協助行銷人員深入瞭解哪些行銷手法最能有效提升公司營收，實現投資報酬最大化。 Marketo Measure是一種行銷歸因解決方案，可自動追蹤和報告管道效能，讓您可見哪些管道可帶來最多客戶參與，並據此將行銷支出最佳化。

目的地可讓企業對企業(B2B)資料從Adobe Experience Platform傳輸至Marketo Measure。 此卡僅限Marketo Measure Ultimate客戶使用。

## 使用案例 {#use-cases}

為協助您更清楚瞭解如何使用Marketo Measure目的地，以下是Adobe Experience Platform客戶可使用此目的地解決的範例使用案例。 此整合：

* 滿足大型企業複雜的資料與效能報告需求。
* 在多個CRM和行銷自動化系統中啟用B2B歸因報告。
* 讓您輕鬆匯入第三方離線接觸點資料。

## 先決條件 {#prerequisites}

請注意Marketo Measure目的地的下列必要條件：

* 管理員應在Marketo Measure設定頁面中完成Experience Platform沙箱對應。 如果沒有沙箱對應，您便無法完成工作流程以連線至目的地並儲存及啟用資料。
* 只能匯出B2B XDM類別的資料集（例如，請參閱XDM商業帳戶和XDM商業機會類別）。 您無法為特定資料來源匯入相同B2B XDM類別的多個資料集。
* 每個資料集只能包含在傳至Marketo Measure目的地的一個資料流中。

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出型別 | **[!UICONTROL 資料集匯出]** | 您正在匯出原始資料集，這些資料集未依對象興趣或資格進行分組或建構。 深入瞭解 [資料集匯出](/help/destinations/destination-types.md#dataset-export-destinations). |
| 匯出頻率 | **[!UICONTROL 批次]** | 此批次目的地每兩小時會將檔案匯出至Marketo Measure平台。 深入瞭解 [排程資料集匯出](/help/destinations/ui/export-datasets.md#scheduling). |

{style="table-layout:auto"}

## 連線到目的地 {#connect}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

若要連線至此目的地，請遵循以下說明的步驟： [目的地設定教學課程](../../ui/connect-destination.md). 在設定目標工作流程中，填寫以下區段列出的欄位。

### 填寫目的地詳細資料 {#destination-details}

若要設定目的地的詳細資訊，請填寫下方的必填和選用欄位。 UI中欄位旁的星號表示該欄位為必填欄位。

* **[!UICONTROL 名稱]**：您日後可辨識此目的地的名稱。
* **[!UICONTROL 說明]**：可協助您日後識別此目的地的說明。

![Marketo Measure目的地的連線至目的地工作流程。](/help/destinations/assets/catalog/adobe/marketo-measure-ultimate/marketo-measure-connect-to-destination.png)

### 啟用警示 {#enable-alerts}

您可以啟用警報以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱以下指南： [使用UI訂閱目的地警報](../../ui/alerts.md).

當您完成提供目的地連線的詳細資訊時，請選取「 」 **[!UICONTROL 下一個]**.

## 將資料集匯出至此目的地 {#export-datasets}

>[!IMPORTANT]
> 
>若要啟用資料，您需要 **[!UICONTROL 管理目的地]**， **[!UICONTROL 啟用目的地]**， **[!UICONTROL 檢視設定檔]**、和 **[!UICONTROL 管理和啟用資料集目的地]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

閱讀 [(Beta)匯出資料集](/help/destinations/ui/export-datasets.md) 教學課程，以取得將資料集匯出至此目的地的詳細指示。

## 驗證資料匯出 {#exported-data}

若要驗證資料集匯出是否成功，您可以檢查資料集是否已成功匯出至 [Snowflake資料倉儲](https://experienceleague.adobe.com/docs/marketo-measure/using/marketo-measure-data-warehouse/data-warehouse-access-reader-account.html).

## 資料使用與控管 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 處理您的資料時，目的地符合資料使用原則。 如需如何操作的詳細資訊 [!DNL Adobe Experience Platform] 強制執行資料控管，讀取 [資料控管概觀](/help/data-governance/home.md).
