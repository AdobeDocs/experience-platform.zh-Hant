---
title: 將身分識別與Audience Manager和Adobe Experience Platform同步
seo-title: 將身分識別與Audience Manager和Adobe Experience Platform與Adobe Experience Platform Web SDK同步
description: 瞭解如何使用Experience Platform Web SDK與Adobe Audience Manager同步身分
seo-description: 瞭解如何使用Experience Platform Web SDK與Adobe Audience Manager同步身分
keywords: audience manager;aam;identities;sync identities;namespace;
translation-type: tm+mt
source-git-commit: 290792cd507248c41690c493cc18daaab869db50
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 0%

---


# 同步身分

Adobe Experience Platform Web SDK支援透過sendEvent命令宣告客戶ID及其驗 [證狀態](./overview.md#syncing-identities) 。

從 [Identity Service Nampesaces](../../identity/../identity-service/namespaces.md) （身份服務名稱空間）中選擇您的名稱空間，通過使用「身份符號」列中的值來指示身份相關的上下文：

![名稱空間UI的視圖](../../assets/edge_namespaceUI_identity-symbol.png)

身為Audience Manager客戶，您所有使用ID類型的現有資料來源：跨裝置會自動擁有對應的身分命名空間。 若要尋找Audience Manager資料來源的對應Identity Namespace，請登入Adobe Experience Platform並導覽至「身分識別」區段。

任何使 [!DNL Audience Manager] 用ID類型的新資料來源：跨裝置將產生對應的身分命名空間。 資料來源ID類型目前不支援Cookie和裝置廣告ID。 此外，在Adobe Experience Platform中建立的任何Identity Namespace都會產生對應的 [!DNL Audience Manager] 「資料來源」，但請注意，syncIdentity方法僅支援Namespace Identity Symbols。
