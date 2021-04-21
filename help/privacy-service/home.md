---
keywords: Experience Platform;home；熱門主題；GDPR;gdpr;ccpa:CCPA;pdpa;PDPA;pdpa_that;PDPA_THA;lgpd;LGPD;lgpd;lgpd_bra;LGPD_BRA;
solution: Experience Platform
title: Privacy Service概觀
topic-legacy: overview
description: Privacy Service可讓您在Experience Cloud資料作業中，自動符合法律隱私權法規。
exl-id: 585f7619-5072-413b-9a62-be0ea0cd4d1b
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1390'
ht-degree: 0%

---

# [!DNL Privacy Service] 概觀

為了提供更好的客戶體驗，您需要收集和儲存客戶的個人資料。 使用這些資料時，請務必瞭解並尊重客戶的隱私權。 新的法律和組織法規讓使用者有權應要求從資料存放區存取或刪除其個人資料。

Adobe Experience Platform[!DNL Privacy Service]是因應企業管理其客戶個人資料的方式發生根本性轉變而開發的。 [!DNL Privacy Service]的主要目的是自動遵守資料隱私權法規，一旦違反該法規，可能會對您的企業造成重大罰款並中斷資料運作。

[!DNL Privacy Service] 提供REST風格的API和使用者介面，協助您管理客戶資料要求。有了[!DNL Privacy Service]，您就可以提交要求，以存取和刪除Adobe Experience Cloud應用程式的個人客戶資料，以利自動符合法律和組織的隱私權規定。

## 開始使用[!DNL Privacy Service] {#getting-started}

為了使用[!DNL Privacy Service]，您必鬚根據組織的隱私權要求、您從客戶收集的身分資料種類，以及將CRM系統與服務介接的最佳方式，做出幾項關鍵決策。

這些決定可透過下列問題加以總結：

1. **我從客戶那裡收集哪些資訊？**
   * 為了充份運用[!DNL Privacy Service]，您必須詳細瞭解您從客戶收集的資料類型，以及其中哪些資料受隱私權法規的規範。 如需詳細資訊，請參閱[決定隱私權要求](#requirements)一節。
1. **我是否已正確標示資料？**
   * 必須正確標示資料，服務才能決定在隱私權工作期間要存取或刪除哪些欄位。 如需詳細資訊，請參閱[標籤資料](#label)一節。
1. **我知道要傳送哪些ID嗎 [!DNL Privacy Service]?**
   * 傳送隱私權要求時，必須提供特定Adobe應用程式的個別客戶ID。 如需詳細資訊，請參閱[提供身分資料](#identity)和[提出隱私權要求](#requests)一節。
1. **我要如何追蹤我的隱私權工作？**
   * 在您提出隱私權要求後，有幾個選項可用來追蹤其狀態和結果。 如需詳細資訊，請參閱[監控隱私權工作](#monitor)一節。

以下各節提供這些重要先決條件步驟的一般指引，並提供進一步[!DNL Privacy Service]檔案的連結，以取得詳細資訊。

### 確定組織的隱私權要求{#requirements}

根據您的業務性質及其經營所在的司法轄區，您的資料營運可能會受到法律隱私權法規的約束。 這些法規通常會賦予您的客戶要求存取您從他們收集的資料的權利，以及要求刪除該儲存資料的權利。 這些客戶對其個人資料的要求在整個檔案中稱為「隱私權要求」。

有關[!DNL Privacy Service]管理要求的不同法律隱私權法規的詳細資訊，包括常見問題的主要術語和答案，請參閱[隱私權法規檔案](./regulations/overview.md)。

如果您的資料作業屬於任何受支援法規的權限，請檢閱其檔案，以取得重要資訊，例如客戶所享有的特定隱私權，以及遵守隱私權要求的遵循窗口。 在決定如何將[!DNL Privacy Service]整合至您的CRM系統時，應考量這些資訊，以及客戶如何與您的網站互動以提出隱私權要求。

除了法律法規外，在做出這些決定時，您組織適用的任何組織或產業標準也應予以考慮。

### 隱私權要求的標籤資料{#label}

根據您使用的[!DNL Experience Cloud]應用程式，您必須標籤應根據隱私權要求而存取或刪除的特定資料欄位。 標籤資料的程式會因應用程式而異。 要瞭解如何為每個支援的Adobe應用程式標籤資料，請參閱[Experience Cloud應用程式](./experience-cloud-apps.md)上的文檔。

### 確定要發送到[!DNL Privacy Service] {#identity}的身份資料類型

為了[!DNL Privacy Service]處理來自客戶的隱私權要求，該要求本身必須提供該客戶的至少一個唯一識別值。 唯一識別值是可用於識別個人及其儲存在[!DNL Experience Cloud]資料儲存區中的個人資料的任何資訊。 [!DNL Privacy Service] 使用此身分資訊，根據要求的性質（存取、刪除或選擇退出）來尋找和處理客戶的個人資料。

根據您的CRM系統所使用的[!DNL Experience Cloud]應用程式，您必須為每個客戶提供的識別值類型和數量會有所不同。 有些應用程式會運用其內部客戶ID值(例如Adobe TargetID)，而其他解決方案則依賴於追蹤所有[!DNL Experience Cloud]應用程式之客戶活動之Adobe[!DNL Experience Cloud Identity Service](ECID)的全域識別碼。 此外，電子郵件地址或電話號碼等一般個人資訊也可當成有效的身分資料。

[隱私權要求的身分資料檔案](./identity-data.md)提供[!DNL Privacy Service]所接受之身分資訊類型的詳細資訊。 本檔案也提供如何運用Adobe技術，在客戶與您的網站互動時，有效地從他們擷取適當的身分資訊，並在API要求中將該資料傳送至[!DNL Privacy Service]的指引。

### 開始提出隱私權要求{#requests}

一旦您確定了企業的隱私權需求，並決定要傳送至[!DNL Privacy Service]的身分值，您就可以開始提出隱私權要求。 [!DNL Privacy Service] 可讓您透過API或UI傳送隱私權要求。

>[!IMPORTANT]
>
>以下各節提供說明如何在API或UI中提出一般隱私權要求的檔案連結。 不過，視您使用的[!DNL Experience Cloud]應用程式而定，您必須在請求裝載中傳送的欄位可能與這些指南中的範例不同。
>
>在遵循API或UI指南時，請參閱[Privacy Service和Experience Cloud應用程式](./experience-cloud-apps.md)上的檔案，以取得有關如何設定特定[!DNL Experience Cloud]應用程式的隱私權要求格式的詳細檔案。
>
>此外，請務必注意，隱私權要求會在Experience Cloud應用程式間以非同步方式處理。 一旦Privacy Service收到要求，每個應用程式只需幾分鐘到數週的時間，即可完成要求。 完成每個請求所需的時間取決於您使用的應用程式，以及需要處理的資料量。

#### 使用API

[[!DNL Privacy Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/privacy-service.yaml)提供數個端點，用於使用REST風格的API呼叫來建立和管理隱私權工作，讓您以程式設計方式處理[!DNL Experience Cloud]應用程式的隱私權法規遵循。 如需如何使用API的詳細步驟，請參閱[Privacy ServiceAPI開發人員指南](api/getting-started.md)。

#### 使用UI

>[!NOTE]
>
>[!DNL Privacy Service] UI目前僅支援存取和刪除請求。 所有選擇退出要求必須改為透過API提出。

[!DNL Privacy Service] UI允許您使用圖形介面建立和監視隱私作業。 UI包含&#x200B;**[!UICONTROL Status Report]**&#x200B;介面工具集，可以視覺化呈現所有作用中請求的狀態，並可讓您使用內建的&#x200B;**[!UICONTROL Request Builder]**&#x200B;或上傳JSON檔案來建立新請求。 有關使用UI的詳細資訊，請參閱[Privacy Service使用手冊](ui/overview.md)。

### 監視隱私作業{#monitor}

完成隱私權工作後，您有數個選項可用來監控其狀態和結果：

| 監控方法 | 說明 |
| --- | --- |
| [!DNL Privacy Service] UI | [!DNL Privacy Service] UI提供監控控制面板，可讓您檢視所有作用中請求狀態的視覺化表示。 如需詳細資訊，請參閱[Privacy Service使用指南](ui/overview.md)。 |
| [!DNL Privacy Service] API | 您可以使用[!DNL Privacy Service] API提供的查閱端點，以程式設計方式監控隱私權工作的狀態。 請參閱[Privacy Service開發人員指南](./api/getting-started.md)以取得如何使用API的詳細步驟。 |
| [!DNL Privacy Events] | [!DNL Privacy Events] 運用傳送至已設定網頁掛接的Adobe I/O事件，以協助有效率的工作要求自動化。它們可降低或免除輪詢[!DNL Privacy Service] API的需求，以檢查工作是否完成或工作流程中是否達到特定里程碑。 如需詳細資訊，請參閱[訂閱隱私權事件的教學課程。](./privacy-events.md) |

## 後續步驟

本檔案提供[!DNL Privacy Service]的高階概述，以及開始使用服務功能所需的主要步驟。 有關使用[!DNL Privacy Service]的各個方面的更深入資訊，請參閱整個概述中連結的文檔。
