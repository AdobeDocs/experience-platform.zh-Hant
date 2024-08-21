---
title: Adobe Experience Platform發行說明2024年8月
description: Adobe Experience Platform 2024 年 8 月版發行說明。
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 019d950e992e6e1ea3264fbc1f141a8bb6bc357a
workflow-type: tm+mt
source-wordcount: '1037'
ht-degree: 27%

---

# Adobe Experience Platform 發行說明

**發行日期： 2024年8月20日**

>[!TIP]
>
>檢視範例使用案例檔案](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/use-cases/overview)的[概觀，以瞭解各種使用案例，例如潛在客戶、贏取等，以及貴組織透過Real-Time CDP可以達成的目標。

Experience Platform現有功能和檔案的更新：

- [目的地](#destinations)
- [體驗資料模式 (XDM)](#xdm)
- [身分識別服務](#identity-service)
- [Segmentation Service](#segmentation)
- [來源](#sources)

## 目的地 {#destinations}

[!DNL Destinations] 是預先建立的和目標平台的整合，可讓來自 Adobe Experience Platform 的資料順暢啟動。您可使用目的地啟用已知和未知的資料，以進行跨通路行銷活動、電子郵件行銷活動、設定目標的廣告活動和其他諸多使用案例。

**新功能或更新的功能** {#destinations-new-updated-functionality}

| 功能 | 說明 |
| ----------- | ----------- |
| 現在一般都能將檔案隨選匯出至批次目的地。 | 所有客戶現在都可以選擇隨選將檔案匯出至批次目的地。 如需詳細資訊，請參閱[專屬檔案](../../destinations/ui/export-file-now.md)。 |
| 在[排程步驟](../../destinations/ui/activate-batch-profile-destinations.md#scheduling)中編輯多個匯出對象的匯出排程。 | 現在，所有客戶都可以使用選項，直接從對象啟用工作流程的排程步驟，編輯多個匯出對象的匯出排程。 ![Experience Platform使用者介面的影像，在排程步驟中醒目提示[編輯排程]選項。](../2024/assets/august/edit-schedule.png){width="250" align="center" zoomable="yes"} |
| 在[排程步驟](../../destinations/ui/activate-batch-profile-destinations.md#scheduling)中編輯多個匯出對象的檔案名稱。 | 現在，所有客戶都可以使用選項，直接從對象啟用工作流程的排程步驟編輯多個匯出檔案的名稱。 ![Experience Platform使用者介面的影像，在排程步驟中醒目提示[編輯檔案名稱]選項。](../2024/assets/august/edit-file-name.png){width="250" align="center" zoomable="yes"} |
| 從[目的地詳細資料](../../destinations/ui/destination-details-page.md#bulk-remove)頁面移除資料流中的多個對象。 | 從&#x200B;**[!UICONTROL 目的地詳細資料]**&#x200B;頁面移除現有資料流中多個對象的選項現在可供所有客戶使用。 ![醒目提示[目的地詳細資料]頁面中[移除對象]選項的Experience Platform使用者介面影像。](../2024/assets/august/bulk-remove-audiences.png){width="250" align="center" zoomable="yes"} |
| 從[目的地詳細資料](../../destinations/ui/destination-details-page.md#bulk-export)頁面，隨選將多個檔案匯出至批次目的地。 | 所有客戶現在都可以選擇從&#x200B;**[!UICONTROL 目的地詳細資料]**&#x200B;頁面，隨選將多個檔案匯出至批次目的地。 ![Experience Platform使用者介面的影像，在「目的地詳細資料」頁面中醒目提示「立即匯出檔案」選項。](../2024/assets/august/bulk-export-file-now.png){width="250" align="center" zoomable="yes"} |
| 從[目的地詳細資料](../../destinations/ui/destination-details-page.md#bulk-edit-file-names)頁面編輯多個匯出對象的檔案名稱。 | 您現在可以直接從&#x200B;**[!UICONTROL 目的地詳細資料]**&#x200B;頁面編輯多個匯出檔案的名稱。 ![Experience Platform使用者介面的影像，在目的地詳細資訊頁面中醒目提示編輯檔案名稱選項。](../2024/assets/august/edit-file-name-destination-details.png){width="250" align="center" zoomable="yes"} |
| 從[目的地詳細資料](../../destinations/ui/export-datasets.md#remove-dataset)頁面移除資料流中的多個資料集。 | 所有客戶現在都可以使用從資料流移除多個資料集的選項。 ![Experience Platform使用者介面的影像，在目的地詳細資訊頁面中醒目提示「移除資料集」選項。](../2024/assets/august/bulk-remove-datasets.png){width="250" align="center" zoomable="yes"} |

{style="table-layout:auto"}

如需詳細資訊，請閱讀[目的地概觀](../../destinations/home.md)。

## 體驗資料模式 (XDM) {#xdm}

XDM 是一種開放原始碼的規格，可為帶到 Adobe Experience Platform 中的資料提供通用結構和定義 (結構描述)。若遵守 XDM 標準，即可將所有客戶體驗資料合併到一個常用表述中，以更快速、更整合的方式傳遞分析。您可以從客戶行為中獲得有價值的分析，透過區段定義客戶對象，並使用客戶屬性實現個人化的目的。

**新功能**

| 功能 | 說明 |
| --- | --- |
| ML輔助的結構描述建立流程 | 使用進階機器學習演演算法來分析範例CSV資料檔案，並使用標準和自訂欄位自動建立最佳化的結構描述。<br>主要功能：<br><ul><li>更快建立方案：使用ML建議和產生的XDM欄位，直接從範例資料檔產生方案。</li><li>靈活的結構描述演化：輕鬆新增或更新產生之結構描述中的欄位。</li><li>緊密整合：與Schema Ul的核心架構建立流程完全整合，確保提供順暢團結的使用者體驗。</li><li>有效率的檢閱和編輯：使用平面檢視編輯器快速檢視和更新您的架構，讓建立過程更有效率且更方便使用。</li></ul> |

{style="table-layout:auto"}

若要深入瞭解，請閱讀[ML輔助結構描述建立概述](../../xdm/ui/ml-assisted-schema-creation.md)

如需有關 Platform 中 XDM 的詳細資訊，請參閱 [XDM 系統概觀](../../xdm/home.md)。

## 身分識別服務 {#identity-service}

使用Adobe Experience Platform Identity Service，透過跨裝置和系統橋接身分，讓您即時提供具影響力的個人數位體驗，進而建立客戶及其行為的全面檢視。

**已更新檔案**

| 功能 | 說明 |
| --- | --- |
| 圖表設定指南 | 請閱讀[圖表組態指南](../../identity-service/identity-graph-linking-rules/example-configurations.md)，以瞭解在使用身分圖表連結規則和身分資料時可能會遇到的常見圖表情境相關資訊。 圖表設定指南提供的範例涵蓋從簡單的單一人員圖表情境到複雜且階層式的多人圖表情境。 您也可以使用指南來取得可在[圖表模擬UI](../../identity-service/identity-graph-linking-rules/graph-simulation.md)中輸入的事件和演演算法設定範例，以及特定圖表情境下如何選取主要身分的劃分。 |

{style="table-layout:auto"}

如需有關Identity服務的詳細資訊，請閱讀[Identity服務概觀](../../identity-service/home.md)。

## Segmentation Service {#segmentation}

[!DNL Segmentation Service] 可讓您將儲存在和個人 (例如客戶、潛在客戶、使用者或組織) 相關的 [!DNL Experience Platform] 中的資料分段為不同的對象。您可以透過區段定義或來自 [!DNL Real-Time Customer Profile] 資料的其他來源建立對象。這些對象會在 [!DNL Platform] 上集中設定及維護，並可透過任何 Adobe 解決方案輕鬆存取。

**更新的功能**

| 功能 | 說明 |
| ------- | ----------- |
| 內嵌詳細資料 | 對於具有自訂上傳來源的對象，您可以在對象詳細資訊頁面中，更全面地檢視對象擷取的詳細資訊。 此外，您可以選取結構並選取要加上標籤的所需屬性，將標籤套用至裝載屬性。 您可以在[對象入口網站指南](../../segmentation/ui/audience-portal.md#ingestion-details)中找到有關內嵌詳細資訊區段的詳細資訊。 |

{style="table-layout:auto"}

如需有關 [!DNL Segmentation Service] 的詳細資訊，請參閱[分段概觀](../../segmentation/home.md)。

## 來源

Experience Platform 可提供 RESTful API 和互動式 UI，可讓您輕鬆為各種資料提供者設定來源連線。這些來源連線可讓您進行驗證並連線到外部儲存系統和 CRM 服務、設定擷取執行的時間並管理資料擷取輸送量。

在Experience Platform中使用來源，從Adobe應用程式或第三方資料來源擷取資料。

**已更新檔案**

| 更新檔案 | 說明 |
| --- | --- |
| 擴充有關更新資料流的檔案 | 已更新UI](../../sources/tutorials/ui/update-dataflows.md)中[更新現有來源資料流程的指南，以提供您可以對現有資料流程進行各種設定的詳細資訊。 指南也經過更新，以釐清已停用資料流重新啟用的預期行為。 |

{style="table-layout:auto"}

如需詳細資訊，請閱讀[來源概觀](../../sources/home.md)。