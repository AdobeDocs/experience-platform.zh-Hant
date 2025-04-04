---
title: Adobe Experience Platform 發行說明 (2020 年 1 月)
description: Adobe Experience Platform 2020 年 1 月版發行說明。
doc-type: release notes
last-update: January 15, 2020
author: crhoades, ens28527
exl-id: e488a50c-2a87-4649-b3a4-f9d45cb12fcb
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '890'
ht-degree: 24%

---

# Adobe Experience Platform 發行說明

**發行日期： 2020年1月15日**

Adobe Experience Platform 現有功能的更新：

* [[!DNL Experience Data Model (XDM) System]](#xdm)
* [[!DNL Privacy Service]](#privacy)
* [[!DNL Sources]](#sources)
* [[!DNL Destinations]](#destinations)

## [!DNL Experience Data Model] (XDM)系統 {#xdm}

標準化和互通性是[!DNL Experience Platform]背後的重要概念。 由Adobe驅動的[!DNL Experience Data Model] (XDM)致力於標準化客戶體驗資料並定義客戶體驗管理的結構描述。

XDM是公開記錄的規格，旨在改善數位體驗的效能。 它為任何應用程式提供通用結構和定義，以便與Adobe Experience Platform上的服務通訊。 只要遵循XDM標準，所有客戶體驗資料都能整合到共同表現中，以更快、更整合的方式提供深入分析。 您可以從客戶行為中獲得有價值的分析，透過區段定義客戶客群，並使用客戶屬性實現個人化的目的。

**新功能**

| 功能 | 說明 |
|--- | ---|
| 相同階層的欄位之欄位型別限制 | 將XDM欄位定義為特定型別後，名稱和階層相同的任何其他欄位必須使用相同的欄位型別，無論它們使用的類別或結構描述欄位群組為何。 例如，如果XDM [!DNL Profile]類別的欄位群組包含型別為「整數」的`profile.age`欄位，則XDM [!DNL ExperienceEvent]的類似欄位群組不能有型別為「字串」的`profile.age`欄位。 為了使用不同的欄位型別，該欄位必須與先前定義的欄位具有不同的階層（例如，`profile.person.age`）。 此功能旨在防止將結構描述集合在聯合時發生衝突。 雖然限制不會回溯影響現有的結構描述，但強烈建議您檢閱結構描述是否有欄位型別衝突，並視需要加以編輯。 |
| 區分大小寫的欄位驗證 | 相同層級上的自訂欄位必須有不同的名稱，無論大小寫為何。 例如，如果您新增名為「電子郵件」的自訂欄位，則無法在名為「電子郵件」的相同層級新增另一個自訂欄位。 |

**已知問題**

* None

若要進一步瞭解如何使用[!DNL Schema Registry] API和[!DNL Schema Editor]使用者介面來使用XDM，請閱讀[XDM系統檔案](../../xdm/home.md)。

## [!DNL Privacy Service] {#privacy}

新的法律和組織法規授予使用者權利，讓使用者有權應要求從您的資料存放區存取或刪除其個人資料。 Adobe Experience Platform [!DNL Privacy Service] 提供 RESTful API 和使用者介面，協助您管理這些來自客戶的資料請求。透過 [!DNL Privacy Service]，您可以提交請求來存取和刪除 Adobe Experience Cloud 應用程式中的私人或個人客戶資料，從而促進法律和組織隱私法規的自動化合規。

**新功能**

| 功能 | 說明 |
|--- | ---|
| [!DNL Privacy Service] 服務更名 | 隨著服務不斷發展以支援 GDPR 以外的其他法規，原先名為「GDPR Service」現已更名為 [!DNL Privacy Service]。 |
| 新的 API 端點 | [!DNL Privacy Service] API的基礎路徑已從`/data/privacy/gdpr`更新為`/data/core/privacy/jobs`。 |
| 新規定要提供 `regulation` 屬性 | 在 [!DNL Privacy Service] API 中建立新作業時，必須在請求承載中提供 `regulation` 屬性，以便指明是根據哪個規則追蹤該作業。接受的值為`gdpr`和`ccpa`。 |
| 支援 [!DNL Adobe Primetime Authentication] | [!DNL Privacy Service]現在接受來自Adobe [!DNL Primetime Authentication]的存取/刪除要求，使用`primetimeAuthentication`作為其產品值。 |
| Privacy Service UI增強功能 | GDPR和CCPA法規的個別工作追蹤頁面。 全新**法規型別**下拉式清單，可切換GDPR和CCPA的追蹤資料。 |

**已知問題**

* None

如需[!DNL Privacy Service]的詳細資訊，請先閱讀[Privacy Service概觀](../../privacy-service/home.md)。

## 來源 {#sources}

Adobe Experience Platform可從外部來源擷取資料，同時允許您使用[!DNL Experience Platform]服務來建構、加標籤及增強該資料。 您可以內嵌來自各種來源的資料，例如Adobe應用程式、雲端儲存、協力廠商軟體和您的CRM系統。

[!DNL Experience Platform]提供RESTful API和互動式UI，讓您輕鬆設定各種資料提供者的來源連線。 這些來源連線可讓您進行驗證並連線到外部儲存系統和 CRM 服務、設定攝取執行的時間並管理資料攝取輸送量。

**新功能**

| 功能 | 說明 |
|--- | ---|
| 支援客戶屬性資料 | 適用於建立串流聯結器以擷取客戶屬性資料的UI和API支援。 |
| 雲端儲存的其他檔案格式支援 | 從雲端儲存區擷取的檔案現在支援XDM相容的Parquet和JSON檔案格式。 |
| 支援存取控制許可權 | Adobe Experience Platform中的存取控制架構提供授予資料擷取中來源存取權所需的許可權。 根據其許可權層級，使用者可以檢視來源、管理來源或被完全拒絕存取。 |

**存取控制許可權**

| 類別 | 權限 | 說明 |
|--- | --- | ---|
| 資料攝取 | 管理來源 | 讀取、建立、編輯和停用來源的存取權。 |
| 資料攝取 | 檢視來源 | 以唯讀方式存取&#x200B;**[!UICONTROL 目錄]**&#x200B;索引標籤中的可用來源，以及&#x200B;**[!UICONTROL 瀏覽]**&#x200B;索引標籤中的已驗證來源。 |

**已知問題**

* None

如需來源的詳細資訊，請參閱[來源概觀](../../sources/home.md)

## 目標 {#destinations}

在[Real-Time CDP](../../rtcdp/overview.md)中，目的地是預先建立的與目的地平台的整合，可透過順暢的方式為這些合作夥伴啟用資料。

**新功能**

| 功能 | 說明 |
|--- | ---|
| 支援存取控制許可權 | Real-Time CDP中的目的地功能可與Adobe Experience Platform存取控制許可權搭配使用。 您可以檢視、管理和啟用目的地，實際取決於您的使用者許可權等級。 |

**存取控制許可權**

| 類別 | 權限 | 說明 |
|--- | --- | ---|
| 目標 | 管理目的地 | 讀取、建立、編輯和停用目的地的存取權。 |
| 目標 | 檢視目的地 | 以唯讀方式存取&#x200B;**[!UICONTROL 目錄]**&#x200B;索引標籤中的可用目的地，以及&#x200B;**瀏覽**&#x200B;索引標籤中的已驗證目的地。 |
| 目標 | 啟用目的地 | 啟用目的地資料的功能。 此許可權需要將「管理目的地」或「檢視目的地」新增至產品設定檔。 |

**已知問題**

* None

如需詳細資訊，請參閱[目的地概觀](../../destinations/home.md)。
