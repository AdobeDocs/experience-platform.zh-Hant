---
keywords: Experience Platform；首頁；熱門主題；存取控制；adobe admin console
solution: Experience Platform
title: 存取控制概觀
description: Adobe Experience Platform的存取控制可透過Adobe Admin Console提供。 此功能運用Admin Console中的產品設定檔，將使用者與許可權和沙箱連結。
exl-id: 591d59ad-2784-4ae4-a509-23649ce712c9
source-git-commit: 6a466770495b226f890ab67b21c5cb027fd46e02
workflow-type: tm+mt
source-wordcount: '3851'
ht-degree: 0%

---

# 存取控制概觀

Adobe Experience Platform的存取控制是透過[Adobe Experience Cloud](https://experience.adobe.com/)中的&#x200B;**[!UICONTROL 許可權]**&#x200B;提供。 此功能利用角色和原則，將使用者與許可權和沙箱連結。

## 存取控制階層與工作流程

若要設定Experience Platform的存取控制，您必須對擁有Experience Platform產品的組織具有系統或產品管理員許可權。 可授予或撤銷許可權的最低角色為產品管理員。 可以管理許可權的其他管理員角色是系統管理員（無限制）。 如需詳細資訊，請參閱[管理角色](https://helpx.adobe.com/tw/enterprise/using/admin-roles.html)上的Adobe說明中心文章。

>[!NOTE]
>
>從此刻起，本檔案中任何提及「管理員」的詞語，都會提及產品管理員或以上人員（如上所述）。

取得及指派存取許可權的高階工作流程可概述如下：

- 授權Adobe Experience Platform或使用Experience Platform的應用程式/應用程式服務後，會傳送電子郵件給授權期間指定的管理員。
- 管理員登入[Adobe Admin Console](#adobe-admin-console)，並從總覽頁面的產品清單中選取&#x200B;**Adobe Experience Platform**。
- 若要授與Experience Platform的存取權，建議管理員將使用者新增至預設產品設定檔： `AEP-Default-All-Users`。
- 在Experience Platform許可權中，管理員可以建立新角色，或編輯任何現有角色的許可權和使用者。
- 在建立或編輯角色時，管理員會使用&#x200B;**[!UICONTROL 使用者]**&#x200B;索引標籤將使用者新增至角色，並透過編輯角色的許可權來授予這些使用者許可權（例如[!UICONTROL 讀取資料集]或[!UICONTROL 管理結構描述]）。 同樣地，管理員可以使用相同的編輯選項指派存取權給沙箱。
- 使用者登入Experience Platform使用者介面時，其對Experience Platform功能的存取是由上一步驟中已授予的許可權所驅動。 例如，如果使用者沒有[!UICONTROL 檢視資料集]許可權，該使用者將無法看到側邊功能表中的&#x200B;**[!UICONTROL 資料集]**&#x200B;索引標籤。

如需如何在Experience Platform中管理存取控制的詳細步驟，請參閱[存取控制使用手冊](./ui/overview.md)。

對Experience Platform API的所有呼叫都會驗證許可權，如果在目前的使用者內容中找不到適當的許可權，則會傳回錯誤。 在UI中，元素會根據授予目前使用者的許可權而隱藏或變更。

## 權限 {#platform-permissions}

[!UICONTROL 許可權]提供管理貴組織Experience Platform存取權的中心位置。 透過[!UICONTROL 許可權]，您可以授與使用者群組各種Experience Platform功能的存取許可權，例如[!UICONTROL 管理資料集]、[!UICONTROL 檢視資料集]或[!UICONTROL 管理設定檔]。

### 角色

在[!UICONTROL 角色]區段中，許可權會透過使用角色指派給使用者。 角色可讓您將許可權授予一或多個使用者，同時也包含他們透過角色指派給他們的沙箱範圍的存取權。 您可以將使用者指派給屬於您組織的一或多個角色。

### 預設角色

Experience Platform隨附兩個預先設定的預設角色。 下表概述每個預設設定檔中提供的內容，包括他們授予存取權的沙箱，以及他們在該沙箱範圍內授予的許可權。

| 角色 | 沙箱存取 | 權限 |
| --- | --- | --- |
| 預設的生產所有存取權 | Prod | 適用於Experience Platform的所有許可權，「沙箱管理」許可權除外。 |
| 沙箱管理員 | 不適用 | 提供`Prod`沙箱的存取權以及沙箱管理許可權。 |

## 沙箱和許可權

非生產沙箱是資料虛擬化的一種形式，可讓您將資料與其他沙箱隔離，通常用於開發實驗、測試或試用。 角色的許可權可讓角色的使用者在他們有權存取的沙箱環境中存取Experience Platform功能。 預設Experience Platform授權會授予您5個沙箱（一個生產環境和4個非生產環境）。 您可以新增10個非生產沙箱的套件，最多總共75個沙箱。 如需詳細資訊，請聯絡貴組織的管理員或您的Adobe銷售代表。

如需Experience Platform中沙箱的詳細資訊，請參閱[沙箱總覽](../sandboxes/home.md)。

### 存取沙箱

沙箱的存取權透過角色進行管理。 如需如何啟用角色存取沙箱的詳細步驟，請參閱[屬性型存取控制角色指南](./abac/ui/roles.md)。

可授予使用者角色中一或多個沙箱的存取權。 如果兩個或更多角色中包含一個使用者，則該使用者將可存取這些角色中包含的所有沙箱。

「沙箱管理」許可權可讓使用者管理、檢視或重設沙箱。

### 資源許可權 {#permissions}

資源許可權可授予存取特定Experience Platform功能的許可權。 資源會劃分為包含一組相關許可權的類別，這些許可權可個別指派給角色。

在[!UICONTROL 許可權]中，角色的資源工作區會顯示該角色的有效沙箱和許可權：

![具有所選類別和許可權清單的角色資源工作區。](./images/permissions.png)

下表概述了Experience Platform和透過許可權管理之應用程式的可用資源類別：

| 類別 | 說明 |
| --- | --- |
| [!DNL Adobe Mix Modeler] | 設定、管理及檢視[!DNL Adobe Mix Modeler]的許可權。 |
| [!DNL AI Assistant] | 設定[!DNL AI Assistant]的許可權。 |
| [!DNL Alerts] | 設定管理、解決和檢視警示和警示歷史記錄的許可權。 |
| [!DNL B2B Account Lists] | 設定B2B帳戶清單的管理、檢視和發佈許可權，包括帳戶清單的新增、移除、匯入和刪除帳戶等動作。 |
| [!DNL B2B Admin Configurations] | 設定管理和檢視B2B管理設定的許可權，包括數位資產管理連線、資產存放庫和事件。 |
| [!DNL B2B Assets] | 設定B2B資產的管理和檢視許可權，包括電子郵件、簡訊、登入頁面、片段、範本和影像。 |
| [!DNL B2B Buying Groups] | 設定B2B購買群組的管理和檢視許可權，包括解決方案興趣、角色範本和購買群組狀態等功能。 |
| [!DNL B2B Channel Configurations] | 設定B2B通道設定的管理和檢視許可權，包括通訊限制、API認證和安全性設定等設定。 |
| [!DNL B2B Dashboards] | 設定B2B儀表板的檢視許可權，包括帳戶參與度、購買群組階段、飆升帳戶和聯絡人涵蓋範圍等功能。 |
| [!DNL B2B Journeys] | 設定B2B歷程的管理、檢視和發佈許可權，包括帳戶和人員動作、事件接聽程式及分割路徑等功能。 |
| [!DNL Campaigns] | 在Journey Optimizer中設定行銷活動的管理、發佈和檢視許可權。 |
| [!DNL Channel Configurations] | 設定管理、檢視和匯出通道設定功能，例如子網域、IP集區、訊息預設集、PTR記錄、隱藏清單、登陸頁面設定、簡訊設定和檔案路由。 |
| [!DNL Collaborations] | 設定管理和檢視Real-time Customer Data Profile Collaboration功能的許可權。 |
| [!DNL Computed Attributes] | 設定管理和檢視草稿或發佈之計算屬性的許可權。 |
| [!DNL Customer Managed Keys] | 設定客戶自控金鑰的管理許可權。 |
| [!DNL Dashboards] | 設定對標準、自訂和授權控制面板的管理和檢視許可權。 |
| [!DNL Data Collection] | 設定管理和檢視資料串流的許可權。 |
| [!DNL Data Governance] | 設定管理、套用和檢視資料管理功能的許可權，例如標籤、原則和活動記錄。 |
| [!DNL Data Ingestion] | 設定管理和檢視資料擷取功能的許可權，例如來源和受眾共用。 |
| [!DNL Data Lifecycle] | 設定管理和檢視資料衛生功能的許可權。 |
| [!DNL Data Management] | 設定資料集和監控資料集及資料流等資料管理功能的管理和檢視許可權。 |
| [!DNL Data Modeling] | 設定資料模型功能（例如結構描述、關係和身分中繼資料）的管理與檢視許可權。 |
| [!DNL Data Science Workspace] | 設定[!DNL Data Science Workspace]的管理許可權。 |
| [!DNL Decision Management] | 在決策管理中設定管理和檢視決策、優惠和排名策略功能的許可權。 |
| [!DNL Destinations] | 設定管理和檢視目標的許可權，包括目標的啟用和製作SDK等功能。 |
| [!DNL Federated Data] | 設定管理和檢視同盟資料功能的許可權。 |
| [!DNL Identity Management] | 設定管理及檢視Identity Service功能（例如身分名稱空間及身分圖表）的許可權。 |
| [!DNL Intelligent Service] | 設定在Intelligent Service中管理和檢視Attribution AI和Customer AI的許可權。 |
| [!DNL IP Warmup Configurations] | 設定管理和檢視IP熱身計畫的許可權，以及檢視檢視IP熱身報告的許可權。 |
| [!DNL Journey Optimizer Library] | 在Adobe Journey Optimizer中設定程式庫專案的管理許可權。 |
| [!DNL Journey Optimizer Rules] | 在Adobe Journey Optimizer中設定頻率規則的管理和檢視許可權。 |
| [!DNL Journeys] | 設定管理、發佈和檢視歷程的許可權，包括歷程報告、事件、資料來源和動作等功能。 |
| [!DNL Messages] | 設定管理、發佈和檢視訊息的許可權，包括訊息預覽和測試等功能。 |
| [!DNL Privacy Service] | 設定管理和檢視Privacy Service功能的許可權。 |
| [!DNL Profile Management] | 設定管理、檢視、匯出和評估設定檔服務功能的許可權，例如對象、設定檔和合併原則。 |
| [!DNL Prospects] | 設定對潛在客戶結構描述、設定檔和對象的管理和檢視許可權，包括檢視潛在客戶摺疊式功能表等功能。 |
| [!DNL Query Service] | 設定查詢服務功能（例如不會到期的認證和結構化SQL查詢）的管理許可權。 |
| [!DNL Reports] | 設定管道報表的檢視許可權。 |
| [!DNL Sandbox Administration] | 管理沙箱時設定管理、檢視和重設許可權。 |
| [!DNL Traits Configuration] | 透過計算屬性UI設定管理和檢視特徵。 |
| [!DNL Translation Services] | 針對專案、任務、評論、內部、設定和提供者，設定翻譯服務的管理和檢視許可權。 |

下表概述角色中Experience Platform的可用許可權，以及使用者授予存取權的特定Experience Platform功能說明。 如需有關如何將許可權新增至角色的詳細步驟，請參閱[基於屬性的存取控制角色指南](./abac/ui/roles.md)。

| 類別 | 權限 | 說明 |
| --- | --- | --- |
| [!DNL Adobe Mix Modeler] | [!UICONTROL 管理Adobe Mix Modeler協調資料] | 檢視和修改協調資料的能力。 |
| [!DNL Adobe Mix Modeler] | [!UICONTROL 檢視Adobe Mix Modeler協調資料] | 以唯讀方式存取協調的資料。 |
| [!DNL Adobe Mix Modeler] | [!UICONTROL 管理Adobe Mix Modeler模型設定] | 檢視和修改模型組態的功能。 |
| [!DNL Adobe Mix Modeler] | [!UICONTROL 檢視Adobe Mix Modeler模型設定] | 以唯讀方式存取模型設定。 |
| [!DNL Adobe Mix Modeler] | [!UICONTROL 管理Adobe Mix Modeler模型計畫設定] | 檢視與修改計畫組態的功能。 |
| [!DNL Adobe Mix Modeler] | [!UICONTROL 檢視Adobe Mix Modeler模型計畫設定] | 計畫組態的唯讀存取權。 |
| [!DNL AI Assistant] | [!UICONTROL 啟用AI小幫手] | 能夠提出[[!DNL [AI assistant]]](../ai-assistant/access.md)個問題。 |
| [!DNL AI Assistant] | [!UICONTROL 檢視營運分析] | 存取以取得[操作性深入分析](../ai-assistant/home.md##operational-insights)查詢的回應。 |
| [!DNL AI Assistant] | [!UICONTROL 產生內容] | 讓使用者能夠使用[!DNL AI Assistant]產生內容。 |
| [!DNL AI Assistant] | [!UICONTROL 管理品牌套件] | 讓使用者能夠使用[!DNL AI Assistant]建立品牌指引。 |
| [!DNL Alerts] | [!UICONTROL 檢視警示歷史記錄] | 警示歷程記錄的唯讀存取權。 |
| [!DNL Alerts] | [!UICONTROL 解決警示] | 讀取、編輯和刪除警示的存取權。 |
| [!DNL Alerts] | [!UICONTROL 檢視警示] | 警示的唯讀存取權。 |
| [!DNL Alerts] | [!UICONTROL 管理警示] | 讀取、建立、編輯和刪除警示的存取權。 |
| [!DNL B2B Account Lists] | [!UICONTROL 管理B2B帳戶清單] | 能夠檢視及存取左側導覽中的&#x200B;**[!UICONTROL 帳戶清單]**。 有權存取&#x200B;**[!UICONTROL 帳戶清單]**&#x200B;的使用者應該有權存取所有帳戶清單CRUD功能： `/accounts-list`。 |
| [!DNL B2B Admin Configurations] | [!UICONTROL 管理B2B管理設定] | 可在左側導覽中檢視及存取&#x200B;**[!UICONTROL B2B管理組態]**。 有權存取&#x200B;**[!UICONTROL B2B管理設定]**&#x200B;的使用者應該有權存取所有SMS API認證CRUD功能： `/admin-configs`。 |
| [!DNL B2B Assets] | [!UICONTROL 管理B2B Assets] | 可在左側導覽中檢視及存取&#x200B;**[!UICONTROL Assets]**。 有權存取&#x200B;**[!UICONTROL Assets]**&#x200B;的使用者應該有權存取所有Assets CRUD功能： `/assets-listing`。 |
| [!DNL B2B Assets] | [!UICONTROL 管理B2B範本] | 可在左側導覽中檢視及存取&#x200B;**[!UICONTROL 範本]**。 有權存取&#x200B;**[!UICONTROL 範本]**&#x200B;的使用者應該有權存取所有範本CRUD功能： `/b2b-content-templates`。 |
| [!DNL B2B Assets] | [!UICONTROL 管理B2B片段] | 可在左側導覽中檢視及存取&#x200B;**[!UICONTROL 片段]**。 有權存取&#x200B;**[!UICONTROL 片段]**&#x200B;的使用者應該有權存取所有片段CRUD函式： `/fragments`。 |
| [!DNL B2B Buying Groups] | [!UICONTROL 管理B2B購買群組] | 可在左側導覽中檢視及存取&#x200B;**[!UICONTROL 購買群組]**。 有權存取&#x200B;**[!UICONTROL 購買群組]**&#x200B;的使用者應該有權存取所有購買群組CRUD功能： `/buying-groups`。 |
| [!DNL B2B Dashboards] | [!UICONTROL 管理B2B參與儀表板] | 可在左側導覽中檢視及存取&#x200B;**[!UICONTROL 儀表板]**。 有權存取&#x200B;**[!UICONTROL 儀表板]**&#x200B;的使用者應該有權存取所有儀表板CRUD功能： `/insights-dashboard`。 |
| [!DNL B2B Channel Configurations] | [!UICONTROL 管理B2B通道設定] | 可在左側導覽中檢視及存取&#x200B;**[!UICONTROL 管道]**。 有權存取&#x200B;**[!UICONTROL 管道]**&#x200B;的使用者應該有權存取所有管道CRUD功能： `/channels-config`。 |
| [!DNL B2B Journeys] | [!UICONTROL 管理B2B帳戶歷程] | 可在左側導覽中檢視及存取&#x200B;**[!UICONTROL 帳戶歷程]**。 有權存取&#x200B;**[!UICONTROL 帳戶歷程]**&#x200B;的使用者應該有權存取所有帳戶歷程CRUD功能： `/account-journeys`。 |
| [!DNL Campaigns] | [!UICONTROL 管理行銷活動] | 讀取、建立、編輯和刪除行銷活動的存取權。 |
| [!DNL Campaigns] | [!UICONTROL 核准並發佈行銷活動] | 核准和發佈行銷活動的功能。 |
| [!DNL Campaigns] | [!UICONTROL 發佈行銷活動] | 發佈行銷活動的功能。 |
| [!DNL Campaigns] | [!UICONTROL 檢視行銷活動] | 行銷活動的唯讀存取權。 |
| [!DNL Campaigns] | [!UICONTROL 檢視行銷活動報告] | 對行銷活動報告的唯讀存取權。 |
| [!DNL Channel Configurations] | [!UICONTROL 檢視郵件一般設定] | 對訊息一般設定的唯讀存取權。 |
| [!DNL Channel Configurations] | [!UICONTROL 管理子網域委派] | 讀取、建立、編輯和刪除子網域委派的存取權。 |
| [!DNL Channel Configurations] | [!UICONTROL 管理IP集區] | 讀取、建立和編輯IP集區的存取權。 |
| [!DNL Channel Configurations] | [!UICONTROL 管理郵件一般設定] | 存取讀取、建立、編輯和刪除訊息的一般設定。 |
| [!DNL Channel Configurations] | [!UICONTROL 管理訊息預設集] | 存取讀取、建立、編輯和刪除訊息預設集。 |
| [!DNL Channel Configurations] | [!UICONTROL 檢視訊息預設集] | 訊息預設集的唯讀存取權。 |
| [!DNL Channel Configurations] | [!UICONTROL 管理PTR記錄] | 讀取和編輯PTR記錄的存取權。 |
| [!DNL Channel Configurations] | [!UICONTROL 檢視PTR記錄] | 對PTR記錄的唯讀存取權。 |
| [!DNL Channel Configurations] | [!UICONTROL 管理隱藏] | 讀取、建立、編輯和刪除隱藏規則的存取權。 |
| [!DNL Channel Configurations] | [!UICONTROL 檢視隱藏清單] | 隱藏清單的唯讀存取權。 |
| [!DNL Channel Configurations] | [!UICONTROL 匯出隱藏清單] | 存取隱藏清單匯出為CSV檔案。 |
| [!DNL Channel Configurations] | [!UICONTROL 管理登入頁面設定] | 存取讀取、建立、編輯和刪除登入頁面設定。 |
| [!DNL Channel Configurations] | [!UICONTROL 管理簡訊設定] | 存取讀取、建立、編輯和刪除簡訊設定。 |
| [!DNL Channel Configurations] | [!UICONTROL 管理SMS子網域] | 讀取、建立、編輯和刪除SMS子網域的存取權。 |
| [!DNL Channel Configurations] | [!UICONTROL 管理檔案路由] | 讀取、建立、編輯和刪除檔案製程的存取權。 |
| [!DNL Channel Configurations] | [!UICONTROL 檢視檔案路由] | 檔案製程的唯讀存取權。 |
| [!DNL Channel Configurations] | [!UICONTROL 管理種子清單] | 建立及編輯Seedlist的功能。 |
| [!DNL Channel Configurations] | [!UICONTROL 管理語言設定] | 能夠建立和編輯語言設定。 |
| [!DNL Channel Configurations] | [!UICONTROL 管理Web子網域] | 建立及編輯CJM Web子網域的功能。 |
| [!DNL Channel Configurations] | [!UICONTROL 管理推播認證] | 建立、編輯和刪除推送認證的功能。 |
| [!DNL Collaborations] | [!UICONTROL 管理Collaboration執行個體] | 檢視、建立、更新及刪除組織的共同作業執行個體。 探索其他組織的共同作業執行個體。 |
| [!DNL Collaborations] | [!UICONTROL 讀取Collaboration執行個體] | 讀取組織的共同作業執行個體並探索其他組織的共同作業執行個體。 |
| [!DNL Collaborations] | [!UICONTROL 管理連線邀請] | 檢視、建立及刪除貴組織所起始的連線邀請。 接受並拒絕其他組織所起始的連線邀請。 |
| [!DNL Collaborations] | [!UICONTROL 讀取連線邀請] | 以唯讀方式存取連線邀請。 |
| [!DNL Collaborations] | [!UICONTROL 管理Collaboration連線] | 廣告商可以檢視、建立和更新設定，以及提交和刪除連線。 發行者可以檢視、接受或拒絕連線。 |
| [!DNL Collaborations] | [!UICONTROL 讀取Collaboration連線] | 對連線的唯讀存取。 |
| [!DNL Collaborations] | [!UICONTROL 管理對象資料] | 入門和探索對象。 更新公開、私人和自訂對象，並管理對象詳細目錄中繼資料設定。 |
| [!DNL Collaborations] | [!UICONTROL 讀取對象資料] | 閱讀和探索對象。 |
| [!DNL Collaborations] | [!UICONTROL 管理測量資料] | 上線、更新及刪除測量資料。 |
| [!DNL Collaborations] | [!UICONTROL 讀取測量資料] | 以唯讀方式存取測量資料。 |
| [!DNL Collaborations] | [!UICONTROL 管理專案] | 檢視、建立、更新和刪除任何探索、共用、啟用和測量活動的專案。 |
| [!DNL Collaborations] | [!UICONTROL 讀取專案] | 檢視任何探索、共用、啟用和測量活動的專案。 |
| [!DNL Collaborations] | [!UICONTROL 讀取使用者活動] | 對使用者活動的唯讀存取權。 |
| [!DNL Collaborations] | [!UICONTROL 匯出使用者活動] | 匯出使用者活動。 |
| [!DNL Collaborations] | [!UICONTROL 讀取Collaboration信用監控] | 組織與執行環境層次的信用監控。 |
| [!DNL Computed Attributes] | [!UICONTROL 檢視計算屬性] | 計算屬性標籤、詳細目錄和詳細資料的唯讀存取權。 |
| [!DNL Computed Attributes] | [!UICONTROL 管理計算屬性] | 讀取、建立、刪除草稿及停用計算屬性的存取權。 |
| [!DNL Customer Managed Keys] | [!UICONTROL 管理客戶管理的金鑰] | 存取以檢視及設定客戶自控金鑰。 |
| [!DNL Dashboards] | [!UICONTROL 檢視授權使用量儀表板] | 唯讀存取權，可檢視授權使用儀表板。 |
| [!DNL Dashboards] | [!UICONTROL 管理標準儀表板] | 新增尚未在Data Warehouse的自訂屬性。 |
| [!DNL Dashboards] | [!UICONTROL 檢視標準儀表板] | 對「設定檔」、「目的地」和「區段」控制面板的唯讀存取權。 也可讓您存取左側導覽中的儀表板，以及儀表板詳細目錄和整合索引標籤。 |
| [!DNL Dashboards] | [!UICONTROL 管理自訂儀表板] | 存取以建立或編輯控制面板。 |
| [!DNL Dashboards] | [!UICONTROL 檢視自訂儀表板] | 對使用者定義控制面板的唯讀存取權。 |
| [!DNL Dashboards] | [!UICONTROL 管理報表排程] | 建立排程的功能。 |
| [!DNL Dashboards] | [!UICONTROL 匯出儀表板資料] | 控制使用者從查詢專業模式儀表板匯出表格資料的能力。 |
| [!DNL Data Collection] | [!UICONTROL 管理資料串流] | 讀取、建立和編輯資料串流的存取權。 |
| [!DNL Data Collection] | [!UICONTROL 檢視資料串流] | 資料串流的唯讀存取權。 |
| [!DNL Data Governance] | [!UICONTROL 管理使用標籤] | 存取讀取、建立和刪除使用標籤。 |
| [!DNL Data Governance] | [!UICONTROL 管理資料使用原則] | 讀取、建立、編輯和刪除資料使用原則的存取權。 |
| [!DNL Data Governance] | [!UICONTROL 檢視資料使用原則] | 屬於您組織的資料使用原則的唯讀存取權。 |
| [!DNL Data Governance] | [!UICONTROL 檢視使用者活動記錄] | 唯讀存取權，可檢視Experience Platform活動中記錄的[稽核記錄](../landing/governance-privacy-security/audit-logs/overview.md)。 |
| [!DNL Data Governance] | [!UICONTROL 檢視隱私主控台] | 對隱私權主控台的唯讀存取。 |
| [!DNL Data Ingestion] | [!UICONTROL 管理來源] | 讀取、建立、編輯和停用來源的存取權。 |
| [!DNL Data Ingestion] | [!UICONTROL 檢視來源] | 以唯讀方式存取&#x200B;**[!UICONTROL 目錄]**&#x200B;索引標籤中的可用來源，以及&#x200B;**[!UICONTROL 瀏覽]**&#x200B;索引標籤中的已驗證來源。 |
| [!DNL Data Ingestion] | [!DNL Manage Audience Share Connections] | 存取建立、接受和拒絕夥伴共用，以連線兩個組織並啟用[!DNL Segment Match]流程。 |
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
| [!DNL Decision Management] | [!UICONTROL 管理體驗決策] | 管理體驗決策實體的功能。 |
| [!DNL Decision Management] | [!UICONTROL 檢視體驗決策] | 唯讀存取體驗決策實體。 |
| [!DNL Decision Management] | [!UICONTROL 管理決定] | 存取讀取、建立、編輯和刪除決策實體。 |
| [!DNL Decisions Management] | [!UICONTROL 檢視決定] | 決策實體的唯讀存取權。 |
| [!DNL Decision Management] | [!UICONTROL 管理優惠方案] | 存取以讀取、建立、編輯和刪除所有優惠方案和元件。 決策和集合的唯讀存取權。 |
| [!DNL Decsion Management] | [!UICONTROL 管理排名策略] | 存取讀取、建立、編輯和刪除自訂報告，以及使用動作功能。 |
| [!DNL Destinations] | [!UICONTROL 檢視目的地] | 以唯讀方式存取&#x200B;**[!UICONTROL 目錄]**&#x200B;索引標籤中的可用目的地，以及&#x200B;**[!UICONTROL 瀏覽]**&#x200B;索引標籤中的已驗證目的地。 |
| [!DNL Destinations] | [!UICONTROL 管理目的地] | 讀取、建立和刪除目的地連線和目的地帳戶的存取權。 |
| [!DNL Destinations] | [!UICONTROL 啟用目的地] | 啟用資料至已建立之作用中目的地的功能。 此許可權也要求將[!UICONTROL 檢視目的地]或[!UICONTROL 管理目的地]授與將啟用目的地的使用者。 |
| [!DNL Destinations] | [!UICONTROL 啟用沒有對應的區段] | 能夠啟用現有目的地的對象，而不顯示[對應步驟](../destinations/ui/activate-batch-profile-destinations.md#mapping)。 使用者可以在啟動工作流程中新增和移除對象，但無法新增或移除對應的屬性或身分。 此許可權也要求將[!UICONTROL 檢視目的地]許可權授與將啟用目的地資料的使用者。 |
| [!DNL Destinations] | [!UICONTROL 管理和啟用資料集目的地] | 可讀取、建立、編輯和停用資料集匯出流程。 還能對已建立的作用中資料集啟用資料。 此許可權也要求將[!UICONTROL 檢視目的地]許可權授與將啟用目的地資料的使用者。 |
| [!DNL Destinations] | [!UICONTROL 目的地製作] | 能夠使用[Adobe Experience Platform Destination SDK](../destinations/destination-sdk/overview.md)編寫目的地。 |
| [!DNL Federated Data] | [!UICONTROL 管理同盟資料] | 能夠存取所有同盟資料功能，例如建立結構描述、模型和組合。 |
| [!DNL Identity Management] | [!UICONTROL 管理身分識別名稱空間] | 讀取、建立、編輯和刪除身分名稱空間的存取權。 |
| [!DNL Identity Management] | [!UICONTROL 檢視身分識別名稱空間] | 身分識別名稱空間的唯讀存取權。 |
| [!DNL Identity Management] | [!UICONTROL 檢視身分圖表] | 身分圖表的唯讀存取權。 |
| [!DNL Identity Management] | [!UICONTROL 管理身分設定] | 讀取、建立和編輯身分設定的存取權。 |
| [!DNL Identity Management] | [!UICONTROL 檢視身分設定] | 以唯讀方式存取身分設定。 |
| [!DNL Intelligent Services] | [!UICONTROL 檢視Attribution AI] | Attribution AI設定和深入分析的唯讀存取權。 |
| [!DNL Intelligent Services] | [!UICONTROL 管理Attribution AI] | 存取讀取、建立、編輯和刪除Attribution AI模型。 |
| [!DNL Intelligent Services] | [!UICONTROL 檢視Customer AI] | 存取以讀取或檢視Customer AI模型。 |
| [!DNL Intelligent Services] | [!UICONTROL 管理Customer AI] | 存取以建立、更新、刪除、啟用或停用Customer AI模型。 |
| [!DNL IP Warmup Configurations] | [!UICONTROL 檢視IP熱身計畫] | 對IP熱身計畫的唯讀存取權。 |
| [!DNL IP Warmup Configurations] | [!UICONTROL 管理IP熱身計畫] | 管理IP熱身計畫的功能。 |
| [!DNL IP Warmup Configurations] | [!UICONTROL 檢視IP熱身報告] | 對IP熱身報告的唯讀存取權。 |
| [!DNL Journeys] | [!UICONTROL 管理歷程] | 讀取、建立、編輯和刪除歷程的存取權。 |
| [!DNL Journeys] | [!UICONTROL 檢視歷程] | 歷程的唯讀存取權。 |
| [!DNL Journeys] | [!UICONTROL 檢視歷程報告] | 對歷程報告的唯讀存取權。 |
| [!DNL Journeys] | [!UICONTROL 管理歷程事件、資料來源及動作] | 讀取、建立、編輯和刪除事件、資料來源或動作的存取權。 |
| [!DNL Journeys] | [!UICONTROL 檢視歷程事件、資料來源及動作] | 以唯讀方式存取事件、資料來源或動作。 |
| [!DNL Journeys] | [!UICONTROL 核准並發佈歷程] | 在套用原則時核准和發佈歷程的功能。 |
| [!DNL Journeys] | [!UICONTROL 發佈歷程] | 發佈歷程的功能。 |
| [!DNL Journey Optimizer Library] | [!UICONTROL 管理程式庫專案] | 新增和刪除已儲存運算式的功能。 |
| [!DNL Journey Optimizer Library] | [!UICONTROL 發佈片段] | 發佈內容片段的功能。 |
| [!DNL Journey Optimizer Library] | [!UICONTROL 模擬內容] | 存取模擬內容選項以進行預覽和校樣。 |
| [!DNL Journey Optimizer Rules] | [!UICONTROL 檢影片率規則] | 頻率規則的唯讀存取權。 |
| [!DNL Journey Optimizer Rules] | [!UICONTROL 管理頻率規則] | 讀取、建立、編輯或刪除頻率規則的存取權。 |
| [!DNL Messages] | [!UICONTROL 管理訊息] | 讀取、建立、編輯和刪除訊息的存取權。 |
| [!DNL Messages] | [!UICONTROL 檢視訊息] | 訊息的唯讀存取權。 |
| [!DNL Messages] | [!UICONTROL 檢視訊息報告] | 存取以讀取和編輯訊息報告。 |
| [!DNL Messages] | [!UICONTROL 發佈訊息] | 發佈訊息的功能。 |
| [!DNL Messages] | [!UICONTROL 管理訊息預覽和測試] | 在套用原則時核准和發佈訊息的功能。 |
| [!DNL Privacy Service] | [!UICONTROL 管理Privacy Service] | 存取讀取和寫入隱私權工作流程。 |
| [!DNL Privacy Service] | [!UICONTROL 檢視Privacy Service] | 隱私權工作流程的唯讀存取權。 |
| [!DNL Profile Management] | [!UICONTROL 管理設定檔] | 存取讀取、建立、編輯和刪除用於客戶設定檔的資料集。 對可用設定檔的唯讀存取權。 |
| [!DNL Profile Management] | [!UICONTROL 檢視設定檔] | 對可用設定檔的唯讀存取權。 |
| [!DNL Profile Management] | [!UICONTROL 管理區段] | 讀取、建立、編輯和刪除對象的存取權。 |
| [!DNL Profile Management] | [!UICONTROL 檢視區段] | 可用對象的唯讀存取權。 |
| [!DNL Profile Management] | [!UICONTROL 管理合併原則] | 讀取、建立、編輯和刪除合併原則的存取權。 |
| [!DNL Profile Management] | [!UICONTROL 檢視合併原則] | 可用合併原則的唯讀存取權。 |
| [!DNL Profile Management] | [!UICONTROL 匯入對象] | 能夠使用CSV上傳工作流程匯入新對象。 |
| [!DNL Profile Management] | [!UICONTROL 匯出對象區段] | 能夠將評估的對象匯出至資料集。 |
| [!DNL Profile Management] | [!UICONTROL 評估區段給對象] | 透過評估區段定義來為對象產生設定檔的功能。 |
| [!DNL Profile Management] | [!UICONTROL 檢視B2B AI] | 以唯讀方式存取所有B2B AI/ML服務的設定和組態。 |
| [!DNL Profile Management] | [!UICONTROL 管理B2B AI] | 存取以讀取、建立、編輯和刪除所有B2B AI/ML服務的設定和組態。 |
| [!DNL Profile Management] | [!UICONTROL 檢視B2B設定檔] | 以唯讀方式存取B2B實體設定檔（例如Account、Opportunity等）、所有B2B AI/ML服務的設定和組態，以及B2B儀表板Widget。 |
| [!DNL Profile Management] | [!UICONTROL 管理B2B設定檔] | 讀取、建立、編輯和刪除B2B實體設定檔（例如Account、Opportunity等）的存取權。 所有B2B AI/ML服務和B2B儀表板Widget之設定和設定的唯讀存取權。 |
| [!DNL Profile Management] | [!UICONTROL 管理Lookalikes] | 建立或刪除相似受眾的功能。 |
| [!DNL Profile Management] | [!UICONTROL 檢視B2B體驗] | 可檢視B2B設定檔和屬性。 |
| [!DNL Profile Management] | [!UICONTROL 檢視設定檔設定] | 所有設定檔設定的唯讀存取權。 |
| [!DNL Profile Management] | [!UICONTROL 管理設定檔設定] | 存取以讀取及編輯所有設定檔設定。 |
| [!DNL Prospects] | [!UICONTROL 檢視潛在客戶] | 對潛在客戶結構描述、設定檔、對象和潛在客戶摺疊式功能表的唯讀存取權。 |
| [!DNL Prospects] | [!UICONTROL 管理潛在客戶] | 能夠建立和管理潛在客戶結構、設定檔和對象。 潛在客戶設定追蹤的唯讀存取權。 |
| [!DNL Query Service] | [!UICONTROL 管理查詢] | 存取Experience Platform資料的讀取、建立、編輯和刪除結構化SQL查詢。 |
| [!DNL Query Service] | [!UICONTROL 管理查詢服務整合] | 存取以建立、更新和刪除不會到期的認證以進行查詢服務存取。 |
| [!DNL Query Service] | [!UICONTROL 管理查詢工作階段] | 能夠逐出現有會議。 |
| [!DNL Query Service] | [!UICONTROL 管理允許清單] | 能夠管理組織的IP限制。 |
| [!DNL Reports] | [!UICONTROL 檢視管道報告] | 檢視和修改管道報表的功能。 |
| [!DNL Sandbox Administration] | [!UICONTROL 管理沙箱] | 存取讀取、建立、編輯和刪除沙箱。 |
| [!DNL Sandbox Administration] | [!UICONTROL 檢視沙箱] | 屬於您組織的沙箱的唯讀存取權。 |
| [!DNL Sandbox Administration] | [!UICONTROL 重設沙箱] | 重設沙箱的功能。 |
| [!DNL Sandbox Administration] | [!UICONTROL 管理封裝] | 存取以建立、匯入或匯出套件。 |
| [!DNL Sandbox Administration] | [!UICONTROL 共用封裝] | 在不同組織間共用套件的存取權。 |
| [!DNL Traits Configurations] | [!UICONTROL 檢視特徵] | 特徵的唯讀存取權。 |
| [!DNL Traits Configurations] | [!UICONTROL 管理特徵] | 存取權以管理特徵。 |
| [!DNL Translation Service] | [!UICONTROL 管理翻譯專案] | 管理翻譯專案的功能。 |
| [!DNL Translation Service] | [!UICONTROL 檢視翻譯專案] | 對翻譯專案的唯讀存取權。 |
| [!DNL Translation Service] | [!UICONTROL 管理翻譯工作] | 管理翻譯任務的能力。 |
| [!DNL Translation Service] | [!UICONTROL 檢視翻譯工作] | 對翻譯任務的唯讀存取權。 |
| [!DNL Translation Service] | [!UICONTROL 管理翻譯評論] | 管理翻譯稽核的功能。 |
| [!DNL Translation Service] | [!UICONTROL 檢視翻譯評論] | 對翻譯評論的唯讀存取權。 |
| [!DNL Translation Service] | [!UICONTROL 內部管理翻譯] | 內部管理翻譯的能力。 |
| [!DNL Translation Service] | [!UICONTROL 檢視內部翻譯] | 內部翻譯的唯讀存取權。 |
| [!DNL Translation Service] | [!UICONTROL 管理翻譯設定] | 管理員管理翻譯設定的功能。 |
| [!DNL Translation Service] | [!UICONTROL 管理翻譯提供者] | 管理翻譯提供者的功能。 |

## 後續步驟

閱讀本指南後，您已經瞭解Experience Platform中的存取控制主要原則。 您現在可以繼續參閱[以屬性為基礎的存取控制使用手冊](./abac/overview.md)，以取得有關如何使用Experience Cloud為Experience Platform建立角色和指派許可權的詳細步驟。
