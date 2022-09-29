---
title: 使用Platform Web SDK在Audience Manager與Adobe Experience Platform之間同步身分
description: 了解如何使用Platform Web SDK在Audience Manager和Adobe Experience Platform之間同步身分
seo-description: Learn how to sync identities with Adobe Audience Manager with Experience Platform Web SDK
keywords: audience manager;aam；身分；同步身分；命名空間
source-git-commit: f5270d1d1b9697173bc60d16c94c54d001ae175a
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---


# 在Audience Manager和Experience Platform之間同步身分

Adobe Experience Platform Web SDK支援透過 [sendEvent](./overview.md#syncing-identities) 命令。

從 [身分識別服務命名空間](../../identity/../identity-service/namespaces.md) 使用「標識符」列中的值，指示標識與其相關的上下文：

![命名空間UI的檢視](../assets/identity/edge_namespaceUI_identity-symbol.png)

身為Audience Manager客戶，您所有使用ID類型的現有資料來源：跨裝置會自動擁有對應的身分命名空間。 若要尋找您Audience Manager資料來源的對應身分命名空間，請登入Adobe Experience Platform並導覽至身分識別區段。

任何新 [!DNL Audience Manager] 使用ID類型的資料來源：跨裝置會產生對應的身分命名空間。 資料來源ID類型Cookie和裝置廣告ID目前不受支援。 此外，在Adobe Experience Platform中建立的任何身分命名空間都會產生對應的 [!DNL Audience Manager] 資料源，但請注意，syncIdentity方法僅支援命名空間標識符號。
