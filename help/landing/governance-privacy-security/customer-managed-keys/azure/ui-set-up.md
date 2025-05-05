---
title: 使用Experience Platform UI為Azure設定及設定客戶自控金鑰
description: 瞭解如何使用您的Azure租使用者設定您的CMK應用程式，並將您的加密金鑰ID傳送至Adobe Experience Platform。
role: Developer
feature: Privacy
exl-id: 5f38997a-66f3-4f9d-9c2f-fb70266ec0a6
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1146'
ht-degree: 0%

---

# 使用Experience Platform UI為Azure設定及設定客戶自控金鑰

本文介紹在Experience Platform中使用UI啟用客戶自控金鑰(CMK)功能的Azure特定指示。 如需AWS的特定指示，請參閱[AWS安裝指南](../aws/ui-set-up.md)。

如需有關如何使用API為Azure代管的Experience Platform執行個體完成此程式的說明，請參閱[API CMK設定檔案](./api-set-up.md)。

## 先決條件

若要在Adobe Experience Platform中檢視並瀏覽[!UICONTROL 加密]區段，您必須已建立角色，並已將[!UICONTROL 管理客戶管理的金鑰]許可權指派給該角色。 任何擁有[!UICONTROL 管理客戶管理的金鑰]許可權的使用者都可以為其組織啟用CMK。

如需在Experience Platform中指派角色和許可權的詳細資訊，請參閱[設定許可權檔案](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/configure-permissions.html?lang=zh-Hant)。

若要啟用CMK，您的[[!DNL Azure] 金鑰儲存庫必須使用下列設定來設定](./azure-key-vault-config.md)：

* [啟用清除保護](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview#purge-protection)
* [啟用軟刪除](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview)
* [使用 [!DNL Azure] 角色型存取控制設定存取權](https://learn.microsoft.com/en-us/azure/role-based-access-control/)
* [設定 [!DNL Azure] 金鑰儲存庫](./azure-key-vault-config.md)

## 設定CMK應用程式 {#register-app}

在您設定金鑰儲存庫後，下一步是註冊將連結至您[!DNL Azure]租使用者的CMK應用程式。

### 快速入門

若要檢視[!UICONTROL 加密設定]儀表板，請選取左側導覽側邊欄[!UICONTROL 管理]標題下的&#x200B;**[!UICONTROL 加密]**。

![加密組態儀表板（含加密）和客戶管理的金鑰卡已反白顯示。](../../../images/governance-privacy-security/customer-managed-keys/encryption-configraion.png)

選取&#x200B;**[!UICONTROL 設定]**&#x200B;以開啟[!UICONTROL 客戶自控金鑰設定]檢視。 此工作區包含完成下列步驟以及與Azure金鑰儲存庫執行整合所需的所有必要值。

### 複製驗證URL {#copy-authentication-url}

若要開始註冊程式，請從[!UICONTROL 客戶自控金鑰組態]檢視複製您組織的應用程式驗證URL，並將其貼到您的[!DNL Azure]環境&#x200B;**[!DNL Key Vault Crypto Service Encryption User]**&#x200B;中。 下一節提供如何[指派角色](#assign-to-role)的詳細資訊。

選取復製圖示(![復製圖示。](../../../../images/icons/copy.png))，由[!UICONTROL 應用程式驗證URL]。

![反白顯示[應用程式驗證URL]區段的[!UICONTROL 客戶受管理的金鑰組態]檢視。](../../../images/governance-privacy-security/customer-managed-keys/application-authentication-url.png)

將[!UICONTROL 應用程式驗證URL]複製並貼到瀏覽器，以開啟驗證對話方塊。 選取&#x200B;**[!DNL Accept]**&#x200B;將CMK應用程式服務主體新增至您的[!DNL Azure]租使用者。 確認驗證會將您重新導向至Experience Cloud登陸頁面。

![反白顯示[!UICONTROL 接受]的Microsoft許可權要求對話方塊。](../../../images/governance-privacy-security/customer-managed-keys/app-permission.png)

>[!IMPORTANT]
>
>如果您有多個[!DNL Microsoft Azure]訂閱，那麼您可能會將您的Experience Platform執行個體連線到錯誤的金鑰儲存庫。 在此情況下，您必須將CMK目錄ID的應用程式驗證URL名稱的`common`區段交換。<br>從[!DNL Microsoft Azure]應用程式的入口網站設定、目錄和訂閱頁面複製CMK目錄ID<br>![反白顯示目錄識別碼的[!DNL Microsoft Azure]應用程式入口網站設定、目錄和訂閱頁面。](../../../images/governance-privacy-security/customer-managed-keys/directory-id.png)<br>接著，將它貼到您的瀏覽器位址列。<br>![反白顯示應用程式驗證URL的「一般」區段的Google瀏覽器頁面。](../../../images/governance-privacy-security/customer-managed-keys/common-url-section.png)

### 將CMK應用程式指派給角色 {#assign-to-role}

完成驗證程式後，請導覽回您的[!DNL Azure]金鑰儲存庫，並在左側導覽中選取&#x200B;**[!DNL Access control]**。 從這裡，依次選取&#x200B;**[!DNL Add]**&#x200B;和&#x200B;**[!DNL Add role assignment]**。

![反白顯示[!DNL Add]和[!DNL Add role assignment]的[!DNL Microsoft Azure]儀表板。](../../../images/governance-privacy-security/customer-managed-keys/add-role-assignment.png)

下一個畫面會提示您選擇此指派的角色。 選取&#x200B;**[!DNL Key Vault Crypto Service Encryption User]**&#x200B;再選取&#x200B;**[!DNL Next]**&#x200B;以繼續。

>[!NOTE]
>
>如果您有[!DNL Managed-HSM Key Vault]層，則必須選取&#x200B;**[!DNL Managed HSM Crypto Service Encryption User]**&#x200B;使用者角色。

![反白顯示[!DNL Key Vault Crypto Service Encryption User]的[!DNL Microsoft Azure]儀表板。](../../../images/governance-privacy-security/customer-managed-keys/select-role.png)

在下一個畫面中，選擇&#x200B;**[!DNL Select members]**&#x200B;以在右側邊欄中開啟對話方塊。 使用搜尋列來尋找CMK應用程式的服務主體，並從清單中選取它。 完成後，選取&#x200B;**[!DNL Save]**。

>[!NOTE]
>
>如果您在清單中找不到您的應用程式，則表示您的服務主體尚未被租使用者接受。 為確保您擁有正確的許可權，請與您的[!DNL Azure]管理員或代表合作。

您可以將[!UICONTROL 客戶受管理金鑰組態]檢視上提供的[!UICONTROL 應用程式識別碼]與[!DNL Microsoft Azure]應用程式總覽上提供的[!DNL Application ID]進行比較，以驗證應用程式。

![反白顯示[!UICONTROL 應用程式識別碼]的[!UICONTROL 客戶受管理的金鑰組態]檢視。](../../../images/governance-privacy-security/customer-managed-keys/application-id.png)

驗證Azure工具所需的所有詳細資訊都包含在Experience Platform UI中。 如果許多使用者希望使用其他Azure工具來增強其監視和記錄這些應用程式對其金鑰儲存庫存取的能力，則會提供此詳細程度等級。 瞭解這些識別碼對於該目的以及協助Adobe服務存取金鑰至關重要。

## 在Experience Platform上啟用加密金鑰設定 {#send-to-adobe}

在[!DNL Azure]上安裝CMK應用程式後，您可以將加密金鑰識別碼傳送至Adobe。 在左側導覽中選取&#x200B;**[!DNL Keys]**，然後選取您要傳送的金鑰名稱。

![反白顯示[!DNL Keys]物件和金鑰名稱的Microsoft Azure儀表板。](../../../images/governance-privacy-security/customer-managed-keys/select-key.png)

選取金鑰的最新版本，其詳細資訊頁面就會顯示。 從這裡，您可以選擇設定金鑰的允許操作。

>[!IMPORTANT]
>
>金鑰允許的最小必要操作為&#x200B;**[!DNL Wrap Key]**&#x200B;和&#x200B;**[!DNL Unwrap Key]**&#x200B;許可權。 您可視需要包含[!DNL Encrypt]、[!DNL Decrypt]、[!DNL Sign]和[!DNL Verify]。

**[!UICONTROL 金鑰識別碼]**&#x200B;欄位會顯示金鑰的URI識別碼。 複製此URI值以用於下一個步驟。

![Microsoft Azure儀表板金鑰詳細資訊，其中[!DNL Permitted operations]和復本金鑰URL區段強調顯示。](../../../images/governance-privacy-security/customer-managed-keys/copy-key-url.png)

取得[!DNL Key vault URI]之後，請返回[!UICONTROL 客戶受管理的金鑰組態]檢視，並輸入描述性的&#x200B;**[!UICONTROL 組態名稱]**。 接著，將取自Azure金鑰詳細資料頁面的[!DNL Key Identifier]新增至&#x200B;**[!UICONTROL 金鑰儲存庫金鑰識別碼]**，並選取&#x200B;**[!UICONTROL 儲存]**。

![具有[!UICONTROL 設定名稱]和[!UICONTROL 金鑰儲存庫金鑰識別碼]區段的[!UICONTROL 客戶受管理金鑰組態]檢視（已強調顯示）。](../../../images/governance-privacy-security/customer-managed-keys/configuration-name.png)

您返回[!UICONTROL 加密設定儀表板]。 [!UICONTROL 客戶受管理的金鑰]組態的狀態會顯示為[!UICONTROL 處理中]。

![具有[!UICONTROL 處理]的[!UICONTROL 加密設定]儀表板在[!UICONTROL 客戶受管理的金鑰]卡上強調顯示。](../../../images/governance-privacy-security/customer-managed-keys/processing.png)

## 驗證設定的狀態 {#check-status}

允許相當長的處理時間。 若要檢查組態狀態，請返回[!UICONTROL 客戶自控金鑰組態]檢視，然後向下捲動至[!UICONTROL 組態狀態]。 進度列已進階至步驟一(3)，並說明系統正在驗證Experience Platform是否擁有金鑰和金鑰儲存庫的存取權。

CMK設定有四種可能的狀態。 具體如下：

* 步驟1：驗證Experience Platform是否能夠存取金鑰和金鑰儲存庫。
* 步驟2：金鑰儲存庫和金鑰名稱正在新增至貴組織的所有資料存放區。
* 步驟3：金鑰儲存庫和金鑰名稱已成功新增至資料存放區。
* `FAILED`：發生問題，主要與金鑰、金鑰儲存庫或多租使用者應用程式設定有關。

## 後續步驟

完成上述步驟，您已成功為Azure代管的組織啟用CMK。 現在將使用[!DNL Azure]金鑰儲存庫中的金鑰加密和解密擷取到主要資料存放區的資料。

為您的Azure託管組織啟用CMK後，監視金鑰使用情況、實施金鑰輪換原則以增強安全性，並確保符合您組織的原則。
