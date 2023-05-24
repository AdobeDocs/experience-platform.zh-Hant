---
title: Adobe Experience Platform發行說明2020年1月
description: 2020年1月為Adobe Experience Platform發行的說明。
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

標準化和互操作性是其背後的關鍵概念 [!DNL Experience Platform]。 [!DNL Experience Data Model] (XDM)在Adobe的推動下，致力於標準化客戶體驗資料並定義客戶體驗管理模式。

XDM是一種公開記錄的規範，旨在提高數字型驗的威力。 它為任何與Adobe Experience Platform服務通信的應用程式提供了共同的結構和定義。 通過遵守XDM標準，所有客戶體驗資料都可以納入到一個通用的表示形式中，以更快、更整合的方式提供洞察力。 您可以從客戶操作中獲得有價值的見解，通過細分市場定義客戶受眾，並將客戶屬性用於個性化目的。

**新功能**

| 功能 | 說明 |
|--- | ---|
| 等層次的欄位的欄位類型限制 | 在將XDM欄位定義為特定類型後，任何具有相同名稱和層次結構的其他欄位都必須使用相同的欄位類型，而不管它們在中使用的類或架構欄位組。 例如，如果XDM的欄位組 [!DNL Profile] 類包含 `profile.age` 類型為&quot;integer&quot;的欄位，XDM的類似欄位組 [!DNL ExperienceEvent] 不能 `profile.age` 「字串」類型的欄位。 為了使用不同的欄位類型，該欄位必須具有與先前定義的欄位不同的層次(例如， `profile.person.age`)。 此功能旨在防止在將架構合併到聯合中時發生衝突。 雖然約束不追溯影響現有方案，但強烈建議您查看方案中的欄位類型衝突，並根據需要編輯它們。 |
| 區分大小寫的欄位驗證 | 同一級別上的自定義欄位必須具有不同的名稱，而不考慮大寫。 例如，如果添加了名為「電子郵件」的自定義欄位，則不能在名為「email」的同一級別添加另一個自定義欄位。 |

**已知問題**

* None

瞭解有關使用XDM的更多資訊 [!DNL Schema Registry] API和 [!DNL Schema Editor] 用戶介面，請閱讀 [XDM系統文檔](../../xdm/home.md)。

## [!DNL Privacy Service] {#privacy}

新的法律和組織法規授予使用者權利，讓使用者有權應要求從您的資料存放區存取或刪除其個人資料。Adobe Experience Platform [!DNL Privacy Service] 提供REST風格的API和用戶介面，幫助您管理客戶的這些資料請求。 與 [!DNL Privacy Service]，您可以提交訪問和刪除Adobe Experience Cloud應用程式中的私人或個人客戶資料的請求，以便自動遵守法律和組織隱私法規。

**新功能**

| 功能 | 說明 |
|--- | ---|
| [!DNL Privacy Service] 重新標籤 | 以前名為「 GDPR服務」已重新標籤為 [!DNL Privacy Service] 隨著服務的發展，除了GDPR外，還支援其他法規。 |
| 新API終結點 | 的基本路徑 [!DNL Privacy Service] API已從 `/data/privacy/gdpr` 至 `/data/core/privacy/jobs`。 |
| 需要新建 `regulation` 屬性 | 在中建立新作業時 [!DNL Privacy Service] API, a `regulation` 必須在請求負載中提供屬性，以指示跟蹤作業的法規。 接受的值為 `gdpr` 和 `ccpa`。 |
| 支援 [!DNL Adobe Primetime Authentication] | [!DNL Privacy Service] 現在接受訪問/刪除來自Adobe的請求 [!DNL Primetime Authentication]，使用 `primetimeAuthentication` 作為產品價值。 |
| Privacy ServiceUI增強 | 為GDPR和CCPA管理法規分開作業跟蹤頁。 新建**Regulation Type **dropdown ，用於在GDPR和CCPA的跟蹤資料之間切換。 |

**已知問題**

* None

有關 [!DNL Privacy Service]，請從閱讀 [Privacy Service概述](../../privacy-service/home.md)。

## 來源 {#sources}

Adobe Experience Platform可以從外部源接收資料，同時允許您使用 [!DNL Platform] 服務。 您可以從多種源(如Adobe應用程式、基於雲的儲存、第三方軟體和CRM系統)中接收資料。

[!DNL Experience Platform] 提供了REST風格的API和互動式UI，使您可以輕鬆地為各種資料提供程式設定源連接。 通過這些源連接，您可以驗證並連接到外部儲存系統和CRM服務，設定接收運行時間，並管理資料接收吞吐量。

**新功能**

| 功能 | 說明 |
|--- | ---|
| 支援客戶屬性資料 | UI和API支援建立流連接器以接收客戶屬性資料。 |
| 對雲儲存的其他檔案格式支援 | 從雲儲存中接收檔案現在支援符合XDM的Parfece和JSON檔案格式。 |
| 支援訪問控制權限 | Adobe Experience Platform的訪問控制框架提供了授予對資料接收中的源的訪問權限所需的權限。 根據用戶的權限級別，用戶可以查看源、管理源或完全被拒絕訪問。 |

**訪問控制權限**

| 類別 | 權限 | 說明 |
|--- | --- | ---|
| 資料擷取 | 管理源 | 訪問讀取、建立、編輯和禁用源。 |
| 資料擷取 | 查看源 | 對中可用源的只讀訪問 **[!UICONTROL 目錄]** 頁籤和經過驗證的源 **[!UICONTROL 瀏覽]** 頁籤。 |

**已知問題**

* None

有關源的詳細資訊，請參見 [源概述](../../sources/home.md)

## 目的地 {#destinations}

在 [Real-Time CDP](../../rtcdp/overview.md)，目標是與目標平台預構建的整合，這些平台可以無縫地向這些合作夥伴激活資料。

**新功能**

| 功能 | 說明 |
|--- | ---|
| 支援訪問控制權限 | Real-Time CDP的目標功能與Adobe Experience Platform訪問控制權限配合使用。 根據用戶的權限級別，您可以查看、管理和激活目標。 |

**訪問控制權限**

| 類別 | 權限 | 說明 |
|--- | --- | ---|
| 目的地 | 管理目標 | 訪問讀取、建立、編輯和禁用目標。 |
| 目的地 | 查看目標 | 對中的可用目標的只讀訪問 **[!UICONTROL 目錄]** 頁籤和已驗證的目標 **瀏覽** 頁籤。 |
| 目的地 | 激活目標 | 能夠將資料激活到目標。 此權限要求將「管理目標」或「查看目標」添加到產品配置檔案中。 |

**已知問題**

* None

查看 [目標概述](../../destinations/home.md) 的子菜單。
