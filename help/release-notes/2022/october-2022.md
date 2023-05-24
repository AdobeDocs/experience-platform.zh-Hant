---
title: Adobe Experience Platform發行說明2022年10月
description: 2022年10月為Adobe Experience Platform發佈的說明。
exl-id: 61ef2472-5e79-433f-9f60-b1245f619b42
source-git-commit: 8bbac729324ad5bd701f8609c443092ddb045b96
workflow-type: tm+mt
source-wordcount: '1328'
ht-degree: 2%

---

# Adobe Experience Platform 發行說明

**發行日期：2022 年 10 月 26 日**

- [客戶管理的密鑰](#cmk)
- [資料收集](#data-collection)
- [目的地](#destinations)
- [體驗資料模型](#xdm)
- [查詢服務](#query-service)
- [來源](#sources-sources)

## 客戶管理的密鑰 {#cmk}

所有儲存在Adobe Experience Platform的資料都使用系統級密鑰在靜態下進行加密。 如果您使用的是構建在平台之上的應用程式，則現在可以選擇使用您自己的加密密鑰，從而讓您能夠更好地控制資料安全。

請參閱 [客戶管理密鑰](../../landing/governance-privacy-security/customer-managed-keys.md) 的上界。

## 資料收集 {#data-collection}

Adobe Experience Platform公司提供了一套技術，使您能夠收集客戶端客戶體驗資料並將其發送到Adobe Experience Platform邊緣網路，在該網路中，資料可以得到豐富、轉換並分發到Adobe或非Adobe目的地。

**新增或更新的功能**

| 功能 | 說明 |
| --- | --- |
| 資料流的敏感資料處理 | Datastreams現在利用多種平台技術來適當地處理由健康保險流通和責任法案(HIPAA)等法規強制實施的敏感資料。 請參閱 [處理資料流中的敏感資料](../../edge/datastreams/overview.md#sensitive) 的子菜單。 |
| [!DNL Splunk] 事件轉發擴展 | 您現在可以將資料發送到 [!DNL Splunk] 使用 [事件轉發](../../tags/ui/event-forwarding/overview.md) 擴展。 查看 [[!DNL Splunk] 擴展概述](../../tags/extensions/server/splunk/overview.md) 的子菜單。 |
| [!DNL Zendesk] 事件轉發擴展 | 您現在可以將資料發送到 [!DNL Zendesk] 使用 [事件轉發](../../tags/ui/event-forwarding/overview.md) 擴展。 查看 [[!DNL Zendesk] 擴展概述](../../tags/extensions/server/zendesk/overview.md) 的子菜單。 |

{style="table-layout:auto"}

## [!DNL Destinations] {#destinations}

[!DNL Destinations] 是預先構建的與目標平台的整合，允許無縫激活來自Adobe Experience Platform的資料。 您可以使用目標來激活跨渠道市場營銷活動、電子郵件活動、目標廣告和許多其他使用案例的已知和未知資料。

**新增或更新的功能**

| 功能 | 說明 |
| --- | --- |
| (Beta)資料集導出 | 的 [資料集導出Beta功能](/help/destinations/ui/export-datasets.md) 允許您導出第一代資料(如 [Real-time Customer Data Platform產品說明](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html))通過目標用戶介面從Adobe Experience Platform輸出到您自己的外部客戶系統。 這使您能夠通過無代碼/低代碼工作流將資料從Experience Platform中移出到六個雲儲存目標（在下表中列出），以用於分析和合規性使用案例。 |
| （測試版）增強的檔案導出功能 | 現在，在導出檔案時，您可以從增強的自定義功能中獲益： <br><ul><li>其他 [檔案命名選項](/help/destinations/ui/activate-batch-profile-destinations.md#file-names)。</li><li>通過 [改進映射步長](/help/destinations/ui/activate-batch-profile-destinations.md#mapping)。</li><li>[能夠自定義導出的CSV資料檔案的格式](/help/destinations/ui/batch-destinations-file-formatting-options.md)。</li></ul> <br> 下表列出的六個新的測試版雲儲存卡支援此功能。 |

{style="table-layout:auto"}

**新建或更新的目標** {#new-or-updated-destinations}

| 目的地 | 說明 |
| ----------- | ----------- |
| [[!DNL Line]](../../destinations/catalog/mobile-engagement/line.md) | 連我是一個熱門的溝通平台，將人、服務和資訊連接起來，並從聊天應用發展成為娛樂、社交和日常活動的中心。 |
| [[!DNL Microsoft Dynamics 365]](../../destinations/catalog/crm/microsoft-dynamics-365.md) | MicrosoftDynamics 365是一個基於雲的業務應用平台，它將企業資源規劃(ERP)和客戶關係管理(CRM)與生產力應用程式和AI工具相結合，使端到端的運營更加平穩和可控，增長潛力更大，成本更低。 |
| [[!DNL (Beta) Adobe Commerce]](../../destinations/catalog/personalization/adobe-commerce.md) | 的 [!DNL (Beta) Adobe Commerce] 目標連接器用於選擇一個或多個Real-Time CDP段以激活到 [!DNL Adobe Commerce] 為購物者提供動態個性化體驗。 在 [!DNL Adobe Commerce]，然後您可以選擇這些Real-Time CDP細分市場，以個性化購物車中的獨特優惠，如「購買2獲得1免費」。 您還可以顯示英雄橫幅，並通過促銷優惠修改產品定價，所有這些優惠都是針對Adobe Real-Time CDP市場進行定製的。 |
| [[!DNL (Beta) Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md) | 建立即時出站連接到 [!DNL Azure Data Lake Storage Gen2] 定期將資料檔案從Adobe Experience Platform導出到您自己的儲存位置。 此新的測試目標提供了增強的檔案導出功能，並支援資料集導出。 |
| [[!DNL (Beta) Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md) | [!DNL Data Landing Zone] 是 [!DNL Azure Blob] 由Adobe Experience Platform提供的儲存介面，允許您訪問安全、基於雲的檔案儲存設施，以將檔案導出到平台。 此新的測試目標提供了增強的檔案導出功能，並支援資料集導出。 |
| [[!DNL (Beta) Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md) | 建立即時出站連接到 [!DNL Google Cloud Storage] 定期將資料檔案從Adobe Experience Platform導出到您自己的儲存桶中。 此新的測試目標提供了增強的檔案導出功能，並支援資料集導出。 |
| [[!DNL (Beta) Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md#changelog) | Beta參與者現在看到兩個 [!DNL Amazon S3] 目標卡在目標目錄中並排。 新的測試目標提供了增強的檔案導出功能，並支援資料集導出。 |
| [[!DNL (Beta) Azure Blob]](../../destinations/catalog/cloud-storage/azure-blob.md#changelog) | Beta參與者現在看到兩個 [!DNL Azure Blob] 目標卡在目標目錄中並排。 新的測試目標提供了增強的檔案導出功能，並支援資料集導出。 |
| [[!DNL (Beta) SFTP]](../../destinations/catalog/cloud-storage/sftp.md#changelog) | Beta參與者現在看到兩個 [!DNL SFTP] 目標卡在目標目錄中並排。 新的測試目標提供了增強的檔案導出功能，並支援資料集導出。 |

{style="table-layout:auto"}

**新建或更新的文檔**

| 文件 | 說明 |
| ----------- | ----------- |
| [目標護欄](../../destinations/guardrails.md) | 此頁提供有關激活行為的預設使用和速率限制。 |

有關目標的更多一般資訊，請參閱 [目標概述](../../destinations/home.md)。

## 體驗資料模型(XDM) {#xdm}

XDM是一種開源規範，它為傳入Adobe Experience Platform的資料提供通用結構和定義（架構）。 通過遵守XDM標準，所有客戶體驗資料都可以納入到共同的表示形式中，以更快、更整合的方式提供見解。 您可以從客戶操作中獲得有價值的見解，通過細分市場定義客戶受眾，並將客戶屬性用於個性化目的。

**更新的XDM元件**

| 元件類型 | 名稱 | 說明 |
| --- | --- | --- |
| 資料類型 | [[!UICONTROL 會話詳細資訊資訊]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | 已更新 `authorized` 欄位，從布爾類型到字串。 `season` 和 `episode` 已從整數更改為字串。 |
| 資料類型 | [[!UICONTROL 廣告詳細資訊資訊]](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingdetails.schema.json) | `name` 已更名為 `friendlyName`, `ID` 已更名為 `name`。 |
| 資料類型 | [[!UICONTROL 錯誤詳細資訊]](https://github.com/adobe/xdm/blob/master/components/datatypes/errordetails.schema.json) | `ID` 已重新命名為 `name`。 |

{style="table-layout:auto"}

有關平台中XDM的詳細資訊，請參見 [XDM系統概述](../../xdm/home.md)。

## 查詢服務 {#query-service}

查詢服務允許您使用標準SQL查詢Adobe Experience Platform的資料 [!DNL Data Lake]。 您可以加入來自 [!DNL Data Lake] 並將查詢結果捕獲為新資料集，用於報告、Data Science Workspace或用於接收到即時客戶配置檔案。

**已更新功能**

| 功能 | 說明 |
| --- | --- |
| 通過平台UI監視查詢 | 查詢服務 [!UICONTROL 計畫查詢] 頁籤通過UI提供了所有查詢作業狀態的更高可見性。 現在，您可以找到有關查詢運行狀態的重要資訊，包括錯誤消息和代碼（如果失敗）。 [!UICONTROL 計畫查詢] 頁籤。 您還可以根據這些查詢的狀態通過UI訂閱其中任何查詢的警報。 查看 [監視查詢文檔](../../query-service/ui/monitor-queries.md) 瞭解有關此功能的詳細資訊。 |
| 查詢加速報告見解資料模型 | 作為資料DistillerSKU的一部分，查詢加速儲存使您能夠減少從資料中獲取關鍵見解所需的時間和處理能力。 通過查詢加速儲存，您可以構建自定義資料模型和/或在現有的Adobe Real-time Customer Data Platform資料模型上擴展，以改進報告洞察力和可視化效果。 查看 [查詢加速儲存報告insights文檔](../../query-service/data-distiller/query-accelerated-store/reporting-insights-data-model.md) 瞭解有關此功能的詳細資訊。 |

{style="table-layout:auto"}

有關查詢服務的詳細資訊，請參閱 [查詢服務概述](../../query-service/home.md)。
Adobe Experience Platform的新功能：

## 來源 {#sources}

Adobe Experience Platform可以從外部源接收資料，同時允許您使用平台服務來構建、標籤和增強資料。 您可以從多種來源(如Adobe應用程式、基於雲的儲存、第三方軟體和您的CRM系統)接收資料。

Experience Platform提供REST風格的API和互動式UI，讓您能夠輕鬆地為各種資料提供程式設定源連接。 通過這些源連接，您可以驗證並連接到外部儲存系統和CRM服務，設定接收運行時間，並管理資料接收吞吐量。

**已更新功能**

| 功能 | 說明 |
| --- | --- | 
| Adobe Workfront源的Beta版本 | 使用 [Adobe Workfront源](../../sources/connectors/adobe-applications/workfront.md) 將您的Workfront資料Experience Platform並執行使用案例，例如將工作記錄與第三方資料組合、對工作記錄應用歷史和時間序列分析，以及使用標準SQL查詢工作資料。 有關詳細資訊，請閱讀上的指南 [在UI中建立Workfront源連接](../../sources/tutorials/ui/create/adobe-applications/workfront.md)。 |

要瞭解有關源的詳細資訊，請閱讀 [源概述](../../sources/home.md)。
