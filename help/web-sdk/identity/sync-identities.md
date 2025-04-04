---
title: 使用Audience Manager Web SDK在Experience Platform和Adobe Experience Platform之間同步身分
description: 瞭解如何使用Experience Platform Web SDK在Audience Manager和Adobe Experience Platform之間同步身分
seo-description: Learn how to sync identities with Adobe Audience Manager with Experience Platform Web SDK
keywords: audience manager；aam；身分；同步身分；名稱空間；
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---


# 在Audience Manager和Experience Platform之間同步身分

Adobe Experience Platform Web SDK支援透過[sendEvent](./overview.md#syncing-identities)命令宣告客戶ID及其驗證狀態的功能。

從[Identity Service名稱空間](../../identity/../identity-service/features/namespaces.md)中選擇您的名稱空間，以使用「識別符號」資料欄中的值來指示識別相關的內容：

![名稱空間UI的檢視](../assets/identity/edge_namespaceUI_identity-symbol.png)

身為Audience Manager客戶，您所有使用ID型別：跨裝置的現有資料來源都會自動擁有對應的身分名稱空間。 若要尋找Audience Manager Data Source的對應身分名稱空間，請登入Adobe Experience Platform並導覽至「身分」區段。

任何使用ID型別：跨裝置的新[!DNL Audience Manager]資料Source都會產生對應的身分名稱空間。 目前不支援資料Source ID型別Cookie和裝置Advertising ID。 此外，在Adobe Experience Platform中建立的任何身分識別名稱空間都會產生對應的[!DNL Audience Manager]資料Source，但請注意，syncIdentity方法僅支援名稱空間身分識別符號。
