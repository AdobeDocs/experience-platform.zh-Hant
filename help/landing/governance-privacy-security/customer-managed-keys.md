---
title: 客戶管理的密鑰在Adobe Experience Platform
description: 瞭解如何為儲存在Adobe Experience Platform的資料設定自己的加密密鑰。
exl-id: cd33e6c2-8189-4b68-a99b-ec7fccdc9b91
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1617'
ht-degree: 0%

---

# 客戶管理的Adobe Experience Platform密鑰

在Adobe Experience Platform儲存的資料使用系統級密鑰在靜止狀態下進行加密。 如果您使用的是構建在平台之上的應用程式，則可以選擇使用您自己的加密密鑰，從而更好地控制資料安全。

>[!NOTE]
>
>使用CMK對Adobe Experience Platform資料湖和Profile儲存(CosmosDB)中的資料進行加密。

本文檔介紹在平台中啟用客戶管理密鑰(CMK)功能的過程。

## 先決條件

為啟用CMK, [!DNL Azure] 密鑰保管庫必須配置以下設定：

* [啟用清除保護](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview#purge-protection)
* [啟用軟刪除](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview)
* [配置訪問 [!DNL Azure] 基於角色的訪問控制](https://learn.microsoft.com/en-us/azure/role-based-access-control/)

## 流程摘要

CMK包括在Healthcare Shield和Privacy and Security Shield產品中，可避免Adobe。 在您的組織為其中一項產品購買許可證後，您可以開始設定該功能的一次性過程。

>[!WARNING]
>
>設定CMK後，無法恢復為系統管理的密鑰。 您負責安全地管理您的密鑰，並提供對您的密鑰保管庫、密鑰和CMK應用程式的訪問 [!DNL Azure] 防止丟失對資料的訪問。

該過程如下：

1. [配置 [!DNL Azure] 密鑰保管庫](#create-key-vault) 根據組織的策略 [生成加密密鑰](#generate-a-key) 最終將與Adobe分享。
1. 使用API調用 [設定CMK應用](#register-app) 和 [!DNL Azure] 租客。
1. 使用API調用 [將加密密鑰ID發送到Adobe](#send-to-adobe) 並啟動功能啟用過程。
1. [檢查配置的狀態](#check-status) 驗證CMK是否已啟用。

完成安裝過程後，所有沙箱上的所有資料都將使用您的 [!DNL Azure] 鍵設定。 要使用CMK，您將利用 [!DNL Microsoft Azure] 可能是其 [公共預覽](https://azure.microsoft.com/en-ca/support/legal/preview-supplemental-terms/)。

## 配置 [!DNL Azure] 密鑰保管庫 {#create-key-vault}

CMK僅支援來自 [!DNL Microsoft Azure] 密鑰保管庫。 要開始，您必須使用 [!DNL Azure] 建立新企業帳戶，或使用現有企業帳戶並按照以下步驟建立密鑰保管庫。

>[!IMPORTANT]
>
>僅針對 [!DNL Azure] 支援密鑰保管庫。 [!DNL Azure Managed HSM]。 [!DNL Azure Dedicated HSM] 和 [!DNL Azure Payments HSM] 不支援。 請參閱 [[!DNL Azure] 文檔](https://learn.microsoft.com/en-us/azure/security/fundamentals/key-management#azure-key-management-services) 的子菜單。

>[!NOTE]
>
>下面的文檔僅介紹建立密鑰保管庫的基本步驟。 在本指南之外，您應根據組織的策略配置密鑰保管庫。

登錄到 [!DNL Azure] 入口並使用搜索欄查找 **[!DNL Key vaults]** 清單下。

![搜索和選擇關鍵保管庫](../images/governance-privacy-security/customer-managed-keys/access-key-vaults.png)

的 **[!DNL Key vaults]** 的子菜單。 從此處，選擇 **[!DNL Create]**。

![建立密鑰保管庫](../images/governance-privacy-security/customer-managed-keys/create-key-vault.png)

使用提供的表單填寫密鑰保管庫的基本詳細資訊，包括名稱和分配的資源組。

>[!WARNING]
>
>雖然大多數選項可以保留為其預設值， **確保啟用軟刪除和清除保護選項**。 如果不開啟這些功能，則刪除密鑰保管庫時可能會丟失對資料的訪問權限。
>
>![啟用清除保護](../images/governance-privacy-security/customer-managed-keys/basic-config.png)

在此處，繼續執行密鑰保管庫建立工作流，並根據組織的策略配置不同的選項。

一旦您到達 **[!DNL Review + create]** 步驟，您可以在密鑰保管庫通過驗證時查看其詳細資訊。 驗證通過後，選擇 **[!DNL Create]** 來完成此過程。

![密鑰保管庫的基本配置](../images/governance-privacy-security/customer-managed-keys/finish-creation.png)

### 配置網路選項

如果將密鑰保管庫配置為限制對某些虛擬網路的公共訪問或完全禁用公共訪問，則必須授予Microsoft防火牆例外。

選擇 **[!DNL Networking]** 的子菜單。 下 **[!DNL Firewalls and virtual networks]**，選中複選框 **[!DNL Allow trusted Microsoft services to bypass this firewall]**，然後選擇 **[!DNL Apply]**。

![密鑰保管庫的基本配置](../images/governance-privacy-security/customer-managed-keys/networking.png)

### 生成密鑰 {#generate-a-key}

建立密鑰保管庫後，可以生成新密鑰。 導航到 **[!DNL Keys]** 頁籤 **[!DNL Generate/Import]**。

![生成密鑰](../images/governance-privacy-security/customer-managed-keys/view-keys.png)

使用提供的表單提供密鑰的名稱，然後選擇 **RSA** 按鈕。 至少， **[!DNL RSA key size]** 必須至少 **3072** 所需的位 [!DNL Cosmos DB]。 [!DNL Azure Data Lake Storage] 與RSA 3027相容。

>[!NOTE]
>
>記住為密鑰提供的名稱，因為在以後的步驟中， [將密鑰發送到Adobe](#send-to-adobe)。

使用其餘控制項配置要生成或導入的鍵。 完成後，選擇 **[!DNL Create]**。

![配置密鑰](../images/governance-privacy-security/customer-managed-keys/configure-key.png)

配置的密鑰將出現在保管庫的密鑰清單中。

![已添加密鑰](../images/governance-privacy-security/customer-managed-keys/key-added.png)

## 設定CMK應用 {#register-app}

配置密鑰保管庫後，下一步是註冊將連結到您的 [!DNL Azure] 租客。

### 快速入門

註冊CMK應用需要您調用平台API。 有關如何收集進行這些調用所需的身份驗證標頭的詳細資訊，請參閱 [平台API驗證指南](../../landing/api-authentication.md)。

同時，身份驗證指南提供了有關如何為所需的產品生成您自己的唯一值的說明 `x-api-key` 請求標頭，本指南中的所有API操作都使用靜態值 `acp_provisioning` 的雙曲餘切值。 您仍必須為 `{ACCESS_TOKEN}` 和 `{ORG_ID}`的雙曲餘切值。

在本指南中顯示的所有API調用中， `platform.adobe.io` 用作預設為VA7區域的根路徑。 如果您的組織使用不同的區域， `platform` 必須跟著一個破折號，並且分配給您的組織的區域代碼： `nld2` 對於NLD2或 `aus5` 對於AUS5(例如： `platform-aus5.adobe.io`)。 如果您不知道您組織的區域，請與系統管理員聯繫。

### 獲取驗證URL

要啟動註冊過程，請向應用註冊終結點發出GET請求，以獲取組織所需的身份驗證URL。

**要求**

```shell
curl -X GET \
  https://platform.adobe.io/data/infrastructure/manager/byok/app-registration \ 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: acp_provisioning' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**回應**

成功的響應返回 `applicationRedirectUrl` 屬性，包含驗證URL。

```json
{
    "id": "byok",
    "name": "acpebae9422Caepcmkmultitenantapp",
    "applicationUri": "https://adobe.com/acpebae9422Caepcmkmultitenantapp",
    "applicationId": "e463a445-c6ac-4ca2-b36a-b5146fcf6a52",
    "applicationRedirectUrl": "https://login.microsoftonline.com/common/oauth2/authorize?response_type=code&client_id=e463a445-c6ac-4ca2-b36a-b5146fcf6a52&redirect_uri=https://adobe.com/acpebae9422Caepcmkmultitenantapp&scope=user.read"
}
```

複製並貼上 `applicationRedirectUrl` 地址到瀏覽器以開啟驗證對話框。 選擇 **[!DNL Accept]** 將CMK應用服務主體添加到 [!DNL Azure] 租客。

![接受權限請求](../images/governance-privacy-security/customer-managed-keys/app-permission.png)

### 將CMK應用分配給角色 {#assign-to-role}

完成身份驗證過程後，導航回您的 [!DNL Azure] 密鑰保管庫並選擇 **[!DNL Access control]** 的子菜單。 從此處，選擇 **[!DNL Add]** 後跟 **[!DNL Add role assignment]**。

![添加角色分配](../images/governance-privacy-security/customer-managed-keys/add-role-assignment.png)

下一個螢幕將提示您為此分配選擇角色。 選擇 **[!DNL Key Vault Crypto Service Encryption User]** 選擇 **[!DNL Next]** 繼續。

![選擇角色](../images/governance-privacy-security/customer-managed-keys/select-role.png)

在下一個螢幕上，選擇 **[!DNL Select members]** 開啟右欄的對話框。 使用搜索欄查找CMK應用程式的服務主體並從清單中選擇它。 完成後，選擇 **[!DNL Save]**。

>[!NOTE]
>
>如果在清單中找不到您的應用程式，則您的服務主體尚未被接受到您的租戶中。 請與 [!DNL Azure] 管理員或代表，確保您擁有正確的權限。

## 在Experience Platform上啟用加密密鑰配置 {#send-to-adobe}

在上安裝CMK應用後 [!DNL Azure]，您可以將加密密鑰標識符發送到Adobe。 選擇 **[!DNL Keys]** 的下一頁。

![選擇鍵](../images/governance-privacy-security/customer-managed-keys/select-key.png)

選擇密鑰的最新版本，並顯示其詳細資訊頁面。 在此處，您可以根據需要為密鑰配置允許的操作。 至少，密鑰必須授予 **[!DNL Wrap Key]** 和 **[!DNL Unwrap Key]** 權限。

的 **[!UICONTROL 密鑰標識符]** 欄位顯示鍵的URI標識符。 複製此URI值，以便在下一步中使用。

![複製密鑰URL](../images/governance-privacy-security/customer-managed-keys/copy-key-url.png)

獲得密鑰保管庫URI後，可以使用POST請求將其發送到CMK配置終結點。

>[!NOTE]
>
>只有密鑰保管庫和密鑰名稱與Adobe一起儲存，而不是密鑰版本。

**要求**

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
| `name` | 配置的名稱。 確保記住此值，因為將要求在 [後續步驟](#check-status)。 值區分大小寫。 |
| `type` | 配置類型。 必須設定為 `BYOK_CONFIG`。 |
| `imsOrgId` | 您的組織 ID。此值必須與 `x-gw-ims-org-id` 標題。 |
| `configData` | 包含有關配置的以下詳細資訊：<ul><li>`providerType`:必須設定為 `AZURE_KEYVAULT`。</li><li>`keyVaultKeyIdentifier`:複製的密鑰保管庫URI [早](#send-to-adobe)。</li></ul> |

**回應**

成功的響應返回配置作業的詳細資訊。

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
    "imsOrgId": "{IMS_ORG}",
    "status": "NEW"
  },
  "status": "CREATED"
}
```

作業應在幾分鐘內完成處理。

## 驗證配置的狀態 {#check-status}

要檢查配置請求的狀態，可以發出GET請求。

**要求**

必須追加 `name` 要檢查到路徑的配置(`config1` )，並包括 `configType` 查詢參數設定為 `BYOK_CONFIG`。

```shell
curl -X GET \
  https://platform.adobe.io/data/infrastructure/manager/customer/config/config1?configType=BYOK_CONFIG \ 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: acp_provisioning' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**回應**

成功的響應返回作業的狀態。

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
  "imsOrgId": "{IMS_ORG}",
  "subscriptionId": "cf978863-7325-47b1-8fd9-554b9fdb6c36",
  "id": "4df7886b-a122-4391-880b-47888d5c5b92",
  "rowType": "BYOK_KEY"
}
```

的 `status` attribute可具有以下含義的四個值之一：

1. `RUNNING`:驗證平台是否能夠訪問密鑰和密鑰保管庫。
1. `UPDATE_EXISTING_RESOURCES`:系統正在將密鑰保管庫和密鑰名稱添加到組織中所有沙箱中的資料儲存中。
1. `COMPLETED`:密鑰保管庫和密鑰名稱已添加到資料儲存中。
1. `FAILED`:出現問題，主要與密鑰、密鑰保管庫或多租戶應用程式設定有關。

## 後續步驟

通過完成上述步驟，您已成功為組織啟用CMK。 現在，將使用您的平台中的密鑰加密和解密已接收到的資料 [!DNL Azure] 密鑰保管庫。 如果要撤消對資料的平台訪問權限，可以從中的密鑰保管庫中刪除與應用程式關聯的用戶角色 [!DNL Azure]。

禁用對應用程式的訪問後，可能需要幾分鐘到24小時的時間，才能使資料在平台中不再可訪問。 當重新啟用對應用程式的訪問時，同一時間延遲將再次對資料進行可用。

>[!WARNING]
>
>一旦禁用了密鑰保管庫、密鑰或CMK應用，且平台中的資料不再可訪問，則與該資料相關的任何下游操作將不再可能。 在對配置進行任何更改之前，請確保您瞭解撤消對資料的平台訪問的下游影響。
