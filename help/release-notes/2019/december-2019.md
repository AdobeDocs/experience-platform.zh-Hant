---
title: Adobe Experience Platform發行說明2019年12月
description: 2019年12月Adobe Experience Platform發行說明。
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

Adobe Experience Platform劃分服務提供使用者介面和RESTful API，可讓您建立區段，並從 [!DNL Real-Time Customer Profile] 資料。 這些區段是在 [!DNL Platform]，讓任何Adobe應用程式都能輕鬆存取。

[!DNL Segmentation Service] 會透過說明區分客戶群中可行銷人員群組的條件，來定義特定設定檔子集。 區段可以根據記錄資料（例如人口統計資訊）或代表客戶與您品牌互動的時間序列事件。

**新功能**

| 功能 | 說明 |
|--- | ---|
| 中的「合併對象」索引標籤 [!DNL Segment Builder] | 此 [!UICONTROL 區段] 和 [!UICONTROL 對象] 標籤 [!DNL Segment Builder] 合併成一個 [!UICONTROL 對象] 標籤。 此索引標籤可讓您瀏覽和搜尋現有對象，然後將其拖放至規則產生器畫布以建立新區段定義。 參考對象可將下列其中一組規則邏輯新增至新區段定義：對象成員資格作為規則，是定義所參考對象的完整規則邏輯集。 |
| 合併策略選擇器的新位置 | 合併策略選擇器在 [!DNL Segment Builder] 已變更。 若要為區段定義選取合併原則，請選取 **[!UICONTROL 欄位]** 標籤，然後使用 **[!UICONTROL 合併策略]** 下拉式功能表，選取您要使用的合併原則。 |

**已知問題**

* None

如需詳細資訊，請參閱 [區段服務概觀](../../segmentation/home.md).

## [!DNL Decisioning Service] {#decisioning}

Adobe Experience Platform [!DNL Decisioning Service] 提供以程式設計方式智慧地從指定個人的一組可用選項中選取「下一個最佳體驗」、將其傳遞至任何通道或應用程式，以及執行報告和分析的功能。

**新功能**

| 功能 | 說明 |
| -----------| ---------- |
| 排名函式 | 設定檔的選件順序現在是透過排名函式衍生，而非所有設定檔的一組固定選件。 |

**已知問題**

* None.

## [!DNL Sources] {#sources}

Adobe Experience Platform可以內嵌來自外部來源的資料，同時允許您使用 [!DNL Platform] 服務。 您可以內嵌來自各種來源的資料，例如Adobe解決方案、雲端儲存、協力廠商軟體和您的CRM系統。

[!DNL Experience Platform] 提供RESTful API和互動式UI，讓您輕鬆為各種資料提供者設定來源連線。 這些源連接允許您對儲存系統和CRM服務進行身份驗證、設定獲取運行的時間，以及管理資料獲取吞吐量。

**新功能**

| 功能 | 說明 |
| ---------- | ------------ |
| 串流連線 | 串流內嵌可讓您將用戶端和伺服器端裝置的資料傳送至 [!DNL Experience Platform] 即時。 版本包含新的串流連線使用者介面。 |
| 用於的連接器支撐 [!DNL Google Cloud Store] | 支援從 [!DNL Google Cloud Store]. |

**已知問題**

* None.

如需來源的詳細資訊，請參閱 [來源概觀](../../sources/home.md).

## [!DNL Experience Data Model] (XDM)系統 {#xdm}

標準化和互操作性是背後的關鍵概念 [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM)受Adobe推動，致力標準化客戶體驗資料並定義客戶體驗管理的結構。

XDM是公開記錄的規格，旨在改善數位體驗的強大功能。 它為與Adobe Experience Platform上的服務通訊的任何應用程式提供共同的結構和定義。 遵循XDM標準，所有客戶體驗資料皆可整合至以更快速、更整合的方式提供深入分析的通用表示法中。 您可以從客戶動作中獲得寶貴的深入分析、透過區段定義客戶受眾，以及將客戶屬性用於個人化目的。

**新功能**

| 功能 | 說明 |
|--- | ---|
| 改善結構驗證 | 新的檢查，以確保參照如預期解析至其他欄位。 新增其他檢查至定義為物件陣列的欄位，以確保物件已完全定義。 改善錯誤訊息，以協助識別和修正問題。 |

**錯誤修正**

* 與存取控制和沙箱相關的維護和改良。
* 支援 `eTag` 針對 `/descriptors` 端點 [!DNL Schema Registry] API。

**已知問題**

* None

若要進一步了解如何使用XDM，請使用 [!DNL Schema Registry] API和 [!DNL Schema Editor] 用戶介面，請閱讀 [XDM系統檔案](../../xdm/home.md).
