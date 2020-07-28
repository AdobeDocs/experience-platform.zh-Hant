---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 存取控制概觀
topic: overview
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '1097'
ht-degree: 3%

---


# 存取控制概觀

存取控制 [!DNL Experience Platform] 權是透過 [Adobe Admin Console提供](https://adminconsole.adobe.com)。 此功能運用中的產品設定檔， [!DNL Admin Console]將使用者與權限和沙盒連結在一起。

## 存取控制階層和工作流程

要配置對的訪問控制， [!DNL Experience Platform]您必須對具有產品整合的組織具有管 [!DNL Experience Platform] 理員權限。 授予或撤消權限的最低角色是產品 **[!UICONTROL 配置檔案管理員]**。 其他可管理權限的管理員角色 **[!UICONTROL 包括產品管理員]** （可管理產品內的所有設定檔）和 **[!UICONTROL 系統管理員]** （無限制）。 如需詳細資訊，請參閱Adobe說明中 [心有關管理](https://helpx.adobe.com/enterprise/using/admin-roles.html) 角色的文章。

>[!NOTE]
>
>從此開始，本檔案中任何提及「管理員」的內容，都是指產品設定檔管理員或更高版本（如上所述）。

獲取和分配訪問權限的高級工作流可總結如下：

- 訂閱Adobe Experience Platform後，會傳送電子郵件給註冊表單中指定的管理員。
- 管理員登入 [Adobe Admin Console](#adobe-admin-console) ，並從概述頁面的產品清單中選取 **** Adobe Experience Platform。
- 管理員可以視需要檢視 [預設產品設定檔](#product-profiles) ，或建立新的客戶產品設定檔。
- 管理員可以編輯任何現有產品設定檔的權限和使用者。
- 在建立或編輯產品配置檔案時，管理員使用 **[!UICONTROL users]** 頁籤將用戶添加到配置檔案中，並通過訪問[!UICONTROL permissionsTab來授予這些用戶(如「]Read Datasets[!UICONTROL 」或「]Manage Schemas **** 」)的權限。 同樣地，管理員也可以使用相同的權限標籤來指派沙盒的存取權。
- 當使用者登入使 [!DNL Experience Platform] 用者介面時，其權 [!DNL Platform] 能存取權是由步驟2授與的權限所驅動。 例如，如果用戶沒有「[!UICONTROL View Datasets]」權限，則側面菜單中的 *[!UICONTROL Datasets]* 頁籤對該用戶將不可見。

有關如何在中管理訪問控制的詳細步驟 [!DNL Experience Platform]，請參 [閱訪問控制使用手冊](./ui/overview.md)。

所有對 [!DNL Experience Platform] API的呼叫都會經過驗證以取得權限，如果目前使用者內容中找不到適當的權限，則會傳回錯誤。 在UI中，元素會根據授予目前使用者的權限而隱藏或變更。

## Adobe Admin Console

Adobe Admin Console提供一個集中位置，可讓您管理Adobe產品權益並存取您的組織。 通過控制台，您可以授予用戶組對各種功能的訪問權 [!DNL Platform] 限，如「[!UICONTROL Manage Datasets]」、「[!UICONTROL View Datasets]」或「[!UICONTROL Manage Profiles]」。

### 產品設定檔

在中， [!DNL Admin Console]會透過使用產品設定檔，將權限指派給 **[!UICONTROL 使用者]**。 產品設定檔可讓您授予一或多個使用者權限，並包含他們透過產品設定檔指派給他們的沙盒範圍的存取權。 使用者可以指派給屬於您組織的一或多個產品設定檔。

### 預設產品設定檔

[!DNL Experience Platform] 提供兩個預先設定的預設產品設定檔。 下表概述每個預設設定檔中提供的內容，包括其授與存取權的沙盒，以及其在該沙盒範圍內授與的權限。

| 產品設定檔 | 沙盒存取 | 權限 |
| --- | --- | --- |
| 預設生產——完全訪問 | 生產 | 除「沙盒管理」權 [!DNL Experience Platform]限外，所有適用的權限。 |
| 預設沙盒管理 | 不適用 | 僅提供「沙盒管理」權限的存取。 |

## 沙盒與權限

[!DNL Experience Platform] 可存取一個「生產」沙盒，並可讓您建立「非生產」 **沙盒**。 非生產沙盒是資料虛擬化的一種形式，可讓您將資料與其他沙盒隔離，通常用於開發實驗、測試或試用。 產品描述檔的 **[!UICONTROL 權限]** ，可讓描述檔的使用者存取已授與 [!DNL Platform] 存取之沙盒環境中的功能。

有關中的沙盒的更多 [!DNL Experience Platform]資訊，請參閱沙盒 [概觀](../sandboxes/home.md)。

### 存取沙盒

沙盒的存取是透過產品設定檔來管理。 如需如何啟用產品設定檔沙盒存取的詳細步驟，請參閱存取控 [制使用指南](./ui/overview.md)。

可授予使用者產品設定檔中一或多個沙盒的存取權。 如果一位使用者包含在兩或多個產品設定檔中，該使用者將可存取這些設定檔中包含的所有沙盒。

「沙盒管理」權限可讓使用者管理、檢視或重設沙盒。

### 權限

產品 **描述檔中的** 「權限」標籤會顯示該描述檔中作用中的沙盒和權限：

![](./images/permissions-overview.png)

透過授予的權限會依 [!DNL Admin Console] 類別排序，而某些權限會授與對數個低階功能的存取權。

下表概述了中的可用權 [!DNL Experience Platform] 限， [!DNL Admin Console]並說明了它們授予訪問權 [!DNL Platform] 限的特定功能。 如需如何將權限新增至產品設定檔的詳細步驟，請參閱 [存取控制使用指南](./ui/overview.md)。

| 類別 | 權限 | 說明 |
| --- | --- | --- |
| [!DNL Data Modeling] | [!UICONTROL 管理結構] | 對讀取、建立、編輯和刪除方案和相關資源的訪問。 |
| [!DNL Data Modeling] | [!UICONTROL 檢視結構] | 方案和相關資源的唯讀存取權。 |
| [!DNL Data Management] | [!UICONTROL 管理資料集] | 存取讀取、建立、編輯和刪除資料集。 結構的只讀訪問。 |
| [!DNL Data Management] | [!UICONTROL 檢視資料集] | 資料集和結構描述的只讀訪問。 |
| [!DNL Data Management] | [!UICONTROL 資料監控] | 監視資料集和流的只讀訪問。 |
| [!DNL Profile Management] | [!UICONTROL 管理設定檔] | 存取用於讀取、建立、編輯和刪除客戶個人檔案的資料集。 可用設定檔的唯讀存取權。 |
| [!DNL Profile Management] | [!UICONTROL 檢視設定檔] | 可用設定檔的唯讀存取權。 |
| [!DNL Profile Management] | [!UICONTROL 匯出區段的對象] | 能夠將評估的觀眾區隔匯出至資料集。 |
| [!DNL Identities] | [!UICONTROL 管理身分識別命名空間] | 存取讀取、建立、編輯和刪除身分名稱空間。 |
| [!DNL Identities] | [!UICONTROL 檢視身分名稱空間] | 身分名稱空間的唯讀存取。 |
| [!DNL Sandbox Administration] | [!UICONTROL 管理沙盒] | 存取讀取、建立、編輯和刪除沙盒。 |
| [!DNL Sandbox Administration] | [!UICONTROL 檢視沙箱] | 屬於您組織的沙盒的唯讀存取權。 |
| [!DNL Sandbox Administration] | [!UICONTROL 重設沙盒] | 可重設沙盒。 |
| [!DNL Destinations] | [!UICONTROL 管理目標] | 存取讀取、建立、編輯和停用目標。* |
| [!DNL Destinations] | [!UICONTROL 查看目標] | 對「目錄」頁籤中可用目標和「瀏覽 **** 」頁籤中已驗證目標的唯讀訪問權。* |
| [!DNL Destinations] | [!UICONTROL 啟動目標] | 能夠將資料啟動至已建立的作用中目標。 此權限要求將「檢視目標」或「管 [!UICONTROL 理目標] 」授予要啟用目標的使用者。* |
| [!DNL Data Ingestion] | [!UICONTROL 管理來源] | 存取讀取、建立、編輯和停用來源。 |
| [!DNL Data Ingestion] | [!UICONTROL 檢視來源] | 對「目錄」標籤中可用來源的唯讀存 *[!UICONTROL 取]* ，以及「瀏覽」標籤中的已驗證 *[!UICONTROL 來源]* 。 |
| [!DNL Data Science Workspace] | [!UICONTROL 管理資料科學工作區] | 在中讀取、建立、編輯和刪除的訪問權限 [!DNL Data Science Workspace]。 |

_(*)本許可要求提供條[!DNL Real-time Customer Data Platform]款。 有關即時CDP的詳細資訊，請首先閱讀[即時CDP概述](https://docs.adobe.com/content/help/en/experience-platform/rtcdp/overview.html)。_

## 後續步驟

閱讀本指南後，您將瞭解存取控制的主要原則 [!DNL Experience Platform]。 您現在可以繼續存取控 [制使用指南](./ui/overview.md) ，以取得如何使用 [!DNL Admin Console] 建立產品設定檔及指派權限的詳細步驟 [!DNL Platform]。