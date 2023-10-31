---
title: 使用平台UI設定及設定客戶自控金鑰
description: 瞭解如何使用您的Azure租使用者設定您的CMK應用程式，並將您的加密金鑰ID傳送至Adobe Experience Platform。
exl-id: 5f38997a-66f3-4f9d-9c2f-fb70266ec0a6
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '1097'
ht-degree: 1%

---

# 使用Platform UI設定及設定客戶自控金鑰

本文介紹在Platform中使用UI啟用客戶自控金鑰(CMK)功能的程式。 如需有關如何使用API完成此程式的說明，請參閱 [API CMK設定檔案](./api-set-up.md).

## 先決條件

若要檢視並造訪 [!UICONTROL 加密] Adobe Experience Platform區段，您必須已建立角色並指派 [!UICONTROL 管理客戶自控金鑰] 該角色的許可權。 任何使用者擁有 [!UICONTROL 管理客戶自控金鑰] 許可權可為其組織啟用CMK。

有關在Experience Platform中指派角色和許可權的詳細資訊，請參閱 [設定許可權檔案](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/configure-permissions.html).

若要啟用CMK，您的 [[!DNL Azure] 必須設定金鑰儲存庫](./azure-key-vault-config.md) 設定下：

* [啟用清除保護](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview#purge-protection)
* [啟用軟刪除](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview)
* [設定存取權，使用 [!DNL Azure] 角色型存取控制](https://learn.microsoft.com/en-us/azure/role-based-access-control/)
* [設定 [!DNL Azure] 金鑰儲存庫](./azure-key-vault-config.md)

## 設定CMK應用程式 {#register-app}

設定好金鑰儲存庫後，下一步就是註冊將連結至您的 [!DNL Azure] 租使用者。

### 快速入門

若要檢視 [!UICONTROL 加密設定] 儀表板，選取 **[!UICONTROL 加密]** 在 [!UICONTROL 管理] 左側導覽側欄的標題。

![加密設定儀表板（含加密）和客戶自控金鑰卡會醒目提示。](../../images/governance-privacy-security/customer-managed-keys/encryption-configraion.png)

選取 **[!UICONTROL 設定]** 以開啟 [!UICONTROL 客戶自控金鑰組態] 檢視。 此工作區包含完成下列步驟以及與Azure金鑰儲存庫執行整合所需的所有必要值。

### 複製驗證URL {#copy-authentication-url}

若要開始註冊程式，請從以下位置複製您組織的應用程式驗證URL： [!UICONTROL 客戶自控金鑰組態] 檢視並貼到 [!DNL Azure] 環境 **[!DNL Key Vault Crypto Service Encryption User]**. 操作方法的詳細資訊 [指派角色](#assign-to-role) 將於下一節提供。

選取復製圖示(![復製圖示。](../../images/governance-privacy-security/customer-managed-keys/copy-icon.png))由 [!UICONTROL 應用程式驗證URL].

![此 [!UICONTROL 客戶自控金鑰組態] 檢視時會醒目提示「應用程式驗證URL」區段。](../../images/governance-privacy-security/customer-managed-keys/application-authentication-url.png)

複製並貼上 [!UICONTROL 應用程式驗證URL] 在瀏覽器中開啟驗證對話方塊。 選取 **[!DNL Accept]** 若要將CMK應用程式服務主體新增至 [!DNL Azure] 租使用者。 確認驗證會將您重新導向至Experience Cloud登陸頁面。

![Microsoft許可權要求對話方塊，其中包含 [!UICONTROL Accept] 反白顯示。](../../images/governance-privacy-security/customer-managed-keys/app-permission.png)

>[!IMPORTANT]
>
>如果您有多個 [!DNL Microsoft Azure] 訂閱，您就可能會將平台執行個體連線到錯誤的金鑰儲存庫。 在此情況下，您必須交換 `common` CMK目錄ID的應用程式驗證URL名稱的區段。<br>從的入口網站設定、目錄和訂閱頁面複製CMK目錄ID [!DNL Microsoft Azure] 應用計畫<br>![此 [!DNL Microsoft Azure] 「應用程式入口網站」設定、「目錄與訂閱」頁面，其中醒目提示目錄ID。](../../images/governance-privacy-security/customer-managed-keys/directory-id.png)<br>接著，貼到您的瀏覽器位址列中。<br>![反白顯示應用程式驗證URL之「通用」區段的Google瀏覽器頁面。](../../images/governance-privacy-security/customer-managed-keys/common-url-section.png)

### 將CMK應用程式指派給角色 {#assign-to-role}

完成驗證程式後，請導覽回 [!DNL Azure] 金鑰儲存庫及選擇 **[!DNL Access control]** ，位於左側導覽器中。 從這裡，選擇 **[!DNL Add]** 後面接著 **[!DNL Add role assignment]**.

![此 [!DNL Microsoft Azure] 儀表板，具有 [!DNL Add] 和 [!DNL Add role assignment] 反白顯示。](../../images/governance-privacy-security/customer-managed-keys/add-role-assignment.png)

下一個畫面會提示您選擇此指派的角色。 選取 **[!DNL Key Vault Crypto Service Encryption User]** 在選取之前 **[!DNL Next]** 以繼續。

![此 [!DNL Microsoft Azure] 儀表板 [!DNL Key Vault Crypto Service Encryption User] 反白顯示。](../../images/governance-privacy-security/customer-managed-keys/select-role.png)

在下一個畫面，選擇 **[!DNL Select members]** 以開啟右側邊欄中的對話方塊。 使用搜尋列來尋找CMK應用程式的服務主體，並從清單中選取它。 完成後，選取 **[!DNL Save]**.

>[!NOTE]
>
>如果您在清單中找不到您的應用程式，則表示您的服務主體尚未被租使用者接受。 為確保您擁有正確的許可權，請使用您的 [!DNL Azure] 管理員或代表。

您可以透過比較 [!UICONTROL 應用程式ID] 提供於 [!UICONTROL 客戶自控金鑰組態] 使用檢視 [!DNL Application ID] 提供於 [!DNL Microsoft Azure] 應用程式概述。

![此 [!UICONTROL 客戶自控金鑰組態] 使用檢視 [!UICONTROL 應用程式ID] 反白顯示。](../../images/governance-privacy-security/customer-managed-keys/application-id.png)

驗證Azure工具所需的所有詳細資訊都包含在平台UI中。 如果許多使用者希望使用其他Azure工具來增強其監視和記錄這些應用程式對其金鑰儲存庫存取的能力，則會提供此詳細程度等級。 瞭解這些識別碼對於該目的以及協助Adobe服務存取金鑰至關重要。

## 在Experience Platform上啟用加密金鑰設定 {#send-to-adobe}

在上安裝CMK應用程式後 [!DNL Azure]，即可將加密金鑰識別碼傳送至Adobe。 選取 **[!DNL Keys]** ，然後輸入要傳送的金鑰名稱。

![Microsoft Azure控制面板具有 [!DNL Keys] 物件和醒目提示的金鑰名稱。](../../images/governance-privacy-security/customer-managed-keys/select-key.png)

選取金鑰的最新版本，其詳細資訊頁面就會顯示。 從這裡，您可以選擇設定金鑰的允許操作。

>[!IMPORTANT]
>
>金鑰允許的最小必要操作為 **[!DNL Wrap Key]** 和 **[!DNL Unwrap Key]** 許可權。 您可以包括 [!DNL Encrypt]， [!DNL Decrypt]， [!DNL Sign]、和 [!DNL Verify] 您想要的話。

此 **[!UICONTROL 金鑰識別碼]** 欄位會顯示金鑰的URI識別碼。 複製此URI值以用於下一個步驟。

![Microsoft Azure儀表板金鑰詳細資訊，包含 [!DNL Permitted operations] 和複製金鑰URL區段強調顯示。](../../images/governance-privacy-security/customer-managed-keys/copy-key-url.png)

取得 [!DNL Key vault URI]，返回 [!UICONTROL 客戶自控金鑰組態] 檢視並輸入描述性 **[!UICONTROL 設定名稱]**. 接下來，新增 [!DNL Key Identifier] 從Azure金鑰詳細資料頁面擷取至 **[!UICONTROL 金鑰儲存庫金鑰識別碼]** 並選取 **[!UICONTROL 儲存]**.

![此 [!UICONTROL 客戶自控金鑰組態] 使用檢視 [!UICONTROL 設定名稱] 和 [!UICONTROL 金鑰儲存庫金鑰識別碼] 區段會反白顯示。](../../images/governance-privacy-security/customer-managed-keys/configuration-name.png)

您將返回 [!UICONTROL 加密設定儀表板]. 的狀態 [!UICONTROL 客戶自控金鑰] 組態顯示為 [!UICONTROL 處理中].

![此 [!UICONTROL 加密設定] 儀表板，具有 [!UICONTROL 處理中] 反白顯示於 [!UICONTROL 客戶自控金鑰] 卡片。](../../images/governance-privacy-security/customer-managed-keys/processing.png)

## 驗證設定的狀態 {#check-status}

允許相當長的處理時間。 若要檢查組態狀態，請返回 [!UICONTROL 客戶自控金鑰組態] 檢視並向下捲動至 [!UICONTROL 設定狀態]. 進度列已進階至步驟一，說明系統正在驗證Platform是否可存取金鑰和金鑰儲存庫。

CMK設定有四種可能的狀態。 具體如下：

* 步驟1：驗證Platform是否能夠存取金鑰和金鑰儲存庫。
* 步驟2：金鑰儲存庫和金鑰名稱正在新增至貴組織的所有資料存放區。
* 步驟3：金鑰儲存庫和金鑰名稱已成功新增至資料存放區。
* `FAILED`：發生問題，主要與金鑰、金鑰儲存庫或多租使用者應用程式設定有關。

## 後續步驟

完成上述步驟，您已成功為組織啟用CMK。 現在，您會使用中的金鑰，將內嵌至主要資料存放區的資料加密和解密。 [!DNL Azure] 金鑰儲存庫。
