---
title: 連線您的PathFactory帳戶，以透過UIExperience Platform
description: 瞭解如何透過UI將您的PathFactory帳戶連結至Experience Platform。
last-substantial-update: 2024-04-30T00:00:00Z
hide: true
hidefromtoc: true
badge: Beta
source-git-commit: 18f6c253aec6815cf84272cbce340a9aa7ed8ab9
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 1%

---

# 連線您的 [!DNL PathFactory] 要透過UIExperience Platform的帳戶

本教學課程提供如何連線至 [!DNL PathFactory] 透過UI將訪客、工作階段和頁面檢視資料傳入Adobe Experience Platform。

## 快速入門

本教學課程需要您實際瞭解下列Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md)：作為依據的標準化架構 [!DNL Experience Platform] 組織客戶體驗資料。
   * [結構描述組合基本概念](../../../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置區塊，包括結構描述組合中的關鍵原則和最佳實務。
   * [結構描述編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md)：瞭解如何使用結構編輯器UI建立自訂結構描述。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者個人檔案。

如果您已有 [!DNL PathFactory] 帳戶，您可以略過本檔案的其餘部分，並前往上的教學課程 [使用UI將行銷自動化資料帶入Experience Platform](../../dataflow/marketing-automation.md).

### 收集必要的認證 {#gather-credentials}

若要在平台上存取您的PathFactory帳戶，您必須提供下列值：

| 認證 | 說明 |
| ---------- | ----------- |
| 使用者名稱 | 您的PathFactory帳戶使用者名稱。 這對於在系統中識別您的帳戶至關重要。 |
| 密碼 | 與您的PathFactory帳戶關聯的密碼。 請確定此功能安全無虞，以防止未經授權的存取。 |
| 網域 | 與您的PathFactory帳戶關聯的網域。 這通常是指您的PathFactory URL中的唯一識別碼。 |
| 存取權杖 | 用於API驗證的唯一Token，以確保您的系統與PathFactory之間的安全通訊。 |
| api端點 | 存取資料的特定API端點：訪客、工作階段和頁面檢視。 每個端點都對應到您可以擷取的不同資料集。 **注意：** 這些規則已由預先定義 [!DNL PathFactory] 和專屬於您要存取的資料： <ul><li>**訪客端點**： `/api/public/v3/data_lake_apis/visitors.json`</li><li>**工作階段端點**： `/api/public/v3/data_lake_apis/sessions.json`</li><li>**頁面檢視端點**： `/api/public/v3/data_lake_apis/page_views.json`</li></ul> |

如需如何保護和使用您認證的詳細指引，以及取得和重新整理存取Token的相關資訊，請造訪 [PathFactory支援中心](https://support.pathfactory.com/categories/adobe/). 此資源提供管理認證的完整指南，並確保有效且安全的API整合。


## 連線您的 [!DNL PathFactory] 帳戶

在Platform UI中選取 **[!UICONTROL 來源]** 從左側導覽存取 [!UICONTROL 來源] 工作區。 此 [!UICONTROL 目錄] 會顯示Experience Platform所支援的各種來源。

您可以從類別清單中選取適當的類別。 您也可以使用搜尋列來篩選特定來源。

在 [!UICONTROL 行銷自動化] 類別，選取 **[!UICONTROL PathFactor]** 然後選取 **[!UICONTROL 設定]**.

![已選取PathFactory來源的來源目錄。](../../../../images/tutorials/create/pathfactory/catalog.png)

此 **[!UICONTROL 連線到PathFactory]** 頁面便會顯示。 您可以在此頁面上建立新帳戶或使用現有帳戶。

### 新帳戶

若要建立新帳戶，請選取 **[!UICONTROL 新帳戶]** 並提供您帳戶的名稱、選擇性說明，以及與您的帳戶對應的驗證認證 [!DNL PathFactory] 帳戶。

完成後，選取 **[!UICONTROL 連線到來源]** 然後等待一段時間以建立新連線。

![新帳戶介面，您可在此驗證PathFactory的新帳戶。](../../../../images/tutorials/create/pathfactory/new.png)

### 現有帳戶

如果您已有帳戶，請選取 **[!UICONTROL 現有帳戶]** 然後從顯示的清單中選取您要使用的帳戶。

![您可以從現有PathFactory帳戶清單中選取的現有帳戶介面。](../../../../images/tutorials/create/pathfactory/existing.png)

## 後續步驟

依照本教學課程所述，您已建立您與 [!DNL PathFactory] 帳戶和Experience Platform。 您現在可以繼續進行下一個教學課程及 [建立資料流，將您的行銷自動化資料匯入Experience Platform](../../dataflow/marketing-automation.md).
