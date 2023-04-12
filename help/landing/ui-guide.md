---
keywords: Experience Platform；首頁；熱門主題；Adobe Experience Platform；使用手冊；ui指南；平台ui指南；平台簡介；控制面板；
solution: Experience Platform
title: Experience PlatformUI概述
description: Adobe Experience Platform
exl-id: 47f9a3fb-731d-4ade-8069-faaa18f224dc
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1797'
ht-degree: 2%

---

# Adobe Experience Platform UI指南

本指南提供使用Adobe Experience Platform使用者介面(UI)的簡介，說明各種元件的用途，並提供進一步說明檔案的連結以取得詳細資訊。

若要進一步了解Adobe Experience Platform，請閱讀 [Experience Platform概述](home.md).

## 主畫面

登入Adobe Experience Platform後，您在 [!UICONTROL 首頁] 頁面，由 [量度控制面板](#metrics), [近期資料](#recent-data)，和 [建議學習](#recommended-learning) 區段。

![](images/user-guide/homepage.png)

### 量度

量度控制面板提供卡片，提供貴組織內資料集、設定檔、區段和目的地的相關資訊。

![](images/user-guide/homepage-dashboard.png)

此 **[!UICONTROL 資料集]** 區段顯示組織內的資料集數量。 建立新資料集時，會更新此數字。 如需資料集的詳細資訊，請參閱 [資料集概述](../catalog/datasets/overview.md).

此 **[!UICONTROL 設定檔]** 區段顯示組織內具有設定檔的人員總數，不包括設定檔片段。 此總人數代表可定址的受眾總數，每24小時更新一次。 如需設定檔的詳細資訊，請參閱 [即時客戶個人檔案概觀](../profile/home.md).

此 **[!UICONTROL 區段]** 區段會顯示在您的組織內建立的區段總數。 建立新區段時，會更新此數字。 如需區段的詳細資訊，請參閱 [區段服務概觀](../segmentation/home.md).

此 **[!UICONTROL 目的地]** 區段顯示為組織建立的目的地總數。 建立新目的地時，會更新此數字。 如需目的地的詳細資訊，請參閱 [目的地概述](../destinations/home.md).

### 近期資料

最近使用的資料控制面板提供最近建立的資料集、來源、區段和目的地的相關資訊。

![](images/user-guide/homepage-recent.png)

此 **[!UICONTROL 最近的資料集]** 區段列出貴組織內最近建立的五個資料集。 每次建立新資料集時，都會更新此清單。 您可以從清單中選取資料集，以檢視指定資料集的詳細資訊，或選取 **[!UICONTROL 查看全部]** ，查看所有已建立資料集的清單。 如需資料集的詳細資訊，請參閱 [資料集概述](../catalog/datasets/overview.md).

此 **[!UICONTROL 最近的來源]** 小節列出貴組織內最近建立的五個來源連接器。 每次建立新源連接器時，都會更新此清單。 您可以從清單中選擇源連接，以查看有關指定連接器的更多資訊，或選擇 **[!UICONTROL 查看全部]** 查看所有已建立源連接的清單。 有關來源的詳細資訊，請參閱 [來源概觀](../sources/home.md).

此 **[!UICONTROL 最近區段]** 一節列出貴組織內最近建立的五個區段定義。 每次建立新區段定義時，就會更新此清單。 您可以從清單中選取區段定義，以檢視有關指定區段定義的詳細資訊，或選取 **[!UICONTROL 查看全部]** ，查看所有已建立區段定義的清單。 如需區段的詳細資訊，請參閱 [區段服務概觀](../segmentation/home.md).

此 **[!UICONTROL 近期目的地]** 區段列出貴組織內最近建立的五個目的地。 每次建立新目的地時，都會更新此清單。 您可以從清單中選取目的地，以檢視有關指定目的地的詳細資訊或選取 **[!UICONTROL 查看全部]** ，查看所有已建立目的地的清單。 如需目的地的詳細資訊，請參閱 [目的地概述](../destinations/home.md).

### 建議的學習

此 **[!UICONTROL 建議的學習]** 一節提供開始使用Adobe Experience Platform的實用檔案連結。

![](images/user-guide/homepage-recommended.png)

## 頂端導覽列

Platform UI的頂端導覽列會顯示您目前登入的組織，並提供數個重要的控制項。

導覽列的左側是Adobe Experience Platform標誌。 您隨時可以選取此標誌，回到Platform UI主畫面。

![](./images/user-guide/homepage-top-nav-bar.png)

### 組織切換器

頂端導覽列右側的第一個項目是 **組織切換器**.

![](./images/user-guide/homepage-ims-org-switcher.png)

選取切換器會開啟您可存取之組織的下拉式功能表（如果有的話）。 若要切換至其他組織，請選取列出的選項。

### 交換應用程式

頂端導覽右側的下一個項目是 **應用程式切換器**，以 ![應用程式切換器](./images/user-guide/app-switcher-icon.png) 表徵圖。 選取此圖示時，您可以在貴組織有權存取的Adobe應用程式之間切換，例如Experience Platform、Analytics、資產等。

### 說明

應用程式切換器的右側是 **說明與支援功能表**，以 ![問號/說明](./images/user-guide/help-icon.png) 表徵圖。 選取此圖示時，彈出式功能表隨即出現，其中包含數個說明和支援資源。 此 **[!UICONTROL 說明]** 索引標籤會顯示您目前所在頁面的相關檔案清單。 此 **[!UICONTROL 支援]** 頁簽可讓您與Adobe支援團隊建立支援票證。 此 **[!UICONTROL 意見反應]** 標籤，即可將Platform的意見提交至Adobe。

![](images/user-guide/homepage-help-clicked.png)

### 通知和公告

在 **通知區段**，以 ![鈴聲/通知和公告](images/user-guide/notification-icon.png) 表徵圖。 此 **[!UICONTROL 通知]** 索引標籤會顯示產品和其他相關更新的重要資訊，而 **[!UICONTROL 公告]** 頁簽顯示有關服務維護的資訊。

### 使用者設定檔

頂端導覽列的最終項目為 **使用者設定**，以 ![用戶設定/用戶配置檔案](images/user-guide/profile-icon.png) 表徵圖。 選取此圖示即可編輯您的偏好設定或登出。

您可以切換Platform介面的明暗主題，且開關位於您的名稱和電子郵件正下方。 選擇您喜歡的主題。

![](images/theme.png)

### 沙箱

沙箱列就位於頂端導覽列的正下方。 此列顯示您目前用於Platform的沙箱。 如需沙箱的詳細資訊，請參閱 [沙箱概述](../sandboxes/home.md).

## 左側導覽 {#left-nav}

畫面左側的導覽列出Platform UI支援的所有不同服務。

按一下功能表圖示來顯示或隱藏左側導覽面板。

![](images/user-guide/hidemenu.png)

您可以在顯示面板後再按一下，將導覽鎖定在開啟的位置。

>[!IMPORTANT]
>
>左側導覽列只顯示您可存取的功能。 在舊版Adobe Experience Platform中，無法使用的項目已停用。 如果您認為應該可以存取未顯示的區段，請聯絡您的系統管理員。

![](images/user-guide/homepage-left.png)

此 **[!UICONTROL 首頁]** 區段可讓您返回Platform UI首頁。

此 **[!UICONTROL 工作流程]** 區段顯示在Platform中執行作業的多步驟工作流程清單。 如需工作流程的詳細資訊，請參閱 [工作流程概觀](./workflows.md).

### [!UICONTROL 連線]

此 **[!UICONTROL 來源]** 區段可讓您建立、更新和刪除來源連線，讓您將外部來源的資料內嵌至Platform。 有關來源的詳細資訊，請參閱 [來源概觀](../sources/home.md).

此 **[!UICONTROL 目的地]** 區段可讓您建立、更新和刪除目的地，以便將資料從Platform匯出至許多外部目的地。 如需目的地的詳細資訊，請參閱 [目的地概述](../destinations/home.md).

### [!UICONTROL 客戶]

此 **[!UICONTROL 設定檔]** 區段可讓您瀏覽客戶設定檔、檢視設定檔量度、建立和管理合併原則，以及檢視聯合結構。 若要進一步了解如何使用 [!UICONTROL 設定檔] 部分，請閱讀 [[!DNL Profile] 使用手冊](../profile/ui/user-guide.md). 如需即時客戶個人檔案的詳細資訊，請參閱 [即時客戶個人檔案概觀](../profile/home.md).

此 **[!UICONTROL 區段]** 區段可讓您建立和管理區段定義。 若要進一步了解如何使用 [!UICONTROL 區段] 部分，請閱讀 [細分使用手冊](../segmentation/ui/overview.md). 如需分段服務的詳細資訊，請參閱 [區段服務概觀](../segmentation/home.md).

此 **[!UICONTROL 身分]** 區段可讓您建立和管理身分識別命名空間。 如需 [!UICONTROL 身分] 一節，包括有關身分識別命名空間以及如何在Platform UI中使用身分識別的資訊，請參閱 [身分命名空間概述](../identity-service/namespaces.md).

### [!UICONTROL 隱私]

此 **[!UICONTROL 原則]** 區段可讓您建立和管理資料使用原則。 若要進一步了解如何使用「原則」區段，請閱讀 [資料使用原則使用指南](../data-governance/policies/user-guide.md). 如需資料使用原則的詳細資訊，請參閱 [資料使用原則概觀](../data-governance/policies/overview.md).

此 **[!UICONTROL 請求]** 區段可讓您建立及管理隱私權要求。 請注意，您必須允許列出，才能存取Privacy ServiceUI。 若要進一步了解如何使用「要求」區段，請閱讀 [Privacy Service使用手冊](../privacy-service/ui/user-guide.md). 如需Privacy Service的詳細資訊，請參閱 [Privacy Service概述](../privacy-service/home.md).

### [!UICONTROL 資料科學]

此 **[!UICONTROL 筆記本]** 小節提供對JupyterLab的存取，此互動式開發環境可讓您探索、分析和建模您的資料。 要了解有關使用筆記本部分的詳細資訊，請閱讀 [JupyterLab使用手冊](../data-science-workspace/jupyterlab/overview.md). 如需Data Science Workspace的詳細資訊，請參閱 [Data Science Workspace概觀](../data-science-workspace/home.md)

此 **[!UICONTROL 模型]** 區段可讓您使用機器學習和人工智慧來建立、開發、訓練和調整模型以進行預測。 有關「模型」區段的詳細資訊，請參閱 [訓練和評估模型](../data-science-workspace/models-recipes/train-evaluate-model-ui.md).

此 **[!UICONTROL 服務]** 區段可讓您管理已發佈的模型以進行排程訓練和計分，或使用Adobe的智慧型服務（一組AI服務，可提供即時、個人化的客戶體驗）。 有關「服務」章節的詳細資訊，請參閱 [發佈Model as a Service教學課程](../data-science-workspace/models-recipes/publish-model-service-ui.md).

### [!UICONTROL 資料管理]

此 **[!UICONTROL 結構]** 區段可讓您建立和管理Experience Data Model(XDM)結構。 若要進一步了解結構，請參閱 [建立架構](../xdm/tutorials/create-schema-ui.md). 如需XDM的詳細資訊，請參閱 [XDM系統概觀](../xdm/home.md).

此 **[!UICONTROL 資料集]** 區段可讓您建立和管理資料集。 如需資料集的詳細資訊，請參閱 [資料集使用指南](../catalog/datasets/user-guide.md).

此 **[!UICONTROL 查詢]** 區段可讓您建立和管理查詢、記錄Adobe Experience Platform Query Service提出的SQL查詢，以及檢視您的 [!DNL PostgreSQL] 憑證。 有關查詢的詳細資訊，請參閱 [查詢服務使用手冊](../query-service/ui/overview.md).

此 **[!UICONTROL 監控]** 區段可讓您監控批次和串流內嵌。 有關監視的詳細資訊，請參閱 [監控資料匯入使用手冊](../ingestion/quality/monitor-data-ingestion.md).

### [!UICONTROL 決策]

Adobe Journey Optimizer是以Experience Platform為基礎打造的應用程式服務。 它可讓您使用功能強大的決策技術，在適當的時間跨所有接觸點為客戶提供最佳的選件和體驗。 深入了解Journey Optimizer，包括使用 [!UICONTROL 選件] 和 [!UICONTROL 活動] 造訪 [Journey Optimizer檔案](https://experienceleague.adobe.com/docs/journey-optimizer.html?lang=zh-Hant).

### [!UICONTROL 管理]

Platform使用者介面(UI)提供控制面板，您可透過控制面板檢視有關組織授權使用情況的重要資訊，如每日快照中所擷取。 透過選取 **[!UICONTROL 授權使用]** 的子母體。 若要進一步了解授權使用控制面板，請造訪 [授權使用控制面板指南](./license-usage-and-guardrails/license-usage-dashboard.md).

>[!IMPORTANT]
>
>授權使用控制面板功能目前位於Alpha版，並非所有使用者皆可使用。 文件和功能可能會有所變更。

## 後續步驟

閱讀本指南後，您現在已熟悉Platform UI的首頁和主要導覽元素。 如需使用者介面的詳細資訊，請參閱各個別Platform服務的檔案。 本檔案的連結位於 [左側導覽](#left-nav) 部分。
