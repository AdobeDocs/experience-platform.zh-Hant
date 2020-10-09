---
keywords: Experience Platform;home;popular topics;Adobe Experience Platform;user guide;ui guide;platform ui guide;introduction to platform;dashboard;
solution: Experience Platform
title: Adobe Experience Platform UI指南
topic: ui guide
description: 'Adobe Experience Platform '
translation-type: tm+mt
source-git-commit: 84f1f840e15cb4487807c13131d0787772fa063a
workflow-type: tm+mt
source-wordcount: '1586'
ht-degree: 0%

---


# Adobe Experience Platform UI指南

本指南是使用Adobe Experience Platform使用者介面(UI)的簡介，說明各種元件的用途，並提供進一步說明檔案的連結，以取得詳細資訊。

若要進一步瞭解Adobe Experience Platform，請閱讀「 [Experience Platform」總覽](./home.md)。

## 首頁畫面

登入Adobe Experience Platform後，您將進入首頁，首頁包含量度儀表板、最近的資料和建議的學習區段。 

![](images/user-guide/homepage.png)

### 量度控制面板

量度控制面板提供卡片，可提供您組織內資料集、設定檔、區段和目的地的相關資訊。

![](images/user-guide/homepage-dashboard.png)

「資 **[!UICONTROL 料集]** 」區段顯示IMS組織內的資料集數目。 建立新資料集時會更新此數字。 有關資料集的詳細資訊，請參 [閱資料集概述](../catalog/datasets/overview.md)。

「設 **[!UICONTROL 定檔]** 」區段顯示IMS組織內具有設定檔的總人數，不包括設定檔片段。 這個總人數代表可定址的觀眾總數，每24小時更新一次。 如需有關個人檔案的詳細資訊，請參 [閱即時客戶個人檔案總覽](../profile/home.md)。

「區 **[!UICONTROL 段]** 」區段會顯示在IMS組織內建立的區段總數。 建立新區段時，會更新此數字。 有關區段的詳細資訊，請參閱區段 [服務概觀](../segmentation/home.md)。

「目 **[!UICONTROL 標]** 」區段顯示為IMS組織建立的目標總數。 當建立新目標時，此數字會更新。 有關目標的詳細資訊，請參閱目 [標概述](../rtcdp/destinations/destinations-overview.md)。

### 最近的資料

最近的資料控制面板提供有關最近建立的資料集、來源、區段和目的地的資訊。

![](images/user-guide/homepage-recent.png)

「最 **[!UICONTROL 近的資料集]** 」區段會列出您IMS組織中最近建立的五個資料集。 每次建立新資料集時都會更新此清單。 您可以從清單中選擇一個資料集來查看有關指定資料集的更多資訊，或選擇「 **[!UICONTROL View all]** 」（查看所有建立的資料集）。 有關資料集的詳細資訊，請參 [閱資料集概述](../catalog/datasets/overview.md)。

「最 **[!UICONTROL 近來源]** 」區段會列出您IMS組織中最近建立的五個來源連接器。 每次建立新源連接器時都會更新此清單。 您可以從清單中選擇源連接以查看有關指定連接器的詳細資訊，或選擇 **[!UICONTROL View all]** （查看全部）查看所有已建立源連接的清單。 有關來源的詳細資訊，請參閱來 [源概述](../sources/home.md)。

「最 **[!UICONTROL 近的區段]** 」區段會列出您IMS組織中最近建立的五個區段定義。 每次建立新區段定義時，都會更新此清單。 您可以從清單中選取區段定義，以檢視指定區段定義的詳細資訊，或選取「全部檢視 **** 」，以檢視所有已建立區段定義的清單。 有關區段的詳細資訊，請參閱區段 [服務概觀](../segmentation/home.md)。

「最 **[!UICONTROL 近目標]** 」區段會列出您IMS組織中最近建立的五個目標。 每次建立新目標時，都會更新此清單。 您可以從清單中選擇一個目標來查看有關指定目標的詳細資訊，或選擇「全部查看 **** 」以查看所有已建立目標的清單。 有關目標的詳細資訊，請參閱目 [標概述](../rtcdp/destinations/destinations-overview.md)。

### 建議的學習

「建 **[!UICONTROL 議的學習]** 」區段提供實用檔案的連結，以開始使用Adobe Experience Platform。

![](images/user-guide/homepage-recommended.png)

## 頂端導覽列

平台UI中的頂端導覽列會顯示您目前登入的IMS組織，並提供數個重要的控制項。

導覽列的左側是Adobe Experience Platform標誌。 選取此選項會將您帶回「平台UI」首頁畫面。

![](./images/user-guide/homepage-top-nav-bar.png)

### IMS組織切換器

導覽列右側的第一個項目是 **IMS組織切換器**。

![](./images/user-guide/homepage-ims-org.png)

選取切換器會開啟您可存取的IMS組織（如果有的話）下拉式選單。 選取列出的選項，以切換至該IMS組織。

![](./images/user-guide/homepage-ims-org-switcher.png)

### 交換機應用程式

右邊的下一個項目是應用程式 **切換器**，由應用程式 ![切換器圖示表示](./images/user-guide/app-switcher-icon.png) 。 當您選取此圖示時，可以在Experience Platform、Assets、Exchange和Launch之間切換。

### 說明

應用程式切換器的右側是說 **明與支援功能表**，以問號／說 ![明圖示表示](./images/user-guide/help-icon.png) 。 當您選取此圖示時，會出現一個快顯功能表，其中包含數個說明與支援資源。 「說 **[!UICONTROL 明]** 」標籤會顯示您目前所在頁面的相關檔案清單。 「支 **[!UICONTROL 援]** 」標籤可讓您與Adobe支援團隊建立支援票證。 「意 **[!UICONTROL 見回饋]** 」標籤可讓您將有關平台的意見回饋提交給Adobe。

![](images/user-guide/homepage-help-clicked.png)

### 通知與公告

在說明與支援功能表後， **會顯示通知區**，此區 ![段由鐘聲／通知與公告圖示表示](images/user-guide/notification-icon.png) 。 「通 **[!UICONTROL 知]** 」標籤顯示有關產品和其他相關更新的重要資訊，而「公告」標籤則 **** 顯示有關服務維護的通知。

### 使用者設定檔

頂端導覽列的最後一個項目是使 **用者設定**，由使用者設定／使 ![用者設定檔圖示表示](images/user-guide/profile-icon.png) 。 選取此圖示可編輯您的偏好設定或登出。

### 沙箱

在頂端導覽列的正下方是沙盒列。 此列顯示您目前用於平台的沙盒。 有關沙盒的詳細資訊，請參閱沙盒 [概觀](../sandboxes/home.md)。

## 左側導覽 {#left-nav}

畫面左側的導覽列出平台UI中支援的所有不同服務。

>[!IMPORTANT]
>
>左側導覽列上的部分可能未顯示或呈灰色顯示。 這是因為您沒有這些功能的存取權。 如果您認為您應該擁有這些章節的存取權，請連絡您的系統管理員。

![](images/user-guide/homepage-left.png)

「首 **[!UICONTROL 頁]** 」區段可讓您返回平台UI首頁。

「工 **[!UICONTROL 作流程]** 」區段顯示在「平台」中執行操作的多步驟工作流程清單。

### [!UICONTROL 連線]

「 **[!UICONTROL 來源]** 」區段可讓您建立、更新和刪除來源連線，讓您將外部來源的資料擷取至平台。 有關來源的詳細資訊，請參閱來 [源概述](../sources/home.md)。

「目 **[!UICONTROL 標]** 」區段可讓您建立、更新和刪除目標，讓您將資料從平台匯出至許多外部目標。 有關目標的詳細資訊，請參閱目 [標概述](../rtcdp/destinations/destinations-overview.md)。

### [!UICONTROL 客戶]

「描 **[!UICONTROL 述檔]** 」區段可讓您瀏覽客戶描述檔、檢視描述檔度量、建立和管理合併原則，以及檢視結合結構。 若要進一步瞭解如何使用 [!UICONTROL Profiles] ，請閱讀使 [[!DNL Profile] 用指南](../profile/ui/user-guide.md)。 有關「即時客戶基本資料」的詳細資訊，請參閱「即 [時客戶基本資料」總覽](../profile/home.md)。

「區 **[!UICONTROL 段]** 」區段可讓您建立和管理區段定義。 若要進一步瞭解如何使用 [!UICONTROL 區段] ，請閱讀區 [段使用指南](../segmentation/ui/overview.md)。 如需區段服務的詳細資訊，請參閱區段服 [務概觀](../segmentation/home.md)。

「身 **[!UICONTROL 分識別]** 」區段可讓您建立和管理身分識別名稱空間。 如需有關「身分 [!UICONTROL 識別] 」區段的詳細資訊，包括有關身分識別名稱空間以及如何在平台UI中使用身分識別的資訊，請參閱 [身分識別名稱空間總覽](../identity-service/namespaces.md)。

### [!UICONTROL 隱私]

「原 **[!UICONTROL 則]** 」區段可讓您建立和管理資料使用原則。 若要進一步瞭解如何使用「原則」區段，請閱讀資 [料使用原則使用指南](../data-governance/policies/user-guide.md)。 有關資料使用原則的詳細資訊，請參閱資 [料使用原則概觀](../data-governance/policies/overview.md)。

「請 **[!UICONTROL 求]** 」區段可讓您建立和管理隱私權請求。 請注意，您必須獲准列出才能存取隱私權服務UI。 若要進一步瞭解如何使用「請求」區段，請閱讀「隱私 [服務」使用指南](../privacy-service/ui/user-guide.md)。 如需隱私權服務的詳細資訊，請參閱隱私權 [服務概觀](../privacy-service/home.md)。

### [!UICONTROL 資料科學]

Notebooks **[!UICONTROL 部分]** (Notebooks)提供對JupyterLab的訪問，JupyterLab是一種互動式開發環境，可讓您探索、分析並建立資料模型。 要瞭解有關使用「Notebooks（筆記本）」部分的更多資訊，請閱讀 [JupyterLab使用手冊](../data-science-workspace/jupyterlab/overview.md)。 有關Data Science Workspace的詳細資訊，請參閱 [Data Science Workspace總覽](../data-science-workspace/home.md)

「模 **[!UICONTROL 型]** 」區段可讓您運用機器學習和人工智慧來建立、開發、訓練和調整模型以進行預測。 有關「模型」(Models)部分的更多資訊，請參閱培訓與評 [估模型的教學課程](../data-science-workspace/models-recipes/train-evaluate-model-ui.md)。

「服 **[!UICONTROL 務]** 」區段可讓您管理已發佈的模型，以進行排程的訓練和計分，或運用Adobe的智慧服務，這是一套AI服務，可提供即時、個人化的客戶體驗。 有關「服務」區段的詳細資訊，請參閱「將模型 [發佈為服務」教學課程](../data-science-workspace/models-recipes/publish-model-service-ui.md)。

### [!UICONTROL 資料管理]

「方 **[!UICONTROL 案]** 」區段可讓您建立和管理方案。 要進一步瞭解如何使用「結構描述」部分，請閱讀有關建立結構描述 [的教程](../xdm/tutorials/create-schema-ui.md)。 有關Experience Data Model(XDM)的更多資訊，請參閱 [XDM概觀](../xdm/home.md)。

「資 **[!UICONTROL 料集]** 」區段可讓您建立和管理資料集。 有關「資料集」部分的詳細資訊，請參閱資料集 [使用手冊](../catalog/datasets/user-guide.md)。

「查 **[!UICONTROL 詢]** 」部分可讓您建立和管理查詢、記錄查詢服務進行的SQL查詢，以及查看PostgreSQL憑據。 有關「查詢」部分的詳細資訊，請參閱「查 [詢服務」使用手冊](../query-service/ui/overview.md)。

「監 **[!UICONTROL 控]** 」區段可讓您監控批次和串流擷取。 有關「監視」部分的詳細資訊，請參閱監 [視資料提取使用手冊](../ingestion/quality/monitor-data-flows.md)。

## 後續步驟

閱讀本指南後，您現在已介紹到Platform UI的首頁和主要導覽元素。 有關使用者介面的詳細資訊，請參閱各項個別平台服務的檔案。 本檔案的連結會提供於本文 [件稍早的左側導覽](#left-nav) 區段中。