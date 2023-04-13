---
title: Adobe Experience Platform發行說明2021年2月
description: 2021年2月Adobe Experience Platform發行說明。
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

- [（測試版）控制面板](#dashboards)

Adobe Experience Platform 現有功能更新：

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Dataflows]](#dataflows)
- [[!DNL Destinations]](#destinations)
- [[!DNL Experience Data Model (XDM) System]](#xdm)
- [[!DNL Identity Service]](#identity)
- [[!DNL Real-Time Customer Profile]](#profile)
- [[!DNL Sources]](#sources)

## （測試版）控制面板 {#dashboards}

Adobe Experience Platform提供多個控制面板，讓您透過這些控制面板檢視有關組織資料的重要資訊，如每日快照中所擷取。

**新功能**

| 功能 | 說明 |
| --- | --- |
| 設定檔、區段、目的地和授權使用控制面板（測試版） | **注意：控制面板功能目前仍在測試中，且不適用於所有使用者。 文件和功能可能會有所變更。**<br/><br/>&#x200B;控制面板可提供組織資料的現成可用報表，並直接內建在Platform內的行銷人員工作流程中。 這些儀表板無需額外的IT支援，也無需花費時間和精力，即可通過額外的資料倉庫設計和實施導出和處理資料。 |

## [!DNL Data Science Workspace] {#dsw}

Data Science Workspace使用機器學習和人工智慧，從您的資料建立深入分析。 整合至Adobe Experience Platform的Data Science Workspace可協助您跨Adobe解決方案，使用內容和資料資產進行預測。

**新功能**

| 功能 | 說明 |
| --- | --- |
| JupyterLab EDA筆記本 | Jupyterlab現已提供探索資料分析(EDA)Python筆記型電腦。 此筆記本旨在幫助您發現資料中的模式、檢查資料的健全性，以及匯總預測模型的相關資料。 請參閱 [探索預測模型的網頁型資料](../../data-science-workspace/jupyterlab/eda-notebook.md) 以取得更多資訊。 |

如需Data Science Workspace的更一般資訊，請參閱 [Data Science Workspace概觀](../../data-science-workspace/home.md).

## [!DNL Dataflows] {#dataflows}

在Adobe Experience Platform中，資料會從多種來源擷取、在Experience Platform內分析，並啟動至多種目的地。 Platform借由提供資料流的透明度，讓追蹤此潛在非線性資料流的程式更輕鬆。

資料流能呈現資料處理作業在平台上移動資料的情形。這些資料流是在不同服務間配置的，有助於將資料從源連接器移動到目標資料集，然後由資料集使用 [!DNL Identity Service] 和 [!DNL Real-Time Customer Profile] 最終啟動至 [!DNL Destinations].

**新功能**

| 功能 | 說明 |
| --- | --- |
| 新的監控控制面板 | 您現在可以使用監控控制面板來提高跨服務的透明度，並為來源資料擷取提供可操作的深入分析。 新的監控控制面板提供從 [!DNL Data Lake] to [!DNL Identity Service] 和 [!DNL Profile]，同時也可讓您監控擷取率、成功和失敗。 請參閱 [監視UI中的源資料流](../../dataflows/ui/monitor-sources.md) 以取得更多資訊。 |

有關資料流的更一般資訊，請參閱 [資料流概述](../../dataflows/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] 預先建置與目的地平台的整合，可順暢地從Adobe Experience Platform啟動資料。 您可以使用目的地來針對跨通路行銷活動、電子郵件行銷活動、目標廣告和其他許多使用案例，啟用已知和未知的資料。

**新目的地**

| 目的地 | 說明 |
| ----------- | ----------- |
| [[!DNL LinkedIn Matched Audiences]](../../destinations/catalog/social/linkedin.md) | 此 [!DNL LinkedIn Matched Audiences] 連線可讓您在 [!DNL LinkedIn] 社交平台。 |

如需目的地的詳細一般資訊，請參閱 [目的地概述](../../destinations/home.md).

## [!DNL Experience Data Model (XDM) System] {#xdm}

標準化和互操作性是背後的關鍵概念 [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM)受Adobe推動，致力標準化客戶體驗資料並定義客戶體驗管理的結構。

XDM是公開記錄的規格，旨在改善數位體驗的強大功能。 它為與Adobe Experience Platform上的服務通訊的任何應用程式提供共同的結構和定義。 遵循XDM標準，所有客戶體驗資料皆可整合至以更快速、更整合的方式提供深入分析的通用表示法中。 您可以從客戶動作中獲得寶貴的深入分析、透過區段定義客戶受眾，以及將客戶屬性用於個人化目的。

**新功能**

| 功能 | 說明 |
| --- | --- |
| 升級的搜索UI | 現在， [!UICONTROL 瀏覽] 標籤 [!UICONTROL 結構] 工作區和「方案」欄位群組選取對話方塊(在 [!DNL Schema Editor].<br><br>先前搜尋詞時，結果只會包含名稱與搜尋查詢相符的XDM資源。 現在，除了名稱與查詢相符的資源外，還會包含包含符合詞語之個別屬性的資源。 這可讓您根據XDM資源所包含的屬性（而非資源名稱）來搜尋XDM資源。<br><br>請參閱 [探索XDM資源](../../xdm/ui/explore.md) 和 [管理結構](../../xdm/ui/resources/schemas.md) ，以取得詳細資訊。 |

如需XDM的更多一般資訊，請參閱 [XDM系統概觀](../../xdm/home.md).

## [!DNL Identity Service] {#identity}

要提供相關的數位體驗，必須全面了解客戶。 當您的客戶資料分散於不同的系統，導致每個個別客戶看起來都有多個「身分」時，就會更加困難。

Adobe Experience Platform [!DNL Identity Service] 可協助您跨裝置和系統橋接身分，以便即時提供具影響力的個人數位體驗，進而更全面了解客戶及其行為。

**新功能**

| 功能 | 說明 |
| --- | --- |
| 身分圖表檢視器 | 身分圖表檢視器可讓您驗證並視覺化UI中匯整在一起的身分識別，以提升除錯和透明度。 請參閱 [標識圖查看器文檔](../../identity-service/ui/identity-graph-viewer.md) 以取得更多資訊。 |

有關 [!DNL Identity Service]，請參閱 [Identity服務概述](../../identity-service/home.md).

## 即時客戶設定檔 {#profile}

Adobe Experience Platform可讓您為客戶提供協調、一致且相關的體驗，無論客戶在何處或何時與您的品牌互動。 透過即時客戶個人檔案，您可以全面了解各個客戶，其中結合來自多個管道的資料，包括線上、離線、CRM和第三方資料。 [!DNL Profile] 可讓您將客戶資料併入統一檢視中，提供每個客戶互動的可操作、時間戳記帳戶。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 計算屬性(Alpha) | ***注意：此功能目前為Alpha版，並非所有使用者都能使用。 文件和功能可能會有所變更。*** <br/><br/>計算屬性是用於將事件層級資料匯總到設定檔層級屬性的函式。 然後，您就可以在細分、啟動和個人化中使用匯總。 這些函式的某些範例包括計數、總和、平均、最小、最大、true/false。 目前僅透過API提供計算屬性。 |

如需即時客戶設定檔的詳細資訊，包括使用的教學課程和最佳實務 [!DNL Profile] 資料，請先閱讀 [即時客戶個人檔案概觀](../../profile/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform可內嵌來自外部來源的資料，同時允許您使用Platform服務來建構、加標籤及增強該資料。 您可以從多種來源擷取資料，例如Adobe應用程式、雲端儲存、協力廠商軟體和您的CRM系統。

Experience Platform提供RESTful API和互動式UI，讓您輕鬆為各種資料提供者設定來源連線。 這些源連接允許您驗證並連接到外部儲存系統和CRM服務、設定獲取運行時間以及管理資料獲取吞吐量。

**新來源**

| 功能 | 說明 |
| --- | --- |
| [!DNL Google PubSub] | 您現在可以連線 [!DNL Google PubSub] to [!DNL Experience Platform] 使用 [!DNL Flow Service] API或UI。 請參閱 [[!DNL Google PubSub] 連接器概觀](../../sources/connectors/cloud-storage/google-pubsub.md) 以取得更多資訊。 |
| [!DNL Oracle Object Storage] | 您現在可以連線 [!DNL Oracle Object Storage] to [!DNL Experience Platform] 使用 [!DNL Flow Service] API或UI。 請參閱 [[!DNL Oracle Object Storage] 連接器概觀](../../sources/connectors/cloud-storage/oracle-object-storage.md) 以取得更多資訊。 |

有關來源的更一般資訊，請參閱 [來源概觀](../../sources/home.md).
