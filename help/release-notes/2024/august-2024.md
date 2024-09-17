---
title: Adobe Experience Platform 發行說明 (2024 年 8 月)
description: Adobe Experience Platform 2024 年 8 月版發行說明。
exl-id: 153891e9-fd82-4894-a047-c8d82f214fef
source-git-commit: 4fecb47084a522b4eb9808dc317e0d70e7ef42c6
workflow-type: ht
source-wordcount: '1562'
ht-degree: 100%

---

# Adobe Experience Platform 發行說明

**發行日期：2024 年 8 月 20 日**

>[!TIP]
>
>檢視[樣本使用案例概觀文件](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/rtcdp/use-cases/overview)，了解您的組織可以透過 Real-Time CDP 實現的各種使用案例，例如勘探、收購等。

Experience Platform 現有功能及文件的更新：

- [屬性型存取控制](#abac)
- [資料擷取](#data-ingestion)
- [目的地](#destinations)
- [體驗資料模式 (XDM)](#xdm)
- [身分識別服務](#identity-service)
- [Segmentation Service](#segmentation)
- [來源](#sources)

## 屬性型存取控制 {#abac}

屬性型存取控制是 Adobe Experience Platform 的一項功能，為注重隱私的品牌提供更大的靈活性來管理使用者存取。可以將結構描述欄位和分段等個別對象指派給使用者角色。此功能允許您授予或撤銷組織中特定平台使用者對個別物件的存取權限。

透過屬性型存取控制，您組織的管理員可以控制使用者對所有 Platform 工作流程及資源的存取權限，包括其中的敏感個人資料 (SPD)、個人身分資訊 (PII) 和其他自訂類型資料。管理員可以定義只能存取特定欄位以及這些欄位對應資料的使用者角色。

**新功能**

| 功能更新 | 說明 |
| --- | --- |
| 新的權限管理器功能 | 您現在可以利用[權限管理器](../../access-control/abac/permission-manager/overview.md)，使用簡單查詢產生報告，這有助於您了解存取管理，並省下在多個工作流程及詳細程度等級之間驗證存取權限的時間。有關為使用者和角色建立報告的詳細資訊，請參閱[權限管理器使用手冊](../../access-control/abac/permission-manager/permissions.md)。![影像：Experience Platform 使用者介面，左側導覽欄位中標示出「權限管理員」。](assets/august/permission-manager-rn.png "使用者介面中的權限管理器。"){width="250" align="center" zoomable="yes"} |

{style="table-layout:auto"}

若要了解更多關於屬性型存取控制，請參閱[屬性型存取控制概觀](../../access-control/abac/overview.md)。關於屬性型存取控制工作流程的綜合指南，請閱讀[屬性型存取控制端對端指南](../../access-control/abac/end-to-end-guide.md)。

## 資料擷取 (8 月 23 日更新) {#data-ingestion}

Adobe Experience Platform 會提供一組豐富的功能，用於擷取任何類型和任何延遲的資料。您可以使用批次或串流 API (使用 Adobe 建置的來源、資料整合合作夥伴或 Adobe Experience Platform UI) 進行擷取。

**批次資料擷取中的日期格式處理方式更新**

此版本解決了批次資料擷取過程中&#x200B;*日期格式處理*&#x200B;的問題。先前，系統會將用戶端插入的日期欄位從 `Date` 格式轉換為 `DateTime` 格式。這表示會自動將時區添加到欄位中，因而對喜歡或需要 `Date` 格式的使用者造成不便。今後，時區將不會自動添加到 `Date` 類型的欄位中。此更新可確保匯出的資料格式與該欄位設定檔中呈現的客戶要求格式相符。

`Date` 欄位於此版本前的格式：`"birthDate": "2018-01-12T00:00:00Z"`
`Date` 欄位於此版本後的格式：`"birthDate": "2018-01-12"`

詳細了解[批次擷取](/help/ingestion/batch-ingestion/overview.md)。

## 目的地 {#destinations}

[!DNL Destinations] 是預先建立的和目標平台的整合，可讓來自 Adobe Experience Platform 的資料順暢啟動。您可使用目的地啟用已知和未知的資料，以進行跨通路行銷活動、電子郵件行銷活動、設定目標的廣告活動和其他諸多使用案例。

**新目的地或更新的目的地** {#new-updated-destinations}

| 目的地 | 說明 |
| ----------- | ----------- |
| [Braze](/help/destinations/catalog/mobile-engagement/braze.md) | [!UICONTROL Braze] 為其儀表板和 REST 端點管理許多不同的實例。[!UICONTROL Braze] 客戶應根據您所佈建的實例使用正確的 REST 端點。此版本新增了一個新的 US-07 端點，您在連線至 [!UICONTROL Braze] 時可以選取該端點。 |

{style="table-layout:auto"}

**新功能或更新的功能** {#destinations-new-updated-functionality}

| 功能 | 說明 |
| ----------- | ----------- |
| 將檔案隨選匯出至批次目標的功能現已正式推出。 | 所有客戶現在都可以選擇將檔案隨選匯出至批次目標。如需詳細資訊，請參閱[專門文件](../../destinations/ui/export-file-now.md)。 |
| 在[排程步驟](../../destinations/ui/activate-batch-profile-destinations.md#scheduling)中編輯多個匯出客群的匯出排程。 | 現在，所有客戶都可以選擇直接從客群啟用工作流程的排程步驟中，編輯多個匯出客群的匯出排程。![影像：Experience Platform 使用者介面，標示出排程步驟中的「編輯排程」選項。](assets/august/edit-schedule.png "在排程步驟中編輯排程選項。"){width="250" align="center" zoomable="yes"} |
| 在[排程步驟](../../destinations/ui/activate-batch-profile-destinations.md#scheduling)中編輯多個匯出客群的檔案名稱。 | 現在，所有客戶都可以選擇直接從客群啟用工作流程的排程步驟中，編輯多個匯出檔案的名稱。![影像：Experience Platform 使用者介面，標示出排程步驟中的「編輯檔案名稱」選項。](assets/august/edit-file-name.png "排程步驟中的編輯檔案名稱選項。"){width="250" align="center" zoomable="yes"} |
| 自[目標詳細資訊](../../destinations/ui/destination-details-page.md#bulk-remove)頁面的資料流中移除多個客群。 | 所有客戶現在都能選擇自&#x200B;**[!UICONTROL 目標詳細資訊]**&#x200B;頁面的現有資料流中移除多個客群。![影像：Experience Platform 使用者介面，標示出目標詳細資訊頁面中的「移除客群」選項。](assets/august/bulk-remove-audiences.png "目標詳細資訊頁面中的「移除客群」選項。"){width="250" align="center" zoomable="yes"} |
| 自[目標詳細資訊](../../destinations/ui/destination-details-page.md#bulk-export)頁面將多個檔案隨選匯出至批次目標。 | 所有客戶現在都能選擇自&#x200B;**[!UICONTROL 目標詳細資訊]**&#x200B;頁面將多個檔案隨選匯出至批次目標。![影像：Experience Platform 使用者介面，標示出目標詳細資訊頁面中的「立即匯出檔案」選項。](assets/august/bulk-export-file-now.png "目標詳細資訊頁面中的「立即匯出檔案」選項。"){width="250" align="center" zoomable="yes"} |
| 自[目標詳細資訊](../../destinations/ui/destination-details-page.md#bulk-edit-file-names)頁面編輯多個匯出客群的檔案名稱。 | 您現在可以直接自&#x200B;**[!UICONTROL 目標詳細資訊]**&#x200B;頁面編輯多個匯出客群的檔案名稱。![影像：Experience Platform 使用者介面，標示出目標詳細資訊頁面中的「編輯檔案名稱」選項。](assets/august/edit-file-name-destination-details.png "目標詳細資訊頁面中的「編輯檔案名稱」選項。"){width="250" align="center" zoomable="yes"} |
| 自[目標詳細資訊](../../destinations/ui/export-datasets.md#remove-dataset)頁面的資料流中移除多個資料集。 | 所有客戶現在都可以選擇自資料流中移除多個資料集。![影像：Experience Platform 使用者介面，標示出目標詳細資訊頁面中的「移除資料集」選項。](assets/august/bulk-remove-datasets.png "目標詳細資訊頁面中的「移除資料集」選項。"){width="250" align="center" zoomable="yes"} |

{style="table-layout:auto"}

如需詳細資訊，請參閱[目標概觀](../../destinations/home.md)。

## 體驗資料模式 (XDM) {#xdm}

XDM 是一種開放原始碼的規格，可為帶到 Adobe Experience Platform 中的資料提供通用結構和定義 (結構描述)。若遵守 XDM 標準，即可將所有客戶體驗資料合併到一個常用表述中，以更快速、更整合的方式傳遞分析。您可以從客戶行為中獲得有價值的分析，透過區段定義客戶客群，並使用客戶屬性實現個人化的目的。

**新功能**

| 功能 | 說明 |
| --- | --- |
| ML 輔助綱要建立流程 | 使用先進的機器學習演算法來分析您的樣本資料檔案，並使用標準和自訂欄位自動建立最佳化的綱要。<br>主要功能：<br><ul><li>更快地建立綱要：使用 ML 推薦及產生的 XDM 欄位直接從樣本資料檔案產生綱要。</li><li>靈活的綱要演變：輕鬆新增或更新已產生之綱要中的欄位。</li><li>緊密整合：與綱要使用者介面中的核心綱要建立流程完全整合，確保流暢且一致的使用者體驗。</li><li>高效的檢閱和編輯：使用平面視圖編輯器快速檢視及更新您的綱要，讓建立過程更加有效率且使用者友善。</li></ul><br>若要了解更多資訊，請參閱 [ML 輔助綱要建立工作流程指南](../../xdm/ui/ml-assisted-schema-creation.md)。 |

{style="table-layout:auto"}

如需有關 Platform 中 XDM 的詳細資訊，請參閱 [XDM 系統概觀](../../xdm/home.md)。

## 身分識別服務 {#identity-service}

使用 Adobe Experience Platform 身分服務，於裝置及系統間進行身分橋接，建立客戶及其行為的全方位檢視，讓您能夠即時實現具有影響力的個人數位體驗。

**更新的文件**

| 功能 | 說明 |
| --- | --- |
| 圖表設定指南 | 請參閱[圖表設定指南](../../identity-service/identity-graph-linking-rules/example-configurations.md)，了解使用識別圖連結規則和身分資料時，可能遇到的常見圖表情境之相關資訊。圖表設定指南提供從簡單的單人圖表情境，到複雜且分層之多人圖表情境的範例。您還能夠使用該指南來取得可以放在[圖表模擬使用者介面](../../identity-service/identity-graph-linking-rules/graph-simulation.md)中的事件和演算法設定範例，以及在特定圖表情境下選取主要身份方法的詳細解析說明。 |

{style="table-layout:auto"}

若要了解更多有關身分服務的資訊，請參閱[身分服務概觀](../../identity-service/home.md)。

## Segmentation Service {#segmentation}

[!DNL Segmentation Service] 可讓您將儲存在和個人 (例如客戶、潛在客戶、使用者或組織) 相關的 [!DNL Experience Platform] 中的資料分段為不同的客群。您可以透過區段定義或來自 [!DNL Real-Time Customer Profile] 資料的其他來源建立客群。這些客群會在 [!DNL Platform] 上集中設定及維護，並可透過任何 Adobe 解決方案輕鬆存取。

**更新的功能**

| 功能 | 說明 |
| ------- | ----------- |
| 內嵌詳細資料 | 對於具有自訂上傳來源的客群，您可以在客群詳細資訊頁面中更全方位地檢視客群擷取的詳細資訊。此外，您可以透過選取綱要及選取所需的標籤屬性來將標籤套用至承載屬性上。有關擷取詳細資訊區段的進一步內容，請參閱[客群入口網站指南](../../segmentation/ui/audience-portal.md#ingestion-details)。 |

{style="table-layout:auto"}

如需有關 [!DNL Segmentation Service] 的詳細資訊，請參閱[分段概觀](../../segmentation/home.md)。

## 來源

Experience Platform 可提供 RESTful API 和互動式 UI，可讓您輕鬆為各種資料提供者設定來源連線。這些來源連線可讓您進行驗證並連線到外部儲存系統和 CRM 服務、設定擷取執行的時間並管理資料擷取輸送量。

使用 Experience Platform 中的來源，自 Adobe 應用程式或第三方資料來源擷取資料。

**更新的功能**

| 功能 | 說明 |
| --- | --- |
| Adobe Analytics 來源連接器的更新 | 由於 Analytics 來源連接器完全由 Adobe 管理，因此資料集活動頁面不會顯示有關批次的資訊。您可以透過查看已擷取記錄的相關指標來監控資料流動。如需詳細資訊，請參閱建立 [Analytics 資料之來源連線](../../sources/tutorials/ui/create/adobe-applications/analytics.md)的指南。 |

**更新的文件**

| 更新的文件 | 說明 |
| --- | --- |
| 有關更新資料流的擴充文件 | [在使用者介面中更新現有來源資料流](../../sources/tutorials/ui/update-dataflows.md)的指南已更新，針對現有資料流能夠進行的各種設定提供進一步資訊。該指南的更新也釐清了重新啟用已停用之資料流時的預期行為。 |

{style="table-layout:auto"}

如需詳細資訊，請參閱[來源概觀](../../sources/home.md)。
