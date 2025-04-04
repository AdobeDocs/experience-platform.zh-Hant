---
keywords: Experience Platform；首頁；熱門主題；客戶屬性
solution: Experience Platform
title: 在使用者介面中建立客戶屬性Source連線
type: Tutorial
description: 瞭解如何在UI中建立來源連線，以將客戶屬性設定檔資料匯入Adobe Experience Platform。
exl-id: 66bdab8f-c00e-4ebe-8b8e-f9e12cf86bbe
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 1%

---

# 在UI中建立客戶屬性來源連線

本教學課程提供在UI中建立來源連線的步驟，以便將客戶屬性設定檔資料引進Adobe Experience Platform。 如需客戶屬性的詳細資訊，請參閱[客戶屬性概觀](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/attributes.html?lang=zh-Hant??lang=zh-Hant)。

>[!IMPORTANT]
>
>客戶屬性來源目前不支援啟用或停用資料流程。

## 建立來源連線

>[!NOTE]
>
>如果您已建立客戶屬性設定檔資料的來源連線，則會停用與來源連線的選項。

在Experience Platform UI中，從左側導覽選取&#x200B;**[!UICONTROL 來源]**&#x200B;以存取[!UICONTROL 來源]工作區。 [!UICONTROL 目錄]畫面會顯示您可以建立連線的各種來源。

您可以從熒幕左側的目錄中選取適當的類別。 或者，您可以使用搜尋列來尋找您要使用的特定來源。

在[!UICONTROL Adobe應用程式]類別下，選取&#x200B;**[!UICONTROL 客戶屬性]**，然後選取&#x200B;**[!UICONTROL 新增資料]**。

![目錄](../../../../images/tutorials/create/customer-attributes/catalog.png)

### 選取客戶屬性資料來源

[!UICONTROL 新增資料]畫面會列出客戶屬性的所有可用資料來源。 每個客戶屬性來源連線只能選取一個資料集。

>[!NOTE]
>
>欄位群組、結構描述和資料集是隨流量布建一起建立的現成可用群組。 這些檔案會維持原狀，如有需要，您必須手動刪除。

客戶屬性來源不支援結構描述演化。 如果客戶屬性資料來源的結構描述輸入變更，則會與Experience Platform不相容。 暫行解決方法是刪除現有的客戶屬性資料流，及其相關資料集、結構描述和欄位群組，然後使用更新的結構描述和資料來源建立新的客戶屬性資料流。

>[!IMPORTANT]
>
>雖然您可以刪除客戶屬性資料流，但即使在刪除資料流後，其對應的資料集仍會保留。 如需如何手動刪除資料集的步驟，請參閱[刪除資料集](../../../../../catalog/datasets/user-guide.md)的指南。

若要建立新連線，請從清單中選取資料來源，然後選取&#x200B;**[!UICONTROL 下一步]**。

![新增資料](../../../../images/tutorials/create/customer-attributes/add-data.png)

### 提供資料流詳細資訊

[!UICONTROL 資料流詳細資料]步驟隨即顯示，允許您為資料流提供名稱和簡短說明。 在此程式期間，您也可以設定[!UICONTROL 錯誤診斷]、[!UICONTROL 部分擷取]和[!UICONTROL 警報]的設定。

[!UICONTROL 錯誤診斷]可針對資料流中發生的任何錯誤記錄產生詳細的錯誤訊息，而[!UICONTROL 部分擷取]可讓您擷取包含錯誤的資料，最多可擷取到您手動定義的特定臨界值。 如需詳細資訊，請參閱[部分批次擷取總覽](../../../../../ingestion/batch-ingestion/partial.md)。

您可以啟用警報以接收有關資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱[使用UI訂閱來源警示](../../alerts.md)的指南。

當您完成提供詳細資料給資料流時，請選取&#x200B;**[!UICONTROL 下一步]**。

![資料流詳細資料](../../../../images/tutorials/create/customer-attributes/dataflow-detail.png)

### 檢閱資料流

[!UICONTROL 檢閱]步驟隨即顯示，可讓您在建立新資料流之前先檢閱該資料流。 詳細資料會分組到以下類別中：

* **[!UICONTROL 連線]**：顯示來源型別、所選來源檔案的相關路徑，以及該來源檔案中的欄數。
* **[!UICONTROL 指派資料集與對應欄位]**：顯示要將來源資料擷取到哪個資料集，包括資料集所堅持的結構描述。

![檢閱](../../../../images/tutorials/create/customer-attributes/review.png)

## 後續步驟

建立連線後，系統會自動建立目標結構和資料集以包含傳入的資料。 初始內嵌完成時，下游的Experience Platform服務（例如[!DNL Real-Time Customer Profile]和[!DNL Segmentation Service]）可以使用客戶屬性設定檔資料。 如需更多詳細資訊，請參閱下列檔案：

* [[!DNL Real-Time Customer Profile] 概觀](../../../../../profile/home.md)
* [[!DNL Segmentation Service] 概觀](../../../../../segmentation/home.md)
