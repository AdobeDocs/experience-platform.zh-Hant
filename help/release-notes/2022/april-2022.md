---
title: Adobe Experience Platform Release Notes April 2022
description: The April 2022 release notes for Adobe Experience Platform.
source-git-commit: fe30444fb2d11c38433c73d88ee4c8e9a32bdff8
workflow-type: tm+mt
source-wordcount: '1045'
ht-degree: 4%

---

# Adobe Experience Platform 發行說明

**發行日期：2022 年 4 月 27 日**

Adobe Experience Platform 現有功能更新：

- [資料流](#dataflows)
- [體驗資料模型(XDM)](#xdm)

## 資料流 {#dataflows}

In Platform, data is ingested from many different sources, analyzed within the system, and activated to a wide variety of destinations. 通過向資料流提供透明性，平台使跟蹤這種潛在的非線性資料流的過程變得更容易。

資料流是跨平台移動資料的作業的表示形式。 這些資料流是跨不同的服務配置的，可幫助將資料從源連接器移動到目標資料集，然後由Identity Service和即時客戶配置檔案使用，最終激活到目標。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| Segments dashboard | 現在，您可以使用監視儀表板監視段的資料流。 To learn more, please read the guide on [monitoring segments in the UI](../../dataflows/ui/monitor-segments.md) |

有關資料流的詳細資訊，請參閱 [資料流概述](../../dataflows/home.md)。 要瞭解有關分段的詳細資訊，請參閱 [分段概述](../../segmentation/home.md)。

## 體驗資料模型(XDM) {#xdm}

XDM是一種開源規範，它為傳入Adobe Experience Platform的資料提供通用結構和定義（架構）。 通過遵守XDM標準，所有客戶體驗資料都可以納入到共同的表示形式中，以更快、更整合的方式提供見解。 您可以從客戶操作中獲得有價值的見解，通過細分市場定義客戶受眾，並將客戶屬性用於個性化目的。

**新功能**

| 功能 | 說明 |
| --- | --- |
| 添加或刪除架構的單個標準欄位 | The Schema Editor UI now allows you to add portions of standard field groups to your schemas, providing more flexibility for the fields you choose to include without needing to build custom resources from scratch.<br><br>現在，您還可以直接在架構結構中定義即席自定義域，並將它們分配給新的或現有的自定義域組，而無需事先建立或編輯域組。<br><br>See the guide on [creating and editing schemas in the UI](../../xdm/ui/resources/schemas.md) for more information on these new workflows. |

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
| 欄位組 | [[!UICONTROL Secondary Recipient Detail For Audit]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/secondary-recipient-detail.schema.json) | Adobe Journey Optimizer欄位組，用於捕獲審核的輔助收件人詳細資訊。 |
| 欄位組 | [[!UICONTROL XDM業務帳戶人員關係詳細資訊]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/account-person/account-person-details.schema.json) | 捕獲與帳戶 — 人員關係相關的詳細資訊。 |
| 欄位組 | [[!UICONTROL 帳戶人員詳細資訊]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/account-person/account-person-details.schema.json) | 捕獲與帳戶 — 人員關係相關的詳細資訊。 |
| 資料類型 | [[!UICONTROL Cart]](https://github.com/adobe/xdm/blob/master/components/datatypes/cart.schema.json) | 捕獲有關電子商務購物車的資訊。 |
| 資料類型 | [[!UICONTROL 裝運]](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.schema.json) | 捕獲一個或多個產品的發運資訊。 |
| Data type | [[!UICONTROL 站點搜索]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-site-search.schema.json) | Captures information on site-search activity. |
| Extension (Workfront) | [[!UICONTROL Operational Task Attributes]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/opTask.schema.json) | Captures details related to an operational task. |
| 分機(Workfront) | [[!UICONTROL Work Portfolio Attributes]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/portfolio.schema.json) | 捕獲與工作組合相關的詳細資訊。 |
| 分機(Workfront) | [[!UICONTROL 工作計畫屬性]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/program.schema.json) | Captures details related to a work program. |
| Extension (Workfront) | [[!UICONTROL 工作項目屬性]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/project.schema.json) | Captures details related to a work project. |

{style=&quot;table-layout:auto&quot;}

**更新的XDM元件**

| 元件類型 | 名稱 | 更新說明 |
| --- | --- | --- |
| Global schema | [[!UICONTROL 目的地]](https://github.com/adobe/xdm/blob/master/schemas/destinations/destination.schema.json) | 新的枚舉值 `destinationCategory`。 |
| 描述符 | [[!UICONTROL 友好名稱描述符]](https://github.com/adobe/xdm/blob/master/schemas/descriptors/display/alternateDisplayInfo.schema.json) | 增加了對刪除建議值的支援(`meta:enum`)。 |
| 欄位組 | [[!UICONTROL 用戶登錄過程]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-user-login-details.schema.json) | `createProfile` 的下界。 |
| 資料類型 | [[!UICONTROL 商務]](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.schema.json) | 已添加幾個與購物車相關的欄位。 |
| 資料類型 | [[!UICONTROL 產品清單項]](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.schema.json) | 為所選選項和折扣金額添加的新欄位。 |
| 擴展（智慧服務） | [[!UICONTROL 智慧服務JourneyAI發送時間優化]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/intelligentServices/profile-journeyai-sendtimeoptimization.schema.json) | 優化發送時間分數的儲存格式。 |
| 分機(Workfront) | [[!UICONTROL Workfront變革事件]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/changeevent.schema.json) | 幾個欄位替換為 `workfront:customData` 的子菜單。 |
| 分機(Workfront) | [[!UICONTROL 工作任務屬性]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/task.schema.json) | 添加了幾個欄位。 |
| Extension (Workfront) | [[!UICONTROL Work Object]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/workobject.schema.json) | 父對象類型和自定義表單域的新欄位。 |

{style=&quot;table-layout:auto&quot;&quot;

For more information on XDM in Platform, see the [XDM System overview](../../xdm/home.md).

