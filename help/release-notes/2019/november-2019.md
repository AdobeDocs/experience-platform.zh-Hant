---
title: Adobe Experience Platform發行說明2019年11月
description: 2019年11月為Adobe Experience Platform發佈的說明。
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

對現有功能的更新：
* [[!DNL Data Science Workspace]](#dsw)
* [[!DNL Experience Data Model (XDM) System]](#xdm)
* [[!DNL Real-Time Customer Profile]](#profile)
* [[!DNL Segmentation Service]](#segmentation)

## [!DNL Real-Time Customer Data Platform] {#rtcdp}

Real-time Customer Data Platform(Real-Time CDP)以Adobe Experience Platform為基礎，幫助各公司將已知和未知的資料匯集在一起，在整個客戶旅程中通過智慧決策激活客戶配置檔案。 Real-Time CDP公司將多個企業資料源結合起來，即時建立統一的配置檔案，這些配置檔案可用於在所有渠道和設備上提供一對一的個性化客戶體驗。

[!DNL Real-Time Customer Data Platform] 包括用於資料治理、身份管理、高級細分和資料科學的工具，以便您能夠構建配置檔案和定義受眾，並獲得豐富的見解，同時能夠實施嚴格的資料治理策略。

Adobe可以連接到大型合作夥伴生態系統，更不用說與Adobe Experience Cloud的本機整合了，因此您可以無縫激活這些受眾，並跨所有渠道（從現場或應用內個性化到電子郵件、付費媒體、呼叫中心、連接設備等）提供絕佳的客戶體驗。

對於Real-Time CDP，您可以：

* 通過從整個企業流式收集客戶資料，實現客戶的單一視圖。
* 負責任地管理配置檔案，並對已知和未知標識符進行可信治理和隱私控制。
* 借助Adobe Sensei支援的人工智慧和機器學習，為營銷人員構建可操作的洞見和擴大受眾。
* 跨所有渠道和目標即時提供個性化體驗。

有關詳細資訊，請參見 [Real-time Customer Data Platform文檔](../../rtcdp/overview.md)。

**主要功能**

| 功能 | 說明 |
|---|---|
| 目的地 | 預構建的與受Adobe支援的目標平台的整合 [!DNL Real-Time Customer Data Platform] 以無縫方式將資料激活給這些合作夥伴。 請參閱 [目標](#destinations) 下面的。 |
| 首頁度量儀表板 | Real-time Customer Data Platform(Real-Time CDP)首頁包含一個顯示有關配置檔案和段的資訊的度量儀表板。 首頁還包含到學習材料的連結。 請參閱 [Real-time Customer Data Platform度量](#real-time-customer-data-platform-metrics) 下。 |
| 來源 | 您可以從多種來源(如Adobe解決方案、基於雲的儲存、第三方軟體和您的CRM)中接收資料。 查看 [源](#sources) 以瞭解更多資訊。 |

**[!DNL Real-Time Customer Data Platform]度量**

登錄到Real-Time CDP時，將顯示Real-time Customer Data Platform(Real-Time CDP)首頁，其中包含度量儀表板。

首頁只是顯示度量卡的位置之一。 Real-Time CDP在您的整個體驗中提供度量卡。 這些指標將通知您系統中的資料、配置檔案和段訪問群體。

如果登錄Real-Time CDP時系統中沒有資料，則首頁上的儀表板不會顯示。 在這種情況下，首頁為第一次用戶體驗提供學習材料。 在收集資料時，儀表板會自動更新以顯示有關該資料的資訊。

要瞭解更多資訊，請參閱 [Real-time Customer Data Platform度量概述](../../rtcdp/home-page-dashboards.md)

## [!DNL Destinations] {#destinations}

[!DNL Destinations] 是預構建的與AdobeReal-time Customer Data Platform支援的目標平台的整合，可無縫地向這些合作夥伴激活資料。 有關詳細資訊，請閱讀 [目標概述](../../destinations/home.md) 文章。

**可用目標**

11月份發佈後，AdobeReal-time Customer Data Platform支援以下目的地：

* Advertising: [!DNL Google]
* 電子郵件營銷：Adobe Campaign, [!DNL Salesforce Marketing Cloud]。 [!DNL Responsys]。 [!DNL Oracle Eloqua]

查看 [目標目錄](../../destinations/catalog/overview.md) 的子菜單。

**已知限制**

* 允許在激活流（計畫步驟）中自定義激活計畫的控制項在初始版本中不可用。
* 當前無法編輯或刪除目標配置。 要繞過此限制，可以啟用或禁用位於 [目標詳細資訊頁面](../../destinations/ui/destination-details-page.md)。
* 連接到目標或儲存帳戶時，當前沒有驗證帳戶詳細資訊、路徑或憑據。 確保輸入了正確的憑據並對拼寫錯誤或拼寫錯誤進行了雙重檢查。
* 初始版本中沒有憑據續訂。 帳戶過期或需要刷新後，必須建立新的目標連接並重新映射以前映射的段。

## 來源 {#sources}

Adobe Experience Platform可以從外部源接收資料，同時允許您使用 [!DNL Platform] 服務。 您可以從多種來源(如Adobe解決方案、基於雲的儲存、第三方軟體和您的CRM系統)接收資料。

[!DNL Experience Platform] 提供了REST風格的API和互動式UI，使您可以輕鬆地為各種資料提供程式設定源連接。 通過這些源連接，您可以驗證儲存系統和CRM服務，設定接收運行時間，並管理資料接收吞吐量。

**主要功能**

| 功能 | 說明 |
| ---------- | ------------ |
| 源UI | 用於建立、查看和管理源連接的新用戶介面。 |
| 修改CRM連接器的工作流 | 用於建立和管理的新的直觀UI工作流 [!DNL Microsoft Dynamics] 和 [!DNL Salesforce] 連接器。 |
| 用於雲儲存的連接器支援 | 連接器現在可以訪問基於雲的儲存。 新源包括 [!DNL Amazon S3]。 [!DNL Azure Blob]和FTP/SFTP伺服器。 |

**已知問題**

* 基於雲的儲存的源連接器不支援壓縮檔案的接收。

有關源的詳細資訊，請參見 [源概述](../../sources/home.md)。

## [!DNL Data Science Workspace] {#dsw}

Adobe Experience Platform [!DNL Data Science Workspace] 使資料科學家能夠通過構建和操作機器學習模型，跨Adobe應用程式和第三方系統無縫地從資料和內容中生成洞見。 [!DNL Data Science Workspace] 與 [!DNL Platform] 並為端到端資料科學生命週期提供動力，包括探索和準備XDM資料，然後開發和實施模型以自動豐富 [!DNL Real-Time Customer Profile] 和機器學習的見解。

**新功能**

| 功能 | 說明 |
| -----------| ---------- |
| 使用 [!DNL Platform] SDK | 預構建的配方和啟動程式筆記本 [!DNL Python] 現在使用 [!DNL Platform] 用於訪問資料的SDK。 |
| 沙箱支援 | 支援即將進行的沙盒功能（目前在試用版中），包括將筆記型電腦和配方隔離到開發或生產沙盒中的能力。 如需詳細資訊，請參閱[沙箱概觀](../../sandboxes/home.md)。 |

有關詳細資訊，請參見 [資料科學工作區概述](../../data-science-workspace/home.md)。

## [!DNL Experience Data Model] (XDM)系統 {#xdm}

標準化和互操作性是其背後的關鍵概念 [!DNL Experience Platform]。 [!DNL Experience Data Model] (XDM)在Adobe的推動下，致力於標準化客戶體驗資料並定義客戶體驗管理模式。

XDM是一種公開記錄的規範，旨在提高數字型驗的威力。 它為任何與Adobe Experience Platform服務通信的應用程式提供了共同的結構和定義。 通過遵守XDM標準，所有客戶體驗資料都可以納入到一個通用的表示形式中，以更快、更整合的方式提供洞察力。 您可以從客戶操作中獲得有價值的見解，通過細分市場定義客戶受眾，並將客戶屬性用於個性化目的。

**新功能**

| 功能 | 說明 |
| ---------- | ------------ |
| 通知架構 | 表示在資料接收過程中發送的通知資料的新架構。 |
| AdobeAdCloud架DSP構 | 新增了5個新模式來表示Adobe Advertising Cloud需求方平台(DSP)元資料：Placement 、 Campaign 、 Package 、 Dactimer 、 Account。 |
| ExperienceEvent實現詳細資訊架構欄位組 | 添加標準欄位以儲存有關用於收集事件的軟體的資訊的新ExperienceEvent欄位組。 |
| [!DNL Profile Privacy] 欄位組 | 新的配置檔案欄位組，添加欄位以接受常規退出和銷售/共用退出信號 [!DNL Real-Time Customer Profile]。 |
| 格式約束 `xdm:alternateDisplayInfo` | 的「標題」和「說明」欄位 `xdm:alternateDisplayInfo` 必須都是字串才能通過驗證。 |
| 名稱更改：XDM [!DNL Individual Profile] | &quot;XDM&quot;的&quot;標題&quot; [!DNL Profile]&quot;類已更新為&quot;XDM [!DNL Individual Profile]。 正式 `$id` 班裡沒有變。 |

**已知問題**

* None.

瞭解有關使用XDM的更多資訊 [!DNL Schema Registry] API和 [!DNL Schema Editor] 用戶介面，請閱讀 [XDM系統文檔](../../xdm/home.md)。

## [!DNL Real-Time Customer Profile] {#profile}

Adobe Experience Platform使您能夠為您的客戶提供協調、一致和相關的體驗，無論客戶在何處或何時與您的品牌進行交互。 與 [!DNL Real-Time Customer Profile]，您可以看到每個客戶的整體視圖，該視圖將來自多個渠道的資料組合在一起，包括線上、離線、CRM和第三方資料。 [!DNL Profile] 允許您將全異的客戶資料整合到一個統一視圖中，為每個客戶交互提供一個可操作且時間戳記的帳戶。

| 功能 | 說明 |
| -----------| ---------- |
| 增強 [!DNL Profile] 查找 | 用戶現在能夠使用引用描述符和相關實體查找配置檔案。 |
| 清除給定資料集的資料 | 用戶現在可以使用 [!DNL Profile] 系統作業API。 |
| 邊緣 [!DNL Profile] 查詢增強 | 應用程式現在可以查詢邊緣 [!DNL Profile] 以給定檔案的身份。 |
| 按投影配置合併策略 | 應用程式現在可以根據投影配置合併策略，以便生成由特定合併策略管理的資料視圖。 |
| 計算屬性 | 計算屬性根據其他值、計算和表達式自動計算欄位的值。 計算屬性在配置檔案級別上基於傳入事件、傳入事件和配置檔案資料或傳入事件、配置檔案資料和歷史事件對聚合值（如「總購買」、「生存期值」或「漏斗狀態」）進行操作。 |

**錯誤修正**

* 合併策略建立工作流中可用ID縫合策略的簡化清單。

**已知問題**

* None.

有關 [!DNL Real-Time Customer Profile]包括教程和最佳實踐 [!DNL Profile] 資料，請閱讀 [即時客戶概要資訊概述](../../profile/home.md)。

## [!DNL Segmentation Service] {#segmentation}

Adobe Experience Platform [!DNL Segmentation Service] 提供了用戶介面和REST風格的API，允許您生成段並從您的 [!DNL Real-Time Customer Profile] 資料。 這些段在 [!DNL Platform]使任何Adobe應用程式都可輕鬆訪問。

[!DNL Segmentation Service] 通過描述區分客戶群中可銷售人員組的標準來定義特定配置檔案子集。 段可以基於記錄資料（如人口統計資訊）或表示客戶與您品牌的交互的時間序列事件。

| 功能 | 說明 |
| -----------| ---------- |
| 計畫的分段 | 用戶現在可以通過UI和API為所有段啟用計畫段評估。 啟用後，將每天對所有段進行一次評估。 這不會影響按需細分功能，這些功能繼續像以前一樣工作。<br/><br/>注：計畫的分割功能不能用於具有五個以上合併策略的沙箱 [!DNL XDM Individual Profile]。 |
| 流分段 | 支援對段的連續評估（流分段），允許在資料傳入時評估大多數段規則 [!DNL Platform]。 此功能意味著段成員身份將是最新的，無需運行計畫的分段作業。 某些例外適用，例如使用多實體關係的段或具有豐富負載的段。 |
| 段作為構件塊 | 使用段生成器UI建立段時，用戶現在可以使用先前定義的段作為附加段的構造塊。 <ul><li>參考當前受眾成員身份：隨著觀眾的進出而更新。</li><li>複製邏輯：將選定段定義複製到新段中。</li></ul> |
| 按ID命名空間查看段成員身份 | 現在，可以通過ID命名空間（電子郵件、ECID和總計數）查看段成員身份。 |
| RBAC支援 | 段生成器現在支援基本的基於角色的訪問控制和權限。 |
| 增強了對外部受眾在以下之間共用的支援 [!DNL Platform] 和Adobe解決方案 | 用戶現在可以引入外部(非[!DNL Experience Platform])受眾元資料在受眾數量較大或事先不知道的情況下。 此版本包括訪問 [!DNL Audience Manager] 為已配置解決方案連接器的客戶提供的元資料。 此受眾元資料可在段生成器中使用以建立新 [!DNL Experience Platform] 段。 <br/><br/> 此外，在 [!DNL Experience Platform] 現在將可用於整合Adobe解決方案，包括 [!DNL Audience Manager]。 [!DNL Target], [!DNL Ad Cloud]。 |

**錯誤修正**

* 修復了導致多實體分割在嵌套關係的情況下返回零配置檔案的問題。
* 修復了排除邏輯返回誤導性結果的問題。
* 提高了多實體資料夾的可讀性。 現在，它們顯示XDM類的友好名稱。
* 修復了出現同一XDM資料夾的多個副本的間歇性問題。
* 現在產生消息以通知用戶如果所選合併策略的段估計不可用。

**已知問題**

* None.

瞭解有關 [!DNL Segmentation Service]，請閱讀 [分段服務概述](../../segmentation/home.md)。
