---
title: Adobe Experience Platform 發行說明 (2022 年 10 月)
description: Adobe Experience Platform 2022 年 10 月版發行說明。
exl-id: 61ef2472-5e79-433f-9f60-b1245f619b42
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1140'
ht-degree: 33%

---

# Adobe Experience Platform 發行說明

**發行日期： 2022年10月26日**

- [客戶自控金鑰](#cmk)
- [資料彙集](#data-collection)
- [目標](#destinations)
- [體驗資料模式](#xdm)
- [查詢服務](#query-service)

## 客戶自控金鑰 {#cmk}

所有儲存在Adobe Experience Platform的資料都會使用系統層級的金鑰進行靜態加密。 如果您使用以Experience Platform為基礎建立的應用程式，現在可以選擇改用您自己的加密金鑰，讓您更能掌控資料安全性。

如需功能的詳細資訊，請參閱[客戶管理的金鑰](../../landing/governance-privacy-security/customer-managed-keys/overview.md)的概觀。

## 資料彙集 {#data-collection}

Adobe Experience Platform 提供了一套技術，讓您可收集用戶端客戶體驗資料並將其傳送到 Adobe Experience Platform Edge Network，在其中可擴充、轉換資料並將其分送至 Adobe 或非 Adobe 目標。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 資料串流的敏感資料處理 | 資料串流現在會運用數種Experience Platform技術，適當處理由健康保險便利與責任法案(HIPAA)等法規強制執行的敏感資料。 請參閱有關[處理資料流中的敏感資料](../../datastreams/overview.md#sensitive)部份，了解更多資訊。 |
| 用於事件轉送的[!DNL Splunk]延伸模組 | 您現在可以使用[事件轉送](../../tags/ui/event-forwarding/overview.md)延伸功能傳送資料給[!DNL Splunk]。 如需詳細資訊，請參閱[[!DNL Splunk] 擴充功能概觀](../../tags/extensions/server/splunk/overview.md)。 |
| 用於事件轉送的[!DNL Zendesk]延伸模組 | 您現在可以使用[事件轉送](../../tags/ui/event-forwarding/overview.md)延伸功能傳送資料給[!DNL Zendesk]。 如需詳細資訊，請參閱[[!DNL Zendesk] 擴充功能概觀](../../tags/extensions/server/zendesk/overview.md)。 |

{style="table-layout:auto"}

## [!DNL Destinations] {#destinations}

[!DNL Destinations] 是與目標平台的預先建立整合，能夠順暢啟用來自 Adobe Experience Platform 的資料。您可以使用目標啟用已知和未知的資料，以進行跨通路行銷活動、電子郵件行銷活動、定向廣告和其他諸多使用案例。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| (Beta)資料集匯出 | [資料集匯出Beta功能](/help/destinations/ui/export-datasets.md)可讓您透過目標使用者介面，將第一代資料(如[Real-Time Customer Data Platform產品說明](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)中的定義)從Adobe Experience Platform匯出至您自己的外部客戶系統。 這可讓您使用無程式碼/低程式碼工作流程，將資料從Experience Platform取出至六個雲端儲存空間目的地（如下表所列），以用於分析和法規遵循使用案例。 |
| (Beta)增強的檔案匯出功能 | 現在，從Experience Platform匯出檔案時，您可以受益於增強的自訂功能： <br><ul><li>其他[檔案命名選項](/help/destinations/ui/activate-batch-profile-destinations.md#file-names)。</li><li>能夠透過[改善的對應步驟](/help/destinations/ui/activate-batch-profile-destinations.md#mapping)，在您匯出的檔案內設定自訂檔案標頭。</li><li>[能夠自訂轉存的CSV資料檔案的格式](/help/destinations/ui/batch-destinations-file-formatting-options.md)。</li></ul> <br>下表列出的六個新Beta版雲端儲存空間卡支援此功能。 |

{style="table-layout:auto"}

**新目標或更新的目標** {#new-or-updated-destinations}

| 目標 | 說明 |
| ----------- | ----------- |
| [[!DNL Line]](../../destinations/catalog/mobile-engagement/line.md) | Line是連線人員、服務和資訊的常用通訊平台，已從聊天應用程式成長為娛樂、社交和日常活動的中樞。 |
| [[!DNL Microsoft Dynamics 365]](../../destinations/catalog/crm/microsoft-dynamics-365.md) | Microsoft Dynamics 365是以雲端為基礎的業務應用程式平台，結合企業資源規劃(ERP)、客戶關係管理(CRM)以及生產力應用程式和AI工具，讓端對端的作業更順暢、控制更嚴格、增長潛力更大、成本更低。 |
| [[!DNL (Beta) Adobe Commerce]](../../destinations/catalog/personalization/adobe-commerce.md) | [!DNL (Beta) Adobe Commerce]目的地聯結器可讓您選取一或多個Real-Time CDP區段，以啟用至您的[!DNL Adobe Commerce]帳戶，為購物者提供動態的個人化體驗。 在[!DNL Adobe Commerce]內，您可以接著選取這些Real-Time CDP區段，以個人化購物車中的獨特優惠，例如「購買2 get 1免費」。 您也可以顯示主圖橫幅，並透過促銷優惠修改產品定價，所有優惠都根據Adobe Real-Time CDP區段自訂。 |
| [[!DNL (Beta) Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md) | 建立與 [!DNL Azure Data Lake Storage Gen2] 的即時輸出連線，定期將資料檔案從 Adobe Experience Platform 匯出至您自己的儲存位置。這個新的測試版目的地提供增強的檔案匯出功能，並支援資料集匯出。 |
| [[!DNL (Beta) Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md) | [!DNL Data Landing Zone]是Adobe Experience Platform布建的[!DNL Azure Blob]儲存體介面，可授予您安全、雲端式的檔案儲存機制存取權，以將檔案匯出Experience Platform。 這個新的測試版目的地提供增強的檔案匯出功能，並支援資料集匯出。 |
| [[!DNL (Beta) Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md) | 建立與 [!DNL Google Cloud Storage] 的即時輸出連線，定期將資料檔案從 Adobe Experience Platform 匯出至您自己的貯體。這個新的測試版目的地提供增強的檔案匯出功能，並支援資料集匯出。 |
| [[!DNL (Beta) Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md#changelog) | Beta參與者現在會在目的地目錄中並排看到兩張[!DNL Amazon S3]目的地卡片。 新的測試版目的地提供增強型檔案匯出功能，並支援資料集匯出。 |
| [[!DNL (Beta) Azure Blob]](../../destinations/catalog/cloud-storage/azure-blob.md#changelog) | Beta參與者現在會在目的地目錄中並排看到兩張[!DNL Azure Blob]目的地卡片。 新的測試版目的地提供增強型檔案匯出功能，並支援資料集匯出。 |
| [[!DNL (Beta) SFTP]](../../destinations/catalog/cloud-storage/sftp.md#changelog) | Beta參與者現在會在目的地目錄中並排看到兩張[!DNL SFTP]目的地卡片。 新的測試版目的地提供增強型檔案匯出功能，並支援資料集匯出。 |

{style="table-layout:auto"}

**新文件或更新的文件**

| 文件 | 說明 |
| ----------- | ----------- |
| [目的地護欄](../../destinations/guardrails.md) | 此頁面提供啟動行為的預設使用量和速率限制。 |

如需有關目標的詳細一般資訊，請參閱[目標概觀](../../destinations/home.md)。

## 體驗資料模式 (XDM) {#xdm}

XDM 是一種開放原始碼的規格，可為帶到 Adobe Experience Platform 中的資料提供通用結構和定義 (結構描述)。若遵守 XDM 標準，即可將所有客戶體驗資料合併到一個常用表述中，以更快速、更整合的方式傳遞分析。您可以從客戶行為中獲得有價值的分析，透過區段定義客戶客群，並使用客戶屬性實現個人化的目的。

**已更新的 XDM 元件**

| 元件類型 | 名稱 | 說明 |
| --- | --- | --- |
| 資料類型 | [[!UICONTROL 工作階段細節資訊]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | 將`authorized`欄位從布林值型別更新為字串。 `season`和`episode`已從整數變更為字串。 |
| 資料類型 | [[!UICONTROL 廣告細節資訊]](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingdetails.schema.json) | `name`已重新命名為`friendlyName`，`ID`已重新命名為`name`。 |
| 資料類型 | [[!UICONTROL 錯誤細節資訊]](https://github.com/adobe/xdm/blob/master/components/datatypes/errordetails.schema.json) | `ID`已重新命名為`name`。 |

{style="table-layout:auto"}

如需Experience Platform中XDM的詳細資訊，請參閱[XDM系統總覽](../../xdm/home.md)。

## 查詢服務 {#query-service}

查詢服務可讓您使用標準的 SQL 查詢 Adobe Experience Platform 中的資料[!DNL Data Lake]。您可以加入 [!DNL Data Lake] 中的任何資料集，並將查詢結果擷取為新資料集，以用於報告、資料科學工作區，或攝取至即時客戶輪廓中。

**更新的功能**

| 功能 | 說明 |
| --- | --- |
| 透過Experience Platform UI監視查詢 | 查詢服務[!UICONTROL 排定的查詢]索引標籤透過UI提供所有查詢工作狀態的可見度改善。 您現在可以從[!UICONTROL 排定的查詢]索引標籤找到有關查詢執行狀態的重要資訊，包括失敗時的錯誤訊息和程式碼。 您也可以透過UI針對這些查詢根據其狀態訂閱警報。 請參閱[監視器查詢檔案](../../query-service/ui/monitor-queries.md)以深入瞭解此功能。 |
| 查詢加速報告見解資料模型 | 作為Data Distiller SKU的一部分，查詢加速存放區可讓您減少從資料獲得重要深入分析所需的時間和處理能力。 透過查詢加速存放區，您可以建立自訂資料模型和/或擴充現有的Adobe Real-Time Customer Data Platform資料模型，以改進您的報告見解及其視覺效果。 請參閱[query accelerated store reporting insights檔案](../../query-service/data-distiller/sql-insights/reporting-insights-data-model.md)以進一步瞭解此功能。 |

{style="table-layout:auto"}

如需查詢服務的詳細資訊，請參閱[查詢服務總覽](../../query-service/home.md)。
Adobe Experience Platform 的新功能：

