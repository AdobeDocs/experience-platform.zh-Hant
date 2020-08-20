---
title: 傳送資料至Adobe Audience Manager
seo-title: 使用Adobe Experience Platform Web SDK將資料傳送至Adobe Audience Manager
description: 瞭解如何使用Experience Platform Web SDK將資料傳送至Adobe Audience Manager
seo-description: 瞭解如何使用Experience Platform Web SDK將資料傳送至Adobe Audience Manager
keywords: audience manager;aam;identities;sync identities;namespace;
translation-type: tm+mt
source-git-commit: 8c256b010d5540ea0872fa7e660f71f2903bfb04
workflow-type: tm+mt
source-wordcount: '256'
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

Adobe Experience Platform Web SDK支援透過sendEvent命令宣告客戶ID及其驗 [證狀態](../../fundamentals/identity.md#syncing-identities) 。

從 [Identity Service Nampesaces](../../../identity/../identity-service/namespaces.md) （身份服務名稱空間）中選擇您的名稱空間，通過使用「身份符號」列中的值來指示身份相關的上下文：

![名稱空間UI的視圖](../../../assets/edge_namespaceUI_identity-symbol.png)

身為Audience Manager客戶，您所有使用ID類型的現有資料來源：跨裝置會自動擁有對應的身分命名空間。 若要尋找Audience Manager資料來源的對應Identity Namespace，請登入Adobe Experience Platform並導覽至「身分識別」區段。

任何使 [!DNL Audience Manager] 用ID類型的新資料來源：跨裝置將產生對應的身分命名空間。 資料來源ID類型目前不支援Cookie和裝置廣告ID。 此外，在Adobe Experience Platform中建立的任何Identity Namespace都會產生對應的 [!DNL Audience Manager] 「資料來源」，但請注意，syncIdentity方法僅支援Namespace Identity Symbols。
