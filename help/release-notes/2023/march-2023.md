---
title: Adobe Experience Platform發行說明2023年2月
description: 2023年3月Adobe Experience Platform發行說明。
source-git-commit: 44075e38664c01c64e7d09f5856353bff64becb5
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 5%

---

# Adobe Experience Platform 發行說明

**發行日期：2023 年 3 月 29 日**

Adobe Experience Platform 現有功能更新：

- [資料收集](#data-collection)
- [資料準備](#data-prep)
- [細分服務](#segmentation)
- [來源](#sources)

## 資料收集 {#data-collection}

Adobe Experience Platform提供一套技術，可讓您收集用戶端客戶體驗資料，並傳送至Adobe Experience Platform Edge Network，以便在中加以擴充、轉換及分發至Adobe或非Adobe目的地。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 中繼轉換API（測試版）的全新快速入門工作流程 | 從資料收集主畫面存取「快速入門」底下的全新快速入門工作流程！ 此 [中繼轉換API的快速入門工作流程](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/meta/overview.html?lang=en#quick-start) 讓客戶只需幾個簡單步驟，即可快速收集和轉送事件資料（從伺服器端轉送至中繼），以進行廣告轉換。 |
| [!DNL Braze] 事件轉送擴充功能 | 此 [[!DNL Braze Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) 事件轉送擴充功能可讓您運用Adobe Experience Platform邊緣網路中擷取的資料，並將其傳送至 [!DNL Braze] 以伺服器端事件的形式，使用 [!DNL Braze] 使用者追蹤API。 |
| [!DNL Mixpanel] 事件轉送擴充功能 | 此 [[!DNL Mixpanel Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) 擴充功能可讓客戶運用事件轉送功能，擷取Adobe Experience Platform邊緣網路中的事件資訊，並使用追蹤事件API將其傳送至Mixpanel。 |

{style="table-layout:auto"}

## 資料準備 {#data-prep}

資料準備可讓資料工程師將資料對應、轉換及驗證至Experience Data Model(XDM)。

**更新功能**

| 功能 | 說明 |
| --- | --- |
| 編碼和解碼URL字串的新函式 | <ul><li>此 `get_url_encoded` 函式會以URL作為輸入，並以ASCII字元取代或編碼特殊字元。</li><li>此 `get_url_decoded` 函式會將URL當作輸入，並將ASCII字元解碼為特殊字元。</li></ul> 如需詳細資訊，請閱讀 [資料準備功能指南](../../data-prep/functions.md). 如需保留字元及其對應編碼字元的完整清單，請閱讀指南，位於 [特殊字元](../../data-prep/functions.md#special-characters). |

有關資料準備的詳細資訊，請閱讀 [資料準備概述](../../data-prep/home.md).

## 分段服務 {#segmentation}

[!DNL Segmentation Service] 會透過說明區分客戶群中可行銷人員群組的條件，來定義特定設定檔子集。 區段可以根據記錄資料（例如人口統計資訊）或代表客戶與您品牌互動的時間序列事件。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 設定檔量度 | 為了讓您更精確地呈現設定檔量度，系統會結合成員劃分和流失量度，現在會在24小時內計算。 如需詳細資訊，請參閱 [區段UI指南](../../segmentation/ui/overview.md) |

{style="table-layout:auto"}

如需 [!DNL Segmentation Service]，請參閱 [區段概觀](../../segmentation/home.md).

## 來源 {#sources}

Adobe Experience Platform可內嵌來自外部來源的資料，並可讓您使用Platform服務來建構、加標籤及增強該資料。 您可以內嵌來自各種來源的資料，例如Adobe應用程式、雲端儲存、協力廠商軟體和您的CRM系統。

Experience Platform提供RESTful API和互動式UI，讓您輕鬆為各種資料提供者設定來源連線。 這些源連接允許您驗證並連接到外部儲存系統和CRM服務、設定獲取運行時間以及管理資料獲取吞吐量。

**更新功能**

| 功能 | 說明 |
| --- | --- |
| 測試版可用性 [!DNL Chatlio] | 此 [!DNL Chatlio] 來源現在可在測試版中取得。 使用 [!DNL Chatlio] 源流 [!DNL Chatlio] 事件資料Experience Platform。 如需詳細資訊，請閱讀 [[!DNL Chatlio] 概述](../../sources/connectors/marketing-automation/chatlio-webhook.md). |
| 測試版可用性 [!DNL Customer.io] | 此 [!DNL Customer.io] 來源現在可在測試版中取得。 使用 [!DNL Customer.io] 來源來串流客戶事件資料至Experience Platform。 如需詳細資訊，請閱讀 [[!DNL Customer.io] 概述](../../sources/connectors/marketing-automation/customerio-webhook.md). |
| 測試版可用性 [!DNL Pendo] | 此 [!DNL Pendo] 來源現在可在測試版中取得。 使用 [!DNL Pendo] 來源，將您的產品分析資料串流至Experience Platform。 如需詳細資訊，請閱讀 [[!DNL Pendo] 概述](../../sources/connectors/analytics/pendo-webhook.md). |
| 支援草稿資料流 | 您現在可以使用流程服務API將資料流設定為草稿狀態。 之後可更新草稿的資料流，並發佈新資訊。 如需詳細資訊，請參閱 [將源資料流設定為草稿](../../sources/tutorials/api/draft.md). |

{style="table-layout:auto"}

若要進一步了解來源，請閱讀 [來源概觀](../../sources/home.md).
