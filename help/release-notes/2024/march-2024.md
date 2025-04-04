---
title: Adobe Experience Platform 發行說明 (2024 年 3 月)
description: Adobe Experience Platform 2024 年 3 月版發行說明。
exl-id: cab47a76-04f3-48ec-82aa-d17645e4eb15
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1192'
ht-degree: 97%

---

# Adobe Experience Platform 發行說明

**發行日期：2024 年 3 月 19 日**

>[!TIP]
>
>利用 [Adobe Experience Platform 字彙表](/help/landing/glossary.md)可熟悉 Real-Time Customer Data Platform 及 Adobe Experience Platform 中使用的字詞。若找不到您想查看的特定字詞，請使用頁面上的意見回饋選項，要求將新的字詞加到字彙表中。

Experience Platform 現有功能的更新：

- [目錄服務](#catalog-service)
- [資料彙集](#data-collection)
- [資料準備](#data-prep)
- [目標](#destinations)
- [體驗資料模式 (XDM)](#xdm)
- [Segmentation Service](#segmentation)
- [來源](#sources)

## 目錄服務 {#catalog-service}

目錄服務是 Adobe Experience Platform 內部的資料位置和譜系記錄系統。雖然攝取至 Experience Platform 中的所有資料都會以檔案及目錄形式儲存在資料湖中，但是為了查詢和監控目的，目錄也會保留這些檔案及目錄的中繼資料與說明。

| 功能 | 說明 |
| --- | --- |
| 更多動作 | 為了使操作更加靈活並協助您管理資料，您現在可以使用詳細檢視中的「更多動作」功能，對資料集執行其他任務。您可以刪除資料集或將其啟用，以便與所選資料集詳細資料頁面上的即時客戶輪廓搭配使用。<br>**備註：**&#x200B;如果您啟用資料集進行輪廓攝取，則該資料集的結構描述必須與即時客戶輪廓相容。<br>![資料集工作區，特別標示出「[!UICONTROL ...更多]」下拉式選單。](../2024/assets/march/more-actions.png "資料集工作區，特別標示出「...更多」下拉式選單。"){width="100" zoomable="yes"}。<br>請閱讀[資料集使用手冊](../../catalog/datasets/user-guide.md)文件以了解其他資訊。 |

{style="table-layout:auto"}

如需有關目錄服務的詳細資訊，請參閱[目錄服務概觀](../../catalog/home.md)。

## 資料準備 {#data-prep}

「資料準備」讓資料工程師可在體驗資料模式 (XDM) 之間對應、轉換和驗證資料。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| Adobe Analytics 的新對應工具函數 | 您現在可以使用以下函數，從 Adobe Analytics 擷取事件資料： <ul><li>`aa_get_event_id`</li><li>`aa_get_event_value`</li><li>`aa_get_product_categories`</li><li>`aa_get_product_names`</li><li>`aa_get_product_quantities`</li><li>`aa_get_product_prices`</li><li>`aa_get_product_event_values`</li><li>`aa_get_product_evars`</li></ul> 如需有關這些函數的詳細資訊，請參閱[資料準備函數指南](../../data-prep/functions.md#analytics-functions)。 |

{style="table-layout:auto"}

如需有關資料準備的詳細資訊，請閱讀[資料準備概觀](../../data-prep/home.md)。

## 資料彙集 {#data-collection}

Adobe Experience Platform 提供了一套技術，讓您可收集用戶端客戶體驗資料並將其傳送到 Adobe Experience Platform Edge Network，在其中可擴充、轉換資料並將其分送至 Adobe 或非 Adobe 目標。

**新功能**

| 類型 | 功能 | 說明 |
| --- | --- | --- |
| 擴充功能 | [!DNL Merkury] 標記擴充功能 | [[!DNL Merkury] 標記擴充功能](https://exchange.adobe.com/apps/ec/600027/merkury-tag)為 [!DNL Merkury] ID 提供領先業界的匿名網站訪客比對率。品牌可以善用 [!DNL Merkury] 標記和 Adobe 的功能來提供即時的個人化網站體驗。此外，[!DNL Merkury] 標記還可促進第一方數位資料以及連線之線上和離線客戶輪廓的成長。 |

{style="table-layout:auto"}

若要深入了解資料彙集，請閱讀[資料彙集概觀](../../tags/home.md)。

## 目標 {#destinations}

[!DNL Destinations] 是與目標平台的預先建立整合，能夠順暢啟用來自 Adobe Experience Platform 的資料。您可使用目標啟用已知和未知的資料，以進行跨通路行銷活動、電子郵件行銷活動、設定目標的廣告活動和其他諸多使用案例。

**新目標和更新的目標** {#new-updated-destinations}

| 目標 | 類型 | 說明 |
| ----------- | --------- | ----------- |
| [(Beta) Acxiom Data Enhancement 連線](../../destinations/catalog/data-partner/acxiom-data-enhancement.md) | 新增 | 使用此連接器可啟用自 Real-Time CDP 到 Acxiom 的第一方輪廓，以便擴充資料並在行銷管道中使用。然後，您可以使用 Acxiom 來源匯入含有增強資料的輪廓，並在 Real-Time CDP 中使用它們。 |
| [(Beta) Acxiom 潛在客戶禁止連線](../../destinations/catalog/data-partner/acxiom-prospect-suppression.md) | 新增 | 將您的第一方客群匯出到 Acxiom 目標，即可允許 Acxiom 禁止已知或已轉換的客戶。接著，使用 [Acxiom 潛在客戶資料匯入](../../sources/connectors/data-partners/acxiom-prospecting-data-import.md)來源連接器，即可從 Acxiom 攝取並啟用潛在客戶清單，並移除已知或已轉換的客戶。 |
| [Amazon Ads 連線](../../destinations/catalog/advertising/amazon-ads.md) | 更新 | 匯出資料至 Amazon Ads 目標時，您現在可以將資料路由至 Amazon DSP 或 Amazon Marketing Cloud (新功能)。 |
| [LiveRamp 上線連線](../../destinations/catalog/advertising/liveramp-onboarding.md) | 更新 | LiveRamp 上線目標現在可支援對歐洲和澳洲的 [!DNL LiveRamp] [!DNL SFTP] 執行個體傳遞內容。匯出檔案的上限大小也提升至 1000 萬列 (先前為 500 萬列)。 |

{style="table-layout:auto"}

<!--

**New or updated functionality** {#destinations-new-updated-functionality}

-->

如需有關目標的詳細一般資訊，請參閱[目標概觀](../../destinations/home.md)。

## 體驗資料模式 (XDM) {#xdm}

XDM 是一種開放原始碼的規格，可為帶到 Adobe Experience Platform 中的資料提供通用結構和定義 (結構描述)。若遵守 XDM 標準，即可將所有客戶體驗資料合併到一個常用表述中，以更快速、更整合的方式傳遞分析。您可以從客戶行為中獲得有價值的分析，透過區段定義客戶客群，並使用客戶屬性實現個人化的目的。

**新功能**

| 功能 | 說明 |
| --- | --- |
| Experience Platform 使用者介面對應資料類型支援 | 在Experience Platform UI中定義對應欄位，進一步自訂Experience Data Model (XDM)資料結構。 現在起，您可以在結構描述編輯器中建立對應欄位，以建置靈活資料結構的模型或有效率地儲存金鑰/值配對。定義新欄位時，請從「類型」下拉式選單中選取「對應」，以設定子欄位並將其指派至欄位群組中。可支援的對應值類型為字串和整數。<br>![結構描述編輯器，特別標示出「類型」和「對應值類型」欄位。](../2024/assets/march/maps.png "結構描述編輯器，特別標示出「類型」和「對應值類型」欄位。"){width="100" zoomable="yes"}<br>若要了解如何[在使用者介面中定義對應欄位](../../xdm/ui/fields/map.md)，請參閱使用者介面指南。 |

{style="table-layout:auto"}

如需Experience Platform中XDM的詳細資訊，請參閱[XDM系統總覽](../../xdm/home.md)。

## Segmentation Service {#segmentation}

[!DNL Segmentation Service] 可讓您將儲存在和個人 (例如客戶、潛在客戶、使用者或組織) 相關的 [!DNL Experience Platform] 中的資料分段為不同的客群。您可以透過區段定義或來自 [!DNL Real-Time Customer Profile] 資料的其他來源建立客群。這些客群會在 [!DNL Experience Platform] 上集中設定及維護，並可透過任何 Adobe 解決方案輕鬆存取。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 大量動作 | 客群庫存現在可以支援大量動作。透過大量動作功能，您可以快速選取多個客群以將其移至資料夾、套用標記、套用存取標籤，或將其刪除。<br> ![在客群使用者介面工作區中執行大量動作的畫面。](../2024/assets/march/bulk-actions.png "在客群使用者介面工作區中執行大量動作的畫面。"){width="100" zoomable="yes"} <br>如需有關此功能的詳細資訊，請閱讀 [Audience Portal 概觀](../../segmentation/ui/audience-portal.md#bulk-actions)。 |

{style="table-layout:auto"}

若要深入了解 Segmentation Service，請閱讀 [Segmentation Service 概觀](../../segmentation/home.md)。

## 來源 {#sources}

Experience Platform 可提供 RESTful API 和互動式 UI，可讓您輕鬆為各種資料提供者設定來源連線。這些來源連線可讓您進行驗證並連線到外部儲存系統和 CRM 服務、設定攝取執行的時間並管理資料攝取輸送量。

**新來源和更新的來源**

| 功能 | 類型 | 說明 |
| --- | --- | --- |
| [!BADGE Beta]{type=Informative} [!DNL Acxiom Data Ingestion] | 新增 | 使用 [[!DNL Acxiom Data Ingestion] 來源](../../sources/tutorials/ui/create/data-partners/acxiom-data-ingestion.md)可將 [!DNL Acxiom] 資料攝取至 Real-Time Customer Data Platform，並擴充第一方輪廓。然後，您可以使用 [!DNL Acxiom] 已擴充的第一方輪廓，以提升客群並在行銷管道中啟用。<br> ![Acxiom 資料攝取來源。](../2024/assets/march/acxiom-data-ingestion.png "新的 Acxiom 資料攝取來源。"){width="100" zoomable="yes"} <br>請閱讀 [[!DNL Acxiom Data Ingestion] 概觀](../../sources/connectors/data-partners/acxiom-data-ingestion.md)以了解有關如何開始使用的資訊。 |
| [!BADGE Beta]{type=Informative} [!DNL Stripe] | 新增 | 使用 [[!DNL Stripe] 來源](../../sources/connectors/payments/stripe.md)可將客戶在購買流程中擷取的資料攝取至 Experience Platform 中。攝取完成後，您就可以利用這些資料來建立個人化產品建議，並解鎖更豐富的業務深入解析。<br> ![Stripe 來源。](../2024/assets/march/stripe.png "新的 Stripe 來源。"){width="100" zoomable="yes"} <br>請閱讀 [[!DNL Stripe] 概觀](../../sources/connectors/payments/stripe.md)以了解有關如何開始使用的資訊。 |
| [!DNL Snowflake Streaming] 的使用者介面支援 | 新增 | 現在起，您可以利用 Experience Platform 使用者介面中的 [[!DNL Snowflake Streaming] 來源](../../sources/tutorials/ui/create/databases/snowflake-streaming.md)，從 [!DNL Snowflake] 資料庫串流資料。<br> ![Snowflake 串流來源。](../2024/assets/march/snowflake-streaming.png "新的 Snowflake 串流來源。"){width="100" zoomable="yes"} <br>請閱讀 [[!DNL Snowflake Streaming] 概觀](../../sources/connectors/databases/snowflake-streaming.md)以了解有關如何開始使用的資訊。 |

{style="table-layout:auto"}

如需有關來源的詳細資訊，請閱讀[來源概觀](../../sources/home.md)。
