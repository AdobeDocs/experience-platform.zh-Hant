---
keywords: Experience Platform；主題；熱門主題；GDPR;gdpr;ccpa:CCPA;pdpa;PDPA;pdpa_that;PDPA_THA;lgpd;LGPD;lgpd;lgpd_bra;LGPD_bra;LGPD_BRA;
solution: Experience Platform
title: Privacy Service概述
description: Privacy Service使您能夠在Experience Cloud資料操作中促進自動遵守法律隱私法規。
exl-id: 585f7619-5072-413b-9a62-be0ea0cd4d1b
source-git-commit: 3296209a15a5f88ab14e16de25d554b9df712445
workflow-type: tm+mt
source-wordcount: '1623'
ht-degree: 5%

---

# [!DNL Privacy Service] 概覽

>[!IMPORTANT]
>
>Adobe Experience Platform Privacy Service的權限已經改進，以提高其粒度級別。 這些更改使組織管理員能夠授予更多用戶以所需的角色和權限級別的訪問權限。 技術帳戶用戶必須更新其Privacy Service權限，因為此即將進行的更新對他們來說是突破性的更改。 此權限更改的強制實施將在 **2023年4月13日**。 請參閱 [遷移舊式API憑據](./permissions.md#migrate-tech-accounts) 以指導解決這個問題。
>
>技術帳戶可供企業客戶使用，並通過Adobe開發者控制台建立。 技術賬戶持有人的Adobe ID `@techacct.adobe.com`。 如果您不確定您是否是技術帳戶持有人，請與組織管理員聯繫。

為了提供更好的客戶體驗，您需要收集和儲存客戶的個人資料。 使用此資料時，瞭解並尊重客戶的隱私非常重要。 新的法律和組織法規授予使用者權利，讓使用者有權應要求從您的資料存放區存取或刪除其個人資料。

Adobe Experience Platform [!DNL Privacy Service] 是為應對企業管理客戶個人資料的方式發生根本性轉變而開發的。 C.C.的核心目的 [!DNL Privacy Service] 是自動化對資料隱私保護法規的遵從，這些法規一旦違反，可能會導致重大罰款並中斷您業務的資料操作。

[!DNL Privacy Service] 提供REST風格的API和用戶介面，幫助您管理客戶資料請求。 與 [!DNL Privacy Service]，您可以提交訪問和刪除Adobe Experience Cloud應用程式中的個人客戶資料的請求，以便自動遵守法律和組織隱私法規。

>[!IMPORTANT]
>
>Privacy Service僅用於資料主題和消費者權利請求。 不支援或不允許使用Privacy Service進行資料清理或維護。 Adobe有法律義務及時履行這些義務。 因此，不允許對Privacy Service進行負載測試，因為它是僅生產環境，並會建立有效隱私請求的不必要的積壓。
>
>現在已設定硬性每日上載限制，以幫助防止濫用服務。 發現濫用系統的用戶將禁用其對服務的訪問權限。 隨後將與他們舉行會議，討論他們的行動並討論可接受的Privacy Service用途。

## 入門 [!DNL Privacy Service] {#getting-started}

為了利用 [!DNL Privacy Service]，需要根據您組織的隱私要求、您從客戶那裡收集的身份資料的種類以及將CRM系統與服務介面的最佳方式，做出幾項關鍵決策。

這些決定可通過以下問題加以總結：

1. **我從客戶那裡收集了哪些資訊？**
   * 充分利用 [!DNL Privacy Service]您必須對從客戶那裡收集的資料類型以及其中哪些資料受隱私法規的約束有詳細的瞭解。 請參閱 [確定隱私要求](#requirements) 的子菜單。
1. **我是否正確地標籤了資料？**
   * 必須正確標籤資料，才能使服務確定在隱私作業期間訪問或刪除哪些欄位。 請參閱 [標籤資料](#label) 的子菜單。
1. **我知道要發送給 [!DNL Privacy Service]?**
   * 在發送隱私請求時，必須提供特定於特定Adobe應用程式的單個客戶ID。 請參閱 [提供身份資料](#identity)  和 [發出隱私請求](#requests) 的子菜單。
1. **如何跟蹤我的隱私工作？**
   * 在您發出隱私請求後，有幾個選項可用於跟蹤其狀態和結果。 請參閱 [監視隱私作業](#monitor) 的子菜單。

以下各節就這些重要的先決條件步驟提供了一般性指導，並提供了進一步的連結 [!DNL Privacy Service] 文檔。

### 確定您組織的隱私要求 {#requirements}

根據您的業務性質及其營運的管轄區，您的資料作業可能受法律隱私權法規的約束。 這些法規通常授予權利給您的客戶，讓他們可請求存取您自他們那裡收集的資料，以及請求您刪除該筆儲存資料。 這些客戶對其個人資料的請求在文檔中稱為「隱私請求」。

有關不同法律隱私法規的詳細資訊， [!DNL Privacy Service] 管理請求，包括關鍵術語和常見問題的答案，請參閱 [隱私法規文檔](./regulations/overview.md)。

如果您的資料操作屬於任何受支援法規的權限範圍，請查看其文檔以瞭解重要資訊，例如他們為客戶提供的特定隱私權以及遵守隱私請求的合規窗口。 在確定如何整合時應考慮這些資訊 [!DNL Privacy Service] 進入您的CRM系統，以及客戶應如何與您的網站進行交互以發出隱私請求。

除了法律法規外，在作出這些決定時還應考慮適用於您組織的任何組織或行業標準。

### 為隱私請求標籤資料 {#label}

取決於 [!DNL Experience Cloud] 您正在使用的應用程式，您必須為特定資料欄位添加標籤，這些資料欄位應根據隱私請求被訪問或刪除。 標籤資料的過程因應用程式而異。 要瞭解如何為每個受支援的Adobe應用程式標籤資料，請參閱上的文檔 [Experience Cloud應用程式](./experience-cloud-apps.md)。

### 確定要發送到的標識資料的類型 [!DNL Privacy Service] {#identity}

為了 [!DNL Privacy Service] 要處理來自客戶的隱私請求，必須在請求本身中提供該客戶的至少一個唯一標識值。 唯一標識值是可用於識別個人及其儲存在您的個人資料的任何資訊 [!DNL Experience Cloud] 資料儲存。 [!DNL Privacy Service] 使用此身份資訊根據請求的性質（訪問、刪除或選擇退出）查找和處理客戶的個人資料。

取決於 [!DNL Experience Cloud] 您的CRM系統所使用的應用程式、您必須為每個客戶提供的標識值的類型和數量將有所不同。 某些應用程式使用其自己的內部客戶ID值(如Adobe TargetID)，而其他解決方案則依賴來自Adobe的全局標識符 [!DNL Experience Cloud Identity Service] (ECID)，它跟蹤所有客戶活動 [!DNL Experience Cloud] 應用程式。 此外，電子郵件地址或電話號碼等一般個人資訊也可以用作有效的身份資料。

上的文檔 [隱私請求的標識資料](./identity-data.md) 提供了有關接受的身份資訊類型的詳細資訊 [!DNL Privacy Service]。 本文檔還就如何利用Adobe技術在客戶與您的網站交互時從他們那裡有效地檢索適當的身份資訊提供指導，並將該資料發送給 [!DNL Privacy Service] 的子目錄。

### 開始發出隱私請求 {#requests}

一旦確定了業務的隱私需要，並決定要發送到的標識值 [!DNL Privacy Service]，可以開始提出隱私請求。 [!DNL Privacy Service] 允許您通過API或UI發送隱私請求。

>[!IMPORTANT]
>
>以下各節提供了指向文檔的連結，這些文檔涉及如何在API或UI中發出一般隱私請求。 但是，根據 [!DNL Experience Cloud] 您正在使用的應用程式，您必須在請求負載中發送的欄位可能與這些指南中所示的示例不同。
>
>隨著API或UI指南的推出，請參閱上的文檔 [Privacy Service和Experience Cloud應用程式](./experience-cloud-apps.md) 有關如何格式化特定隱私請求的進一步文檔 [!DNL Experience Cloud] 應用程式。
>
>還必須注意的是，隱私請求是跨Experience Cloud應用程式非同步處理的。 一旦Privacy Service接收到請求，每個應用程式可能需要幾分鐘到幾週的時間來完成請求。 完成每個請求所花費的時間量取決於您正在使用的應用程式以及需要處理的資料量。

#### 使用 API

的 [[!DNL Privacy Service API]](https://www.adobe.io/experience-platform-apis/references/privacy-service/) 為使用REST風格的API調用建立和管理隱私作業提供了多個端點，使您能夠以寫程式方式為您提供隱私法規合規性 [!DNL Experience Cloud] 應用程式。 有關如何使用API的詳細步驟，請參見 [Privacy ServiceAPI指南](api/overview.md)。

#### 使用UI

>[!NOTE]
>
>的 [!DNL Privacy Service] UI當前僅支援訪問和刪除請求。 所有選擇退出請求必須通過API進行。

的 [!DNL Privacy Service] UI允許您使用圖形介面建立和監視隱私作業。 UI包括 **[!UICONTROL 狀態報告]** 提供所有活動請求狀態的可視化表示的構件，並允許您使用內置的 **[!UICONTROL 請求生成器]** 或上傳JSON檔案。 有關使用UI的詳細資訊，請參見 [Privacy Service使用手冊](ui/overview.md)。

### 監視隱私作業 {#monitor}

一旦您完成了隱私作業，您就有幾個用於監視其狀態和結果的選項：

| 監控方法 | 說明 |
| --- | --- |
| [!DNL Privacy Service] UI | 的 [!DNL Privacy Service] UI提供了監視儀表板，允許您查看所有活動請求狀態的可視表示形式。 查看 [Privacy Service使用手冊](ui/overview.md) 的子菜單。 |
| [!DNL Privacy Service] API | 可以通過使用提供的查找端點，以寫程式方式監視隱私作業的狀態 [!DNL Privacy Service] API。 查看 [Privacy ServiceAPI指南](./api/overview.md) 有關如何使用API的詳細步驟。 |
| [!DNL Privacy Events] | [!DNL Privacy Events] 利用發送到已配置Webhook的Adobe I/O事件，以便於高效地執行作業請求自動化。 它們減少或消除了 [!DNL Privacy Service] API，以檢查作業是否完成或是否已達到工作流中的某個里程碑。 請參閱上的教程 [訂閱隱私事件](./privacy-events.md) 的子菜單。 |

## 後續步驟

本文檔提供了對 [!DNL Privacy Service] 以及開始使用服務功能所需的主要步驟。 請參閱在整個概述中連結的文檔，瞭解有關使用的各個方面的更深入資訊 [!DNL Privacy Service]。
