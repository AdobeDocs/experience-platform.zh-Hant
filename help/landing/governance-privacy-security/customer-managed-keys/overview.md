---
title: Adobe Experience Platform中的客戶自控金鑰
description: 瞭解如何為Adobe Experience Platform中儲存的資料設定您自己的加密金鑰。
exl-id: cd33e6c2-8189-4b68-a99b-ec7fccdc9b91
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '716'
ht-degree: 0%

---

# Adobe Experience Platform中的客戶自控金鑰

儲存在Adobe Experience Platform上的資料會使用系統層級的金鑰進行靜態加密。 如果您使用以Platform為基礎建立的應用程式，可以選擇改用您自己的加密金鑰，讓您更能掌控資料安全性。

>[!NOTE]
>
>Adobe Experience Platform Data Lake和設定檔存放區中的資料已使用CMK加密。 這些會視為您的主要資料存放區。

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

## 撤銷存取權 {#revoke-access}

如果您想要撤銷平台對您資料的存取權，可以在[!DNL Azure]內從金鑰儲存庫中移除與應用程式相關聯的使用者角色。

>[!WARNING]
>
>停用金鑰儲存庫、金鑰或CMK應用程式可能會導致重大變更。 一旦金鑰儲存庫、金鑰或CMK應用程式停用，且資料無法在Platform中存取，任何與該資料相關的下游作業都將無法再進行。 在對設定進行任何變更之前，請確定您瞭解撤銷平台對您金鑰的存取權的下游影響。

移除金鑰存取權或停用/刪除[!DNL Azure]金鑰儲存庫中的金鑰後，此設定可能需要幾分鐘到24小時的時間才能傳播至主要資料存放區。 平台工作流程也包含效能和核心應用程式功能所需的快取和暫時性資料存放區。 透過此類快取和暫時性存放區傳播CMK撤銷最多可能需要七天，具體取決於其資料處理工作流程。 例如，這表示「設定檔」儀表板會保留並顯示其快取資料存放區的資料，並且需要七天的時間來讓快取資料存放區中的資料過期，做為重新整理週期的一部分。 重新啟用對應用程式的存取權時，資料再次可用的時間也會延遲。

>[!NOTE]
>
>非主要（快取/暫時）資料的7天資料集到期有兩個使用案例特定例外。 如需這些功能的詳細資訊，請參閱其各自的檔案。<ul><li>[Adobe Journey Optimizer URL Shortener](https://experienceleague.adobe.com/docs/journey-optimizer/using/sms/sms-configuration.html?lang=zh-Hant#message-preset-sms)</li><li>[Edge投影](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html#edge-projections)</li></ul>

## 後續步驟

若要開始此程式，請從[設定 [!DNL Azure] 金鑰儲存庫](./azure-key-vault-config.md)和[產生加密金鑰](./azure-key-vault-config.md#generate-a-key)以與Adobe共用。
