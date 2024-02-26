---
title: 使用API設定及設定客戶自控金鑰
description: 瞭解如何使用您的Azure租使用者設定您的CMK應用程式，並將您的加密金鑰ID傳送至Adobe Experience Platform。
exl-id: c9a1888e-421f-4bb4-b4c7-968fb1d61746
source-git-commit: 4f08e8fcc8d53b981af60226f1397a1d1ac4d8dc
workflow-type: tm+mt
source-wordcount: '1002'
ht-degree: 1%

---

# 使用API設定及設定客戶自控金鑰

本文介紹在Adobe Experience Platform中使用API啟用客戶自控金鑰(CMK)功能的程式。 如需有關如何使用UI完成此程式的說明，請參閱 [UI CMK設定檔案](./ui-set-up.md).

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

註冊CMK應用程式時，您必須呼叫平台API。 如需有關如何收集進行這些呼叫所需的驗證標題的詳細資訊，請參閱 [平台API驗證指南](../../api-authentication.md).

而驗證指南會提供如何針對所需產生您自己的唯一值的指示 `x-api-key` 請求標頭，本指南中的所有API作業都使用靜態值 `acp_provisioning` 而非。 您仍然必須提供自己的值 `{ACCESS_TOKEN}` 和 `{ORG_ID}`，但是。

在本指南中顯示的所有API呼叫中， `platform.adobe.io` 作為根路徑，預設為VA7區域。 如果您的組織使用不同的地區， `platform` 後面必須跟有破折號和指派給您的組織的區域代碼： `nld2` 適用於NLD2或 `aus5` 適用於AUS5 (例如： `platform-aus5.adobe.io`)。 如果您不知道您組織的區域，請聯絡您的系統管理員。

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

成功的回應會傳回 `applicationRedirectUrl` 屬性，包含驗證URL。

```json
{
    "id": "byok",
    "name": "acpebae9422Caepcmkmultitenantapp",
    "applicationUri": "https://adobe.com/acpebae9422Caepcmkmultitenantapp",
    "applicationId": "e463a445-c6ac-4ca2-b36a-b5146fcf6a52",
    "applicationRedirectUrl": "https://login.microsoftonline.com/common/oauth2/authorize?response_type=code&client_id=e463a445-c6ac-4ca2-b36a-b5146fcf6a52&redirect_uri=https://adobe.com/acpebae9422Caepcmkmultitenantapp&scope=user.read"
}
```

複製並貼上 `applicationRedirectUrl` 位址放入瀏覽器以開啟驗證對話方塊。 選取 **[!DNL Accept]** 若要將CMK應用程式服務主體新增至 [!DNL Azure] 租使用者。

![Microsoft許可權要求對話方塊，其中包含 [!UICONTROL Accept] 反白顯示。](../../images/governance-privacy-security/customer-managed-keys/app-permission.png)

### 將CMK應用程式指派給角色 {#assign-to-role}

完成驗證程式後，請導覽回 [!DNL Azure] 金鑰儲存庫及選擇 **[!DNL Access control]** ，位於左側導覽器中。 從這裡，選擇 **[!DNL Add]** 後面接著 **[!DNL Add role assignment]**.

![Microsoft Azure控制面板，具有 [!DNL Add] 和 [!DNL Add role assignment] 反白顯示。](../../images/governance-privacy-security/customer-managed-keys/add-role-assignment.png)

下一個畫面會提示您選擇此指派的角色。 選取 **[!DNL Key Vault Crypto Service Encryption User]** 在選取之前 **[!DNL Next]** 以繼續。

>[!NOTE]
>
>如果您擁有 [!DNL Managed-HSM Key Vault] 層，則必須選取 **[!DNL Managed HSM Crypto Service Encryption User]** 使用者角色。

![Microsoft Azure控制面板具有 [!DNL Key Vault Crypto Service Encryption User] 反白顯示。](../../images/governance-privacy-security/customer-managed-keys/select-role.png)

在下一個畫面，選擇 **[!DNL Select members]** 以開啟右側邊欄中的對話方塊。 使用搜尋列來尋找CMK應用程式的服務主體，並從清單中選取它。 完成後，選取 **[!DNL Save]**.

>[!NOTE]
>
>如果您在清單中找不到您的應用程式，則表示您的服務主體尚未被租使用者接受。 為確保您擁有正確的許可權，請使用您的 [!DNL Azure] 管理員或代表。

## 在Experience Platform上啟用加密金鑰設定 {#send-to-adobe}

在上安裝CMK應用程式後 [!DNL Azure]，即可將加密金鑰識別碼傳送至Adobe。 選取 **[!DNL Keys]** ，然後輸入要傳送的金鑰名稱。

![Microsoft Azure控制面板具有 [!DNL Keys] 物件和醒目提示的金鑰名稱。](../../images/governance-privacy-security/customer-managed-keys/select-key.png)

選取金鑰的最新版本，其詳細資訊頁面就會顯示。 從這裡，您可以選擇設定金鑰的允許操作。

>[!IMPORTANT]
>
>金鑰允許的最小必要操作為 **[!DNL Wrap Key]** 和 **[!DNL Unwrap Key]** 許可權。 您可以包括 [!DNL Encrypt]， [!DNL Decrypt]， [!DNL Sign]、和 [!DNL Verify] 您想要的話。

此 **[!UICONTROL 金鑰識別碼]** 欄位會顯示金鑰的URI識別碼。 複製此URI值以用於下一個步驟。

![Microsoft Azure儀表板金鑰詳細資訊，包含 [!DNL Permitted operations] 和複製金鑰URL區段強調顯示。](../../images/governance-privacy-security/customer-managed-keys/copy-key-url.png)

取得金鑰儲存庫URI後，您可以使用POST請求將其傳送到CMK設定端點。

>[!NOTE]
>
>只有金鑰儲存庫和金鑰名稱與Adobe一起儲存，而不是金鑰版本。

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
| `name` | 設定的名稱。 請確定您記住此值，因為若要檢查設定的狀態， [後續步驟](#check-status). 值區分大小寫。 |
| `type` | 設定型別。 必須設為 `BYOK_CONFIG`. |
| `imsOrgId` | 您的組織ID。 此ID的值必須與 `x-gw-ims-org-id` 標頭。 |
| `configData` | 此屬性包含有關設定的下列詳細資訊：<ul><li>`providerType`：必須設為 `AZURE_KEYVAULT`.</li><li>`keyVaultKeyIdentifier`：您複製的金鑰儲存庫URI [較早](#send-to-adobe).</li></ul> |

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

您必須附加 `name` 要檢查的設定的路徑(`config1` （在以下範例中）並包含 `configType` 查詢引數設為 `BYOK_CONFIG`.

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

此 `status` attribute可以有四個值之一，其含義如下：

1. `RUNNING`：驗證平台能否存取金鑰和金鑰儲存庫。
1. `UPDATE_EXISTING_RESOURCES`：系統會將金鑰儲存庫和金鑰名稱新增至組織中所有沙箱內的資料存放區。
1. `COMPLETED`：金鑰儲存庫和金鑰名稱已成功新增到資料存放區。
1. `FAILED`：發生問題，主要與金鑰、金鑰儲存庫或多租使用者應用程式設定有關。

## 後續步驟

完成上述步驟，您已成功為組織啟用CMK。 現在，您會使用中的金鑰，將內嵌至主要資料存放區的資料加密和解密。 [!DNL Azure] 金鑰儲存庫。 若要進一步瞭解Adobe Experience Platform中的資料加密，請參閱 [加密檔案](../encryption.md).
