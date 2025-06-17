---
title: 使用UI將Azure Databricks連線至Experience Platform
description: 瞭解如何使用使用者介面將Azure Databricks連線至Experience Platform。
badgeUltimate: label="Ultimate" type="Positive"
badgeBeta: label="Beta" type="Informative"
source-git-commit: 2bd16d5a55c5bbeedbc6a6012d9f0229eee8433a
workflow-type: tm+mt
source-wordcount: '483'
ht-degree: 4%

---

# 在UI中連線[!DNL Azure Databricks]至Experience Platform

>[!AVAILABILITY]
>
>* [!DNL Azure Databricks]來源可在來源目錄中提供給已購買Real-Time CDP Ultimate的使用者。
>
>* [!DNL Azure Databricks]來源是測試版。 閱讀來源概觀中的[條款與條件](../../../../home.md#terms-and-conditions)，以取得有關使用測試版標籤之來源的詳細資訊。

請閱讀本指南，瞭解如何使用UI中的來源工作區將您的[!DNL Azure Databricks]帳戶連結至Adobe Experience Platform。

## 快速入門

本指南需要您深入瞭解下列Experience Platform元件：

* [來源](../../../../home.md)： Experience Platform允許從各種來源擷取資料，同時讓您能夠使用Experience Platform服務來建構、加標籤以及增強傳入的資料。
* [沙箱](../../../../../sandboxes/home.md)： Experience Platform提供的虛擬沙箱可將單一Experience Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

### 收集必要的認證

提供下列認證的值，以便將[!DNL Azure Databricks]連線至Experience Platform。

| 認證 | 說明 |
| --- | --- |
| 網域 | [!DNL Azure Databricks]工作區的URL。 例如 `https://adb-1234567890123456.7.azuredatabricks.net`。 |
| 叢集ID | [!DNL Azure Databricks]中叢集的識別碼。 此叢集必須是現有的叢集，而且應該是互動式叢集。 |
| 存取權杖 | 驗證您[!DNL Azure Databricks]帳戶的存取Token。 您可以使用[!DNL Azure Databricks]工作區產生存取權杖。 |
| 資料庫 | 三角湖中的資料庫名稱。 |

如需詳細資訊，請閱讀 [[!DNL Azure Databricks]  概觀](../../../../connectors/databases/databricks.md)。

## 瀏覽來源目錄

在Experience Platform UI中，從左側導覽選取&#x200B;**[!UICONTROL 來源]**&#x200B;以存取&#x200B;*[!UICONTROL 來源]*&#x200B;工作區。 選擇類別或使用搜尋列來尋找您的來源。

若要連線到[!DNL Azure Databricks]，請移至&#x200B;*[!UICONTROL 資料庫]*&#x200B;類別，選取&#x200B;**[!UICONTROL Azure Databricks]**&#x200B;來源卡，然後選取&#x200B;**[!UICONTROL 設定]**。

>[!TIP]
>
>當指定的來源尚未具有已驗證的帳戶時，來源目錄中的來源會顯示&#x200B;**[!UICONTROL 設定]**&#x200B;選項。 建立已驗證的帳戶後，此選項會變更為&#x200B;**[!UICONTROL 新增資料]**。

![已選取Azure Databricks來源卡的來源目錄。](../../../../images/tutorials/create/databricks/catalog.png)

### 使用現有帳戶

若要使用現有帳戶，請選取&#x200B;**[!UICONTROL 現有帳戶]**，然後選取您要使用的[!DNL Azure Databricks]帳戶。

![來源工作流程中已選取「現有帳戶」的現有帳戶介面。](../../../../images/tutorials/create/databricks/existing.png)

### 建立新帳戶

若要建立新帳戶，請選取&#x200B;**[!UICONTROL 新帳戶]**，並提供名稱，並選擇性地為您的帳戶新增說明。 接著，提供下列驗證認證的值：

* 網域
* 叢集ID
* 存取權杖
* 資料庫

![來源工作流程中的新帳戶介面已提供帳戶名稱和選擇性說明。](../../../../images/tutorials/create/databricks/new.png)

此外，您必須將[!UICONTROL 分段SAS URI]認證複製並貼到您的[!DNL Azure Databricks]環境。 完成後，請選取&#x200B;**[!UICONTROL 連線到來源]**，並等待一段時間以建立連線。

![SAS URI暫存認證。](../../../../images/tutorials/create/databricks/sas-uri.png)

## 建立[!DNL Azure Databricks]資料的資料流

現在您已經成功連線[!DNL Azure Databricks]帳戶，您現在可以[建立資料流，並將資料庫中的資料擷取到Experience Platform](../../dataflow/databases.md)。
