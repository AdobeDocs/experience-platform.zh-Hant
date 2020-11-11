---
title: Adobe Experience Platform 發行說明
description: Experience Platform發行說明2020年11月11日
doc-type: release notes
last-update: November 10, 2020
author: crhoades, ens25212
translation-type: tm+mt
source-git-commit: 7c4b60dad1ad2071bb19a9b9e181f2db495187c2
workflow-type: tm+mt
source-wordcount: '2049'
ht-degree: 3%

---


# Adobe Experience Platform 發行說明

**發行日期：2020 年 11 月 11 日**

Adobe Experience Platform的新功能：

- [Adobe Experience Platform Data Lake移轉](#migration)
- [[!DNL Access control]](#access-control)
- [[!DNL Offer Decisioning]](#offer-decisioning)
- [[!DNL Sandboxes]](#sandboxes)

更新現有功能：

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Destinations] 服務](#destinations)
- [[!DNL Intelligent Services]](#intelligent-services)
- [[!DNL Real-time Customer Profile]](#profile)
- [[!DNL Sources]](#sources)

## Adobe Experience Platform Data Lake移轉 {#migration}

當Adobe將Data Lake從Gen1移轉至Gen2時，使用者將能夠從Data Lake讀取，但寫入Data Lake的所有功能都將受到影響。 Adobe將聯絡系統管理員，詳細討論移轉的影響，並確認特定IMS組織的移轉日期和時間。

如需詳細資訊，請閱讀資料 [湖移轉指南](../../landing/adls2-gen2-migration.md)。

## [!DNL Access control] {#access-control}

[!DNL Experience Platform] 運用 [Adobe Admin Console](https://adminconsole.adobe.com) 產品設定檔，將使用者與權限和沙盒連結。 權限控制對各種平台功能的存取，包括資料模型、描述檔管理和沙盒管理。

**主要功能**

| 功能 | 說明 |
| ------- | ----------- |
| 權限 | 在中， [!DNL Admin Console]產品配置檔案中的選 [!DNL Platform] 項卡允許您自定義附加到該 [!DNL Platform] 配置檔案的用戶可以使用哪些功能。 可用權限類別包括： **[!UICONTROL 資料管理、]**&#x200B;資料管理 **[!UICONTROL 、資料管理、身份管理、Identity Data Management]**、Identity Data Management Monigration、Administration Data Proding Data Projection Doming、Dobe Moding Dades ************************************、 Data Data、 Chog Da、 Da、 Moding、 Da、 Da、 Mog、 Mode Moding Shona、S、 Moding、 Da、 Mok、 Mona、S、S、S、D、S、D、S、D An、DS、S、DS、Da、DDS、DS、S、D MoS、D |
| 存取沙盒 | 產品 **[!UICONTROL 設定檔中的]** 「權限」 [!DNL Platform] 標籤可授予使用者特定沙盒的存取權。 如需詳細資訊，請參 [閱下方](#sandboxes) 「沙盒」一節。 |

如需詳細資訊，請參閱存 [取控制概觀](../../access-control/home.md)。

## [!DNL Offer Decisioning] {#offer-decisioning}

[!DNL Offer Decisioning] 是與整合的應用程式服務 [!DNL Experience Platform]。 它可讓您運用 [!DNL Platform] 在適當的時間跨所有觸點為客戶提供最佳的優惠和體驗。

**主要功能**

| 功能 | 說明 |
| ------- | ----------- |
| 集中化選件庫 | 您建立和管理不同元素的介面，這些元素會組成選件，並定義其規則和限制。 |
| 選件決策引擎 | 選件決策引擎 [!DNL Platform] 運用資 [!DNL Real-time Customer Profiles]料，以及選件庫，以選擇要提供選件的適當時間、客戶和通道。 |

For more information, please see the [[!DNL Offer Decisioning]](https://experienceleague.adobe.com/docs/offer-decisioning/using/offer-decisioning-home.html?lang=en) documentation.

## [!DNL Sandboxes] {#sandboxes}

[!DNL Experience Platform] 旨在讓全球數位體驗應用程式更加豐富。 公司通常並行執行多種數位體驗應用程式，並需要滿足這些應用程式的開發、測試和部署需求，同時確保運作符合規範。 為了滿足此需求，提供 [!DNL Experience Platform] 沙盒，將單一執行個體分割為 [!DNL Platform] 個別的虛擬環境，以協助開發和發展數位體驗應用程式。

**主要功能**

| 功能 | 說明 |
| ------- | ----------- |
| 製作沙盒 | [!DNL Experience Platform] 提供單一生產沙盒，無法刪除或重設。 可用沙盒（生產與非生產）的總數由所取得的授權決定。 |
| 非生產沙盒 | 您可針對單一執行個體建立多個非生產沙盒，讓 [!DNL Platform] 您測試功能、執行實驗並建立自訂組態，而不會影響您的生產沙盒。 |
| 沙盒切換器 | 在使用 [!DNL Experience Platform] 者介面中，畫面左上角的沙盒切換器可讓您透過下拉式選單，在可用沙盒之間切換。 沙盒切換器也提供搜尋功能，可讓您篩選可用的沙盒。 |
| `x-sandbox-name` 標題 | 所有對 [!DNL Experience Platform] API的呼叫現在必須包含新 `x-sandbox-name` 標題，其值會參 `name` 考執行作業的沙盒屬性。 |

如需詳細資訊，請參閱 [沙盒總覽](../../sandboxes/home.md)。

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] 可讓資料工程師將資料對應、轉換及驗證資料與Experience Data Model(XDM)。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 迭代運算 | [!DNL Data Prep] 映射器現在支援對層次執行迭代操作。 |
| 映射器函式 | [!DNL Data Prep] 映射程式現在能夠 **不將** 屬性從源複製到目標XDM。 |

如需詳細資訊，請參閱總 [[!DNL Data Prep] 覽](../../data-prep/home.md)。

## Data Science Workspace {#dsw}

Data Science Workspace使用機器學習和人工智慧，從您的資料中建立見解。 Data Science Workspace整合至Adobe Experience Platform，可協助您透過Adobe解決方案使用內容和資料資產進行預測。 Data Science Workspace的其中一個方式就是使用 [!DNL JupyterLab]。 [!DNL JupyterLab] 是Web使用者介面，可 [[!DNL Project Jupyter]](https://jupyter.org/) 與Adobe Experience Platform緊密整合。 它提供互動式開發環境，讓資料科學家可以使用筆 [!DNL Jupyter] 記型電腦、程式碼和資料。

**主要功能**

| 功能 | 說明 |
| ------- | ----------- |
| [!DNL JupyterLab] 方式產生器範本 | 筆記型電腦，符合配方需求使用和版本更新。 [!DNL Python] ML Runtime基本影像已更新為只 [!DNL Python] 使用3.6.7和 [!DNL Conda] 環境。 |

如需詳細資訊，請閱讀有關使用Jupyter筆 [記型電腦建立配方的檔案](../../data-science-workspace/jupyterlab/create-a-recipe.md)。

## [!DNL Destinations] 服務 {#destinations}

在 [Adobe即時客戶資料平台中](../../rtcdp/overview.md)，目標是與目標平台預先建立的整合，以順暢的方式將資料啟動給這些合作夥伴。

**新目標**

| 目的地 | 說明 |
| ----------- | ----------- |
| Microsoft Bing | Microsoft Bing目標可協助您在Microsoft Display Advertising中執行重新鎖定目標及受眾鎖定的數位宣傳。 |
| 貿易部門 | 交易台是廣告購買者的自助服務平台，可跨展示廣告、視訊和行動庫存來源執行重新鎖定目標及受眾目標數位宣傳。 |

<!-- | Braze | Braze is a comprehensive customer engagement platform that power relevant and memorable experiences between customers and the brands they love. |  -->

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 必填欄位 | 使用者可將欄位標示為必填，以確保只匯出包含必填欄位的欄位。 |

<!-- | File scheduling | For both email based and cloud storage destinations, users can create a one-time export or create daily snapshots. |
| File encryption | For file based destinations, users can now add encryption to their exported files. | -->

如需詳細資訊，請參閱「目 [標」概觀](../../rtcdp/destinations/destinations-overview.md)。

## Intelligent Services {#intelligent-services}

智慧型服務可讓行銷分析師和從業人員在客戶體驗使用案例中運用人工智慧和機器學習的強大功能。 這可讓行銷分析人員使用商業層級的組態來設定特定公司需求的預測，而不需要資料科學的專業知識。

**主要功能**

| 功能 | 說明 |
| ------- | ----------- |
| 消費者體驗事件(CEE)資料集 | 現在，建立CEE資料集支援使用模式編輯器向資料集添加標識欄位。 歸因AI和客戶AI使用主要識別碼來結合事件。 |

如需詳細資訊，請閱讀智慧型服務資 [料準備指南中有關新增身分欄位](../../intelligent-services/data-preparation.md#add-identity-fields-to-the-dataset) 至資料集的章節。

### 歸因AI

歸因人工智慧(Attribution AI)是智慧服務的一部分，是多通道的演算法歸因服務，可計算客戶互動對特定結果的影響和增量影響。

**主要功能**

| 功能 | 說明 |
| ------- | ----------- |
| 資料來源連結 | 您可從所選服務例項的右側檢視並導覽至原始資料集來源的連結。 |
| 編輯實例名稱 | 您現在可以修改現有Attribution AI例項的名稱。 |
| 複製實例 | 複製當前選定的服務實例設定並允許修改。 |
| 修改實例配置參數 | 現在，如果現有Attribution AI例項尚未開始計分，您可以修改其設定。 |
| 一次性得分 | 您現在可以在Attribution AI例項中觸發臨機模型計分。 |
| 傳遞欄 | 您現在可以設定將新增至原始輸出分數檔案的其他欄，以新增其他維度至BI工具檢視。 |
| 執行個體啟動和取消啟動 | 您現在可以啟動並取消啟動Attribution AI例項的排程模型訓練和計分。 |
| 權益追蹤 | 您可以在建立例項容器中找到您帳戶使用的歸因分析總數。 |
| 觸點劃分（依位置區分） | 新的前瞻分析圖表，可依據轉換路徑位置分析觸點。 |
| 頂層轉換路徑 | 位於「路徑分析」索引標籤中的新前瞻分析圖表。 圖表包含前5個轉換路徑的清單，顯示導致最多轉換的行銷渠道觸點順序。 |
| 觸點效能 | 提供模型衡量觸點效能的三個最重要變數的深入見解。 變數包括接觸的正反路徑比、接觸點效率和接觸點體積。 |

如需詳細資訊，請閱讀 [Attribution AI概觀](../../intelligent-services/attribution-ai/overview.md)。

### 客戶人工智慧

客戶人工智慧(Customer AI)是智慧型服務的一部分，可讓行銷人員在個人層級產生客戶預測，並提供說明。 借助影響因素，客戶人工智慧可以告訴您客戶可能做什麼以及為什麼。 此外，行銷人員可從客戶人工智慧預測和見解中獲益，透過提供最適當的優惠和訊息來個人化客戶體驗。

**主要功能**

| 功能 | 說明 |
| ------- | ----------- |
| 資料來源連結 | 您可從所選服務例項的右側檢視並導覽至原始資料集來源的連結。 |
| 編輯實例名稱 | 您可以修改現有客戶AI實例的名稱。 |
| 修改實例配置參數 | 如果現有客戶AI實例尚未開始計分，您現在可以修改其配置。 |
| 複製實例 | 複製當前選定的服務實例設定並允許修改。 |
| 權益追蹤 | 您可以在建立例項容器中找到由客戶AI為您的帳戶計分的描述檔總數。 |
| 預測目標 | 建立預測目標的靈活性已增強，有了新的選項來預測「將發生」或「將不發生」。 此外，新增了可預測「所有」事件發生或「任何」事件發生的選項。 |
| 影響因素深入分析 | 傾向最高影響因素區間現在包含向下切入。 追溯是傾向時段內每個最主要影響因素的更深層值摘要。 |

如需詳細資訊，請閱讀 [Customer AI概觀](../../intelligent-services/customer-ai/overview.md)。

## 即時客戶個人檔案 {#profile}

Adobe Experience Platform可讓您為客戶推動協調、一致且相關的體驗，不論客戶在何處或何時與您的品牌互動。 透過即時客戶個人檔案，您可以全面瞭解每個客戶，並結合來自多個通道的資料，包括線上、離線、CRM和第三方資料。 [!DNL Profile] 可讓您將分散的客戶資料整合為統一的檢視，提供每個客戶互動的可操作、時間戳記帳戶。

**主要功能**

| 功能 | 說明 |
| ------- | ----------- |
| 更新的合併原則工作流程 | 平台已將合併策略配置升級為新的逐步工作流。 此工作流程可讓使用者從多個描述檔資料集合資料片段，並設定如何在這些資料集合資料的優先順序，以建立每個個人的完整檢視。 用戶可以通過選擇適當的合併方法（按時間戳順序或資料集優先順序）和將ExperienceEvent資料集附加到Profile資料集來合併選定的XDM Individual Profile資料集。 |
| 聯合架構視圖 | 在Experience Platform UI中，使用者可以更輕鬆地找到有關所有結構描述和資料集的資訊，以及表面金鑰屬性，例如身分和關係欄位。 這些更新可改善疑難排解和驗證描述檔已正確設定、身分識別已正確銜接，以及資料已成功擷取的能力。 |

如需即時客戶個人檔案的詳細資訊，包括使用資料的教學課程和最佳實務，請 [!DNL Profile] 閱讀即時 [客戶個人檔案總覽](../../profile/home.md)。

## [!DNL Sources] {#sources}

Adobe Experience Platform可以從外部來源擷取資料，同時讓您使用服務來建構、標示和增強該資 [!DNL Platform] 料。 您可以從多種來源收集資料，例如Adobe應用程式、雲端儲存空間、協力廠商軟體和您的CRM系統。

[!DNL Experience Platform] 提供REST風格的API和互動式UI，讓您輕鬆地為各種資料提供者設定來源連線。 這些源連接允許您驗證並連接到外部儲存系統和CRM服務、設定接收運行的時間，以及管理資料接收吞吐量。

**新來源**
|功能 |說明 |
| — | — |
| [!DNL Shopify] |您現在可以使 [!DNL Shopify] 用 [!DNL Experience Platform] API [!DNL Flow Service] 或UI連線至。 如需詳細 [資訊，請參閱Shopify連接器概觀](../../sources/connectors/ecommerce/shopify.md) 。 |

**主要功能**

| 功能 | 說明 |
| ------- | ----------- |
| 更新連接資訊 | 您現在可以使用 [!DNL Flow Service] API和UI更新現有批次連線的名稱、說明和認證。 如需詳細資訊，請參閱使用Flow Service API [更新連線](../../sources/tutorials/api/update.md) ，以及使 [用UI編輯帳戶詳細資訊的教學課程](../../sources/tutorials/ui/monitor.md)。 |
| 刪除連接 | 現在，可以使用 [!DNL Flow Service] API和UI刪除包含錯誤或已變為不必要的批次連接。 如需詳細資訊，請參閱教學課程 [，說明如何使用Flow Service API刪除連線](../../sources/tutorials/api/delete.md) , [以及如何使用UI刪除帳戶](../../sources/tutorials/ui/delete-accounts.md)。 |
| 串流來源中對應的API支援 | 您現在可以使用API來執行串流來源的對應功能。 |
| API支援雲端儲存來源的自訂分隔字元 | 您現在可以使用雲端儲存來源收集非CSV分隔的檔案。 您可以使用任何單一欄分隔字元，例如制表符、逗號、管道、分號或雜湊，以任何格式收集平面檔案。 如果未提供，則值預設為逗號。 |
| Adobe Audience Manager連接器的沙盒支援 | Audience Manager連接器現在可感知沙盒。 使用者可以啟用連接器，將Audience Manager資料集路由至其選擇的沙盒（包括非生產沙盒）。 此設定限制為每個IMS組織一個沙盒。 |
| UX改進 | 現在可透過來源目錄存取檔案擷取。 |

若要進一步瞭解來源，請參閱 [來源概觀](../../sources/home.md)。