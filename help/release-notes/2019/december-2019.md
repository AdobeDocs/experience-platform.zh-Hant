---
title: Adobe Experience Platform發行說明2019年12月
description: Adobe Experience Platform 2019年12月版本注意事項。
doc-type: release notes
last-update: December 12, 2019
author: ens71067
exl-id: 98d50b90-38ed-4cc2-ad48-78b712b453f7
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 15%

---

# Adobe Experience Platform 發行說明

**發行日期： 2019年12月11日**

Adobe Experience Platform 現有功能的更新：

* [[!DNL Segmentation Service]](#segmentation)
* [[!DNL Decisioning Service]](#decisioning)
* [[!DNL Sources]](#sources)
* [[!DNL Experience Data Model (XDM) System]](#xdm)

## [!DNL Segmentation Service] {#segmentation}

Adobe Experience Platform Segmentation Service提供使用者介面和RESTful API，可讓您建立區段，並從[!DNL Real-Time Customer Profile]資料產生對象。 這些區段是在[!DNL Experience Platform]上集中設定和維護，讓任何Adobe應用程式都能輕鬆存取。

[!DNL Segmentation Service] 會說明區分客戶群中可行銷的一群人的標準，從而定義輪廓的特定子集。區段的基礎可能是記錄資料 (例如人口統計資訊) 或表示客戶與您的品牌互動的時間序列事件。

**新功能**

| 功能 | 說明 |
|--- | ---|
| [!DNL Segment Builder]中的合併對象索引標籤 | [!DNL Segment Builder]中的[!UICONTROL 區段]和[!UICONTROL 對象]索引標籤已合併至單一[!UICONTROL 對象]索引標籤。 此索引標籤可讓您瀏覽及搜尋現有對象，然後將其拖放到規則產生器畫布中以建立新的區段定義。 參照對象可將下列規則邏輯集合之一新增至新的區段定義：對象成員資格如規則，定義參照對象的完整規則邏輯集合。 |
| 合併原則選擇器的新位置 | [!DNL Segment Builder]中合併原則選擇器的位置已變更。 若要選取區段定義的合併原則，請選取&#x200B;**[!UICONTROL 欄位]**&#x200B;索引標籤上的齒輪圖示，然後使用&#x200B;**[!UICONTROL 合併原則]**&#x200B;下拉式功能表選取您要使用的合併原則。 |

**已知問題**

* None

如需詳細資訊，請參閱[分段服務總覽](../../segmentation/home.md)。

## [!DNL Decisioning Service] {#decisioning}

Adobe Experience Platform [!DNL Decisioning Service]能以程式設計方式，聰明地從一組可供特定個人使用的選項中選取「下一個最佳體驗」，將其傳遞至任何管道或應用程式，以及執行報表和分析。

**新功能**

| 功能 | 說明 |
| -----------| ---------- |
| 排名函式 | 個人檔案的優惠方案順序現在透過排名函式衍生，而不是所有個人檔案中的固定優惠方案集。 |

**已知問題**

* 無。

## [!DNL Sources] {#sources}

Adobe Experience Platform可從外部來源擷取資料，同時允許您使用[!DNL Experience Platform]服務來建構、加標籤及增強該資料。 您可以從多種來源擷取資料，例如Adobe解決方案、雲端型儲存空間、協力廠商軟體和您的CRM系統。

[!DNL Experience Platform]提供RESTful API和互動式UI，讓您輕鬆設定各種資料提供者的來源連線。 這些來源連線可讓您驗證儲存系統和CRM服務、設定擷取執行時間，以及管理資料擷取輸送量。

**新功能**

| 功能 | 說明 |
| ---------- | ------------ |
| 串流連線 | 串流擷取可讓您即時從使用者端和伺服器端裝置傳送資料至[!DNL Experience Platform]。 此版本包含新的串流連線使用者介面。 |
| [!DNL Google Cloud Store]的聯結器支援 | 支援從[!DNL Google Cloud Store]收集資料。 |

**已知問題**

* 無。

如需來源的詳細資訊，請參閱[來源概觀](../../sources/home.md)。

## [!DNL Experience Data Model] (XDM)系統 {#xdm}

標準化和互通性是[!DNL Experience Platform]背後的重要概念。 由Adobe驅動的[!DNL Experience Data Model] (XDM)致力於標準化客戶體驗資料並定義客戶體驗管理的結構描述。

XDM是公開記錄的規格，旨在改善數位體驗的效能。 它為任何應用程式提供通用結構和定義，以便與Adobe Experience Platform上的服務通訊。 只要遵循XDM標準，所有客戶體驗資料都能整合到共同表現中，以更快、更整合的方式提供深入分析。 您可以從客戶行為中獲得有價值的分析，透過區段定義客戶客群，並使用客戶屬性實現個人化的目的。

**新功能**

| 功能 | 說明 |
|--- | ---|
| 改善的結構描述驗證 | 新檢查可確保參考按預期解析為其他欄位。 對定義為物件陣列的欄位新增額外檢查，以確保物件已完全定義。 改善錯誤訊息，以協助識別和修正問題。 |

**錯誤修正**

* 與存取控制和沙箱相關的維護和改善。
* 在[!DNL Schema Registry] API中支援`/descriptors`端點的`eTag`。

**已知問題**

* None

若要進一步瞭解如何使用[!DNL Schema Registry] API和[!DNL Schema Editor]使用者介面來使用XDM，請閱讀[XDM系統檔案](../../xdm/home.md)。
