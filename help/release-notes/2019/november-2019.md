---
title: Adobe Experience Platform發行說明2019年11月
description: Adobe Experience Platform的2019年11月發行說明。
doc-type: release notes
last-update: November 18, 2019
author: crhoades, ens28527
exl-id: 2c417c56-cc61-4788-b248-d98ea6cf89f0
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1889'
ht-degree: 7%

---

# Adobe Experience Platform 發行說明

**發行日期： 2019年11月18日**

Adobe Experience Platform中的新功能：
* [[!DNL Real-Time Customer Data Platform]](#rtcdp)
* [[!DNL Destinations]](#destinations)
* [[!DNL Sources]](#sources)

更新現有功能：
* [[!DNL Data Science Workspace]](#dsw)
* [[!DNL Experience Data Model (XDM) System]](#xdm)
* [[!DNL Real-Time Customer Profile]](#profile)
* [[!DNL Segmentation Service]](#segmentation)

## [!DNL Real-Time Customer Data Platform] {#rtcdp}

Real-time Customer Data Platform (Real-Time CDP)以Adobe Experience Platform為基礎，可協助公司整合已知和未知的資料，透過客戶歷程中的智慧型決策來啟用客戶設定檔。 Real-Time CDP結合多個企業資料來源以即時建立統一的設定檔，其可用於跨所有管道和裝置提供一對一的個人化客戶體驗。

[!DNL Real-Time Customer Data Platform]包含資料控管、身分管理、進階細分和資料科學的工具，因此您可以建立設定檔和定義對象，並獲得豐富的見解，同時能夠強制實施嚴格的資料控管原則。

Adobe可連結至龐大的合作夥伴生態系統，更不用說與Adobe Experience Cloud的原生整合，因此您可以順暢地啟用這些對象，並在所有管道（從站上或應用程式內個人化，到電子郵件、付費媒體、呼叫中心、連線裝置等）提供絕佳的客戶體驗。

透過Real-Time CDP，您可以：

* 透過串流收集整個企業的客戶資料，以單一檢視方式呈現您的客戶。
* 使用已知和未知識別碼的信任治理和隱私控制負責任地管理設定檔。
* 使用由Adobe Sensei提供支援並專為行銷人員建置的AI和機器學習來產生可操作的見解並擴展受眾。
* 跨所有管道和目的地即時提供個人化體驗。

如需詳細資訊，請參閱[Real-time Customer Data Platform檔案](../../rtcdp/overview.md)。

**主要功能**

| 功能 | 說明 |
|---|---|
| 目的地 | 預先建立與Adobe [!DNL Real-Time Customer Data Platform]支援的目的地平台的整合，這些平台以順暢的方式為這些合作夥伴啟用資料。 如需詳細資訊，請參閱下方的[目的地](#destinations)。 |
| 首頁量度控制面板 | Real-time Customer Data Platform (Real-Time CDP)首頁包含量度控制面板，顯示設定檔和區段的相關資訊。 首頁也包含學習資料的連結。 請參閱下方[Real-time Customer Data Platform量度](#real-time-customer-data-platform-metrics)的相關章節。 |
| 來源 | 您可以從多種來源擷取資料，例如Adobe解決方案、雲端型儲存、協力廠商軟體和您的CRM。 請參閱下面的[來源](#sources)區段以瞭解更多資訊。 |

**[!DNL Real-Time Customer Data Platform]個量度**

Real-time Customer Data Platform (Real-Time CDP)首頁包含量度控制面板，會在您登入Real-Time CDP時顯示。

首頁只是量度卡片出現的其中一個位置。 Real-Time CDP會在您整個體驗中提供量度卡片。 這些量度會通知您系統中的資料、設定檔和區段對象。

如果您登入Real-Time CDP時系統中沒有資料，首頁上的儀表板不會出現。 在此情況下，首頁會提供初次使用者體驗的學習資料。 收集資料後，控制面板會自動更新，以顯示有關該資料的資訊。

若要深入瞭解，請參閱[Real-time Customer Data Platform量度概觀](../../rtcdp/home-page-dashboards.md)

## [!DNL Destinations] {#destinations}

[!DNL Destinations]是預先建立的整合，與Adobe Real-time Customer Data Platform支援的目的平台，以順暢的方式為這些合作夥伴啟用資料。 如需詳細資訊，請閱讀[目的地概觀](../../destinations/home.md)文章。

**可用的目的地**

在11月版本中，Adobe的Real-time Customer Data Platform支援以下目的地：

* Advertising： [!DNL Google]
* 電子郵件行銷： Adobe Campaign，[!DNL Salesforce Marketing Cloud]，[!DNL Responsys]，[!DNL Oracle Eloqua]

如需每個目的地的相關資訊，請參閱[目的地目錄](../../destinations/catalog/overview.md)。

**已知限制**

* 在啟動流程（「排程」步驟）中允許自訂啟動排程的控制不適用於初始核發。
* 目前無法編輯或刪除目的地設定。 若要解決此限制，您可以啟用或停用[目的地詳細資訊頁面](../../destinations/ui/destination-details-page.md)右上角的目的地。
* 連線至您的目的地或儲存體帳戶時，目前沒有驗證帳戶詳細資料、路徑或認證。 請確定您輸入的認證正確無誤，並仔細檢查是否有拼字錯誤或拼字錯誤。
* 初次發行時未進行認證更新。 帳戶過期或需要重新整理後，您必須建立新的目的地連線，並重新對應您先前對應的區段。

## 來源 {#sources}

Adobe Experience Platform可從外部來源擷取資料，同時允許您使用[!DNL Platform]服務來建構、加標籤及增強該資料。 您可以從多種來源擷取資料，例如Adobe解決方案、雲端儲存、協力廠商軟體和您的CRM系統。

[!DNL Experience Platform]提供RESTful API和互動式UI，讓您輕鬆設定各種資料提供者的來源連線。 這些來源連線可讓您驗證儲存系統和CRM服務、設定擷取執行時間，以及管理資料擷取輸送量。

**主要功能**

| 功能 | 說明 |
| ---------- | ------------ |
| 來源UI | 用於建立、檢視和管理來源連線的新使用者介面。 |
| CRM聯結器工作流程改版 | 建立和管理[!DNL Microsoft Dynamics]和[!DNL Salesforce]聯結器的全新直覺式UI工作流程。 |
| 雲端儲存的聯結器支援 | 聯結器現在可以存取雲端儲存。 新來源包括[!DNL Amazon S3]、[!DNL Azure Blob]和FTP/SFTP伺服器。 |

**已知問題**

* 適用於雲端儲存空間的Source聯結器不支援擷取壓縮檔案。

如需來源的詳細資訊，請參閱[來源概觀](../../sources/home.md)。

## [!DNL Data Science Workspace] {#dsw}

Adobe Experience Platform [!DNL Data Science Workspace]可讓資料科學家透過建置和操作機器學習模型，順暢地從Adobe應用程式和協力廠商系統的資料和內容產生深入分析。 [!DNL Data Science Workspace]與[!DNL Platform]緊密整合，並支援端對端資料科學生命週期，包括探索和準備XDM資料，接著開發和操作模型，以使用機器學習深入分析自動豐富[!DNL Real-Time Customer Profile]。

**新功能**

| 功能 | 說明 |
| -----------| ---------- |
| 使用[!DNL Platform] SDK的資料存取 | [!DNL Python]中預先建立的配方和啟動器筆記本現在會使用[!DNL Platform] SDK來存取資料。 |
| 沙箱支援 | 支援即將推出的沙箱功能（目前為測試版），包括能夠將筆記本和配方隔離到開發或生產沙箱中。 如需詳細資訊，請參閱[沙箱概觀](../../sandboxes/home.md)。 |

如需詳細資訊，請參閱[資料科學Workspace概觀](../../data-science-workspace/home.md)。

## [!DNL Experience Data Model] (XDM)系統 {#xdm}

標準化和互通性是[!DNL Experience Platform]背後的重要概念。 [!DNL Experience Data Model] (XDM)由Adobe驅動，致力於標準化客戶體驗資料並定義客戶體驗管理的結構描述。

XDM是公開記錄的規格，旨在改善數位體驗的效能。 它為任何應用程式提供通用結構和定義，以便與Adobe Experience Platform上的服務通訊。 只要遵循XDM標準，所有客戶體驗資料都能整合到共同表現中，以更快、更整合的方式提供深入分析。 您可以從客戶行為中獲得有價值的分析，透過區段定義客戶對象，並使用客戶屬性實現個人化的目的。

**新功能**

| 功能 | 說明 |
| ---------- | ------------ |
| 通知結構描述 | 新結構描述，代表資料擷取程式期間傳送的通知資料。 |
| AdobeAdCloud DSP結構描述 | 已新增五個新結構描述，以代表Adobe Advertising Cloud需求端平台(DSP)中繼資料：位置、行銷活動、套件、廣告商、帳戶。 |
| ExperienceEvent實作詳細資料結構欄位群組 | 新的ExperienceEvent欄位群組，可新增標準欄位以儲存有關用於收集事件的軟體的資訊。 |
| [!DNL Profile Privacy]欄位群組 | 新增設定檔欄位群組，新增欄位以接受[!DNL Real-Time Customer Profile]的一般退出和銷售/共用退出訊號。 |
| `xdm:alternateDisplayInfo`的格式限制 | `xdm:alternateDisplayInfo`的「標題」和「說明」欄位都必須是字串，才能通過驗證。 |
| 名稱變更： XDM [!DNL Individual Profile] | 「XDM [!DNL Profile]」類別的「標題」已更新為「XDM [!DNL Individual Profile]」。 類別的正式`$id`尚未變更。 |

**已知問題**

* 無。

若要進一步瞭解如何使用[!DNL Schema Registry] API和[!DNL Schema Editor]使用者介面來使用XDM，請閱讀[XDM系統檔案](../../xdm/home.md)。

## [!DNL Real-Time Customer Profile] {#profile}

Adobe Experience Platform 讓您能夠為客戶提供一致且相關的協調體驗，無論他們何時何地與您的品牌互動。透過[!DNL Real-Time Customer Profile]，您可以看到結合來自多個管道（包括線上、離線、CRM和第三方資料）之資料的每個個別客戶的整體檢視。 [!DNL Profile]可讓您將不同的客戶資料合併成統一的檢視表，針對每個客戶互動提供可採取行動且附有時間戳記的說明。

| 功能 | 說明 |
| -----------| ---------- |
| [!DNL Profile]查閱的增強功能 | 使用者現在可以使用參照描述元和相關實體來查詢設定檔。 |
| 清理指定資料集的資料 | 使用者現在可以使用[!DNL Profile]系統作業API，刪除指定資料集或批次的資料。 |
| Edge [!DNL Profile]查詢增強功能 | 應用程式現在可以使用指定設定檔的任何身分來查詢Edge [!DNL Profile]。 |
| 為每個投影設定合併原則 | 應用程式現在可以設定每個投影的合併原則，以產生由特定合併原則所控管的資料檢視。 |
| 計算屬性 | 計算屬性會根據其他值、計算和運算式自動計算欄位值。 運算屬性會在設定檔層級上操作，以根據傳入事件、傳入事件和設定檔資料，或傳入事件、設定檔資料和歷史事件來彙總值，例如「總購買」、「期限值」或「漏斗狀態」。 |

**錯誤修正**

* 合併原則建立工作流程中可用ID拼接策略的簡化清單。

**已知問題**

* 無。

如需[!DNL Real-Time Customer Profile]的詳細資訊，包括使用[!DNL Profile]資料的教學課程和最佳實務，請閱讀[即時客戶個人檔案總覽](../../profile/home.md)。

## [!DNL Segmentation Service] {#segmentation}

Adobe Experience Platform [!DNL Segmentation Service]提供使用者介面和RESTful API，可讓您從[!DNL Real-Time Customer Profile]資料建立區段並產生對象。 這些區段是在[!DNL Platform]上集中設定和維護，讓任何Adobe應用程式都能輕鬆存取。

[!DNL Segmentation Service] 會說明區分客戶群中可行銷的一群人的標準，從而定義設定檔的特定子集。區段的基礎可能是記錄資料 (例如人口統計資訊) 或表示客戶與您的品牌互動的時間序列事件。

| 功能 | 說明 |
| -----------| ---------- |
| 已排程分段 | 使用者現在可以透過UI和API為所有區段啟用已排程的區段評估。 啟用後，每天將會評估所有區段一次。 這不會影響依需求分段功能，這些功能會如先前般繼續運作。<br/><br/>注意：排程的區段功能無法用於[!DNL XDM Individual Profile]擁有五個以上合併原則的沙箱。 |
| 串流區段 | 支援持續評估區段（串流區段），可在資料傳入[!DNL Platform]時評估大部分割槽段規則。 此功能表示區段會籍將是最新狀態，不需要執行排程的區段工作。 有些例外情況適用，例如使用多實體關係或擴充負載的區段。 |
| 區段作為建置區塊 | 使用區段產生器UI建立區段時，使用者現在可以使用先前定義的區段作為其他區段的建置區塊。 <ul><li>參考目前的對象成員資格：當人員進出對象時進行更新。</li><li>複製邏輯：取得選取的區段定義，並將其複製到新區段中。</li></ul> |
| 依ID名稱空間檢視區段會籍 | 區塊會籍現在可依ID名稱空間（電子郵件、ECID和總數）檢視。 |
| RBAC支援 | 「區段產生器」現在支援基本角色型存取控制項和許可權。 |
| 加強支援[!DNL Platform]與Adobe解決方案之間的外部受眾共用 | 在對象數量很大或先驗未知的情況下，使用者現在可以引進外部（非[!DNL Experience Platform]）對象中繼資料。 此版本包含已布建解決方案聯結器的客戶的存取[!DNL Audience Manager]中繼資料。 此對象中繼資料可用於區段產生器，以建立新的[!DNL Experience Platform]區段。 <br/><br/>此外，在[!DNL Experience Platform]中建立的區段現在可用於整合式Adobe解決方案，包括[!DNL Audience Manager]、[!DNL Target]和[!DNL Ad Cloud]。 |

**錯誤修正**

* 修正在巢狀關聯的情況下導致多實體分段傳回零設定檔的問題。
* 修正排除邏輯傳回誤導結果的問題。
* 改善多實體資料夾的可讀性。 它們現在會顯示XDM類別的易記名稱。
* 修正同一XDM資料夾出現多個副本的間歇性問題。
* 現在會產生訊息，以在所選合併原則沒有區段預估時通知使用者。

**已知問題**

* 無。

若要深入瞭解[!DNL Segmentation Service]，請閱讀[分段服務總覽](../../segmentation/home.md)。
