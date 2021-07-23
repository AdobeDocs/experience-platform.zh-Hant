---
title: 使用Platform Web SDK在Audience Manager與Adobe Experience Platform之間同步身分
description: 了解如何使用Platform Web SDK在Audience Manager和Adobe Experience Platform之間同步身分
seo-description: 了解如何使用Web SDK將身分識別同步至Adobe Audience Manager
keywords: audience manager;aam；身分；同步身分；命名空間
source-git-commit: 3a1d08a4ea87ee3db7a2a8b048d5721fa679c372
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 0%

---


# 在Audience Manager和Experience Platform之間同步身分

Adobe Experience Platform Web SDK支援透過[sendEvent](./overview.md#syncing-identities)命令來宣告客戶ID及其驗證狀態。

使用「身分符號」欄中的值，從[Identity服務命名空間](../../identity/../identity-service/namespaces.md)中選擇您的命名空間，以指示與身分相關的內容：

![命名空間UI的檢視](../images/identity/edge_namespaceUI_identity-symbol.png)

身為Audience Manager客戶，您所有使用ID類型的現有資料來源：跨裝置會自動擁有對應的身分命名空間。 若要尋找您Audience Manager資料來源的對應身分命名空間，請登入Adobe Experience Platform並導覽至身分識別區段。

任何使用ID類型的新[!DNL Audience Manager]資料源：跨裝置會產生對應的身分命名空間。 資料來源ID類型Cookie和裝置廣告ID目前不受支援。 此外，在Adobe Experience Platform中建立的任何身分識別命名空間都會產生對應的[!DNL Audience Manager]資料來源，但請注意，syncIdentity方法僅支援命名空間身分符號。
