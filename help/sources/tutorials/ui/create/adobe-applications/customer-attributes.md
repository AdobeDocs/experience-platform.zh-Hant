---
keywords: Experience Platform；首頁；熱門主題；客戶屬性
solution: Experience Platform
title: 在UI中建立客戶屬性來源連線
type: Tutorial
description: 了解如何在UI中建立來源連線，將客戶屬性設定檔資料匯入Adobe Experience Platform。
exl-id: 66bdab8f-c00e-4ebe-8b8e-f9e12cf86bbe
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 4%

---

# 在UI中建立客戶屬性來源連線

本教學課程提供在UI中建立來源連線的步驟，以將客戶屬性設定檔資料匯入Adobe Experience Platform。 如需客戶屬性的詳細資訊，請參閱 [客戶屬性概觀](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/attributes.html?lang=zh-Hant??lang=zh-Hant).

>[!IMPORTANT]
>
>客戶屬性源當前不支援啟用或禁用資料流。

## 建立源連接

>[!NOTE]
>
>如果您已為客戶屬性配置檔案資料建立源連接，則禁用與源連接的選項。

在平台UI中，選取 **[!UICONTROL 來源]** 從左側導覽器存取 [!UICONTROL 來源] 工作區。 此 [!UICONTROL 目錄] 螢幕會顯示您可建立連線的各種來源。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋列找到您要使用的特定來源。

在 [!UICONTROL Adobe應用程式] 類別，選擇 **[!UICONTROL 客戶屬性]** 然後選取 **[!UICONTROL 新增資料]**.

![目錄](../../../../images/tutorials/create/customer-attributes/catalog.png)

### 選擇客戶屬性資料源

此 [!UICONTROL 新增資料] 畫面會列出客戶屬性的所有可用資料來源。 每個客戶屬性來源連線只能選取一個資料集。

>[!NOTE]
>
>欄位群組、結構和資料集會隨流程布建而立即建立。 它們會維持原狀，而您必須視需要手動刪除它們。

客戶屬性來源不支援結構演變。 如果客戶屬性資料來源的結構輸入變更，則會與Platform不相容。 作為解決方法，您可以刪除現有客戶屬性資料流及其關聯的資料集、架構和欄位組，然後使用更新的架構和資料源建立新的資料流。

>[!IMPORTANT]
>
>雖然您可以刪除客戶屬性資料流，但即使刪除資料流後，其對應的資料集仍會保留。 請參閱 [刪除資料集](../../../../../catalog/datasets/user-guide.md) 以取得手動刪除資料集的步驟。

若要建立新連線，請從清單中選取資料來源，然後選取 **[!UICONTROL 下一個]**.

![新增資料](../../../../images/tutorials/create/customer-attributes/add-data.png)

### 提供資料流詳細資訊

此 [!UICONTROL 資料流詳細資訊] 步驟，允許您為資料流提供名稱和簡短說明。 在此程式中，您也可以為 [!UICONTROL 錯誤診斷], [!UICONTROL 部分擷取]，和 [!UICONTROL 警報].

[!UICONTROL 錯誤診斷] 為資料流中發生的任何錯誤記錄啟用詳細的錯誤消息生成，同時 [!UICONTROL 部分擷取] 可讓您內嵌包含錯誤的資料，最高可以是您手動定義的特定臨界值。 請參閱 [部分批次內嵌概觀](../../../../../ingestion/batch-ingestion/partial.md) 以取得更多資訊。

您可以啟用警報，以接收有關資料流狀態的通知。 從清單中選擇要訂閱的警報，以接收有關資料流狀態的通知。 如需警報的詳細資訊，請參閱 [使用UI訂閱來源警報](../../alerts.md).

完成向資料流提供詳細資訊後，請選擇 **[!UICONTROL 下一個]**.

![dataflow detail](../../../../images/tutorials/create/customer-attributes/dataflow-detail.png)

### 審核資料流

此 [!UICONTROL 檢閱] 步驟顯示，允許您在建立新資料流之前對其進行查看。 詳細資料會分組為下列類別：

* **[!UICONTROL 連線]**:顯示源類型、所選源檔案的相關路徑以及該源檔案中的列數。
* **[!UICONTROL 指派資料集和對應欄位]**:顯示要擷取來源資料的資料集，包括資料集所遵守的結構。

![審查](../../../../images/tutorials/create/customer-attributes/review.png)

## 後續步驟

建立連線後，系統會自動建立目標結構和資料集以包含傳入的資料。完成初始內嵌時，下游Platform服務(例如 [!DNL Real-Time Customer Profile] 和 [!DNL Segmentation Service]. 如需詳細資訊，請參閱下列檔案：

* [[!DNL Real-Time Customer Profile] 概覽](../../../../../profile/home.md)
* [[!DNL Segmentation Service] 概覽](../../../../../segmentation/home.md)
