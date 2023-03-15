---
title: Adobe Experience Platform發行說明2020年1月
description: 2020年1月Adobe Experience Platform發行說明。
doc-type: release notes
last-update: January 15, 2020
author: crhoades, ens28527
exl-id: e488a50c-2a87-4649-b3a4-f9d45cb12fcb
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '888'
ht-degree: 9%

---

# Adobe Experience Platform 發行說明

**發行日期：2020 年 1 月 15 日**

Adobe Experience Platform 現有功能更新：

* [[!DNL Experience Data Model (XDM) System]](#xdm)
* [[!DNL Privacy Service]](#privacy)
* [[!DNL Sources]](#sources)
* [[!DNL Destinations]](#destinations)

## [!DNL Experience Data Model] (XDM)系統 {#xdm}

標準化和互操作性是背後的關鍵概念 [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM)受Adobe推動，致力標準化客戶體驗資料並定義客戶體驗管理的結構。

XDM是公開記錄的規格，旨在改善數位體驗的強大功能。 它為與Adobe Experience Platform上的服務通訊的任何應用程式提供共同的結構和定義。 遵循XDM標準，所有客戶體驗資料皆可整合至以更快速、更整合的方式提供深入分析的通用表示法中。 您可以從客戶動作中獲得寶貴的深入分析、透過區段定義客戶受眾，以及將客戶屬性用於個人化目的。

**新功能**

| 功能 | 說明 |
|--- | ---|
| 等層次結構欄位的欄位類型限制 | 將XDM欄位定義為特定類型後，任何其他名稱和階層相同的欄位都必須使用相同的欄位類型，無論其中使用的類別或架構欄位群組為何。 例如，如果XDM的欄位群組 [!DNL Profile] 類包含 `profile.age` 類型為&quot;integer&quot;的欄位，與XDM的類似欄位群組 [!DNL ExperienceEvent] 不能有 `profile.age` 「字串」類型的欄位。 若要使用不同的欄位類型，欄位必須具有與先前定義的欄位不同的階層(例如， `profile.person.age`)。 此功能的用意是在結合中結合結構時防止衝突。 雖然此限制不會回溯影響現有結構，但強烈建議您檢閱您的結構中的欄位類型衝突，並視需要加以編輯。 |
| 區分大小寫欄位驗證 | 相同層級的自訂欄位必須有不同的名稱，不論大小寫為何。 例如，如果您新增名為「Email」的自訂欄位，則無法在同一層級新增名為「email」的其他自訂欄位。 |

**已知問題**

* None

若要進一步了解如何使用XDM，請使用 [!DNL Schema Registry] API和 [!DNL Schema Editor] 用戶介面，請閱讀 [XDM系統檔案](../../xdm/home.md).

## [!DNL Privacy Service] {#privacy}

新的法律和組織法規授予使用者權利，讓使用者有權應要求從您的資料存放區存取或刪除其個人資料。Adobe Experience Platform [!DNL Privacy Service] 提供RESTful API和使用者介面，協助您管理客戶的這些資料請求。 使用 [!DNL Privacy Service]，您可以提交從Adobe Experience Cloud應用程式存取和刪除私人或個人客戶資料的請求，協助您自動遵循法律和組織隱私權法規。

**新功能**

| 功能 | 說明 |
|--- | ---|
| [!DNL Privacy Service] 品牌重塑 | 先前名為「GDPR服務」的品牌已重新命名為 [!DNL Privacy Service] 隨著服務逐漸發展，除了GDPR以外，還可支援其他法規。 |
| 新API端點 | 的基本路徑 [!DNL Privacy Service] API已從 `/data/privacy/gdpr` to `/data/core/privacy/jobs`. |
| 新增必要項目 `regulation` 屬性 | 在 [!DNL Privacy Service] API, a `regulation` 必須在要求裝載中提供屬性，以指出要追蹤工作的法規。 接受的值為 `gdpr` 和 `ccpa`. |
| 支援 [!DNL Adobe Primetime Authentication] | [!DNL Privacy Service] 現在接受來自Adobe的存取/刪除請求 [!DNL Primetime Authentication]，使用 `primetimeAuthentication` 作為其產品價值。 |
| Privacy ServiceUI增強功能 | 區隔GDPR和CCPA法規的工作追蹤頁面。 新**規則類型**下拉式清單，可切換GDPR和CCPA的追蹤資料。 |

**已知問題**

* None

如需 [!DNL Privacy Service]，請先閱讀 [Privacy Service概述](../../privacy-service/home.md).

## 來源 {#sources}

Adobe Experience Platform可以內嵌來自外部來源的資料，同時允許您使用 [!DNL Platform] 服務。 您可以從多種來源擷取資料，例如Adobe應用程式、雲端儲存、協力廠商軟體和您的CRM系統。

[!DNL Experience Platform] 提供RESTful API和互動式UI，讓您輕鬆為各種資料提供者設定來源連線。 這些源連接允許您驗證並連接到外部儲存系統和CRM服務、設定獲取運行時間以及管理資料獲取吞吐量。

**新功能**

| 功能 | 說明 |
|--- | ---|
| 支援客戶屬性資料 | 建立串流連接器以內嵌客戶屬性資料的UI和API支援。 |
| 雲端儲存空間的其他檔案格式支援 | 從雲端儲存擷取檔案現在支援符合XDM的Parquet和JSON檔案格式。 |
| 支援存取控制權限 | Adobe Experience Platform中的存取控制架構提供授與資料擷取中來源存取權所需的權限。 根據用戶的權限級別，用戶可以查看源、管理源或完全被拒絕訪問。 |

**存取控制權限**

| 類別 | 權限 | 說明 |
|--- | --- | ---|
| 資料擷取 | 管理來源 | 讀取、建立、編輯和禁用源的訪問權。 |
| 資料擷取 | 查看源 | 對 **[!UICONTROL 目錄]** 標籤和已驗證的來源(在 **[!UICONTROL 瀏覽]** 標籤。 |

**已知問題**

* None

如需來源的詳細資訊，請參閱 [來源概觀](../../sources/home.md)

## 目的地 {#destinations}

在 [Real-Time CDP](../../rtcdp/overview.md)，目的地是與目的地平台預先建立的整合，可順暢地向這些合作夥伴啟用資料。

**新功能**

| 功能 | 說明 |
|--- | ---|
| 支援存取控制權限 | Real-Time CDP中的目的地功能可與Adobe Experience Platform存取控制權限搭配使用。 您可以檢視、管理和啟用目的地，視使用者的權限層級而定。 |

**存取控制權限**

| 類別 | 權限 | 說明 |
|--- | --- | ---|
| 目的地 | 管理目的地 | 讀取、建立、編輯和停用目的地的存取權。 |
| 目的地 | 檢視目的地 | 以唯讀方式存取 **[!UICONTROL 目錄]** 標籤和已驗證的目的地 **瀏覽** 標籤。 |
| 目的地 | 啟動目的地 | 可對目的地啟用資料。 此權限需要將「管理目的地」或「檢視目的地」新增至產品設定檔。 |

**已知問題**

* None

請參閱 [目的地概觀](../../destinations/home.md) 以取得更多資訊。
