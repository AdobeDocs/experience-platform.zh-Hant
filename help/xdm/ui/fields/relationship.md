---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM系統；experience資料模型；資料模型；ui;workspace;relations;field;
solution: Experience Platform
title: 在UI中定義關係欄位
description: 瞭解如何在Experience Platform使用者介面中定義關係欄位。
topic: user guide
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%

---


# 在UI中定義關係欄位

在Experience Data Model(XDM)中，[union架構](../../schema/composition.md#union)是屬於同一類的所有架構的統一視圖，同時也為[即時客戶概要檔案](../../../profile/home.md)啟用了該視圖。 Profile利用聯合架構，從不同的體驗資料建構客戶的完整表現。

在某些情況下，您可能正在吸收不一定是描述檔一部分但仍與描述檔相關的資料。 此類資料的範例是客戶「最愛的酒店」欄位。 由於人員最愛酒店的屬性不是人員本身的屬性，因此最好以基於自訂類別（而非[!DNL XDM Individual Profile]）的獨立架構來呈現酒店。

由於聯合架構僅基於共用同一類的架構，因此僅啟用「Hotels」架構以便用於配置檔案時，將不包括其[!DNL XDM Individual Profile]的欄位聯合架構。 您必須改為定義「酒店」與屬於工會的其他結構之間的關係。 這包括在引用目標方案主標識的源方案中定義&#x200B;**關係欄位**。

如需在Adobe Experience Platform UI中定義兩個結構之間關係的詳細步驟，請參閱[關係UI教學課程](../../tutorials/relationship-ui.md)。