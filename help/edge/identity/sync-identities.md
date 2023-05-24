---
title: 使用平台Web SDK在Audience Manager和Adobe Experience Platform之間同步身份
description: 瞭解如何使用平台Web SDK在Audience Manager和Adobe Experience Platform之間同步標識
seo-description: Learn how to sync identities with Adobe Audience Manager with Experience Platform Web SDK
keywords: 受眾管理器；aam;identities;sync identitys;namespace;audience manager;aam;identitys;namespace
source-git-commit: f5270d1d1b9697173bc60d16c94c54d001ae175a
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---


# 在Audience Manager和Experience Platform之間同步身份

Adobe Experience PlatformWeb SDK支援通過 [sendEvent](./overview.md#syncing-identities) 的子菜單。

從 [標識服務命名空間](../../identity/../identity-service/namespaces.md) 使用「身份符號」列中的值來指示標識與其相關的上下文：

![命名空間UI的視圖](../assets/identity/edge_namespaceUI_identity-symbol.png)

作為Audience Manager客戶，您使用ID類型的所有現有資料源：跨設備自動具有相應的標識命名空間。 要查找Audience Manager資料源的相應標識名稱空間，請登錄到Adobe Experience Platform並導航到標識部分。

任何新 [!DNL Audience Manager] 使用ID類型的資料源：跨設備將生成相應的標識命名空間。 當前不支援資料源ID類型Cookie和設備廣告ID。 此外，在Adobe Experience Platform建立的任何Identity Namespace都將生成 [!DNL Audience Manager] 資料源，但請注意，syncIdentity方法只支援命名空間標識符號。
