---
title: Adobe Experience Platform 發行說明 (2020 年 11 月)
description: Adobe Experience Platform 2020 年 11 月版發行說明。
doc-type: release notes
last-update: November 10, 2020
author: crhoades, ens25212
exl-id: 29179b56-e49a-44e8-8c64-a7c383c2eaaf
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2178'
ht-degree: 10%

---

# Adobe Experience Platform 發行說明

**發行日期： 2020年11月11日**

Adobe Experience Platform 的新功能：

- [Adobe Experience Platform資料湖移轉](#migration)
- [[!DNL Access control]](#access-control)
- [[!DNL Offer Decisioning]](#offer-decisioning)
- [[!DNL Sandboxes]](#sandboxes)

更新現有功能：

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Destinations]服務](#destinations)
- [[!DNL Intelligent Services]](#intelligent-services)
- [[!DNL Real-Time Customer Profile]](#profile)
- [[!DNL Sources]](#sources)

## Adobe Experience Platform資料湖移轉 {#migration}

雖然Adobe正在將Data Lake從Gen1移轉至Gen2，使用者將能從Data Lake讀取，但寫入至Data Lake的所有功能都將受到影響。 Adobe將會連絡系統管理員，詳細討論移轉的影響，並確認特定組織的移轉日期和時間。

如需詳細資訊，請參閱[資料湖移轉指南](../../landing/adls2-gen2-migration.md)。

## [!DNL Access control] {#access-control}

[!DNL Experience Platform]利用[Adobe Admin Console](https://adminconsole.adobe.com)產品設定檔將使用者與許可權和沙箱連結。 許可權可控制各種Experience Platform功能的存取權，包括資料模型製作、設定檔管理和沙箱管理。

**主要功能**

| 功能 | 說明 |
| ------- | ----------- |
| 權限 | 在[!DNL Admin Console]中，[!DNL Experience Platform]產品設定檔中的索引標籤可讓您自訂哪些[!DNL Experience Platform]功能可供附加到該設定檔的使用者使用。 可用的許可權類別包括： **[!UICONTROL 資料模型]**、**[!UICONTROL 資料管理]**、**[!UICONTROL 設定檔管理]**、**[!UICONTROL Identity Management]**、**[!UICONTROL 資料監視]**、**[!UICONTROL 沙箱管理]**、**[!UICONTROL 目的地]**、**[!UICONTROL 資料擷取]**、**[!UICONTROL 資料科學Workspace]**、**[!UICONTROL 查詢服務]**&#x200B;以及&#x200B;**[!UICONTROL 資料控管]**。 |
| 存取沙箱 | [!DNL Experience Platform]產品設定檔中的&#x200B;**[!UICONTROL 許可權]**&#x200B;索引標籤可授予使用者存取特定沙箱的許可權。 如需詳細資訊，請參閱以下[沙箱](#sandboxes)的相關章節。 |

如需詳細資訊，請參閱[存取控制總覽](../../access-control/home.md)。

## [!DNL Offer Decisioning] {#offer-decisioning}

[!DNL Offer Decisioning]是與[!DNL Experience Platform]整合的應用程式服務。 它可讓您運用[!DNL Experience Platform]，在適當的時間為所有接觸點的客戶提供最佳優惠和體驗。

**主要功能**

| 功能 | 說明 |
| ------- | ----------- |
| 集中式優惠資料庫 | 此介面可讓您建立和管理組成優惠方案的不同元素，並定義其規則和限制。 |
| 優惠決定引擎 | 優惠決定引擎運用[!DNL Experience Platform]資料和[!DNL Real-Time Customer Profiles]以及優惠資料庫，以選擇即將提供優惠的適當時間、客戶和管道。 |

如需詳細資訊，請參閱[[!DNL Offer Decisioning]](https://experienceleague.adobe.com/docs/offer-decisioning/using/offer-decisioning-home.html?lang=zh-Hant)檔案。

## [!DNL Sandboxes] {#sandboxes}

[!DNL Experience Platform]是專為豐富全球的數位體驗應用程式而建置。 公司經常要並行執行多個數位體驗應用程式，且在顧及這些應用程式的開發、測試和部署等需求的同時，也必須確保營運合規性。為了滿足此需求，[!DNL Experience Platform]提供可將單一[!DNL Experience Platform]執行個體分割成個別虛擬環境的沙箱，以協助開發及改進數位體驗應用程式。

**主要功能**

| 功能 | 說明 |
| ------- | ----------- |
| 生產沙箱 | [!DNL Experience Platform]提供單一生產沙箱，無法刪除或重設。 可用沙箱（包括生產及非生產）的總數取決於取得的授權。 |
| 非生產沙箱 | 您可以為單一[!DNL Experience Platform]執行個體建立多個非生產沙箱，讓您測試功能、執行實驗及進行自訂設定，而不會影響您的生產沙箱。 |
| 沙箱切換器 | 在[!DNL Experience Platform]使用者介面中，熒幕左上角的沙箱切換器可讓您透過下拉式功能表在可用沙箱之間切換。 沙箱切換器也提供搜尋功能，可讓您篩選可用沙箱。 |
| `x-sandbox-name`標題 | 所有對[!DNL Experience Platform] API的呼叫現在必須包含新的`x-sandbox-name`標頭，其值會參考將進行作業的沙箱的`name`屬性。 |

如需詳細資訊，請參閱[沙箱總覽](../../sandboxes/home.md)。

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep]可讓資料工程師對應、轉換及驗證與Experience Data Model (XDM)之間的資料。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 反複運算 | [!DNL Data Prep]對應程式現在支援在階層上執行反複作業。 |
| 對應程式函式 | [!DNL Data Prep]對應程式現在能夠&#x200B;**不**&#x200B;將屬性從來源複製到目標XDM。 |

如需詳細資訊，請參閱[[!DNL Data Prep] 總覽](../../data-prep/home.md)。

## Data Science Workspace {#dsw}

資料科學Workspace使用機器學習和人工智慧，從您的資料建立深入分析。 資料科學Workspace已整合至Adobe Experience Platform，可協助您跨Adobe解決方案使用您的內容和資料資產進行預測。 Data Science Workspace完成此作業的其中一個方法是使用[!DNL JupyterLab]。 [!DNL JupyterLab]是[[!DNL Project Jupyter]](https://jupyter.org/)的網頁式使用者介面，且已緊密整合至Adobe Experience Platform。 它為資料科學家提供互動式開發環境，以使用[!DNL Jupyter]筆記本、程式碼和資料。

**主要功能**

| 功能 | 說明 |
| ------- | ----------- |
| [!DNL JupyterLab]配方產生器範本 | 筆記型電腦到配方需求使用方式及版本已更新。 已更新[!DNL Python] ML執行階段基底影像以專門使用[!DNL Python] 3.6.7和[!DNL Conda]環境。 |

如需詳細資訊，請參閱[使用Jupyter Notebooks建立配方](../../data-science-workspace/jupyterlab/create-a-model.md)的檔案。

## [!DNL Destinations]服務 {#destinations}

在[Real-Time Customer Data Platform](../../rtcdp/overview.md)中，目的地是預先建立的與目的地平台的整合，可透過順暢的方式為這些合作夥伴啟用資料。

**新目的地**

| 目標 | 說明 |
| ----------- | ----------- |
| 釺焊 | Braze是全方位的客戶參與平台，可在客戶與所喜愛品牌之間提供相關且令人難忘的體驗。 |
| Microsoft Bing | Microsoft Bing目的地可幫助您在Microsoft Display Advertising中執行重新定位以及以對象為目標的數位行銷活動。 |
| The Trade Desk | Trade Desk是廣告買方適用的自助式平台，可在各種顯示、影片和行動詳細目錄來源中執行重新定位以及以對象為目標的數位行銷活動。 |

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 目的地詳細資料UX更新 | Real-Time CDP的目標工作流程現在包含內嵌監視，以便您檢視哪些批次啟用成功。 此功能可讓使用者透過警報，以及追蹤處理管道中錯誤的監視儀表板，直接解決批次目的地工作流程中的問題。 |
| 檔案加密 | 針對以檔案為基礎的目的地，使用者現在可以新增加密至其匯出的檔案。 |
| 檔案排程 | 針對電子郵件和雲端儲存目標，使用者可以建立一次性匯出或建立每日快照。 |
| 必填欄位 | 使用者可以將欄位標示為必填欄位，以確保僅匯出包含必填欄位的欄位。 |

如需詳細資訊，請參閱[目的地概觀](../../destinations/home.md)。

## Intelligent Services {#intelligent-services}

智慧型服務可讓行銷分析師及從業人員運用客戶體驗使用案例中人工智慧和機器學習的強大功能。 這可讓行銷分析人員利用業務層級設定，針對公司需求設定專屬預測，而無需資料科學的專業知識。

**主要功能**

| 功能 | 說明 |
| ------- | ----------- |
| 取用者體驗事件(CEE)資料集 | 建立CEE資料集現在支援使用結構編輯器將身分欄位新增到資料集。 Attribution AI和Customer AI會使用主要身分來合併事件。 |

如需詳細資訊，請閱讀Intelligent Services資料準備指南中[將身分欄位新增至資料集](../../intelligent-services/data-preparation.md#add-identity-fields-to-the-dataset)的章節。

### Attribution AI

Attribution AI是Intelligent Services的一部分，它是一種多管道的演演算法歸因服務，可計算客戶互動對指定結果的影響和累加影響。

**主要功能**

| 功能 | 說明 |
| ------- | ----------- |
| 資料來源連結 | 原始資料集來源的連結可從所選服務執行個體的右側邊欄檢視並導覽至。 |
| 編輯執行個體名稱 | 您現在可以修改現有Attribution AI執行個體的名稱。 |
| 複製執行個體 | 複製目前選取的服務執行個體設定，並允許修改。 |
| 修改執行個體組態引數 | 如果現有Attribution AI執行個體尚未開始評分，您現在可以修改其設定。 |
| 單次評分 | 您現在可以在Attribution AI執行個體中觸發臨機模型評分。 |
| 通過欄 | 您現在可以設定要新增至原始輸出分數檔案的其他欄，以新增其他維度至BI工具檢視。 |
| 執行個體啟用和停用 | 您現在可以啟用和停用您的Attribution AI執行個體已排程的模型訓練和評分。 |
| 權益追蹤 | 您可以在建立執行個體容器中找到您的帳戶使用的歸因深入分析總數。 |
| 依位置的接觸點劃分 | 新的深入分析圖表，可依轉換路徑位置提供接觸點分析。 |
| 排名在前的轉換路徑 | 位於「路徑分析」標籤中的新見解圖表。 此圖表包含前五個轉換路徑的清單，顯示帶來最多轉換的行銷管道接觸點順序。 |
| 接觸點有效性 | 針對您的模型用來測量接觸點有效性的最重要三個變數，提供深入分析。 變數是接觸正面與負面路徑的比率、接觸點效率以及接觸點數量。 |

如需詳細資訊，請閱讀[Attribution AI總覽](../../intelligent-services/attribution-ai/overview.md)。

### Customer AI

Customer AI是Intelligent Services的一部分，它讓行銷人員能夠產生個人層面的客戶預測，並提供相關解釋。 在影響因子的協助下，Customer AI可告知您客戶可能會做什麼以及為什麼。 此外，行銷人員可受益於Customer AI預測和深入分析，藉由提供最適合的方案和訊息來打造個人化客戶體驗。

**主要功能**

| 功能 | 說明 |
| ------- | ----------- |
| 資料來源連結 | 原始資料集來源的連結可從所選服務執行個體的右側邊欄檢視並導覽至。 |
| 編輯執行個體名稱 | 您可以修改現有Customer AI執行個體的名稱。 |
| 修改執行個體組態引數 | 如果現有Customer AI執行個體尚未開始評分，您現在可以修改其設定。 |
| 複製執行個體 | 複製目前選取的服務執行個體設定，並允許修改。 |
| 權益追蹤 | 您可以在「建立例項」容器中找到Customer AI為您的帳戶評分的設定檔總數。 |
| 預測目標 | 建立預測目標時的彈性已增強，現在有新的選項可用來預測「將會發生」或「不會發生」某件事。 此外，已新增預測「所有」事件是否發生，或「任何」事件在使用多個事件時發生的選項。 |
| 影響因子深入分析 | 傾向主要影響因素貯體現在包含深入研究。 深入研究是傾向性貯體中每個主要影響因素的值的深入層級摘要。 |

如需詳細資訊，請閱讀[Customer AI總覽](../../intelligent-services/customer-ai/overview.md)。

## 即時客戶輪廓 {#profile}

Adobe Experience Platform 讓您能夠為客戶提供一致且相關的協調體驗，無論他們何時何地與您的品牌互動。透過即時客戶輪廓，您可查看每個個別客戶合併了多個管道的資料 (包括線上、離線、CRM 和協力廠商資料) 的整體檢視。 [!DNL Profile]可讓您將不同的客戶資料合併成統一的檢視表，針對每個客戶互動提供可採取行動且附有時間戳記的說明。

**主要功能**

| 功能 | 說明 |
| ------- | ----------- |
| 已更新合併原則工作流程 | Experience Platform已將合併原則設定升級為新的逐步工作流程。 此工作流程可讓使用者將多個設定檔資料集的資料片段彙整在一起，並設定這些資料集間資料合併方式的優先順序，以便建立每個人的完整檢視。 使用者可以合併所選的XDM個別設定檔資料集，方法是選取適當的合併方法（依時間戳記或資料集優先順序），並將ExperienceEvent資料集附加至設定檔資料集。 |
| 聯合結構描述檢視 | 在Experience Platform UI中，使用者可以更輕鬆地找到有關貢獻聯合結構的所有結構描述和資料集的資訊，以及表面關鍵屬性，例如身分和關係欄位。 這些更新可改善疑難排解功能，並驗證設定檔是否已正確設定、身分是否已正確連結，以及資料是否已成功內嵌。 |

如需即時客戶個人檔案的詳細資訊，包括使用[!DNL Profile]資料的教學課程和最佳實務，請閱讀[即時客戶個人檔案總覽](../../profile/home.md)。

## [!DNL Sources] {#sources}

Adobe Experience Platform可從外部來源擷取資料，同時允許您使用[!DNL Experience Platform]服務來建構、加標籤及增強該資料。 您可以內嵌來自各種來源的資料，例如Adobe應用程式、雲端儲存、協力廠商軟體和您的CRM系統。

[!DNL Experience Platform]提供RESTful API和互動式UI，讓您輕鬆設定各種資料提供者的來源連線。 這些來源連線可讓您進行驗證並連線到外部儲存系統和 CRM 服務、設定攝取執行的時間並管理資料攝取輸送量。

**新的來源**

| 功能 | 說明 |
| ------- | ----------- |
| [!DNL Shopify] | 您現在可以使用[!DNL Flow Service] API或UI連線[!DNL Shopify]至[!DNL Experience Platform]。 如需詳細資訊，請參閱[Shopify聯結器總覽](../../sources/connectors/ecommerce/shopify.md)。 |

**主要功能**

| 功能 | 說明 |
| ------- | ----------- |
| 更新連線資訊 | 您現在可以使用[!DNL Flow Service] API和UI更新現有批次連線的名稱、說明和認證。 如需詳細資訊，請參閱有關[使用流程服務API更新連線](../../sources/tutorials/api/update.md)和[使用UI編輯帳戶詳細資料](../../sources/tutorials/ui/monitor.md)的教學課程。 |
| 刪除連線 | 現在可以使用[!DNL Flow Service] API和UI刪除含有錯誤或變得不必要的批次連線。 如需詳細資訊，請參閱教學課程，瞭解如何使用[使用流程服務API刪除連線](../../sources/tutorials/api/delete.md)，以及使用UI](../../sources/tutorials/ui/delete-accounts.md)刪除帳戶[。 |
| 階層對應 | 您可以在資料擷取程式期間預覽階層式來源檔案，例如JSON或Parquet。 如需詳細資訊，請參閱有關[在UI](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md)中為雲端儲存聯結器設定資料流的教學課程。 |
| API支援串流來源中的對應 | 您現在可以使用API來透過串流來源執行對應功能。 |
| 雲端儲存空間來源的自訂分隔符號的API支援 | 您現在可以使用雲端儲存空間來源收集非CSV分隔的檔案。 您可以使用任何單一欄分隔符號（例如定位字元、逗號、垂直號、分號或雜湊）來收集任何格式的平面檔案。 |
| Adobe Audience Manager聯結器的沙箱支援 | Audience Manager聯結器現在可辨識沙箱。 使用者可以啟用聯結器，將Audience Manager資料集路由到他們選擇的沙箱（包括非生產沙箱）。 每個組織的設定限製為一個沙箱。 |
| UX改進 | 現在可透過來源目錄存取檔案式內嵌。 |

若要深入瞭解來源，請參閱[來源概觀](../../sources/home.md)。
