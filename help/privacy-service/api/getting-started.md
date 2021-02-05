---
keywords: Experience Platform;home；熱門主題
solution: Experience Platform
title: 隱私權服務API指南
description: 隱私權服務API可讓開發人員建立並管理客戶要求，以便在Experience Cloud應用程式中存取或刪除其個人資料，以符合法律隱私權法規。 請依照本指南，瞭解如何使用API執行關鍵作業。
topic: developer guide
translation-type: tm+mt
source-git-commit: e649ab3da077cdd8e98562199b8bdece6108a572
workflow-type: tm+mt
source-wordcount: '795'
ht-degree: 0%

---


# [!DNL Privacy Service] API指南

Adobe Experience Platform [!DNL Privacy Service]提供REST風格的API和使用者介面，可讓您跨Adobe Experience Cloud應用程式管理（存取和刪除）資料主體（客戶）的個人資料。 [!DNL Privacy Service] 還提供了集中審計和記錄機制，允許您訪問涉及應用程式的作業的狀態和 [!DNL Experience Cloud] 結果。

本指南介紹如何使用[!DNL Privacy Service] API。 如需如何使用UI的詳細資訊，請參閱[隱私權服務UI概觀](../ui/overview.md)。 有關[!DNL Privacy Service] API中所有可用端點的完整清單，請參閱[API參考](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/privacy-service.yaml)。

## 快速入門 {#getting-started}

本指南需要有效瞭解下列[!DNL Experience Platform]功能：

* [[!DNL Privacy Service]](../home.md):提供REST風格的API和使用者介面，可讓您跨Adobe Experience Cloud應用程式管理資料主體（客戶）的存取和刪除要求。

以下各節提供您必須知道的其他資訊，以便成功呼叫隱私權服務API。

### 讀取範例API呼叫

本教學課程提供範例API呼叫，以示範如何設定請求的格式。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱[!DNL Experience Platform]疑難排解指南中[如何讀取範例API呼叫](../../landing/troubleshooting.md)一節。

## 收集必要標題的值

若要呼叫[!DNL Privacy Service] API，您必須先收集要用於必要標題的存取認證：

* 授權：載體`{ACCESS_TOKEN}`
* x-api-key:`{API_KEY}`
* x-gw-ims-org-id:`{IMS_ORG}`

這包括在Adobe Admin Console中取得[!DNL Experience Platform]的開發人員權限，然後在Adobe Developer Console中產生認證。

### 取得[!DNL Experience Platform]的開發人員存取權

若要取得[!DNL Platform]的開發人員存取權，請依照[體驗平台驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)中的開始步驟進行。 進入步驟「在Adobe Developer Console中產生存取認證」後，請返回本教學課程，以產生[!DNL Privacy Service]專屬的認證。

### 生成訪問憑據

使用Adobe Developer Console，您必須產生下列三種存取憑證：

* `{IMS_ORG}`
* `{API_KEY}`
* `{ACCESS_TOKEN}`

您的`{IMS_ORG}`和`{API_KEY}`只需產生一次，就可在未來的API呼叫中重複使用。 但是，您的`{ACCESS_TOKEN}`是暫時的，必須每24小時重新產生一次。

產生這些值的步驟詳細說明如下。

#### 一次性設定

前往[Adobe Developer Console](https://www.adobe.com/go/devs_console_ui)並使用您的Adobe ID登入。 接下來，請依照[教學課程中說明的步驟，在Adobe Developer Console檔案中建立空白專案](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md)。

建立新專案後，請在&#x200B;**[!UICONTROL 專案概述]**&#x200B;畫面上選取&#x200B;**[!UICONTROL 新增API]**。

![](../images/api/getting-started/add-api-button.png)

出現「**[!UICONTROL 新增API]**」畫面。 在選擇&#x200B;**[!UICONTROL Next]**&#x200B;之前，從可用API清單中選擇&#x200B;**[!UICONTROL 隱私服務API]**。

![](../images/api/getting-started/add-privacy-service-api.png)

出現「**[!UICONTROL Configure API]**（配置API）」螢幕。 選擇&#x200B;**[!UICONTROL 生成鍵對]**&#x200B;的選項，然後選擇右下角的&#x200B;**[!UICONTROL 生成鍵對]**。

![](../images/api/getting-started/generate-key-pair.png)

系統會自動產生金鑰對，並將包含私密金鑰和公用憑證的ZIP檔案下載至您的本機電腦（稍後的步驟將會使用）。 選擇&#x200B;**[!UICONTROL 保存配置的API]**&#x200B;以完成配置。

![](../images/api/getting-started/key-pair-generated.png)

在將API新增至專案後，專案頁面會重新出現在&#x200B;**隱私權服務API概觀**&#x200B;頁面。 從這裡，向下滾動到&#x200B;**[!UICONTROL 服務帳戶(JWT)]**&#x200B;部分，該部分提供對[!DNL Privacy Service] API的所有調用所需的以下訪問憑據：

* **[!UICONTROL 用戶端ID]**:必須在x-api-key標 `{API_KEY}` 題中提供用戶端ID。
* **[!UICONTROL 組織ID]**:組織ID是必 `{IMS_ORG}` 須用在x-gw-ims-org-id標題中的值。

![](../images/api/getting-started/jwt-credentials.png)

#### 每個會話的驗證

您必須收集的最終必要憑證是`{ACCESS_TOKEN}`，它用於「授權」標題中。 與`{API_KEY}`和`{IMS_ORG}`的值不同，必須每24小時產生一個新Token，才能繼續使用[!DNL Platform] API。

若要產生新的`{ACCESS_TOKEN}`，請開啟先前下載的私密金鑰，並將其內容貼入&#x200B;**[!UICONTROL 產生存取Token]**&#x200B;旁的文字方塊中，再選取&#x200B;**[!UICONTROL 產生Token]**。

![](../images/api/getting-started/paste-private-key.png)

產生新的存取Token，並提供將Token複製至剪貼簿的按鈕。 此值用於所需的「授權」標頭，且必須以`Bearer {ACCESS_TOKEN}`格式提供。

![](../images/api/getting-started/generated-access-token.png)

## 後續步驟

現在您已瞭解要使用哪些標題，可以開始呼叫[!DNL Privacy Service] API。 有關[隱私權工作](privacy-jobs.md)的檔案會逐步說明您可使用[!DNL Privacy Service] API進行的各種API呼叫。 每個範例呼叫都包含一般API格式、顯示必要標題的範例要求，以及範例回應。
