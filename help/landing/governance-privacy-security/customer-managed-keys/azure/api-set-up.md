---
title: 使用API為Azure設定及設定客戶自控金鑰
description: 瞭解如何使用您的Azure租使用者設定您的CMK應用程式，並將您的加密金鑰ID傳送至Adobe Experience Platform。
role: Developer
feature: API, Privacy
exl-id: c9a1888e-421f-4bb4-b4c7-968fb1d61746
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1035'
ht-degree: 1%

---

# 使用API為Azure設定及設定客戶自控金鑰

本文介紹在Adobe Experience Platform中使用API啟用客戶自控金鑰(CMK)的Azure特定指示。 如需有關如何使用Azure代管Experience Platform執行個體的UI完成此程式的說明，請參閱[UI CMK設定檔案](./ui-set-up.md)。

如需AWS的特定指示，請參閱[AWS安裝指南](../aws/ui-set-up.md)。

## 先決條件

若要在Adobe Experience Platform中檢視並瀏覽[!UICONTROL 加密]區段，您必須已建立角色，並已將[!UICONTROL 管理客戶管理的金鑰]許可權指派給該角色。 任何擁有[!UICONTROL 管理客戶管理的金鑰]許可權的使用者都可以為其組織啟用CMK。

如需在Experience Platform中指派角色和許可權的詳細資訊，請參閱[設定許可權檔案](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/configure-permissions.html?lang=zh-Hant)。

若要為Azure代管的Experience Platform執行個體啟用CMK，您的[[!DNL Azure] 金鑰儲存庫必須使用下列設定來設定](./azure-key-vault-config.md)：

* [啟用清除保護](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview#purge-protection)
* [啟用軟刪除](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview)
* [使用 [!DNL Azure] 角色型存取控制設定存取權](https://learn.microsoft.com/en-us/azure/role-based-access-control/)
* [設定 [!DNL Azure] 金鑰儲存庫](./azure-key-vault-config.md)

## 設定CMK應用程式 {#register-app}

在您設定金鑰儲存庫後，下一步是註冊將連結至您[!DNL Azure]租使用者的CMK應用程式。

### 快速入門

註冊CMK應用程式時，您必須呼叫Experience Platform API。 如需有關如何收集進行這些呼叫所需的驗證標頭的詳細資訊，請參閱[Experience Platform API驗證指南](../../../api-authentication.md)。

雖然驗證指南提供如何為必要的`x-api-key`請求標頭產生您自己的唯一值的指示，但本指南中的所有API作業都使用靜態值`acp_provisioning`。 不過，您仍必須提供您自己的`{ACCESS_TOKEN}`和`{ORG_ID}`值。

在本指南中顯示的所有API呼叫中，`platform.adobe.io`會作為根路徑，其預設值為VA7區域。 如果貴組織使用不同的地區，`platform`後面必須加上破折號和指派給貴組織的地區代碼： NLD2為`nld2`或AUS5為`aus5` （例如： `platform-aus5.adobe.io`）。 如果您不知道您組織的區域，請聯絡您的系統管理員。

### 擷取驗證URL {#fetch-authentication-url}

若要開始註冊程式，請向應用程式註冊端點發出GET請求，以擷取組織所需的驗證URL。

**要求**

```shell
curl -X GET \
  https://platform.adobe.io/data/infrastructure/manager/byok/app-registration \ 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: acp_provisioning' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**回應**

成功的回應傳回包含驗證URL的`applicationRedirectUrl`屬性。

```json
{
    "id": "byok",
    "name": "acpebae9422Caepcmkmultitenantapp",
    "applicationUri": "https://adobe.com/acpebae9422Caepcmkmultitenantapp",
    "applicationId": "e463a445-c6ac-4ca2-b36a-b5146fcf6a52",
    "applicationRedirectUrl": "https://login.microsoftonline.com/common/oauth2/authorize?response_type=code&client_id=e463a445-c6ac-4ca2-b36a-b5146fcf6a52&redirect_uri=https://adobe.com/acpebae9422Caepcmkmultitenantapp&scope=user.read"
}
```

將`applicationRedirectUrl`位址複製並貼到瀏覽器中，以開啟驗證對話方塊。 選取&#x200B;**[!DNL Accept]**&#x200B;將CMK應用程式服務主體新增至您的[!DNL Azure]租使用者。

![反白顯示[!UICONTROL 接受]的Microsoft許可權要求對話方塊。](../../../images/governance-privacy-security/customer-managed-keys/app-permission.png)

### 將CMK應用程式指派給角色 {#assign-to-role}

完成驗證程式後，請導覽回您的[!DNL Azure]金鑰儲存庫，並在左側導覽中選取&#x200B;**[!DNL Access control]**。 從這裡，依次選取&#x200B;**[!DNL Add]**&#x200B;和&#x200B;**[!DNL Add role assignment]**。

![反白顯示[!DNL Add]和[!DNL Add role assignment]的Microsoft Azure儀表板。](../../../images/governance-privacy-security/customer-managed-keys/add-role-assignment.png)

下一個畫面會提示您選擇此指派的角色。 選取&#x200B;**[!DNL Key Vault Crypto Service Encryption User]**&#x200B;再選取&#x200B;**[!DNL Next]**&#x200B;以繼續。

>[!NOTE]
>
>如果您有[!DNL Managed-HSM Key Vault]層，則必須選取&#x200B;**[!DNL Managed HSM Crypto Service Encryption User]**&#x200B;使用者角色。

![反白顯示[!DNL Key Vault Crypto Service Encryption User]的Microsoft Azure儀表板。](../../../images/governance-privacy-security/customer-managed-keys/select-role.png)

在下一個畫面中，選擇&#x200B;**[!DNL Select members]**&#x200B;以在右側邊欄中開啟對話方塊。 使用搜尋列來尋找CMK應用程式的服務主體，並從清單中選取它。 完成後，選取&#x200B;**[!DNL Save]**。

>[!NOTE]
>
>如果您在清單中找不到您的應用程式，則表示您的服務主體尚未被租使用者接受。 為確保您擁有正確的許可權，請與您的[!DNL Azure]管理員或代表合作。

## 在Experience Platform上啟用加密金鑰設定 {#send-to-adobe}

在[!DNL Azure]上安裝CMK應用程式後，您可以將加密金鑰識別碼傳送至Adobe。 在左側導覽中選取&#x200B;**[!DNL Keys]**，然後選取您要傳送的金鑰名稱。

![反白顯示[!DNL Keys]物件和金鑰名稱的Microsoft Azure儀表板。](../../../images/governance-privacy-security/customer-managed-keys/select-key.png)

選取金鑰的最新版本，其詳細資訊頁面就會顯示。 從這裡，您可以選擇設定金鑰的允許操作。

>[!IMPORTANT]
>
>金鑰允許的最小必要操作為&#x200B;**[!DNL Wrap Key]**&#x200B;和&#x200B;**[!DNL Unwrap Key]**&#x200B;許可權。 您可視需要包含[!DNL Encrypt]、[!DNL Decrypt]、[!DNL Sign]和[!DNL Verify]。

**[!UICONTROL 金鑰識別碼]**&#x200B;欄位會顯示金鑰的URI識別碼。 複製此URI值以用於下一個步驟。

![Microsoft Azure儀表板金鑰詳細資訊，其中[!DNL Permitted operations]和復本金鑰URL區段強調顯示。](../../../images/governance-privacy-security/customer-managed-keys/copy-key-url.png)

取得金鑰儲存庫URI後，您可以使用POST請求將其傳送到CMK設定端點。

>[!NOTE]
>
>Adobe中只會儲存金鑰儲存庫和金鑰名稱，不會儲存金鑰版本。

**要求**

+++ 將金鑰儲存庫URI傳送至CMK設定端點的範例要求。

```shell
curl -X POST \
  https://platform.adobe.io/data/infrastructure/manager/customer/config \ 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: acp_provisioning' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -d '{
        "name": "Config1",
        "type": "BYOK_CONFIG",
        "imsOrgId": "{ORG_ID}",
        "configData": {
          "providerType": "AZURE_KEYVAULT",
          "keyVaultKeyIdentifier": "https://adobecmkexample.vault.azure.net/keys/adobeCMK-key/7c1d50lo28234cc895534c00d7eb4eb4"
        }
      }'
```

| 屬性 | 說明 |
| --- | --- |
| `name` | 設定的名稱。 請確定您記得這個值，因為在[之後的步驟](#check-status)中需要檢查組態狀態。 值區分大小寫。 |
| `type` | 設定型別。 必須設定為`BYOK_CONFIG`。 |
| `imsOrgId` | 您的組織ID。 此ID的值必須與`x-gw-ims-org-id`標頭下提供的值相同。 |
| `configData` | 此屬性包含有關設定的下列詳細資訊：<ul><li>`providerType`：必須設定為`AZURE_KEYVAULT`。</li><li>`keyVaultKeyIdentifier`：您複製[early](#send-to-adobe)的金鑰儲存庫URI。</li></ul> |

+++

**回應**

+++ 成功的回應會傳回設定工作的詳細資訊。

```json
{
  "id": "4df7886b-a122-4391-880b-47888d5c5b92",
  "config": {
    "configData": {
      "keyVaultUri": "https://adobecmkexample.vault.azure.net",
      "keyVaultKeyIdentifier": "https://adobecmkexample.vault.azure.net/keys/adobeCMK-key/7c1d50lo28234cc895534c00d7eb4eb4",
      "keyVersion": "7c1d50lo28234cc895534c00d7eb4eb4",
      "keyName": "Config1",
      "providerType": "AZURE_KEYVAULT"
    },
    "name": "acpcf978863Aaepcmkmultitenantapp",
    "type": "BYOK_CONFIG",
    "imsOrgId": "{ORG_ID}",
    "status": "NEW"
  },
  "status": "CREATED"
}
```

+++

工作應在幾分鐘內完成處理。

## 驗證設定的狀態 {#check-status}

若要檢查設定要求的狀態，您可以提出GET要求。

**要求**

您必須將您要檢查之設定的`name`附加至路徑（以下範例中為`config1`），並包含設定為`BYOK_CONFIG`的`configType`查詢引數。

+++ 檢查設定要求狀態的範例要求。

```shell
curl -X GET \
  https://platform.adobe.io/data/infrastructure/manager/customer/config/config1?configType=BYOK_CONFIG \ 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: acp_provisioning' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

+++

**回應**

+++ 成功的回應會傳回工作的狀態。

```json
{
  "name": "acpcf978863Aaepcmkmultitenantapp",
  "type": "BYOK_CONFIG",
  "status": "COMPLETED",
  "configData": {
    "keyVaultUri": "https://adobecmkexample.vault.azure.net",
    "keyVaultKeyIdentifier": "https://adobecmkexample.vault.azure.net/keys/adobeCMK-key/7c1d50lo28234cc895534c00d7eb4eb4",
    "keyVersion": "7c1d50lo28234cc895534c00d7eb4eb4",
    "keyName": "Config1",
    "providerType": "AZURE_KEYVAULT"
  },
  "imsOrgId": "{ORG_ID}",
  "subscriptionId": "cf978863-7325-47b1-8fd9-554b9fdb6c36",
  "id": "4df7886b-a122-4391-880b-47888d5c5b92",
  "rowType": "BYOK_KEY"
}
```

+++

`status`屬性可以有以下含義的四個值之一：

1. `RUNNING`：驗證Experience Platform是否可以存取金鑰和金鑰儲存庫。
1. `UPDATE_EXISTING_RESOURCES`：系統正在將金鑰儲存庫和金鑰名稱新增至貴組織所有沙箱的資料存放區。
1. `COMPLETED`：金鑰儲存庫和金鑰名稱已成功新增至資料存放區。
1. `FAILED`：發生問題，主要與金鑰、金鑰儲存庫或多租使用者應用程式設定有關。

## 後續步驟

完成上述步驟，您已成功為組織啟用CMK。 對於Azure代管的Experience Platform執行個體，現在將使用[!DNL Azure]金鑰儲存庫中的金鑰加密和解密擷取到主要資料存放區的資料。

若要進一步瞭解Adobe Experience Platform中的資料加密，請參閱[加密檔案](../../encryption.md)。
