---
title: Adobe Experience Platform 發行說明
description: 2021年2月24日的Experience Platform發行說明。
doc-type: release notes
last-update: February 24, 2021
author: ens70167
translation-type: tm+mt
source-git-commit: 7142d13b144f34d92087affe101c5ccfcb52d90e
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 6%

---


# Adobe Experience Platform 發行說明

**發行日期：2021 年 2 月 24 日**

Adobe Experience Platform 現有功能更新：

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Dataflows]](#dataflows)
- [[!DNL Experience Data Model (XDM) System]](#xdm)
- [[!DNL Identity Service]](#identity)
- [[!DNL Sources]](#sources)

## [!DNL Data Science Workspace] {#dsw}

Data Science Workspace使用機器學習和人工智慧，從您的資料中建立見解。 Data Science Workspace整合至Adobe Experience Platform，可協助您透過Adobe解決方案使用內容和資料資產進行預測。

**新功能**

| 功能 | 說明 |
| --- | --- |
| JupyterLab EDA筆記型電腦 | 探索性資料分析(EDA)Python筆記型電腦現已在Jupyterlab中提供。 本筆記型電腦旨在幫助您發現資料中的模式、檢查資料的健全性，並匯總預測模型的相關資料。 如需詳細資訊，請參閱[關於探索預測性模型的網路資料的教學課程](../../data-science-workspace/jupyterlab/eda-notebook.md)。 |

有關Data Science Workspace的更多一般資訊，請參閱[Data Science Workspace概觀](../../data-science-workspace/home.md)。

## [!DNL Dataflows] {#dataflows}

在Adobe Experience Platform中，資料會從多種來源擷取，在Experience Platform中分析，並啟動至多種目的地。 平台提供資料流透明度，讓追蹤這種可能非線性的資料流程變得更輕鬆。

資料流能呈現資料處理作業在 Platform 上移動資料的情形。這些資料流是跨不同的服務配置的，有助於將資料從源連接器移動到目標資料集，然後[!DNL Identity Service]和[!DNL Real-time Customer Profile]將其用於目標資料集，最終激活到[!DNL Destinations]。

**新功能**

| 功能 | 說明 |
| --- | --- |
| 新的監控控制面板 | 您現在可以使用監控控制面板來提供跨服務的透明度，以及來源資料擷取的可執行見解。 新的監控控制面板提供從[!DNL Data Lake]到[!DNL Identity Service]和[!DNL Profile]所處理的資料的完整檢視，同時也可讓您監控擷取率、成功和失敗。 有關詳細資訊，請參閱UI](../../dataflows/ui/monitor-sources.md)中有關[監視源資料流的教程。 |

有關資料流的更多一般資訊，請參閱[資料流概述](../../dataflows/home.md)。

## [!DNL Experience Data Model (XDM) System] {#xdm}

標準化和互操作性是[!DNL Experience Platform]背後的關鍵概念。 [!DNL Experience Data Model] (XDM)是由Adobe推動，旨在標準化客戶體驗資料並定義客戶體驗管理的架構。

XDM是公開記載的規格，旨在改善數位體驗的強大功能。 它提供任何應用程式的通用結構和定義，以便與Adobe Experience Platform上的服務通訊。 遵循XDM標準，所有客戶體驗資料都可整合在以更快速、更整合的方式提供見解的通用表現形式中。 您可以從客戶行動中獲得寶貴見解，透過細分定義客戶受眾，並將客戶屬性用於個人化目的。

**新功能**

| 功能 | 說明 |
| --- | --- |
| 升級搜尋UI | [!UICONTROL 方案]工作區的[!UICONTROL 瀏覽]標籤和[!DNL Schema Editor]的混合選擇對話方塊中現在提供改進的搜尋功能。<br><br>在先前搜尋詞語時，結果只會包含名稱與搜尋查詢相符的XDM資源。現在，除了名稱與查詢相符的資源外，還會包含包含符合詞語之個別屬性的資源。 這可讓您根據XDM資源包含的屬性來搜尋XDM資源，而非依據資源名稱。<br><br>如需詳細資訊，請 [參閱UI中](../../xdm/ui/explore.md) 的XDM資 [源和](../../xdm/ui/resources/schemas.md) 管理架構的相關檔案。 |

有關XDM的更多一般資訊，請參閱[XDM系統概述](../../xdm/home.md)。

## [!DNL Identity Service] {#identity}

要提供相關的數位體驗，必須全面瞭解客戶。 當客戶資料分散在不同的系統上時，這會更加困難，導致每個客戶看起來都有多個「身分」。

Adobe Experience Platform [!DNL Identity Service]可跨裝置和系統橋接身分，協助您更全面地瞭解客戶及其行為，讓您即時提供具影響力的個人化數位體驗。

**新功能**

| 功能 | 說明 |
| --- | --- |
| 身分圖表檢視器 | 身分圖形檢視器可讓您驗證並視覺化UI中銜接的身分識別，進而改善除錯和透明度。 如需詳細資訊，請參閱[識別圖檢視器檔案](../../identity-service/ui/identity-graph-viewer.md)。 |

有關[!DNL Identity Service]的更多一般資訊，請參閱[Identity Service概述](../../identity-service/home.md)。

## [!DNL Sources] {#sources}

Adobe Experience Platform可以從外部來源擷取資料，同時允許您使用平台服務來建構、標示和增強該資料。 您可以從多種來源收集資料，例如Adobe應用程式、雲端儲存空間、協力廠商軟體和您的CRM系統。

Experience Platform提供REST風格的API和互動式UI，讓您輕鬆為各種資料提供者設定來源連線。 這些源連接允許您驗證並連接到外部儲存系統和CRM服務、設定接收運行的時間，以及管理資料接收吞吐量。

**新來源**

| 功能 | 說明 |
| --- | --- |
| [!DNL Google PubSub] | 您現在可以使用[!DNL Flow Service] API或UI將[!DNL Google PubSub]連線至[!DNL Experience Platform]。 如需詳細資訊，請參閱[[!DNL Google PubSub] 連接器概觀](../../sources/connectors/cloud-storage/google-pubsub.md)。 |
| [!DNL Oracle Object Storage] | 您現在可以使用[!DNL Flow Service] API或UI將[!DNL Oracle Object Storage]連線至[!DNL Experience Platform]。 如需詳細資訊，請參閱[[!DNL Oracle Object Storage] 連接器概觀](../../sources/connectors/cloud-storage/oracle-object-storage.md)。 |

有關來源的更多一般資訊，請參閱[來源概述](../../sources/home.md)。
