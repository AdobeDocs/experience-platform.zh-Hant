---
title: Adobe Experience Platform發行說明2019年9月
description: 2019年9月Adobe Experience Platform發行說明。
doc-type: release notes
last-update: September 13, 2019
author: ens28527
exl-id: 7f503046-a3b4-4fdb-833c-4205b6e9fa04
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 5%

---

# Adobe Experience Platform 發行說明

**發行日期：2019 年 9 月 10 日**

Adobe Experience Platform 現有功能更新：

* [[!DNL Data Ingestion]](#ingestion)
* [[!DNL Data Science Workspace]](#dsw)
* [[!DNL Query Service]](#query)

## [!DNL Data Ingestion] {#ingestion}

Adobe Experience Platform提供一組豐富的功能，可擷取任何類型和資料延遲。 Adobe Experience Platform [!DNL Data Ingestion] 提供多種資料擷取替代選項，包括批次API、串流API、原生Adobe連接器、資料整合合作夥伴或Adobe Experience Platform UI。

**新功能**

| 功能 | 說明 |
| ----------- | ---------- |
| 串流獲取的新網域 | 此 `dcs.data.adobe.net` 網域已移至新的通用資料收集網域 `dcs.adobedc.net`. 使用者必鬚根據修訂的Adobe Experience Platform串流獲取檔案更新其實作。 已更新與Adobe Experience Platform串流擷取相關的所有檔案，以使用新網域。 |

如需詳細資訊，請造訪 [資料擷取檔案](../../ingestion/home.md).

## [!DNL Data Science Workspace] {#dsw}

Adobe Experience Platform [!DNL Data Science Workspace] 是 [!DNL Experience Platform] 這可讓資料科學家建立並運作機器學習模型，從Adobe解決方案和協力廠商系統的資料和內容無縫產生見解。 [!DNL Data Science Workspace] 緊密整合於 [!DNL Platform] 並支援端對端資料科學的生命週期，包括探索和準備XDM資料，接著開發並實施模型以自動豐富 [!DNL Real-Time Customer Profile] 以及機器學習深入分析。

**新功能**

| 功能 | 說明 |
| -----------| ---------- |
| 透過UI排程服務 | 與整合 [!DNL Platform] 協調服務，使用UI，透過使用者定義的排程自動化模型訓練和計分。 |
| [!DNL Service Gallery] | 瀏覽、監視和訪問機器學習服務，並能夠安排自動培訓和計分工作，所有這些都在重新設計的 [!DNL Service Gallery]. |
| [!DNL JupyterLab] 5.0.0 | [!DNL JupyterLab] UI改良。 |

**已知問題**

* 目前無法存取 [!DNL Service Gallery] 刪除現有服務。 同時，請參閱 [Sensei機器學習API參考](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) 若要透過API呼叫刪除現有服務。
* 此 [!DNL Service Gallery] 不支援分頁以篩選服務的訓練和分數執行。
* 設定排程訓練或分數時，會透過 [!DNL Service Gallery]，則將頻率設為每小時會防止套用排程。

如需詳細資訊，請造訪 [Data Science Workspace概述](../../data-science-workspace/home.md).

## [!DNL Query Service] {#query}

[!DNL Query Service] 提供在Adobe Experience Platform中使用標準SQL查詢資料的功能，以支援各種分析和資料管理使用案例。 這是無伺服器工具，可讓您從 [!DNL Data Lake] 並將查詢結果擷取為新資料集以用於報表， [!DNL Data Science Workspace]，或擷取至 [!DNL Real-Time Customer Profile].

您可以使用 [!DNL Query Service] 建立資料分析生態系統，建立客戶在不同互動管道中的形象。 這些管道可能包括銷售點系統、網頁、行動裝置或CRM系統。

**新功能**

| 功能 | 說明 |
| -----------| ---------- |
| 改善 [!DNL Query Editor] | 新增儲存函式，可讓您儲存查詢並稍後處理。 在 [!DNL Query Service] Adobe Experience Platform上的使用者介面，顯示組織中的使用者儲存的查詢。 實作「查詢詳細資料」面板，顯示所檢視查詢的實用中繼資料。 |
| 新的歸因函式 | Adobe定義的函式 [!DNL Query Service] 以使用過期參數查詢管道歸因。 |
| SQL語法的增強功能 | 支援iLike語法。 |
| 使用已定義的XDM結構產生資料集 | 在Create Table as Select(CTAS)查詢中新增了新子句，允許您指定目標架構。 |

如需詳細資訊，請參閱 [查詢服務檔案](../../query-service/home.md).
