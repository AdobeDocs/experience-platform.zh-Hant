---
title: Adobe Experience Platform 發行說明
description: Experience Platform發行說明2020年1月15日
doc-type: release notes
last-update: January 15, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: f881c1365684b1ca9e6bf9a8ce866d234dc54128
workflow-type: tm+mt
source-wordcount: '881'
ht-degree: 6%

---


# Adobe Experience Platform 發行說明

**發行日期：2020 年 1 月 15 日**

Adobe Experience Platform現有功能的更新：

* [!DNL Experience Data Model (XDM) System](#xdm)
* [!DNL Privacy Service](#privacy)
* [!DNL Sources](#sources)
* [!DNL Destinations](#destinations)

## [!DNL Experience Data Model] (XDM)系統 {#xdm}

標準化和互操作性是其背後的關鍵概念 [!DNL Experience Platform]。 [!DNL Experience Data Model] (XDM)是由Adobe推動，旨在標準化客戶體驗資料並定義客戶體驗管理的架構。

XDM是公開記載的規格，旨在改善數位體驗的強大功能。 它提供任何應用程式的通用結構和定義，以便與Adobe Experience Platform上的服務通訊。 遵循XDM標準，所有客戶體驗資料都可整合在以更快速、更整合的方式提供見解的通用表現形式中。 您可以從客戶行動中獲得寶貴見解，透過細分定義客戶受眾，並將客戶屬性用於個人化目的。

**新功能**

| 功能 | 說明 |
|--- | ---|
| 等等階層欄位的欄位類型限制 | 在將XDM欄位定義為特定類型後，任何具有相同名稱和層次結構的其他欄位都必須使用相同的欄位類型，而不管它們在中使用的類或混合。 例如，如果XDM類的混音包 [!DNL Profile] 含「整數」類型的欄位 `profile.age` ，則XDM的類似混 [!DNL ExperienceEvent] 音不能具 `profile.age` 有「字串」類型的欄位。 為了使用不同的欄位類型，該欄位必須具有與先前定義的欄位不同的層次(例如 `profile.person.age`)。 此功能可防止在結合中將結構描述匯整在一起時發生衝突。 雖然約束不會追溯影響現有方案，但強烈建議您複查欄位類型衝突的方案並根據需要進行編輯。 |
| 區分大小寫欄位驗證 | 相同層級的自訂欄位必須有不同的名稱，不論大小寫。 例如，如果您新增名為「電子郵件」的自訂欄位，則無法在相同層級新增名為「email」的自訂欄位。 |

**已知問題**

* 無

若要進一步瞭解如何使用 [!DNL Schema Registry] API和使用者介 [!DNL Schema Editor] 面使用XDM，請閱讀 [XDM系統檔案](../../xdm/home.md)。

## [!DNL Privacy Service] {#privacy}

新的法律和組織法規讓使用者有權應要求從資料存放區存取或刪除其個人資料。 Adobe Experience Platform提 [!DNL Privacy Service] 供REST風格的API和使用者介面，可協助您管理客戶的這些資料要求。 您可 [!DNL Privacy Service]以提交從Adobe Experience Cloud應用程式存取和刪除私人或個人客戶資料的要求，以利自動符合法律和組織的隱私權法規。

**新功能**

| 功能 | 說明 |
|--- | ---|
| [!DNL Privacy Service] 品牌再造 | 由於該服務已發展為支援除GDPR外的其他管 [!DNL Privacy Service] 理法規，原名「GDPR服務」已重新命名。 |
| 新的API端點 | API的基本路 [!DNL Privacy Service] 徑已從更新 `/data/privacy/gdpr` 為 `/data/core/privacy/jobs`。 |
| 新的必要 `regulation` 屬性 | 在 [!DNL Privacy Service] API中建立新工作時，請求裝載中必 `regulation` 須提供屬性，以指出要追蹤工作的規則。 接受的值是 `gdpr` 和 `ccpa`。 |
| 支援 [!DNL Adobe Primetime Authentication] | [!DNL Privacy Service] 現在可接受Adobe的存取／刪 [!DNL Primetime Authentication]除請求， `primetimeAuthentication` 並視其產品值而定。 |
| 隱私權服務UI增強功能 | 針對GDPR和CCPA法規分開工作追蹤頁面。 新的 _規則類型下拉式清單_ ，可在GDPR和CCPA的追蹤資料之間切換。 |

**已知問題**

* 無

如需詳細資訊， [!DNL Privacy Service]請先閱讀隱私權服務 [概觀](../../privacy-service/home.md)。

## 來源 {#sources}

Adobe Experience Platform可以從外部來源擷取資料，同時讓您使用服務來建構、標示和增強該資 [!DNL Platform] 料。 您可以從多種來源收集資料，例如Adobe應用程式、雲端儲存空間、協力廠商軟體和您的CRM系統。

[!DNL Experience Platform] 提供REST風格的API和互動式UI，讓您輕鬆地為各種資料提供者設定來源連線。 這些源連接允許您驗證並連接到外部儲存系統和CRM服務、設定接收運行的時間，以及管理資料接收吞吐量。

**新功能**

| 功能 | 說明 |
|--- | ---|
| 支援客戶屬性資料 | 建立串流連接器以收錄客戶屬性資料的UI和API支援。 |
| 雲端儲存空間的其他檔案格式支援 | 從雲端儲存區擷取檔案現在支援XDM相容的Parke和JSON檔案格式。 |
| 支援存取控制權限 | Adobe Experience Platform中的存取控制架構提供授與資料擷取來源存取權所需的權限。 根據使用者的權限層級，使用者可以檢視來源、管理來源或完全被拒絕存取。 |

**存取控制權限**

| 類別 | 權限 | 說明 |
|--- | --- | ---|
| 資料擷取 | 管理來源 | 存取讀取、建立、編輯和停用來源。 |
| 資料擷取 | 檢視來源 | 對「目錄」標籤中可用來源的唯讀存 *[!UICONTROL 取]* ，以及「瀏覽」標籤中的已驗證 *[!UICONTROL 來源]* 。 |

**已知問題**

* 無

如需來源的詳細資訊，請參閱來 [源概觀](../../sources/home.md)

## 目的地 {#destinations}

在 [Adobe Real-time CDP](../../rtcdp/overview.md)，目標是預先建立的與目標平台的整合，以順暢的方式將資料啟動給這些合作夥伴。

**新功能**

| 功能 | 說明 |
|--- | ---|
| 支援存取控制權限 | 即時CDP中的「目標」功能可與Adobe Experience Platform存取控制權限搭配使用。 視使用者的權限層級而定，您可以檢視、管理和啟用目標。 |

**存取控制權限**

| 類別 | 權限 | 說明 |
|--- | --- | ---|
| 目的地 | 管理目標 | 存取讀取、建立、編輯和停用目標。 |
| 目的地 | 查看目標 | 對「目錄」標籤中可用目標和「瀏覽」 [!UICONTROL _標籤中已驗證目標&#x200B;_]，進行唯讀_&#x200B;存取&#x200B;_。 |
| 目的地 | 啟動目標 | 能夠將資料啟動至目標。 此權限要求將「管理目標」或「檢視目標」新增至產品設定檔。 |

**已知問題**

* 無

如需詳細 [資訊，請參閱](../../rtcdp/destinations/destinations-overview.md) 「目標概觀」。