---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 隱私權服務開發人員指南
description: 使用REST風格的API，跨Adobe Experience Cloud應用程式管理資料主體的個人資料
topic: developer guide
translation-type: tm+mt
source-git-commit: 1bb896f7629d7b71b94dd107eeda87701df99208
workflow-type: tm+mt
source-wordcount: '762'
ht-degree: 0%

---


# [!DNL Privacy Service] 開發人員指南

Adobe Experience Platform提 [!DNL Privacy Service] 供REST風格的API和使用者介面，可讓您跨Adobe Experience Cloud應用程式管理（存取和刪除）資料主體（客戶）的個人資料。 [!DNL Privacy Service] 還提供了集中審計和記錄機制，允許您訪問涉及應用程式的作業的狀態和 [!DNL Experience Cloud] 結果。

本指南涵蓋如何使用 [!DNL Privacy Service] API。 如需如何使用UI的詳細資訊，請參閱隱私 [服務UI概觀](../ui/overview.md)。 如需API中所有可用端點的完整清 [!DNL Privacy Service] 單，請參閱 [API參考](https://www.adobe.io/apis/experiencecloud/gdpr/api-reference.html)。

## 快速入門 {#getting-started}

本指南需要熟悉下列功 [!DNL Experience Platform] 能：

* [[!DNL隱私服務]](../home.md):提供REST風格的API和使用者介面，可讓您跨Adobe Experience Cloud應用程式管理資料主體（客戶）的存取和刪除要求。

以下各節提供您必須知道的其他資訊，以便成功呼叫隱私權服務API。

### 讀取範例API呼叫

本教學課程提供範例API呼叫，以示範如何設定請求的格式。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱疑難排解指 [南中有關如何讀取範例API呼叫的](../../landing/troubleshooting.md)[!DNL Experience Platform] 章節。

## 收集必要標題的值

若要呼叫 [!DNL Privacy Service] API，您必須先收集要用於必要標題的存取認證：

* 授權：生產者 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

這包括在Adobe Admin Console中取 [!DNL Experience Platform] 得開發人員權限，然後在Adobe Developer Console中產生認證。

### 取得開發人員的存取權 [!DNL Experience Platform]

若要取得開發人員的 [!DNL Platform]存取權，請依照 [Experience Platform驗證教學課程的開](../../tutorials/authentication.md)始步驟進行。 在您進入「在Adobe Developer Console中產生存取認證」步驟後，請返回本教學課程，以產生特定的認證 [!DNL Privacy Service]。

### 生成訪問憑據

使用Adobe Developer Console，您必須產生下列三種存取憑證：

* `{IMS_ORG}`
* `{API_KEY}`
* `{ACCESS_TOKEN}`

您 `{IMS_ORG}` 的 `{API_KEY}` API呼叫只需產生一次，即可重複使用。 但是，您的 `{ACCESS_TOKEN}` 作業是暫時的，必須每24小時重新生一次。

產生這些值的步驟詳細說明如下。

#### 一次性設定

前往 [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) ，使用您的Adobe ID登入。 接著，請依照教學課程中說明的步驟， [在Adobe Developer Console檔案中建立空白的專案](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) 。

建立新專案後，按一下「專 **[!UICONTROL 案概述」畫面上的]****[!UICONTROL 「新增API]** 」。

![](../images/api/getting-started/add-api-button.png)

出現 **[!UICONTROL 「Add an API]** （添加API）」螢幕。 按一 **[!UICONTROL 下「下一步]** 」前，從可用API清單中選取「隱私權服務 **[!UICONTROL API」]**。

![](../images/api/getting-started/add-privacy-service-api.png)

此時 **[!UICONTROL 會顯示「設定API]** 」畫面。 選取「產生 **[!UICONTROL 鍵對」選項]**，然後按一下右下角 **[!UICONTROL 的「產生鍵對]** 」。

![](../images/api/getting-started/generate-key-pair.png)

系統會自動產生金鑰對，並將包含私密金鑰和公用憑證的ZIP檔案下載至您的本機電腦（稍後的步驟將會使用）。 選擇 **[!UICONTROL 保存配置的API]** ，以完成配置。

![](../images/api/getting-started/key-pair-generated.png)

在將API新增至專案後，專案頁面會重新顯示在「隱私權服務 _API概觀」頁面_ 。 從這裡，向下捲動至「 **[!UICONTROL Service Account(JWT)]** 」區段，該區段提供對 [!DNL Privacy Service] API的所有呼叫所需的下列存取憑證：

* **[!UICONTROL 用戶端ID]**:必須在x-api-key標 `{API_KEY}` 題中提供用戶端ID。
* **[!UICONTROL 組織ID]**:組織ID是必 `{IMS_ORG}` 須用在x-gw-ims-org-id標題中的值。

![](../images/api/getting-started/jwt-credentials.png)

#### 每個會話的驗證

您必須收集的最終必要憑證是您 `{ACCESS_TOKEN}`的，此憑證會用於「授權」標題。 與和的值不 `{API_KEY}` 同， `{IMS_ORG}`必須每24小時產生一個新的Token，才能繼續使用 [!DNL Platform] API。

若要產生新 `{ACCESS_TOKEN}`密鑰，請開啟先前下載的私密金鑰，並將其內容貼入「產生存取Token」旁的文字方塊， **[!UICONTROL 再按一下「產]** 生Token ****」。

![](../images/api/getting-started/paste-private-key.png)

產生新的存取Token，並提供將Token複製至剪貼簿的按鈕。 此值用於所需的授權標題，且必須以格式提供 `Bearer {ACCESS_TOKEN}`。

![](../images/api/getting-started/generated-access-token.png)

## 後續步驟

現在，您已瞭解要使用哪些標題，可以開始呼叫 [!DNL Privacy Service] API。 隱私權工 [作的檔案](privacy-jobs.md) ，會逐步說明您可使用API進行的各種API [!DNL Privacy Service] 呼叫。 每個範例呼叫都包含一般API格式、顯示必要標題的範例要求，以及範例回應。
