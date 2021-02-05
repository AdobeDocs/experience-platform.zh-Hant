---
keywords: Experience Platform;home；熱門主題；架構；架構；XDM；個人配置檔案；欄位；架構；Schemas;identityMap;IdentityMap;Schema設計；Map;Union架構；union
solution: Experience Platform
title: IdentityMap Mixin
topic: overview
description: 本文檔概述了XDM Individual Profile類。
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 0%

---


# [!UICONTROL IdentityMapmixin] 

>[!NOTE]
>
>幾個混音的名字已經改變。 如需詳細資訊，請參閱[mixin name updates](../name-updates.md)上的檔案。

 IdentityMap是類別的標準混 [[!DNL XDM Individual Profile] 合檔](../../classes/individual-profile.md)。mixin提供單一映射欄位，其中包含由namespace鍵入的一組使用者身分識別。

>[!WARNING]
>
>系統會隨身份資料的擷取，自動更新`IdentityMap`欄位。 為了將此欄位正確用於[即時客戶概要檔案](../../../profile/home.md)，請勿嘗試手動更新資料操作中的欄位內容。

<img src="../../images/mixins/identitymap.png" width="600" /><br />

有關方案組合的詳細資訊，請參閱[基本架構組合](../../schema/composition.md#identityMap)中有關身份映射的部分。