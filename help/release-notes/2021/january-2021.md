---
title: Adobe Experience Platform發行說明2021年1月
description: 2021年1月為Adobe Experience Platform發佈的說明。
doc-type: release notes
last-update: January 27, 2021
author: ens60013
exl-id: 6fb92e35-922c-47ba-8cf4-44edd92acfa1
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 5%

---

# Adobe Experience Platform 發行說明

**發行日期：2021 年 1 月 27 日**

Adobe Experience Platform 現有功能更新：

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Destinations]](#destinations)
- [[!DNL Real-Time Customer Profile]](#profile)
- [[!DNL Sources]](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] 允許資料工程師將資料映射到體驗資料模型(XDM)並驗證資料。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 規則運算式函式 | [!DNL Data Prep] 映射器現在支援基於規則運算式匹配和提取輸入欄位的一部分。 |

有關詳細資訊，請參閱 [[!DNL Data Prep] 概述](../../data-prep/home.md)。

## 目的地 {#destinations}

[!DNL Destinations] 是預先構建的與目標平台的整合，允許無縫激活來自Adobe Experience Platform的資料。 您可以使用目標來激活跨渠道市場營銷活動、電子郵件活動、目標廣告和許多其他使用案例的已知和未知資料。

**新目標**

| 目的地 | 說明 |
| ----------- | ----------- |
| [!DNL Azure Blob] | [!DNL Azure Blob] 是Microsoft的雲對象儲存解決方案。 |

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 高級ID匹配 | 增強中的受眾匹配率功能 [!DNL Facebook Custom Audiences] 和 [!DNL Google Customer Match]，通過添加對其他身份匹配的支援，如外部ID、電話號碼和移動設備ID。 有關詳細資訊，請參閱以下文檔： <ul><li>[Facebook](../../destinations/catalog/social/facebook.md)</li><li>[Google客戶匹配目標](../../destinations/catalog/advertising/google-customer-match.md)</li><li>[將受眾資料激活到流段導出目標](../../destinations/ui/activate-segment-streaming-destinations.md)</li></ul> |

要瞭解更多資訊，請訪問 [目標概述](../../destinations/home.md)。

## 即時客戶設定檔 {#profile}

Adobe Experience Platform使您能夠為您的客戶提供協調、一致和相關的體驗，無論客戶在何處或何時與您的品牌進行交互。 使用即時客戶配置檔案，您可以看到每個客戶的整體視圖，該視圖將來自多個渠道的資料組合在一起，包括線上、離線、CRM和第三方資料。 [!DNL Profile] 允許您將客戶資料整合到一個統一視圖中，為每次客戶交互提供一個可操作且時間戳記的帳戶。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 從配置檔案儲存中刪除資料集 | 從Experience Platform資料湖中刪除資料集時，也會自動從配置檔案儲存中刪除該資料集。 您不再需要使用配置檔案系統作業API終結點來發出刪除請求以從配置檔案儲存中顯式刪除資料集。 有關詳細資訊，請參見 [配置檔案系統作業API終結點指南](../../profile/api/profile-system-jobs.md)。 |
| 給定段的估計ID命名空間計數 | 對於估計的配置檔案計數，預覽API現在報告：<ul><li>給定命名空間的段中估計配置檔案的總數。</li><li>給定命名空間的配置檔案聯合架構中估計的配置檔案總數。</li></ul>要瞭解更多資訊，請參閱 [配置檔案預覽API終結點指南](../../profile/api/preview-sample-status.md)。 |

有關即時客戶概要資訊的詳細資訊，包括有關使用的教程和最佳做法 [!DNL Profile] 資料，請從讀取 [即時客戶概要資訊概述](../../profile/home.md)。

## [!DNL Sources] {#sources}

Adobe Experience Platform可以從外部源接收資料，同時允許您使用平台服務來構建、標籤和增強資料。 您可以從多種源(如Adobe應用程式、基於雲的儲存、第三方軟體和CRM系統)中接收資料。

Experience Platform提供REST風格的API和互動式UI，讓您能夠輕鬆地為各種資料提供程式設定源連接。 通過這些源連接，您可以驗證並連接到外部儲存系統和CRM服務，設定接收運行時間，並管理資料接收吞吐量。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| Adobe Audience Manager源連接器增強 | 現在，您可以篩選和選擇從Audience Manager到接收到平台的單個第一方段，並篩選出第一方特徵。 請參閱上的教程 [建立Audience Manager源連接器](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md) 的子菜單。 |
| [!DNL Google BigQuery] 源連接器增強 | 現在，您可以使用 [!DNL BigQuery] 源連接器。 查看 [[!DNL BigQuery] 源連接器概述](../../sources/connectors/databases/bigquery.md) 的子菜單。 |
| 支援雲儲存的複雜資料類型 | 使用雲儲存源連接器時，現在可以接收複雜的資料類型，如JSON檔案中的陣列。 請參閱有關建立雲儲存資料流的教程 [在UI中](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) 或 [使用 [!DNL Flow Service] API](../../sources/tutorials/api/collect/cloud-storage.md) 的子菜單。 |
| 支援基於服務主體密鑰的身份驗證 [!DNL Microsoft Dynamics] 源 | 您現在可以通過身份驗證 [!DNL Dynamics] 使用服務主體密鑰作為基於密碼的身份驗證的替代方法的帳戶。 查看 [[!DNL Dynamics] 源連接器概述](../../sources/connectors/crm/ms-dynamics.md) 的子菜單。 |
| 雲儲存源中自定義分隔符的UI支援 | 現在可以設定自定義列分隔符，如逗號(`,`)`\t`)或管道(`|`)，以收集UI中的分隔檔案。 請參閱上的教程 [使用雲儲存源連接器建立資料流](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) 的 |

要瞭解有關源的詳細資訊，請參閱 [源概述](../../sources/home.md)。
