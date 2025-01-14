---
title: Adobe Experience Platform 發行說明 (2019 年 9 月)
description: Adobe Experience Platform 2019 年 9 月版發行說明。
doc-type: release notes
last-update: September 13, 2019
author: ens28527
exl-id: 7f503046-a3b4-4fdb-833c-4205b6e9fa04
source-git-commit: 863889984e5e77770638eb984e129e720b3d4458
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 8%

---

# Adobe Experience Platform 發行說明

**發行日期： 2019年9月10日**

Adobe Experience Platform 現有功能的更新：

* [[!DNL Data Ingestion]](#ingestion)
* [[!DNL Data Science Workspace]](#dsw)
* [[!DNL Query Service]](#query)

## [!DNL Data Ingestion] {#ingestion}

Adobe Experience Platform提供豐富的功能，可擷取任何型別和延遲的資料。 Adobe Experience Platform [!DNL Data Ingestion]提供多種擷取資料的替代方案，包括批次API、串流API、原生Adobe聯結器、資料整合合作夥伴或Adobe Experience Platform UI。

**新功能**

| 功能 | 說明 |
| ----------- | ---------- |
| 串流擷取的新網域 | `dcs.data.adobe.net`網域已移至新的通用資料收集網域`dcs.adobedc.net`。 使用者必須根據修訂的Adobe Experience Platform串流擷取檔案更新其實施。 所有與Adobe Experience Platform串流擷取相關的檔案都已更新，以使用新網域。 |

如需詳細資訊，請瀏覽[資料擷取檔案](../../ingestion/home.md)。

## [!DNL Data Science Workspace] {#dsw}

Adobe Experience Platform [!DNL Data Science Workspace]是[!DNL Experience Platform]中完全受管理的服務，可讓資料科學家透過建置和操作機器學習模型，順暢地從Adobe解決方案和協力廠商系統的資料和內容產生深入分析。 [!DNL Data Science Workspace]與[!DNL Platform]緊密整合，並支援端對端資料科學生命週期，包括探索和準備XDM資料，接著開發和操作模型，以使用機器學習深入分析自動豐富[!DNL Real-Time Customer Profile]。

**新功能**

| 功能 | 說明 |
| -----------| ---------- |
| 透過UI排程服務 | 已與[!DNL Platform]協調服務整合，以使用UI透過使用者定義的排程自動進行模型訓練和評分。 |
| [!DNL Service Gallery] | 瀏覽、監視和存取機器學習服務，並排程自動化訓練和評分工作，所有這些都在重新設計的[!DNL Service Gallery]內。 |
| [!DNL JupyterLab] 5.0.0 | [!DNL JupyterLab] UI改良。 |

**已知問題**

* [!DNL Service Gallery]中目前沒有刪除現有服務的存取方式。 同時，請參閱[Sensei機器學習API參考](https://developer.adobe.com/experience-platform-apis/references/sensei-machine-learning/)以透過API呼叫刪除現有服務。
* [!DNL Service Gallery]沒有分頁支援來篩選服務的訓練和評分回合。
* 當透過[!DNL Service Gallery]設定已排程的訓練或評分回合時，將頻率設定為每小時可防止套用排程。

如需詳細資訊，請造訪[資料科學Workspace概觀](../../data-science-workspace/home.md)。

## [!DNL Query Service] {#query}

[!DNL Query Service]提供在Adobe Experience Platform中使用標準SQL查詢資料的功能，以支援各種分析和資料管理使用案例。 這是一種無伺服器工具，可讓您從[!DNL Data Lake]加入資料集，並將查詢結果擷取為新資料集，以用於報表、[!DNL Data Science Workspace]或內嵌至[!DNL Real-Time Customer Profile]。

您可以使用[!DNL Query Service]來建置資料分析生態系統，進而瞭解客戶在不同互動管道中的行為。 這些管道可能包括銷售點系統、網路、行動裝置或CRM系統。

**新功能**

| 功能 | 說明 |
| -----------| ---------- |
| [!DNL Query Editor]的改善 | 新增儲存功能，可讓您儲存查詢並稍後處理。 在Adobe Experience Platform的[!DNL Query Service]使用者介面中新增「瀏覽」標籤，顯示貴組織使用者儲存的查詢。 實作「查詢詳細資訊」面板，顯示有關正在檢視的查詢的有用中繼資料。 |
| 新的歸因函式 | [!DNL Query Service]中的Adobe定義函式，以查詢具有到期引數的管道歸因。 |
| SQL語法的增強功能 | 支援iLike語法。 |
| 使用定義的XDM結構描述產生資料集 | 在「建立表格為選取」(CTAS)查詢中新增子句，可讓您指定目標綱要。 |

如需詳細資訊，請參閱[查詢服務檔案](../../query-service/home.md)。
