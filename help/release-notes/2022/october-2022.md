---
title: Adobe Experience Platform發行說明2022年10月
description: Adobe Experience Platform 2022年10月版本注意事項。
exl-id: 61ef2472-5e79-433f-9f60-b1245f619b42
source-git-commit: e1deeadb98240f885e9dc95ecbc58ae48049a190
workflow-type: tm+mt
source-wordcount: '1159'
ht-degree: 26%

---

# Adobe Experience Platform 發行說明

**發行日期：2022 年 10 月 26 日**

- [客戶自控金鑰](#cmk)
- [資料集合](#data-collection)
- [目的地](#destinations)
- [體驗資料模式](#xdm)
- [查詢服務](#query-service)

## 客戶自控金鑰 {#cmk}

所有儲存在Adobe Experience Platform的資料都會使用系統層級的金鑰進行靜態加密。 如果您使用以Platform為基礎建立的應用程式，現在可以選擇改用您自己的加密金鑰，讓您更能掌控資料安全性。

請參閱以下主題的概觀： [客戶自控金鑰](../../landing/governance-privacy-security/customer-managed-keys.md) 以取得功能的詳細資訊。

## 資料集合 {#data-collection}

Adobe Experience Platform 提供了一套技術，讓您可收集用戶端客戶體驗資料並將其傳送到 Adob&#x200B;&#x200B;e Experience Platform Edge Network，在其中可擴充、轉換資料並將其分送至 Adob&#x200B;&#x200B;e 或非 Adob&#x200B;&#x200B;e 目的地。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 資料串流的敏感資料處理 | 資料串流現在運用數種平台技術，可適當處理由健康保險便利與責任法案(HIPAA)等法規強制執行的敏感資料。 請參閱以下小節： [處理資料串流中的敏感性資料](../../datastreams/overview.md#sensitive) 以取得詳細資訊。 |
| [!DNL Splunk] 事件轉送的擴充功能 | 您現在可以將資料傳送至 [!DNL Splunk] 使用 [事件轉送](../../tags/ui/event-forwarding/overview.md) 副檔名。 請參閱 [[!DNL Splunk] 擴充功能概觀](../../tags/extensions/server/splunk/overview.md) 以取得詳細資訊。 |
| [!DNL Zendesk] 事件轉送的擴充功能 | 您現在可以將資料傳送至 [!DNL Zendesk] 使用 [事件轉送](../../tags/ui/event-forwarding/overview.md) 副檔名。 請參閱 [[!DNL Zendesk] 擴充功能概觀](../../tags/extensions/server/zendesk/overview.md) 以取得詳細資訊。 |

{style="table-layout:auto"}

## [!DNL Destinations] {#destinations}

[!DNL Destinations] 是預先建立的和目標平台的整合，可讓來自 Adob&#x200B;&#x200B;e Experience Platform 的資料順暢啟動。您可使用目的地啟用已知和未知的資料，以進行跨通路行銷活動、電子郵件行銷活動、設定目標的廣告活動和其他諸多使用案例。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| (Beta)資料集匯出 | 此 [資料集匯出Beta版功能](/help/destinations/ui/export-datasets.md) 可讓您匯出第一代資料(如 [Real-time Customer Data Platform產品說明](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html))經由目標使用者介面，從Adobe Experience Platform前往您自己的外部客戶系統。 這可讓您利用無程式碼/低程式碼工作流程，將資料從Experience Platform中帶到6個雲端儲存目標（如下表所列），以用於分析和法規遵循使用案例。 |
| (Beta)增強的檔案匯出功能 | 現在，將檔案匯出出Experience Platform時，您可以受益於增強的自訂功能： <br><ul><li>其他 [檔案命名選項](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).</li><li>可透過以下方式設定匯出檔案中的自訂檔案標題： [改善對應步驟](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).</li><li>[能夠自訂匯出的CSV資料檔案的格式](/help/destinations/ui/batch-destinations-file-formatting-options.md).</li></ul> <br> 下表列出的六個新Beta版雲端儲存空間卡支援此功能。 |

{style="table-layout:auto"}

**新目的地或更新的目的地** {#new-or-updated-destinations}

| 目的地 | 說明 |
| ----------- | ----------- |
| [[!DNL Line]](../../destinations/catalog/mobile-engagement/line.md) | Line是連線人員、服務和資訊的常用通訊平台，已從聊天應用程式成長為娛樂、社交和日常活動的中樞。 |
| [[!DNL Microsoft Dynamics 365]](../../destinations/catalog/crm/microsoft-dynamics-365.md) | Microsoft Dynamics 365是以雲端為基礎的業務應用程式平台，結合企業資源規劃(ERP)、客戶關係管理(CRM)以及生產力應用程式和AI工具，以實現端對端更順暢、控制更嚴的作業、更佳的增長潛力以及更低的成本。 |
| [[!DNL (Beta) Adobe Commerce]](../../destinations/catalog/personalization/adobe-commerce.md) | 此 [!DNL (Beta) Adobe Commerce] 目的地聯結器可讓您選取一或多個Real-Time CDP區段，以啟用至 [!DNL Adobe Commerce] 帳戶，為購物者提供動態的個人化體驗。 範圍 [!DNL Adobe Commerce]，接著您可以選取這些Real-Time CDP區段，以個人化購物車中的獨特優惠方案，例如「購買2 get 1 free」。 您也可以顯示主圖橫幅，並透過促銷優惠修改產品定價，所有優惠都根據Adobe Real-Time CDP區段自訂。 |
| [[!DNL (Beta) Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md) | 建立與的即時輸出連線 [!DNL Azure Data Lake Storage Gen2] 以定期從Adobe Experience Platform將資料檔案匯出至您自己的儲存位置。 這個新的測試版目的地提供增強的檔案匯出功能，並支援資料集匯出。 |
| [[!DNL (Beta) Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md) | [!DNL Data Landing Zone] 是 [!DNL Azure Blob] 由Adobe Experience Platform布建的儲存體介面，可讓您存取安全的雲端型檔案儲存設施，以將檔案匯出至Platform。 這個新的測試版目的地提供增強的檔案匯出功能，並支援資料集匯出。 |
| [[!DNL (Beta) Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md) | 建立與的即時輸出連線 [!DNL Google Cloud Storage] 以定期從Adobe Experience Platform將資料檔案匯出至您自己的貯體。 這個新的測試版目的地提供增強的檔案匯出功能，並支援資料集匯出。 |
| [[!DNL (Beta) Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md#changelog) | Beta版參與者現在看到兩個 [!DNL Amazon S3] 目的地卡片在目的地目錄中並排顯示。 新的測試版目的地提供增強型檔案匯出功能，並支援資料集匯出。 |
| [[!DNL (Beta) Azure Blob]](../../destinations/catalog/cloud-storage/azure-blob.md#changelog) | Beta版參與者現在看到兩個 [!DNL Azure Blob] 目的地卡片在目的地目錄中並排顯示。 新的測試版目的地提供增強型檔案匯出功能，並支援資料集匯出。 |
| [[!DNL (Beta) SFTP]](../../destinations/catalog/cloud-storage/sftp.md#changelog) | Beta版參與者現在看到兩個 [!DNL SFTP] 目的地卡片在目的地目錄中並排顯示。 新的測試版目的地提供增強型檔案匯出功能，並支援資料集匯出。 |

{style="table-layout:auto"}

**新文件或更新的文件**

| 文件 | 說明 |
| ----------- | ----------- |
| [目的地護欄](../../destinations/guardrails.md) | 此頁面提供啟動行為的預設使用量和速率限制。 |

如需有關目的地的詳細一般資訊，請參閱[目的地概觀](../../destinations/home.md)。

## 體驗資料模式 (XDM) {#xdm}

XDM 是一種開放原始碼的規格，可為帶到 Adob&#x200B;&#x200B;e Experience Platform 中的資料提供通用結構和定義 (綱要)。若遵守 XDM 標準，即可將所有客戶體驗資料合併到一個常用表述中，以更快速、更整合的方式傳遞分析。您可以從客戶行為中獲得有價值的分析，透過區段定義客戶對象，並使用客戶屬性實現個人化的目的。

**已更新的 XDM 元件**

| 元件類型 | 名稱 | 說明 |
| --- | --- | --- |
| 資料類型 | [[!UICONTROL 工作階段細節資訊]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | 已更新 `authorized` 欄位從布林值型別轉換為字串。 `season` 和 `episode` 已由整數變更為字串。 |
| 資料類型 | [[!UICONTROL 廣告細節資訊]](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingdetails.schema.json) | `name` 已重新命名為 `friendlyName`、和 `ID` 已重新命名為 `name`. |
| 資料類型 | [[!UICONTROL 錯誤細節資訊]](https://github.com/adobe/xdm/blob/master/components/datatypes/errordetails.schema.json) | `ID` 已重新命名為 `name`。 |

{style="table-layout:auto"}

如需有關 Platform 中 XDM 的詳細資訊，請參閱 [XDM 系統概觀](../../xdm/home.md)。

## 查詢服務 {#query-service}

查詢服務可讓您使用標準的 SQL 查詢 Adob&#x200B;&#x200B;e Experience Platform 中的資料[!DNL Data Lake]。您可以從以下位置加入任何資料集： [!DNL Data Lake] 並將查詢結果擷取為新資料集，以用於報表、資料科學工作區或內嵌到即時客戶個人檔案中。

**更新的功能**

| 功能 | 說明 |
| --- | --- |
| 透過Platform UI監視查詢 | 查詢服務 [!UICONTROL 排定的查詢] 索引標籤透過UI提供所有查詢作業狀態的可見性改進。 您現在可以找到有關查詢執行狀態的重要資訊，包括失敗時的錯誤訊息和代碼，來自 [!UICONTROL 排定的查詢] 標籤。 您也可以透過UI針對這些查詢根據其狀態訂閱警報。 請參閱 [監視查詢檔案](../../query-service/ui/monitor-queries.md) 以進一步瞭解此功能。 |
| 查詢加速報告見解資料模型 | 作為Data Distiller SKU的一部分，查詢加速存放區可讓您減少從資料獲得重要深入分析所需的時間和處理能力。 透過查詢加速存放區，您可以建立自訂資料模型和/或擴充現有的Adobe Real-time Customer Data Platform資料模型，以改進您的報告見解及其視覺效果。 請參閱 [查詢加速商店報告見解檔案](../../query-service/data-distiller/query-accelerated-store/reporting-insights-data-model.md) 以進一步瞭解此功能。 |

{style="table-layout:auto"}

如需有關查詢服務的詳細資訊，請參閱[查詢服務概觀](../../query-service/home.md)。Adobe Experience Platform中的新功能：

