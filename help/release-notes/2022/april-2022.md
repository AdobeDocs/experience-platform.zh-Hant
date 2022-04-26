---
title: Adobe Experience Platform發行說明2022年4月
description: 2022年4月為Adobe Experience Platform發行的說明。
source-git-commit: d09eb2e71a5ebce31aeaf8560c20f0c8595f5d19
workflow-type: tm+mt
source-wordcount: '1473'
ht-degree: 5%

---

# Adobe Experience Platform 發行說明

**發行日期：2022 年 4 月 27 日**

Adobe Experience Platform 現有功能更新：

- [資料流](#dataflows)
- [[!DNL Data Prep]](#data-prep)
- [體驗資料模型(XDM)](#xdm)
- [Real-time Customer Data Platform B2B Edition](#B2B)
- [來源](#sources)

## 資料流 {#dataflows}

在平台中，資料被從許多不同的源中攝取，在系統內進行分析，並被激活到各種目的地。 通過向資料流提供透明性，平台使跟蹤這種潛在的非線性資料流的過程變得更容易。

資料流是跨平台移動資料的作業的表示形式。 這些資料流是跨不同的服務配置的，可幫助將資料從源連接器移動到目標資料集，然後由Identity Service和即時客戶配置檔案使用，最終激活到目標。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 段操控板 | 現在，您可以使用監視儀表板監視段的資料流。 要瞭解更多資訊，請閱讀上的指南 [監視UI中的段](../../dataflows/ui/monitor-segments.md) |

有關資料流的詳細資訊，請參閱 [資料流概述](../../dataflows/home.md)。 要瞭解有關分段的詳細資訊，請參閱 [分段概述](../../segmentation/home.md)。

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] 允許資料工程師將資料映射到體驗資料模型(XDM)並驗證資料。

**已更新功能**

| 功能 | 說明 |
| --- | --- |
| 支援Adobe Analytics來源 | Adobe Analytics源現在支援資料準備功能，允許您在建立資料流時將分析報告套件資料映射到目標XDM架構。 請參閱上的教程 [建立分析源連接](../../sources/tutorials/ui/create/adobe-applications/analytics.md) 的子菜單。 |
| 支援導入現有映射規則 | 現在，您可以從現有資料流導入映射規則，以加快資料流配置並限制錯誤。 請參閱上的教程 [導入現有映射規則](../../data-prep/ui/mapping.md) 的子菜單。 |

有關 [!DNL Data Prep]，請參閱 [[!DNL Data Prep] 概述](../../data-prep/home.md)。

## 體驗資料模型(XDM) {#xdm}

XDM是一種開源規範，它為傳入Adobe Experience Platform的資料提供通用結構和定義（架構）。 通過遵守XDM標準，所有客戶體驗資料都可以納入到共同的表示形式中，以更快、更整合的方式提供見解。 您可以從客戶操作中獲得有價值的見解，通過細分市場定義客戶受眾，並將客戶屬性用於個性化目的。

**新功能**

| 功能 | 說明 |
| --- | --- |
| 添加或刪除架構的單個標準欄位 | 現在，通過架構編輯器UI，您可以將標準欄位組的部分添加到您的架構中，從而為您選擇包括的欄位提供了更大的靈活性，而無需從頭構建自定義資源。<br><br>現在，您還可以直接在架構結構中定義即席自定義域，並將它們分配給新的或現有的自定義域組，而無需事先建立或編輯域組。<br><br>請參閱上的指南 [在UI中建立和編輯架構](../../xdm/ui/resources/schemas.md) 的子菜單。 |

{style=&quot;table-layout:auto&quot;}

**新的XDM元件**

| 元件類型 | 名稱 | 說明 |
| --- | --- | --- |
| 全局架構 | [[!UICONTROL 資料衛生操作請求]](https://github.com/adobe/xdm/blob/master/schemas/hygiene/aep-hygiene-ops-record.schema.json) | 捕獲資料清除請求的詳細資訊，以刪除或修改指定資料集或沙盒中的記錄。 |
| 描述符 | [[!UICONTROL 時間序列粒度描述符]](https://github.com/adobe/xdm/blob/master/schemas/descriptors/time-series/descriptorTimeSeriesGranularity.schema.json) | 指示時間序列和摘要資料的粒度。 應用到架構時，架構 `timestamp` 欄位是此粒度週期中的第一個時間戳。 |
| 類 | [[!UICONTROL XDM摘要度量]](https://github.com/adobe/xdm/blob/master/components/classes/summary_metrics.schema.json) | 提供具有分組維的預匯總度量，如具有GROUP BY的SQL SELECT的結果。 |
| 欄位組 | [[!UICONTROL 同意策略評估結果圖]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-site-search.schema.json) | 捕獲個人的同意策略評估結果。 |
| 欄位組 | [[!UICONTROL 站點搜索]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-site-search.schema.json) | 捕獲與站點搜索相關的資訊，如搜索查詢、篩選和排序。 |
| 欄位組 | [[!UICONTROL 合併銷售線索]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/events/merge-leads.schema.json) | 捕獲合併兩個或多個銷售線索的事件的詳細資訊。 |
| 欄位組 | [[!UICONTROL 已傳送電子郵件]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/events/emailsent.schema.json) | 捕獲將電子郵件發送到收件人的事件的詳細資訊。 |
| 欄位組 | [[!UICONTROL 拼接欄位]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-stitching.schema.json) | 捕獲通過事件的標識拼接過程計算的值。 |
| 欄位組 | [[!UICONTROL 審核的輔助收件人詳細資訊]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/secondary-recipient-detail.schema.json) | Adobe Journey Optimizer欄位組，用於捕獲審核的輔助收件人詳細資訊。 |
| 欄位組 | [[!UICONTROL XDM業務帳戶人員關係詳細資訊]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/account-person/account-person-details.schema.json) | 捕獲與帳戶 — 人員關係相關的詳細資訊。 |
| 欄位組 | [[!UICONTROL 帳戶人員詳細資訊]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/account-person/account-person-details.schema.json) | 捕獲與帳戶 — 人員關係相關的詳細資訊。 |
| 資料類型 | [[!UICONTROL 購物車]](https://github.com/adobe/xdm/blob/master/components/datatypes/cart.schema.json) | 捕獲有關電子商務購物車的資訊。 |
| 資料類型 | [[!UICONTROL 裝運]](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.schema.json) | 捕獲一個或多個產品的發運資訊。 |
| 資料類型 | [[!UICONTROL 站點搜索]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-site-search.schema.json) | 捕獲有關站點搜索活動的資訊。 |
| 分機(Workfront) | [[!UICONTROL 操作任務屬性]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/opTask.schema.json) | 捕獲與操作任務相關的詳細資訊。 |
| 分機(Workfront) | [[!UICONTROL 工作Portfolio屬性]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/portfolio.schema.json) | 捕獲與工作組合相關的詳細資訊。 |
| 分機(Workfront) | [[!UICONTROL 工作計畫屬性]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/program.schema.json) | 捕獲與工作程式相關的詳細資訊。 |
| 分機(Workfront) | [[!UICONTROL 工作項目屬性]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/project.schema.json) | 捕獲與工作項目相關的詳細資訊。 |

{style=&quot;table-layout:auto&quot;&quot;

**更新的XDM元件**

| 元件類型 | 名稱 | 更新說明 |
| --- | --- | --- |
| 全局架構 | [[!UICONTROL 目的地]](https://github.com/adobe/xdm/blob/master/schemas/destinations/destination.schema.json) | 新的枚舉值 `destinationCategory`。 |
| 描述符 | [[!UICONTROL 友好名稱描述符]](https://github.com/adobe/xdm/blob/master/schemas/descriptors/display/alternateDisplayInfo.schema.json) | 增加了對刪除建議值的支援(`meta:enum`)。 |
| 欄位組 | [[!UICONTROL 用戶登錄過程]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-user-login-details.schema.json) | `createProfile` 的下界。 |
| 資料類型 | [[!UICONTROL 商務]](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.schema.json) | 已添加幾個與購物車相關的欄位。 |
| 資料類型 | [[!UICONTROL 產品清單項]](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.schema.json) | 為所選選項和折扣金額添加的新欄位。 |
| 擴展（智慧服務） | [[!UICONTROL 智慧服務JourneyAI發送時間優化]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/intelligentServices/profile-journeyai-sendtimeoptimization.schema.json) | 優化發送時間分數的儲存格式。 |
| 分機(Workfront) | [[!UICONTROL Workfront變革事件]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/changeevent.schema.json) | 幾個欄位替換為 `workfront:customData` 的子菜單。 |
| 分機(Workfront) | [[!UICONTROL 工作任務屬性]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/task.schema.json) | 添加了幾個欄位。 |
| 分機(Workfront) | [[!UICONTROL 工作對象]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/workobject.schema.json) | 父對象類型和自定義表單域的新欄位。 |

{style=&quot;table-layout:auto&quot;&quot;

有關平台中XDM的詳細資訊，請參見 [XDM系統概述](../../xdm/home.md)。

### Real-time Customer Data PlatformB2B版 {#B2B}

即時CDP B2B版本構建在Real-time Customer Data Platform（即時CDP）之上，專門為以業務到業務服務模式運營的營銷人員而構建。 它將來自多個來源的資料匯集在一起，並將其合併到人員和帳戶配置檔案的單個視圖中。 此統一資料使營銷人員能夠精確地瞄準特定受眾，並跨所有可用渠道接觸這些受眾。

**已更新功能**

| 功能 | 說明 |
| --- | --- |
| 支援 `isDeleted` 功能 | 全部 [!DNL Marketo] 資料集 `Activities` 現在支援 `isDeleted` 映射。 新映射將自動添加到現有B2B資料流中。 您可以使用 `isDeleted` 映射以過濾已刪除的記錄，以便 [!DNL Data Lake] 與源資料一致。 查看 [[!DNL Marketo] 映射欄位指南](../../sources/connectors/adobe-applications/mapping/marketo.md) 的 `isDeleted`。 |

要瞭解有關Real-time Customer Data PlatformB2B版的詳細資訊，請參閱 [B2B概述](../../rtcdp/b2b-overview.md)。

## 來源 {#sources}

Adobe Experience Platform可以從外部源接收資料，同時允許您使用平台服務來構建、標籤和增強資料。 您可以從多種來源(如Adobe應用程式、基於雲的儲存、第三方軟體和您的CRM系統)接收資料。

Experience Platform提供REST風格的API和互動式UI，讓您能夠輕鬆地為各種資料提供程式設定源連接。 通過這些源連接，您可以驗證並連接到外部儲存系統和CRM服務，設定接收運行時間，並管理資料接收吞吐量。

**已更新功能**

| 功能 | 說明 |
| --- | --- |
| 支援 [!DNL OneTrust Integration] | 您現在可以使用 [!DNL OneTrust Integration] 從您的 [!DNL OneTrust] 帳戶到平台。 請參閱 [建立 [!DNL OneTrust Integration] 源連接](../../sources/connectors/consent-and-preferences/onetrust.md) 的子菜單。 |
| 支援 [!DNL Square] | 您現在可以使用 [!DNL Square] 從您的 [!DNL Square] 帳戶到平台。 |
| 支援刪除客戶屬性資料流 | 現在，您可以刪除使用「客戶屬性」源連接器建立的資料流。 |

要瞭解有關源的詳細資訊，請參閱 [源概述](../../sources/home.md)。
