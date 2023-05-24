---
title: Adobe Experience Platform發行說明2023年2月
description: 2023年2月為Adobe Experience Platform發佈的說明。
exl-id: 1c30a646-d9f8-4749-ac25-40bc48365a40
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '1293'
ht-degree: 4%

---

# Adobe Experience Platform 發行說明

**發行日期：2023 年 2 月 22 日**

Adobe Experience Platform 現有功能更新：

- [資料收集](#data-collection)
- [[!DNL Destinations]](#destinations)
- [體驗資料模型(XDM)](#xdm)
- [查詢服務](#query-service)
- [Real-Time Customer Data Platform B2B 版本](#b2b)
- [來源](#sources)

## 資料收集 {#data-collection}

Adobe Experience Platform公司提供了一套技術，使您能夠收集客戶端客戶體驗資料並將其發送到Adobe Experience Platform邊緣網路，在該網路中，資料可以得到豐富、轉換並分發到Adobe或非Adobe目的地。

### 保證 {#assurance}

Adobe保障允許您檢查、驗證、模擬和驗證如何在移動應用中收集資料或提供體驗。

**新增或更新的功能**

| 功能 | 說明 |
| ------- | ----------- |
| 公共API | Adobe保障API現在可用。 Assurance API是API的集合，當用Mobile SDK配置Adobe保障擴展時，它使用戶能夠test和調試自己的Web和移動應用。 要瞭解有關Assurance API的更多資訊，請閱讀 [保障API概述](https://developer.adobe.com/adobe-assurance-public-apis/)。 |

{style="table-layout:auto"}

有關Assurance的詳細資訊，請閱讀 [保證文檔](https://developer.adobe.com/client-sdks/documentation/platform-assurance/)。

## [!DNL Destinations] {#destinations}

[!DNL Destinations] 是預先構建的與目標平台的整合，允許無縫激活來自Adobe Experience Platform的資料。 您可以使用目標來激活跨渠道市場營銷活動、電子郵件活動、目標廣告和許多其他使用案例的已知和未知資料。

**新增或更新的功能** {#destinations-new-updated-features}

| 功能 | 說明 |
| ----------- | ----------- |
| [同意策略增強](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-enhancement) 用於整合 [基於檔案（批處理）的目標](/help/destinations/destination-types.md#file-based) | <p> 當配置檔案不再符合許可策略的條件時，Experience Platform現在會主動將其策略退出通知到基於檔案的目標。 這跟 [2023年2月發佈](/help/release-notes/2023/january-2023.md#destinations-new-updated-functionality) 流目標的功能相同。 </p> <p> <b>注釋</b>:此功能僅適用於 **[!UICONTROL 隱私和安全防護]**&#x200B;和 **[!UICONTROL 醫療保健盾]**。 </p> |

{style="table-layout:auto"}

**新建或更新的文檔** {#destinations-new-updated-documentation}

| 文件 | 說明 |
| ----------- | ----------- |
| 目標工作方式文檔 | <p>根據用戶的常見問題，我們發表了三篇關於目標工作方式的新解釋文章：</p> <p><ul><li>[目標中的可配置和常用導出設定](/help/destinations/how-destinations-work/destinations-configurations.md)</li><li>[不同目標類型的配置檔案導出行為](/help/destinations/how-destinations-work/profile-export-behavior.md)</li><li>[目標激活工作流中的身份處理](/help/destinations/how-destinations-work/identity-handling.md)</li></p> |

有關目標的更多一般資訊，請參閱 [目標概述](../../destinations/home.md)。

## 體驗資料模型(XDM) {#xdm}

XDM是一種開源規範，它為傳入Adobe Experience Platform的資料提供通用結構和定義（架構）。 通過遵守XDM標準，所有客戶體驗資料都可以納入到共同的表示形式中，以更快、更整合的方式提供見解。 您可以從客戶操作中獲得有價值的見解，通過細分市場定義客戶受眾，並將客戶屬性用於個性化目的。

**已更新功能**

| 功能 | 說明 |
| --- | --- |
| 通過UI的欄位棄用 | 你現在可以 [在接收資料後，已取消架構中的欄位](../../xdm/tutorials/field-deprecation-ui.md)。 XDM欄位過時允許您從UI視圖中刪除欄位，同時保留這些欄位以供使用。 如果需要，您可以再次顯示已過時的欄位，引用這些欄位的任何段、查詢或下游解決方案將照常運行。 |

{style="table-layout:auto"}

**新的XDM元件**

| 元件類型 | 名稱 | 說明 |
| --- | --- | --- |
| 類別 | [[!UICONTROL XDM個人潛在客戶配置檔案]](https://github.com/adobe/xdm/pull/1669/files) | XDM Individual Prospect Profile類將引入合作夥伴提供的ID。 |

{style="table-layout:auto"}

**更新的XDM元件**

| 元件類型 | 名稱 | 說明 |
| --- | --- | --- |
| 欄位群組 | [!UICONTROL 頻率上限約束] | 的 [!UICONTROL 頻率上限約束] 欄位組已 [已更新以支援重複事件和自定義事件](https://github.com/adobe/xdm/pull/1641/files)。 |
| 資料類型 | [!UICONTROL Web引用者] | Web引用者屬性已 [已更新，包括 `xdm:linkName` 和 `xdm:linkRegion`](https://github.com/adobe/xdm/pull/1666/files)。 分別是在上一頁上選擇的HTML元素的名稱和區域。 |
| 欄位組 | [!UICONTROL AdobeCJM ExperienceEvent — 消息交互詳細資訊] | [的 [!UICONTROL 跟蹤器URL] 已添加欄位](https://github.com/adobe/xdm/pull/1665/files) 到 [!UICONTROL AdobeCJM體驗事件]。 此跟蹤器提供用戶選擇的URL。 |
| 欄位組 | [!UICONTROL AdobeCJM ExperienceEvent — 消息交互詳細資訊] | [空 `meta:enum` 屬性已刪除](https://github.com/adobe/xdm/pull/1668/files) 的子菜單。 [!UICONTROL 跟蹤類型] 的子菜單。 |
| 資料類型 | [!UICONTROL 媒體資訊] | [從 `videoSegment` 物業 [!UICONTROL 媒體資訊] 資料類型已刪除](https://github.com/adobe/xdm/pull/1667/files)。 |

{style="table-layout:auto"}

有關平台中XDM的詳細資訊，請閱讀 [XDM系統概述](../../xdm/home.md). &#x200B;

## 查詢服務 {#query-service}

查詢服務允許您使用標準SQL查詢Adobe Experience Platform的資料 [!DNL Data Lake]。 您可以加入資料湖中的任何資料集，並將查詢結果捕獲為新資料集，以用於報告、Data Science Workspace或接收到即時客戶配置檔案。

**已更新功能**

| 功能 | 說明 |
| --- | --- |
| 為使用SQL的配置檔案啟用資料集 | [在CTAS查詢中使用LABEL使資料集「配置檔案已啟用」](../../query-service/sql/syntax.md#create-table-as-select)或使用ALTER更新要為配置檔案啟用的現有資料集。 您可以使用此擴展的SQL構造為Real-Time Customer Profile業務使用案例的派生屬性提供無縫支援。 查看 [派生屬性文檔的無縫SQL流](../../query-service/data-distiller/derived-attributes/seamless-sql-flow.md) 的子菜單。 |
| 監視計畫查詢 | 使用 [「計畫查詢」頁籤](../../query-service/ui/monitor-queries.md) 查找有關查詢運行和訂閱警報的重要資訊。 如果計畫詳細資訊、狀態和錯誤消息/代碼失敗，則監視查詢。 |
| 切換自動完成功能 | 消除某些元資料命令並通過 [切換查詢編輯器自動完成功能](../../query-service/ui/user-guide.md#auto-complete)。 此功能在您編寫查詢時自動建議可能的SQL關鍵字和表詳細資訊。 |
| 資料集示例 | 在查詢中指定採樣率， [使用資料集樣本建立統一隨機樣本](../../query-service/essential-concepts/dataset-samples.md)，或根據特定條件建立條件樣本。 |

{style="table-layout:auto"}

有關查詢服務的詳細資訊，請參閱 [查詢服務概述](../../query-service/home.md)。


## Real-Time Customer Data Platform B2B 版本 {#b2b}

Real-Time CDPB2B版本以Real-time Customer Data Platform(Real-Time CDP)為基礎，專門為以企業對企業服務模式運營的營銷人員而設計。 它將來自多個來源的資料匯集在一起，並將其合併到人員和帳戶配置檔案的單個視圖中。 此統一資料使營銷人員能夠精確地瞄準特定受眾，並跨所有可用渠道接觸這些受眾。

**已更新功能**

| 功能 | 說明 |
| --- | --- |
| 啟用相關帳戶服務 | 新的切換功能允許您啟用帳戶上的相關帳戶服務。 有關詳細資訊，請閱讀上的指南 [啟用相關帳戶服務](../../rtcdp/b2b-ai-ml-services/related-accounts.md#enable)。 |

{style="table-layout:auto"}

要瞭解有關Real-Time CDPB2B版的更多資訊，請閱讀 [Real-Time CDPB2B版概述](../../rtcdp/overview.md)。

## 來源 {#sources}

Adobe Experience Platform可以從外部源接收資料，並允許您使用平台服務來構建、標籤和增強資料。 您可以從多種來源(如Adobe應用程式、基於雲的儲存、第三方軟體和您的CRM系統)接收資料。

Experience Platform提供REST風格的API和互動式UI，讓您能夠輕鬆地為各種資料提供程式設定源連接。 通過這些源連接，您可以驗證並連接到外部儲存系統和CRM服務，設定接收運行時間，並管理資料接收吞吐量。

**已更新功能**

| 功能 | 說明 |
| --- | --- |
| 指定訂閱級訪問 [!DNL Google PubSub] | 現在，您可以在使用 [!DNL Google PubSub] 提供訂閱ID來源。 有關詳細資訊，請閱讀 [!DNL Google PubSub] 驗證教程 [使用流服務API](../../sources/tutorials/api/create/cloud-storage/google-pubsub.md) 或 [平台UI](../../sources/tutorials/ui/create/cloud-storage/google-pubsub.md)。 |
| 從中接收自定義活動資料 [!DNL Marketo] | 現在，您可以從 [!DNL Marketo] 實例到Experience Platform。 要接收自定義活動資料，必須在B2B活動架構中設定自定義活動欄位組，並使用活動資料集建立資料流。 資料流完成後，接收的資料集將同時包含來自您的 [!DNL Marketo] 實例。 然後，您可以 [查詢服務](../../query-service/home.md) 訪問平台上的自定義活動記錄。 有關詳細資訊，請閱讀上的指南 [為自定義活動資料建立資料流](../../sources/tutorials/ui/create/adobe-applications/marketo-custom-activities.md)。 |
| 從 [!DNL Marketo] | 現在，您可以配置在為公司資料建立資料流時，是否要排除或包括未申請帳戶的接收。 有關詳細資訊，請閱讀上的指南 [建立源連接和資料流 [!DNL Marketo]](../../sources/tutorials/ui/create/adobe-applications/marketo.md)。 |

{style="table-layout:auto"}

要瞭解有關源的詳細資訊，請閱讀 [源概述](../../sources/home.md)。
