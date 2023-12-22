---
keywords: Experience Platform；首頁；熱門主題；GDPR；gdpr；ccpa：CCPA；PDPA；PDPA_that；PDPA_THA；lgpd；LGPD；lgpd_bra；LGPD_BRA；
solution: Experience Platform
title: Privacy Service概觀
description: 探索Privacy Service如何在您的Experience Cloud資料作業中，促進自動符合隱私權法規。
exl-id: 585f7619-5072-413b-9a62-be0ea0cd4d1b
source-git-commit: 19b33ddf2fc3f8d889d370eedfc732ac54178dcd
workflow-type: tm+mt
source-wordcount: '1532'
ht-degree: 5%

---

# Privacy Service 概觀

為了提供更好的客戶體驗，您必須收集和儲存客戶的個人資料。 使用此資料時，請務必瞭解並尊重客戶的隱私權。 新的法律和組織法規授予使用者權利，讓使用者有權應要求從您的資料存放區存取或刪除其個人資料。

Adobe Experience Platform Privacy Service的開發是為了因應企業管理客戶個人資料方式上的根本性轉變。 Privacy Service的主要目的是自動遵守資料隱私權法規，一旦違反法規，可能導致企業遭受重大罰款並中斷資料作業。

Privacy Service提供RESTful API和使用者介面，協助您管理客戶資料請求。 您可以使用Privacy Service提交存取和刪除Adobe Experience Cloud應用程式中個人客戶資料的請求，促進自動遵守法律和組織隱私權法規。

>[!IMPORTANT]
>
>Privacy Service僅適用於資料主體和消費者權利要求。 不支援或允許將Privacy Service用於資料清理或維護的任何其他用途。 Adobe有法定義務須及時履行。 因此，不允許在Privacy Service上進行負載測試，因為這是僅限生產的環境，且會為有效隱私權請求建立不必要的待處理專案。
>
>現已設定每日硬性上傳限制，以協助防止濫用服務。 發現濫用系統的使用者將會停用其服務的存取權。 隨後將與他們舉行會議，討論他們的動作，並討論可接受的Privacy Service用途。

## Privacy Service快速入門 {#getting-started}

為了最佳地使用Privacy Service，根據貴組織的隱私權要求、您從客戶那裡收集的身分資料型別，以及將CRM系統與服務介面的最佳方式，必須做出幾項重要決定。

這些決定可透過下列問題加以摘要：

1. **我從客戶那裡收集哪些資訊？**
   * 為了充分利用Privacy Service，您必須詳細瞭解您從客戶那裡收集的資料型別，以及哪些資料受隱私權法規的約束。 請參閱以下小節： [判斷隱私權需求](#requirements) 以取得詳細資訊。
1. **我是否正確標示我的資料？**
   * 必須為服務正確標示資料，以決定在隱私權工作期間要存取或刪除哪些欄位。 請參閱以下小節： [標籤資料](#label) 以取得詳細資訊。
1. **我是否知道要將哪些ID傳送給Privacy Service？**
   * 傳送隱私權要求時，必須提供特定Adobe應用程式專用的個別客戶ID。 請參閱以下小節： [提供身分資料](#identity)  和 [提出隱私權請求](#requests) 以取得詳細資訊。
1. **如何追蹤我的隱私權工作？**
   * 在提出隱私權請求後，您可使用數個選項來追蹤其狀態和結果。 請參閱以下小節： [監控隱私權工作](#monitor) 以取得詳細資訊。

以下章節提供這些重要必要步驟的一般指引，也提供更多Privacy Service檔案的連結，以取得詳細資訊。

### 判斷貴組織的隱私權要求 {#requirements}

根據您的業務性質及其營運的管轄區，您的資料作業可能受法律隱私權法規的約束。 這些法規通常授予權利給您的客戶，讓他們可請求存取您自他們那裡收集的資料，以及請求您刪除該筆儲存資料。 客戶對其個人資料的請求，在本檔案稱為「隱私權請求」。

如需Privacy Service管理請求的各種法律隱私權法規的詳細資訊，包括重要辭彙及常見問題的解答，請參閱 [隱私權法規檔案](./regulations/overview.md).

如果您的資料作業屬於任何受支援法規的管轄範圍，請檢閱其檔案以取得重要資訊，例如他們提供給客戶的特定隱私權，以及遵循隱私權請求的合規視窗。 在決定如何將Privacy Service整合至您的CRM系統，以及客戶應如何與您的網站互動以提出隱私權要求時，應考量這些資訊。

除了法律規定外，在做出這些決定時，也應考量適用於您組織的任何組織或產業標準。

### 隱私權請求的標籤資料 {#label}

依據 [!DNL Experience Cloud] 您正在使用的應用程式，必須標示回應隱私權要求時應存取或刪除的特定資料欄位。 標籤資料的程式因應用程式而異。 若要瞭解如何為每個支援的Adobe應用程式加上標籤，請參閱以下檔案： [Experience Cloud應用程式](./experience-cloud-apps.md).

### 決定要傳送給Privacy Service的身分資料型別 {#identity}

為了讓Privacy Service處理來自客戶的隱私權請求，請求本身必須提供至少一個唯一身分值。 唯一身分值是可用於識別個人及其在您網站中儲存的個人資料的任何資訊， [!DNL Experience Cloud] 資料存放區。 Privacy Service會使用此身分資訊，根據請求的性質（存取、刪除或選擇退出）來尋找及處理客戶的個人資料。

依據 [!DNL Experience Cloud] 您的CRM系統所使用的應用程式，您為每個客戶提供的身分值型別和數量會有所不同。 有些應用程式會使用自己的內部客戶ID值(例如Adobe Target ID)，而其他解決方案則需仰賴Adobe提供的全域識別碼 [!DNL Experience Cloud Identity Service] (ECID)追蹤所有客戶活動 [!DNL Experience Cloud] 應用程式。 此外，電子郵件地址或電話號碼等一般個人資訊也可作為有效的身分資料。

閱讀檔案於 [隱私權請求的身分資料](./identity-data.md) 以取得Privacy Service可接受的身分資訊型別的詳細資訊。 本檔案也提供如何套用Adobe技術，以便在客戶與您的網站互動時，有效擷取適當的身分資訊，並將資料傳送至API請求中的Privacy Service的相關指引。

### 開始提出隱私權請求 {#requests}

一旦您決定好企業的隱私權需求，並決定要將哪些身分值傳送給Privacy Service，您就可以開始提出隱私權要求。 使用Privacy Service透過API或UI傳送隱私權請求。

>[!IMPORTANT]
>
>以下各節提供檔案的連結，涵蓋如何在API或UI中提出一般隱私權請求。 然而，取決於 [!DNL Experience Cloud] 若您正在使用的應用程式，您在要求裝載中必須傳送的欄位，可能會與這些指南中顯示的範例不同。
>
>當您按照API或UI指南進行操作時，請參閱以下檔案： [Privacy Service和Experience Cloud應用程式](./experience-cloud-apps.md) 有關如何格式化您特定隱私權請求的進一步檔案 [!DNL Experience Cloud] 應用程式。
>
>也請務必注意，隱私權請求會跨Experience Cloud應用程式以非同步方式處理。 當Privacy Service收到請求後，每個應用程式可能需要幾分鐘到幾週的時間才能完成請求。 完成每個要求所需的時間會因您所使用的應用程式而有所不同，而且需要處理的資料量也會有所不同。

#### 使用 API {#api}

以程式設計方式處理您隱私權法規的合規性 [!DNL Experience Cloud] 應用程式，您可以使用RESTful API呼叫來 [[!DNL Privacy Service API]](https://developer.adobe.com/experience-platform-apis/references/privacy-service/) 用來建立及管理隱私權工作的端點。 如需如何使用API的詳細步驟，請參閱 [Privacy Service API指南](api/overview.md).

#### 使用UI {#ui}

>[!NOTE]
>
>Privacy Service UI目前僅支援存取和刪除請求。 所有選擇退出請求必須改透過API提出。

您可以使用圖形介面搭配Privacy ServiceUI來建立和監視隱私權工作。 UI包含 **[!UICONTROL 狀態報表]** Widget以視覺化方式呈現所有作用中請求的狀態，而您可以使用內建的程式碼建立請求 **[!UICONTROL 請求產生器]** 或上傳JSON檔案。 如需使用UI的詳細資訊，請參閱 [Privacy Service使用手冊](ui/overview.md).

### 監視隱私權工作 {#monitor}

完成隱私權工作後，您有數個選項可監控其狀態和結果：

| 監視方法 | 說明 |
| --- | --- |
| PRIVACY SERVICEUI | 您可以使用Privacy ServiceUI監視儀表板來檢視所有作用中請求狀態的視覺化表示。 請參閱 [Privacy Service使用手冊](ui/overview.md) 以取得詳細資訊。 |
| PRIVACY SERVICE API | 您可以使用Privacy ServiceAPI提供的查詢端點，以程式設計方式監視隱私權工作的狀態。 請參閱 [Privacy Service API指南](./api/overview.md) 瞭解如何使用API的詳細步驟。 |
| [!DNL Privacy Events] | [!DNL Privacy Events] 使用傳送至已設定webhook的Adobe I/O事件來促進有效的工作請求自動化。 它們減少或消除了輪詢Privacy ServiceAPI以檢查工作是否完成或工作流程中是否已達到特定里程碑的需求。 請參閱上的教學課程 [訂閱隱私權事件](./privacy-events.md) 以取得詳細資訊。 |

## 後續步驟

本檔案提供Privacy Service的整體概觀，以及開始使用服務功能所需的主要步驟。 如需有關使用Privacy Service各個層面的更深入資訊，請參閱整份概覽中的檔案連結。
