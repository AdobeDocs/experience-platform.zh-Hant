---
keywords: Experience Platform；主題；熱門主題；api;API;XDM;XDM系統；經驗資料模型；資料模型；ui;workspace;relationship;field;
solution: Experience Platform
title: 在UI中定義關係欄位
description: 瞭解如何在Experience Platform用戶介面中定義關係欄位。
exl-id: 8a6be545-0edb-4b9c-b164-e44a7a5f54f5
source-git-commit: 7021725e011a1e1d95195c6c7318ecb5afe05ac6
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%

---

# 在UI中定義關係欄位

在體驗資料模型(XDM)中， [聯合架構](../../schema/composition.md#union) 是屬於同一類的所有架構的統一視圖，這些架構也已為 [即時客戶配置檔案](../../../profile/home.md)。 聯合模式由Profile利用，以便從不同的體驗資料構造客戶的完整表示。

在某些情況下，您可能正在接收不一定是配置檔案一部分但與配置檔案相關的資料。 此類資料的一個示例是客戶「最喜愛的酒店」欄位。 由於人喜愛的酒店的屬性不是人本身的屬性，因此最好由基於自定義類而不是自定義類的單獨模式來表示酒店 [!DNL XDM Individual Profile]。

由於聯合架構僅基於共用同一類的架構，因此僅啟用「Hotels」架構以在配置檔案中使用將不包括其欄位的聯合架構 [!DNL XDM Individual Profile]。 相反，您必須定義「Hotels」與屬於工會的另一個架構之間的關係。 這包括定義 **關係欄位** 引用引用架構的主標識的源架構中。

有關在Adobe Experience PlatformUI中定義兩個架構之間關係的詳細步驟，請參見 [關係UI教程](../../tutorials/relationship-ui.md)。
