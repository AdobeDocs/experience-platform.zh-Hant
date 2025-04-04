---
keywords: Experience Platform；首頁；熱門主題；API；API；XDM；XDM系統；體驗資料模型；資料模型；ui；工作區；身分；欄位；
solution: Experience Platform
title: 在UI中定義身分欄位
description: 瞭解如何在Experience Platform使用者介面中定義身分欄位。
exl-id: 11a53345-4c3f-4537-b3eb-ee7a5952df2a
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '652'
ht-degree: 6%

---

# 在UI中定義身分欄位

在Experience Data Model (XDM)中，身分欄位代表可用來識別與記錄或時間序列事件相關的個人欄位。 本文介紹如何在Adobe Experience Platform UI中定義身分欄位。

## 先決條件

身分欄位是在Experience Platform中建構客戶身分圖表的重要元件，這最終會影響Real-time Customer Profile如何將不同的資料片段合併在一起，以獲得客戶的完整檢視。 在定義結構描述中的身分欄位之前，請參閱以下檔案以瞭解與身分欄位相關的主要服務和概念：

* [Adobe Experience Platform Identity服務](../../../identity-service/home.md)：跨裝置和系統橋接身分，根據資料集所符合的XDM結構描述所定義的身分欄位，將資料集連結在一起。
   * [身分識別名稱空間](../../../identity-service/features/namespaces.md)：身分識別名稱空間會定義與單一人員相關的不同身分識別資訊型別，而且是每個身分識別欄位的必要元件。
* [即時客戶個人檔案](../../../profile/home.md)：運用客戶身分圖表，根據來自多個來源的彙總資料提供統一的客戶個人檔案，並以近乎即時的方式更新。

## 定義身分識別欄位 {#define-a-identity-field}

>[!CONTEXTUALHELP]
>id="platform_schemas_identityField_primaryIdentityRestriction"
>title="對主要身分識別的限制"
>abstract="此結構描述使用的欄位群組用於特定來源連接。此連線要求將 identityMap 做為主要身分識別並已自動設定。"

在UI中定義[新欄位](./overview.md#define)時，您可以選取右側邊欄中的&#x200B;**[!UICONTROL 身分]**&#x200B;核取方塊，將其設定為身分欄位。

![](../../images/ui/fields/special/identity.png)

勾選核取方塊後，會出現其他控制項。 如果您希望此欄位成為結構描述的主要身分，請選取&#x200B;**[!UICONTROL 主要身分]**&#x200B;核取方塊。

>[!NOTE]
>
>單一結構描述可能定義了許多身分欄位，但只能有一個主要身分。 所有身分欄位（主要或其他身分欄位）都會協助個別客戶的身分圖表，但即時客戶設定檔在合併資料片段時，僅使用主要身分作為真實來源。 如果您想要啟用結構描述以用於設定檔，結構描述必須定義主要身分。

在&#x200B;**[!UICONTROL 身分識別名稱空間]**&#x200B;底下，使用下拉式功能表為身分識別欄位選取適當的名稱空間。 Adobe提供的標準名稱空間以及貴組織定義的任何自訂名稱空間都會列在清單中。

完成後，選取&#x200B;**[!UICONTROL 套用]**&#x200B;將變更套用至結構描述。

>[!IMPORTANT]
>
>如果已設定主要身分欄位，您可以依照上述步驟變更架構中的主要身分欄位。 不過，您必須停用設定檔中的任何關聯資料集，然後重新啟用，變更才會生效。

![](../../images/ui/fields/special/identity-config.png)

畫布會更新以反映變更，而選取的欄位會取得指紋符號(![](/help/images/icons/identity-service.png))以將其指定為身分。 在左側欄中，身分欄位現在會列在提供結構描述欄位的類別或結構描述欄位群組的名稱底下。

如果欄位也設定為主要身分，它也會列在左側邊欄的&#x200B;**[!UICONTROL 必要欄位]**&#x200B;下。 如果身分欄位巢狀內嵌於架構結構中，則所有父欄位也會依需求列出。

![](../../images/ui/fields/special/identity-applied.png)

如果您已定義結構描述的主要身分，您現在可以繼續[啟用結構描述以用於Real-Time Customer Profile](../resources/schemas.md#profile)。

## 後續步驟

本指南說明如何在UI中定義身分欄位。 使用此結構描述擷取資料時，您的客戶身分圖表將會更新，以反映結構描述的身分欄位。 請參閱[身分圖表檢視器](../../../identity-service/features/identity-graph-viewer.md)上的指南，瞭解如何在UI中探索您組織的私人圖表。

請參閱[在UI](./overview.md#special)中定義欄位的概觀，瞭解如何在[!DNL Schema Editor]中定義其他XDM欄位型別。

