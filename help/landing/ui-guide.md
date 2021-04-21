---
keywords: Experience Platform; home；熱門主題；Adobe Experience Platform；使用手冊；ui指南；平台ui指南；平台簡介；儀表板；
solution: Experience Platform
title: Experience PlatformUI概觀
topic-legacy: ui guide
description: Adobe Experience Platform
exl-id: 47f9a3fb-731d-4ade-8069-faaa18f224dc
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1695'
ht-degree: 3%

---

# Adobe Experience PlatformUI指南

本指南是使用Adobe Experience Platform用戶介面(UI)的介紹，說明各種元件的用途，並提供指向進一步文檔的連結以瞭解詳細資訊。

若要進一步瞭解Adobe Experience Platform，請閱讀[Experience Platform概觀](home.md)。

## 首頁畫面

登入Adobe Experience Platform後，您位於[!UICONTROL Home]頁面，該頁面由[度量儀表板](#metrics)、[最新資料](#recent-data)和[建議學習](#recommended-learning)區段組成。

![](images/user-guide/homepage.png)

### 量度

量度控制面板提供卡片，可提供您組織內資料集、設定檔、區段和目的地的相關資訊。

![](images/user-guide/homepage-dashboard.png)

**[!UICONTROL Datasets]**&#x200B;區段顯示IMS組織內的資料集數目。 建立新資料集時會更新此數字。 有關資料集的詳細資訊，請參閱[資料集概述](../catalog/datasets/overview.md)。

**[!UICONTROL Profiles]**&#x200B;區段顯示IMS組織內具有設定檔的總人數，不包括設定檔片段。 這個總人數代表可定址的觀眾總數，每24小時更新一次。 有關配置檔案的詳細資訊，請參閱[即時客戶配置檔案概述](../profile/home.md)。

**[!UICONTROL Segments]**&#x200B;區段顯示在IMS組織內建立的區段總數。 建立新區段時，會更新此數字。 有關區段的詳細資訊，請參閱[區段服務概述](../segmentation/home.md)。

**[!UICONTROL Destinations]**&#x200B;區段顯示為IMS組織建立的目標總數。 當建立新目標時，此數字會更新。 有關目標的詳細資訊，請參閱[目標概述](../destinations/home.md)。

### 最近的資料

最近的資料控制面板提供有關最近建立的資料集、來源、區段和目的地的資訊。

![](images/user-guide/homepage-recent.png)

**[!UICONTROL Recent datasets]**&#x200B;區段會列出您IMS組織中最近建立的五個資料集。 每次建立新資料集時都會更新此清單。 您可以從清單中選擇資料集以查看有關指定資料集的更多資訊，或選擇&#x200B;**[!UICONTROL View all]**&#x200B;以查看所有已建立資料集的清單。 有關資料集的詳細資訊，請參閱[資料集概述](../catalog/datasets/overview.md)。

**[!UICONTROL Recent sources]**&#x200B;區段會列出您IMS組織中最近建立的五個來源連接器。 每次建立新源連接器時都會更新此清單。 您可以從清單中選擇源連接以查看有關指定連接器的更多資訊，或選擇&#x200B;**[!UICONTROL View all]**&#x200B;查看所有已建立源連接的清單。 有關來源的更多資訊，請參閱[來源概觀](../sources/home.md)。

**[!UICONTROL Recent segments]**&#x200B;區段會列出您IMS組織中最近建立的五個區段定義。 每次建立新區段定義時，都會更新此清單。 您可以從清單中選取區段定義，以檢視有關指定區段定義的詳細資訊，或選取&#x200B;**[!UICONTROL View all]**&#x200B;以檢視所有已建立區段定義的清單。 有關區段的詳細資訊，請參閱[區段服務概述](../segmentation/home.md)。

**[!UICONTROL Recent destinations]**&#x200B;區段會列出您IMS組織中最近建立的五個目標。 每次建立新目標時，都會更新此清單。 您可以從清單中選擇一個目標以查看有關指定目標的更多資訊，或選擇&#x200B;**[!UICONTROL View all]**&#x200B;以查看所有已建立目標的清單。 有關目標的詳細資訊，請參閱[目標概述](../destinations/home.md)。

### 建議的學習

**[!UICONTROL Recommended learning]**&#x200B;一節提供了有關有用文檔的連結，以便開始使用Adobe Experience Platform。

![](images/user-guide/homepage-recommended.png)

## 頂端導覽列

平台UI中的頂端導覽列會顯示您目前登入的IMS組織，並提供數個重要的控制項。

導覽列的左側是Adobe Experience Platform標誌。 您隨時選取此選項，將會回到Platform UI首頁畫面。

![](./images/user-guide/homepage-top-nav-bar.png)

### IMS組織切換器

頂端導覽列右側的第一個項目是&#x200B;**IMS組織切換器**。

![](./images/user-guide/homepage-ims-org.png)

選取切換器會開啟您可存取的IMS組織（如果有的話）下拉式選單。 選取列出的選項，以切換至該IMS組織。

![](./images/user-guide/homepage-ims-org-switcher.png)

### 交換機應用程式

頂端導覽右側的下一個項目是&#x200B;**應用程式切換器**，由![應用程式切換器](./images/user-guide/app-switcher-icon.png)圖示表示。 當您選取此圖示時，可以在IMS組織可存取的Adobe應用程式之間切換，例如Experience Platform、分析、資產和啟動。

### 說明

應用程式切換器右側是&#x200B;**幫助和支援菜單**，該菜單由![問號／幫助](./images/user-guide/help-icon.png)表徵圖表示。 當您選取此圖示時，會出現一個快顯功能表，其中包含數個說明與支援資源。 **[!UICONTROL Help]**&#x200B;標籤顯示您目前所在頁面的相關檔案清單。 **[!UICONTROL Support]**&#x200B;頁籤允許您與Adobe支援團隊建立支援票證。 **[!UICONTROL Feedback]**&#x200B;標籤可讓您將有關平台的意見回饋提交給Adobe。

![](images/user-guide/homepage-help-clicked.png)

### 通知與公告

在&#x200B;**通知部分**&#x200B;中，![bell/Notifications and Announcements](images/user-guide/notification-icon.png)表徵圖表示。 **[!UICONTROL Notifications]**&#x200B;標籤顯示有關產品和其他相關更新的重要資訊，而&#x200B;**[!UICONTROL Announcements]**&#x200B;標籤顯示有關服務維護的資訊。

### 使用者設定檔

頂端導覽列的最後一個項目是&#x200B;**使用者設定**，由![使用者設定／使用者設定檔](images/user-guide/profile-icon.png)圖示表示。 選取此圖示可編輯您的偏好設定或登出。

### 沙盒

在頂端導覽列的正下方是沙盒列。 此列顯示您目前用於平台的沙盒。 有關沙盒的更多資訊，請參閱[沙盒概述](../sandboxes/home.md)。

## 左側導覽{#left-nav}

畫面左側的導覽列出平台UI中支援的所有不同服務。

>[!IMPORTANT]
>
>左側導覽列上的部分可能未顯示或呈灰色顯示。 這是因為您無權存取這些功能。 如果您認為您應該擁有這些章節的存取權，請連絡您的系統管理員。

![](images/user-guide/homepage-left.png)

**[!UICONTROL Home]**&#x200B;區段可讓您返回平台UI首頁。

**[!UICONTROL Workflows]**&#x200B;區段顯示用於在平台中執行操作的多步驟工作流的清單。 有關工作流程的更多資訊，請參閱[工作流程概述](./workflows.md)。

### [!UICONTROL Connections]

**[!UICONTROL Sources]**&#x200B;區段可讓您建立、更新和刪除來源連線，讓您將外部來源的資料內嵌至平台。 有關來源的更多資訊，請參閱[來源概觀](../sources/home.md)。

**[!UICONTROL Destinations]**&#x200B;區段可讓您建立、更新和刪除目標，讓您將資料從平台匯出至許多外部目標。 有關目標的詳細資訊，請參閱[目標概述](../destinations/home.md)。

### [!UICONTROL Customer]

**[!UICONTROL Profiles]**&#x200B;區段可讓您瀏覽客戶個人檔案、檢視個人檔案度量、建立和管理合併原則，以及檢視合併結構。 若要進一步瞭解如何使用[!UICONTROL Profiles]區段，請閱讀[[!DNL Profile] 使用指南](../profile/ui/user-guide.md)。 有關即時客戶概要資訊的詳細資訊，請參閱[即時客戶概要資訊](../profile/home.md)。

**[!UICONTROL Segments]**&#x200B;區段可讓您建立和管理區段定義。 若要進一步瞭解如何使用[!UICONTROL Segments]區段，請閱讀[區段使用指南](../segmentation/ui/overview.md)。 有關分段服務的詳細資訊，請參閱[分段服務概述](../segmentation/home.md)。

**[!UICONTROL Identities]**&#x200B;區段可讓您建立和管理身分名稱空間。 有關[!UICONTROL Identities]章節的詳細資訊，包括有關身分名稱空間以及如何在平台UI中使用身分的資訊，請參閱[身分名稱空間概述](../identity-service/namespaces.md)。

### [!UICONTROL Privacy]

**[!UICONTROL Policies]**&#x200B;區段可讓您建立和管理資料使用原則。 要瞭解有關使用「策略」部分的更多資訊，請閱讀[資料使用策略使用手冊](../data-governance/policies/user-guide.md)。 有關資料使用策略的詳細資訊，請參閱[資料使用策略概述](../data-governance/policies/overview.md)。

**[!UICONTROL Requests]**&#x200B;區段可讓您建立和管理隱私權要求。 請注意，您必須獲准列出才能存取Privacy ServiceUI。 若要進一步瞭解如何使用「請求」區段，請閱讀[Privacy Service使用指南](../privacy-service/ui/user-guide.md)。 有關Privacy Service的更多資訊，請參閱[Privacy Service概述](../privacy-service/home.md)。

### [!UICONTROL Data Science]

**[!UICONTROL Notebooks]**&#x200B;區段提供對JupyterLab的存取，JupyterLab是互動式開發環境，可讓您探索、分析並建立資料模型。 要瞭解有關使用「Notebooks（筆記型電腦）」部分的更多資訊，請閱讀[JupyterLab使用手冊](../data-science-workspace/jupyterlab/overview.md)。 有關Data Science Workspace的更多資訊，請參閱[Data Science Workspace概觀](../data-science-workspace/home.md)

**[!UICONTROL Models]**&#x200B;區段可讓您運用機器學習和人工智慧來建立、開發、訓練和調整模型以進行預測。 有關「模型」部分的詳細資訊，請參閱[培訓教程，並評估模型](../data-science-workspace/models-recipes/train-evaluate-model-ui.md)。

**[!UICONTROL Services]**&#x200B;區段可讓您管理已發佈的模型，以進行排程的訓練和計分，或運用Adobe的智慧服務，這是一組AI服務，可提供即時、個人化的客戶體驗。 有關「服務」部分的詳細資訊，請參閱[將模型作為服務發佈教程](../data-science-workspace/models-recipes/publish-model-service-ui.md)。

### [!UICONTROL Data management]

**[!UICONTROL Schemas]**&#x200B;區段可讓您建立和管理體驗資料模型(XDM)結構。 要瞭解有關方案的更多資訊，請閱讀有關建立方案[的教程。 ](../xdm/tutorials/create-schema-ui.md)有關XDM的更多資訊，請參見[XDM系統概述](../xdm/home.md)。

**[!UICONTROL Datasets]**&#x200B;區段可讓您建立和管理資料集。 有關資料集的詳細資訊，請參閱[資料集使用手冊](../catalog/datasets/user-guide.md)。

**[!UICONTROL Queries]**&#x200B;部分可讓您建立和管理查詢、記錄Adobe Experience Platform查詢服務進行的SQL查詢，以及查看PostgreSQL憑據。 有關查詢的詳細資訊，請參閱[查詢服務使用手冊](../query-service/ui/overview.md)。

**[!UICONTROL Monitoring]**&#x200B;區段可讓您監控批次和串流擷取。 有關監視的詳細資訊，請參閱[監視資料接收使用手冊](../ingestion/quality/monitor-data-ingestion.md)。

### [!UICONTROL Decisioning]

Offer Decisioning 是一項與 Adobe Experience Platform 整合的應用程式服務。它可讓您運用 Experience Platform，在適當的時間跨所有接觸點為客戶提供最佳的優惠和體驗。若要進一步瞭解Offer decisioning，包括使用[!UICONTROL Offers]和[!UICONTROL Activities]Offer decisioning檔案[，請造訪](https://experienceleague.adobe.com/docs/offer-decisioning.html)。

### [!UICONTROL Administration]

平台使用者介面(UI)提供控制面板，您可透過此控制面板檢視有關貴組織授權使用情況的重要資訊，如每日快照中所擷取。 您可以在導覽中選取&#x200B;**[!UICONTROL License usage]**&#x200B;來存取此項。 若要進一步瞭解授權使用控制面板，請造訪[授權使用控制面板指南](license-usage-dashboard.md)。

>[!IMPORTANT]
>
>授權使用資料板功能目前為alpha版，並非所有使用者都能使用。 文件和功能可能會有所變更。

## 後續步驟

閱讀本指南後，您現在已介紹到Platform UI的首頁和主要導覽元素。 有關使用者介面的詳細資訊，請參閱各項個別平台服務的檔案。 本檔案的連結位於本檔案前面的[左導覽](#left-nav)區段。
