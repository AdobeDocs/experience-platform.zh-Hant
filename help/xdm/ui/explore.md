---
keywords: Experience Platform；主題；熱門主題；UI;UI;XDM;XDM系統；體驗資料模型；體驗資料模型；資料模型；資料模型；瀏覽；類；欄位組；資料類型；架構；
solution: Experience Platform
title: 在UI中瀏覽架構資源
description: 瞭解如何在Experience Platform用戶介面中瀏覽現有架構、類、架構欄位組和資料類型。
type: Tutorial
exl-id: b527b2a0-e688-4cfe-a176-282182f252f2
source-git-commit: 7021725e011a1e1d95195c6c7318ecb5afe05ac6
workflow-type: tm+mt
source-wordcount: '958'
ht-degree: 0%

---

# 在UI中瀏覽架構資源

在Adobe Experience Platform，所有體驗資料模型(XDM)架構資源都儲存在 [!DNL Schema Library]包括由Adobe提供的標準資源和由您的組織定義的自定義資源。 在Experience PlatformUI中，可以查看中任何現有架構、類、欄位組或資料類型的結構和欄位 [!DNL Schema Library]。 這在規劃和準備資料接收時特別有用，因為UI提供了有關這些XDM資源提供的每個欄位的預期資料類型和使用案例的資訊。

本教程介紹了在Experience PlatformUI中探索現有架構、類、欄位組和資料類型的步驟。

## 查找架構資源 {#lookup}

在平台UI中，選擇 **[!UICONTROL 架構]** 的子菜單。 的 [!UICONTROL 架構] 工作區提供 **[!UICONTROL 瀏覽]** 頁籤，用於瀏覽組織中的所有架構，以及其他專用頁籤，用於 **[!UICONTROL 類]**。 **[!UICONTROL 欄位組]**, **[!UICONTROL 資料類型]** 分別進行。

![](../images/ui/explore/tabs.png)

篩選器表徵圖(![篩選表徵圖影像](../images/ui/explore/icon.png))顯示左滑軌中的控制項，以縮小列出的結果。 顯示的控制項因所列資源類型而異。

例如，要篩選清單以僅顯示Adobe提供的標準資料類型，請選擇 **[!UICONTROL 資料類型]** 和 **[!UICONTROL Adobe]** 下 **[!UICONTROL 類型]** 和 **[!UICONTROL 所有者]** 的下界。

的 **[!UICONTROL 包括在配置檔案中]** 切換允許您篩選結果以僅顯示在已啟用供使用的方案中使用的資源 [即時客戶配置檔案](../../profile/home.md)。

![](../images/ui/explore/filter.png)

將資源列在 **[!UICONTROL 類]**。 **[!UICONTROL 欄位組]**&#x200B;或 **[!UICONTROL 資料類型]** 頁籤，可以選擇 **[!UICONTROL Adobe]** 僅顯示標準資源或 **[!UICONTROL 客戶]** 只顯示您的組織建立的資源。

![](../images/ui/explore/filter-data-type.png)

也可以使用搜索欄進一步縮小結果範圍。

![](../images/ui/explore/search.png)

搜索結果中顯示的資源首先按標題匹配，然後按說明匹配排序。 反過來，這些類別中匹配的單詞越多，資源在清單中的顯示越高。

找到要瀏覽的資源後，請從清單中選擇其名稱，以在畫布中查看其結構。

## 在畫布中瀏覽XDM資源 {#explore}

選擇資源後，其結構將在畫布中開啟。

![](../images/ui/explore/canvas.png)

預設情況下，包含子屬性的所有對象類型欄位在首次出現在畫布中時都會折疊。 要顯示任何欄位的子屬性，請選擇其名稱旁的表徵圖。

![](../images/ui/explore/field-expand.png)

### 系統生成的欄位 {#system-fields}

某些欄位名稱以下划線(如 `_repo` 和 `_id`。 這些表示系統將在接收資料時自動生成和分配的欄位的佔位符。

因此，在登錄到平台時，這些欄位中的大多數應從資料結構中排除。 此規則的主要例外是 [`_{TENANT_ID}` 場](../api/getting-started.md#know-your-tenant_id)，在您的組織下建立的所有XDM欄位必須與之同名。

### 資料類型 {#data-types}

對於畫布中顯示的每個欄位，其相應的資料類型會顯示在其名稱旁邊，它一目瞭然地表示該欄位需要接收的資料類型。

![](../images/ui/explore/data-types.png)

附加有方括弧(`[]`)表示該特定資料類型的陣列。 例如， **[!UICONTROL 字串]\[]** 指示欄位需要字串值的陣列。 資料類型 **[!UICONTROL 付款項]\[]** 指示符合 [!UICONTROL 付款項] 資料類型。

如果陣列欄位基於對象類型，則可以在畫布中選擇其表徵圖以顯示每個陣列項的預期屬性。

![](../images/ui/explore/array-type.png)

### [!UICONTROL 欄位屬性] {#field-properties}

選擇畫布中任何欄位的名稱時，右滑軌將更新以顯示下方有關該欄位的詳細資訊 **[!UICONTROL 欄位屬性]**。 這可以包括欄位的預期使用情形、預設值、模式、格式的說明，以及是否需要該欄位等。

![](../images/ui/explore/field-properties.png)

如果您正在檢查的欄位是枚舉欄位，則右欄還將顯示該欄位預期接收的可接受值。

![](../images/ui/explore/enum-field.png)

### 身分欄位 {#identity}

在檢查包含標識欄位的方案時，這些欄位將列在向方案提供它們的類或欄位組的左欄中。 選擇左滑軌中的標識欄位名稱以顯示畫布中的欄位，而不管其嵌套程度如何。

標識欄位在畫布中用指紋表徵圖突出顯示(![指紋表徵圖影像](../images/ui/explore/identity-symbol.png))。 如果選擇標識欄位的名稱，則可以查看其他資訊，如 [標識命名空間](../../identity-service/namespaces.md) 以及欄位是否是架構的主標識。

![](../images/ui/explore/identity-field.png)

>[!NOTE]
>
>請參閱上的指南 [定義標識欄位](./fields/identity.md) 有關身份欄位及其與下游平台服務的關係的詳細資訊。

### 關係欄位 {#relationship}

如果您正在檢查包含關係欄位的架構，該欄位將列在左側欄的下方 **[!UICONTROL 關係]**。 選擇左滑軌中的關係欄位名稱以顯示畫布中的欄位，而不管其嵌套的深度如何。

關係欄位也在畫布中唯一突出顯示，顯示欄位連結到的引用架構的名稱。 如果選擇關係欄位的名稱，則可以在右欄中查看引用架構主標識的標識命名空間。

![](../images/ui/explore/relationship-field.png)

>[!NOTE]
>
>請參閱上的教程 [在UI中建立關係](../tutorials/relationship-ui.md) 的子菜單。

## 後續步驟

本文檔介紹了如何瀏覽Experience PlatformUI中的現有XDM資源。 有關不同功能的詳細資訊 [!UICONTROL 架構] 工作區和 [!DNL Schema Editor]，請參見 [[!UICONTROL 架構] 工作區概述](./overview.md)。
