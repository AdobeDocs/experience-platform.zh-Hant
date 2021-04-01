---
keywords: Experience Platform；首頁；熱門主題；客戶屬性
solution: Experience Platform
title: 在UI中建立客戶屬性來源連線
topic: 概述
type: 教學課程
description: 瞭解如何在UI中建立來源連線，以收集客戶屬性描述檔資料至Adobe Experience Platform。
translation-type: tm+mt
source-git-commit: 08a3026e969a8739a8b57226c35a6d1d3150006e
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 6%

---


# 在UI中建立客戶屬性來源連線

本教學課程提供在UI中建立來源連線的步驟，以收集客戶屬性描述檔資料至Adobe Experience Platform。 有關客戶屬性的詳細資訊，請參閱[客戶屬性概述](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/attributes.html)。

>[!IMPORTANT]
>
>客戶屬性來源目前不支援停用、啟用和刪除資料流功能。

## 建立源連接

在平台UI中，從左側導覽器選擇&#x200B;**[!UICONTROL Sources]**&#x200B;以存取[!UICONTROL Sources]工作區。 [!UICONTROL Catalog]畫面會顯示多種來源，您可以用來建立連線。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋列，找到您要使用的特定來源。

在[!UICONTROL Adobe applications]類別下，選擇&#x200B;**[!UICONTROL Customer Attributes]**，然後選擇&#x200B;**[!UICONTROL Add data]**。

>[!NOTE]
>
>如果您已建立「客戶屬性」描述檔資料的來源連線，則會停用與來源連線的選項。

![](../../../../images/tutorials/create/customer-attributes/catalog.png)

[!UICONTROL Add data]畫面會列出客戶屬性的所有可用資料來源。 要建立新連接，請從清單中選擇資料源，然後選擇&#x200B;**[!UICONTROL Next]**。

>[!NOTE]
>
>每個「客戶屬性」來源連線只能選取一個資料集。

![](../../../../images/tutorials/create/customer-attributes/add-data.png)

出現[!UICONTROL Dataflow detail]步驟，允許您命名新資料流並提供簡要說明。

在此過程中，您也可以啟用[!UICONTROL Partial ingestion]和[!UICONTROL Error diagnostics]。 [!UICONTROL Partial ingestion] 提供可收錄包含錯誤的資料的功能，最高可設定特定臨界值，同時提供 [!UICONTROL Error diagnostics] 任何個別批次錯誤資料的詳細資訊。如需詳細資訊，請參閱[部分批次擷取概觀](../../../../../ingestion/batch-ingestion/partial.md)。

![](../../../../images/tutorials/create/customer-attributes/dataflow-detail.png)

出現[!UICONTROL Review]步驟，允許您在建立新資料流之前對其進行查看。 詳細資訊會分組在下列類別中：

* **[!UICONTROL Connection]**:顯示源檔案的類型、所選源檔案的相關路徑，以及該源檔案中的列數。
* **[!UICONTROL Assign dataset & map fields]**:顯示源資料被吸收到的資料集，包括資料集所附的模式。

![](../../../../images/tutorials/create/customer-attributes/review.png)

## 後續步驟

建立連線後，系統會自動建立目標結構和資料集以包含傳入的資料。當初始擷取完成時，下游平台服務（例如[!DNL Real-time Customer Profile]和[!DNL Segmentation Service]）可使用客戶屬性描述檔資料。 如需詳細資訊，請參閱下列檔案：

* [[!DNL Real-time Customer Profile] 概觀](../../../../../profile/home.md)
* [[!DNL Segmentation Service] 概觀](../../../../../segmentation/home.md)
