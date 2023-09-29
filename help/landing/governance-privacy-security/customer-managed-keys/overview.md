---
title: Adobe Experience Platform中的客戶自控金鑰
description: 瞭解如何為Adobe Experience Platform中儲存的資料設定您自己的加密金鑰。
exl-id: cd33e6c2-8189-4b68-a99b-ec7fccdc9b91
source-git-commit: a81c3f220203d65ef810a92896edcfc489a0327a
workflow-type: tm+mt
source-wordcount: '739'
ht-degree: 2%

---

# Adobe Experience Platform中的客戶自控金鑰

儲存在Adobe Experience Platform上的資料會使用系統層級的金鑰進行靜態加密。 如果您使用以Platform為基礎建立的應用程式，可以選擇改用您自己的加密金鑰，讓您更能掌控資料安全性。

>[!NOTE]
>
>Adobe Experience Platform Data Lake和設定檔存放區中的資料是使用CMK加密。 這些會視為您的主要資料存放區。

本檔案提供在Platform中啟用客戶自控金鑰(CMK)功能的程式概覽，以及完成這些步驟所需的先決條件資訊。

## 先決條件

若要檢視並造訪 [!UICONTROL 加密] Adobe Experience Platform區段，您必須已建立角色並指派 [!UICONTROL 管理客戶自控金鑰] 該角色的許可權。 任何使用者擁有 [!UICONTROL 管理客戶自控金鑰] 許可權可為其組織啟用CMK。

有關在Experience Platform中指派角色和許可權的詳細資訊，請參閱 [設定許可權檔案](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/configure-permissions.html).

為了啟用CMK，您的 [!DNL Azure] 金鑰儲存庫必須設定以下設定：

* [啟用清除保護](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview#purge-protection)
* [啟用軟刪除](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview)
* [設定存取權，使用 [!DNL Azure] 角色型存取控制](https://learn.microsoft.com/en-us/azure/role-based-access-control/)

請閱讀連結的檔案，以更加瞭解此程式。

## 程式摘要 {#process-summary}

CMK包含在Healthcare Shield以及Adobe的Privacy and Security Shield產品中。 您的組織購買其中一項方案的授權後，您就可以開始一次性流程來設定功能。

>[!WARNING]
>
>設定CMK後，您無法還原為系統管理的金鑰。 您有責任安全地管理您的金鑰，並提供您對中的金鑰儲存庫、金鑰和CMK應用程式的存取權。 [!DNL Azure] 以防止無法存取您的資料。

程式如下：

1. [設定 [!DNL Azure] 金鑰儲存庫](./azure-key-vault-config.md) 根據您組織的原則，然後 [產生加密金鑰](./azure-key-vault-config.md#generate-a-key) 最終將與Adobe共用。
1. 使用您的設定CMK應用程式 [!DNL Azure] 租使用者，透過 [API呼叫](./api-set-up.md#register-app) 或 [UI](./ui-set-up.md#register-app).
1. 將您的加密金鑰ID傳送至Adobe，然後啟動功能的啟用程式： [在UI中](./ui-set-up.md#send-to-adobe) 或使用 [API呼叫](./api-set-up.md#send-to-adobe).
1. 檢查設定的狀態以確認CMK是否已啟用 [在UI中](./ui-set-up.md#check-status) 或使用 [API呼叫](./api-set-up.md#check-status).

完成設定程式後，所有所有沙箱中上線到Platform的所有資料，都會使用您的系統加密。 [!DNL Azure] 金鑰設定。 若要使用CMK，請善用 [!DNL Microsoft Azure] 可能屬於其 [公開預覽計畫](https://azure.microsoft.com/en-ca/support/legal/preview-supplemental-terms/).

## 撤銷存取權 {#revoke-access}

如果您想要撤銷Platform對您資料的存取權，可以從的金鑰儲存庫中移除與應用程式相關聯的使用者角色 [!DNL Azure].

>[!WARNING]
>
>停用金鑰儲存庫、金鑰或CMK應用程式可能會導致重大變更。 一旦金鑰儲存庫、金鑰或CMK應用程式停用，且資料無法在Platform中存取，任何與該資料相關的下游作業都將無法再進行。 在對設定進行任何變更之前，請確定您瞭解撤銷平台對您金鑰的存取權的下游影響。

移除金鑰存取權或停用/刪除金鑰之後 [!DNL Azure] 金鑰儲存庫可能需要幾分鐘到24小時的時間，才能讓此設定傳播到主要資料存放區。 平台工作流程也包含效能和核心應用程式功能所需的快取和暫時性資料存放區。 透過此類快取和暫時性存放區傳播CMK撤銷最多可能需要七天，具體取決於其資料處理工作流程。 例如，這表示「設定檔」儀表板會保留並顯示其快取資料存放區的資料，並且需要七天的時間來讓快取資料存放區中的資料過期，做為重新整理週期的一部分。 重新啟用對應用程式的存取權時，資料再次可用的時間也會延遲。

>[!NOTE]
>
>非主要（快取/暫時）資料的7天資料集到期有兩個使用案例特定例外。 如需這些功能的詳細資訊，請參閱其各自的檔案。<ul><li>[Adobe Journey Optimizer URL Shortener](https://experienceleague.adobe.com/docs/journey-optimizer/using/sms/sms-configuration.html?lang=zh-Hant#message-preset-sms)</li><li>[邊緣投影](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html#edge-projections)</li></ul>

## 後續步驟

若要開始此程式，請由 [設定 [!DNL Azure] 金鑰儲存庫](./azure-key-vault-config.md) 和 [產生加密金鑰](./azure-key-vault-config.md#generate-a-key) 以與Adobe共用。
