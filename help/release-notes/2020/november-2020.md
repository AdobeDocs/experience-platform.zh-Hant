---
title: Adobe Experience Platform發行說明2020年11月
description: 2020年11月Adobe Experience Platform發行說明。
doc-type: release notes
last-update: November 10, 2020
author: crhoades, ens25212
exl-id: 29179b56-e49a-44e8-8c64-a7c383c2eaaf
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '2184'
ht-degree: 5%

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

當Adobe將資料湖從Gen1遷移到Gen2時，用戶將能夠從資料湖中讀取資料，但寫入資料湖的所有功能都將受到影響。 Adobe會聯絡系統管理員，詳細討論移轉的影響，並確認特定IMS組織的移轉日期和時間。

欲知更多資訊，請閱讀 [Data Lake移轉指南](../../landing/adls2-gen2-migration.md).

## [!DNL Access control] {#access-control}

[!DNL Experience Platform] 利用 [Adobe Admin Console](https://adminconsole.adobe.com) 產品設定檔，將使用者與權限和沙箱連結。 權限可控制對各種Platform功能的存取，包括資料模型、設定檔管理和沙箱管理。

**主要功能**

| 功能 | 說明 |
| ------- | ----------- |
| 權限 | 在 [!DNL Admin Console]，則 [!DNL Platform] 產品設定檔可讓您自訂 [!DNL Platform] 功能適用於附加至該設定檔的使用者。 可用的權限類別包括： **[!UICONTROL 資料模型]**, **[!UICONTROL 資料管理]**, **[!UICONTROL 設定檔管理]**, **[!UICONTROL Identity Management]**, **[!UICONTROL 資料監控]**, **[!UICONTROL 沙箱管理]**, **[!UICONTROL 目的地]**, **[!UICONTROL 資料擷取]**, **[!UICONTROL Data Science Workspace]**, **[!UICONTROL 查詢服務]**，和 **[!UICONTROL 資料控管]**. |
| 存取沙箱 | 此 **[!UICONTROL 權限]** 標籤 [!DNL Platform] 產品設定檔可授予使用者特定沙箱的存取權。 請參閱 [沙箱](#sandboxes) 以取得詳細資訊。 |

如需詳細資訊，請參閱 [存取控制概觀](../../access-control/home.md).

## [!DNL Offer Decisioning] {#offer-decisioning}

[!DNL Offer Decisioning] 是與整合的應用程式服務 [!DNL Experience Platform]. 它可讓您善用 [!DNL Platform] 以在適當的時間跨所有接觸點為客戶提供最佳選件和體驗。

**主要功能**

| 功能 | 說明 |
| ------- | ----------- |
| 集中優惠方案庫 | 在此介面中，您建立和管理構成選件的不同元素，以及定義其規則和限制。 |
| 優惠方案決策引擎 | 優惠方案決策引擎採用 [!DNL Platform] 資料和 [!DNL Real-time Customer Profiles]，以及優惠方案庫，以選取要提供優惠方案的適當時間、客戶和管道。 |

如需詳細資訊，請參閱 [[!DNL Offer Decisioning]](https://experienceleague.adobe.com/docs/offer-decisioning/using/offer-decisioning-home.html?lang=zh-Hant) 檔案。

## [!DNL Sandboxes] {#sandboxes}

[!DNL Experience Platform] 旨在在全球範圍內豐富數位體驗應用程式。 公司通常並行運行多個數字型驗應用程式，需要滿足這些應用程式的開發、測試和部署，同時確保操作合規性。 為了滿足這一需求， [!DNL Experience Platform] 提供可將單一 [!DNL Platform] 例項放入個別的虛擬環境，以協助開發及改進數位體驗應用程式。

**主要功能**

| 功能 | 說明 |
| ------- | ----------- |
| 生產沙箱 | [!DNL Experience Platform] 提供單一生產沙箱，無法刪除或重設。 可用沙箱的總數（生產及非生產）由所取得的牌照釐定。 |
| 非生產沙箱 | 可針對單一建立多個非生產沙箱 [!DNL Platform] 例項，可讓您測試功能、執行實驗及建立自訂設定，而不會影響生產沙箱。 |
| 沙箱切換器 | 在 [!DNL Experience Platform] 使用者介面，畫面左上角的沙箱切換器可讓您透過下拉式功能表，在可用的沙箱之間切換。 沙箱切換器也提供搜尋功能，可讓您篩選可用的沙箱。 |
| `x-sandbox-name` 標題 | 所有呼叫 [!DNL Experience Platform] API現在必須包含新 `x-sandbox-name` 標題，其值引用 `name` 操作將發生的沙箱的屬性。 |

如需詳細資訊，請參閱 [沙箱概述](../../sandboxes/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] 可讓資料工程師將資料對應、轉換及驗證至Experience Data Model(XDM)。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 迭代運算 | [!DNL Data Prep] 映射器現在支援對層次執行迭代操作。 |
| 映射器函式 | [!DNL Data Prep] 映射程式現在能夠 **not** 將屬性從來源複製到目標XDM。 |

如需詳細資訊，請參閱 [[!DNL Data Prep] 概述](../../data-prep/home.md).

## Data Science Workspace {#dsw}

Data Science Workspace使用機器學習和人工智慧，從您的資料建立深入分析。 整合至Adobe Experience Platform的Data Science Workspace可協助您跨Adobe解決方案，使用內容和資料資產進行預測。 Data Science Workspace完成此作業的其中一種方式是使用 [!DNL JupyterLab]. [!DNL JupyterLab] 是 [[!DNL Project Jupyter]](https://jupyter.org/) 與Adobe Experience Platform緊密整合。 它為資料科學家提供互動式開發環境，以便與 [!DNL Jupyter] 筆記本、代碼和資料。

**主要功能**

| 功能 | 說明 |
| ------- | ----------- |
| [!DNL JupyterLab] 方式產生器範本 | 筆記型電腦至配方需求使用和版本已更新。 [!DNL Python] ML運行時基本映像已更新為使用 [!DNL Python] 3.6.7和a [!DNL Conda] 環境專屬 |

欲知更多資訊，請閱讀 [使用Jupyter Notebooks建立配方](../../data-science-workspace/jupyterlab/create-a-model.md).

## [!DNL Destinations] 服務 {#destinations}

在 [Real-time Customer Data Platform](../../rtcdp/overview.md)，目的地是與目的地平台預先建立的整合，可順暢地向這些合作夥伴啟用資料。

**新目的地**

| 目的地 | 說明 |
| ----------- | ----------- |
| 佈雷茲 | Braze是一個全面的客戶參與平台，可為客戶與其喜愛的品牌之間提供相關且難忘的體驗。 |
| Microsoft兵 | Microsoft Bing目的地可協助您在Microsoft Display Advertising中執行重新鎖定目標和對象鎖定目標的數位促銷活動。 |
| 交易台 | 交易台是廣告購買者的自助平台，可跨顯示器、視訊和行動詳細目錄來源執行重新定位和對象鎖定的數位促銷活動。 |

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 目的地詳細資訊UX更新 | Real-Time CDP的目標工作流程現在包含內嵌監控，讓您查看哪些批次啟動成功。 此功能可讓使用者透過警報和監控控制面板，直接在批次目的地的工作流程中解決問題，以追蹤處理管道中的錯誤。 |
| 檔案加密 | 針對檔案型目的地，使用者現在可以將加密新增至匯出的檔案。 |
| 檔案排程 | 對於電子郵件型和雲端儲存目的地，使用者可以建立一次性匯出或建立每日快照。 |
| 必填欄位 | 使用者可將欄位標示為必填欄位，確保僅匯出包含必填欄位的欄位。 |

如需詳細資訊，請參閱 [目的地概觀](../../destinations/home.md).

## Intelligent Services {#intelligent-services}

智慧服務讓行銷分析師和從業人員能夠在客戶體驗使用案例中運用人工智慧和機器學習的強大功能。 這可讓行銷分析人員使用業務層級設定，針對公司的需求設定專屬預測，而不需要資料科學的專業知識。

**主要功能**

| 功能 | 說明 |
| ------- | ----------- |
| 消費者體驗事件(CEE)資料集 | 建立CEE資料集現在支援使用結構編輯器將身分欄位新增至資料集。 Attribution AI和Customer AI會使用主要身分來結合事件。 |

欲知更多資訊，請閱讀 [新增身分欄位至資料集](../../intelligent-services/data-preparation.md#add-identity-fields-to-the-dataset) （位於Intelligent Services資料準備指南中）。

### Attribution AI

Attribution AI是Intelligent Services的一部分，是多管道的演算法歸因服務，可計算客戶互動對指定結果的影響和增量影響。

**主要功能**

| 功能 | 說明 |
| ------- | ----------- |
| 資料來源連結 | 您可以從所選服務執行個體的右側邊欄，檢視並導覽至原始資料集來源的連結。 |
| 編輯實例名稱 | 您現在可以修改現有Attribution AI例項的名稱。 |
| 原地複製執行個體 | 複製當前選擇的服務實例設定並允許修改。 |
| 修改執行個體設定參數 | 如果現有Attribution AI例項尚未開始計分，您現在可以修改其設定。 |
| 一分 | 您現在可以在您的Attribution AI例項中觸發臨機模型計分。 |
| 傳遞欄 | 您現在可以設定將新增至原始輸出分數檔案的其他欄，以新增其他維度至BI工具檢視。 |
| 執行個體啟動和停用 | 您現在可以啟動並取消啟動Attribution AI例項的排程模型訓練和計分。 |
| 權益追蹤 | 您可以在建立例項容器中找到帳戶所耗用的歸因分析總數。 |
| 接觸點依位置劃分 | 新的深入分析圖表，可依轉換路徑位置分析接觸點。 |
| 最上層轉換路徑 | 位於「路徑分析」標籤的新前瞻分析圖表。 圖形包含前5個轉換路徑的清單，顯示導致最多轉換的行銷管道接觸點的順序。 |
| 接觸點有效性 | 提供模型用來衡量接觸點成效的三個最重要變數的深入分析。 變數包括接觸的正面和負面路徑、接觸點效率和接觸點體積的比率。 |

欲知更多資訊，請閱讀 [Attribution AI概述](../../intelligent-services/attribution-ai/overview.md).

### Customer AI

Customer AI是Intelligent Services的一部分，可讓行銷人員在個別層級產生客戶預測並提供說明。 在影響因子的協助下，Customer AI 可告知您客戶可能會有什麼行為以及原因何在。 此外，行銷人員可受益於 Customer AI 預測和洞見，藉由提供最適合的方案和訊息來打造個人化客戶體驗。

**主要功能**

| 功能 | 說明 |
| ------- | ----------- |
| 資料來源連結 | 您可以從所選服務執行個體的右側邊欄，檢視並導覽至原始資料集來源的連結。 |
| 編輯實例名稱 | 您可以修改現有Customer AI例項的名稱。 |
| 修改執行個體設定參數 | 如果現有Customer AI例項尚未開始計分，您現在可以修改其設定。 |
| 原地複製執行個體 | 複製當前選擇的服務實例設定並允許修改。 |
| 權益追蹤 | 您可以在建立執行個體容器中找到由Customer AI為您的帳戶評分的設定檔總數。 |
| 預測目標 | 建立預測目標的靈活性已增加，新的選項可預測某個「將發生」還是「將不發生」。 此外，新增可預測使用多個事件時，「全部」事件是否發生，或「任何」事件是否發生的選項。 |
| 影響因素深入分析 | 傾向最高影響因素貯體現在包含向下切入。 向下切入是傾向貯體內每個最重要影響因素之值的更深層摘要。 |

欲知更多資訊，請閱讀 [Customer AI概觀](../../intelligent-services/customer-ai/overview.md).

## 即時客戶個人檔案 {#profile}

Adobe Experience Platform可讓您為客戶提供協調、一致且相關的體驗，無論客戶在何處或何時與您的品牌互動。 透過即時客戶個人檔案，您可以全面了解各個客戶，其中結合來自多個管道的資料，包括線上、離線、CRM和第三方資料。 [!DNL Profile] 可讓您將不同的客戶資料整合至統一的檢視中，提供每個客戶互動的可操作、時間戳記帳戶。

**主要功能**

| 功能 | 說明 |
| ------- | ----------- |
| 更新合併原則工作流程 | Platform已將合併策略配置升級為新的逐步式工作流。 此工作流程可讓使用者匯整多個設定檔資料集的資料片段，並為資料在這些資料集合的方式設定優先順序，以便建立個別資料的完整檢視。 使用者可以選取適當的合併方法（依時間戳記排序或資料集優先順序），並將ExperienceEvent資料集附加至「設定檔」資料集，以合併選取的XDM個別設定檔資料集。 |
| 聯合架構視圖 | 在Experience PlatformUI中，使用者可更輕鬆找到關於聯合結構的所有結構和資料集，以及身分和關係欄位等表面關鍵屬性的資訊。 這些更新可改善疑難排解及驗證設定檔已正確設定、身分識別已正確匯整，以及資料已成功內嵌的功能。 |

如需即時客戶設定檔的詳細資訊，包括使用的教學課程和最佳實務 [!DNL Profile] 資料，請閱讀 [即時客戶個人檔案概觀](../../profile/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform可以內嵌來自外部來源的資料，同時允許您使用 [!DNL Platform] 服務。 您可以從多種來源擷取資料，例如Adobe應用程式、雲端儲存、協力廠商軟體和您的CRM系統。

[!DNL Experience Platform] 提供RESTful API和互動式UI，讓您輕鬆為各種資料提供者設定來源連線。 這些源連接允許您驗證並連接到外部儲存系統和CRM服務、設定獲取運行時間以及管理資料獲取吞吐量。

**新來源**

| 功能 | 說明 |
| ------- | ----------- |
| [!DNL Shopify] | 您現在可以連線 [!DNL Shopify] to [!DNL Experience Platform] 使用 [!DNL Flow Service] API或UI。 請參閱 [Shopify連接器概觀](../../sources/connectors/ecommerce/shopify.md) 以取得更多資訊。 |

**主要功能**

| 功能 | 說明 |
| ------- | ----------- |
| 更新連接資訊 | 您現在可以使用 [!DNL Flow Service] API和UI。 如需詳細資訊，請參閱 [使用流量服務API更新連線](../../sources/tutorials/api/update.md) 和 [使用UI編輯帳戶詳細資訊](../../sources/tutorials/ui/monitor.md). |
| 刪除連線 | 現在可以使用 [!DNL Flow Service] API和UI。 如需詳細資訊，請參閱 [使用流服務API刪除連接](../../sources/tutorials/api/delete.md) 和 [使用UI刪除帳戶](../../sources/tutorials/ui/delete-accounts.md). |
| 分層映射 | 您可以在資料擷取程式期間預覽階層式來源檔案，例如JSON或Parquet。 請參閱 [在UI中為雲儲存連接器配置資料流](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) 以取得更多資訊。 |
| 串流來源中對應的API支援 | 您現在可以使用API來執行串流來源的對應功能。 |
| 雲端儲存來源自訂分隔字元的API支援 | 您現在可以使用雲端儲存來源收集非CSV分隔的檔案。 您可以使用任何單一欄的分隔字元（例如索引標籤、逗號、垂直號、分號或雜湊），以任何格式收集平面檔案。 |
| Adobe Audience Manager連接器的沙箱支援 | Audience Manager連接器現在可感知沙箱。 使用者可讓連接器將Audience Manager資料集路由至自己選擇的沙箱（包括非生產沙箱）。 設定限制為每個IMS組織一個沙箱。 |
| UX改良功能 | 檔案型擷取現在可透過來源目錄存取。 |

若要進一步了解來源，請參閱 [來源概觀](../../sources/home.md).
