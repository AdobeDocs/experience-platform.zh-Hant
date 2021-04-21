---
keywords: Experience Platform;home；熱門主題；模式；模式；XDM；個人配置檔案；欄位；模式；模式；標識圖；標識圖；標識圖；模式設計；映射；聯合模式；聯合模式
solution: Experience Platform
title: IdentityMap Mixin
topic-legacy: overview
description: 本文檔概述了XDM Individual Profile類。
exl-id: c9928e85-ef1e-4739-ba1d-80505a9e60c3
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 0%

---

# [!UICONTROL IdentityMap] mixin

>[!NOTE]
>
>幾個混音的名字已經改變。 如需詳細資訊，請參閱[mixin name updates](../name-updates.md)上的檔案。

[!UICONTROL IdentityMap] 是班級的標準混音 [[!DNL XDM Individual Profile] 詞](../../classes/individual-profile.md)。mixin提供單一映射欄位，其中包含由namespace鍵入的一組使用者身分識別。

>[!WARNING]
>
>系統會隨身份資料的擷取，自動更新`IdentityMap`欄位。 為了將此欄位正確用於[即時客戶概要檔案](../../../profile/home.md)，請勿嘗試手動更新資料操作中的欄位內容。

<img src="../../images/mixins/identitymap.png" width="600" /><br />

有關方案組合的詳細資訊，請參閱[基本架構組合](../../schema/composition.md#identityMap)中有關身份映射的部分。
