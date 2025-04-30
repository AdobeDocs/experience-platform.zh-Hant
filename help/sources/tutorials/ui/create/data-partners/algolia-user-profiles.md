---
title: 使用UI將Algolia使用者設定檔連結到Experience Platform
description: 瞭解如何將Algolia使用者意圖連結至Experience Platform
exl-id: d4c936a7-4983-4a12-a813-03b672116e44
source-git-commit: 9bc7d372eba9ffcfe64f90d2d58a532411e5f1ce
workflow-type: tm+mt
source-wordcount: '1136'
ht-degree: 1%

---

# 使用UI將[!DNL Algolia User Profiles]資料內嵌至Experience Platform

閱讀本教學課程，瞭解如何使用使用者介面將資料從您的[!DNL Algolia User Profiles]帳戶擷取到Adobe Experience Platform。

## 快速入門

>[!IMPORTANT]
>
>開始之前，請確定您已完成[[!DNL Algolia User Profiles] 總覽](../../../../connectors/data-partners/algolia-user-profiles.md#prerequisites)中概述的先決條件步驟。

本教學課程需要您實際瞭解下列Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md)： Experience Platform用來組織客戶體驗資料的標準化架構。
   * [結構描述組合的基本概念](../../../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置區塊，包括結構描述組合中的關鍵原則和最佳實務。
   * [結構描述編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md)：瞭解如何使用結構描述編輯器使用者介面建立自訂結構描述。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。
* [來源](../../../../home.md)： Experience Platform允許從各種來源擷取資料，同時讓您能夠使用Experience Platform服務來建構、加標籤以及增強傳入的資料。

### 收集必要的認證

若要將[!DNL Algolia]連線至Experience Platform，您必須提供下列認證的值：

| 認證 | 說明 |
| --- | --- |
| 應用程式ID | [!DNL Algolia]應用程式識別碼是指派給您[!DNL Algolia]帳戶的唯一識別碼。 |
| API金鑰 | [!DNL Algolia] API金鑰是用來向[!DNL Algolia]的搜尋和索引服務驗證及授權API要求的認證。 |

如需這些認證的詳細資訊，請參閱[!DNL Algolia] [驗證檔案](https://www.algolia.com/doc/tools/cli/get-started/authentication/)。

## 連線您的[!DNL Algolia]帳戶

在Experience Platform UI中，從左側導覽選取&#x200B;**[!UICONTROL 來源]**&#x200B;以存取&#x200B;*[!UICONTROL 來源]*&#x200B;工作區。 您可以在&#x200B;*[!UICONTROL 類別]*&#x200B;面板中選取適當的類別。 或者，您可以使用搜尋列導覽至您要使用的特定來源。

若要使用[!DNL Algolia]，請選取&#x200B;*[!UICONTROL Data &amp; Identity Partners]*&#x200B;底下的&#x200B;**[!UICONTROL Algoria]**&#x200B;來源卡，然後選取&#x200B;**[!UICONTROL 設定]**。

>[!TIP]
>
>當指定的來源尚未具有已驗證的帳戶時，來源目錄中的來源會顯示&#x200B;**[!UICONTROL 設定]**&#x200B;選項。 一旦驗證帳戶存在，此選項就會變更為&#x200B;**[!UICONTROL 新增資料]**。

![已選取Algoria使用者設定檔來源的來源目錄。](../../../../images/tutorials/create/algolia/user-profiles/catalog.png)

## Authentication

### 使用現有帳戶

若要使用現有帳戶，請選取&#x200B;**[!UICONTROL 現有帳戶]**，然後選取您要使用的[!DNL Algolia User Profiles]帳戶。 若要繼續，請選取&#x200B;**[!UICONTROL 下一步]**。

![現有的帳戶介面。](../../../../images/tutorials/create/algolia/user-profiles/existing-account.png)

### 建立新帳戶

如果您正在建立新帳戶，請選取&#x200B;**[!UICONTROL 新帳戶]**，然後提供名稱、選擇性說明和[!DNL Algolia]認證。 完成時，請選取&#x200B;**[!UICONTROL 連線到來源]**，然後等待一段時間以建立新連線。

![新帳戶介面。](../../../../images/tutorials/create/algolia/user-profiles/new-account.png)

## 新增資料

建立[!DNL Algolia User Profiles]帳戶後，**[!UICONTROL 新增資料]**&#x200B;步驟隨即顯示，提供介面供您探索要帶入Experience Platform的[!DNL Algolia]使用者設定檔。

* 介面的左側部分可供您輸入選用的&#x200B;**[!UICONTROL 索引]**&#x200B;和&#x200B;**[!UICONTROL 相似性]**&#x200B;欄位。
* 介面的右側部分可讓您預覽最多100列的使用者設定檔。

完成選取和預覽要擷取的資料後，請選取&#x200B;**[!UICONTROL 下一步]**。

![工作流程的選取資料步驟。](../../../../images/tutorials/create/algolia/user-profiles/select-data.png)

## 提供資料流詳細資訊

如果您使用現有的資料集，請選取與使用[!DNL Algolia Profile]欄位群組的結構描述相關聯的資料集。

![來源工作流程的現有資料集步驟。](../../../../images/tutorials/create/algolia/user-profiles/dataflow-detail-existing-dataset.png)

如果您要建立新的資料集，請選取使用對應步驟中所需的[!DNL Algolia Profile]欄位群組的結構描述。

![來源工作流程的新資料集步驟。](../../../../images/tutorials/create/algolia/user-profiles/dataflow-detail-new-dataset.png)

## 將資料欄位對應至XDM結構描述

在將資料擷取至Experience Platform之前，請使用對應介面將來源資料對應至適當的結構描述欄位。  如需詳細資訊，請閱讀UI](../../../../../data-prep/ui/mapping.md)中的[對應指南。

![來源工作流程的對應步驟。](../../../../images/tutorials/create/algolia/user-profiles/mapping.png)

## 排程內嵌執行

接下來，使用排程介面來定義資料流的擷取排程。

<!-- The Scheduling step allows for configuration of the data/time to execute the [!DNL Algolia Uer Profiles] Source connector. There is configuration to backfill the data from [!DNL Algolia] which will pull all the profiles from the source system.  If the source is scheduled, then it will retrieve modified profiles from the [!DNL Algolia] based on the configured time interval. -->

![來源工作流程的排程步驟。](../../../../images/tutorials/create/algolia/user-profiles/scheduling.png)

| 正在排程設定 | 說明 |
| --- | --- |
| 頻率 | 設定頻率以指出資料流執行的頻率。 您可以將頻率設為： <ul><li>**一次**：將您的頻率設定為`once`以建立一次性內嵌。 建立一次性擷取資料流時，無法使用間隔和回填的設定。 依預設，排程頻率會設定為一次。</li><li>**分鐘**：將頻率設為`minute`，排程您的資料流以每分鐘擷取資料。</li><li>**小時**：將頻率設為`hour`，排程您的資料流以每小時為基礎擷取資料。</li><li>**天**：將您的頻率設為`day`，排程您的資料流每天擷取資料。</li><li>**周**：將頻率設為`week`，排程您的資料流每週擷取資料。</li></ul> |
| 間隔 | 選取頻率後，您就可以設定間隔設定，以建立每次擷取之間的時間範圍。 例如，如果您將頻率設為「天」，並將間隔設為15，則您的資料流將每隔15天執行一次。 您不能將間隔設定為零。 每個頻率的最小接受間隔值如下：<ul><li>**一次**：不適用</li><li>**分鐘**： 15</li><li>**小時**： 1</li><li>**天**： 1</li><li>**周**： 1</li></ul> |
| 開始時間 | 預計執行的時間戳記，以UTC時區顯示。 |
| 回填 | 回填會決定最初要擷取的資料。 如果已啟用回填，則會在第一次排程擷取期間擷取指定路徑中的所有目前檔案。 如果停用回填，則只會擷取在第一次內嵌執行到開始時間之間載入的檔案。 將不會擷取在開始時間之前載入的檔案。 |

## 檢閱您的資料流

使用「複查」頁面可在擷取前取得資料流的摘要。 詳細資料會分組到以下類別中：

* **連線** — 顯示來源型別、所選來源檔案的相關路徑，以及該來源檔案中的欄數。
* **指派資料集與對應欄位** — 顯示要將來源資料擷取到哪個資料集，包括資料集所堅持的結構描述。
* **排程** — 顯示內嵌排程的有效期間、頻率和間隔。

檢閱您的資料流後，請選取&#x200B;**[!UICONTROL 完成]**，並等待一些時間來建立資料流。

![來源工作流程的稽核步驟。](../../../../images/tutorials/create/algolia/user-profiles/review.png)

## 後續步驟

依照本教學課程中的指示，您已成功建立資料流，以將意圖資料從[!DNL Algolia]來源帶入Experience Platform。 如需其他資源，請瀏覽以下概述的檔案。

### 監視資料流

建立資料流後，您可以監視透過它擷取的資料，以檢視擷取率、成功和錯誤的資訊。 如需如何監視資料流的詳細資訊，請造訪有關UI](../../../../../dataflows/ui/monitor-sources.md)中[監視帳戶和資料流的教學課程。

### 更新您的資料流

若要更新資料流排程、對應和一般資訊的設定，請瀏覽有關[在UI中更新來源資料流的教學課程](../../update-dataflows.md)。

### 刪除您的資料流

您可以刪除不再需要的資料流，或使用&#x200B;**[!UICONTROL 資料流]**&#x200B;工作區中可用的&#x200B;**[!UICONTROL 刪除]**&#x200B;功能建立錯誤的資料流。 如需有關如何刪除資料流的詳細資訊，請瀏覽教學課程，瞭解如何在UI](../../delete.md)中刪除資料流[。
