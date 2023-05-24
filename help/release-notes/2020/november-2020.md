---
title: Adobe Experience Platform發行說明2020年11月
description: 2020年11月為Adobe Experience Platform發佈的說明。
doc-type: release notes
last-update: November 10, 2020
author: crhoades, ens25212
exl-id: 29179b56-e49a-44e8-8c64-a7c383c2eaaf
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '2182'
ht-degree: 5%

---

# Adobe Experience Platform 發行說明

**發行日期：2020 年 11 月 11 日**

Adobe Experience Platform的新功能：

- [Adobe Experience Platform資料湖遷移](#migration)
- [[!DNL Access control]](#access-control)
- [[!DNL Offer Decisioning]](#offer-decisioning)
- [[!DNL Sandboxes]](#sandboxes)

對現有功能的更新：

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Destinations] 服務](#destinations)
- [[!DNL Intelligent Services]](#intelligent-services)
- [[!DNL Real-Time Customer Profile]](#profile)
- [[!DNL Sources]](#sources)

## Adobe Experience Platform資料湖遷移 {#migration}

當Adobe將Data Lake從Gen1遷移到Gen2時，用戶將能夠從Data Lake中讀取，但寫入Data Lake的所有功能都將受到影響。 Adobe將聯繫系統管理員，詳細討論遷移的影響，並確認特定組織的遷移日期和時間。

有關詳細資訊，請閱讀 [資料湖遷移指南](../../landing/adls2-gen2-migration.md)。

## [!DNL Access control] {#access-control}

[!DNL Experience Platform] 利用 [Adobe Admin Console](https://adminconsole.adobe.com) 產品配置檔案，用於將用戶與權限和沙箱連結起來。 權限控制對各種平台功能的訪問，包括資料建模、配置檔案管理和沙盒管理。

**主要功能**

| 功能 | 說明 |
| ------- | ----------- |
| 權限 | 在 [!DNL Admin Console]，則 [!DNL Platform] 產品配置檔案允許您定制 [!DNL Platform] 權能可用於附加到該配置檔案的用戶。 可用權限類別包括： **[!UICONTROL 資料建模]**。 **[!UICONTROL 資料管理]**。 **[!UICONTROL 配置檔案管理]**。 **[!UICONTROL Identity Management]**。 **[!UICONTROL 資料監視]**。 **[!UICONTROL 沙盒管理]**。 **[!UICONTROL 目標]**。 **[!UICONTROL 資料接收]**。 **[!UICONTROL 資料科學工作區]**。 **[!UICONTROL 查詢服務]**, **[!UICONTROL 資料治理]**。 |
| 訪問沙箱 | 的 **[!UICONTROL 權限]** 頁籤 [!DNL Platform] 產品配置檔案可授予用戶對特定沙箱的訪問權限。 請參閱 [沙箱](#sandboxes) 下面的。 |

有關詳細資訊，請參閱 [訪問控制概述](../../access-control/home.md)。

## [!DNL Offer Decisioning] {#offer-decisioning}

[!DNL Offer Decisioning] 是與 [!DNL Experience Platform]。 它允許你利用 [!DNL Platform] 在適當的時間跨所有接觸點為客戶提供最佳的服務和體驗。

**主要功能**

| 功能 | 說明 |
| ------- | ----------- |
| 集中式服務庫 | 建立和管理構成聘用的不同元素並定義其規則和約束的介面。 |
| 提供決策引擎 | 服務決策引擎利用 [!DNL Platform] 資料 [!DNL Real-Time Customer Profiles]與「優惠庫」一起，選擇合適的時間、客戶和渠道來提供優惠。 |

有關詳細資訊，請參閱 [[!DNL Offer Decisioning]](https://experienceleague.adobe.com/docs/offer-decisioning/using/offer-decisioning-home.html?lang=zh-Hant) 文檔。

## [!DNL Sandboxes] {#sandboxes}

[!DNL Experience Platform] 旨在在全球範圍豐富數字型驗應用。 公司通常並行運行多個數字型驗應用程式，需要滿足這些應用程式的開發、測試和部署需要，同時確保操作合規性。 為了滿足這一需求， [!DNL Experience Platform] 提供將單個 [!DNL Platform] 實例到獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

**主要功能**

| 功能 | 說明 |
| ------- | ----------- |
| 生產沙盒 | [!DNL Experience Platform] 提供一個無法刪除或重置的單個生產沙盒。 可用沙箱（生產及非生產）總數由所取得之牌照釐定。 |
| 非生產沙箱 | 可以為單個沙箱建立多個非生產沙箱 [!DNL Platform] 實例，允許您test功能、運行實驗和進行自定義配置，而不影響生產沙箱。 |
| 沙盒切換器 | 在 [!DNL Experience Platform] 用戶介面，螢幕左上角的沙盒切換器允許您通過下拉菜單在可用沙盒之間切換。 沙盒切換器還提供了搜索功能，允許您過濾可用沙盒。 |
| `x-sandbox-name` 標題 | 所有呼叫 [!DNL Experience Platform] API現在必須包括新 `x-sandbox-name` 標題，其值引用 `name` 操作將在中進行的沙盒的屬性。 |

有關詳細資訊，請參閱 [箱概述](../../sandboxes/home.md)。

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] 允許資料工程師將資料映射到體驗資料模型(XDM)並驗證資料。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 迭代運算 | [!DNL Data Prep] 映射器現在支援在層次上執行迭代操作。 |
| 映射器函式 | [!DNL Data Prep] 映射器現在能夠 **不** 將屬性從源複製到目標XDM。 |

有關詳細資訊，請參閱 [[!DNL Data Prep] 概述](../../data-prep/home.md)。

## Data Science Workspace {#dsw}

Data Science Workspace使用機器學習和人工智慧從資料中建立洞見。 整合到Adobe Experience Platform的Data Science Workspace可幫助您跨Adobe解決方案使用內容和資料資產進行預測。 「資料科學工作區」(Data Science Workspace)完成此操作的方法之一是使用 [!DNL JupyterLab]。 [!DNL JupyterLab] 是基於Web的用戶介面 [[!DNL Project Jupyter]](https://jupyter.org/) 並且緊密融入Adobe Experience Platform。 它為資料科學家提供了一個互動式開發環境 [!DNL Jupyter] 筆記本、代碼和資料。

**主要功能**

| 功能 | 說明 |
| ------- | ----------- |
| [!DNL JupyterLab] 處方生成器模板 | 筆記本至處方要求使用和版本已更新。 [!DNL Python] ML運行時基本映像已更新為使用 [!DNL Python] 3.6.7和 [!DNL Conda] 僅限於環境。 |

有關詳細資訊，請閱讀 [使用Jupyter筆記本建立配方](../../data-science-workspace/jupyterlab/create-a-model.md)。

## [!DNL Destinations] 服務 {#destinations}

在 [Real-time Customer Data Platform](../../rtcdp/overview.md)，目標是與目標平台預構建的整合，這些平台可以無縫地向這些合作夥伴激活資料。

**新目標**

| 目的地 | 說明 |
| ----------- | ----------- |
| 佈雷茲 | Braze是一個全面的客戶參與平台，為客戶和他們喜愛的品牌之間提供相關而令人難忘的體驗。 |
| Microsoft兵 | Microsoft必應目標可幫助您執行重定目標，並在Microsoft顯示廣告中針對受眾開展針對性的數字活動。 |
| 交易台 | 交易台是一個自助服務平台，供廣告購買者跨顯示器、視頻和移動庫存來源執行重定目標和受眾定向數字活動。 |

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 目標詳細資訊UX更新 | Real-Time CDP的目標工作流現在包括內聯監視，以便您可以查看哪些批處理激活成功。 此功能將允許用戶通過警報和監控面板直接解決批處理目標的工作流中的問題，以跟蹤處理管道中的錯誤。 |
| 檔案加密 | 對於基於檔案的目標，用戶現在可以向其導出的檔案添加加密。 |
| 檔案計畫 | 對於基於電子郵件和雲儲存的目標，用戶可以建立一次性導出或建立每日快照。 |
| 必填欄位 | 用戶可以將欄位標籤為強制欄位，確保只導出包含該強制欄位的欄位。 |

有關詳細資訊，請參閱 [目標概述](../../destinations/home.md)。

## Intelligent Services {#intelligent-services}

智慧服務使營銷分析師和從業人員能夠利用人工智慧和機器學習在客戶體驗使用案例中的威力。 這使市場營銷分析員能夠使用業務級配置來設定特定於公司需要的預測，而無需資料科學專業知識。

**主要功能**

| 功能 | 說明 |
| ------- | ----------- |
| 消費者體驗事件(CEE)資料集 | 現在，建立CEE資料集支援使用模式編輯器向資料集添加標識欄位。 Attribution AI和客戶AI使用主標識來組合事件。 |

有關詳細資訊，請閱讀 [向資料集添加標識欄位](../../intelligent-services/data-preparation.md#add-identity-fields-to-the-dataset) 中的「智慧服務」資料準備指南。

### Attribution AI

Attribution AI，作為智慧服務的一部分，是一種多渠道的算法歸屬服務，它計算客戶交互對特定結果的影響和增量影響。

**主要功能**

| 功能 | 說明 |
| ------- | ----------- |
| 資料源連結 | 可以從所選服務實例的右欄查看和導航到到原始資料集源的連結。 |
| 編輯實例名稱 | 現在可以修改現有Attribution AI實例的名稱。 |
| 克隆實例 | 複製當前選定的服務實例設定並允許修改。 |
| 修改實例配置參數 | 現在，如果現有Attribution AI實例尚未開始計分，則可以修改其配置。 |
| 一個 | 現在，您可以在Attribution AI實例中觸發即席模型計分。 |
| 傳遞列 | 現在，您可以配置將添加到原始輸出分數檔案的附加列，以將附加維添加到BI工具視圖。 |
| 實例激活和取消激活 | 現在，您可以激活並取消激活計畫的模型培訓和Attribution AI實例的評分。 |
| 權利跟蹤 | 您可以在建立實例容器中查找帳戶使用的屬性洞察總量。 |
| 按位置分析的觸地點故障 | 提供按轉換路徑位置分析觸點的新透視圖。 |
| 頂部轉換路徑 | 位於「路徑分析」(Path Analysis)頁籤中的新透視圖。 該圖表包含前五個轉換路徑的清單，這些路徑顯示了導致最多轉換的營銷渠道觸點的順序。 |
| 觸點效能 | 深入瞭解模型衡量觸地效率的三個最重要變數。 變數為正、負接觸路徑比、觸點效率、觸點體積。 |

有關詳細資訊，請閱讀 [Attribution AI概述](../../intelligent-services/attribution-ai/overview.md)。

### 客戶AI

作為智慧服務的一部分，客戶人工智慧為營銷人員提供了在個人級別生成客戶預測並提供解釋的能力。 在影響因子的協助下，Customer AI 可告知您客戶可能會有什麼行為以及原因何在。 此外，行銷人員可受益於 Customer AI 預測和洞見，藉由提供最適合的方案和訊息來打造個人化客戶體驗。

**主要功能**

| 功能 | 說明 |
| ------- | ----------- |
| 資料源連結 | 可以從所選服務實例的右欄查看和導航到到原始資料集源的連結。 |
| 編輯實例名稱 | 您可以修改現有客戶AI實例的名稱。 |
| 修改實例配置參數 | 現在，如果現有客戶AI實例尚未啟動計分，則可以修改其配置。 |
| 克隆實例 | 複製當前選定的服務實例設定並允許修改。 |
| 權利跟蹤 | 您可以在建立實例容器中查找由客戶AI為您的帳戶評分的配置檔案總數。 |
| 預測目標 | 通過新的選擇來預測「將發生」還是「不會發生」，在制定預測目標方面的靈活性得到了提高。 此外，還添加了用於預測在使用多個事件時「所有」事件是發生還是「任何」事件發生的選項。 |
| 影響因素細化 | 傾向性最大影響因素桶現在包含追溯。 追溯是對傾向時段內每個最主要影響因素的值進行更深入的匯總。 |

有關詳細資訊，請閱讀 [客戶AI概述](../../intelligent-services/customer-ai/overview.md)。

## 即時客戶設定檔 {#profile}

Adobe Experience Platform使您能夠為您的客戶提供協調、一致和相關的體驗，無論客戶在何處或何時與您的品牌進行交互。 使用即時客戶配置檔案，您可以看到每個客戶的整體視圖，該視圖將來自多個渠道的資料組合在一起，包括線上、離線、CRM和第三方資料。 [!DNL Profile] 允許您將全異的客戶資料整合到一個統一視圖中，為每個客戶交互提供一個可操作且時間戳記的帳戶。

**主要功能**

| 功能 | 說明 |
| ------- | ----------- |
| 更新的合併策略工作流 | 平台已將合併策略配置升級為新的逐步式工作流。 此工作流使用戶能夠將來自多個Profile資料集的資料片段集合起來，並設定如何在這些資料集上合併資料的優先順序，以便建立每個個體的全面視圖。 用戶可以通過選擇適當的合併方法（按時間戳順序或資料集優先順序）和將ExperienceEvent資料集附加到Profile資料集來合併選定的XDM Individual Profile資料集。 |
| 聯合架構視圖 | 在Experience PlatformUI中，用戶可以更輕鬆地找到有關所有模式和對聯合模式有貢獻的資料集的資訊，以及諸如標識和關係欄位等表面鍵屬性。 這些更新提高了故障排除和驗證配置檔案配置正確、標識被正確縫合以及資料已成功接收的能力。 |

有關即時客戶概要資訊的詳細資訊，包括有關使用的教程和最佳做法 [!DNL Profile] 資料，請閱讀 [即時客戶概要資訊概述](../../profile/home.md)。

## [!DNL Sources] {#sources}

Adobe Experience Platform可以從外部源接收資料，同時允許您使用 [!DNL Platform] 服務。 您可以從多種源(如Adobe應用程式、基於雲的儲存、第三方軟體和CRM系統)中接收資料。

[!DNL Experience Platform] 提供了REST風格的API和互動式UI，使您可以輕鬆地為各種資料提供程式設定源連接。 通過這些源連接，您可以驗證並連接到外部儲存系統和CRM服務，設定接收運行時間，並管理資料接收吞吐量。

**新源**

| 功能 | 說明 |
| ------- | ----------- |
| [!DNL Shopify] | 現在可以連接 [!DNL Shopify] 至 [!DNL Experience Platform] 使用 [!DNL Flow Service] API或UI。 查看 [Shopify連接器概述](../../sources/connectors/ecommerce/shopify.md) 的子菜單。 |

**主要功能**

| 功能 | 說明 |
| ------- | ----------- |
| 更新連接資訊 | 現在，您可以使用 [!DNL Flow Service] API和UI。 有關詳細資訊，請參見上的教程 [使用流服務API更新連接](../../sources/tutorials/api/update.md) 和 [使用UI編輯帳戶詳細資訊](../../sources/tutorials/ui/monitor.md)。 |
| 刪除連線 | 現在，可以使用 [!DNL Flow Service] API和UI。 有關詳細資訊，請參見上的教程 [使用流服務API刪除連接](../../sources/tutorials/api/delete.md) 和 [使用UI刪除帳戶](../../sources/tutorials/ui/delete-accounts.md)。 |
| 分層映射 | 在資料接收過程中，可以預覽分層源檔案，如JSON或Parce。 請參閱上的教程 [為UI中的雲儲存連接器配置資料流](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) 的子菜單。 |
| 流源中映射的API支援 | 現在，您可以使用API來使用流源執行映射函式。 |
| API支援雲儲存源的自定義分隔符 | 您現在可以使用雲儲存源收集非CSV分隔的檔案。 可以使用任何單列分隔符（如制表符、逗號、管道、分號或散列）來收集任何格式的平面檔案。 |
| 用於Adobe Audience Manager連接器的沙盒支援 | Audience Manager連接器現在可感知沙盒。 用戶可以使連接器將Audience Manager資料集路由到其選擇的沙盒（包括非生產沙盒）。 每個組織只能有一個沙箱。 |
| UX改進 | 現在可通過源目錄訪問基於檔案的接收。 |

要瞭解有關源的詳細資訊，請參閱 [源概述](../../sources/home.md)。
