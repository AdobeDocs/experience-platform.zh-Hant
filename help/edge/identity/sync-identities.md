---
title: 使用平台網頁SDK同步Audience Manager與Adobe Experience Platform之間的身份
description: 瞭解如何使用Platform Web SDK在Audience Manager和Adobe Experience Platform之間同步身分
seo-description: 瞭解如何使用Experience Platform Web SDK與Adobe Audience Manager同步身分
keywords: audience manager;aam;identities;sync identities;namespace;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 0%

---


# 在Audience Manager和Experience Platform之間同步身分

Adobe Experience Platform Web SDK支援透過[sendEvent](./overview.md#syncing-identities)命令宣告客戶ID及其驗證狀態。

從[身分服務名稱空間](../../identity/../identity-service/namespaces.md)中選擇您的名稱空間，使用「身分符號」欄中的值來指示身分相關的內容：

![名稱空間UI的視圖](../../assets/edge_namespaceUI_identity-symbol.png)

身為Audience Manager客戶，您所有使用ID類型的現有資料來源：跨裝置會自動擁有對應的身分命名空間。 若要尋找Audience Manager資料來源的對應Identity Namespace，請登入Adobe Experience Platform並導覽至「身分識別」區段。

任何使用ID類型的新[!DNL Audience Manager]資料來源：跨裝置將產生對應的身分命名空間。 資料來源ID類型目前不支援Cookie和裝置廣告ID。 此外，在Adobe Experience Platform中建立的任何Identity Namespace都會產生對應的[!DNL Audience Manager]資料來源，但請注意，syncIdentity方法僅支援Namespace Identity Symbols。
