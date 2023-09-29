---
title: 設定Azure金鑰儲存庫
description: 瞭解如何使用Azure建立新的企業帳戶，或使用現有的企業帳戶並建立金鑰儲存庫。
source-git-commit: a0df05cde19e97d4abdad7abd19eafea8efe1096
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 0%

---

# 設定 [!DNL Azure] 金鑰儲存庫

客戶自控金鑰(CMK)僅支援來自 [!DNL Microsoft Azure] 金鑰儲存庫。 若要開始使用，您必須使用 [!DNL Azure] 建立新的企業帳戶，或使用現有的企業帳戶，然後依照下列步驟建立金鑰儲存庫。

>[!IMPORTANT]
>
>僅限高階和標準服務層級 [!DNL Azure] 支援金鑰儲存庫。 [!DNL Azure Managed HSM]， [!DNL Azure Dedicated HSM] 和 [!DNL Azure Payments HSM] 不受支援。 請參閱 [[!DNL Azure] 檔案](https://learn.microsoft.com/en-us/azure/security/fundamentals/key-management#azure-key-management-services) 以取得所提供的金鑰管理服務的詳細資訊。

>[!NOTE]
>
>以下檔案僅涵蓋建立金鑰儲存庫的基本步驟。 在本指引之外，您應根據組織的原則設定金鑰儲存庫。

登入 [!DNL Azure] 入口網站，並使用搜尋列來尋找 **[!DNL Key vaults]** 在服務清單底下。

![中的搜尋功能 [!DNL Microsoft Azure] 替換為 [!DNL Key vaults] 在搜尋結果中反白顯示。](../../images/governance-privacy-security/customer-managed-keys/access-key-vaults.png)

此 **[!DNL Key vaults]** 頁面會在選取服務後顯示。 從這裡，選擇 **[!DNL Create]**.

![此 [!DNL Key vaults] 中的儀表板 [!DNL Microsoft Azure] 替換為 [!DNL Create] 反白顯示。](../../images/governance-privacy-security/customer-managed-keys/create-key-vault.png)

使用提供的表單，填寫「金鑰儲存庫」的基本詳細資訊，包括名稱和指定的資源群組。

>[!WARNING]
>
>雖然大多數選項都可保留為預設值， **請務必啟用「軟刪除」和「清除保護」選項**. 如果您未開啟這些功能，則在刪除金鑰儲存庫時，您可能會失去對資料的存取權。
>
>![此 [!DNL Microsoft Azure] [!DNL Create a Key Vault] 強調軟刪除和清除保護的工作流程。](../../images/governance-privacy-security/customer-managed-keys/basic-config.png)

從這裡，繼續進行Key Vault建立工作流程，並根據您組織的原則設定不同選項。

一旦您到達 **[!DNL Review + create]** 步驟，您可以在金鑰儲存庫進行驗證時檢閱其詳細資訊。 驗證通過後，選取 **[!DNL Create]** 以完成程式。

![Microsoft Azure Key儲存庫檢閱和建立頁面時，反白顯示「建立」。](../../images/governance-privacy-security/customer-managed-keys/finish-creation.png)

## 設定網路選項 {#configure-network-options}

如果您的金鑰儲存庫設定為限制對特定虛擬網路的公開存取或完全停用公開存取，您必須授予 [!DNL Microsoft] 防火牆例外。

選取 **[!DNL Networking]** ，位於左側導覽器中。 在 **[!DNL Firewalls and virtual networks]**，選取核取方塊 **[!DNL Allow trusted Microsoft services to bypass this firewall]**，然後選取 **[!DNL Apply]**.

![此 [!DNL Networking] 標籤之 [!DNL Microsoft Azure] 替換為 [!DNL Networking] 和 [!DNL Allow trusted Microsoft surfaces to bypass this firewall] 反白顯示例外狀況。](../../images/governance-privacy-security/customer-managed-keys/networking.png)

### 產生金鑰 {#generate-a-key}

建立「金鑰儲存庫」後，即可產生新的金鑰。 導覽至 **[!DNL Keys]** 標籤並選取 **[!DNL Generate/Import]**.

![此 [!DNL Keys] 標籤之 [!DNL Azure] 替換為 [!DNL Generate import] 反白顯示。](../../images/governance-privacy-security/customer-managed-keys/view-keys.png)

使用提供的表單提供索引鍵的名稱，然後選取 **RSA** 鍵型別。 至少 **[!DNL RSA key size]** 至少必須是 **3072** 位元（視需求） [!DNL Cosmos DB]. [!DNL Azure Data Lake Storage] 也與RSA 3027相容。

>[!NOTE]
>
>記住您為金鑰提供的名稱，因為傳送金鑰至Adobe是必要的。

使用剩餘的控制項來設定您想要產生或匯入的金鑰。 完成後，選取 **[!DNL Create]**.

![建立金鑰控制面板 [!DNL 3072] 位元醒目提示。](../../images/governance-privacy-security/customer-managed-keys/configure-key.png)

已設定的金鑰會出現在儲存庫的金鑰清單中。

![此 [!DNL Keys] 標示金鑰名稱的工作區。](../../images/governance-privacy-security/customer-managed-keys/key-added.png)

## 後續步驟

若要繼續設定客戶自控金鑰功能的一次性程式，請使用 [API](./api-set-up.md) 或 [UI](./ui-set-up.md) 客戶自控金鑰設定指南。
