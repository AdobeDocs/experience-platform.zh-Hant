---
title: Adobe Experience Platform 發行說明
description: Experience Platform發行說明2019年9月10日
doc-type: release notes
last-update: September 13, 2019
author: ens28527
translation-type: tm+mt
source-git-commit: 1b398e479137a12bcfc3208d37472aae3d6721e1
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 5%

---


# Adobe Experience Platform 發行說明

**發行日期: 2019 年 9 月 10 日**

Adobe Experience Platform現有功能的更新：

* [[!DNL資料提取]](#ingestion)
* [[!DNL資料科學工作區]](#dsw)
* [[!DNL查詢服務]](#query)

## [!DNL Data Ingestion] {#ingestion}

Adobe Experience Platform提供一組豐富的功能，可吸收任何類型的資料和延遲。 Adobe Experience Platform提供 [!DNL Data Ingestion] 多種替代方式來擷取資料，包括批次API、串流API、原生Adobe連接器、資料整合合作夥伴或Adobe Experience Platform UI。

**新功能**

| 功能 | 說明 |
| ----------- | ---------- |
| 串流擷取的新網域 | 網 `dcs.data.adobe.net` 域已移至新的公用資料收集網域 `dcs.adobedc.net`。 使用者必鬚根據修訂的Adobe Experience Platform串流擷取檔案更新其實作。 所有與Adobe Experience Platform串流擷取相關的檔案都已更新為使用新網域。 |

如需詳細資訊，請造訪「資料 [擷取」檔案](../../ingestion/home.md)。

## [!DNL Data Science Workspace] {#dsw}

Adobe Experience Platform是一 [!DNL Data Science Workspace] 項全面管理的服務，可讓資料科學家透過建立 [!DNL Experience Platform] 並執行機器學習模型，從Adobe解決方案和協力廠商系統的資料和內容順暢地產生見解。 [!DNL Data Science Workspace] 與端對端資 [!DNL Platform] 料科學生命週期緊密整合，並推動端對端資料科學生命週期，包括探索和準備XDM資料，然後開發和運作模型，以自動豐富機器學習 [!DNL Real-time Customer Profile] 見解。

**新功能**

| 功能 | 說明 |
| -----------| ---------- |
| 透過UI排程服務 | 與協調服 [!DNL Platform] 務整合，使用UI使用使用者定義的排程，將模型訓練和計分自動化。 |
| [!DNL Service Gallery] | 瀏覽、監控和存取機器學習服務，並可排程自動化訓練和計分工作，全都在重新設計的功能中完成 [!DNL Service Gallery]。 |
| [!DNL JupyterLab] 5.0.0 | [!DNL JupyterLab] UI改進。 |

**已知問題**

* 刪除現有服務目前沒有 [!DNL Service Gallery] 可存取的方式。 同時，請參閱 [Sensei Machine Learning API參考](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) ，透過API呼叫刪除現有服務。
* 不 [!DNL Service Gallery] 支援分頁以篩選服務的訓練和計分執行。
* 在設定已排程的訓練或計分時， [!DNL Service Gallery]將頻率設為每小時，以防止套用排程。

如需詳細資訊，請造訪資 [料科學工作區概觀](../../data-science-workspace/home.md)。

## [!DNL Query Service] {#query}

[!DNL Query Service] 提供使用標準SQL在Adobe Experience Platform中查詢資料的能力，以支援各種分析和資料管理使用案例。 It is a serverless tool that allows you to join datasets from the [!DNL Data Lake] and capture the query results as a new dataset for use in reporting, [!DNL Data Science Workspace], or for ingestion into [!DNL Real-time Customer Profile].

You can use [!DNL Query Service] to build data analysis ecosystems, creating a picture of customers across their various interaction channels. 這些通道可能包括銷售點系統、網路、行動或CRM系統。

**新功能**

| 功能 | 說明 |
| -----------| ---------- |
| 改進功能： [!DNL Query Editor] | 已新增儲存函式，可讓您儲存查詢，並稍後再處理。 新增「瀏覽」標籤至Adobe Experience Platform上 [!DNL Query Service] 的使用者介面，以顯示您組織中使用者儲存的查詢。 實作「查詢詳細資料」面板，顯示有關所檢視之查詢的有用中繼資料。 |
| 新的歸因功能 | Adobe定義的函式， [!DNL Query Service] 以使用過期參數來查詢渠道歸因。 |
| SQL語法的增強功能 | 支援iLike語法。 |
| 使用定義的XDM模式生成資料集 | 在Create Table as Select(CTAS)查詢中添加了新子句，該子句允許您指定目標方案。 |

For more information, refer to the [Query Service documentation](../../query-service/home.md).