---
keywords: Experience Platform；主題；熱門主題；Adobe Experience Platform；使用手冊；使用手冊；平台使用手冊；平台使用手冊；平台簡介；
solution: Experience Platform
title: Experience PlatformUI概述
description: Adobe Experience Platform
exl-id: 47f9a3fb-731d-4ade-8069-faaa18f224dc
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1797'
ht-degree: 2%

---

# Adobe Experience PlatformUI指南

本指南是使用Adobe Experience Platform用戶介面(UI)的簡介，說明了各種元件的用途，並提供了指向進一步文檔的連結以瞭解更多資訊。

要瞭解有關Adobe Experience Platform的更多資訊，請閱讀 [Experience Platform概述](home.md)。

## 主螢幕

登錄Adobe Experience Platform後，你 [!UICONTROL 首頁] 頁面，由 [指標儀表板](#metrics)。 [近期資料](#recent-data), [建議學習](#recommended-learning) 的下界。

![](images/user-guide/homepage.png)

### 量度

度量儀表板提供卡，用於提供有關組織內資料集、配置檔案、段和目標的資訊。

![](images/user-guide/homepage-dashboard.png)

的 **[!UICONTROL 資料集]** 部分顯示組織內的資料集數。 建立新資料集時將更新此數字。 有關資料集的詳細資訊，請參閱 [資料集概述](../catalog/datasets/overview.md)。

的 **[!UICONTROL 配置檔案]** 部分顯示組織內具有配置檔案的人員總數（不包括配置檔案片段）。 這一總人數代表總可定址受眾，每24小時更新一次。 有關配置檔案的詳細資訊，請參閱 [即時客戶概要資訊概述](../profile/home.md)。

的 **[!UICONTROL 段]** 部分顯示在組織內建立的段總數。 此數字在建立新段時更新。 有關段的詳細資訊，請參閱 [分段服務概述](../segmentation/home.md)。

的 **[!UICONTROL 目標]** 部分顯示為組織建立的目標總數。 建立新目標時，將更新此編號。 有關目標的詳細資訊，請參閱 [目標概述](../destinations/home.md)。

### 最近的資料

最近的資料儀表板提供有關最近建立的資料集、源、段和目標的資訊。

![](images/user-guide/homepage-recent.png)

的 **[!UICONTROL 最近的資料集]** 部分列出了組織中最近建立的五個資料集。 每次建立新資料集時都會更新此清單。 可以從清單中選擇資料集以查看有關指定資料集的詳細資訊或選擇 **[!UICONTROL 查看全部]** 查看所有已建立資料集的清單。 有關資料集的詳細資訊，請參閱 [資料集概述](../catalog/datasets/overview.md)。

的 **[!UICONTROL 最近的來源]** 部分列出了您組織中最近建立的五個源連接器。 每次建立新的源連接器時都會更新此清單。 可以從清單中選擇源連接以查看有關指定連接器的詳細資訊或選擇 **[!UICONTROL 查看全部]** 查看所有已建立源連接的清單。 有關源的詳細資訊，請參閱 [源概述](../sources/home.md)。

的 **[!UICONTROL 最近段]** 部分列出了您組織中最近建立的五個段定義。 每次建立新段定義時都會更新此清單。 可以從清單中選擇段定義以查看有關指定段定義的詳細資訊或選擇 **[!UICONTROL 查看全部]** 查看所有建立的段定義的清單。 有關段的詳細資訊，請參閱 [分段服務概述](../segmentation/home.md)。

的 **[!UICONTROL 最近的目的地]** 部分列出了您組織中最近建立的五個目標。 每次建立新目標時都會更新此清單。 可以從清單中選擇一個目標，以查看有關指定目標的詳細資訊或選擇 **[!UICONTROL 查看全部]** 查看所有已建立目標的清單。 有關目標的詳細資訊，請參閱 [目標概述](../destinations/home.md)。

### 建議學習

的 **[!UICONTROL 建議學習]** 部分提供了有用文檔的連結以開始使用Adobe Experience Platform。

![](images/user-guide/homepage-recommended.png)

## 頂部導航欄

平台UI中的頂部導航欄顯示您當前登錄的組織，並提供幾個重要控制項。

導航欄左側是Adobe Experience Platform徽標。 隨時選擇此徽標將返回到平台UI主螢幕。

![](./images/user-guide/homepage-top-nav-bar.png)

### 組織切換器

頂部導航欄右側的第一項是 **組織切換器**。

![](./images/user-guide/homepage-ims-org-switcher.png)

選擇該切換器將開啟您有權訪問的組織的下拉菜單（如果有）。 要切換到其他組織，請選擇列出的選項。

### 交換機應用程式

頂部導航右側的下一項是 **應用交換機**，由 ![應用交換機](./images/user-guide/app-switcher-icon.png) 表徵圖 選擇此表徵圖時，您可以在您的組織有權訪問的Adobe應用程式之間切換，如Experience Platform、分析、資產和其他應用程式。

### 說明

在應用程式切換器右側 **幫助和支援菜單**，由 ![問號/幫助](./images/user-guide/help-icon.png) 表徵圖 選擇此表徵圖時，將出現一個跨距菜單，其中包含多個幫助和支援資源。 的 **[!UICONTROL 幫助]** 頁籤顯示當前所在頁面的相關文檔清單。 的 **[!UICONTROL 支援]** 頁籤允許您與Adobe支援團隊建立支援票證。 的 **[!UICONTROL 反饋]** 頁籤允許您將有關平台的反饋提交到Adobe。

![](images/user-guide/homepage-help-clicked.png)

### 通知和公告

在 **通知部分**，由 ![貝爾/通知和公告](images/user-guide/notification-icon.png) 表徵圖 的 **[!UICONTROL 通知]** 頁籤顯示有關產品和其他相關更新的重要資訊， **[!UICONTROL 公告]** 頁籤顯示有關服務維護的資訊。

### 使用者設定檔

頂部導航欄上的最後一項是 **用戶設定**，由 ![用戶設定/用戶配置檔案](images/user-guide/profile-icon.png) 表徵圖 選擇此表徵圖可編輯首選項或註銷。

您可以在平台介面的明暗主題之間切換，交換機位於您的姓名和電子郵件正下方。 選擇您喜歡的主題。

![](images/theme.png)

### 沙箱

頂部導航欄的正下方是沙箱欄。 此欄顯示您當前正在用於平台的沙盒。 有關沙箱的詳細資訊，請參閱 [箱概述](../sandboxes/home.md)。

## 左側導覽 {#left-nav}

螢幕左側的導航列出了平台UI中支援的所有不同服務。

按一下菜單表徵圖可顯示或隱藏左側導航面板。

![](images/user-guide/hidemenu.png)

在顯示面板後再次按一下可鎖定開啟位置的導航。

>[!IMPORTANT]
>
>左側導航欄僅顯示您可以訪問的功能。 在以前的Adobe Experience Platform版本中，禁用了不可用項。 如果您認為您應該有權訪問未顯示的分區，請與系統管理員聯繫。

![](images/user-guide/homepage-left.png)

的 **[!UICONTROL 首頁]** 頁。

的 **[!UICONTROL 工作流]** 部分顯示用於在平台內執行操作的多步驟工作流的清單。 有關工作流的詳細資訊，請參閱 [工作流概述](./workflows.md)。

### [!UICONTROL 連線]

的 **[!UICONTROL 源]** 部分，用於建立、更新和刪除源連接，允許將資料從外部源接收到平台。 有關源的詳細資訊，請參閱 [源概述](../sources/home.md)。

的 **[!UICONTROL 目標]** 部分，您可以建立、更新和刪除目標，從而將資料從平台導出到許多外部目標。 有關目標的詳細資訊，請參閱 [目標概述](../destinations/home.md)。

### [!UICONTROL 客戶]

的 **[!UICONTROL 配置檔案]** 部分用於瀏覽客戶配置檔案、查看配置檔案度量、建立和管理合併策略以及查看聯合架構。 瞭解有關使用 [!UICONTROL 配置檔案] ，請閱讀 [[!DNL Profile] 使用手冊](../profile/ui/user-guide.md)。 有關Real-Time Customer Profile的詳細資訊，請參閱 [即時客戶概要資訊概述](../profile/home.md)。

的 **[!UICONTROL 段]** 部分，用於建立和管理段定義。 瞭解有關使用 [!UICONTROL 段] ，請閱讀 [分段使用手冊](../segmentation/ui/overview.md)。 有關分段服務的詳細資訊，請參閱 [分段服務概述](../segmentation/home.md)。

的 **[!UICONTROL 身份]** 部分，用於建立和管理標識命名空間。 有關 [!UICONTROL 身份] 部分，包括有關標識命名空間的資訊以及如何在平台UI中使用標識，請參閱 [標識命名空間概述](../identity-service/namespaces.md)。

### [!UICONTROL 隱私]

的 **[!UICONTROL 策略]** 部分，用於建立和管理資料使用策略。 要瞭解有關使用「策略」部分的詳細資訊，請閱讀 [資料使用策略使用手冊](../data-governance/policies/user-guide.md)。 有關資料使用策略的詳細資訊，請參閱 [資料使用策略概述](../data-governance/policies/overview.md)。

的 **[!UICONTROL 請求]** 部分，用於建立和管理隱私請求。 請注意，必須允許您列出才能訪問Privacy ServiceUI。 要瞭解有關使用「請求」部分的更多資訊，請閱讀 [Privacy Service使用手冊](../privacy-service/ui/user-guide.md)。 有關Privacy Service的詳細資訊，請參閱 [Privacy Service概述](../privacy-service/home.md)。

### [!UICONTROL 資料科學]

的 **[!UICONTROL 筆記本]** 部分提供對JupyterLab的訪問，JupyterLab是一個互動式開發環境，允許您探索、分析和建模資料。 要瞭解有關使用筆記本部分的詳細資訊，請閱讀 [JupyterLab使用手冊](../data-science-workspace/jupyterlab/overview.md)。 有關Data Science Workspace的詳細資訊，請參閱 [資料科學工作區概述](../data-science-workspace/home.md)

的 **[!UICONTROL 模型]** 部分允許您使用機器學習和人工智慧來建立、開發、訓練和調整模型以做出預測。 有關「模型」(Models)部分的詳細資訊，請參見上面的教程 [訓練和評估模型](../data-science-workspace/models-recipes/train-evaluate-model-ui.md)。

的 **[!UICONTROL 服務]** 部分允許您管理已發佈的模型以進行計畫的培訓和評分，或使用Adobe的智慧服務，這是一組AI服務，可提供即時、個性化的客戶體驗。 有關「服務」部分的詳細資訊，請參見 [發佈模型作為服務教程](../data-science-workspace/models-recipes/publish-model-service-ui.md)。

### [!UICONTROL 資料管理]

的 **[!UICONTROL 架構]** 部分，用於建立和管理體驗資料模型(XDM)架構。 要瞭解有關架構的詳細資訊，請閱讀有關 [建立架構](../xdm/tutorials/create-schema-ui.md)。 有關XDM的詳細資訊，請參閱 [XDM系統概述](../xdm/home.md)。

的 **[!UICONTROL 資料集]** 部分，用於建立和管理資料集。 有關資料集的詳細資訊，請參閱 [資料集使用手冊](../catalog/datasets/user-guide.md)。

的 **[!UICONTROL 查詢]** 部分，用於建立和管理查詢、記錄Adobe Experience Platform查詢服務所做的SQL查詢，以及查看 [!DNL PostgreSQL] 憑據。 有關查詢的詳細資訊，請參閱 [查詢服務使用手冊](../query-service/ui/overview.md)。

的 **[!UICONTROL 監視]** 的子目錄中。 有關監視的詳細資訊，請參閱 [監控資料接收使用手冊](../ingestion/quality/monitor-data-ingestion.md)。

### [!UICONTROL 決定]

Adobe Journey Optimizer是建立在Experience Platform之上的應用程式服務。 它允許您使用功能強大的決策技術，在適當的時間跨所有接觸點為客戶提供最佳的服務和體驗。 瞭解有關Journey Optimizer的更多資訊，包括與 [!UICONTROL 優惠] 和 [!UICONTROL 活動] 訪問 [Journey Optimizer文檔](https://experienceleague.adobe.com/docs/journey-optimizer.html?lang=zh-Hant)。

### [!UICONTROL 管理]

平台用戶介面(UI)提供了一個儀表板，您可以通過該儀表板查看有關組織許可證使用情況的重要資訊，這些資訊在每日快照中捕獲。 通過選擇 **[!UICONTROL 許可證使用]** 的子菜單。 要瞭解有關許可證使用儀表板的詳細資訊，請訪問 [許可證使用儀表板指南](./license-usage-and-guardrails/license-usage-dashboard.md)。

>[!IMPORTANT]
>
>許可證使用儀表板功能當前位於Alpha中，並且不適用於所有用戶。 文件和功能可能會有所變更。

## 後續步驟

通過閱讀本指南，您現在已被介紹到平台UI的首頁和主要導航元素。 有關在用戶介面中工作的詳細資訊，請參閱每個平台服務的文檔。 此文檔的連結在 [左導航](#left-nav) 的子菜單。
