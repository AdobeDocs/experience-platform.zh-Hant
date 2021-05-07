---
title: Adobe Experience Platform 發行說明
description: Experience Platform發行說明2019年11月18日
doc-type: release notes
last-update: November 18, 2019
author: crhoades, ens28527
exl-id: 2c417c56-cc61-4788-b248-d98ea6cf89f0
translation-type: tm+mt
source-git-commit: ab0798851e5f2b174d9f4241ad64ac8afa20a938
workflow-type: tm+mt
source-wordcount: '1883'
ht-degree: 4%

---

# Adobe Experience Platform 發行說明

**發行日期：2019 年 11 月 18 日**

Adobe Experience Platform的新功能：
* [[!DNL Real-time Customer Data Platform]](#rtcdp)
* [[!DNL Destinations]](#destinations)
* [[!DNL Sources]](#sources)

更新現有功能：
* [[!DNL Data Science Workspace]](#dsw)
* [[!DNL Experience Data Model (XDM) System]](#xdm)
* [[!DNL Real-time Customer Profile]](#profile)
* [[!DNL Segmentation Service]](#segmentation)

## [!DNL Real-time Customer Data Platform] {#rtcdp}

即時客戶資料平台(Real-time CDP)建立在Adobe Experience Platform之上，可協助公司將已知和未知的資料匯整在一起，在客戶歷程中運用智慧決策來啟動客戶個人檔案。 即時CDP結合了多個企業資料源，以即時建立統一的配置檔案，可用於跨所有通道和設備提供一對一的個性化客戶體驗。

[!DNL Real-time Customer Data Platform] 包括資料管理、身分識別管理、進階細分和資料科學等工具，讓您能夠建立個人檔案並定義受眾，並獲得豐富的洞見，同時能夠執行嚴格的資料治理政策。

Adobe可連結到龐大的合作夥伴生態系統，更不用說與Adobe Experience Cloud的原生整合，因此您可以透過所有通道順暢地激活這些受眾，並提供絕佳的客戶體驗，從現場或應用程式內個人化到電子郵件、付費媒體、客服中心、連線裝置等。

使用即時CDP ，您可以：

* 從企業內部串流收集客戶資料，讓客戶獲得單一視圖。
* 使用受信任的治理及已知和未知識別碼的隱私權控制，以負責任的方式管理個人檔案。
* 運用由Adobe Sensei提供並專為行銷人員打造的人工智慧和機器學習，產生可操作的見解並擴大受眾。
* 跨所有通道和目的地即時提供個人化體驗。

如需詳細資訊，請參閱[即時客戶資料平台檔案](../../rtcdp/overview.md)。

**主要功能**

| 功能 | 說明 |
|---|---|
| 目的地 | 與Adobe[!DNL Real-time Customer Data Platform]支援的目標平台預先建立整合，以順暢的方式將資料啟動給這些合作夥伴。 如需詳細資訊，請參閱下方的[目標](#destinations)。 |
| 首頁度量控制面板 | 即時客戶資料平台（即時CDP）首頁包含度量儀表板，可顯示個人檔案和細分的相關資訊。 首頁也包含學習教材的連結。 請參閱以下[即時客戶資料平台量度](#real-time-customer-data-platform-metrics)一節。 |
| 來源 | 您可以從多種來源收集資料，例如Adobe解決方案、雲端儲存空間、協力廠商軟體和您的CRM。 請參閱下面的[Sources](#sources)一節以瞭解更多資訊。 |

**[!DNL Real-time Customer Data Platform]量度**

當您登入即時CDP時，會顯示即時客戶資料平台（即時CDP）首頁，其中包含量度儀表板。

首頁只是顯示量度卡片的位置之一。 即時CDP在您的整個體驗中提供度量卡。 這些量度會通知您系統中的資料、設定檔和區段對象。

如果登錄到即時CDP時系統中沒有資料，則首頁上的儀表板不會顯示。 在這種情況下，首頁會提供首次使用者體驗的學習教材。 當收集資料時，控制面板會自動更新以顯示該資料的相關資訊。

如需詳細資訊，請參閱[即時客戶資料平台量度概觀](../../rtcdp/home-page-dashboards.md)

## [!DNL Destinations] {#destinations}

[!DNL Destinations] 是預先建立的整合，具有之目的地平台受到 Adobe 的 Real-time Customer Data Platform 支援，其可透過順暢的方式為這些合作夥伴啟動資料。如需詳細資訊，請閱讀[目標概觀](../../destinations/home.md)文章。

**可用目的地**

在11月的發行中，Adobe的即時客戶資料平台支援以下目標：

* 廣告: [!DNL Google]
* 電子郵件行銷：Adobe Campaign、[!DNL Salesforce Marketing Cloud]、[!DNL Responsys]、[!DNL Oracle Eloqua]

有關每個目標的資訊，請參見[目標目錄](../../destinations/catalog/overview.md)。

**已知限制**

* 在初始發行中，不提供允許在[啟動流程](../../destinations/ui/activate-destinations.md#activate-data)（計畫步驟）中自訂啟動計畫的控制項。
* 目前無法編輯或刪除目標配置。 要解決此限制，您可以在[目標詳細資訊頁面](../../destinations/ui/destination-details-page.md)的右上角啟用或禁用目標。
* 當連線至您的目標或儲存帳戶時，目前沒有驗證帳戶詳細資訊、路徑或憑證。 請確定您輸入了正確的認證，並仔細檢查拼字錯誤或錯字。
* 初始發行後，未進行任何憑證續約。 一旦帳戶過期或需要重新整理，您必須建立新的目的地連線並重新對應先前映射的區段。

## 來源 {#sources}

Adobe Experience Platform可以從外部來源收集資料，同時允許您使用[!DNL Platform]服務來建構、標籤和增強該資料。 您可以從多種來源收集資料，例如Adobe解決方案、雲端儲存空間、協力廠商軟體和您的CRM系統。

[!DNL Experience Platform] 提供REST風格的API和互動式UI，讓您輕鬆地為各種資料提供者設定來源連線。這些源連接允許您對儲存系統和CRM服務進行身份驗證，設定接收運行的時間，並管理資料接收吞吐量。

**主要功能**

| 功能 | 說明 |
| ---------- | ------------ |
| Sources UI | 用於建立、查看和管理源連接的新用戶介面。 |
| 改良的CRM連接器工作流程 | 建立和管理[!DNL Microsoft Dynamics]和[!DNL Salesforce]連接器的全新直覺式UI工作流程。 |
| 雲端儲存空間的連接器支援 | 連接器現在可以存取雲端儲存空間。 新來源包括[!DNL Amazon S3]、[!DNL Azure Blob]和FTP/SFTP伺服器。 |

**已知問題**

* 雲端儲存的來源連接器不支援擷取壓縮檔案。

有關源的詳細資訊，請參閱[源概述](../../sources/home.md)。

## [!DNL Data Science Workspace] {#dsw}

Adobe Experience Platform[!DNL Data Science Workspace]可讓資料科學家建立並執行機器學習模型，從跨Adobe應用程式和協力廠商系統的資料和內容順暢地產生見解。 [!DNL Data Science Workspace] 與端對端資 [!DNL Platform] 料科學生命週期緊密整合，包括探索和準備XDM資料，然後開發和運作模型以自動豐富機器學習 [!DNL Real-time Customer Profile] 見解。

**新功能**

| 功能 | 說明 |
| -----------| ---------- |
| 使用[!DNL Platform] SDK存取資料 | [!DNL Python]中預先建立的配方和啟動器筆記型電腦現在使用[!DNL Platform] SDK來存取資料。 |
| 支援沙盒 | 支援即將推出的沙盒功能（目前為測試版），包括將筆記型電腦和配方隔離至開發或生產沙盒的功能。 如需詳細資訊，請參閱[沙盒概述](../../sandboxes/home.md)。 |

如需詳細資訊，請參閱[資料科學工作區概觀](../../data-science-workspace/home.md)。

## [!DNL Experience Data Model] (XDM)系統  {#xdm}

標準化和互操作性是[!DNL Experience Platform]背後的關鍵概念。 [!DNL Experience Data Model] (XDM)由Adobe驅動，旨在標準化客戶體驗資料並定義客戶體驗管理的架構。

XDM是公開記載的規格，旨在改善數位體驗的強大功能。 它為與Adobe Experience Platform服務通訊的任何應用程式提供共同的架構和定義。 遵循XDM標準，所有客戶體驗資料都可整合在以更快速、更整合的方式提供見解的通用表現形式中。 您可以從客戶行動中獲得寶貴見解，透過細分定義客戶受眾，並將客戶屬性用於個人化目的。

**新功能**

| 功能 | 說明 |
| ---------- | ------------ |
| 通知結構 | 表示資料擷取程式期間傳送之通知資料的新架構。 |
| AdobeAdCloud結DSP構 | 已新增5種新結構來代表Adobe Advertising Cloud需求端平台(DSP)中繼資料：位置、促銷活動、封裝、廣告商、帳戶。 |
| ExperienceEvent實作詳細資訊結構欄位群組 | 新增ExperienceEvent欄位群組，新增標準欄位以儲存用於收集事件之軟體的相關資訊。 |
| [!DNL Profile Privacy] 欄位組 | 新的描述檔欄位群組，新增欄位以接受[!DNL Real-time Customer Profile]的一般退出和銷售／共用退出訊號。 |
| `xdm:alternateDisplayInfo`的格式限制 | `xdm:alternateDisplayInfo`的「標題」和「說明」欄位必須同時是字串，才能通過驗證。 |
| 名稱變更：XDM [!DNL Individual Profile] | &quot;XDM [!DNL Profile]&quot;類的&quot;title&quot;已更新為&quot;XDM [!DNL Individual Profile]&quot;。 類的正式`$id`未更改。 |

**已知問題**

* None.

要瞭解有關使用[!DNL Schema Registry] API和[!DNL Schema Editor]用戶介面使用XDM的更多資訊，請閱讀[ XDM系統文檔](../../xdm/home.md)。

## [!DNL Real-time Customer Profile] {#profile}

Adobe Experience Platform可讓您為客戶推動協調、一致且相關的體驗，不論客戶在何處或何時與您的品牌互動。 透過[!DNL Real-time Customer Profile]，您可以全面瞭解每個客戶，並結合來自多個通道的資料，包括線上、離線、CRM和第三方資料。 [!DNL Profile] 可讓您將分散的客戶資料整合為統一的檢視，提供每個客戶互動的可操作、時間戳記帳戶。

| 功能 | 說明 |
| -----------| ---------- |
| [!DNL Profile]查閱的增強功能 | 使用者現在可以使用參考描述子和相關實體來尋找描述檔。 |
| 清除指定資料集的資料 | 使用者現在可以使用[!DNL Profile]系統工作API刪除特定資料集或批次的資料。 |
| Edge [!DNL Profile]查詢增強功能 | 應用程式現在可以依指定描述檔的任何身分來查詢Edge [!DNL Profile]。 |
| 根據投影配置合併策略 | 應用程式現在可以針對每個投影設定合併原則，以產生由特定合併原則所控制之資料的檢視。 |
| 計算屬性 | 計算屬性會根據其他值、計算和運算式自動計算欄位的值。 計算屬性在描述檔層級上運作，以根據傳入事件、傳入事件和描述檔資料，或傳入事件、描述檔資料和歷史事件，來匯總「購買總計」、「期限值」或「漏斗狀態」等值。 |

**錯誤修正**

* 合併原則建立工作流程中可用ID接合策略的簡化清單。

**已知問題**

* 沒有。

有關[!DNL Real-time Customer Profile]的詳細資訊，包括使用[!DNL Profile]資料的教學課程和最佳實務，請閱讀[即時客戶資料概觀](../../profile/home.md)。

## [!DNL Segmentation Service] {#segmentation}

Adobe Experience Platform[!DNL Segmentation Service]提供使用者介面和RESTful API，可讓您建立區段並從您的[!DNL Real-time Customer Profile]資料產生觀眾。 這些區段是集中設定並維護在[!DNL Platform]上，讓任何Adobe應用程式都可輕鬆存取。

[!DNL Segmentation Service] 定義個人檔案的特定子集，方法是描述區分客戶群中有價人群的標準。區段可以根據記錄資料（例如人口統計資訊）或代表客戶與品牌互動的時間系列事件來劃分。

| 功能 | 說明 |
| -----------| ---------- |
| 排程的區段 | 使用者現在可以透過UI和API，為所有區段啟用排程的區段評估。 啟用後，每天會評估一次所有區段。 這不會影響依需求而繼續運作的區段功能。<br/><br/>注意：已排程的分段功能無法用於超過五個合併原則的沙盒 [!DNL XDM Individual Profile]。 |
| 串流區段 | 支援持續評估區段（串流區段），可讓資料傳入[!DNL Platform]時，評估大部分區段規則。 此功能表示區段會籍將是最新的，不需要執行排程的區段工作。 有些例外適用，例如使用多實體關係或包含豐富負載的區段。 |
| 區段做為建立區塊 | 使用「區段產生器」UI建立區段時，使用者現在可以使用先前定義的區段作為其他區段的建立區塊。 <ul><li>參考目前的觀眾會籍：隨著受眾的移入和移出而更新。</li><li>複製邏輯：將選取的區段定義複製到新區段。</li></ul> |
| 依ID命名空間檢視區段成員資格 | 區段會籍現在可依ID命名空間（電子郵件、ECID和總計）來檢視。 |
| RBAC支援 | 區段產生器現在支援基本的角色存取控制與權限。 |
| 增強[!DNL Platform]與Adobe解決方案之間外部觀眾共用的支援 | 使用者現在可在觀眾數量龐大或先驗未知的情況下，引入外部（非[!DNL Experience Platform]）觀眾中繼資料。 此版本包含對已布建解決方案連接器之客戶的[!DNL Audience Manager]中繼資料的存取。 此觀眾中繼資料可用於區段產生器中，以建立新的[!DNL Experience Platform]區段。 <br/><br/> 此外，在中建立的 [!DNL Experience Platform] 區段現在可用於整合的Adobe解決方案， [!DNL Audience Manager]包括 [!DNL Target]、和 [!DNL Ad Cloud]。 |

**錯誤修正**

* 修正在巢狀關係出現時，「多實體分段」會傳回零個描述檔的問題。
* 修正排除邏輯傳回誤導結果的問題。
* 改善多實體資料夾的可讀性。 現在會顯示XDM類別的好記名稱。
* 修正同一XDM資料夾出現多份副本的間歇性問題。
* 現在產生訊息，以通知使用者選取的合併原則無法使用區段估計。

**已知問題**

* 沒有。

若要進一步瞭解[!DNL Segmentation Service]，請閱讀[分段服務概觀](../../segmentation/home.md)。
