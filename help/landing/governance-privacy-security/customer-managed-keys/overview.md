---
title: Adobe Experience Platform中的客戶自控金鑰
description: 瞭解如何為Adobe Experience Platform中儲存的資料設定您自己的加密金鑰。
exl-id: cd33e6c2-8189-4b68-a99b-ec7fccdc9b91
source-git-commit: 5a5d35dad5f1b89c0161f4b29722b76c3caf3609
workflow-type: tm+mt
source-wordcount: '752'
ht-degree: 0%

---

# Adobe Experience Platform中的客戶自控金鑰

儲存在Adobe Experience Platform上的資料會使用系統層級的金鑰進行靜態加密。 如果您使用以Platform為基礎建立的應用程式，可以選擇改用您自己的加密金鑰，讓您更能掌控資料安全性。

>[!NOTE]
>
>儲存在Platform [!DNL Azure Data Lake]和[!DNL Azure Cosmos DB]設定檔存放區的客戶設定檔資料在啟用後，將僅使用CMK加密。 主要資料存放區中的金鑰撤銷可能需要&#x200B;**幾分鐘到24小時**&#x200B;之間的任何時間，而暫時性或次要資料存放區可能需要更長的時間&#x200B;**到7天**。 如需其他詳細資訊，請參閱[撤銷金鑰存取許可權的影響區段](#revoke-access)。

本檔案提供在Platform中啟用客戶自控金鑰(CMK)功能的程式概覽，以及完成這些步驟所需的先決條件資訊。

>[!NOTE]
>
>若為Customer Journey Analytics客戶，請依照[Customer Journey Analytics檔案](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-privacy/cmk.html?lang=zh-Hant)中的指示操作。

## 先決條件

若要在Adobe Experience Platform中檢視並瀏覽[!UICONTROL 加密]區段，您必須已建立角色，並已將[!UICONTROL 管理客戶管理的金鑰]許可權指派給該角色。 任何擁有[!UICONTROL 管理客戶管理的金鑰]許可權的使用者都可以為其組織啟用CMK。

有關在Experience Platform中指派角色和許可權的詳細資訊，請參閱[設定許可權檔案](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/configure-permissions.html)。

為了啟用CMK，您的[!DNL Azure]金鑰儲存庫必須設定下列設定：

* [啟用清除保護](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview#purge-protection)
* [啟用軟刪除](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview)
* [使用 [!DNL Azure] 角色型存取控制設定存取權](https://learn.microsoft.com/en-us/azure/role-based-access-control/)

請閱讀連結的檔案，以更加瞭解此程式。

## 程式摘要 {#process-summary}

CMK包含在Healthcare Shield以及Adobe的Privacy and Security Shield產品中。 您的組織購買其中一項方案的授權後，您就可以開始一次性流程來設定功能。

>[!WARNING]
>
>設定CMK後，您無法還原為系統管理的金鑰。 您有責任安全地管理您的金鑰，並在[!DNL Azure]內提供金鑰儲存庫、金鑰和CMK應用程式的存取權，以防止無法存取您的資料。

程式如下：

1. [根據您組織的原則設定 [!DNL Azure] 金鑰儲存庫](./azure-key-vault-config.md)，然後[產生加密金鑰](./azure-key-vault-config.md#generate-a-key)，最終將與Adobe共用。
1. 透過[API呼叫](./api-set-up.md#register-app)或[UI](./ui-set-up.md#register-app)與您的[!DNL Azure]租使用者設定CMK App。
1. 將您的加密金鑰識別碼傳送到UI](./ui-set-up.md#send-to-adobe)中的[或透過[API呼叫](./api-set-up.md#send-to-adobe)Adobe及啟動功能的啟用程式。
1. 檢查組態的狀態，以確認CMK已在UI](./ui-set-up.md#check-status)中[或透過[API呼叫](./api-set-up.md#check-status)啟用。

設定程式一旦完成，所有沙箱上線到Platform的所有資料都將使用您的[!DNL Azure]金鑰設定加密。 若要使用CMK，您將善用[!DNL Microsoft Azure]功能，這些功能可能是其[公開預覽方案](https://azure.microsoft.com/en-ca/support/legal/preview-supplemental-terms/)的一部分。

## 撤銷金鑰存取許可權的影響 {#revoke-access}

撤銷或停用金鑰儲存庫、金鑰或CMK應用程式的存取權可能會造成重大中斷，包括平台運作上的重大變更。 停用這些索引鍵後，可能無法存取Platform中的資料，且任何依賴此資料的下游作業都將停止運作。 在對您的關鍵設定進行任何變更之前，完全瞭解下游影響至關重要。

如果您決定撤銷Platform對您資料的存取權，您可以從[!DNL Azure]內的金鑰儲存庫中移除與應用程式相關聯的使用者角色，以撤銷存取權。

### 傳輸時間表 {#propagation-timelines}

從您的[!DNL Azure]金鑰儲存庫撤銷金鑰存取後，變更將傳播如下：

| **存放區型別** | **說明** | **時間表** |
|---|---|---|
| 主要資料存放區 | 這些存放區包括Azure Data Lake和Azure Cosmos DB設定檔存放區。 一旦金鑰存取遭撤銷，資料將無法存取。 | **分鐘到24小時**。 |
| 快取/暫時性資料存放區 | 包括用於效能和核心應用程式功能的資料存放區。 金鑰撤銷的影響已延遲。 | **最多7天**。 |

例如，設定檔儀表板最多會在資料過期並重新整理前七天持續顯示其快取中的資料。 同樣地，重新啟用應用程式的存取權時，也需要同樣的時間來還原這些存放區中的資料可用性。

>[!NOTE]
>
>非主要（快取/暫時）資料的7天資料集到期有兩個使用案例特定例外。 如需這些功能的詳細資訊，請參閱其各自的檔案。<ul><li>[Adobe Journey Optimizer URL Shortener](https://experienceleague.adobe.com/docs/journey-optimizer/using/sms/sms-configuration.html?lang=zh-Hant#message-preset-sms)</li><li>[Edge投影](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html#edge-projections)</li></ul>

## 後續步驟

若要開始此程式，請從[設定 [!DNL Azure] 金鑰儲存庫](./azure-key-vault-config.md)和[產生加密金鑰](./azure-key-vault-config.md#generate-a-key)以與Adobe共用。
