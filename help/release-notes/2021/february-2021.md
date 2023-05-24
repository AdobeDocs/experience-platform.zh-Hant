---
title: Adobe Experience Platform發行說明2021年2月
description: 2021年2月為Adobe Experience Platform發佈的說明。
doc-type: release notes
last-update: February 24, 2021
author: ens70167
exl-id: 8c3142af-4021-4f7e-acbd-c5277dd188d1
source-git-commit: 8f61840ad60b7d24c980b218b6f742485f5ebfdd
workflow-type: tm+mt
source-wordcount: '1135'
ht-degree: 6%

---

# Adobe Experience Platform 發行說明

**發行日期：2021 年 2 月 24 日**

Adobe Experience Platform的新功能：

- [（測試版）儀表板](#dashboards)

Adobe Experience Platform 現有功能更新：

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Dataflows]](#dataflows)
- [[!DNL Destinations]](#destinations)
- [[!DNL Experience Data Model (XDM) System]](#xdm)
- [[!DNL Identity Service]](#identity)
- [[!DNL Real-Time Customer Profile]](#profile)
- [[!DNL Sources]](#sources)

## （測試版）儀表板 {#dashboards}

Adobe Experience Platform提供了多個儀表板，您可以通過這些儀表板查看有關組織資料的重要資訊，這些資訊在每日快照期間捕獲。

**新功能**

| 功能 | 說明 |
| --- | --- |
| 配置檔案、段、目標和許可證使用控制板(Beta) | **注：儀表板功能當前處於測試版中，並且不適用於所有用戶。 文件和功能可能會有所變更。**<br/><br/>&#x200B;控制面板提供有關組織資料的現成報告，並直接內置到平台內的營銷員工作流中。 這些控制板可用，無需額外的IT支援，也無需花費額外的時間和精力，通過額外的資料倉庫設計和實施來導出和處理資料。 |

## [!DNL Data Science Workspace] {#dsw}

Data Science Workspace使用機器學習和人工智慧從資料中建立洞見。 整合到Adobe Experience Platform的Data Science Workspace可幫助您跨Adobe解決方案使用內容和資料資產進行預測。

**新功能**

| 功能 | 說明 |
| --- | --- |
| JupyterLab EDA筆記本 | 探索性資料分析(EDA)Python筆記本現在在Jupyterlab上提供。 此筆記本旨在幫助您發現資料中的模式、檢查資料健全性並為預測模型匯總相關資料。 請參閱上的教程 [用於預測模型的基於Web的資料](../../data-science-workspace/jupyterlab/eda-notebook.md) 的子菜單。 |

有關Data Science Workspace的更一般資訊，請參閱 [資料科學工作區概述](../../data-science-workspace/home.md)。

## [!DNL Dataflows] {#dataflows}

在Adobe Experience Platform，資料從各種來源中攝取，在Experience Platform內分析，並激活到各種目的地。 通過向資料流提供透明性，平台使跟蹤這種潛在的非線性資料流的過程變得更容易。

資料流能呈現資料處理作業在平台上移動資料的情形。這些資料流是跨不同的服務配置的，可幫助將資料從源連接器移動到目標資料集，然後由 [!DNL Identity Service] 和 [!DNL Real-Time Customer Profile] 最終被激活 [!DNL Destinations]。

**新功能**

| 功能 | 說明 |
| --- | --- |
| 新建監視儀表板 | 現在，您可以使用監控面板來實現跨服務的透明性，並為源資料接收提供可操作的見解。 新的監控面板提供了從 [!DNL Data Lake] 至 [!DNL Identity Service] 和 [!DNL Profile]，同時還允許您監控攝入率、成功和失敗。 請參閱上的教程 [監視UI中的源資料流](../../dataflows/ui/monitor-sources.md) 的子菜單。 |

有關資料流的詳細資訊，請參閱 [資料流概述](../../dataflows/home.md)。

## [!DNL Destinations] {#destinations}

[!DNL Destinations] 是預先構建的與目標平台的整合，允許無縫激活來自Adobe Experience Platform的資料。 您可以使用目標來激活跨渠道市場營銷活動、電子郵件活動、目標廣告和許多其他使用案例的已知和未知資料。

**新目標**

| 目的地 | 說明 |
| ----------- | ----------- |
| [[!DNL LinkedIn Matched Audiences]](../../destinations/catalog/social/linkedin.md) | 的 [!DNL LinkedIn Matched Audiences] 連接允許您在 [!DNL LinkedIn] 社交平台。 |

有關目標的更多一般資訊，請參閱 [目標概述](../../destinations/home.md)。

## [!DNL Experience Data Model (XDM) System] {#xdm}

標準化和互操作性是其背後的關鍵概念 [!DNL Experience Platform]。 [!DNL Experience Data Model] (XDM)在Adobe的推動下，致力於標準化客戶體驗資料並定義客戶體驗管理模式。

XDM是一種公開記錄的規範，旨在提高數字型驗的威力。 它為任何與Adobe Experience Platform服務通信的應用程式提供了共同的結構和定義。 通過遵守XDM標準，所有客戶體驗資料都可以納入到一個通用的表示形式中，以更快、更整合的方式提供洞察力。 您可以從客戶操作中獲得有價值的見解，通過細分市場定義客戶受眾，並將客戶屬性用於個性化目的。

**新功能**

| 功能 | 說明 |
| --- | --- |
| 已升級搜索UI | 現在，在 [!UICONTROL 瀏覽] 的 [!UICONTROL 架構] 工作區和架構欄位組選擇對話框 [!DNL Schema Editor]。<br><br>在以前搜索術語時，結果將只包括名稱與搜索查詢匹配的XDM資源。 現在，除了名稱與查詢匹配的資源外，還將包括包含與術語匹配的單個屬性的資源。 這允許您根據XDM資源包含的屬性而不是按資源名稱搜索XDM資源。<br><br>查看上的文檔 [探索XDM資源](../../xdm/ui/explore.md) 和 [管理架構](../../xdm/ui/resources/schemas.md) 的子菜單。 |

有關XDM的更多一般資訊，請參閱 [XDM系統概述](../../xdm/home.md)。

## [!DNL Identity Service] {#identity}

提供相關數字型驗需要全面瞭解您的客戶。 當您的客戶資料分散在不同的系統中，導致每個客戶都顯示有多個「身份」時，這就變得更加困難了。

Adobe Experience Platform [!DNL Identity Service] 通過跨設備和系統橋接身份，幫助您更好地瞭解客戶及其行為，讓您能夠即時提供有影響的個人數字型驗。

**新功能**

| 功能 | 說明 |
| --- | --- |
| 標識圖形查看器 | 標識圖形查看器允許您驗證和可視化在UI中拼合在一起的標識，從而改進調試和透明度。 查看 [標識圖查看器文檔](../../identity-service/ui/identity-graph-viewer.md) 的子菜單。 |

有關 [!DNL Identity Service]，請參閱 [Identity Service概述](../../identity-service/home.md)。

## 即時客戶設定檔 {#profile}

Adobe Experience Platform使您能夠為您的客戶提供協調、一致和相關的體驗，無論客戶在何處或何時與您的品牌進行交互。 使用即時客戶配置檔案，您可以看到每個客戶的整體視圖，該視圖將來自多個渠道的資料組合在一起，包括線上、離線、CRM和第三方資料。 [!DNL Profile] 允許您將客戶資料整合到一個統一視圖中，為每次客戶交互提供一個可操作且時間戳記的帳戶。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 計算屬性(Alpha) | ***注：此功能當前位於Alpha中，並且不適用於所有用戶。 文件和功能可能會有所變更。*** <br/><br/>計算屬性是用於將事件級資料聚合到配置檔案級屬性中的函式。 然後，可以在分段、激活和個性化中使用聚合。 這些函式的一些示例包括count 、 sum 、 average 、 min 、 max 、 true/false。 計算屬性當前僅通過API可用。 |

有關即時客戶概要資訊的詳細資訊，包括有關使用的教程和最佳做法 [!DNL Profile] 資料，請從讀取 [即時客戶概要資訊概述](../../profile/home.md)。

## [!DNL Sources] {#sources}

Adobe Experience Platform可以從外部源接收資料，同時允許您使用平台服務來構建、標籤和增強資料。 您可以從多種源(如Adobe應用程式、基於雲的儲存、第三方軟體和CRM系統)中接收資料。

Experience Platform提供REST風格的API和互動式UI，讓您能夠輕鬆地為各種資料提供程式設定源連接。 通過這些源連接，您可以驗證並連接到外部儲存系統和CRM服務，設定接收運行時間，並管理資料接收吞吐量。

**新源**

| 功能 | 說明 |
| --- | --- |
| [!DNL Google PubSub] | 現在可以連接 [!DNL Google PubSub] 至 [!DNL Experience Platform] 使用 [!DNL Flow Service] API或UI。 查看 [[!DNL Google PubSub] 連接器概述](../../sources/connectors/cloud-storage/google-pubsub.md) 的子菜單。 |
| [!DNL Oracle Object Storage] | 現在可以連接 [!DNL Oracle Object Storage] 至 [!DNL Experience Platform] 使用 [!DNL Flow Service] API或UI。 查看 [[!DNL Oracle Object Storage] 連接器概述](../../sources/connectors/cloud-storage/oracle-object-storage.md) 的子菜單。 |

有關來源的更多一般資訊，請參閱 [源概述](../../sources/home.md)。
