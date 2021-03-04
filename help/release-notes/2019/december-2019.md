---
title: Adobe Experience Platform 發行說明
description: Experience Platform發行說明2019年12月11日
doc-type: release notes
last-update: December 12, 2019
author: ens71067
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '657'
ht-degree: 7%

---


# Adobe Experience Platform 發行說明

**發行日期：2019年12月11日**

Adobe Experience Platform 現有功能更新：

* [[!DNL Segmentation Service]](#segmentation)
* [[!DNL Decisioning Service]](#decisioning)
* [[!DNL Sources]](#sources)
* [[!DNL Experience Data Model (XDM) System]](#xdm)

## [!DNL Segmentation Service] {#segmentation}

Adobe Experience Platform區段服務提供使用者介面和REST風格的API，可讓您建立區段並從您的[!DNL Real-time Customer Profile]資料產生觀眾。 這些區段是集中設定並維護在[!DNL Platform]上，讓任何Adobe應用程式都可輕鬆存取。

[!DNL Segmentation Service] 定義個人檔案的特定子集，方法是描述區分客戶群中有價人群的標準。區段可以根據記錄資料（例如人口統計資訊）或代表客戶與品牌互動的時間系列事件來劃分。

**新功能**

| 功能 | 說明 |
|--- | ---|
| [!DNL Segment Builder]中的「合併對象」標籤 | [!DNL Segment Builder]中的[!UICONTROL 區段]和[!UICONTROL 觀眾]標籤已合併為單一[!UICONTROL 觀眾]標籤。 此標籤可讓您瀏覽並搜尋現有的對象，然後拖放至規則產生器畫布以建立新的區段定義。 參考對象可將下列規則集邏輯新增至新區段定義：作為規則的對象會籍，是定義參考對象的完整規則邏輯集。 |
| 合併策略選擇器的新位置 | 合併策略選擇器在[!DNL Segment Builder]中的位置已更改。 要為段定義選擇合併策略，請在&#x200B;**[!UICONTROL 欄位]**&#x200B;頁籤上選擇齒輪表徵圖，然後使用&#x200B;**[!UICONTROL 合併策略]**&#x200B;下拉菜單來選擇要使用的合併策略。 |

**已知問題**

* None

如需詳細資訊，請參閱[分段服務概觀](../../segmentation/home.md)。

## [!DNL Decisioning Service] {#decisioning}

Adobe Experience Platform[!DNL Decisioning Service]提供以程式設計方式智慧地從一組可供特定個人使用的選項中選取「下一個最佳體驗」、將這些選項傳送至任何通道或應用程式，以及執行報告和分析的能力。

**新功能**

| 功能 | 說明 |
| -----------| ---------- |
| 排名函式 | 描述檔的選件順序現在會透過排名函式來衍生，而不是所有描述檔的固定選件集。 |

**已知問題**

* None.

## [!DNL Sources] {#sources}

Adobe Experience Platform可以從外部來源收集資料，同時允許您使用[!DNL Platform]服務來建構、標籤和增強該資料。 您可以從多種來源收集資料，例如Adobe解決方案、雲端儲存空間、協力廠商軟體和您的CRM系統。

[!DNL Experience Platform] 提供REST風格的API和互動式UI，讓您輕鬆地為各種資料提供者設定來源連線。這些源連接允許您對儲存系統和CRM服務進行身份驗證，設定接收運行的時間，並管理資料接收吞吐量。

**新功能**

| 功能 | 說明 |
| ---------- | ------------ |
| 串流連線 | 串流擷取可讓您從用戶端和伺服器端裝置即時傳送資料至[!DNL Experience Platform]。 發行包含新的串流連線使用者介面。 |
| [!DNL Google Cloud Store]的連接器支援 | 支援從[!DNL Google Cloud Store]收集資料。 |

**已知問題**

* 沒有。

如需來源的詳細資訊，請參閱[來源概觀](../../sources/home.md)。

## [!DNL Experience Data Model] (XDM)系統  {#xdm}

標準化和互操作性是[!DNL Experience Platform]背後的關鍵概念。 [!DNL Experience Data Model] (XDM)由Adobe驅動，旨在標準化客戶體驗資料並定義客戶體驗管理的架構。

XDM是公開記載的規格，旨在改善數位體驗的強大功能。 它為與Adobe Experience Platform服務通訊的任何應用程式提供共同的架構和定義。 遵循XDM標準，所有客戶體驗資料都可整合在以更快速、更整合的方式提供見解的通用表現形式中。 您可以從客戶行動中獲得寶貴見解，透過細分定義客戶受眾，並將客戶屬性用於個人化目的。

**新功能**

| 功能 | 說明 |
|--- | ---|
| 改良的架構驗證 | 新的檢查可確保參照如預期解析為其他欄位。 新增其他檢查至定義為物件陣列的欄位，以確保物件已完整定義。 已改善錯誤訊息，以協助識別和修正問題。 |

**錯誤修正**

* 存取控制與沙盒相關的維護與改進。
* 支援[!DNL Schema Registry] API中`/descriptors`端點的`eTag`。

**已知問題**

* 無

要瞭解有關使用[!DNL Schema Registry] API和[!DNL Schema Editor]用戶介面使用XDM的更多資訊，請閱讀[ XDM系統文檔](../../xdm/home.md)。