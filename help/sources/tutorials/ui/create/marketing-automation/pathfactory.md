---
title: 透過UI將您的PathFactory帳戶連線至Experience Platform
description: 瞭解如何透過UI將您的PathFactory帳戶連結至Experience Platform。
badge: Beta
exl-id: 859dd0c1-8c4b-43e3-a87b-84c879460bc0
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 2%

---

# 透過UI將您的[!DNL PathFactory]帳戶連線至Experience Platform

本教學課程提供如何透過UI將您的[!DNL PathFactory]訪客、工作階段和頁面檢視資料連結至Adobe Experience Platform的步驟。

## 快速入門

本教學課程需要您實際瞭解下列Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md)： [!DNL Experience Platform]用來組織客戶體驗資料的標準化架構。
   * [結構描述組合的基本概念](../../../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置區塊，包括結構描述組合中的關鍵原則和最佳實務。
   * [結構描述編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md)：瞭解如何使用結構描述編輯器使用者介面建立自訂結構描述。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。

如果您已有[!DNL PathFactory]帳戶，可以略過本檔案的其餘部分，然後繼續進行[使用UI將行銷自動化資料帶入Experience Platform的教學課程](../../dataflow/marketing-automation.md)。

### 收集必要的認證 {#gather-credentials}

若要在Experience Platform上存取PathFactory帳戶，您必須提供下列值：

| 認證 | 說明 |
| ---------- | ----------- |
| 使用者名稱 | 您的PathFactory帳戶使用者名稱。 這對於在系統中識別您的帳戶至關重要。 |
| 密碼 | 與您的PathFactory帳戶關聯的密碼。 請確定此功能安全無虞，以防止未經授權的存取。 |
| 網域 | 與您的PathFactory帳戶關聯的網域。 這通常是指您的PathFactory URL中的唯一識別碼。 |
| 存取權杖 | 用於API驗證的唯一Token，以確保您的系統與PathFactory之間的安全通訊。 |
| api端點 | 存取資料的特定API端點：訪客、工作階段和頁面檢視。 每個端點都對應到您可以擷取的不同資料集。 **注意：**&#x200B;這些資料已由[!DNL PathFactory]預先定義，而且是您想要存取的特定資料： <ul><li>**訪客端點**： `/api/public/v3/data_lake_apis/visitors.json`</li><li>**工作階段端點**： `/api/public/v3/data_lake_apis/sessions.json`</li><li>**頁面檢視端點**： `/api/public/v3/data_lake_apis/page_views.json`</li></ul> |

如需如何保護及使用認證的詳細指引，以及取得和重新整理存取Token的相關資訊，請造訪[PathFactory支援中心](https://support.pathfactory.com/categories/adobe/)。 此資源提供管理認證的完整指南，並確保有效且安全的API整合。


## 連線您的[!DNL PathFactory]帳戶

在Experience Platform UI中，從左側導覽選取&#x200B;**[!UICONTROL 來源]**&#x200B;以存取[!UICONTROL 來源]工作區。 [!UICONTROL 目錄]顯示Experience Platform支援的各種來源。

您可以從類別清單中選取適當的類別。 您也可以使用搜尋列來篩選特定來源。

在[!UICONTROL 行銷自動化]類別下，選取&#x200B;**[!UICONTROL PathFactory]**，然後選取&#x200B;**[!UICONTROL 設定]**。

![已選取PathFactory來源的來源目錄。](../../../../images/tutorials/create/pathfactory/catalog.png)

**[!UICONTROL 連線到PathFactory]**&#x200B;頁面就會顯示。 您可以在此頁面上建立新帳戶或使用現有帳戶。

### 新帳戶

若要建立新帳戶，請選取「**[!UICONTROL 新帳戶]**」，並提供您帳戶的名稱、選擇性說明，以及與您[!DNL PathFactory]帳戶對應的驗證認證。

完成時，請選取&#x200B;**[!UICONTROL 連線到來源]**，然後等待一段時間以建立新連線。

![新帳戶介面，您可以在此介面驗證PathFactory的新帳戶。](../../../../images/tutorials/create/pathfactory/new.png)

### 現有帳戶

如果您已有現有的帳戶，請選取&#x200B;**[!UICONTROL 現有的帳戶]**，然後從顯示的清單中選取您要使用的帳戶。

![您可以從現有PathFactory帳戶清單中選取的現有帳戶介面。](../../../../images/tutorials/create/pathfactory/existing.png)

## 後續步驟

依照本教學課程中的指示，您已建立[!DNL PathFactory]帳戶與Experience Platform之間的連線。 您現在可以繼續進行下一個教學課程，並[建立資料流，將您的行銷自動化資料匯入Experience Platform](../../dataflow/marketing-automation.md)。
