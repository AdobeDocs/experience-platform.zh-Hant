---
title: Adobe Experience Platform 發行說明
description: Experience Platform發行說明2019年9月10日
doc-type: release notes
last-update: September 13, 2019
author: ens28527
translation-type: tm+mt
source-git-commit: e5fa12b92f7006f2c5c428b25f81dade57733498

---


# Adobe Experience Platform 發行說明

**發行日期: 2019 年 9 月 10 日**

Adobe Experience Platform現有功能的更新：

* [資料擷取](#ingestion)
* [資料科學工作區](#dsw)
* [查詢服務](#query)

## 資料擷取 {#ingestion}

Adobe Experience Platform提供一組豐富的功能，可吸收任何類型的資料和延遲。 Adobe Experience Platform Data Ingestion提供多種替代方式來擷取資料，包括批次API、串流API、原生Adobe連接器、資料整合合作夥伴或Adobe Experience Platform UI。

**新功能**

| 功能 | 說明 |
| ----------- | ---------- |
| 串流擷取的新網域 | 網 `dcs.data.adobe.net` 域已移至新的公用資料收集網域 `dcs.adobedc.net`。 使用者必鬚根據修訂的Adobe Experience Platform串流擷取檔案更新其實作。 所有與Adobe Experience Platform串流擷取相關的檔案都已更新為使用新網域。 |

如需詳細資訊，請造訪「資料 [擷取」檔案](../../ingestion/home.md)。

## 資料科學工作區 {#dsw}

Adobe Experience Platform Data Science Workspace是Experience Platform內的完整管理服務，可讓資料科學家建立並執行機器學習模型，從Adobe解決方案和協力廠商系統的資料和內容順暢地產生見解。 Data Science Workspace與平台緊密整合，為端對端資料科學生命週期提供了動力，包括探索和準備XDM資料，然後開發並實施模型，以利用機器學習見解自動豐富即時客戶個人檔案。

**新功能**

| 功能 | 說明 |
| -----------| ---------- |
| 透過UI排程服務 | 與平台協調服務整合，使用使用者介面使用使用者定義的排程，將模型訓練和評分自動化。 |
| 服務庫 | 瀏覽、監視和存取機器學習服務，並可排程自動化培訓和計分工作，全都在重新設計的服務收藏館中完成。 |
| JupyterLab 5.0.0 | JupyterLab UI改進。 |

**已知問題**

* 服務收藏館中目前沒有可存取的方式來刪除現有服務。 同時，請參閱 [Sensei Machine Learning API參考](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) ，透過API呼叫刪除現有服務。
* 「服務收藏館」沒有分頁支援來篩選「服務」的訓練和計分執行。
* 在「服務收藏館」中設定已排程的訓練或計分時，將頻率設為每小時，可避免套用排程。

如需詳細資訊，請造訪資 [料科學工作區概觀](../../data-science-workspace/home.md)。

## 查詢服務 {#query}

查詢服務提供使用標準SQL來查詢Adobe Experience Platform中資料的能力，以支援各種分析和資料管理使用案例。 它是一種無伺服器工具，可讓您從Data Lake加入資料集，並將查詢結果擷取為新資料集，以用於報告、Data Science Workspace或擷取至即時客戶個人檔案。

您可以使用查詢服務來建立資料分析生態系統，以建立客戶在不同互動通道中的形象。 這些通道可能包括銷售點系統、網路、行動或CRM系統。

**新功能**

| 功能 | 說明 |
| -----------| ---------- |
| 查詢編輯器的改進 | 已新增儲存函式，可讓您儲存查詢，並稍後再處理。 新增「瀏覽」標籤至Adobe Experience Platform上的查詢服務使用者介面，以顯示由您組織中的使用者儲存的查詢。 實作「查詢詳細資料」面板，顯示有關所檢視之查詢的有用中繼資料。 |
| 新的歸因功能 | Adobe在查詢服務中定義的函式，以使用過期參數來查詢渠道歸因。 |
| SQL語法的增強功能 | 支援iLike語法。 |
| 使用定義的XDM模式生成資料集 | 在Create Table as Select(CTAS)查詢中添加了新子句，該子句允許您指定目標方案。 |

For more information, refer to the [Query Service documentation](../../query-service/home.md).