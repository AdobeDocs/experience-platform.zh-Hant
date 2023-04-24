---
title: Adobe Experience Platform發行說明2023年4月
description: 2023年4月Adobe Experience Platform發行說明。
source-git-commit: 9f50ca4b2a4c576af5ce8ee5c085a7603fed2560
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 6%

---

# Adobe Experience Platform 發行說明

**發行日期：2023 年 4 月 26 日**

Adobe Experience Platform 現有功能更新：

- [資料準備](#data-prep)
- [來源](#sources)

## 資料準備 {#data-prep}

資料準備可讓資料工程師將資料對應、轉換及驗證至Experience Data Model(XDM)。

**更新功能**

| 功能 | 說明 |
| --- | --- |
| 更新非生產沙箱中Adobe Analytics的回填期間 | 非生產沙箱中Adobe Analytics的回填期已縮短至三個月。 生產沙箱的回填在13個月內保持不變。 此變更僅適用於新流，不會影響現有流。 如需詳細資訊，請閱讀 [Adobe Analytics概述](../../sources/connectors/adobe-applications/analytics.md). |
| 新的映射程式函式，可將FPID字串轉換為ECID | 使用 `fpid_to_ecid` 函式將FPID字串轉換為ECID，以用於Experience Platform和Experience Cloud應用程式。 如需詳細資訊，請閱讀 [資料準備功能指南](../../data-prep/functions.md). |

{style="table-layout:auto"}

有關資料準備的詳細資訊，請閱讀 [資料準備概述](../../data-prep/home.md).

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
