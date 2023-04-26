---
title: Adobe Experience Platform 發行說明
description: 2023年3月Adobe Experience Platform發行說明。
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 938b4ba7affadc7ad0eca086d7cc2c9ce1a54a83
workflow-type: tm+mt
source-wordcount: '779'
ht-degree: 6%

---

# Adobe Experience Platform 發行說明

**發行日期：2023 年 4 月 26 日**

Adobe Experience Platform 現有功能更新：

- [儀表板](#dashboards)
- [資料準備](#data-prep)
- [體驗資料模型](#xdm)
- [即時客戶設定檔](#profile)
- [來源](#sources)

## 儀表板 {#dashboards}

Adobe Experience Platform提供多個控制面板，讓您透過這些控制面板檢視組織資料的重要深入分析（在每日快照中擷取）。

**新功能或更新功能** {#dashboards-new-updated-features}

| 功能 | 說明 |
| --- | --- |
| 使用者定義的控制面板 | 您現在可以 **篩選歷史資料** 從介面工具集分析，並使用最近的資料或自訂分析時段。<br>您現在也可以 **複製現有小工具**. 透過自訂復本並編輯其屬性，您可以避免在建立新、獨特的Widget時從頭重新啟動。 |

{style="table-layout:auto"}

如需控制面板的詳細資訊，包括如何授與存取權限和建立自訂Widget，請從閱讀 [控制面板概觀](../../dashboards/home.md).

## 資料準備 {#data-prep}

資料準備可讓資料工程師將資料對應、轉換及驗證至Experience Data Model(XDM)。

**更新功能**

| 功能 | 說明 |
| --- | --- |
| 更新非生產沙箱中Adobe Analytics的回填期間 | 非生產沙箱中Adobe Analytics的回填期已縮短至三個月。 生產沙箱的回填在13個月內保持不變。 此變更僅適用於新流，不會影響現有流。 如需詳細資訊，請閱讀 [Adobe Analytics概述](../../sources/connectors/adobe-applications/analytics.md). |
| 新的映射程式函式，可將FPID字串轉換為ECID | 使用 `fpid_to_ecid` 函式將FPID字串轉換為ECID，以用於Experience Platform和Experience Cloud應用程式。 如需詳細資訊，請閱讀 [資料準備功能指南](../../data-prep/functions.md). |

{style="table-layout:auto"}

有關資料準備的詳細資訊，請閱讀 [資料準備概述](../../data-prep/home.md).

## Experience Data Model(XDM) {#xdm}

XDM是開放原始碼規格，可針對匯入Adobe Experience Platform的資料提供通用結構和定義（結構）。 遵循XDM標準，所有客戶體驗資料皆可整合至通用表示法，以更快速、更整合的方式提供深入分析。 您可以從客戶動作中獲得寶貴的深入分析、透過區段定義客戶受眾，以及將客戶屬性用於個人化目的。

**更新功能**

| 功能 | 說明 |
| --- | --- |
| 顯示名稱切換 | 結構編輯器現在提供切換按鈕，讓您在原始欄位名稱和更容易閱讀的顯示名稱之間進行變更。 此彈性可改善欄位探索能力，以及編輯結構。 標準欄位群組的顯示名稱是系統產生的，但如有需要，也可透過UI自訂。 |

{style="table-layout:auto"}

如需Platform中XDM的詳細資訊，請參閱 [XDM系統概觀](../../xdm/home.md).

## 即時客戶設定檔 {#profile}

Adobe Experience Platform可讓您為客戶提供協調、一致且相關的體驗，無論客戶在何處或何時與您的品牌互動。 透過即時客戶個人檔案，您可以全面了解各個客戶，其中結合來自多個管道的資料，包括線上、離線、CRM和第三方資料。 設定檔可讓您將客戶資料併入統一檢視中，提供每個客戶互動的可操作、時間戳記帳戶。

**更新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 假名的設定檔資料過期 | 現在正式提供匿名的設定檔資料過期！ 啟用後，此版本會持續從您的Experience Platform例項移除過時的匿名設定檔。 若要進一步了解此功能和假名的設定檔，請閱讀 [假名描述檔資料過期指南](../../profile/pseudonymous-profiles.md). |

## 來源 {#sources}

Adobe Experience Platform可內嵌來自外部來源的資料，並可讓您使用Platform服務來建構、加標籤及增強該資料。 您可以內嵌來自各種來源的資料，例如Adobe應用程式、雲端儲存、協力廠商軟體和您的CRM系統。

Experience Platform提供RESTful API和互動式UI，讓您輕鬆為各種資料提供者設定來源連線。 這些源連接允許您驗證並連接到外部儲存系統和CRM服務、設定獲取運行時間以及管理資料獲取吞吐量。

**更新功能**

| 功能 | 說明 |
| --- | --- |
| API支援篩選Microsoft Dynamics、Salesforce CRM和SalesforceMarketing Cloud的列層級資料 | 使用邏輯和比較運算子來篩選Microsoft Dynamics、Salesforce CRM和SalesforceMarketing Cloud來源的列層級資料。 閱讀指南 [使用API篩選來源的資料](../../sources/tutorials/api/filter.md) 以取得更多資訊。 |
| Shopify串流測試版可用性 | 此 [Shopify流源](../../sources/connectors/ecommerce/shopify-streaming.md) 現已提供測試版。 使用Shopify串流來源，將資料從Shopify合作夥伴帳戶串流到Experience Platform。 |
| OneTrust整合的全面推出 | 此 [OneTrust整合源](../../sources/connectors/consent-and-preferences/onetrust.md) 現已正式啟用。 使用OneTrust整合源將OneTrust整合帳戶中的同意和首選項資料帶入Experience Platform。 |
| oracle服務雲端正式發行 | 此 [Oracle服務雲端來源](../../sources/connectors/customer-success/oracle-service-cloud.md) 現已正式啟用。 使用Oracle服務雲端來源將Oracle服務雲端資料帶入Experience Platform。 |

{style="table-layout:auto"}

若要進一步了解來源，請閱讀 [來源概觀](../../sources/home.md).