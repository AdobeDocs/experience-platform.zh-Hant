---
title: Adobe Experience Platform 發行說明
description: Experience Platform發行說明2020年5月13日
doc-type: release notes
last-update: May 13, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: db3acec75c24a0cb75d1d88e7aa2171e794abc4f
workflow-type: tm+mt
source-wordcount: '1299'
ht-degree: 5%

---


# Adobe Experience Platform 發行說明

**發行日期: 2020 年 5 月 13 日**

Adobe Experience Platform現有功能的更新：

- [使用者介面更新](#ux)
- [資料科學工作區](#dsw)
- [目的地](#destinations)
- [Experience Platform Web SDK與Experience Platform Edge Network](#edge)
- [即時客戶個人檔案](#profile)
- [來源](#sources)

## 使用者介面更新 {#ux}

Adobe Experience Platform將發佈網域和標題列的更新，以改善您的體驗並與其他Experience Cloud應用程式統一。

- 更輕鬆地在組織之間切換或切換至不同的應用程式
- 改善使用者說明，包括說明功能表中的精選文章和內容相關檔案
- 能夠提供有關Experience Platform和檔案支援票證的意見回饋

新體驗的推出是漸進的。 您可以在https://experience.adobe.com/platform上檢視 [體驗](https://experience.adobe.com/platform)。

## 資料科學工作區 {#dsw}

Data Science Workspace使用機器學習和人工智慧，從您的資料中釋放深入資訊。 Data Science Workspace整合至Adobe Experience Platform，可協助您透過Adobe解決方案使用內容和資料資產進行預測。 Data Science Workspace的其中一個實現方式是使用JupyterLab。 JupyterLab是專案Jupyter的網路使用者介面， <a href="https://jupyter.org/" target="_blank"></a> 並與Adobe Experience Platform緊密整合。 它為資料科學家提供互動式開發環境，以便與Jupyter筆記型電腦、程式碼和資料搭配使用。

**新功能**

| 功能 | 說明 |
|--- | ---|
| JupyterLab Launcher | JupyterLab Launcher現在包含Spark 2.4筆記型電腦的啟動器。 Spark 2.3筆記型起動器現在已標示為已過時，並設定在後續版本中移除。 |
| Spark 2.4 | 全新Scala(Spark)和PySpark配方現在使用Spark 2.4。 |
| 內核 | Scala(Spark)筆記本現在是透過Scala內核製作的。 PySpark筆記本現在是透過Python Kernel製作的。 Spark和PySpark內核已過時，並設定在後續版本中移除。 |
| 配方 | 新的PySpark和Spark配方現在會遵循類似Python和R配方的Docker工作流程。 |

有關遷移筆記型電腦和使用Spark 2.4的配方的詳細資訊，請參閱筆記本 [遷移指南](../../data-science-workspace/recipe-notebook-migration.md)。 如需資料科學工作區的詳細資訊，請參閱總 [覽檔案](../../data-science-workspace/home.md)。

## 目的地 {#destinations}

在 [Adobe即時客戶資料平台中](../../rtcdp/overview.md)，目標是與目標平台預先建立的整合，以順暢的方式將資料啟動給這些合作夥伴。

**Facebook**

Adobe即時CDP現在支援Facebook的資料啟動功能，讓您啟用Facebook宣傳的個人檔案，以便根據雜湊的電子郵件鎖定受眾、個人化和抑制受眾。

如需新功能的詳細資訊，請參閱 [Facebook目標頁面](/help/rtcdp/destinations/facebook-destination.md) 。

<br> 

**Amazon Kinesis和Azure事件集線器流雲儲存目標**

Adobe即時CDP現在支援將資料啟動至串流雲端儲存目的地，讓您以JSON格式將觀眾資料和事件匯出至這些目的地。 然後，您可以在目的地的這些活動上描述商業邏輯。 如需詳細資訊，請參閱以下：

>[!NOTE]
>
>Adobe [!DNL Amazon Kinesis] 即時 [!DNL Azure Event Hubs] CDP中的目標和目標目前都在測試中。 文件和功能可能會有所變更。

| 文件 | 說明 |
|--- | ---|
| [（測試版）Amazon Kinesis目標](/help/rtcdp/destinations/amazon-kinesis-destination.md) | 本文說明如何建立儲存空間的即時出站連線，以 [!DNL Amazon Kinesis] 便從Adobe Experience Platform串流資料。 |
| [（測試版）Azure事件集線器目標](/help/rtcdp/destinations/azure-event-hubs-destination.md) | 本文說明如何建立儲存空間的即時出站連線，以 [!DNL Azure Event Hubs] 便從Adobe Experience Platform串流資料。 |
| [API教學課程——連線至串流目的地並啟用資料](/help/rtcdp/destinations/streaming-destinations-api-tutorial.md) | 本教學課程示範如何使用API呼叫連線至您的Adobe Experience Platform資料、建立串流雲端儲存目的地（Amazon Kinesis或Azure事件中樞）的連線、建立資料流至新建立的目的地，以及啟用資料至新建立的目的地。 |

如需詳細資訊，請參閱「目 [標」概觀](/help/rtcdp/destinations/destinations-overview.md)。

## Experience Platform Web SDK與Experience Platform Edge Network {#edge}

Experience Platform Web SDK和Experience Platform Edge Network可讓使用者針對一般使用者裝置和瀏覽器，即時將資料傳送至Adobe Experience Platform和其他Adobe解決方案。 我們的公開路線圖經常更新，您可以找到最 [新的](https://github.com/adobe/alloy/projects/5) 「使用案例」清單。

**新功能**

| 功能 | 說明 |
|--- | ---|
| 支援ECID | SDK支援ECID立即可用，而不需安裝任何其他程式庫或資訊 |
| 設定UI | 使用Launch中新的Edge組態UI管理您的組態ID設定，必須加入白名單才能存取 |
| Adobe Experience Platform Web SDK Mixin | 與包含所有支援欄位的Experience Platform網頁SDK搭配使用的混合程式。 |
| 課程許可控制 | 為公司提供選擇加入和選擇退出Experience Platform Web SDK的控制 |
| 全新Experience Cloud除錯程式擴充功能的用戶端除錯支援 | 檢視來自Experience Platform網頁SDK的要求以及邊緣追蹤，以瞭解資料在系統中的流程。 |
| Adobe Analytics | 透過邊緣設定，將資料傳送至Analytics報表套裝。 XDM已平面化為內容資料，支援多套裝標籤 |
| Adobe Target | 支援Adobe Target。 包括VEC、表單撰寫器、A/B、XT、自動個人化、MVT |
| Adobe Audience Manager支援 | 支援Audience Manager ID同步、URL目的地和Cookie目的地 |
| 身分同步 | 重新 `setCustomersIds` 命名 `syncIdentity` 為，以更清楚顯示 |
| XDM Object Builder | 在啟動擴充功能中，您現在可以將XDM物件建立為資料元素 |

如需有關Platform Web SDK和Edge Network的詳細資訊，請參閱文 [件](../../edge/home.md)。

## 即時客戶個人檔案 {#profile}

Adobe Experience Platform可讓您為客戶推動協調、一致且相關的體驗，不論客戶在何處或何時與您的品牌互動。 透過即時客戶個人檔案，您可以全面瞭解每個客戶，並結合來自多個通道的資料，包括線上、離線、CRM和第三方資料。 個人檔案可讓您將分散的客戶資料整合到統一的檢視中，為每次客戶互動提供可操作的時間戳記帳戶。

**新功能**

| 功能 | 說明 |
| -----------| ---------- |
| 新的描述檔匯出量度 | 新增度量至描述檔匯出工作，顯示每個命名空間中匯出的描述檔總數和描述檔數。 |
| 新的可觀測性見解度量 | 可觀測性洞察API現在提供下列量度，用於串流擷取至描述檔： 傳入請求率、成功擷取率、已收錄記錄大小。 |
| 大量GET端點 | 新增大量GET端點至即時客戶設定檔API，以在單一API呼叫中擷取多個結果。 您現在最多可以批量使用100個ID來識別區段定義、區段工作和合併原則。 |
| 依身分瀏覽描述檔 | 在平台UI中，您現在可以選取識別名稱空間並提供識別值，以瀏覽描述檔。 |

**錯誤修正**

- 無.

**已知問題**

- 無.

如需即時客戶個人檔案的詳細資訊，包括使用個人檔案資料的教學課程和最佳實務，請閱 [讀即時客戶個人檔案概觀](../../profile/home.md)。

## 來源 {#sources}

Adobe Experience Platform可以從外部來源擷取資料，同時允許您使用平台服務來建構、標示和增強該資料。 您可以從多種來源收集資料，例如Adobe應用程式、雲端儲存空間、協力廠商軟體和您的CRM系統。

Experience Platform提供REST風格的API和互動式UI，讓您輕鬆為各種資料提供者設定來源連線。 這些源連接允許您驗證並連接到外部儲存系統和CRM服務、設定接收運行的時間，以及管理資料接收吞吐量。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 雲端儲存系統的其他API和UI支援 | Azure檔案儲存的新來源連接器。 |
| 其他資料庫的API和UI支援 | Azure資料總管、IBM DB2和Oracle DB的新來源連接器。 |
| Adobe Audience Manager提供Experience Platform資料共用功能 | Audience Manager連接器的布建程式已更新。 「即時客戶個人檔案」的Audience Manager資料集現在預設為停用。 您可以手動選擇要提升至描述檔的資料集。 新的預設設定不具可回溯性，而且只會影響新Audience Manager連接器的布建。 請參閱「資料集使用 [指南」中的詳細資訊](../../catalog/datasets/user-guide.md)。 |

**已知問題**

- 無.

若要進一步瞭解來源，請參閱 [來源概觀](../../sources/home.md)。