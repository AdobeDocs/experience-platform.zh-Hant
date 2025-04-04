---
title: Adobe Experience Platform中的客戶自控金鑰
description: 瞭解如何為Adobe Experience Platform中儲存的資料設定您自己的加密金鑰。
role: Developer
feature: Privacy
exl-id: cd33e6c2-8189-4b68-a99b-ec7fccdc9b91
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1111'
ht-degree: 0%

---

# Adobe Experience Platform中的客戶自控金鑰

儲存在Adobe Experience Platform上的資料會使用系統層級的金鑰進行靜態加密。 如果您使用以Experience Platform為基礎建立的應用程式，則可以選擇改用您自己的加密金鑰，讓您更能掌控資料安全性。

>[!AVAILABILITY]
>
>Adobe Experience Platform同時支援Microsoft Azure和Amazon Web Services (AWS)的客戶自控金鑰(CMK)。 目前有限數量的客戶可使用在AWS上執行的Experience Platform 。 如果您的實作在AWS上執行，您可以選擇使用金鑰管理服務(KMS)進行Experience Platform資料加密。 如需支援之基礎結構的詳細資訊，請參閱[Experience Platform multi-cloud概述](https://experienceleague.adobe.com/en/docs/experience-platform/landing/multi-cloud)。
>
>若要瞭解AWS KMS中加密金鑰的建立與管理，請參閱[AWS KMS資料加密指南](./aws/configure-kms.md)。 若為Azure實作，請參閱[Azure Key Vault設定指南](./azure/azure-key-vault-config.md)。

>[!NOTE]
>
>對於[!DNL Azure]個託管的Experience Platform執行個體，儲存在Experience Platform的[!DNL Azure Data Lake]和[!DNL Azure Cosmos DB]設定檔存放區的客戶設定檔資料，一經啟用即僅使用CMK加密。 主要資料存放區中的金鑰撤銷可能需要&#x200B;**幾分鐘到24小時**&#x200B;以及&#x200B;**最多7天**&#x200B;的時間（暫時性或次要資料存放區）。 如需其他詳細資訊，請參閱[撤銷金鑰存取許可權的影響區段](#revoke-access)。

本檔案提供在[!DNL Azure]和AWS中啟用Experience Platform中客戶自控金鑰(CMK)功能的程式整體概觀，以及完成這些步驟所需的先決條件資訊。

>[!NOTE]
>
>若為Customer Journey Analytics客戶，請依照[Customer Journey Analytics檔案](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-privacy/cmk.html?lang=zh-Hant)中的指示操作。

## 先決條件

若要啟用CMK，您平台的裝載環境([!DNL Azure]或AWS)必須符合特定的設定需求：

### 一般必要條件

若要在Adobe Experience Platform中檢視及存取[!UICONTROL 加密]區段，您必須已建立角色，並已將[!UICONTROL 管理客戶管理的金鑰]許可權指派給該角色。  任何具有[!UICONTROL 管理客戶受管理金鑰]許可權的使用者都可以為其組織啟用CMK。

如需在Experience Platform中指派角色和許可權的詳細資訊，請參閱[設定許可權檔案](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/configure-permissions.html)。

### Azure專屬必要條件

針對Azure代管實作，請使用下列設定來設定您的[!DNL Azure]金鑰儲存庫：

- [啟用清除保護](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview#purge-protection)
- [啟用軟刪除](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview)
- [使用 [!DNL Azure] 角色型存取控制設定存取權](https://learn.microsoft.com/en-us/azure/role-based-access-control/)

### AWS專屬必要條件

針對AWS託管的實作，請依照以下方式設定您的AWS環境：

- 確保您擁有使用AWS Identity and Access Management (IAM)管理加密金鑰的許可權。 如需詳細資訊，請參閱AWS KMS的[IAM原則](https://docs.aws.amazon.com/kms/latest/developerguide/iam-policies.html)。
- 設定支援CMK的AWS KMS。 請參閱[AWS KMS資料加密指南](./aws/configure-kms.md)。

## 程式摘要 {#process-summary}

客戶自控金鑰(CMK)可透過Adobe的Healthcare Shield及Privacy and Security Shield產品提供。 在Azure上，CMK同時支援Healthcare Shield和Privacy and Security Shield。 在AWS上，CMK僅支援Privacy and Security Shield，不適用於Healthcare Shield。 您的組織購買其中一項方案的授權後，您就可以開始啟用CMK的一次性設定流程。

>[!WARNING]
>
>設定CMK後，您無法還原為系統管理的金鑰。 您有責任安全地管理您的金鑰，以避免無法存取您的資料。

程式如下：

### 適用於Azure {#azure-process-summary}

1. [根據您組織的原則設定 [!DNL Azure] 金鑰儲存庫](./azure/azure-key-vault-config.md)，然後[產生加密金鑰](./azure/azure-key-vault-config.md#generate-a-key)以與Adobe共用。
1. 透過[API呼叫](./azure/api-set-up.md#register-app)或[UI](./azure/ui-set-up.md#register-app)與您的[!DNL Azure]租使用者設定CMK App。
1. 將您的加密金鑰ID傳送到Adobe，並啟動該功能的啟用程式（在UI](./azure/ui-set-up.md#send-to-adobe)中[或使用[API呼叫](./azure/api-set-up.md#send-to-adobe)）。
1. 檢查組態的狀態，以確認UI](./azure/ui-set-up.md#check-status)中的[或使用[API呼叫](./azure/api-set-up.md#check-status)是否已啟用CMK。

完成Azure代管的Experience Platform執行個體的設定程式後，所有沙箱上線到Experience Platform的所有資料都將使用您的[!DNL Azure]金鑰設定進行加密。 若要使用CMK，您將善用[!DNL Microsoft Azure]功能，這些功能可能是其[公開預覽方案](https://azure.microsoft.com/en-ca/support/legal/preview-supplemental-terms/)的一部分。

### 適用於AWS {#aws-process-summary}

1. [設定要與AWS共用的加密金鑰，以設定Adobe KMS](./aws/configure-kms.md)。
2. 遵循[UI安裝指南](./aws/ui-set-up.md)中的AWS特定指示。
3. 驗證設定，確認已使用AWS代管的金鑰加密Experience Platform資料。

<!--  Pending: or [API setup guide]() -->

AWS託管的Experience Platform執行個體的設定程式一旦完成，所有沙箱上線至Experience Platform的所有資料，都會使用您的AWS金鑰管理服務(KMS)設定進行加密。 若要在AWS上使用CMK，您將使用AWS金鑰管理服務來建立和管理您的加密金鑰，以符合貴組織的安全需求。

## 撤銷金鑰存取許可權的影響 {#revoke-access}

撤銷或停用Azure中金鑰儲存庫、金鑰或CMK應用程式的存取權或AWS中的加密金鑰可能會導致重大中斷，包括對Experience Platform操作的重大變更。 索引鍵停用後，Experience Platform中的資料可能會變得無法存取，且依賴此資料的任何下游作業都將停止運作。 在對您的關鍵設定進行任何變更之前，完全瞭解下游影響至關重要。

若要撤銷Experience Platform對您在[!DNL Azure]中資料的存取權，請從金鑰儲存庫中移除與應用程式相關聯的使用者角色。 對於AWS，您可以停用金鑰或更新原則陳述式。 如需AWS程式的詳細說明，請參閱[金鑰撤銷區段](./aws/ui-set-up.md#key-revocation)。


### 傳輸時間表 {#propagation-timelines}

從您的[!DNL Azure]金鑰儲存庫撤銷金鑰存取後，變更將傳播如下：

| **存放區型別** | **說明** | **時間表** |
|---|---|---|
| 主要資料存放區 | 包括資料湖(Azure Data Lake、AWS S3)和Azure Cosmos DB設定檔存放區。 一旦金鑰存取遭撤銷，資料將無法存取。 | **分鐘到24小時**。 |
| 快取/暫時性資料存放區 | 包括用於效能和核心應用程式功能的次要資料存放區。 金鑰撤銷的影響已延遲。 | **最多7天**。 |

例如，設定檔儀表板最多會在資料過期並重新整理前七天持續顯示其快取中的資料。 同樣地，重新啟用應用程式的存取權時，也需要同樣的時間來還原這些存放區中的資料可用性。

>[!NOTE]
>
>重新啟用應用程式的存取權可能需要與撤銷相同的時間，才能還原這些存放區中的資料可用性。

>[!TIP]
>
>非主要（快取/暫時）資料的7天資料集到期有兩個使用案例特定例外。 如需這些功能的詳細資訊，請參閱其各自的檔案。<ul><li>[Adobe Journey Optimizer URL Shortener](https://experienceleague.adobe.com/docs/journey-optimizer/using/sms/sms-configuration.html?lang=zh-Hant#message-preset-sms)</li><li>[Edge投影](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html#edge-projections)</li></ul>

## 後續步驟

若要開始此程式：

- 對於Azure：首先[設定 [!DNL Azure] 金鑰儲存庫](./azure/azure-key-vault-config.md)，然後[產生加密金鑰](./azure/azure-key-vault-config.md#generate-a-key)以與Adobe共用。
- 針對AWS： [請設定AWS KMS](./aws/configure-kms.md)，並確保IAM和KMS設定正確，然後再繼續參閱UI或API設定指南。
