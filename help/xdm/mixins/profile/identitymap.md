---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;individual profile;fields;schemas;Schemas;identityMap;identity map;Identity map;Schema design;map;Map;union schema;union
solution: Experience Platform
title: IdentityMap混音
topic: overview
description: 本文檔概述了XDM Individual Profile類。
translation-type: tm+mt
source-git-commit: fd5bd4134bd35d5d87c79bf1e75bc88c67511b2b
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 0%

---


# [!UICONTROL IdentityMap] mixin

[!UICONTROL IdentityMap] 是類別的標準混 [[!DNL XDM Individual Profile] 合檔](../../classes/individual-profile.md)。 mixin提供單一映射欄位，其中包含由namespace鍵入的一組使用者身分識別。

>[!WARNING]
>
>系統 `IdentityMap` 會隨著識別資料的擷取，自動更新欄位。 為了適當利用此欄位進行 [即時客戶配置檔案](../../../profile/home.md)，請勿嘗試手動更新資料操作中該欄位的內容。

<img src="../../images/mixins/identitymap.png" width="600" /><br />

如需其使用案例的詳細資訊，請參 [閱架構構成基礎中的識別地圖](../../schema/composition.md#identityMap) 。