---
title: Adobe Experience Platform 發行說明
description: Adobe Experience Platform 2023年9月版本注意事項。
source-git-commit: 1bfd5e05642e0ac8f80af5502878eaee0b33c704
workflow-type: tm+mt
source-wordcount: '907'
ht-degree: 32%

---

# Adobe Experience Platform 發行說明

**發行日期：2023 年 9 月 28 日**

Adobe Experience Platform中的新功能：

- [計算的屬性](#computed-attributes)

 Experience Platform 現有功能的更新：

- [警報](#alerts)
- [資料收集](#data-collection)
- [身分識別服務](#identity-service)
- [Segmentation Service](#segmentation)
- [來源](#sources)

## 計算的屬性 {#computed-attributes}

計算屬性可讓您透過直覺式UI輕鬆將事件資料摘要為設定檔屬性，以強化行為型細分、個人化和啟用。 透過此功能，您可以自助建立計算屬性、管理這些屬性，並用於區段、Real-Time CDP目的地或Adobe Journey Optimizer。 此外，計算屬性可簡化細分和歷程工作流程，協助您順暢地提供相關體驗。 若要深入瞭解計算屬性，請參閱 [計算屬性概述](../../profile/computed-attributes/overview.md).

## 警報 {#alerts}

Experience Platform可讓您訂閱各種Platform活動的事件型警報。 您可以透過以下方式訂閱不同的警報規則： [!UICONTROL 警報] 索引標籤顯示，並可選擇在UI本身或透過電子郵件通知接收警報訊息。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 警示歷史記錄標籤 | 警示 [!UICONTROL 歷史記錄] 索引標籤現在將包含所有事件，包括延遲、開始、成功和失敗。 閱讀 [警報UI檔案](../../observability/alerts/ui.md) 以取得有關「歷史記錄」標籤的詳細資訊。 |

{style="table-layout:auto"}

若要進一步瞭解警示，請閱讀 [[!DNL Observability Insights] 概述](../../observability/home.md).

## 資料收集 {#data-collection}

Adobe Experience Platform 提供了一套技術，讓您可收集用戶端客戶體驗資料並將其傳送到 Adobe Experience Platform Edge Network，在其中可擴充、轉換資料並將其分送至 Adobe 或非 Adobe 目的地。

**新功能或更新功能**

| 類型 | 功能 | 說明 |
| --- | --- | --- |
| 資料流 | 裝置查詢支援 | 設定資料流時，您現在可以選取要收集的裝置查詢資訊層級。 裝置查詢資訊包括裝置、硬體、作業系統以及用來與頁面互動的瀏覽器的相關資料。 <br>  裝置查詢資訊無法與使用者代理程式和使用者端提示一起收集。 選擇收集裝置資訊將會停用收集使用者代理程式和使用者端提示，反之亦然。 所有裝置查詢資訊都儲存在 `xdm:device` 欄位群組。 從以下檔案瞭解更多資訊： [設定資料串流](../../datastreams/configure.md#geolocation-device-lookup). |
| 擴充功能 | [!DNL TikTok] 網站事件API擴充功能 | 此 [[!DNL TikTok] 網頁事件API](https://exchange.adobe.com/apps/ec/109834/tiktok-web-events-api) 擴充功能可讓您善用Adobe Experience Platform Edge Network中擷取的資料，並將其傳送至 [!DNL TikTok] 以伺服器端事件的形式使用 [!DNL TikTok] 網頁事件API。 |

{style="table-layout:auto"}

若要進一步瞭解資料彙集，請參閱 [資料收集概觀](../../tags/home.md).

## 身分識別服務 {#identity-service}

Adobe Experience Platform 身分識別服務透過跨裝置和系統橋接身分，為您提供客戶及其行為的全方位檢視，讓您可即時實現有影響力的個人數位體驗。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| Identity Service UI增強功能 | 在Experience Platform UI中使用改良的自訂名稱空間建立工具，以便更妥善地管理您的自訂名稱空間及其對應的身分型別。 增強的Identity Service UI提供您以下功能： <ul><li>關聯式體驗：視覺提示、清晰度，以及身分名稱空間和身分型別的關聯式。</li><li>準確性：處理錯誤的能力更強，不再有重複的身分名稱。</li><li>可發現性：從產品內對話方塊存取檔案。</li></ul> 如需詳細資訊，請閱讀以下指南： [建立自訂名稱空間](../../identity-service/namespaces.md#create-namespaces). |
| 身分識別圖譜限制的變更 | 身分圖表限制已從150個身分變更為50個身分。 將新身分擷取到完整圖表時，會刪除根據擷取時間戳記和身分型別的最舊身分。 Cookie身分型別會優先刪除。 Adobe如果您的生產沙箱包含： <ul><li>個人識別碼 (例如 CRM ID) 設定為 cookie/裝置身分識別類型的自訂命名空間。</li><li>cookie/裝置識別碼被設定為跨裝置身分識別類型的自訂命名空間。</li></ul> Adobe 工程部門將手動處理這些要求。若要了解更多資訊，請閱讀[身分識別服務資料的護欄](../../identity-service/guardrails.md)。 |

{style="table-layout:auto"}

若要進一步瞭解Identity Service，請參閱 [Identity Service總覽](../../identity-service/home.md).

## Segmentation Service {#segmentation}

[!DNL Segmentation Service] 可讓您將儲存在和個人 (例如客戶、潛在客戶、使用者或組織) 相關的 [!DNL Experience Platform] 中的資料分段為不同的對象。您可以透過區段定義或來自 [!DNL Real-Time Customer Profile] 資料的其他來源建立對象。這些對象會在 [!DNL Platform] 上集中設定及維護，並可透過任何 Adobe 解決方案輕鬆存取。

**新功能或更新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 可自訂欄 | 您現在可以使用可重新調整大小的欄來自訂對象入口網站的版面。 如需有關此功能的詳細資訊，請參閱 [分段UI指南](../../segmentation/ui/overview.md#customize). |
| 更新頻率劃分 | 您現在可以檢視組織中對象更新頻率的劃分。 如需有關此功能的詳細資訊，請參閱 [分段UI指南](../../segmentation/ui/overview.md#browse). |

若要深入瞭解來源，請參閱 [來源概觀](../../sources/home.md).

若要深入瞭解分段服務，請參閱 [Segmentation Service概述](../../segmentation/home.md).

## 來源 {#sources}

Experience Platform 可提供 RESTful API 和互動式 UI，可讓您輕鬆為各種資料提供者設定來源連線。這些來源連線可讓您進行驗證並連線到外部儲存系統和 CRM 服務、設定擷取執行的時間並管理資料擷取輸送量。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 的新引數 `offset` 自助式來源中的分頁（批次SDK） | 您現在可以指定 `endConditionName` 和 `endConditionValue` 使用時用於您的來源 `offset` 分頁。 這些引數可讓您指定將在下一個HTTP請求中結束分頁回圈的條件。 如需詳細資訊，請閱讀 [自助來源分頁指南（批次SDK）](../../sources/sources-sdk/config/sourcespec.md#pagination). |

{style="table-layout:auto"}

若要深入瞭解來源，請參閱 [來源概觀](../../sources/home.md).