---
title: Adobe Experience Platform發行說明2019年12月
description: 2019年12月發佈的Adobe Experience Platform說明。
doc-type: release notes
last-update: December 12, 2019
author: ens71067
exl-id: 98d50b90-38ed-4cc2-ad48-78b712b453f7
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '661'
ht-degree: 6%

---

# Adobe Experience Platform 發行說明

**發行日期：2019年12月11日**

Adobe Experience Platform 現有功能更新：

* [[!DNL Segmentation Service]](#segmentation)
* [[!DNL Decisioning Service]](#decisioning)
* [[!DNL Sources]](#sources)
* [[!DNL Experience Data Model (XDM) System]](#xdm)

## [!DNL Segmentation Service] {#segmentation}

Adobe Experience Platform分段服務提供用戶介面和REST風格的API，使您能夠生成分段並從您的 [!DNL Real-Time Customer Profile] 資料。 這些段在 [!DNL Platform]使任何Adobe應用程式都可輕鬆訪問。

[!DNL Segmentation Service] 通過描述區分客戶群中可銷售人員組的標準來定義特定配置檔案子集。 段可以基於記錄資料（如人口統計資訊）或表示客戶與您品牌的交互的時間序列事件。

**新功能**

| 功能 | 說明 |
|--- | ---|
| 合併的受眾頁籤 [!DNL Segment Builder] | 的 [!UICONTROL 段] 和 [!UICONTROL 觀眾] 頁籤 [!DNL Segment Builder] 被合為一個 [!UICONTROL 觀眾] 頁籤。 此頁籤允許您瀏覽和搜索現有受眾，然後可將其拖放到規則生成器畫布中，以建立新段定義。 引用訪問群體可將以下一組規則邏輯添加到新段定義中：作為規則的受眾成員資格，是定義引用的受眾的全套規則邏輯。 |
| 合併策略選擇器的新位置 | 合併策略選擇器在 [!DNL Segment Builder] 已更改。 要為段定義選擇合併策略，請在 **[!UICONTROL 欄位]** ，則使用 **[!UICONTROL 合併策略]** 下拉菜單，以選擇要使用的合併策略。 |

**已知問題**

* None

有關詳細資訊，請參閱 [分段服務概述](../../segmentation/home.md)。

## [!DNL Decisioning Service] {#decisioning}

Adobe Experience Platform [!DNL Decisioning Service] 提供了以寫程式方式智慧地從給定個人的一組可用選項中選擇「下一最佳體驗」、將它們交付到任何渠道或應用程式以及執行報告和分析的能力。

**新功能**

| 功能 | 說明 |
| -----------| ---------- |
| 排序函式 | 配置檔案的聘用順序現在通過排序函式而不是所有配置檔案的固定聘用集來導出。 |

**已知問題**

* None.

## [!DNL Sources] {#sources}

Adobe Experience Platform可以從外部源接收資料，同時允許您使用 [!DNL Platform] 服務。 您可以從多種來源(如Adobe解決方案、基於雲的儲存、第三方軟體和您的CRM系統)接收資料。

[!DNL Experience Platform] 提供了REST風格的API和互動式UI，使您可以輕鬆地為各種資料提供程式設定源連接。 通過這些源連接，您可以驗證儲存系統和CRM服務，設定接收運行時間，並管理資料接收吞吐量。

**新功能**

| 功能 | 說明 |
| ---------- | ------------ |
| 流連接 | 流式接收使您能夠將資料從客戶端和伺服器端設備發送到 [!DNL Experience Platform] 即時。 版本包括新的流連接用戶介面。 |
| 連接器支撐 [!DNL Google Cloud Store] | 支援從 [!DNL Google Cloud Store]。 |

**已知問題**

* None.

有關源的詳細資訊，請參見 [源概述](../../sources/home.md)。

## [!DNL Experience Data Model] (XDM)系統 {#xdm}

標準化和互操作性是其背後的關鍵概念 [!DNL Experience Platform]。 [!DNL Experience Data Model] (XDM)在Adobe的推動下，致力於標準化客戶體驗資料並定義客戶體驗管理模式。

XDM是一種公開記錄的規範，旨在提高數字型驗的威力。 它為任何與Adobe Experience Platform服務通信的應用程式提供了共同的結構和定義。 通過遵守XDM標準，所有客戶體驗資料都可以納入到一個通用的表示形式中，以更快、更整合的方式提供洞察力。 您可以從客戶操作中獲得有價值的見解，通過細分市場定義客戶受眾，並將客戶屬性用於個性化目的。

**新功能**

| 功能 | 說明 |
|--- | ---|
| 改進的架構驗證 | 新檢查以確保引用按預期解析到其他欄位。 向定義為對象陣列的欄位添加了其他檢查，以確保對象已完全定義。 改進了錯誤消息，以幫助識別和解決問題。 |

**錯誤修正**

* 與訪問控制和沙箱相關的維護和改進。
* 支援 `eTag` 為 `/descriptors` 端點 [!DNL Schema Registry] API。

**已知問題**

* None

瞭解有關使用XDM的更多資訊 [!DNL Schema Registry] API和 [!DNL Schema Editor] 用戶介面，請閱讀 [XDM系統文檔](../../xdm/home.md)。
