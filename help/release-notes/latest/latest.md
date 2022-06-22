---
title: Adobe Experience Platform發行說明2022年6月
description: 2022年6月為Adobe Experience Platform發佈的說明。
source-git-commit: 98b9e79fadecc6e0d5ee8e86b785fd905643f725
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 6%

---

# Adobe Experience Platform 發行說明

**發行日期：2022 年 6 月 22 日**

Adobe Experience Platform 現有功能更新：

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Destinations]](#destinations)
- [查詢服務](#query-service)
- [來源](#sources)

## [!DNL Data Science Workspace] {#dsw}

Data Science Workspace使用機器學習和人工智慧從資料中釋放洞見。 整合到Adobe Experience Platform的Data Science Workspace可幫助您跨Adobe解決方案使用內容和資料資產進行預測。 Data Science Workspace的一種實現方法是使用JupyterLab。 JupyterLab是一個基於Web的用戶介面，用於 <a href="https://jupyter.org/" target="_blank">朱佩特工程</a> 並且緊密融入Adobe Experience Platform。 它為資料科學家提供了互動式開發環境，以便他們與Jupyter筆記本、代碼和資料一起工作。

| 功能 | 說明 |
| --- | --- |
| JupyterLab啟動程式 | JupyterLab Launcher現在包括Spark 3.2筆記型電腦的啟動器。 Spark 2.4筆記型電腦啟動器現在由Spark 3.2筆記型電腦取代，並將成為此版本的一部分。 |
| 火花3.2 | 新的Scala(Spark)和PySpark配方現在使用Spark 3.2 |
| 核 | Scala(Spark)筆記本現在通過Scala內核編寫。 PySpark筆記本現在通過Python Kernel編寫。 Spark和PySpark內核已棄用，並設定為在後續版本中刪除。 |
| 食譜 | 新的PySpark和Spark配方現在遵循與Python和R配方類似的Docker工作流。 |

{style=&quot;table-layout:auto&quot;}

有關資料科學工作區的更多一般資訊，請參見 [概述文檔](../../data-science-workspace/home.md)。

## [!DNL Destinations] {#destinations}

[!DNL Destinations] 是預先構建的與目標平台的整合，允許無縫激活來自Adobe Experience Platform的資料。 您可以使用目標來激活跨渠道市場營銷活動、電子郵件活動、目標廣告和許多其他使用案例的已知和未知資料。

**新目標**

| 目的地 | 說明 |
| ----------- | ----------- |
| [[!DNL Medallia]](/help/destinations/catalog/voice/medallia-connector.md) | 激活針對Medallia調查和反饋收集的配置檔案，以便更好地瞭解客戶需求和期望。 |

{style=&quot;table-layout:auto&quot;&quot;

有關目標的更多一般資訊，請參閱 [目標概述](../../destinations/home.md)。

## 查詢服務 {#query-service}

查詢服務允許您使用標準SQL查詢Adobe Experience Platform的資料 [!DNL Data Lake]。 您可以加入來自 [!DNL Data Lake] 並將查詢結果捕獲為新資料集，用於報告、Data Science Workspace或用於接收到即時客戶概要檔案。

**已更新功能**

| 功能 | 說明 |
| --- | --- |
| 即席架構標籤 | 通過將標籤應用於通過查詢服務CTAS查詢自動生成的即席架構的資料欄位，管理對敏感資料的訪問。 您可以限制特定架構的某些欄位或資料集的使用，以控制對敏感個人資料和個人身份資訊的訪問。 通過使用基於屬性的訪問控制功能，您可以通過平台UI為ad hoc架構欄位添加標籤。 |
| `FLATTEN` 設定 | 通過第三方BI工具連接到資料庫時， `FLATTEN` 設定會將嵌套的資料結構拼合到單獨的列中，其中屬性名稱將成為保存行值的列名。 這提高了即席模式的可用性，並減少了在不支援嵌套資料結構的BI工具中檢索、分析、轉換和報告資料所需的工作量。 |

{style=&quot;table-layout:auto&quot;&quot;

有關查詢服務的詳細資訊，請參閱 [查詢服務概述](../../query-service/home.md)。

## 來源 {#sources}

Adobe Experience Platform可以從外部源接收資料，同時允許您使用平台服務來構建、標籤和增強資料。 您可以從多種來源(如Adobe應用程式、基於雲的儲存、第三方軟體和您的CRM系統)接收資料。

Experience Platform提供REST風格的API和互動式UI，讓您能夠輕鬆地為各種資料提供程式設定源連接。 通過這些源連接，您可以驗證並連接到外部儲存系統和CRM服務，設定接收運行時間，並管理資料接收吞吐量。

| 功能 | 說明 |
| --- | --- |
| Beta版 [!DNL Mixpanel] 源 | 您現在可以使用 [!DNL Mixpanel] 源：從 [!DNL Mixpanel] 帳戶到Experience Platform。 查看 [[!DNL Mixpanel] 源文檔](../../sources/connectors/analytics/mixpanel.md) 的子菜單。 |

{style=&quot;table-layout:auto&quot;&quot;

要瞭解有關源的詳細資訊，請參閱 [源概述](../../sources/home.md)。
