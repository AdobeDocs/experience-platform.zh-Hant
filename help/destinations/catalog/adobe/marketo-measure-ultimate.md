---
title: Marketo Measure最終目的地
description: 了解如何將資料連線並啟動至Marketo Measure Ultimate目的地。
last-substantial-update: 2023-03-07T00:00:00Z
source-git-commit: c2c7a4cd860fed2c8124fe46fe3fd405ba49ecf4
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 1%

---


# Marketo Measure Ultimate Destination {#mmu-destination}

## 總覽 {#overview}

Marketo Measure（前身為Bizible）可讓行銷人員深入了解哪些行銷工作最能有效促進收入，並為公司創造最大的投資報酬率。 Marketo Measure是行銷歸因解決方案，可自動追蹤及報告管道效能，讓您洞察哪些管道吸引最多客戶參與，並據此最佳化行銷支出。

此目的地可讓企業對企業(B2B)資料從Adobe Experience Platform流向Marketo Measure。 此卡僅供Marketo Measure Ultimate客戶使用。

## 使用案例 {#use-cases}

為協助您更清楚了解應如何及何時使用Marketo Measure目的地，以下是Adobe Experience Platform客戶可透過此目的地解決的範例使用案例。 此整合：

* 滿足大型企業的複雜資料和效能報告要求。
* 透過多個CRM和行銷自動化系統啟用B2B歸因報表。
* 輕鬆導入第三方離線接觸點資料。

## 先決條件 {#prerequisites}

請注意Marketo Measure目的地的下列必要條件：

* Experience Platform沙箱對應應由管理員在Marketo Measure設定頁面中完成。 若沒有沙箱對應，您將無法完成連線至目的地儲存及啟用資料的工作流程。
* 只能匯出B2B XDM類別的資料集（例如，請參閱XDM商業帳戶和XDM商業機會類別）。 無法為指定的資料來源帶入多個相同B2B XDM類別的資料集。
* 每個資料集只能包含在一個通往Marketo Measure目的地的資料流中。

## 匯出類型和頻率 {#export-type-frequency}

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出類型 | **[!UICONTROL 資料集匯出]** | 您要匯出原始資料集，這些資料集未依對象興趣或資格進行分組或結構化。 深入了解 [資料集匯出](/help/destinations/destination-types.md#dataset-export-destinations). |
| 匯出頻率 | **[!UICONTROL 批次]** | 此批次目的地會每兩小時將檔案匯出至Marketo Measure平台一次。 深入了解 [排程資料集匯出](/help/destinations/ui/export-datasets.md#scheduling). |

{style="table-layout:auto"}

## 連接到目標 {#connect}

>[!IMPORTANT]
> 
>若要連線至目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。

若要連線至此目的地，請依照 [目的地設定教學課程](../../ui/connect-destination.md). 在設定目標工作流程中，填寫下方區段中列出的欄位。

### 填寫目的地詳細資訊 {#destination-details}

若要設定目的地的詳細資訊，請填寫下方的必填和選填欄位。 UI中欄位旁的星號表示該欄位為必要欄位。

* **[!UICONTROL 名稱]**:日後您將透過此名稱識別此目的地。
* **[!UICONTROL 說明]**:未來可協助您識別此目的地的說明。

![Marketo Measure目的地的連線至目的地工作流程。](/help/destinations/assets/catalog/adobe/marketo-measure-ultimate/marketo-measure-connect-to-destination.png)

### 啟用警報 {#enable-alerts}

您可以啟用警報，接收有關資料流到目標狀態的通知。 從清單中選擇要訂閱的警報，以接收有關資料流狀態的通知。 如需警報的詳細資訊，請參閱 [使用UI訂閱目的地警報](../../ui/alerts.md).

完成提供目標連接的詳細資訊後，請選擇 **[!UICONTROL 下一個]**.

## 將資料集匯出至此目的地 {#export-datasets}

>[!IMPORTANT]
> 
>若要啟用資料，您需要 **[!UICONTROL 管理目的地]**, **[!UICONTROL 啟動目的地]**, **[!UICONTROL 檢視設定檔]**，和 **[!UICONTROL 管理和啟用資料集目的地]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。

閱讀 [（測試版）匯出資料集](/help/destinations/ui/export-datasets.md) 教學課程，以取得將資料集匯出至此目的地的詳細指示。

## 驗證資料匯出 {#exported-data}

若要驗證資料集匯出是否成功，您可以檢查資料集是否已成功傳入您的 [Snowflake資料倉儲](https://experienceleague.adobe.com/docs/marketo-measure/using/marketo-measure-data-warehouse/data-warehouse-access-reader-account.html?lang=en).

## 資料使用與控管 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 處理資料時，目的地符合資料使用原則。 有關如何 [!DNL Adobe Experience Platform] 強制實施資料治理，讀取 [資料控管概觀](/help/data-governance/home.md).


