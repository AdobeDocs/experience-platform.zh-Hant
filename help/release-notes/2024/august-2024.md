---
title: Adobe Experience Platform 發行說明 (2024 年 8 月)
description: Adobe Experience Platform 2024 年 8 月版發行說明。
exl-id: 153891e9-fd82-4894-a047-c8d82f214fef
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1565'
ht-degree: 95%

---

# Adobe Experience Platform 發行說明

**發行日期：2024 年 8 月 20 日**

>[!TIP]
>
>檢視[樣本使用案例概觀文件](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/rtcdp/use-cases/overview)，即可了解您的組織能夠透過 Real-Time CDP 實現的各種使用案例，例如勘探、收購等。

Experience Platform 現有功能及文件的更新：

- [屬性型存取控制](#abac)
- [資料攝取](#data-ingestion)
- [目標](#destinations)
- [體驗資料模式 (XDM)](#xdm)
- [身分識別服務](#identity-service)
- [Segmentation Service](#segmentation)
- [來源](#sources)

## 屬性型存取控制 {#abac}

屬性型存取控制是 Adobe Experience Platform 的一項功能，為注重隱私的品牌提供更大的彈性來管理使用者存取。可以將結構描述欄位和分段等個別物件指派給使用者角色。此功能可讓您為貴組織中的特定Experience Platform使用者授予或撤銷個別物件的存取權。

透過以屬性為基礎的存取控制，您組織的管理員可以控制使用者對所有Experience Platform工作流程和資源的敏感個人資料(SPD)、個人識別資訊(PII)及其他自訂資料型別的存取。 管理員可以將使用者角色定義為只能存取特定欄位及這些欄位對應的資料。

**新功能**

| 功能更新 | 說明 |
| --- | --- |
| 新的權限管理器功能 | 您現在可以利用[權限管理器](../../access-control/abac/permission-manager/overview.md)，透過簡易查詢來產生報告；這有助於您了解存取管理，並省下在多個工作流程及詳細程度等級之間驗證存取權限的時間。有關為使用者和角色建立報告的詳細資訊，請參閱[權限管理器使用手冊](../../access-control/abac/permission-manager/permissions.md)。![影像：Experience Platform 使用者介面，左側導覽欄位中特別標示「權限管理員」。](assets/august/permission-manager-rn.png "使用者介面中的權限管理器。"){width="250" align="center" zoomable="yes"} |

{style="table-layout:auto"}

若要了解更多關於屬性型存取控制，請參閱[屬性型存取控制概觀](../../access-control/abac/overview.md)。關於屬性型存取控制工作流程的綜合指南，請閱讀[屬性型存取控制端對端指南](../../access-control/abac/end-to-end-guide.md)。

## 資料攝取 (8 月 23 日更新) {#data-ingestion}

Adobe Experience Platform 會提供一組豐富的功能，用於攝取任何類型和任何延遲的資料。您可以使用批次或串流 API (使用 Adobe 建置的來源、資料整合合作夥伴或 Adobe Experience Platform UI) 進行攝取。

**批次資料攝取中的日期格式處理方式更新**

此版本解決了批次資料攝取過程中&#x200B;*日期格式處理*&#x200B;的問題。先前系統會將用戶端插入的日期欄位從 `Date` 格式轉換為 `DateTime` 格式。這表示時區已自動新增到欄位中，因而對偏好或需要 `Date` 格式的使用者造成不便。今後，時區將不會自動新增到 `Date` 類型的欄位中。此更新可確保匯出的資料格式會依照客戶要求，與該欄位輪廓中呈現的格式相符。

`Date` 欄位於此版本之前的格式：`"birthDate": "2018-01-12T00:00:00Z"`
`Date` 欄位於此版本之後的格式：`"birthDate": "2018-01-12"`

閱讀更多有關[批次攝取](/help/ingestion/batch-ingestion/overview.md)的資訊。

## 目標 {#destinations}

[!DNL Destinations] 是與目標平台的預先建立整合，能夠順暢啟用來自 Adobe Experience Platform 的資料。您可以使用目標啟用已知和未知的資料，以進行跨通路行銷活動、電子郵件行銷活動、定向廣告和其他諸多使用案例。

**新目標或更新的目標** {#new-updated-destinations}

| 目標 | 說明 |
| ----------- | ----------- |
| [Braze](/help/destinations/catalog/mobile-engagement/braze.md) | [!UICONTROL Braze] 為其儀表板和 REST 端點管理許多不同的執行個體。[!UICONTROL Braze] 客戶應根據您佈建的執行個體來使用正確的 REST 端點。此版本新增了一個 US-07 端點，可供您在連線至 [!UICONTROL Braze] 時選取。 |

{style="table-layout:auto"}

**新功能或更新的功能** {#destinations-new-updated-functionality}

| 功能 | 說明 |
| ----------- | ----------- |
| 將檔案隨選匯出至批次目標的功能現已正式推出。 | 所有客戶現在都可以選擇將檔案隨選匯出至批次目標。如需詳細資訊，請參閱[專用文件](../../destinations/ui/export-file-now.md)。 |
| 在[排程步驟](../../destinations/ui/activate-batch-profile-destinations.md#scheduling)中為多個匯出的客群編輯匯出排程。 | 現在起，所有客戶都可以選擇直接從客群啟用工作流程的排程步驟中，為多個匯出的客群編輯匯出排程。![影像：Experience Platform 使用者介面，特別標示出排程步驟中的「編輯排程」選項。](assets/august/edit-schedule.png "在排程步驟中編輯排程選項。"){width="250" align="center" zoomable="yes"} |
| 在[排程步驟](../../destinations/ui/activate-batch-profile-destinations.md#scheduling)中為多個匯出的客群編輯檔案名稱。 | 現在起，所有客戶都可以選擇直接從客群啟用工作流程的排程步驟中，為多個匯出檔案編輯名稱。![影像：Experience Platform 使用者介面，特別標示出排程步驟中的「編輯檔案名稱」選項。](assets/august/edit-file-name.png "排程步驟中的「編輯檔案名稱」選項。"){width="250" align="center" zoomable="yes"} |
| 從「[目標詳細資料](../../destinations/ui/destination-details-page.md#bulk-remove)」頁面的資料流中移除多個客群。 | 所有客戶現在都能選擇從「**[!UICONTROL 目標詳細資料]**」頁面的現有資料流中移除多個客群。![影像：Experience Platform 使用者介面，特別標示出「目標詳細資料」頁面中的「移除客群」選項。](assets/august/bulk-remove-audiences.png "「目標詳細資料」頁面中的「移除客群」選項。"){width="250" align="center" zoomable="yes"} |
| 從「[目標詳細資料](../../destinations/ui/destination-details-page.md#bulk-export)」頁面將多個檔案隨選匯出至批次目標。 | 所有客戶現在都能選擇從「**[!UICONTROL 目標詳細資料]**」頁面將多個檔案隨選匯出至批次目標。![影像：Experience Platform 使用者介面，特別標示出「目標詳細資料」頁面中的「立即匯出檔案」選項。](assets/august/bulk-export-file-now.png "「目標詳細資料」頁面中的「立即匯出檔案」選項。"){width="250" align="center" zoomable="yes"} |
| 從「[目標詳細資料](../../destinations/ui/destination-details-page.md#bulk-edit-file-names)」頁面為多個匯出的客群編輯檔案名稱。 | 您現在可以直接從「**[!UICONTROL 目標詳細資料]**」頁面為多個匯出的客群編輯檔案名稱。![影像：Experience Platform 使用者介面，特別標示出「目標詳細資料」頁面中的「編輯檔案名稱」選項。](assets/august/edit-file-name-destination-details.png "「目標詳細資料」頁面中的「編輯檔案名稱」選項。"){width="250" align="center" zoomable="yes"} |
| 從「[目標詳細資料](../../destinations/ui/export-datasets.md#remove-dataset)」頁面的資料流中移除多個資料集。 | 所有客戶現在都可以選擇從資料流中移除多個資料集。![影像：Experience Platform 使用者介面，特別標示出「目標詳細資料」頁面中的「移除資料集」選項。](assets/august/bulk-remove-datasets.png "「目標詳細資料」頁面中的「移除資料集」選項。"){width="250" align="center" zoomable="yes"} |

{style="table-layout:auto"}

如需詳細資訊，請閱讀[目標概觀](../../destinations/home.md)。

## 體驗資料模式 (XDM) {#xdm}

XDM 是一種開放原始碼的規格，可為帶到 Adobe Experience Platform 中的資料提供通用結構和定義 (結構描述)。若遵守 XDM 標準，即可將所有客戶體驗資料合併到一個常用表述中，以更快速、更整合的方式傳遞分析。您可以從客戶行為中獲得有價值的分析，透過區段定義客戶客群，並使用客戶屬性實現個人化的目的。

**新功能**

| 功能 | 說明 |
| --- | --- |
| ML 輔助結構描述建立流程 | 使用進階的機器學習演算法可分析您的樣本資料檔案，並使用標準和自訂欄位來自動建立最佳化的結構描述。<br>主要功能：<br><ul><li>更快建立結構描述：使用 ML 推薦及產生的 XDM 欄位，直接從樣本資料檔案產生結構描述。</li><li>靈活的結構描述演變：輕鬆新增或更新已產生之結構描述中的欄位。</li><li>緊密整合：與結構描述使用者介面中的核心結構描述建立流程完全整合，確保流暢且一致的使用者體驗。</li><li>高效的檢閱和編輯：使用平面檢視編輯器快速檢視和更新結構描述，讓建立過程更有效率且適合使用者使用。</li></ul><br>若要深入了解，請閱讀 [ML 輔助結構描述建立工作流程指南](../../xdm/ui/ml-assisted-schema-creation.md)。 |

{style="table-layout:auto"}

如需Experience Platform中XDM的詳細資訊，請參閱[XDM系統總覽](../../xdm/home.md)。

## 身分識別服務 {#identity-service}

使用 Adobe Experience Platform 身分識別服務，可在裝置及系統間進行身分識別橋接來建立客戶及其行為的全方位檢視，從而讓您即時實現具影響力的個人數位體驗。

**更新的文件**

| 功能 | 說明 |
| --- | --- |
| 圖表設定指南 | 閱讀[圖表設定指南](../../identity-service/identity-graph-linking-rules/example-configurations.md)可了解使用身分識別圖連結規則和身分識別資料時，可能遇到之常見圖表情境的相關資訊。圖表設定指南提供從簡易單人圖表情境到複雜且分層之多人圖表情境的範例。您也能夠使用該指南來取得可輸入到[圖表模擬使用者介面](../../identity-service/identity-graph-linking-rules/graph-simulation.md)中的事件和演算法設定範例，以及如何在特定圖表情境下選取主要身分識別的詳細說明。 |

{style="table-layout:auto"}

若要深入了解身分識別服務，請閱讀[身分識別服務概觀](../../identity-service/home.md)。

## Segmentation Service {#segmentation}

[!DNL Segmentation Service] 可讓您將儲存在和個人 (例如客戶、潛在客戶、使用者或組織) 相關的 [!DNL Experience Platform] 中的資料分段為不同的客群。您可以透過區段定義或來自 [!DNL Real-Time Customer Profile] 資料的其他來源建立客群。這些客群會在 [!DNL Experience Platform] 上集中設定及維護，並可透過任何 Adobe 解決方案輕鬆存取。

**更新的功能**

| 功能 | 說明 |
| ------- | ----------- |
| 攝取詳細資料 | 對於具有自訂上傳來源的客群，您可以在客群詳細資料頁面中更全方位地檢視客群攝取的詳細資料。此外，您還可以透過選取結構描述及選取所需標籤屬性，將標籤套用至承載屬性上。如要深入了解攝取詳細資料區段，請參閱 [Audience Portal 指南](../../segmentation/ui/audience-portal.md#ingestion-details)。 |

{style="table-layout:auto"}

如需有關 [!DNL Segmentation Service] 的詳細資訊，請參閱[分段概觀](../../segmentation/home.md)。

## 來源

Experience Platform 可提供 RESTful API 和互動式 UI，可讓您輕鬆為各種資料提供者設定來源連線。這些來源連線可讓您進行驗證並連線到外部儲存系統和 CRM 服務、設定攝取執行的時間並管理資料攝取輸送量。

使用 Experience Platform 中的來源，即可從 Adobe 應用程式或第三方資料來源攝取資料。

**更新的功能**

| 功能 | 說明 |
| --- | --- |
| Adobe Analytics 來源連接器的更新 | 由於 Analytics 來源連接器完全由 Adobe 管理，因此資料集活動頁面不會顯示有關批次的資訊。您可以透過查看已攝取記錄的相關指標來監控資料的流動。如需詳細資訊，請閱讀建立 [Analytics 資料之來源連線](../../sources/tutorials/ui/create/adobe-applications/analytics.md)的指南。 |

**更新的文件**

| 更新的文件 | 說明 |
| --- | --- |
| 擴充有關更新資料流的文件 | [在使用者介面中更新現有來源資料流](../../sources/tutorials/ui/update-dataflows.md)的指南已更新，針對現有資料流能夠進行的各種設定提供更多資訊。該指南的更新也釐清了重新啟用已停用之資料流時的預期行為。 |

{style="table-layout:auto"}

如需詳細資訊，請閱讀[來源概觀](../../sources/home.md)。
