---
keywords: Experience Platform；首頁；熱門主題；API;API;XDM;XDM系統；體驗資料模型；資料模型；ui；工作區；關係；欄位；
solution: Experience Platform
title: 在UI中定義關係欄位
description: 了解如何在Experience Platform使用者介面中定義關係欄位。
exl-id: 8a6be545-0edb-4b9c-b164-e44a7a5f54f5
source-git-commit: 5caa4c750c9f786626f44c3578272671d85b8425
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%

---

# 在UI中定義關係欄位

在Experience Data Model(XDM)中， [聯合方案](../../schema/composition.md#union) 是屬於相同類別且已啟用的所有結構的統一檢視 [即時客戶個人檔案](../../../profile/home.md). 設定檔會運用聯合結構，以從不同的體驗資料建構客戶的完整表示法。

在某些情況下，您可能會擷取不一定是設定檔一部分的資料，但仍與設定檔相關。 這類資料的範例是客戶「最喜愛的酒店」欄位。 由於人們最喜愛的酒店的屬性不是人本身的屬性，因此，酒店最好以基於定制類別的單獨模式來表示，而不是 [!DNL XDM Individual Profile].

由於聯合結構僅以共用相同類別的結構為基礎，因此僅在「設定檔」中啟用「酒店」結構即不會包含其欄位的聯合結構 [!DNL XDM Individual Profile]. 相反，您必須定義「酒店」與屬於聯合的其他架構之間的關係。 這包括定義 **關係欄位** 在引用目標架構的主標識的源架構中。

如需在Adobe Experience Platform UI中定義兩個結構之間關係的詳細步驟，請參閱 [relationship UI教學課程](../../tutorials/relationship-ui.md).
