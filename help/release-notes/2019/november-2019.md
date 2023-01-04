---
title: Adobe Experience Platform發行說明2019年11月
description: 2019年11月Adobe Experience Platform發行說明。
doc-type: release notes
last-update: November 18, 2019
author: crhoades, ens28527
exl-id: 2c417c56-cc61-4788-b248-d98ea6cf89f0
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1887'
ht-degree: 2%

---

# Adobe Experience Platform 發行說明

**發行日期：2019 年 11 月 18 日**

Adobe Experience Platform的新功能：
* [[!DNL Real-Time Customer Data Platform]](#rtcdp)
* [[!DNL Destinations]](#destinations)
* [[!DNL Sources]](#sources)

更新現有功能：
* [[!DNL Data Science Workspace]](#dsw)
* [[!DNL Experience Data Model (XDM) System]](#xdm)
* [[!DNL Real-Time Customer Profile]](#profile)
* [[!DNL Segmentation Service]](#segmentation)

## [!DNL Real-Time Customer Data Platform] {#rtcdp}

Real-time Customer Data Platform(Real-Time CDP)以Adobe Experience Platform為基礎，可協助公司匯集已知和未知的資料，在客戶歷程中透過智慧決策來啟用客戶設定檔。 Real-Time CDP結合多個企業資料來源，以即時建立統一的設定檔，以用於在所有管道和裝置上提供一對一的個人化客戶體驗。

[!DNL Real-Time Customer Data Platform] 包含資料控管、身分管理、進階細分和資料科學等工具，讓您能夠建立設定檔和定義對象，並在能夠執行嚴格的資料控管原則的同時獲得豐富的深入分析。

Adobe可連接到大型合作夥伴生態系統，更不用說與Adobe Experience Cloud的原生整合，因此您可以順暢地啟用這些受眾，並在所有管道提供絕佳的客戶體驗，從站上或應用程式內個人化，到電子郵件、付費媒體、客服中心、連線裝置等等。

使用Real-Time CDP，您可以：

* 從整個企業串流收集客戶資料，以達到客戶的單一檢視。
* 以信任的控管和已知和未知識別碼的隱私權控制，負責任地管理設定檔。
* 運用AI和Adobe Sensei所提供的機器學習技術，為行銷人員打造，產生可操作的深入分析並擴大受眾。
* 在所有通道和目的地間即時提供個人化體驗。

如需詳細資訊，請參閱 [Real-time Customer Data Platform檔案](../../rtcdp/overview.md).

**主要功能**

| 功能 | 說明 |
|---|---|
| 目的地 | 預先建置的與Adobe支援的目的地平台整合 [!DNL Real-Time Customer Data Platform] 以順暢的方式向這些合作夥伴啟用資料。 請參閱 [目的地](#destinations) 以取得詳細資訊。 |
| 首頁量度控制面板 | Real-time Customer Data Platform(Real-Time CDP)首頁包含量度控制面板，可顯示設定檔和區段的相關資訊。 首頁還包含學習材料的連結。 請參閱 [Real-time Customer Data Platform量度](#real-time-customer-data-platform-metrics) 下方。 |
| 來源 | 您可以內嵌來自各種來源的資料，例如Adobe解決方案、雲端儲存、協力廠商軟體和您的CRM。 請參閱 [來源](#sources) 一節以深入了解。 |

**[!DNL Real-Time Customer Data Platform]量度**

Real-time Customer Data Platform(Real-Time CDP)首頁包含量度控制面板，會在您登入Real-Time CDP時顯示。

首頁只是顯示量度卡的其中一個位置。 Real-Time CDP會在您的整個體驗中提供量度卡。 這些量度會通知您系統中的資料、設定檔和區段對象。

如果您登入Real-Time CDP時系統中沒有資料，首頁的控制面板就不會顯示。 在這種情況下，首頁會提供第一次使用者體驗的學習資料。 收集資料時，控制面板會自動更新以顯示該資料的相關資訊。

若要進一步了解，請參閱 [Real-time Customer Data Platform量度概觀](../../rtcdp/home-page-dashboards.md)

## [!DNL Destinations] {#destinations}

[!DNL Destinations] 預先建置與AdobeReal-time Customer Data Platform所支援的目的地平台的整合，可順暢地向這些合作夥伴啟用資料。 如需詳細資訊，請閱讀 [目的地概觀](../../destinations/home.md) 文章。

**可用目的地**

11月發行版本中，Adobe的Real-time Customer Data Platform支援下列目的地：

* Advertising: [!DNL Google]
* 電子郵件行銷：Adobe Campaign, [!DNL Salesforce Marketing Cloud], [!DNL Responsys], [!DNL Oracle Eloqua]

請參閱 [目的地目錄](../../destinations/catalog/overview.md) 以取得每個目的地的相關資訊。

**已知限制**

* 在初始發行中，無法使用允許啟動流程中自訂啟動排程（排程步驟）的控制項。
* 目前無法編輯或刪除目標配置。 若要解決此限制，您可以啟用或停用 [目的地詳細資訊頁面](../../destinations/ui/destination-details-page.md).
* 當前未對帳戶詳細資訊、路徑或憑據進行驗證，無法連接到您的目標或儲存帳戶。 請務必輸入正確的憑證，並仔細檢查拼字錯誤或錯字。
* 初始發行時沒有憑據續訂。 帳戶過期或需要重新整理後，您必須建立新的目的地連線並重新對應先前對應的區段。

## 來源 {#sources}

Adobe Experience Platform可以內嵌來自外部來源的資料，同時允許您使用 [!DNL Platform] 服務。 您可以內嵌來自各種來源的資料，例如Adobe解決方案、雲端儲存、協力廠商軟體和您的CRM系統。

[!DNL Experience Platform] 提供RESTful API和互動式UI，讓您輕鬆為各種資料提供者設定來源連線。 這些源連接允許您對儲存系統和CRM服務進行身份驗證、設定獲取運行的時間，以及管理資料獲取吞吐量。

**主要功能**

| 功能 | 說明 |
| ---------- | ------------ |
| 來源UI | 用於建立、查看和管理源連接的新用戶介面。 |
| CRM連接器的改版工作流程 | 用於建立和管理的全新直覺式UI工作流程 [!DNL Microsoft Dynamics] 和 [!DNL Salesforce] 連接器。 |
| 雲端儲存的連接器支援 | 連接器現在可以存取雲端儲存空間。 新來源包括 [!DNL Amazon S3], [!DNL Azure Blob]和FTP/SFTP伺服器。 |

**已知問題**

* 雲端儲存的來源連接器不支援擷取壓縮檔案。

如需來源的詳細資訊，請參閱 [來源概觀](../../sources/home.md).

## [!DNL Data Science Workspace] {#dsw}

Adobe Experience Platform [!DNL Data Science Workspace] 通過構建和操作機器學習模型，資料科學家可以跨Adobe應用程式和第三方系統無縫地從資料和內容生成見解。 [!DNL Data Science Workspace] 緊密整合於 [!DNL Platform] 並支援端對端資料科學的生命週期，包括探索和準備XDM資料，接著開發並實施模型以自動豐富 [!DNL Real-Time Customer Profile] 以及機器學習深入分析。

**新功能**

| 功能 | 說明 |
| -----------| ---------- |
| 使用 [!DNL Platform] SDK | 預先構建的配方和啟動器筆記型電腦 [!DNL Python] 現在使用 [!DNL Platform] 用於存取資料的SDK。 |
| 支援沙箱 | 支援即將推出的沙箱功能（目前為測試版），包括將筆記型電腦和配方隔離至開發或生產沙箱的功能。 請參閱 [沙箱概述](../../sandboxes/home.md) 以取得更多資訊。 |

如需詳細資訊，請參閱 [Data Science Workspace概觀](../../data-science-workspace/home.md).

## [!DNL Experience Data Model] (XDM)系統 {#xdm}

標準化和互操作性是背後的關鍵概念 [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM)受Adobe推動，致力標準化客戶體驗資料並定義客戶體驗管理的結構。

XDM是公開記錄的規格，旨在改善數位體驗的強大功能。 它為與Adobe Experience Platform上的服務通訊的任何應用程式提供共同的結構和定義。 遵循XDM標準，所有客戶體驗資料皆可整合至以更快速、更整合的方式提供深入分析的通用表示法中。 您可以從客戶動作中獲得寶貴的深入分析、透過區段定義客戶受眾，以及將客戶屬性用於個人化目的。

**新功能**

| 功能 | 說明 |
| ---------- | ------------ |
| 通知結構 | 代表資料擷取程式期間所傳送之通知資料的新結構。 |
| AdobeAdCloud DSP結構 | 已新增五個新結構，以呈現Adobe Advertising Cloud需求端平台(DSP)中繼資料：版位、行銷活動、套件、廣告商、帳戶。 |
| ExperienceEvent實作詳細資料結構欄位群組 | 新增標準欄位以儲存用於收集事件之軟體的相關資訊的ExperienceEvent欄位群組。 |
| [!DNL Profile Privacy] 欄位群組 | 新的設定檔欄位群組，新增欄位以接受 [!DNL Real-Time Customer Profile]. |
| 格式限制 `xdm:alternateDisplayInfo` | 的「標題」和「說明」欄位 `xdm:alternateDisplayInfo` 必須兩者皆為字串，才能通過驗證。 |
| 名稱更改：XDM [!DNL Individual Profile] | XDM的&quot;標題&quot; [!DNL Profile]「 」類別已更新為「 XDM」 [!DNL Individual Profile]」。 正式 `$id` 班級沒有更改。 |

**已知問題**

* None.

若要進一步了解如何使用XDM，請使用 [!DNL Schema Registry] API和 [!DNL Schema Editor] 用戶介面，請閱讀 [XDM系統檔案](../../xdm/home.md).

## [!DNL Real-Time Customer Profile] {#profile}

Adobe Experience Platform可讓您為客戶提供協調、一致且相關的體驗，無論客戶在何處或何時與您的品牌互動。 使用 [!DNL Real-Time Customer Profile]，您可以全面了解將多個管道資料結合在一起的每個客戶，包括線上、離線、CRM和協力廠商資料。 [!DNL Profile] 可讓您將不同的客戶資料整合至統一的檢視中，提供每個客戶互動的可操作、時間戳記帳戶。

| 功能 | 說明 |
| -----------| ---------- |
| 的增強功能 [!DNL Profile] 查閱 | 使用者現在能使用參考描述元和相關實體來尋找設定檔。 |
| 清除指定資料集的資料 | 使用者現在可以使用 [!DNL Profile] 系統作業API。 |
| Edge [!DNL Profile] 查詢增強功能 | 應用程式現在可以查詢Edge [!DNL Profile] 的任何身分。 |
| 根據投影配置合併策略 | 現在，應用程式可以針對每個投影配置合併策略，以便生成由特定合併策略管理的資料視圖。 |
| 計算屬性 | 計算屬性會根據其他值、計算和運算式自動計算欄位的值。 計算屬性會在設定檔層級上運作，以根據傳入事件、傳入事件和設定檔資料，或傳入事件、設定檔資料和歷史事件，匯總「購買總計」、「期限值」或「漏斗狀態」等值。 |

**錯誤修正**

* 簡化合併原則建立工作流程中可用ID匯整策略的清單。

**已知問題**

* None.

如需 [!DNL Real-Time Customer Profile]，包括教學課程和使用的最佳實務 [!DNL Profile] 資料，請閱讀 [即時客戶個人檔案概觀](../../profile/home.md).

## [!DNL Segmentation Service] {#segmentation}

Adobe Experience Platform [!DNL Segmentation Service] 提供使用者介面和RESTful API，可讓您建立區段，並從中產生對象 [!DNL Real-Time Customer Profile] 資料。 這些區段是在 [!DNL Platform]，讓任何Adobe應用程式都能輕鬆存取。

[!DNL Segmentation Service] 會透過說明區分客戶群中可行銷人員群組的條件，來定義特定設定檔子集。 區段可以根據記錄資料（例如人口統計資訊）或代表客戶與您品牌互動的時間序列事件。

| 功能 | 說明 |
| -----------| ---------- |
| 排程分段 | 使用者現在可以透過UI和API，為所有區段啟用排程的區段評估。 啟用後，每天會評估一次所有區段。 這不會影響隨需分段功能，這些功能可繼續如先前般運作。<br/><br/>注意：排程分段功能無法用於沙箱中，其中的 [!DNL XDM Individual Profile]. |
| 串流細分 | 支援持續評估區段（串流分段），可在資料傳入時評估大部分的區段規則 [!DNL Platform]. 此功能表示區段成員資格將為最新狀態，不需要執行已排程的分段工作。 有些例外適用，例如使用多實體關係或包含擴充裝載的區段。 |
| 區段作為建置區塊 | 使用區段產生器UI建立區段時，使用者現在可以使用先前定義的區段作為其他區段的建置區塊。 <ul><li>參考目前的受眾成員資格：當人員移入和移出對象時更新。</li><li>複製邏輯：取用選取的區段定義，並將其複製到新區段中。</li></ul> |
| 依ID命名空間檢視區段成員資格 | 您現在可以透過ID命名空間（電子郵件、ECID和總計）來檢視區段成員資格。 |
| RBAC支援 | 區段產生器現在支援基本的角色型存取控制和權限。 |
| 增強支援外部受眾在 [!DNL Platform] 和Adobe解決方案 | 使用者現在可以帶入外部(非[!DNL Experience Platform])對象中繼資料，其中對象數量很大或不是先驗。 此版本包含 [!DNL Audience Manager] 已布建解決方案連接器之客戶的中繼資料。 此受眾中繼資料可在「區段產生器」內使用，以建立新 [!DNL Experience Platform] 區段。 <br/><br/> 此外，在 [!DNL Experience Platform] 現在可用於整合Adobe解決方案，包括 [!DNL Audience Manager], [!DNL Target]，和 [!DNL Ad Cloud]. |

**錯誤修正**

* 修正造成多實體分段在巢狀關係中傳回零設定檔的問題。
* 修正排除邏輯傳回誤導結果的問題。
* 改善多實體資料夾的可讀性。 現在會顯示XDM類別的易記名稱。
* 修正了間歇性問題，亦即出現多個相同XDM資料夾復本。
* 現在會產生訊息，以在所選合併原則無法使用區段估計時通知使用者。

**已知問題**

* None.

若要深入了解 [!DNL Segmentation Service]，請閱讀 [區段服務概觀](../../segmentation/home.md).
