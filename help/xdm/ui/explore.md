---
keywords: Experience Platform；首頁；熱門主題；UI;UI;XDM;XDM系統；體驗資料模型；體驗資料模型；資料模型；資料模型；探索；類別；欄位群組；資料類型；結構；
solution: Experience Platform
title: 在UI中探索結構資源
description: 了解如何在Experience Platform使用者介面中探索現有結構、類別、結構欄位群組和資料類型。
topic-legacy: tutorial
type: Tutorial
exl-id: b527b2a0-e688-4cfe-a176-282182f252f2
source-git-commit: 744d87c82b7e7e06782c6c1b9db2ec46a5444d28
workflow-type: tm+mt
source-wordcount: '957'
ht-degree: 0%

---

# 在UI中探索結構資源

在Adobe Experience Platform中，所有Experience Data Model(XDM)結構資源都儲存在 [!DNL Schema Library]，包括Adobe提供的標準資源和貴組織定義的自訂資源。 在Experience PlatformUI中，您可以在 [!DNL Schema Library]. 這在規劃和準備資料擷取時特別實用，因為UI會提供這些XDM資源所提供之每個欄位的預期資料類型和使用案例資訊。

本教學課程涵蓋在Experience PlatformUI中探索現有結構、類別、欄位群組和資料類型的步驟。

## 查找架構資源 {#lookup}

在平台UI中，選取 **[!UICONTROL 結構]** 的下一頁。 此 [!UICONTROL 結構] 工作區提供 **[!UICONTROL 瀏覽]** 索引標籤，以探索組織中的所有結構，以及其他專用索引標籤，以探索 **[!UICONTROL 類別]**, **[!UICONTROL 欄位群組]**，和 **[!UICONTROL 資料類型]** 分別為5個。

![](../images/ui/explore/tabs.png)

篩選圖示(![篩選表徵圖影像](../images/ui/explore/icon.png))會顯示左側邊欄中的控制項，以縮小列出的結果。 顯示的控制項會因列出的資源類型而異。

例如，若要篩選清單以僅顯示Adobe提供的標準資料類型，請選取 **[!UICONTROL 資料類型]** 和 **[!UICONTROL Adobe]** 在 **[!UICONTROL 類型]** 和 **[!UICONTROL 擁有者]** 區段。

此 **[!UICONTROL 包含在設定檔中]** 切換可讓您篩選結果，只顯示在已啟用供使用的結構中使用的資源 [即時客戶個人檔案](../../profile/home.md).

![](../images/ui/explore/filter.png)

將資源列於 **[!UICONTROL 類別]**, **[!UICONTROL 欄位群組]**，或 **[!UICONTROL 資料類型]** 索引標籤，您可以選取 **[!UICONTROL Adobe]** 僅顯示標準資源或 **[!UICONTROL 客戶]** 僅顯示貴組織建立的資源。

![](../images/ui/explore/filter-data-type.png)

您也可以使用搜尋列進一步縮小結果範圍。

![](../images/ui/explore/search.png)

搜索結果中顯示的資源首先按標題匹配排序，然後按說明匹配排序。 反過來，任一類別中符合的字詞越多，清單中出現的資源就越多。

找到要探索的資源後，從清單中選取其名稱以在畫布中檢視其結構。

## 在畫布中探索XDM資源 {#explore}

選取資源後，其結構會在畫布中開啟。

![](../images/ui/explore/canvas.png)

包含子屬性的所有對象類型欄位首次出現在畫布中時，預設會收合。 若要顯示任何欄位的子屬性，請選取其名稱旁的圖示。

![](../images/ui/explore/field-expand.png)

### 系統生成欄位 {#system-fields}

有些欄位名稱會以底線為前置詞，例如 `_repo` 和 `_id`. 這些代表欄位的預留位置，系統會在擷取資料時自動產生並指派。

因此，擷取至Platform時，這些欄位大多應排除在資料結構之外。 此規則的主要例外是 [`_{TENANT_ID}` 欄位](../api/getting-started.md#know-your-tenant_id)，您組織下建立的所有XDM欄位都必須以下的命名空間命名。

### 資料類型 {#data-types}

對於畫布中顯示的每個欄位，其對應的資料類型會顯示在其名稱旁，一覽地指出該欄位預期擷取的資料類型。

![](../images/ui/explore/data-types.png)

附加方括弧(`[]`)代表該特定資料類型的陣列。 例如，資料類型為 **[!UICONTROL 字串]\[]** 指出欄位預期字串值的陣列。 資料類型 **[!UICONTROL 付款項]\[]** 指示符合 [!UICONTROL 付款項] 資料類型。

如果陣列欄位是根據對象類型，則可以在畫布中選取其圖示，以顯示每個陣列項目的預期屬性。

![](../images/ui/explore/array-type.png)

### [!UICONTROL 欄位屬性] {#field-properties}

當您在畫布中選取任何欄位的名稱時，右側邊欄會更新，顯示下方該欄位的詳細資訊 **[!UICONTROL 欄位屬性]**. 這可包含欄位預期使用案例、預設值、模式、格式的說明，無論欄位是否必要，等等。

![](../images/ui/explore/field-properties.png)

如果您檢查的欄位是列舉欄位，右側邊欄也會顯示欄位預期會收到的可接受值。

![](../images/ui/explore/enum-field.png)

### 身分欄位 {#identity}

檢查包含身分欄位的結構時，這些欄位會列在提供給結構的類別或欄位群組下的左側欄中。 在左側邊欄中選取身分欄位名稱，以顯示畫布中的欄位，無論欄位巢狀的深度為何。

身分欄位在畫布中會以指紋圖示(![指紋表徵圖影像](../images/ui/explore/identity-symbol.png))。 如果您選取身分欄位的名稱，則可以檢視其他資訊，例如 [身分命名空間](../../identity-service/namespaces.md) 以及欄位是否為架構的主要身分。

![](../images/ui/explore/identity-field.png)

>[!NOTE]
>
>請參閱 [定義身分欄位](./fields/identity.md) 以取得身分欄位及其與下游Platform服務之關係的詳細資訊。

### 關係欄位 {#relationship}

如果您檢查包含關係欄位的結構，欄位將列在下方的左側邊欄中 **[!UICONTROL 關係]**. 在左側邊欄中選取關係欄位名稱，以顯示畫布中的欄位，而無論其巢狀深度為何。

關係欄位也會在畫布中唯一強調顯示，顯示欄位所參考的目標架構名稱。 如果您選取關係欄位的名稱，您可以在右側邊欄中檢視目的地架構主要身分識別的身分命名空間。

![](../images/ui/explore/relationship-field.png)

>[!NOTE]
>
>請參閱 [在UI中建立關係](../tutorials/relationship-ui.md) 以取得在XDM結構中使用關係的詳細資訊。

## 後續步驟

本檔案說明如何在Experience PlatformUI中探索現有的XDM資源。 如需 [!UICONTROL 結構] 工作區與 [!DNL Schema Editor]，請參閱 [[!UICONTROL 結構] 工作區概述](./overview.md).
