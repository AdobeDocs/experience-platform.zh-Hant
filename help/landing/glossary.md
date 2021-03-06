---
keywords: Experience Platform；首頁；熱門主題
solution: Experience Platform
title: Adobe Experience Platform辭彙表
topic-legacy: getting started
description: Experience Platform 重要術語表。
exl-id: 00eae5f5-7dfa-45ac-aff9-9e1769a3a53a
source-git-commit: c0f01efa224bffb5b435e2f247e793edfbc576b9
workflow-type: tm+mt
source-wordcount: '7428'
ht-degree: 0%

---

# Adobe Experience Platform 術語 {#adobe-experience-platform-glossary}

## A

**訪問控制**:基於角色的訪問控制使管理員能夠將訪問權限和權限分配給Experience Platform用戶。 權限包括查看和/或使用Experience Platform功能（如建立沙箱、定義方案和管理資料集）的能力。

**訪問密鑰ID**:訪問密鑰ID是與 [!DNL Amazon] S3密鑰訪問密鑰。 訪問密鑰ID和密鑰訪問密鑰一起用於簽名 [!DNL Amazon Web Services] (AWS)請求。

**操作**:在標籤上下文中，操作是特定類型的規則元件，用於定義事件發生和評估和傳遞條件後應發生的情況。

**激活**:激活是用戶將段或配置檔案映射到目標(如 [!DNL Oracle Eloqua]。 [!DNL Google]或 [!DNL Salesforce Marketing Cloud]。

**活動**:在 [!DNL Offer Decisioning]，活動包含通知選擇聘用的邏輯。

**管理員**:您組織中的一個或多個個人可以配置和自定義在Adobe Admin ConsoleExperience Platform的權限。

**Adobe Admin Console**:Adobe Admin Console為管理Adobe產品權利和組織訪問提供了一個中心位置。 通過控制台，管理員可以授予用戶組對各種平台功能（如「管理資料集」、「查看資料集」或「管理配置式」）的訪問權限。

**Adobe Experience Platform**:Adobe Experience Platform在整個企業中標準化了資料和內容，為即時消費者配置提供了動力，實現了資料科學，並加快了內容速度，以推動客戶體驗個性化。

**Adobe Experience Platform查詢服務**:使資料分析員能夠查詢事件和配置檔案，以便在分析和機器學習中使用。 使用查詢服務，資料科學家和分析師可以提取儲存在Experience Platform中的所有資料集(包括行為資料以及銷售點(POS)、客戶關係管理(CRM)等)，並查詢這些資料集以回答有關資料的特定問題。

**Adobe Experience Platform分段服務**:支援構建段並根據即時客戶配置檔案資料生成受眾。 然後，這些訪問群體可以導出到Data Lake中他們自己的資料集。

**Adobe智慧服務**:智慧服務(如Attribution AI和客戶AI)是機器學習、基於人工智慧的模型，專門構建，需要Experience Platform來運行和操作。

**Adobe I/O**:Adobe I/O是Experience Platform的一部分，可讓開發人員訪問整合、擴展和定制平台所需的所有內容，包括API、事件、開發人員控制台和有用的工具。

**Adobe Sensei**:Adobe Sensei是Experience Platform的情報框架。 它還提供一套人工智慧服務，使品牌能夠增強提供即時個性化客戶體驗的能力。

**AmazonS3桶**: [!DNL Amazon S3] 儲存桶是儲存在 [!DNL Amazon] 生態系統。 儲存段包含對象，每個對象都使用唯一的開發人員分配密鑰進行儲存和檢索。

**AmazonS3連接器**:的 [!DNL Amazon] S3連接器允許Experience Platform客戶安全地連接和訪問其 [!DNL Amazon] S3資料。

**追加保存策略**:「追加」保存策略是指定第三方資料以通過連接進行接收，並在資料集末尾附加任何新資料或行時使用的選項。 以前攝取的行保持不變，僅將自上次計畫運行後建立的行攝取到Experience Platform。 源系統中更改的所有行在Experience Platform中保持不變。

**陣列**:陣列用於具有相同資料類型的有序元素。

**人工智慧**:人工智慧是電腦系統的理論和發展，能夠執行通常需要人類智慧的任務，如視覺感知、語音識別、決策和語言間的翻譯。

**屬性**:屬性是指定的特徵，表示配置檔案。

**屬性合併**:使用即時客戶配置檔案API定義合併策略時， `attributeMerge` object指示在發生資料衝突時合併策略優先處理配置檔案屬性的方式。 它相當於選擇 [!UICONTROL 合併方法] 在平台UI中定義合併策略時。

**Attribution AI**: [!DNL Attribution AI] 是由Adobe Sensei公司支援的智慧服務，在整個客戶生命週期中提供算法多通道歸屬功能。

**觀眾**:受眾是符合段定義標準的結果配置檔案集。

**受眾大小**:受眾規模是滿足段定義標準並符合受眾成員資格的配置檔案總數。

**受眾快照**:受眾快照捕獲在分段時符合段標準的所有配置檔案。

## B

**回填**:對於計畫的源，回填選項允許接收歷史資料。

**回填期間**:回填期間是設定通過源連接接收第三方歷史資料的時間長度的選項。 選擇「forever」的回填期將將源資料的整個歷史記錄錄入Experience Platform。

**批**:批是一組在一段時間內收集並作為單個單位一起處理的資料。 資料集由多個批處理組成。

**批ID**:批ID是Adobe生成的資料批的標識符。

**批量攝取**:批處理接收允許您將資料作為批處理檔案接收到Experience Platform中。 批次是多個資料單位，由一或多個要作為一個單位進行內嵌的檔案所組成。

**批分段**:批分段是持續資料選擇過程的替代方法，它通過段定義一次移動所有配置檔案資料以產生相應的受眾。 建立後，將保存並儲存此段，以便導出該段供使用。

**生成**:在標籤上下文中，生成是一個檔案或一組檔案，包含執行庫內包含的業務邏輯所需的所有配置和代碼，允許您在網站或移動應用上部署該庫。

**商業智慧工具**:業務智慧(BI)工具主要與 [!DNL Experience Platform Query Service]。 BI工具是一種應用程式軟體，可收集和處理來自內部和外部系統的大量非結構化資料。

## C

**封頂**:在 [!DNL Offer Decisioning]，在判定規則中使用capping（也稱為頻率capping）來定義提供的次數。 有兩種類型的大寫：在合併的目標受眾中可以建議多少次（稱為「全局上限」），向同一最終用戶建議一次要約的次數（稱為「概要上限」）。

**目錄**:在源和目的地的上下文中，目錄是一個庫，它具有與Adobe應用程式和第三方技術的可用連接。 不要與 [!DNL Catalog Service]。

**[!DNL Catalog Service]**: [!DNL Catalog Service] (有時 [!DNL Catalog])是Adobe Experience Platform內資料位置和譜系的記錄系統。 當所有被攝入Experience Platform的資料都作為檔案和目錄儲存在資料湖中時， [!DNL Catalog] 保存這些檔案和目錄的元資料和說明，以便進行查找、監視和資料管理。

**類**:在體驗資料模型(XDM)中，類定義用於構建架構的最小欄位集，並定義架構所表示的業務對象的基本行為。

**客戶端**:客戶端是連接到 [!DNL Query Service] 通過PostgreSQL協定或HTTP API。

**集合**:在 [!DNL Offer Decisioning]，集合是基於由商家定義的預定義條件（例如要約的類別）的要約的子集。

**與PII營銷活動結合**:將任何個人身份資訊(PII)與匿名資料相結合的市場營銷操作。 從廣告網路、廣告伺服器和第三方資料提供商獲取的資料合同通常包括禁止使用直接可識別資料的此類資料的具體合同。

**命令行介面**:命令行介面是基於文本的工具，可用於連接到 [!DNL Query Service] 執行原始查詢。

**組合**:組合是組成架構的元件。

**條件**:在標籤的上下文中，條件是一個規則元件，它計算必須返回的邏輯語句 `true` 或 `false`。 所有條件都必須評估為 `true` 並且所有例外條件必須計算 `false` 執行規則上的任何操作之前。

**控制台**:在 [!DNL Query Service]，控制台提供有關查詢狀態和操作的資訊。 控制台顯示與 [!DNL Query Service]、正在執行的查詢操作以及這些查詢產生的任何錯誤消息。

**合同(「C」)標籤**:合同(「C」)資料使用標籤用於對具有合同義務或與客戶的資料治理策略相關的資料進行分類。

**C1合同標籤**:A `C1` 合同資料使用標籤指定資料只能以聚合形式從Adobe Experience Cloud導出，而不包括單個或設備標識符。 例如，源自社交網路的資料。

**C2合同標籤**:A `C2` contract data usage標籤指定無法導出到第三方的資料。 一些資料提供者在其合同中規定了禁止從最初收集的地方導出資料的條款。 例如，社交網路合同通常會限制您從它們接收到的資料的傳輸。 C2比C1限制性更強，C1隻需要聚合和匿名資料。

**C3合同標籤**:A `C3` contract data usage標籤指定不能與直接可識別資訊組合或以其他方式使用的資料。 一些資料提供商在合同中有條款，禁止將資料與直接可識別資訊合併或使用。 例如，從廣告網路、廣告伺服器和第三方資料提供商獲取的資料合同通常包括對使用直接可識別資料的具體合同禁令。

**C4合同標籤**:A `C4` contract data usage標籤指定資料不能用於針對任何廣告或內容，無論是現場還是跨站點。 C4是限制性最強的標籤，因為它包含C5、C6和C7標籤。

**C5合同標籤**:A `C5` 合同資料使用標籤指定資料不能用於基於興趣的內容或廣告的跨站點目標。 如果滿足以下三個條件，即基於興趣的目標或個性化：現場採集的資料用於推斷用戶的興趣；用於其他上下文，如其他站點或應用；並用於根據這些推理選擇服務哪些內容或廣告。

**C6合同標籤**:A `C6` contract data usage標籤指定資料不能用於現場廣告目標。 現場廣告目標包括在您組織的網站或應用上選擇和發佈廣告，或衡量此類廣告的交付和效果。 這包括使用先前收集的關於用戶興趣的現場資料來選擇廣告、處理關於顯示哪些廣告的資料、顯示時間和地點的資料以及用戶是否採取了與廣告相關的任何操作，如選擇廣告或購買。

**C7合同標籤**:A `C7` contract data usage標籤指定資料不能用於內容的現場目標。 現場內容目標包括選擇和傳遞您組織網站或應用上的內容，或衡量此類內容的傳遞和有效性。 這包括先前收集的有關用戶對選擇內容的興趣的資訊、處理有關顯示內容的資料、顯示時間、顯示時間、位置以及用戶是否採取了與內容相關的任何操作（例如選擇內容）的資料。

**C8合同標籤**:A `C8` 合同資料使用標籤指定資料不能用於測量您組織的網站或應用。 這不包括基於興趣的目標，即收集有關您使用此服務以隨後在其他上下文中個性化內容和/或廣告的資訊。

**C9合同標籤**:A `C9` contract data usage標籤指定資料不能在資料科學工作流中使用。 一些合同明確禁止資料科學使用的資料。 有時，這些措辭的措辭禁止將資料用於人工智慧(AI)、機器學習(ML)或建模。

**C10合同標籤**:A `C10` contract data usage標籤指定資料不能用於縫合標識激活。 某些資料使用策略限制使用縫合標識資料進行個性化。 的 `C10` 如果段的合併策略使用「專用圖形」選項，則標籤將自動應用於段。

**「建立日期」列**:通過源連接指定第三方資料時，選擇「建立日期」列是一個選項。 選擇追加保存策略且資料集架構包含多個日期欄位時，必須從可用架構中選擇以指定「建立日期」鍵列。 選擇覆蓋保存策略時，「建立日期」選項不可用。

**按選擇建立表**:「建立表為選擇」(CTAS)是SQL命令，在作為完整有效SQL查詢的一部分執行時，該命令將指示 [!DNL Query Service] 將查詢結果保留在資料集中。 可以建立新結果集、覆蓋先前的結果或追加到先前的結果。

**跨站點資料**:跨站點資料是來自多個站點的資料的組合，包括現場資料和非現場資料的組合，或來自多個非現場源的資料的組合。

**跨站點目標營銷活動**:使用資料進行跨站點廣告目標的市場營銷操作。 來自多個站點的資料的組合，包括現場資料和非現場資料的組合或來自多個非現場源的資料的組合，稱為跨站點資料。 通常收集和處理跨站點資料以推斷客戶的興趣。

**自定義標識命名空間**:您的組織可以建立自定義標識命名空間以表示特定組織或業務案例的標識。

**自定義標籤**:自定義資料使用標籤允許您建立特定標籤並將其應用於滿足特定業務需求的資料欄位。

**客戶AI**:客戶AI是由Adobe Sensei提供的智慧服務，它用基於AI的特性豐富了客戶概況，並增強了客戶細分和目標化的能力。

## D

**每日**:在計畫檔案導出的上下文中，在用戶指定的時間將完整或增量檔案導出安排為從開始日期到結束日期的每天一次。

**資料字典**:在標籤的上下文中，資料字典（也稱為資料映射）是在屬性中定義的一組資料元素。

**資料元素**:在標籤的上下文中，資料元素是在規則和擴展中使用的指針，用於指向客戶端設備上存在的特定資料段。

**資料接收**:資料接收是將資料從源添加到Experience Platform的過程。 資料可以通過多種方式（包括流、批處理或通過源連接器添加）接收到平台。

**資料層**:在標籤的上下文中，資料層是客戶端設備上存在的資料結構，該資料結構包含有關查看頁面或螢幕的上下文的元資料。

**資料治理**:資料治理包括用於確保資料符合有關資料使用的法規和組織政策的戰略和技術。

**資料整合合作夥伴**:資料整合合作夥伴簡化並自動化了從200多個源到Experience Platform的大量資料的載入和轉換，而無需編寫代碼。

**資料集標籤**:資料使用標籤可以添加到資料集。 該資料集中的所有欄位將繼承該資料集的標籤。

**資料科學工作區**: [!DNL Data Science Workspace] 在Experience Platform中，客戶可以建立機器學習模型，利用跨平台和Adobe應用程式的資料建立智慧段、生成洞察力和提供預測，從而大大增強最終用戶的數字型驗。

**資料源**:資料源是用戶指定的資料源。 資料源的示例是移動應用、配置檔案和/或體驗事件、網站配置檔案事件或CRM。

**資料管理員**:資料管理員是負責管理、監督和實施組織資料資產的人員。 資料管理員還確保資料治理政策得到保護並得到維護，以符合政府法規和組織政策。

**資料流**:資料流是共用相同模式且由同一源發送的消息集或集合。

**資料類型**:資料類型是可重用的XDM資源，它定義了在分層表示中包含多個屬性的對象類型欄位。

**資料使用標籤**:資料使用標籤允許您對反映與隱私相關的考慮事項和符合法規和公司策略的合同條件的資料進行分類。 添加到資料集的資料使用標籤將繼承下來或應用到該資料集中的所有欄位。 資料使用標籤也可以直接應用於欄位。

**資料流**:資料流是從源流入平台並流出目的地的虛擬資料管道。

**資料流運行**:資料流運行是基於用戶指定的調度而進入Experience Platform的資料流。

**資料集**:資料集是用於資料集合（通常是表）的儲存和管理構造，該資料集包含模式（列）和欄位（行）。

**資料集ID**:Adobe生成的用於所攝取資料集的標識符。

**資料集輸出**:資料集輸出提供了一種機制，用於確定「將表建立為選擇」選項將用於特定 [!DNL Query Service] 跑。

**重複資料消除密鑰**:用戶定義的主鍵，它確定用戶希望對其配置檔案進行重複資料消除的標識&#x200B;。

**增量列**:增量列允許您選擇源資料欄位來表示增量接收的時間戳。

**增量保存策略**:增量保存策略是用於通過源連接接收第三方資料的選項。 該選項允許用戶指定新的或更改的源資料行被接收到Experience Platform。 將新行添加到資料集的末尾，並在Experience Platform的資料集中更新更改的行。

**描述符**:在體驗資料模型(XDM)中，描述符是描述欄位特定行為的與模式相關的元資料的附加集。 Experience Platform可以使用描述符來瞭解預期的模式行為，如兩個模式之間的關係。

**目標**:目標是任何終端節點的通用術語，例如Adobe應用程式、廣告平台、雲儲存服務或營銷服務，在這些端點中激活和傳遞受眾。

**目標類別**:目標類別是具有相似特徵的目標的分組。

**目標目錄**:目標目錄是Experience Platform中可用目標的清單。

**直接呼叫規則**:在標籤上下文中，直接調用規則是當直接從頁面調用時執行的規則，它繞過了事件檢測和查找系統。

**顯示名稱**:在體驗資料模型(XDM)中，顯示名稱是UI中顯示的欄位的用戶友好名稱。

## E

**合格報價**:合格的優惠可以始終如一地提供給配置檔案，因為它滿足上游定義的約束。

**資格規則**:在 [!DNL Offer Decisioning]，資格規則將應用於與日曆、計畫和封頂限制相關的配置檔案。

**電子郵件目標營銷活動**:在電子郵件目標市場活動中使用資料的市場營銷活動。

**嵌入代碼**:在標籤的上下文中，嵌入代碼是放置在站點或環境上的HTML中的指令碼標籤。 嵌入代碼指示瀏覽器在何處檢索生成。

**枚舉**:枚舉(enum)是一個XDM欄位，它被約束為一組預定義的值。

**環境**:在標籤上下文中，環境是一組部署說明，它指定生成的主機傳遞和檔案格式。 必須將庫與環境配對，才能生成庫。

**錯誤診斷**:錯誤診斷可為接收的批生成詳細的錯誤消息。 錯誤閾值允許您配置批失敗前可接受錯誤的百分比。

**事件**:在標籤的上下文中，事件是特定類型的規則元件，它是在客戶端設備上發生的開始執行規則的觸發器。

**事件實體**:在資料建模的上下文中，事件實體表示與客戶可以採取的操作、系統事件或任何其它您可能希望跟蹤隨時間變化的概念相關的概念。 屬於此類別的實體應由基於 [!DNL XDM ExperienceEvent] 類。

**事件**:事件是與配置檔案關聯的行為資料。

**體驗資料模型(XDM)** [!DNL Experience Data Model] (XDM)是一個開源框架，它使用標準架構來統一資料，以便與Experience Platform和Adobe Experience Cloud應用程式一起使用。 XDM標準化了資料的結構，並加快和簡化了從大量資料中獲取見解的過程。

**實驗**:一個實驗是通過用即時生產資料的樣本部分訓練實例來建立訓練模型的過程。 這不同於針對抑制test資料集測試的訓練模型。 這也不同於一些機器學習框架中的實驗的概念，在這個框架中，它實際上意味著一個示例建模項目。

**體驗事件**:「體驗事件」表示發生與客戶體驗相關的交互或事件時系統的快照。 「體驗事件」是不可改變的事實記錄，它表示發生的事實，而不進行聚合或解釋。 在經驗資料模型(XDM)中，此概念由 [!DNL XDM ExperienceEvent] 類。

**導出完整檔案**:包含選定段所有配置檔案資格的完整快照的導出檔案。

**導出增量檔案**:一系列導出檔案，其中第一個檔案是所選段的所有配置檔案資格的完整快照，而後續檔案是自上次導出以來的增量配置檔案資格。

**擴展**:在標籤的上下文中，擴展是添加到標籤屬性中的功能包。 擴展通常側重於特定的營銷或分析解決方案，並提供將該技術部署到客戶端環境中所需的工具。

**擴展包**:在標籤上下文中，擴展包是擴展開發人員建立和上載的ZIP檔案，它提供了標籤用戶在其屬性內安裝擴展所需的一切。 擴展包包含清單，該清單指定有關擴展的資訊、最終用戶配置標籤擴展的行為所需的HTML/JavaScript以及交付給客戶端環境的可執行JavaScript（如果需要）。

## F

**回退優惠**:回退優惠是當最終用戶不符合使用的集合中的任何優惠時顯示的預設優惠。

**特徵映射**:特徵映射是指將特徵從資料映射到機器學習模型所需的輸入和目標特徵的過程。

**欄位**:欄位是資料集的最低級別元素，由資料集的XDM架構定義。 每個欄位都有一個用於引用的名稱和一個類型，用於指示它所包含的資料類型。 欄位類型可以包括（但不限於）整數、數字、字串、布爾和對象。

**欄位組**:請參閱「架構欄位組」。

**欄位標籤**:欄位標籤是從資料集繼承或直接應用於欄位的資料治理標籤。

**欄位名**:欄位名稱用於引用查詢和下游服務中欄位的值。

**頻率**:在 [!DNL Query Service]，頻率確定定期計畫查詢的運行頻率。

## G

**地方科學**:地質是由GPS或RFID技術定義的虛擬地理邊界，使軟體能夠在移動設備進入或離開特定區域時觸發響應。

**GDPR（一般資料保護法規）**:《一般資料保護條例》(GDPR)是一個法律框架，為收集和處理歐盟（歐盟）內個人的個人資訊制定了指導方針。 GDPR規定了資料管理原則和個人權利，涵蓋了處理歐盟公民資料的所有公司。

**護欄**:護欄是指為資料和系統使用、效能優化和避免錯誤或意外結果在Adobe Experience Platform提供指導的閾值。 護欄可以參考您對許可權利的使用或資料的使用和處理。

## H

**主機**:在標籤上下文中，主機指定系統傳遞生成所需的位置、域和用戶憑據。

**每小時**:在計畫檔案導出的上下文中，計畫每3、6、8或12小時進行一次增量檔案導出。

## I

**身份**:標識是唯一表示單個客戶的標識符，如Cookie ID、設備ID或電子郵件ID。

**標識欄位**:標識欄位是XDM欄位，用於拼合來自多個資料源的單個客戶的資訊。 必須定義單個主標識，才能在即時客戶配置檔案中啟用方案。

**標識(「I」)標籤**:標識(「I」)資料使用標籤用於對可識別或聯繫特定人的資料進行分類。

**標識圖**:標識圖是針對單個客戶的縫合標識和連結標識之間的關係圖。 每個身份圖都隨客戶活動近即時更新。 資料中標識關係的公共結構由 [!UICONTROL 專用圖]作為每個個體身份圖的結構藍圖。

**標識命名空間**:標識命名空間定義標識符的上下文，如電子郵件地址或CRM ID。

**身份服務**: [!DNL Experience Platform Identity Service] 允許建立和管理標識類型，允許您跨設備和渠道連結客戶標識。 該服務將身份連結在一起的能力使即時客戶概要檔案能夠完整地代表每個客戶。

**身份拼接**:身份拼接是識別資料片段並將它們拼接在一起形成完整檔案記錄的過程。

**身份符號**:標識符號是標識命名空間的縮寫，可以在API中用作引用。

**標識值**:標識值與標識名稱空間結合，是表示唯一個人、組織或資產的標識符。 當跨配置檔案片段匹配記錄資料時，命名空間和標識值必須匹配。

**I1資料使用標籤**:的 `I1` 資料使用標籤用於對能夠直接識別或聯繫特定人而不是設備的資料進行分類。

**I2資料使用標籤**:的 `I2` 資料使用標籤用於對可以與任何其他資料組合使用的資料進行分類，以間接地識別或聯繫特定人。

**IMS組織**:IMS組織（有時稱為IMS組織）是用於標識公司或公司內跨Adobe產品的特定組的名稱。 管理員可以配置和管理對組織用戶的功能的訪問權限和權限。

**攝取**:請參閱資料攝取。

**攝取計畫**:接收計畫在從源到Experience Platform進行接收時提供基於時間的選項。

**輸入特徵**:在特徵映射中指定輸入特徵並由機器學習模型用於進行預測。

**[!DNL Intelligent Services]**: [!DNL Intelligent Services] 例如 [!DNL Attribution AI] 和 [!DNL Customer AI] 是機器學習、基於人工智慧的模型，需要Experience Platform(或Real-time Customer Data Platform等平台之上構建的應用程式)來運行和運行。

**基於興趣的目標或個性化**:如果滿足以下三個條件，則會發生基於興趣的目標（也稱為個性化）:

1. 現場收集的資料用於推斷用戶的興趣。
1. 資料在其他上下文中使用，如在其他站點或應用（非站點）上。
1. 資料用於根據這些推理選擇服務哪些內容或廣告。

## J

**[!DNL JupyterLab]**:Project的開源、基於Web的介面 [!DNL Jupyter] 整合到平台UI中。

**[!DNL Jupyter Notebook]**:與JupyterLab整合的Jupyter筆記型電腦使您能夠以多種語言（如Python、Scala和PySpark）對Experience Platform資料執行資料清理和轉換、數值模擬、統計建模、資料可視化、機器學習等更多操作。

## K

## L

**庫**:在標籤上下文中，庫是一組業務邏輯，其中包含關於標籤庫在客戶端設備上應如何操作的說明。

**查找實體**:在資料建模的上下文中，查找實體表示可與個人相關的概念，但不能直接用於標識個人。 屬於此類別的實體應由基於自定義體驗資料模型(XDM)類的架構來表示。

## M

**機器學習**:機器學習是一個研究領域，它使電腦能夠在不經過明確寫程式的情況下學習。

**機器學習模型**:機器學習模型是使用歷史資料和配置進行訓練以便為業務使用案例解決的機器學習配方的實例。 在Adobe Experience Platform資料科學工作區，機器學習模型被稱為配方。

**必需屬性**:一個啟用用戶的複選框，可確保所有配置檔案記錄都包含所選屬性。 例如：所有導出的配置檔案都包含電子郵件地址。

**映射**:資料映射是將源資料欄位映射到目標中相關目標欄位的過程。

**營銷活動**:在資料治理框架中，營銷活動（也稱為營銷使用案例）是Experience Platform資料使用者採取的行動，需要檢查其是否違反了資料使用策略。

**合併方法**:當使用平台UI定義合併策略時，合併方法指定在發生衝突時應如何對資料片段進行優先順序化。 使用即時客戶配置檔案API定義合併策略時，使用 `attributeMerge` 的雙曲餘切值。

**合併策略**:合併策略是Experience Platform用來確定如何組合來自多個源的客戶資料片段以建立單個配置檔案的規則。 當發生資料衝突時，合併策略確定哪些資料應按優先順序排列以便包含在配置檔案中。

**米辛**:請參閱「架構欄位組」。

**模組**:在標籤的上下文中，模組是擴展提供的可執行JavaScript的片段，該擴展在客戶端環境中執行操作而不需要建立規則。

## N

**非生產沙盒**:非生產沙箱是通常用於開發試驗、測試或試驗的沙箱。 與生產沙箱不同，非生產沙箱可以重置和刪除。

**[!DNL Notebooks]**: [!DNL Notebooks] 是使用 [!DNL Jupyter Notebook] 可以運行以執行資料分析。

## O

**優惠**:報價是一條營銷資訊，包含面向（潛在）客戶的業務或銷售建議。 優惠通常具有確定誰有資格查看或接收這些優惠的特定規則。

**[!DNL Offer Decisioning]**: [!DNL Offer Decisioning] 使營銷人員能夠根據跨渠道和應用程式收集的資料與最終用戶接洽時，管理規則和經過培訓的服務建議模型。

**提供庫**:服務庫是用於管理個性化和備用服務、決策規則和活動的中央庫。

**現場個性化營銷活動**:使用資料進行現場內容個性化的市場營銷操作。 現場個性化是用於推斷用戶興趣的任何資料，並用於根據這些推斷選擇服務哪些內容或廣告。

**針對現場的營銷活動**:使用資料進行現場廣告的營銷活動，包括在您組織的網站或應用上選擇和交付廣告，或衡量此類廣告的交付和效果。

**一次**:在計畫檔案導出的上下文中，安排一次性、按需、完整檔案導出。

**覆蓋保存策略**:「覆蓋」保存策略是用於通過連接接收第三方資料的選項，在該選項中，您可以指定是否在指定的時間表覆蓋所接收的資料。

## P

**部分攝取**:部分攝取允許在指定錯誤閾值內攝取批處理資料的有效記錄。 可以在下載或訪問失敗記錄的錯誤診斷 [!UICONTROL 監視] 或 [!UICONTROL 源] 資料流運行概述。

**鑲木檔案**:Parket檔案是具有複雜嵌套資料結構的列式儲存檔案格式。 添加資料以填充模式資料集需要拼花檔案。

**個性化服務**:個性化服務是基於資格規則和約束的可定製營銷資訊。

**投放位置**：投放位置是優惠方案在其中為一般使用者顯示的投放位置和內容。

**策略工作區**:平台UI中的工作區，它使資料管理員能夠查看和管理組織的資料使用標籤和策略。

**策略**:資料使用策略是一條規則，它指定基於應用於平台資料的使用標籤的應用而受限的營銷操作。

**策略執行**:允許您使用應用的市場營銷操作強制實施資料使用策略，以防止在組織內構成策略違規的資料操作。

**主鍵**:主鍵是模式中唯一標識所有記錄的指定。

**優先順序**:在 [!DNL Offer Decisioning]，優先順序用於對滿足所有約束（如資格、日曆和封頂）的優惠進行排名。

**專用標識圖**:專用標識圖（有時稱為專用圖）是縫合標識和連結標識之間的關係的專用映射，該映射基於第一方資料構建，僅由您的組織可見。 每個組織只有一個專用圖形，並作為為與您的品牌交互的每個客戶生成的單個標識圖形的結構藍圖。

**產品配置檔案**:產品配置檔案使管理員能夠授予用戶對與Experience Platform關聯的所有服務或服務子集的訪問權限。

**生產沙盒**:生產沙盒是供生產環境使用的沙盒。 與非生產沙箱不同，不能重置或刪除生產沙箱。

**配置檔案**:不要將即時客戶概要檔案作為服務混為一談，概要檔案是單個客戶的完整表示，由合併的記錄和來自多個來源的時間序列資料構建。

**配置檔案訪問**:的 `/entities` 即時客戶配置檔案API中的終結點允許您訪問配置檔案資料儲存中的記錄資料和時間序列事件。 另請參閱：配置檔案實體

**配置檔案資料**:配置檔案資料是指位於配置檔案資料儲存中的任何資料。

**配置檔案資料儲存**:配置檔案資料儲存（有時稱為配置檔案儲存）是獨立於資料湖的資料儲存系統，即時客戶配置檔案用於建立和儲存配置檔案。

**配置檔案實體**:配置檔案實體表示與個人（通常是客戶）相關的屬性。 屬於此類別的實體應由基於 [!DNL XDM Individual Profile] 類。 另請參閱：配置檔案訪問

**配置檔案導出**: [!DNL Profile] 導出是Experience Platform的兩種目的地之一。 [!DNL Profile] export生成包含配置檔案和屬性的檔案，並將原始PII資料與電子郵件一起使用，以便與營銷和電子郵件自動化平台整合。

**配置檔案片段**:配置檔案片段是特定客戶現有身份清單中僅有一個身份的配置檔案資訊。

**配置檔案ID**:配置檔案ID是與標識類型關聯的自動生成的標識符，並表示配置檔案。

**屬性**:在標籤的上下文中，屬性是部署一組標籤所需的所有內容的容器。

## Q

**查詢**:查詢是對資料庫表中的資料的請求。

**查詢編輯器**:查詢編輯器是用於在中編寫、驗證和提交SQL陳述式的工具 [!DNL Query Service]。

## R

**Real-time Customer Data Platform**: [!DNL Real-time Customer Data Platform] 將已知和未知的客戶資料匯集在一起，通過簡化整合、智慧細分和在數字客戶旅程中即時激活來建立可信客戶配置檔案。

**即時客戶概要資訊**:即時客戶配置檔案（有時稱為配置檔案）通過組合來自多個渠道的資料（包括線上、離線、CRM和第三方），為每個客戶提供整體視圖。 配置檔案允許您將客戶資料整合到單個配置檔案中，為每次客戶交互提供可操作且時間戳記的帳戶。

**食譜**:配方是模型規範的Adobe術語，是表示構建和執行經過訓練的模型所需的特定機器學習進程、AI算法、處理邏輯和配置參數的頂級容器，因此有助於解決特定的業務問題。

**記錄**:記錄是作為資料集中的行持續存在的資料。

**記錄資料**:提供有關主題屬性的資訊。 主題可以是組織或個人。

**重複**:在 [!DNL Query Service]，循環定義查詢是計畫只運行一次還是定期運行。

**表示法**:在 [!DNL Offer Decisioning]，表示是由渠道用於顯示要約的資訊，如位置或語言。

**資源**:在標籤上下文中，資源是一個泛型術語，它引用了標籤用戶可以在客戶端環境中配置的選項，包括擴展、資料元素和規則。

**基於角色的訪問控制**:基於角色的訪問控制使管理員能夠將訪問權限和權限分配給Experience Platform用戶。 權限包括查看和/或使用Experience Platform功能（如建立沙箱、定義方案和管理資料集）的能力。

**規則**:在標籤上下文中，規則是一組元件的集合，這些元件定義了應按邏輯分組的特定事件、條件和操作集。

**規則元件**:在標籤的上下文中，規則元件是構成規則的事件、條件和操作。

**運行時**:運行時為機器學習配方指定運行時環境。 [!DNL Python], [!DNL Spark]、PySpark和Tensorflow運行時允許您為處方源輸入Docker影像的URL。

## S

**示例資料**:示例資料是資料檔案（通常是前100行）的預覽，它為資料科學家或工程師提供了資料檔案中模式或資料的概念。

**沙盒**:沙盒是一種虛擬構造，用於將單個平台實例分區到單獨的虛擬環境中，以幫助開發和發展數字型驗應用程式。

**沙盒重置**:沙盒重置會刪除沙盒內的所有資料，包括資料、配置檔案和段。 沙盒重置會影響連接到內部或外部目標的資料。

**沙盒切換器**:Experience Platform中的沙盒切換器控制項允許用戶在他們有權訪問的沙盒之間導航。 切換沙盒將更改所有內容，並可能根據權限更改功能訪問。

**計畫**:時間表是用戶定義的關於從第三方資料源到Adobe Experience Platform的資料接收的頻率或順序的規範。

**評分**:評分是使用訓練好的模型從資料生成洞見的過程。

**架構**:模式是一組規則，用於表示和驗證資料的結構和格式。 模式由類和可選欄位組組成，用於建立資料集和資料流。 架構可包括行為屬性、時間戳、標識、屬性定義、關係等。

**架構欄位組**:在體驗資料模型(XDM)中，模式欄位組允許用戶擴展可重用欄位以定義要包含在模式中的一個或多個屬性。

**架構庫**:架構庫包含由Adobe提供的行業標準XDM資源以及由您的組織定義的自定義資源。

**架構註冊表**:架構註冊表提供了用戶介面和REST風格的API，用於查看和管理架構庫中與架構相關的所有資源。

**秘密訪問密鑰**:密鑰是 [!DNL Amazon] 與訪問密鑰ID一起使用以對AWS請求進行簽名的S3密鑰。

**段**:段是一組規則，包括屬性和事件資料，這些屬性和事件資料限定了多個配置檔案成為受眾。

**段生成器**:的 [!DNL Segment Builder] 是用於生成段定義的可視化開發環境。 它是使用Experience Platform分段服務的所有應用程式的通用元件。

**段定義**:段定義是用於描述目標受眾的關鍵特徵或行為的規則集。 一旦概念化，段定義中概述的規則將用於確定段的合格受眾成員。

**分段評價方法**:分段評價方法有兩種：按時和按需。 計畫評估支援在特定時間運行導出作業的循環計畫，而按需評估涉及建立段作業以立即構建受眾。

**段導出**:段導出是Experience Platform中的兩種目標之一。 通過段導出，您可以發送符合條件且已映射到目標的配置檔案。 使用段和用戶ID以及假名資料，並通常與社交網路和其他數字媒體目標平台整合。

**段ID**:段ID是與段關聯的自動生成的標識符。

**段成員資格**:段成員資格顯示配置檔案當前屬於哪些段。

**段規則**:段規則定義確定配置檔案是否符合段的條件。

**分段**:細分是將大量客戶、潛在客戶或消費者分成小組的過程，這些小組具有相似的屬性，並且會對特定的營銷策略做出類似的反應。

**SenseiML框架**:SenseiML框架是一個統一的機器學習(ML)框架，它利用Experience Platform資料使資料科學家能夠以更快、可擴展和可重複使用的方式開發由機器學習驅動的情報服務。

**敏感(「S」)標籤**:敏感(「S」)標籤用於對被視為敏感的資料進行分類，例如要標籤為敏感的不同類型的行為或地理資料。

**服務**:通過利用Adobe智慧服務實現人工智慧和機器學習服務的強大框架。 服務提供即時、個性化的客戶體驗，或實施定制智慧服務。

**單一身份個性化營銷活動**:使用資料進行現場內容個性化的營銷操作。 現場個性化是用於推斷用戶興趣的任何資料，並用於根據這些推斷選擇提供哪些內容或廣告。

**S1資料使用標籤**:安 `S1` 資料使用標籤用於對指定緯度和經度的資料進行分類，所述緯度和經度可用於確定設備的精確位置。

**S2資料使用標籤**:安 `S2` 資料使用標籤用於對可用於確定廣義定義的地理區域的資料進行分類。

**源**:源是平台中任何輸入連接器的通用術語。 另請參閱：源連接器

**源屬性**:源屬性是源資料集中的欄位。 源屬性映射到目標架構欄位。

**源目錄**:源目錄是Experience Platform中可用源連接器的清單。

**源類別**:源類別是具有相似特徵的源的分組。

**源連接器**:源連接器（也稱為源）幫助用戶輕鬆地從多個源接收資料，從而允許使用Experience Platform服務對資料進行結構化、標籤和增強。 可以從多種來源（如基於雲的儲存、第三方軟體和CRM系統）接收資料。

**流連接**:流連接是由Adobe提供的唯一端點，並與客戶的IMS組織關聯以將資料流到Experience Platform。

**標準標識命名空間**:標準標識命名空間是Adobe提供的預定義標識命名空間，它代表通常用於標識客戶的行業標準解決方案。

**流攝入**:流式接收允許您將資料從客戶端和伺服器端設備發送到即時Experience Platform。

**流分段**:流分段是一種持續的資料選擇過程，它根據用戶活動更新分段。 一旦生成並保存了段，將針對傳入資料應用段定義。 [!DNL Real-time Customer Profile]。 定期處理段添加和刪除，確保目標受眾保持相關性。

**系統視圖**:「系統視圖」是流經的源資料集的可視表示 [!DNL Real-time Customer Profile] 到目的地。

## T

**標籤**:在Adobe Experience Platform，標籤提供了部署、統一和管理分析、營銷和廣告整合的工具，這些整合是在所有客戶端設備上提供相關客戶體驗所必需的。

**目標功能**:在特徵映射中，目標特徵是模型預測的特徵。

**時間序列資料**:時間序列資料提供記錄主題直接或間接執行操作時系統的快照。

**訓練模型**:訓練後的模型表示模型訓練過程的可執行輸出，其中一組訓練資料被應用到模型實例。 經過培訓的模型將維護對從其建立的任何智慧Web服務的引用。 一種訓練好的模型適合於評分和建立智慧Web服務。

**令牌**:令牌是一種雙因素身份驗證安全性，可用於授權使用電腦服務 [!DNL Query Service]。

## U

**聯合架構**:聯合架構是共用同一類且已為 [!DNL Real-time Customer Profile]。 組織可以存在多個聯合架構，但每個類只能有一個聯合架構。

## V

## W

## X

**XDM**:請參閱體驗資料模型(XDM)。

**XDM決策事件**:XDM決策事件是一個基於時間序列的類，用於捕獲有關決策活動結果和上下文的觀察結果。 這包括關於如何作出決定、何時作出決定、提出（和選擇）哪些選項以及在決策過程中影響決定或可以觀察到的背景狀態的資訊。

**XDM體驗事件**:XDM ExperienceEvent是基於時間序列的類，用於在發生事件（或事件集）時捕獲系統的狀態，包括所涉及主題的時間點和標識。 另請參閱：體驗事件

**XDM個人配置檔案**:XDM [!DNL Individual Profile] 是基於記錄的類，它對已識別和部分識別的主題的屬性形成單一表示。 高度識別的配置檔案可用於個人通信或目標預訂，並且可以包含詳細的個人資訊，例如姓名、性別、出生日期、地點和聯繫資訊，包括電話號碼和電子郵件地址。

**XDM系統**:XDM系統表示一個框架，該框架可操作XDM架構，以便在下游Experience Platform服務中使用。

## Y

## Z
