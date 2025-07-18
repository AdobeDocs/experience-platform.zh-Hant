---
title: 設定客戶自控金鑰的Azure金鑰儲存庫
description: 瞭解如何使用Azure建立新的企業帳戶，或使用現有的企業帳戶並建立金鑰儲存庫。
role: Developer
feature: Privacy
exl-id: 670e3ca3-a833-4b28-9ad4-73685fa5d74d
source-git-commit: c920f78363ee5f040964dbd3a0d0815474094b07
workflow-type: tm+mt
source-wordcount: '675'
ht-degree: 0%

---

# 設定客戶自控金鑰的[!DNL Azure]金鑰儲存庫

客戶自控金鑰(CMK)支援來自[!DNL Microsoft Azure]金鑰儲存庫和AWS [!DNL Key Management Service (KMS)]的金鑰。 如果您的實作託管於[!DNL Azure]，請依照下列步驟建立金鑰儲存庫。 如需AWS代管的實作，請參閱[AWS KMS設定指南](../aws/configure-kms.md)。

>[!IMPORTANT]
>
>僅支援[!DNL Azure]金鑰儲存庫的標準、進階及受管理的HSM層級。 不支援[!DNL Azure Dedicated HSM]和[!DNL Azure Payments HSM]。 請參閱[[!DNL Azure] 檔案](https://learn.microsoft.com/en-us/azure/security/fundamentals/key-management#azure-key-management-services)，以取得所提供金鑰管理服務的詳細資訊。

>[!NOTE]
>
>以下檔案僅涵蓋建立金鑰儲存庫的基本步驟。 在本指引之外，您應根據組織的原則設定金鑰儲存庫。

登入[!DNL Azure]入口網站，並使用搜尋列在服務清單下尋找&#x200B;**[!DNL Key vaults]**。

![搜尋結果中反白顯示[!DNL Key vaults]的[!DNL Microsoft Azure]搜尋功能。](../../../images/governance-privacy-security/customer-managed-keys/access-key-vaults.png)

選取服務後會顯示&#x200B;**[!DNL Key vaults]**&#x200B;頁面。 從此處選取&#x200B;**[!DNL Create]**。

![ [!DNL Microsoft Azure]中的[!DNL Key vaults]儀表板已反白顯示[!DNL Create]。](../../../images/governance-privacy-security/customer-managed-keys/create-key-vault.png)

使用提供的表單，填寫「金鑰儲存庫」的基本詳細資訊，包括名稱和指定的資源群組。

>[!WARNING]
>
>雖然大多數選項可以保留為其預設值，但&#x200B;**請確定您已啟用軟刪除和清除保護選項**。 如果您未開啟這些功能，則在刪除金鑰儲存庫時，您可能會失去對資料的存取權。
>
>![反白顯示具有軟刪除和清除保護的[!DNL Microsoft Azure] [!DNL Create a Key Vault]工作流程。](../../../images/governance-privacy-security/customer-managed-keys/basic-config.png)

從這裡，繼續進行Key Vault建立工作流程，並根據您組織的原則設定不同選項。

一旦您到達&#x200B;**[!DNL Review + create]**&#x200B;步驟，您可以在金鑰儲存庫進行驗證時檢視其詳細資訊。 驗證通過後，選取&#x200B;**[!DNL Create]**&#x200B;以完成程式。

![Microsoft Azure Key儲存庫檢閱並建立反白顯示的「建立」頁面。](../../../images/governance-privacy-security/customer-managed-keys/finish-creation.png)

## 設定存取權 {#configure-access}

接下來，為您的金鑰儲存庫啟用Azure角色型存取控制。 在左側導覽的[!DNL Settings]區段中選取&#x200B;**[!DNL Access configuration]**，然後選取&#x200B;**[!DNL Azure role-based access control]**&#x200B;以啟用設定。 此步驟至關重要，因為稍後必須將CMK應用程式與Azure角色相關聯。 指派角色記錄在[API](./api-set-up.md#assign-to-role)和[UI](./ui-set-up.md#assign-to-role)工作流程中。

![反白顯示[!DNL Access configuration]和[!DNL Azure role-based access control]的[!DNL Microsoft Azure]儀表板。](../../../images/governance-privacy-security/customer-managed-keys/access-configuration.png)

## 設定網路選項 {#configure-network-options}

如果您的金鑰儲存庫設定為限制特定虛擬網路的公開存取或完全停用公開存取，您必須授予[!DNL Microsoft]防火牆例外。

在左側導覽中選取&#x200B;**[!DNL Networking]**。 在&#x200B;**[!DNL Firewalls and virtual networks]**&#x200B;底下，選取核取方塊&#x200B;**[!DNL Allow trusted Microsoft services to bypass this firewall]**，然後選取&#x200B;**[!DNL Apply]**。

>[!NOTE]
>
>如果您的金鑰儲存庫使用受限制的網路存取，Adobe建議您新增下列靜態IP位址： `20.88.123.53`。 新增此IP位址可讓Adobe服務更有效率地監控連線，並在偵測到存取問題時提供平台內警報。
>
>若要進一步瞭解何時允許列出Adobe的IP位址、警示如何運作以及如何回應金鑰存取失敗通知，請參閱[設定Azure CMK的警示和IP存取](./alerts-and-ip-access.md)。
>
>如果您的金鑰儲存庫已設定為允許公用網路存取，則不需要執行進一步的動作。

![反白顯示[!DNL Microsoft Azure]的[!DNL Networking]索引標籤（包含[!DNL Networking]和[!DNL Allow trusted Microsoft surfaces to bypass this firewall]例外狀況）。](../../../images/governance-privacy-security/customer-managed-keys/networking.png)

### 產生金鑰 {#generate-a-key}

建立「金鑰儲存庫」後，即可產生新的金鑰。 瀏覽至&#x200B;**[!DNL Keys]**&#x200B;索引標籤並選取&#x200B;**[!DNL Generate/Import]**。

![反白顯示[!DNL Generate import]的[!DNL Azure]的[!DNL Keys]標籤。](../../../images/governance-privacy-security/customer-managed-keys/view-keys.png)

使用提供的表單提供金鑰的名稱，然後為金鑰型別選取&#x200B;**RSA**&#x200B;或&#x200B;**RSA-HSM**。 針對[!DNL Azure]代管的實作，**[!DNL RSA key size]**&#x200B;至少必須是&#x200B;**3072**&#x200B;位元（如[!DNL Azure Cosmos DB]所需）。 [!DNL Azure Data Lake Storage]也與RSA 3027相容。

>[!NOTE]
>
>請記住您為金鑰提供的名稱，因為將金鑰傳送至Adobe是必要的。

使用剩餘的控制項來設定您想要產生或匯入的金鑰。 完成後，選取&#x200B;**[!DNL Create]**。

![反白顯示[!DNL 3072]位元的[!DNL Create a key]儀表板。](../../../images/governance-privacy-security/customer-managed-keys/configure-key.png)

已設定的金鑰會出現在儲存庫的金鑰清單中。

![金鑰名稱反白顯示的[!DNL Keys]工作區。](../../../images/governance-privacy-security/customer-managed-keys/key-added.png)

## 後續步驟

若要繼續設定客戶自控金鑰功能的一次性程式，請遵循平台託管環境的設定指南：

- 針對[!DNL Azure]，請使用[API](./api-set-up.md)或[UI](./ui-set-up.md)安裝指南。
- 若為AWS，請參閱[AWS設定KMS指南](../aws/configure-kms.md)和[UI設定指南](../aws/ui-set-up.md)。
