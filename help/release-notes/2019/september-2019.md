---
title: Adobe Experience Platform發行說明2019年9月
description: 2019年9月為Adobe Experience Platform發佈的說明。
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

Adobe Experience Platform提供了豐富的功能集，可接收任何類型和延遲的資料。 Adobe Experience Platform [!DNL Data Ingestion] 為接收資料提供了多種備選方案，包括批處理API、流API、本機Adobe連接器、資料整合合作夥伴或Adobe Experience PlatformUI。

**新功能**

| 功能 | 說明 |
| ----------- | ---------- |
| 用於流式接收的新域 | 的 `dcs.data.adobe.net` 域已移動到新的公用資料收集域 `dcs.adobedc.net`。 用戶必鬚根據修訂的Adobe Experience Platform流攝入文檔更新其實施。 已更新與Adobe Experience Platform流攝入相關的所有文檔，以使用新域。 |

有關詳細資訊，請訪問 [資料接收文檔](../../ingestion/home.md)。

## [!DNL Data Science Workspace] {#dsw}

Adobe Experience Platform [!DNL Data Science Workspace] 是內部的完全托管服務 [!DNL Experience Platform] 使資料科學家能夠通過構建和操作機器學習模型，跨Adobe解決方案和第三方系統無縫地從資料和內容中生成洞見。 [!DNL Data Science Workspace] 與 [!DNL Platform] 並為端到端資料科學生命週期提供動力，包括探索和準備XDM資料，然後開發和實施模型以自動豐富 [!DNL Real-Time Customer Profile] 和機器學習的見解。

**新功能**

| 功能 | 說明 |
| -----------| ---------- |
| 通過UI安排服務 | 與 [!DNL Platform] 業務流程服務，使用UI使用用戶定義的計畫自動進行模型培訓和評分。 |
| [!DNL Service Gallery] | 瀏覽、監控和訪問機器學習服務，並能夠安排自動培訓和評分作業，所有這些都在重新設計的範圍內 [!DNL Service Gallery]。 |
| [!DNL JupyterLab] 5.0.0 | [!DNL JupyterLab] UI改進。 |

**已知問題**

* 當前沒有可訪問的方式 [!DNL Service Gallery] 刪除現有服務。 同時，請參閱 [Sensei機器學習API參考](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) 通過API調用刪除現有服務。
* 的 [!DNL Service Gallery] 沒有分頁支援，無法篩選服務的培訓和評分運行。
* 配置計畫培訓或計分運行時 [!DNL Service Gallery]，將頻率設定為小時可阻止應用計畫。

有關詳細資訊，請訪問 [資料科學工作區概述](../../data-science-workspace/home.md)。

## [!DNL Query Service] {#query}

[!DNL Query Service] 提供了使用標準SQL查詢Adobe Experience Platform資料的能力，以支援各種分析和資料管理使用案例。 它是一個無伺服器工具，允許您從 [!DNL Data Lake] 並將查詢結果捕獲為新資料集以用於報告， [!DNL Data Science Workspace]或者，攝入 [!DNL Real-Time Customer Profile]。

您可以使用 [!DNL Query Service] 構建資料分析生態系統，建立客戶跨其各種交互渠道的圖景。 這些渠道可能包括銷售點系統、Web、移動或CRM系統。

**新功能**

| 功能 | 說明 |
| -----------| ---------- |
| 對 [!DNL Query Editor] | 已添加保存函式，允許您保存查詢並稍後處理該查詢。 將「瀏覽」頁籤添加到 [!DNL Query Service] 在Adobe Experience Platform上的用戶介面，顯示組織中的用戶保存的查詢。 已實現「查詢詳細資訊」面板，該面板顯示有關正在查看的查詢的有用元資料。 |
| 新屬性函式 | Adobe定義函式 [!DNL Query Service] 查詢具有到期參數的通道屬性。 |
| SQL語法的增強 | 支援iLike語法。 |
| 使用已定義的XDM架構生成資料集 | 在「將表建立為選擇」(CTAS)查詢中添加了新子句，該子句允許您指定目標方案。 |

有關詳細資訊，請參閱 [查詢服務文檔](../../query-service/home.md)。
