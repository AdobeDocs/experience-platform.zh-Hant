---
title: Adobe Experience Platform 發行說明
description: Adobe Experience Platform的最新發行說明。
source-git-commit: cf8f630360c2cdbba1082913b179e719156183f4
workflow-type: tm+mt
source-wordcount: '1060'
ht-degree: 5%

---

# Adobe Experience Platform 發行說明

**發行日期：2022 年 10 月 26 日**

Adobe Experience Platform的新功能：

- [客戶管理金鑰](#cmk)

Adobe Experience Platform 現有功能更新：

- [資料收集](#data-collection)
- [目的地](#destinations)
- [Experience Data Model(XDM)](#xdm)
- [查詢服務](#query-service)
- [來源](#sources)

## 客戶管理金鑰 {#cmk}

儲存在Adobe Experience Platform上的所有資料都會使用系統層級的金鑰進行靜態加密。 如果您使用的是以Platform為建置基礎的應用程式，您現在可以選擇使用您自己的加密密鑰，讓您能夠更好地控制資料安全性。

請參閱 [客戶管理金鑰](../../landing/governance-privacy-security/customer-managed-keys.md) 以取得功能的詳細資訊。

## 資料收集 {#data-collection}

Adobe Experience Platform提供一套技術，可讓您收集用戶端客戶體驗資料，並傳送至Adobe Experience Platform Edge Network，以便在中加以擴充、轉換及分發至Adobe或非Adobe目的地。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 資料流的敏感資料處理 | Datastreams現在利用多種Platform技術適當處理受醫療保險可移植性和責任法案(HIPAA)等法規強制實施的敏感資料。 請參閱 [處理資料流中的敏感資料](../../edge/datastreams/overview.md#sensitive) 以取得更多資訊。 |
| [!DNL Splunk] 事件轉送擴充功能 | 您現在可以將資料傳送至 [!DNL Splunk] 使用 [事件轉送](../../tags/ui/event-forwarding/overview.md) 擴充功能。 請參閱 [[!DNL Splunk] 擴充功能概觀](../../tags/extensions/web/splunk/overview.md) 以取得更多資訊。 |
| [!DNL Zendesk] 事件轉送擴充功能 | 您現在可以將資料傳送至 [!DNL Zendesk] 使用 [事件轉送](../../tags/ui/event-forwarding/overview.md) 擴充功能。 請參閱 [[!DNL Zendesk] 擴充功能概觀](../../tags/extensions/web/zendesk/overview.md) 以取得更多資訊。 |

{style=&quot;table-layout:auto&quot;}

## [!DNL Destinations] {#destinations}

[!DNL Destinations] 預先建置與目的地平台的整合，可順暢地從Adobe Experience Platform啟動資料。 您可以使用目的地來針對跨通路行銷活動、電子郵件行銷活動、目標廣告和其他許多使用案例，啟用已知和未知的資料。

**新目的地或更新目的地**

| 目的地 | 說明 |
| ----------- | ----------- |
| [[!DNL Line]](../../destinations/catalog/mobile-engagement/line.md) | Line是一個熱門的通訊平台，將人員、服務和資訊連接起來，並從聊天應用程式發展為娛樂、社交和日常活動的中心。 |
| [[!DNL Microsoft Dynamics 365]](../../destinations/catalog/crm/microsoft-dynamics-365.md) | Microsoft Dynamics 365是一個基於雲的業務應用平台，它將企業資源規劃(ERP)和客戶關係管理(CRM)與生產應用程式和AI工具結合在一起，從而實現端到端更流暢、更受控的操作、更好的增長潛力和降低成本。 |
| [[!DNL (Beta) Adobe Commerce]](../../destinations/catalog/personalization/adobe-commerce.md) | 此 [!DNL (Beta) Adobe Commerce] 目的地連接器可讓您選取一或多個要啟用的Real-Time CDP區段 [!DNL Adobe Commerce] 帳戶，為購物者提供動態的個人化體驗。 內 [!DNL Adobe Commerce]，您就可以選取這些Real-Time CDP區段，以個人化購物車中的獨特選件，例如「購買2即可免費獲得1」。 您也可以顯示主圖橫幅廣告，並透過促銷優惠方案修改產品定價，所有優惠方案皆自訂為Adobe Real-Time CDP區段。 |

{style=&quot;table-layout:auto&quot;}

**新檔案或更新檔案**

| 文件 | 說明 |
| ----------- | ----------- |
| [目的地護欄](../../destinations/guardrails.md) | 此頁面提供與啟動行為相關的預設使用量和比率限制。 |

如需目的地的詳細一般資訊，請參閱 [目的地概述](../../destinations/home.md).

## Experience Data Model(XDM) {#xdm}

XDM是開放原始碼規格，可針對匯入Adobe Experience Platform的資料提供通用結構和定義（結構）。 遵循XDM標準，所有客戶體驗資料皆可整合至通用表示法，以更快速、更整合的方式提供深入分析。 您可以從客戶動作中獲得寶貴的深入分析、透過區段定義客戶受眾，以及將客戶屬性用於個人化目的。

**更新XDM元件**

| 元件類型 | 名稱 | 說明 |
| --- | --- | --- |
| 資料類型 | [[!UICONTROL 工作階段詳細資訊]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | 更新 `authorized` 欄位（從布林類型）轉換為字串。 `season` 和 `episode` 已從整數變更為字串。 |
| 資料類型 | [[!UICONTROL 廣告詳細資訊]](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingdetails.schema.json) | `name` 已重新命名為 `friendlyName`，和 `ID` 已重新命名為 `name`. |
| 資料類型 | [[!UICONTROL 錯誤詳細資訊]](https://github.com/adobe/xdm/blob/master/components/datatypes/errordetails.schema.json) | `ID` 已重新命名為 `name`。 |

{style=&quot;table-layout:auto&quot;}

如需Platform中XDM的詳細資訊，請參閱 [XDM系統概觀](../../xdm/home.md).

## 查詢服務 {#query-service}

查詢服務可讓您使用標準SQL在Adobe Experience Platform中查詢資料 [!DNL Data Lake]. 您可以從 [!DNL Data Lake] 並將查詢結果擷取為新資料集，以用於報表、Data Science Workspace或擷取至「即時客戶個人檔案」。

**更新功能**

| 功能 | 說明 |
| --- | --- |
| 透過Platform UI監控查詢 | 查詢服務 [!UICONTROL 排程查詢] 索引標籤可改善透過UI查詢作業狀態的可見性。 您現在可以找到查詢執行狀態的重要資訊，包括錯誤訊息和失敗的程式碼，從 [!UICONTROL 排程查詢] 標籤。 您也可以根據其狀態，透過UI訂閱這些查詢中任何一個的警報。 請參閱 [監視查詢文檔](../../query-service/monitor-queries.md) 以深入了解此功能。 |
| 查詢加速報告前瞻分析資料模型 | 作為Data Distiller SKU的一部分，查詢加速儲存可讓您減少從資料中獲取重要見解所需的時間和處理能力。 透過查詢加速存放區，您可以建立自訂資料模型及/或擴充現有的Adobe Real-time Customer Data Platform資料模型，以改善您的報表分析及其視覺效果。 請參閱 [查詢加速儲存報告深入分析檔案](../../query-service/query-accelerated-store/reporting-insights-data-model.md) 以深入了解此功能。 |

{style=&quot;table-layout:auto&quot;}

有關Query Services的詳細資訊，請參閱 [查詢服務概述](../../query-service/home.md).
Adobe Experience Platform的新功能：

## 來源 {#sources}

Adobe Experience Platform可內嵌來自外部來源的資料，同時允許您使用Platform服務來建構、加標籤及增強該資料。 您可以內嵌來自各種來源的資料，例如Adobe應用程式、雲端儲存、協力廠商軟體和您的CRM系統。

Experience Platform提供RESTful API和互動式UI，讓您輕鬆為各種資料提供者設定來源連線。 這些源連接允許您驗證並連接到外部儲存系統和CRM服務、設定獲取運行時間以及管理資料獲取吞吐量。

**更新功能**

| 功能 | 說明 |
| --- | --- | 
| Adobe Workfront來源測試版可用性 | 使用 [Adobe Workfront來源](../../sources/connectors/adobe-applications/workfront.md) 將Workfront資料帶入Experience Platform，並執行使用案例，如將工作記錄與第三方資料結合、對工作記錄套用歷史和時間序列分析，以及使用標準SQL查詢工作資料。 如需詳細資訊，請參閱 [在UI中建立Workfront來源連線](../../sources/tutorials/ui/create/adobe-applications/workfront.md). |
| oracle服務雲源的測試版可用性 | 使用Oracle服務雲端來源，將資料從您的Oracle服務雲端帳戶內嵌至Experience Platform。 如需詳細資訊，請參閱 [Oracle服務雲端來源](../../sources/connectors/customer-success/oracle-service-cloud.md). |

若要進一步了解來源，請閱讀 [來源概觀](../../sources/home.md).
