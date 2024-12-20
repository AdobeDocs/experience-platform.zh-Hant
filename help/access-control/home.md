---
keywords: Experience Platform；首頁；熱門主題；存取控制；adobe admin console
solution: Experience Platform
title: 存取控制概覽
description: Adobe Experience Platform的存取控制可透過Adobe Admin Console提供。 此功能運用Admin Console中的產品設定檔，將使用者與許可權和沙箱連結。
exl-id: 591d59ad-2784-4ae4-a509-23649ce712c9
source-git-commit: 5d5c57dfb9e4abda6b1bca96147a95d063bc17c6
workflow-type: tm+mt
source-wordcount: '1787'
ht-degree: 1%

---

# 存取控制概覽

Adobe Experience Platform的存取控制是透過[Adobe Experience Cloud](https://experience.adobe.com/)中的&#x200B;**[!UICONTROL 許可權]**&#x200B;提供。 此功能利用角色和原則，將使用者與許可權和沙箱連結。

## 存取控制階層與工作流程

若要設定Experience Platform的存取控制，您必須擁有擁有Experience Platform產品的組織的系統或產品管理員許可權。 可授予或撤銷許可權的最低角色為產品管理員。 可以管理許可權的其他管理員角色是系統管理員（無限制）。 如需詳細資訊，請參閱[管理角色](https://helpx.adobe.com/enterprise/using/admin-roles.html)上的Adobe Help Center文章。

>[!NOTE]
>
>從此刻起，本檔案中任何提及「管理員」的詞語，都會提及產品管理員或以上人員（如上所述）。

取得及指派存取許可權的高階工作流程可概述如下：

- 授權Adobe Experience Platform或使用Experience Platform的應用程式/應用程式服務後，會傳送電子郵件給授權期間指定的管理員。
- 管理員登入[Adobe Admin Console](#adobe-admin-console)，並從總覽頁面的產品清單中選取&#x200B;**Adobe Experience Platform**。
- 若要授與Experience Platform的存取權，建議管理員將使用者新增至預設產品設定檔： `AEP-Default-All-Users`。
- 在「Experience Platform許可權」中，管理員可以建立新角色，或編輯任何現有角色的許可權和使用者。
- 在建立或編輯角色時，管理員會使用&#x200B;**[!UICONTROL 使用者]**&#x200B;索引標籤將使用者新增至角色，並透過編輯角色的許可權來授予這些使用者許可權（例如[!UICONTROL 讀取資料集]或[!UICONTROL 管理結構描述]）。 同樣地，管理員可以使用相同的編輯選項指派存取權給沙箱。
- 當使用者登入Experience Platform使用者介面時，他們對該Experience Platform功能的存取是由先前步驟授予他們的許可權所驅動。 例如，如果使用者沒有[!UICONTROL 檢視資料集]許可權，該使用者將無法看到側邊功能表中的&#x200B;**[!UICONTROL 資料集]**&#x200B;索引標籤。

如需有關如何在Experience Platform中管理存取控制的詳細步驟，請參閱[存取控制使用手冊](./ui/overview.md)。

對Experience Platform API的所有呼叫都會驗證許可權，如果在目前的使用者內容中找不到適當的許可權，則會傳回錯誤。 在UI中，元素會根據授予目前使用者的許可權而隱藏或變更。

## 權限 {#platform-permissions}

[!UICONTROL 許可權]提供管理貴組織Experience Platform存取權的中心位置。 透過[!UICONTROL 許可權]，您可以授予使用者群組各種Experience Platform功能的存取許可權，例如[!UICONTROL 管理資料集]、[!UICONTROL 檢視資料集]或[!UICONTROL 管理設定檔]。

### 角色

在[!UICONTROL 角色]區段中，許可權會透過使用角色指派給使用者。 角色可讓您將許可權授予一或多個使用者，同時也包含他們透過角色指派給他們的沙箱範圍的存取權。 您可以將使用者指派給屬於您組織的一或多個角色。

### 預設角色

Experience Platform隨附兩個預先設定的預設角色。 下表概述每個預設設定檔中提供的內容，包括他們授予存取權的沙箱，以及他們在該沙箱範圍內授予的許可權。

| 角色 | 沙箱存取 | 權限 |
| --- | --- | --- |
| 預設的生產所有存取權 | 生產 | 所有適用於Experience Platform的許可權，「沙箱管理」許可權除外。 |
| 沙箱管理員 | 不適用 | 僅提供對沙箱管理許可權的存取。 |

## 沙箱和許可權

非生產沙箱是資料虛擬化的一種形式，可讓您將資料與其他沙箱隔離，通常用於開發實驗、測試或試用。 角色的許可權可讓角色的使用者存取其有權存取之沙箱環境中的Experience Platform功能。 預設Experience Platform授權會授予您5個沙箱（一個生產環境和4個非生產環境）。 您可以新增10個非生產沙箱的套件，最多總共75個沙箱。 如需詳細資訊，請聯絡貴組織的管理員或您的Adobe銷售代表。

如需Experience Platform沙箱的詳細資訊，請參閱[沙箱總覽](../sandboxes/home.md)。

### 存取沙箱

沙箱的存取權透過角色進行管理。 如需如何啟用角色存取沙箱的詳細步驟，請參閱[屬性型存取控制角色指南](./abac/ui/roles.md)。

可授予使用者角色中一或多個沙箱的存取權。 如果兩個或更多角色中包含一個使用者，則該使用者將可存取這些角色中包含的所有沙箱。

「沙箱管理」許可權可讓使用者管理、檢視或重設沙箱。

### 資源許可權 {#permissions}

角色中的資源[!UICONTROL 許可權]標籤會顯示該角色的有效沙箱和許可權：

![許可權總覽](./images/permissions.png)

透過資源許可權授與的許可權會依類別排序，有些許可權會授與存取幾個低階功能的許可權。

下表概述角色中Experience Platform的可用許可權，以及使用者授予存取權的特定Experience Platform功能說明。 如需有關如何將許可權新增至角色的詳細步驟，請參閱[基於屬性的存取控制角色指南](./abac/ui/roles.md)。

| 類別 | 權限 | 說明 |
| --- | --- | --- |
| [!DNL AI Assistant] | [!UICONTROL 啟用AI小幫手] | 能夠詢問[AI助理](../ai-assistant/access.md)問題。 |
| [!DNL AI Assistant] | [!UICONTROL 檢視營運分析] | 存取以取得[操作性深入分析](../ai-assistant/home.md##operational-insights)查詢的回應。 |
| [!DNL Alerts] | [!UICONTROL 檢視警示歷史記錄] | 警示歷程記錄的唯讀存取權。 |
| [!DNL Alerts] | [!UICONTROL 解決警示] | 讀取、編輯和刪除警示的存取權。 |
| [!DNL Alerts] | [!UICONTROL 檢視警示] | 警示的唯讀存取權。 |
| [!DNL Alerts] | [!UICONTROL 管理警示] | 讀取、建立、編輯和刪除警示歷程記錄的存取權。 |
| [!DNL Computed Attributes] | [!UICONTROL 檢視計算屬性] | 計算屬性標籤、詳細目錄和詳細資料的唯讀存取權。 |
| [!DNL Computed Attributes] | [!UICONTROL 管理計算屬性] | 讀取、建立、刪除草稿及停用計算屬性的存取權。 |
| [!DNL Dashboards] | [!UICONTROL 檢視授權使用量儀表板] | 唯讀存取權，可檢視授權使用儀表板。 |
| [!DNL Dashboards] | [!UICONTROL 管理標準儀表板] | 新增尚未在Data Warehouse的自訂屬性。 |
| [!DNL Data Governance] | [!UICONTROL 管理使用標籤] | 存取讀取、建立和刪除使用標籤。 |
| [!DNL Data Governance] | [!UICONTROL 管理資料使用原則] | 讀取、建立、編輯和刪除資料使用原則的存取權。 |
| [!DNL Data Governance] | [!UICONTROL 檢視資料使用原則] | 屬於您組織的資料使用原則的唯讀存取權。 |
| [!DNL Data Governance] | [!UICONTROL 檢視使用者活動記錄] | 唯讀存取權，可檢視Platform活動中記錄的[稽核記錄](../landing/governance-privacy-security/audit-logs/overview.md)。 |
| [!DNL Data Ingestion] | [!UICONTROL 管理來源] | 讀取、建立、編輯和停用來源的存取權。 |
| [!DNL Data Ingestion] | [!UICONTROL 檢視來源] | 以唯讀方式存取&#x200B;**[!UICONTROL 目錄]**&#x200B;索引標籤中的可用來源，以及&#x200B;**[!UICONTROL 瀏覽]**&#x200B;索引標籤中的已驗證來源。 |
| [!DNL Data Ingestion] | [!DNL Manage Audience Share Connections] | 存取建立、接受和拒絕夥伴握手以連線兩個組織並啟用[!DNL Segment Match]流程。 |
| [!DNL Data Ingestion] | [!DNL Manage Audience Share] | 存取使用中夥伴讀取、建立、編輯和發佈[!DNL Segment Match]摘要。 |
| [!DNL Data Lifecycle] | [!UICONTROL 檢視資料生命週期] | 資料生命週期的唯讀存取。 |
| [!DNL Data Lifecycle] | [!UICONTROL 管理資料生命週期] | 讀取、建立、編輯和刪除資料生命週期的存取權。 |
| [!DNL Data Modeling] | [!UICONTROL 管理結構描述] | 讀取、建立、編輯和刪除結構描述和相關資源的存取權。 |
| [!DNL Data Modeling] | [!UICONTROL 檢視結構描述] | 對結構描述和相關資源的唯讀存取權。 |
| [!DNL Data Modeling] | [!UICONTROL 管理關係] | 讀取、建立、編輯和刪除綱要關係的存取權。 |
| [!DNL Data Modeling] | [!UICONTROL 管理身分中繼資料] | 存取讀取、建立、編輯和刪除結構描述的中繼資料。 |
| [!DNL Data Management] | [!UICONTROL 管理資料集] | 存取讀取、建立、編輯和刪除資料集。 結構描述的唯讀存取權。 |
| [!DNL Data Management] | [!UICONTROL 檢視資料集] | 資料集和結構描述的唯讀存取權。 |
| [!DNL Data Management] | [!UICONTROL 資料監視] | 監督資料集和資料流的唯讀存取權。 |
| [!DNL Data Science Workspace] | [!UICONTROL 管理資料科學Workspace] | 在[!DNL Data Science Workspace]中讀取、建立、編輯和刪除的存取權。 |
| [!DNL Destinations] | [!UICONTROL 檢視目的地] | 以唯讀方式存取&#x200B;**[!UICONTROL 目錄]**&#x200B;索引標籤中的可用目的地，以及&#x200B;**[!UICONTROL 瀏覽]**&#x200B;索引標籤中的已驗證目的地。 |
| [!DNL Destinations] | [!UICONTROL 管理目的地] | 讀取、建立和刪除目的地連線和目的地帳戶的存取權。 |
| [!DNL Destinations] | [!UICONTROL 啟用目的地] | 讓使用者能啟用現有目的地的區段。 在啟動工作流程中啟用對應步驟。 此許可權也要求將[!UICONTROL 檢視目的地]許可權授與將啟用目的地資料的使用者。 |
| [!DNL Destinations] | [!UICONTROL 啟用沒有對應的區段] | 讓使用者能夠啟用現有目的地的區段，而不顯示[對應步驟](../destinations/ui/activate-batch-profile-destinations.md#mapping)。 使用者可以在啟動工作流程中新增和移除區段，但無法新增或移除對應的屬性或身分。 此許可權也要求將[!UICONTROL 檢視目的地]許可權授與將啟用目的地資料的使用者。 |
| [!DNL Destinations] | [!UICONTROL 管理和啟用資料集目的地] | 可讀取、建立、編輯和停用資料集匯出流程。 還能對已建立的作用中資料集啟用資料。 此許可權也要求將[!UICONTROL 檢視目的地]許可權授與將啟用目的地資料的使用者。 |
| [!DNL Destinations] | [!UICONTROL 目的地製作] | 能夠使用[Adobe Experience Platform Destination SDK](../destinations/destination-sdk/overview.md)編寫目的地。 |
| [!DNL Identity Management] | [!UICONTROL 管理身分識別名稱空間] | 讀取、建立、編輯和刪除身分名稱空間的存取權。 |
| [!DNL Identity Management] | [!UICONTROL 檢視身分識別名稱空間] | 身分識別名稱空間的唯讀存取權。 |
| [!DNL Identity Management] | [!UICONTROL 檢視身分圖表] | 身分圖表的唯讀存取權。 |
| [!DNL Intelligent Services] | [!UICONTROL 檢視Attribution AI] | Attribution AI設定和深入分析的唯讀存取權。 |
| [!DNL Intelligent Services] | [!UICONTROL 管理Attribution AI] | 讀取、建立、編輯和刪除Attribution AI模型的存取權。 |
| [!DNL Intelligent Services] | [!UICONTROL 檢視Customer AI] | 存取以讀取或檢視Customer AI模型。 |
| [!DNL Intelligent Services] | [!UICONTROL 管理Customer AI] | 存取以建立、更新、刪除、啟用或停用Customer AI模型。 |
| [!DNL Profile Management] | [!UICONTROL 管理設定檔] | 從多個來源擷取資料、為個別客戶建立強大的設定檔，並將設定檔啟用的資料儲存在Data Lake和即時客戶設定檔資料存放區。 |
| [!DNL Profile Management] | [!UICONTROL 檢視設定檔] | 對可用設定檔的唯讀存取權。 |
| [!DNL Profile Management] | [!UICONTROL 管理區段] | 讀取、建立、編輯和刪除區段的存取權。 |
| [!DNL Profile Management] | [!UICONTROL 檢視區段] | 可用區段的唯讀存取權。 |
| [!DNL Profile Management] | [!UICONTROL 管理合併原則] | 讀取、建立、編輯和刪除合併原則的存取權。 |
| [!DNL Profile Management] | [!UICONTROL 檢視合併原則] | 可用合併原則的唯讀存取權。 |
| [!DNL Profile Management] | [!UICONTROL 匯入對象] | 存取讀取、建立、編輯和刪除匯入的對象。 |
| [!DNL Profile Management] | [!UICONTROL 匯出區段的對象] | 能夠將評估的對象區段匯出至資料集。 |
| [!DNL Profile Management] | [!UICONTROL 評估區段給對象] | 透過評估區段定義來為對象產生設定檔的功能。 |
| [!DNL Profile Management] | [!UICONTROL 檢視B2B AI] | 以唯讀方式存取所有B2B AI/ML服務的設定和組態。 |
| [!DNL Profile Management] | [!UICONTROL 管理B2B AI] | 存取以讀取、建立、編輯和刪除所有B2B AI/ML服務的設定和組態。 |
| [!DNL Profile Management] | [!UICONTROL 檢視B2B設定檔] | 以唯讀方式存取B2B實體設定檔（例如Account、Opportunity等）、所有B2B AI/ML服務的設定和組態，以及B2B儀表板Widget。 |
| [!DNL Profile Management] | [!UICONTROL 管理B2B設定檔] | 讀取、建立、編輯和刪除B2B實體設定檔（例如Account、Opportunity等）的存取權。 所有B2B AI/ML服務和B2B儀表板Widget之設定和設定的唯讀存取權。 |
| [!DNL Query Service] | [!UICONTROL 管理查詢] | 存取Platform資料的讀取、建立、編輯和刪除結構化SQL查詢。 |
| [!DNL Query Service] | [!UICONTROL 管理查詢服務整合] | 存取以建立、更新和刪除不會到期的認證以進行查詢服務存取。 |
| [!DNL Sandbox Administration] | [!UICONTROL 管理沙箱] | 存取讀取、建立、編輯和刪除沙箱。 |
| [!DNL Sandbox Administration] | [!UICONTROL 檢視沙箱] | 屬於您組織的沙箱的唯讀存取權。 |
| [!DNL Sandbox Administration] | [!UICONTROL 重設沙箱] | 重設沙箱的功能。 |

## 後續步驟

閱讀本指南後，您將瞭解Experience Platform中存取控制的主要原則。 您現在可以繼續參閱[以屬性為基礎的存取控制使用手冊](./abac/overview.md)，以取得有關如何使用Experience Cloud建立Experience Platform和指派角色的許可權的詳細步驟。
