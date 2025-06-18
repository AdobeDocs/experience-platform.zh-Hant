---
title: 在使用者介面中建立Azure Synapse Analytics Source連線
description: 瞭解如何使用Adobe Experience Platform UI建立Azure Synapse Analytics （以下稱為「Synapse」）來源連線。
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 1f1ce317-eaaf-4ad2-a5fb-236983220bd7
source-git-commit: f8eb8640360205e8ae9579d4b664d4880bf8a368
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 0%

---

# 在使用者介面中建立[!DNL Azure Synapse Analytics]來源連線

>[!IMPORTANT]
>
>[!DNL Azure Synapse Analytics]來源可在來源目錄中提供給已購買Real-Time Customer Data Platform Ultimate的使用者。

請閱讀本指南，瞭解如何使用UI中的來源工作區將您的[!DNL Azure Synapse Analytics]帳戶連結至Adobe Experience Platform。

## 快速入門

本教學課程需要您實際瞭解下列Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md)： [!DNL Experience Platform]用來組織客戶體驗資料的標準化架構。
   * [結構描述組合的基本概念](../../../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置區塊，包括結構描述組合中的關鍵原則和最佳實務。
   * [結構描述編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md)：瞭解如何使用結構描述編輯器使用者介面建立自訂結構描述。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。

如果您已經有有效的[!DNL Azure Synapse Analytics]連線，您可以略過本檔案的其餘部分，並繼續進行有關[設定資料流](../../dataflow/databases.md)的教學課程。

### 收集必要的認證

閱讀[[!DNL Azure Synapse Analytics] 總覽](../../../../connectors/databases/synapse-analytics.md#prerequisites)以取得驗證的相關資訊。

## 瀏覽來源目錄

在Experience Platform UI中，從左側導覽選取&#x200B;**[!UICONTROL 來源]**&#x200B;以存取&#x200B;*[!UICONTROL 來源]*&#x200B;工作區。 選擇類別或使用搜尋列來尋找您的來源。

若要連線到[!DNL Azure Synapse Analytics]，請移至&#x200B;*[!UICONTROL 資料庫]*&#x200B;類別，選取&#x200B;**[!UICONTROL Azure Synapse分析]**&#x200B;來源卡，然後選取&#x200B;**[!UICONTROL 設定]**。

>[!TIP]
>
>當指定的來源尚未具有已驗證的帳戶時，來源目錄中的來源會顯示&#x200B;**[!UICONTROL 設定]**&#x200B;選項。 建立已驗證的帳戶後，此選項會變更為&#x200B;**[!UICONTROL 新增資料]**。

![已選取「Azure Synapse Analytics」的來源目錄。](../../../../images/tutorials/create/azure-synapse-analytics/catalog.png)

## 使用現有帳戶 {#existing}

若要使用現有帳戶，請選取&#x200B;**[!UICONTROL 現有帳戶]**，然後選取您要使用的[!DNL Azure Synapse Analytics]帳戶。

![來源工作流程的現有帳戶介面。](../../../../images/tutorials/create/azure-synapse-analytics/existing.png)

## 建立新帳戶 {#new}

若要建立新帳戶，請選取&#x200B;**[!UICONTROL 新帳戶]**，然後提供名稱並選擇性地為您的帳戶新增說明。

![來源工作流程的新帳戶介面。](../../../../images/tutorials/create/azure-synapse-analytics/new.png)

### 連線至Experience Platform

您可以使用帳戶金鑰驗證或服務主體與金鑰驗證，將您的[!DNL Azure Synapse Analytics]帳戶連線至Experience Platform。

>[!BEGINTABS]

>[!TAB 帳戶金鑰驗證]

若要使用帳戶金鑰驗證，請選取&#x200B;**[!UICONTROL 帳戶金鑰驗證]**，提供您的[連線字串](../../../../connectors/databases/synapse-analytics.md#prerequisites)，然後選取&#x200B;**[!UICONTROL 連線至來源]**。

![來源工作流程中的「建立新帳戶」步驟（已選取「帳戶金鑰驗證」）。](../../../../images/tutorials/create/azure-synapse-analytics/account-key-auth.png)

>[!TAB 服務主體和金鑰驗證]

或者，選取&#x200B;**[!UICONTROL 服務主體和金鑰驗證]**，提供您的[驗證認證](../../../../connectors/databases/synapse-analytics.md#prerequisites)的值，然後選取&#x200B;**[!UICONTROL 連線到來源]**。

![來源工作流程中已選取「服務主體和金鑰驗證」的「建立新帳戶」步驟。](../../../../images/tutorials/create/azure-synapse-analytics/service-principal.png)

>[!ENDTABS]

## 建立[!DNL Azure Synapse Analytics]資料的資料流

現在您已經成功連線[!DNL Azure Synapse Analytics]資料庫，您現在可以[建立資料流，並將資料庫中的資料擷取到Experience Platform](../../dataflow/databases.md)。
