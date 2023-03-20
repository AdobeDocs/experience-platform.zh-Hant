---
keywords: Experience Platform；首頁；熱門主題；API;API;XDM;XDM系統；體驗資料模型；資料模型；ui；工作區；身分；欄位；
solution: Experience Platform
title: 在UI中定義身分欄位
description: 了解如何在Experience Platform使用者介面中定義身分欄位。
exl-id: 11a53345-4c3f-4537-b3eb-ee7a5952df2a
source-git-commit: 857c1d4f74b6352e90f9c97ef22d686a883e3563
workflow-type: tm+mt
source-wordcount: '610'
ht-degree: 5%

---

# 在UI中定義身分欄位

在Experience Data Model(XDM)中，身分欄位代表一個欄位，可用來識別與記錄或時間序列事件相關的個人。 本檔案說明如何在Adobe Experience Platform UI中定義身分欄位。

## 先決條件

身分欄位是在Platform中建構客戶身分圖形的重要元件，這最終會影響即時客戶設定檔如何合併不同的資料片段，以完整了解客戶。 在定義結構中的身分欄位之前，請參閱下列檔案，以了解與身分欄位相關的重要服務和概念：

* [Adobe Experience Platform Identity Service](../../../identity-service/home.md):橋接跨裝置和系統的身分，根據資料集所遵循的XDM結構所定義的身分欄位，將資料集連結在一起。
   * [身分識別命名空間](../../../identity-service/namespaces.md):身分識別命名空間會定義可與單一人員相關的不同身分資訊類型，且是每個身分欄位的必要元件。
* [即時客戶個人檔案](../../../profile/home.md):運用客戶身分圖表，根據來自多個來源的匯總資料提供統一的消費者設定檔，且幾乎即時更新。

## 定義身分欄位 {#define-a-identity-field}

>[!CONTEXTUALHELP]
>id="platform_schemas_identityField_primaryIdentityRestriction"
>title="對主要身分的限制"
>abstract="此結構描述使用的欄位群組用於特定來源連接。此連接要求將 identityMap 做為主要身分並已自動設定。"

當 [定義新欄位](./overview.md#define) 在UI中，您可以選取 **[!UICONTROL 身分]** 核取方塊。

![](../../images/ui/fields/special/identity.png)

選取核取方塊後，會顯示其他控制項。 如果希望此欄位成為架構的主要身分，請選取 **[!UICONTROL 主要身分]** 核取方塊。

>[!NOTE]
>
>單一架構可能已定義多個身分欄位，但只能有一個主要身分。 所有身分欄位（主要或其他）都會為個別客戶的身分圖表貢獻內容，但即時客戶設定檔在將資料片段合併時，只會使用主要身分作為真相的來源。 如果要啟用架構以在配置檔案中使用，該架構必須定義主標識。

在 **[!UICONTROL 身分命名空間]**，請使用下拉式功能表，為身分欄位選取適當的命名空間。 會列出Adobe提供的標準命名空間，以及貴組織定義的任何自訂命名空間。

完成後，請選取 **[!UICONTROL 套用]** 將更改應用到架構。

![](../../images/ui/fields/special/identity-config.png)

畫布會更新以反映變更，選取的欄位會獲得指紋符號(![](../../images/ui/fields/special/identity-symbol.png))，將其指定為身分。 在左側邊欄中，身分欄位現在會列在類別或架構欄位群組的名稱下，該群組會為架構提供欄位。

如果欄位也設為主要身分，則也會列在 **[!UICONTROL 必填欄位]** 在左側邊欄。 如果在架構結構內巢狀內嵌身分欄位，則所有上層欄位也將視需要列出。

![](../../images/ui/fields/special/identity-applied.png)

如果您為結構定義了主要身分，現在可以繼續 [啟用結構以用於即時客戶個人檔案](../resources/schemas.md#profile).

## 後續步驟

本指南說明如何在UI中定義身分欄位。 使用此結構擷取資料時，您的客戶身分圖表將會更新，以反映結構的身分欄位。 請參閱 [身分圖表檢視器](../../../identity-service/ui/identity-graph-viewer.md) 了解如何在UI中探索貴組織的私密圖表。

請參閱 [定義UI中的欄位](./overview.md#special) 若要了解如何定義 [!DNL Schema Editor].
