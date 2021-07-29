---
keywords: Experience Platform；首頁；熱門主題；Adobe Experience Platform；使用手冊；ui指南；平台ui指南；平台簡介；控制面板；
solution: Experience Platform
title: Experience PlatformUI概述
topic-legacy: ui guide
description: Adobe Experience Platform
exl-id: 47f9a3fb-731d-4ade-8069-faaa18f224dc
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '1755'
ht-degree: 3%

---

# Adobe Experience Platform UI指南

本指南提供使用Adobe Experience Platform使用者介面(UI)的簡介，說明各種元件的用途，並提供進一步說明檔案的連結以取得詳細資訊。

若要深入了解Adobe Experience Platform，請閱讀[Experience Platform概述](home.md)。

## 主畫面

登入Adobe Experience Platform後，您位於[!UICONTROL Home]頁面，該頁面由[度量儀表板](#metrics)、[最近的資料](#recent-data)和[建議的學習](#recommended-learning)區段組成。

![](images/user-guide/homepage.png)

### 量度

量度控制面板提供卡片，供您了解組織內的資料集、設定檔、區段和目的地。

![](images/user-guide/homepage-dashboard.png)

**[!UICONTROL 資料集]**&#x200B;區段顯示IMS組織內的資料集數量。 建立新資料集時，會更新此數字。 如需資料集的詳細資訊，請參閱[資料集概述](../catalog/datasets/overview.md)。

**[!UICONTROL 設定檔]**&#x200B;區段顯示IMS組織內具有設定檔的人員總數，不包括設定檔片段。 此總人數代表可定址的受眾總數，每24小時更新一次。 如需設定檔的詳細資訊，請參閱[即時客戶設定檔概述](../profile/home.md)。

**[!UICONTROL 區段]**&#x200B;區段會顯示在您的IMS組織內建立的區段總數。 建立新區段時，會更新此數字。 如需區段的詳細資訊，請參閱[分段服務概述](../segmentation/home.md)。

**[!UICONTROL Destinations]**&#x200B;區段顯示為IMS組織建立的目的地總數。 建立新目的地時，會更新此數字。 有關目的地的詳細資訊，請參閱[目的地概述](../destinations/home.md)。

### 近期資料

最近使用的資料控制面板提供最近建立的資料集、來源、區段和目的地的相關資訊。

![](images/user-guide/homepage-recent.png)

「**[!UICONTROL 最近的資料集]**」區段列出您IMS組織中最近建立的五個資料集。 每次建立新資料集時，都會更新此清單。 您可以從清單中選取資料集，以檢視指定資料集的詳細資訊，或選取&#x200B;**[!UICONTROL 檢視全部]**，以查看所有已建立資料集的清單。 如需資料集的詳細資訊，請參閱[資料集概述](../catalog/datasets/overview.md)。

「**[!UICONTROL 最近的來源]**」區段列出您IMS組織中最近建立的五個來源連接器。 每次建立新源連接器時，都會更新此清單。 您可以從清單中選擇源連接以查看有關指定連接器的更多資訊，或選擇&#x200B;**[!UICONTROL 查看全部]**&#x200B;查看所有已建立源連接的清單。 有關源的更多資訊，請參見[sources overview](../sources/home.md)。

**[!UICONTROL 最近的區段]**&#x200B;區段會列出您IMS組織中最近建立的五個區段定義。 每次建立新區段定義時，就會更新此清單。 您可以從清單中選取區段定義，以檢視指定區段定義的詳細資訊，或選取&#x200B;**[!UICONTROL 檢視全部]**&#x200B;以查看所有已建立區段定義的清單。 如需區段的詳細資訊，請參閱[分段服務概述](../segmentation/home.md)。

「**[!UICONTROL 最近的目的地]**」區段會列出您IMS組織中最近建立的五個目的地。 每次建立新目的地時，都會更新此清單。 您可以從清單中選擇一個目標以查看有關指定目標的更多資訊，或選擇&#x200B;**[!UICONTROL 查看全部]**&#x200B;以查看所有已建立目標的清單。 有關目的地的詳細資訊，請參閱[目的地概述](../destinations/home.md)。

### 建議的學習

**[!UICONTROL 建議的學習]**&#x200B;區段提供可開始使用Adobe Experience Platform的實用檔案連結。

![](images/user-guide/homepage-recommended.png)

## 頂端導覽列

Platform UI的頂端導覽列會顯示您目前登入的IMS組織，並提供數個重要的控制項。

導覽列的左側是Adobe Experience Platform標誌。 您隨時選取此選項，就會回到Platform UI主畫面。

![](./images/user-guide/homepage-top-nav-bar.png)

### IMS組織切換器

頂端導覽列右側的第一個項目是&#x200B;**IMS組織切換器**。

![](./images/user-guide/homepage-ims-org.png)

選取切換器會開啟您可存取之IMS組織的下拉式功能表（如果有的話）。 選取列出的選項，以切換至該IMS組織。

![](./images/user-guide/homepage-ims-org-switcher.png)

### 交換應用程式

頂端導覽右側的下一個項目是&#x200B;**應用程式切換器**，由![應用程式切換器](./images/user-guide/app-switcher-icon.png)圖示表示。 選取此圖示時，您可以在您的IMS組織可存取的Adobe應用程式之間切換，例如Experience Platform、Analytics、資產等。

### 說明

應用程式切換器的右側是&#x200B;**幫助和支援菜單**，該菜單由![問號/幫助](./images/user-guide/help-icon.png)表徵圖表示。 選取此圖示時，彈出式功能表隨即出現，其中包含數個說明和支援資源。 **[!UICONTROL Help]**&#x200B;標籤顯示當前所在頁面的相關文檔清單。 **[!UICONTROL Support]**&#x200B;頁簽允許您與Adobe支援團隊建立支援票證。 **[!UICONTROL Feedback]**&#x200B;標籤可讓您提交關於Platform的意見以Adobe。

![](images/user-guide/homepage-help-clicked.png)

### 通知和公告

在&#x200B;**notifications部分**&#x200B;中，該部分由![bell/Notifications and Annoments](images/user-guide/notification-icon.png)表徵圖表示。 **[!UICONTROL Notifications]**&#x200B;標籤顯示有關產品和其他相關更新的重要資訊，而&#x200B;**[!UICONTROL Announcements]**&#x200B;標籤顯示有關服務維護的資訊。

### 使用者設定檔

頂端導覽列上的最終項目是&#x200B;**使用者設定**，以![使用者設定/使用者設定檔](images/user-guide/profile-icon.png)圖示表示。 選取此圖示即可編輯您的偏好設定或登出。

### 沙盒

沙箱列就位於頂端導覽列的正下方。 此列顯示您目前用於Platform的沙箱。 如需沙箱的詳細資訊，請參閱[沙箱概述](../sandboxes/home.md)。

## 左側導覽 {#left-nav}

畫面左側的導覽列出Platform UI支援的所有不同服務。

>[!IMPORTANT]
>
>左側導覽列上的某些區段可能未顯示，或呈現灰色。 這是因為您無權存取這些功能。 如果您認為您應有權存取這些區段，請聯絡您的系統管理員。

![](images/user-guide/homepage-left.png)

**[!UICONTROL Home]**&#x200B;區段可讓您返回Platform UI首頁。

**[!UICONTROL Workflows]**&#x200B;區段顯示用於在Platform中執行操作的多步驟工作流清單。 有關工作流程的詳細資訊，請參閱[工作流程概述](./workflows.md)。

### [!UICONTROL 連線]

**[!UICONTROL Sources]**&#x200B;區段可讓您建立、更新和刪除來源連線，讓您將外部來源的資料內嵌至Platform。 有關源的更多資訊，請參見[sources overview](../sources/home.md)。

**[!UICONTROL 目標]**&#x200B;區段可讓您建立、更新和刪除目標，以便將資料從Platform匯出至許多外部目標。 有關目的地的詳細資訊，請參閱[目的地概述](../destinations/home.md)。

### [!UICONTROL 客戶]

**[!UICONTROL 設定檔]**&#x200B;區段可讓您瀏覽客戶設定檔、檢視設定檔量度、建立和管理合併原則，以及檢視聯合結構。 若要進一步了解如何使用[!UICONTROL Profiles]區段，請參閱[[!DNL Profile] 使用手冊](../profile/ui/user-guide.md)。 有關「即時客戶設定檔」的詳細資訊，請參閱[「即時客戶設定檔概述」](../profile/home.md)。

**[!UICONTROL 區段]**&#x200B;區段可讓您建立和管理區段定義。 若要進一步了解如何使用[!UICONTROL 區段]區段，請參閱[區段使用手冊](../segmentation/ui/overview.md)。 如需分段服務的詳細資訊，請參閱[分段服務概述](../segmentation/home.md)。

**[!UICONTROL 身分]**&#x200B;區段可讓您建立和管理身分識別命名空間。 如需[!UICONTROL 身分]區段的詳細資訊，包括有關身分識別命名空間以及如何在Platform UI中使用身分識別的資訊，請參閱[身分識別命名空間概述](../identity-service/namespaces.md)。

### [!UICONTROL 隱私]

**[!UICONTROL Policies]**&#x200B;區段可讓您建立和管理資料使用策略。 要了解有關使用「策略」部分的詳細資訊，請閱讀[資料使用策略使用手冊](../data-governance/policies/user-guide.md)。 有關資料使用策略的詳細資訊，請參閱[資料使用策略概述](../data-governance/policies/overview.md)。

**[!UICONTROL Requests]**&#x200B;區段可讓您建立和管理隱私權要求。 請注意，您必須允許列出，才能存取Privacy ServiceUI。 若要進一步了解如何使用「要求」區段，請參閱[Privacy Service使用手冊](../privacy-service/ui/user-guide.md)。 有關Privacy Service的詳細資訊，請參閱[Privacy Service概述](../privacy-service/home.md)。

### [!UICONTROL 資料科學]

**[!UICONTROL Notebooks]**&#x200B;部分提供對JupyterLab的訪問，JupyterLab是一種互動式開發環境，允許您探索、分析和建模資料。 要了解有關使用「筆記本」部分的詳細資訊，請閱讀[JupyterLab使用手冊](../data-science-workspace/jupyterlab/overview.md)。 有關Data Science Workspace的詳細資訊，請參閱[Data Science Workspace overview](../data-science-workspace/home.md)

**[!UICONTROL 模型]**&#x200B;區段可讓您運用機器學習和人工智慧來建立、開發、訓練和調整模型以進行預測。 有關「模型」部分的詳細資訊，請參閱[培訓和評估模型](../data-science-workspace/models-recipes/train-evaluate-model-ui.md)的教程。

**[!UICONTROL 服務]**&#x200B;區段可讓您管理已發佈的模型以進行排程訓練和計分，或運用Adobe的智慧型服務，這是一組AI服務，可提供即時的個人化客戶體驗。 有關「服務」部分的詳細資訊，請參閱[ Publishing a Model as a Service教程](../data-science-workspace/models-recipes/publish-model-service-ui.md)。

### [!UICONTROL 資料管理]

**[!UICONTROL 結構]**&#x200B;區段可讓您建立和管理Experience Data Model(XDM)結構。 若要進一步了解結構，請閱讀有關[建立結構](../xdm/tutorials/create-schema-ui.md)的教學課程。 有關XDM的詳細資訊，請參閱[XDM系統概述](../xdm/home.md)。

**[!UICONTROL 資料集]**&#x200B;區段可讓您建立和管理資料集。 如需資料集的詳細資訊，請參閱[資料集使用指南](../catalog/datasets/user-guide.md)。

**[!UICONTROL 查詢]**&#x200B;區段可讓您建立和管理查詢、記錄Adobe Experience Platform Query Service提出的SQL查詢，以及檢視您的PostgreSQL憑證。 有關查詢的詳細資訊，請參閱[查詢服務使用手冊](../query-service/ui/overview.md)。

**[!UICONTROL 監控]**&#x200B;區段可讓您監控批次和串流內嵌。 有關監視的更多資訊，請參閱[監視資料獲取使用手冊](../ingestion/quality/monitor-data-ingestion.md)。

### [!UICONTROL 決策]

Offer Decisioning 是一項與 Adobe Experience Platform 整合的應用程式服務。 它可讓您運用 Experience Platform，在適當的時間跨所有接觸點為客戶提供最佳的優惠和體驗。若要進一步了解Offer decisioning，包括使用[!UICONTROL Offers]和[!UICONTROL Activities]，請造訪[Offer decisioning檔案](https://experienceleague.adobe.com/docs/offer-decisioning.html)。

### [!UICONTROL 管理]

Platform使用者介面(UI)提供控制面板，您可透過控制面板檢視有關組織授權使用情況的重要資訊，如每日快照中所擷取。 您可以在導覽中選取&#x200B;**[!UICONTROL 授權使用]**&#x200B;來存取此項。 若要進一步了解授權使用控制面板，請造訪[授權使用控制面板指南](license-usage-dashboard.md)。

>[!IMPORTANT]
>
>授權使用控制面板功能目前位於Alpha版，並非所有使用者皆可使用。 文件和功能可能會有所變更。

## 後續步驟

閱讀本指南後，您現在已熟悉Platform UI的首頁和主要導覽元素。 如需使用者介面的詳細資訊，請參閱各個別Platform服務的檔案。 本檔案的連結位於本檔案前面找到的[左側導覽](#left-nav)區段中。
