---
keywords: Experience Platform；首頁；熱門主題；GDPR;gdpr;ccpa:CCPA;pdpa;PDPA;pdpa_that;PDPA_THA;lgpd;LGPD;lgpd;lgpd_bra;LGPD_BRA;
solution: Experience Platform
title: Privacy Service概述
topic-legacy: overview
description: Privacy Service可讓您在Experience Cloud資料操作中，自動遵循法律隱私權法規。
exl-id: 585f7619-5072-413b-9a62-be0ea0cd4d1b
source-git-commit: 8133804076b1c0adf2eae5b748e86a35f3186d14
workflow-type: tm+mt
source-wordcount: '1390'
ht-degree: 2%

---

# [!DNL Privacy Service] 概觀

為了提供更好的客戶體驗，您需要收集和儲存客戶的個人資料。 使用此資料時，請務必了解並尊重客戶的隱私。 新的法律和組織法規授予使用者權利，讓使用者有權應要求從您的資料存放區存取或刪除其個人資料。

Adobe Experience Platform [!DNL Privacy Service]是為應對企業管理其客戶個人資料的方式發生根本性轉變而開發的。 [!DNL Privacy Service]的核心目的是自動遵守資料隱私權法規，一旦違反這些法規，可能會導致大額罰款，並中斷您業務的資料操作。

[!DNL Privacy Service] 提供RESTful API和使用者介面，協助您管理客戶資料請求。透過[!DNL Privacy Service]，您可以提交從Adobe Experience Cloud應用程式存取和刪除個人客戶資料的請求，協助您自動遵守法律和組織隱私權法規。

## [!DNL Privacy Service]快速入門 {#getting-started}

若要使用[!DNL Privacy Service]，需要根據貴組織的隱私權要求、您從客戶收集的身分資料種類，以及將CRM系統與服務介面的最佳方式，進行幾項重要決策。

這些決定可通過以下問題進行總結：

1. **我從客戶那裡收集了哪些資訊？**
   * 若要最有效地使用[!DNL Privacy Service]，您必須詳細了解從客戶收集的資料類型，以及其中哪些資料受隱私權法規規範約束。 如需詳細資訊，請參閱[決定隱私權需求](#requirements)一節。
1. **我是否已正確標示資料？**
   * 必須正確標示資料，服務才能決定在隱私權工作期間要存取或刪除哪些欄位。 如需詳細資訊，請參閱[標籤資料](#label)上的一節。
1. **我知道要傳送哪些ID嗎 [!DNL Privacy Service]?**
   * 傳送隱私權要求時，必須提供特定Adobe應用程式專屬的個別客戶ID。 如需詳細資訊，請參閱[提供身分資料](#identity)和[提出隱私權要求](#requests)的相關章節。
1. **如何追蹤我的隱私權工作？**
   * 提出隱私權要求後，有數個選項可用來追蹤其狀態和結果。 如需詳細資訊，請參閱[監控隱私權工作](#monitor)一節。

以下各節提供有關這些重要先決條件步驟的一般指導，並提供指向進一步[!DNL Privacy Service]文檔的連結，以了解更多詳細資訊。

### 決定貴組織的隱私權要求 {#requirements}

根據您的業務性質及其運營所在的司法管轄區，您的資料操作可能受法律隱私權法規的約束。 這些法規通常會授予您的客戶請求存取您從他們收集的資料的權利，以及請求刪除該儲存資料的權利。 在整個檔案中，這些客戶對其個人資料的請求稱為「隱私權請求」。

有關[!DNL Privacy Service]管理請求的不同法律隱私權法規的詳細資訊，包括常見問題的主要術語和答案，請參閱[隱私權法規檔案](./regulations/overview.md)。

如果您的資料操作屬於任何受支援法規的權限，請查看其文檔以獲取重要資訊，例如他們為客戶提供的特定隱私權，以及履行隱私權請求的合規性窗口。 在決定如何將[!DNL Privacy Service]整合至您的CRM系統，以及客戶應如何與您的網站互動以提出隱私權要求時，應考量這些資訊。

除了法律法規外，在做出這些決定時，還應考慮適用於貴組織的任何組織或行業標準。

### 為隱私權要求加上標籤資料 {#label}

根據您使用的[!DNL Experience Cloud]應用程式，您必須標籤應根據隱私權要求存取或刪除的特定資料欄位。 標籤資料的過程因應用程式而異。 若要了解如何為每個支援的Adobe應用程式標籤資料，請參閱[Experience Cloud應用程式](./experience-cloud-apps.md)上的文檔。

### 確定要發送到[!DNL Privacy Service]的身份資料類型 {#identity}

為了讓[!DNL Privacy Service]處理來自客戶的隱私權請求，請求本身必須提供該客戶的至少一個唯一身分值。 唯一身分值是可用於識別[!DNL Experience Cloud]資料儲存區中個人及其儲存的個人資料的任何資訊。 [!DNL Privacy Service] 會根據請求的性質（存取、刪除或選擇退出），使用此身分資訊來尋找和處理客戶的個人資料。

根據您的CRM系統使用的[!DNL Experience Cloud]應用程式，您必須為每個客戶提供的標識值的類型和數量將有所不同。 有些應用程式會使用其自己的內部客戶ID值(例如Adobe Target ID)，而其他解決方案則仰賴Adobe[!DNL Experience Cloud Identity Service](ECID)中的全域識別碼，以追蹤所有[!DNL Experience Cloud]應用程式中的客戶活動。 此外，一般個人資訊（例如電子郵件地址或電話號碼）也可作為有效的身分資料。

有關隱私權請求[身份資料的文檔](./identity-data.md)提供了有關[!DNL Privacy Service]接受的身份資訊類型的更詳細資訊。 本檔案也提供如何運用Adobe技術，在客戶與您的網站互動時，從他們有效擷取適當的身分資訊，並在API要求中將該資料傳送至[!DNL Privacy Service]的指引。

### 開始提出隱私權要求 {#requests}

在您決定了企業的隱私權需求，並決定要傳送至[!DNL Privacy Service]的身分值後，就可以開始提出隱私權要求。 [!DNL Privacy Service] 可讓您透過API或UI傳送隱私權要求。

>[!IMPORTANT]
>
>以下各節提供檔案的連結，說明如何在API或UI中提出一般隱私權要求。 不過，根據您使用的[!DNL Experience Cloud]應用程式，您在請求裝載中必須傳送的欄位可能與這些指南中顯示的範例不同。
>
>隨著您遵循API或UI指南，請參閱[Privacy Service和Experience Cloud應用程式](./experience-cloud-apps.md)上的檔案，以取得如何設定特定[!DNL Experience Cloud]應用程式隱私權要求的格式的進一步檔案。
>
>同時請務必注意，隱私權要求會在Experience Cloud應用程式間以非同步方式處理。 Privacy Service收到請求後，每個應用程式可能需要幾分鐘到幾週的時間才能完成請求。 完成每個請求所花的時間取決於您使用的應用程式，以及需要處理的資料量。

#### 使用 API

[[!DNL Privacy Service API]](https://www.adobe.io/experience-platform-apis/references/privacy-service/)提供了使用RESTful API呼叫建立和管理隱私權作業的多個端點，允許您以程式設計方式處理[!DNL Experience Cloud]應用程式的隱私權法規遵循。 如需如何使用API的詳細步驟，請參閱[Privacy ServiceAPI開發人員指南](api/getting-started.md)。

#### 使用UI

>[!NOTE]
>
>[!DNL Privacy Service] UI目前僅支援存取和刪除請求。 所有選擇退出請求都必須改為透過API提出。

[!DNL Privacy Service] UI可讓您使用圖形介面來建立和監控隱私權作業。 UI包含&#x200B;**[!UICONTROL 狀態報表]**&#x200B;介面工具集，可以視覺化呈現所有作用中請求的狀態，並可讓您使用內建的&#x200B;**[!UICONTROL 請求產生器]**&#x200B;或上傳JSON檔案來建立新請求。 有關使用UI的詳細資訊，請參閱[Privacy Service使用手冊](ui/overview.md)。

### 監視隱私權作業 {#monitor}

完成隱私權工作後，您便有數個選項可監控其狀態和結果：

| 監控方法 | 說明 |
| --- | --- |
| [!DNL Privacy Service] UI | [!DNL Privacy Service] UI提供監控控制面板，可讓您檢視所有作用中請求狀態的視覺表示法。 如需詳細資訊，請參閱[Privacy Service使用手冊](ui/overview.md) 。 |
| [!DNL Privacy Service] API | 您可以使用[!DNL Privacy Service] API提供的查閱端點，以程式設計方式監控隱私權作業的狀態。 請參閱[Privacy Service開發人員指南](./api/getting-started.md) ，了解如何使用API的詳細步驟。 |
| [!DNL Privacy Events] | [!DNL Privacy Events] 運用傳送至已設定之webhook的Adobe I/O事件，以促進有效的工作請求自動化。它們會減少或消除輪詢[!DNL Privacy Service] API的需求，以檢查工作是否完成，或工作流程中是否已達到特定里程碑。 如需詳細資訊，請參閱[訂閱隱私權事件](./privacy-events.md)的教學課程。 |

## 後續步驟

本檔案提供[!DNL Privacy Service]的概觀，以及開始使用服務功能所需的主要步驟。 請參閱整個概述中連結的檔案，以深入了解使用[!DNL Privacy Service]的各個層面。
