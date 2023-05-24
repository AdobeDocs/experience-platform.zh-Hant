---
keywords: Experience Platform；主題；熱門主題；api;API;XDM;XDM系統；經驗資料模型；資料模型；ui;workspace;identity;field;
solution: Experience Platform
title: 在UI中定義標識欄位
description: 瞭解如何在Experience Platform用戶介面中定義標識欄位。
exl-id: 11a53345-4c3f-4537-b3eb-ee7a5952df2a
source-git-commit: 857c1d4f74b6352e90f9c97ef22d686a883e3563
workflow-type: tm+mt
source-wordcount: '610'
ht-degree: 5%

---

# 在UI中定義標識欄位

在體驗資料模型(XDM)中，標識欄位表示一個欄位，該欄位可用於標識與記錄或時間系列事件相關的個人。 本文檔介紹如何在Adobe Experience PlatformUI中定義標識欄位。

## 先決條件

身份欄位是如何在平台中構建客戶身份圖的關鍵元件，它最終影響即時客戶配置檔案如何將不同的資料片段合併到一起以獲得客戶的完整視圖。 在架構中定義標識欄位之前，請參閱以下文檔以瞭解與標識欄位相關的關鍵服務和概念：

* [Adobe Experience Platform身份服務](../../../identity-service/home.md):跨設備和系統橋接身份，根據它們遵循的XDM架構定義的身份欄位將資料集連結在一起。
   * [標識命名空間](../../../identity-service/namespaces.md):標識名稱空間定義可與單個人相關的不同類型的標識資訊，並且是每個標識欄位的必需元件。
* [即時客戶配置檔案](../../../profile/home.md):利用客戶身份圖表，根據來自多個來源的聚合資料提供統一的消費者配置檔案，這些資料幾乎即時更新。

## 定義標識欄位 {#define-a-identity-field}

>[!CONTEXTUALHELP]
>id="platform_schemas_identityField_primaryIdentityRestriction"
>title="對主要身分識別的限制"
>abstract="此方案使用的欄位群組用於特定來源連接。此連線要求將 identityMap 做為主要身分識別並已自動設定。"

當 [定義新欄位](./overview.md#define) 在UI中，通過選擇 **[!UICONTROL 身份]** 的子菜單。

![](../../images/ui/fields/special/identity.png)

選中該複選框後，將顯示其他控制項。 如果希望此欄位是架構的主標識，請選擇 **[!UICONTROL 主標識]** 複選框。

>[!NOTE]
>
>單個架構可能定義了多個標識欄位，但只能有一個主標識。 所有標識欄位（主要或其他）都會為單個客戶的標識圖形提供幫助，但即時客戶配置檔案在合併資料片段時只使用主標識作為真相來源。 如果要啟用在配置檔案中使用的架構，則該架構必須定義主標識。

下 **[!UICONTROL 標識命名空間]**，使用下拉菜單為標識欄位選擇適當的命名空間。 列出了Adobe提供的標準命名空間以及您的組織定義的任何自定義命名空間。

完成後，選擇 **[!UICONTROL 應用]** 將更改應用到架構。

![](../../images/ui/fields/special/identity-config.png)

畫布將更新以反映更改，選定欄位將獲取指紋符號(![](../../images/ui/fields/special/identity-symbol.png))將其指定為標識。 在左欄中，標識欄位現在列在為架構提供該欄位的類或架構欄位組的名稱下。

如果欄位也設定為主標識，則還將在 **[!UICONTROL 必填欄位]** 左欄。 如果標識欄位嵌套在架構結構中，則所有父欄位也將根據需要列出。

![](../../images/ui/fields/special/identity-applied.png)

如果為架構定義了主標識，則現在可以繼續 [啟用方案以在Real-Time Customer Profile中使用](../resources/schemas.md#profile)。

## 後續步驟

本指南介紹如何在UI中定義標識欄位。 當使用此架構接收資料時，您的客戶標識圖將更新以反映該架構的標識欄位。 請參閱 [標識圖查看器](../../../identity-service/ui/identity-graph-viewer.md) 瞭解如何在UI中瀏覽組織的專用圖表。

請參閱 [定義UI中的欄位](./overview.md#special) 瞭解如何在 [!DNL Schema Editor]。
