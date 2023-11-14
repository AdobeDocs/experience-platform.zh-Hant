---
keywords: Experience Platform；首頁；熱門主題；API；API；XDM；XDM系統；體驗資料模型；資料模型；ui；工作區；身分；欄位；
solution: Experience Platform
title: 在UI中定義身分欄位
description: 瞭解如何在Experience Platform使用者介面中定義身分欄位。
exl-id: 11a53345-4c3f-4537-b3eb-ee7a5952df2a
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '609'
ht-degree: 6%

---

# 在UI中定義身分欄位

在Experience Data Model (XDM)中，身分欄位代表可用來識別與記錄或時間序列事件相關的個人欄位。 本文介紹如何在Adobe Experience Platform UI中定義身分欄位。

## 先決條件

身分欄位是在Platform中建構客戶身分圖表的重要元件，這最終會影響Real-time Customer Profile如何將不同的資料片段合併在一起，以獲得客戶的完整檢視。 在定義結構描述中的身分欄位之前，請參閱以下檔案以瞭解與身分欄位相關的主要服務和概念：

* [Adobe Experience Platform Identity服務](../../../identity-service/home.md)：跨裝置和系統橋接身分，根據資料集符合的XDM結構描述所定義的身分欄位將其連結在一起。
   * [身分名稱空間](../../../identity-service/namespaces.md)：身分名稱空間會定義與單一人員相關的不同型別的身分資訊，且是每個身分欄位的必要元件。
* [即時客戶個人檔案](../../../profile/home.md)：運用客戶身分圖表，根據來自多個來源的彙總資料提供統一的消費者個人檔案，並近乎即時更新。

## 定義身分欄位 {#define-a-identity-field}

>[!CONTEXTUALHELP]
>id="platform_schemas_identityField_primaryIdentityRestriction"
>title="對主要身分識別的限制"
>abstract="此方案使用的欄位群組用於特定來源連接。此連線要求將 identityMap 做為主要身分識別並已自動設定。"

時間 [定義新欄位](./overview.md#define) 在UI中，您可以選取「 」，將其設定為身分欄位 **[!UICONTROL 身分]** 核取方塊。

![](../../images/ui/fields/special/identity.png)

勾選核取方塊後，會出現其他控制項。 如果您希望此欄位成為結構描述的主要身分，請選取 **[!UICONTROL 主要身分]** 核取方塊。

>[!NOTE]
>
>單一結構描述可能定義了許多身分欄位，但只能有一個主要身分。 所有身分欄位（主要或其他身分欄位）都會協助個別客戶的身分圖表，但即時客戶設定檔在合併資料片段時，僅使用主要身分作為真實來源。 如果您想要啟用結構描述以用於設定檔，結構描述必須定義主要身分。

在 **[!UICONTROL 身分名稱空間]**，使用下拉式選單為身分欄位選取適當的名稱空間。 列出Adobe提供的標準名稱空間，以及貴組織定義的任何自訂名稱空間。

完成後，選取 **[!UICONTROL 套用]** 將變更套用至結構描述。

![](../../images/ui/fields/special/identity-config.png)

畫布會更新以反映變更，而選取的欄位會取得指紋符號(![](../../images/ui/fields/special/identity-symbol.png))，以將其指定為身分。 在左側欄中，身分欄位現在會列在提供結構描述欄位的類別或結構描述欄位群組的名稱底下。

如果欄位也設定為主要身分，它也會列在底下 **[!UICONTROL 必填欄位]** 在左側邊欄中。 如果身分欄位巢狀內嵌於架構結構中，則所有父欄位也會依需求列出。

![](../../images/ui/fields/special/identity-applied.png)

如果您已定義結構描述的主要身分，現在可以繼續前往 [啟用結構以用於Real-Time Customer Profile](../resources/schemas.md#profile).

## 後續步驟

本指南說明如何在UI中定義身分欄位。 使用此結構描述擷取資料時，您的客戶身分圖表將會更新，以反映結構描述的身分欄位。 請參閱 [身分圖表檢視器](../../../identity-service/ui/identity-graph-viewer.md) 以瞭解如何在UI中探索您組織的私人圖表。

請參閱以下主題的概觀： [在UI中定義欄位](./overview.md#special) 瞭解如何在中定義其他XDM欄位型別 [!DNL Schema Editor].
