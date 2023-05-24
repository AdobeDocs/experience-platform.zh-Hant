---
title: Adobe Experience Platform發行說明2020年3月
description: 2020年3月為Adobe Experience Platform發行的說明。
doc-type: release notes
last-update: March 10, 2020
author: ens71067
keywords: 發行說明;
exl-id: 407c2bac-4c8a-4939-b3dd-788250f15650
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '855'
ht-degree: 6%

---

# Adobe Experience Platform 發行說明

**發行日期：2020 年 3 月 11 日**

Adobe Experience Platform 現有功能更新：

* [資料治理](#governance)
* [[!DNL Data Ingestion]](#ingestion)
* [[!DNL Destinations]](#destinations)
* [[!DNL Identity Service]](#identity)
* [[!DNL Sources]](#sources)

## 資料治理 {#governance}

[!DNL Experience Platform] 使公司能夠將來自多個企業系統的資料整合在一起，從而更好地讓營銷人員識別、理解和接觸客戶。 [!DNL Experience Platform] 包括端到端的資料治理基礎架構，以確保正確使用 [!DNL Platform] 和系統間共用時。

Adobe Experience Platform資料治理是用於管理客戶資料和確保遵守適用於資料使用的法規、限制和策略的一系列戰略和技術。 它在 [!DNL Experience Platform] 包括編目、資料沿襲、資料使用標籤、資料存取策略和對資料的訪問控制，以執行市場營銷操作。

**新功能**

>[!NOTE]
>
>以下一些新功能當前處於測試版中，並且不適用於所有用戶。 測試版功能可能會更改。

| 功能 | 說明 |
| ------- | ----------- |
| 自動實施資料使用策略 [!DNL Real-Time Customer Data Platform] | 資料使用策略現在在將資料激活到目標的工作流中實施。 在進行影響現有激活的更改（如對資料集標籤的更改、合併策略、段定義等）時，還嵌入並強制實施資料管理。 |
| 用於強制的資料沿襲 | 在Real-Time CDP違反資料使用策略時，UI將顯示包含資料沿襲資訊的通知，以幫助用戶瞭解違反策略的原因以及他們可以採取哪些措施來解決違規。 |


**已知問題**

* None

有關資料治理的詳細資訊，請參見 [資料治理概述](../../data-governance/home.md)。

## 資料擷取 {#ingestion}

Adobe Experience Platform提供了豐富的功能集，可接收任何類型和延遲的資料。 Adobe Experience Platform [!DNL Data Ingestion] 為接收資料提供了多種備選方案，包括批處理API、流API、本機Adobe連接器、資料整合合作夥伴或Adobe Experience PlatformUI。

**新功能**

| 功能 | 說明 |
|------- | -----------|
| 部分批量攝取 | 部分批處理接收是指能夠接收包含錯誤的資料，最高可達到某個閾值。 利用此功能，用戶可以成功將其所有正確資料接收到Adobe Experience Platform，同時將其所有不正確的資料單獨進行批處理。 詳細資訊會添加到不成功的批中，以解釋它們未通過驗證的原因。 有關部分批接收的詳細資訊，請參閱 [部分批處理問題文檔](../../ingestion/batch-ingestion/partial.md)。 |

**已知問題**

* None

要瞭解有關將資料導入平台的詳細資訊，請訪問 [資料接收文檔](../../ingestion/home.md)。


## 目的地 {#destinations}

在 [Real-time Customer Data Platform](../../rtcdp/overview.md)，目標是與目標平台預構建的整合，這些平台可以無縫地向這些合作夥伴激活資料。

**新目標**

新目標可用，您可以在其中激活Adobe Experience Platform資料。 有關詳細資訊，請參閱下面：

| 目的地 | 說明 |
|--- | ---|
| 雲儲存目標 | Real-Time CDP現在可以將段作為資料檔案傳送到 [!DNL Amazon S3] 或SFTP雲儲存位置。 這使您能夠通過CSV或制表符分隔的檔案將訪問對象及其配置檔案屬性發送到內部系統。 |
| 廣告目的地 | 的 [!DNL Google] 目標卡現在分為三個目標卡，用於三個不同的目標卡 [!DNL Google] Real-Time CDP目前支援的平台： [!DNL Google Ads]。 [!DNL Google Ad Manager]。 [!DNL Google] 顯示和視頻360。 |

要瞭解更多資訊，請訪問 [目標概述](../../destinations/home.md)

## [!DNL Identity Service] {#identity}

提供相關數字型驗需要全面瞭解您的客戶。 當您的客戶資料分散在不同的系統中，導致每個客戶都顯示有多個「身份」時，這就變得更加困難了。

Adobe Experience Platform [!DNL Identity Service] 通過跨設備和系統橋接身份，幫助您更好地瞭解客戶及其行為，讓您能夠即時提供有影響的個人數字型驗。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 增強的專用圖 | 專用圖形功能已增強，以減少圖形生成延遲，從每週批處理流程到每日刷新圖形，從而允許 [!DNL Identity Service] 訪問更新的身份圖和聯繫。 |

**已知問題**

* None

有關 [!DNL Identity Service]，請參見 [Identity Service概述](../../identity-service/home.md)。

## 來源 {#sources}

Adobe Experience Platform可以從外部源接收資料，同時允許您使用 [!DNL Platform] 服務。 您可以從多種來源(如Adobe應用程式、基於雲的儲存、第三方軟體和您的CRM系統)接收資料。

[!DNL Experience Platform] 提供了REST風格的API和互動式UI，使您可以輕鬆地為各種資料提供程式設定源連接。 通過這些源連接，您可以驗證並連接到外部儲存系統和CRM服務，設定接收運行時間，並管理資料接收吞吐量。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 不建議使用的Adobe Audience Manager連接器信號 | 將不再發送來自「受眾管理器」的信號級資料。 請注意，Traits和Segments的段成員資格仍將包括在內。 由於此更改，將不再生成入站資料集。 |
| 已更名資料集 | 由Audience Manger連接器生成的資料集將具有更新的名稱和說明。 |
| 啟用 [!DNL Profile] 在「受眾管理器」中切換 | [!DNL Profile] 可以啟用或禁用切換以將資料集提升到 [!DNL Real-Time Customer Profile]。 預設情況下將啟用切換。 |
| 雲儲存系統的UI支援 | 新源連接器 [!DNL Azure Data Lake Storage Gen2] 的子菜單。 |
| CRM系統的UI支援 | 新源連接器 [!DNL HubSpot]。 [!DNL Salesforce Service Cloud], [!DNL ServiceNow] 的子菜單。 |
| 資料庫系統的UI支援 | 新源連接器 [!DNL AWS Redshift]。 [!DNL Google BigQuery]。 [!DNL MariaDB]。 [!DNL Microsoft SQL Server], [!DNL MySQL] 的子菜單。 |

**已知問題**

* None

要瞭解有關源的詳細資訊，請參閱 [源概述](../../sources/home.md)。
