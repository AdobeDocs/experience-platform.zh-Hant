---
keywords: Experience Platform;home;popular topics;GDPR;gdpr;ccpa:CCPA
solution: Experience Platform
title: Adobe Experience Platform隱私權服務
topic: overview
translation-type: tm+mt
source-git-commit: 1b398e479137a12bcfc3208d37472aae3d6721e1
workflow-type: tm+mt
source-wordcount: '1502'
ht-degree: 2%

---


# Adobe Experience Platform [!DNL Privacy Service] overview

為了提供更好的客戶體驗，您需要收集和儲存客戶的個人資料。 使用這些資料時，請務必瞭解並尊重客戶的隱私權。 新的法律和組織法規讓使用者有權應要求從資料存放區存取或刪除其個人資料。

Adobe Experience Platform是為 [!DNL Privacy Service] 因應企業管理客戶個人資料的方式發生根本性轉變而開發的。 其核心目的是 [!DNL Privacy Service] 自動遵守資料隱私權法規，一旦違反這些法規，可能會導致重大罰款並中斷您企業的資料運作。

[!DNL Privacy Service] 提供REST風格的API和使用者介面，協助您管理客戶資料要求。 您可 [!DNL Privacy Service]以提交從Adobe Experience Cloud應用程式存取和刪除個人客戶資料的要求，以協助自動符合法律和組織的隱私權法規。

## Getting started with [!DNL Privacy Service] {#getting-started}

為了善用 [!DNL Privacy Service]，您必鬚根據組織的隱私權要求、您從客戶收集的身分資料種類，以及將CRM系統與服務介接的最佳方式，做出幾項關鍵決策。

這些決定可透過下列問題加以總結：

1. **我從客戶那裡收集哪些資訊？**
   * 為了充份運用資 [!DNL Privacy Service]訊，您必須詳細瞭解您從客戶收集的資料類型，以及其中哪些資料受隱私權法規的規範。 如需詳細資訊，請 [參閱決定隱私權](#requirements) 要求一節。
1. **我是否已正確標示資料？**
   * 必須正確標示資料，服務才能決定在隱私權工作期間要存取或刪除哪些欄位。 如需詳細資訊，請 [參閱標籤](#label) 資料一節。
1. **我知道要傳送哪些ID嗎[!DNL Privacy Service]?**
   * 傳送隱私權要求時，必須提供特定Adobe應用程式專屬的個別客戶ID。 如需詳細資訊，請 [參閱提供身分資](#identity)[料](#requests) 和提出隱私權要求的相關章節。
1. **我要如何追蹤我的隱私權工作？**
   * 在您提出隱私權要求後，有幾個選項可用來追蹤其狀態和結果。 如需詳細資訊，請 [參閱監控隱私](#monitor) 工作一節。

以下各節提供這些重要先決條件步驟的一般指引，並提供進一步說明檔案的連 [!DNL Privacy Service] 結，以取得詳細資訊。

### 確定您組織的隱私權要求 {#requirements}

根據您的業務性質及其經營所在的司法轄區，您的資料營運可能會受到法律隱私權法規的約束。 這些法規通常會賦予您的客戶要求存取您從他們收集的資料的權利，以及要求刪除該儲存資料的權利。 這些客戶對其個人資料的要求在整個檔案中稱為「隱私權要求」。

下表概述管理要求的法律隱私權規 [!DNL Privacy Service] 定，包括說明檔案的連結，以取得詳細資訊：

| 法規 | 說明 |
| --- | --- |
| CCPA（加州） | The [!DNL California Consumer Privacy Act] (CCPA) enhances privacy rights and consumer protection for residents of California, United States. CCPA為加州居民提供新的資料隱私權，包括存取和刪除其個人資料的權利，以得知其個人資料是賣給或披露（以及向誰），以及選擇不將其資料賣給第三方的權利。<br/><br/>進一步說明檔案的連結： <ul><li>[法律概觀](https://oag.ca.gov/privacy/ccpa)</li><li>[CCPA常見問答集](ccpa/faq.md)</li></ul> |
| GDPR（歐盟） | The [!DNL General Data Protection Regulation] (GDPR) introduced several new data privacy rights for members of the European Union, including the **Right to Access** and the **Right to be Forgotten**. 這表示貴公司已收集其個人資料的任何歐盟公民，都有權隨時請求存取或刪除其資料。<br/><br/>進一步說明檔案的連結： <ul><li>[法律概觀](https://gdpr-info.eu/)</li><li>[GDPR 常見問題集](gdpr/faq.md)</li><li>[GDPR 術語](gdpr/terminology.md)</li></ul> |
| PDPA_THA（泰國） | 泰國的個人資料保護法(PDPA)是為保護泰國資料擁有者不被非法收集、使用或揭露其個人資料而制定的。 受歐盟GDPR的啟發，該規定授予泰國公民要求訪問或刪除其儲存的個人資料的權利。<br/><br/>進一步說明檔案的連結： <ul><li>[法律概觀](https://www.dataprotectionreport.com/2020/02/thailand-personal-data-protection-law/)</li><li>[PDPA_THA常見問答集](pdpa-tha/faq.md)</li><li>[PDPA_THA術語](pdpa-tha/terminology.md)</li></ul> |

如果您的資料作業屬於上述任何法規的權限，請檢閱其檔案，以取得重要資訊，例如客戶所享有的特定隱私權，以及遵守隱私權要求的遵循窗口。 在決定如何整合至您的CRM系統時，應考 [!DNL Privacy Service] 慮這些資訊，以及客戶應如何與您的網站互動，以提出隱私權要求。

除了法律法規外，在做出這些決定時，您組織適用的任何組織或產業標準也應予以考慮。

### 隱私權要求的標籤資料 {#label}

根據您使 [!DNL Experience Cloud] 用的應用程式，您必須標籤特定資料欄位，以因應隱私權要求而存取或刪除。 標籤資料的程式會因應用程式而異。 如要瞭解如何為每個支援的Adobe應用程式標示資料，請參閱 [Experience Cloud應用程式的檔案](./experience-cloud-apps.md)。

### 確定要傳送至 [!DNL Privacy Service] {#identity}

為了處理 [!DNL Privacy Service] 來自客戶的隱私權要求，該要求本身必須提供該客戶的至少一個唯一識別值。 唯一識別值是可用於識別個人及其儲存在資料倉庫中的個人資料的任何 [!DNL Experience Cloud] 資訊。 [!DNL Privacy Service] 使用此身分資訊，根據要求的性質（存取、刪除或選擇退出）來尋找和處理客戶的個人資料。

根據您的 [!DNL Experience Cloud] CRM系統所使用的應用程式，您必須為每個客戶提供的識別值類型和數量會有所不同。 有些應用程式會運用其專屬的內部客戶ID值（例如Adobe Target ID），而其他解決方案則依賴Adobe [!DNL Experience Cloud Identity Service] (ECID)的全域識別碼，以追蹤所有應用程式的客戶活 [!DNL Experience Cloud] 動。 此外，電子郵件地址或電話號碼等一般個人資訊也可當成有效的身分資料。

隱私權要 [求的身分資料檔案](./identity-data.md) ，提供更詳細的身分資訊類型資訊，供您參考 [!DNL Privacy Service]。 本檔案也提供如何運用Adobe技術，在客戶與您的網站互動時，有效地從他們擷取適當的身分資訊，並在API要求中傳送該資 [!DNL Privacy Service] 料的指引。

### 開始提出隱私權要求 {#requests}

一旦您決定了企業的隱私權需求，並決定要傳送哪些身分值後，您就可 [!DNL Privacy Service]以開始提出隱私權要求。 [!DNL Privacy Service] 可讓您透過API或UI傳送隱私權要求。

>[!IMPORTANT]
>
>以下各節提供說明如何在API或UI中提出一般隱私權要求的檔案連結。 不過，視您使用 [!DNL Experience Cloud] 的應用程式而定，您必須在請求裝載中傳送的欄位可能與這些指南中顯示的範例不同。
>
>在遵循API或UI指南時，請參閱 [Privacy Service和Experience Cloud應用程式上的檔案，以取得有關如何設定特定應用程式的隱私權要求格式的](./experience-cloud-apps.md)[!DNL Experience Cloud] 詳細檔案。

#### 使用API

[! [DNL隱私服務API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/privacy-service.yaml) 提供數個端點，用於使用REST風格的API呼叫來建立和管理隱私權工作，讓您以程式設計方式處理應用程式的隱私權規範 [!DNL Experience Cloud] 規範。 如需如何使用API的詳細步驟，請參閱「隱私 [服務API開發人員指南」](api/getting-started.md)。

#### 使用UI

>[!NOTE]
>
>UI [!DNL Privacy Service] 目前僅支援存取和刪除請求。 所有選擇退出要求必須改為透過API提出。

UI [!DNL Privacy Service] 允許您使用圖形介面建立和監視隱私作業。 UI包含狀態報 **[!UICONTROL 表介面工具集]** ，可以視覺化呈現所有作用中請求的狀態，並可讓您使用內建的 **[!UICONTROL Request Builder]** 或上傳JSON檔案來建立新請求。 如需使用UI的詳細資訊，請參閱「隱私 [服務」使用指南](ui/overview.md)。

### 監控隱私權工作 {#monitor}

完成隱私權工作後，您有數個選項可用來監控其狀態和結果：

| 監控方法 | 說明 |
| --- | --- |
| [!DNL Privacy Service] UI | UI [!DNL Privacy Service] 提供監控控制面板，可讓您檢視所有作用中請求狀態的視覺化表示。 如需詳細 [資訊，請參閱Privacy Service使用指南](ui/overview.md) 。 |
| [!DNL Privacy Service] API | 您可以使用API提供的查閱端點，以程式設計方式監控隱私權工作的 [!DNL Privacy Service] 狀態。 請參閱隱 [私權服務開發人員指南](./api/getting-started.md) ，以取得如何使用API的詳細步驟。 |
| [!DNL Privacy Events] | [!DNL Privacy Events] 運用傳送至已設定網頁掛接的Adobe I/O事件，以協助有效率的工作要求自動化。 它們可降低或免除輪詢 [!DNL Privacy Service] API的需求，以檢查工作是否完成或工作流程中是否達到特定里程碑。 如需詳細資訊，請 [參閱訂閱隱私權事件](./privacy-events.md) 的教學課程。 |

## 後續步驟

本檔案提供開始使用服 [!DNL Privacy Service] 務功能的高階概觀和主要步驟。 請參閱整個概述中連結的檔案，以取得有關使用各個方面的深入資訊 [!DNL Privacy Service]。
