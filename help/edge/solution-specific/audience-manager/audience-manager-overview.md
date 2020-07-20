---
title: 傳送資料至Adobe Audience Manager
seo-title: 使用Adobe Experience Platform Web SDK將資料傳送至Adobe Audience Manager
description: 瞭解如何使用Experience Platform Web SDK將資料傳送至Adobe Audience Manager
seo-description: 瞭解如何使用Experience Platform Web SDK將資料傳送至Adobe Audience Manager
translation-type: tm+mt
source-git-commit: 7b07a974e29334cde2dee7027b9780a296db7b20
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 0%

---


# [!DNL Audience Manager] 在 [!DNL Experience Platform Edge Network]

Adobe Experience Platform已與Adobe Audience Manager整 [!DNL Web SDK] 合，並支援從Cookie和URL目的地傳送及 [!DNL Audience Manager]接收資料以及ID同步。

## 啟用 [!DNL Audience Manager]

若要啟 [!DNL Audience Manager] 用，您需要執行下列動作：

- 在邊緣 [!DNL Audience Manager] 設定中 [啟用](../../fundamentals/edge-configuration.md)。
- 啟用或停用Cookie和URL目的地。
- 指定外部合作夥伴同步的ID同步容器（選用）

## 同步身分識別

Adobe Experience Platform支 [!DNL Web SDK] 援透過 [SyncIdentity](../../fundamentals/identity.md) 命令宣告客戶ID及其驗證狀態。

syncIdentity方法使用 [Identity Service Namespaces](../../../identity/../identity-service/namespaces.md) ，以指出身份相關的上下文。 身為客 [!DNL Audience Manager] 戶，您所有使用ID類型的現有資料來源： 跨裝置將自動擁有對應的裝置 [!DNL Identity Namespace]。 若要尋找您 [!DNL Identity Namespace] 的對 [!DNL Audience Manager Data Source]應項目，請登入Adobe Experience Platform並導覽至該 [!DNL Identities] 區段。

![名稱空間UI的視圖](../../../assets/edge_configuration_identity.png)

您可以在這裡依名稱搜 [!DNL Audience Manager] 尋資料來源。 syncIdentity方法使用Identity Symbol來指定Namespace。

任何使 [!DNL Audience Manager] 用ID類型的新資料來源： 跨裝置將產生對應的身分命名空間。 資料來源ID類型目前不支援Cookie和裝置廣告ID。 此外，在Adobe Experience Platform中建立的任何Identity Namespace都會產生對應的 [!DNL Audience Manager] 「資料來源」，但請注意，syncIdentity方法僅支援Namespace Identity Symbols。
