---
keywords: 體驗平台；首頁；熱門主題；ui;UI;XDM;XDM系統；體驗資料模型；體驗資料模型；資料模型；資料模型；瀏覽；類；混合；資料類型；模式；
solution: Experience Platform
title: 在UI中探索XDM資源
description: 瞭解如何在Experience Platform使用者介面中探索現有的架構、類別、混合和資料類型。
topic: tutorial
type: Tutorial
translation-type: tm+mt
source-git-commit: 912d02477febdafa4a53aebc83bc3a93b0f84f09
workflow-type: tm+mt
source-wordcount: '941'
ht-degree: 0%

---


# 在UI中探索XDM資源

在Adobe Experience Platform中，所有Experience Data Model(XDM)資源都儲存在[!DNL Schema Library]中，包括Adobe提供的標準資源以及貴組織定義的自訂資源。 在Experience Platform UI中，您可以在[!DNL Schema Library]中檢視任何現有架構、類別、混合或資料類型的結構和欄位。 當規劃和準備資料擷取時，這特別有用，因為UI會提供這些XDM資源所提供之每個欄位的預期資料類型和使用案例資訊。

本教學課程涵蓋探索Experience Platform UI中現有結構、類別、混合和資料類型的步驟。

## 查找XDM資源{#lookup}

在平台UI中，選擇左側導航中的&#x200B;**[!UICONTROL 方案]**。 [!UICONTROL 結構描述]工作區提供&#x200B;**[!UICONTROL 瀏覽]**&#x200B;標籤，以探索組織中所有現有的XDM資源，以及用於特別探索&#x200B;**[!UICONTROL 類]**、**[!UICONTROL Mixins]**&#x200B;和&#x200B;**[!UICONTROL 資料類型]**&#x200B;的附加專用標籤。

![](../images/ui/explore/tabs.png)

在[!UICONTROL Browse]標籤上，您可以使用篩選圖示（![篩選圖示影像](../images/ui/explore/icon.png)）來顯示左側導軌中的控制項，以縮小列出的結果。

例如，若要篩選清單以僅顯示Adobe提供的標準資料類型，請分別在&#x200B;**[!UICONTROL Type]**&#x200B;和&#x200B;**[!UICONTROL Owner]**&#x200B;區段下選取&#x200B;**[!UICONTROL Datatype]**&#x200B;和&#x200B;**[!UICONTROL Adobe]**。

**[!UICONTROL 包含在Profile]**&#x200B;中的切換功能可讓您篩選結果，只顯示已啟用在[即時客戶配置檔案](../../profile/home.md)中使用的架構中使用的資源。

![](../images/ui/explore/filter.png)

您也可以使用搜尋列進一步縮小結果。 在搜尋詞語時，排名最前的項目代表名稱與搜尋查詢相符的資源。 在這些項下，在&#x200B;**[!UICONTROL 標準欄位]**&#x200B;下，將列出包含與查詢匹配的欄位的所有資源。 這樣，您就可以根據所包含的資料類型來搜索XDM資源，而無需事先知道該資源的名稱。

![](../images/ui/explore/search.png)

找到要瀏覽的資源後，請從清單中選擇其名稱，以在畫布中查看其結構。

## 在畫布{#explore}中探索XDM資源

選取資源後，其結構就會在畫布中開啟。

![](../images/ui/explore/canvas.png)

包含子屬性的所有物件類型欄位在首次出現在畫布時，預設會收合。 若要顯示任何欄位的子屬性，請選取其名稱旁的圖示。

![](../images/ui/explore/field-expand.png)

### 系統生成的欄位{#system-fields}

有些欄位名稱會加上底線，例如`_repo`和`_id`。 這些代表欄位的預留位置，系統會在擷取資料時自動產生並指派。

因此，在將這些欄位匯入平台時，大部分的欄位應排除在資料結構之外。 此規則的主要例外是[`_{TENANT_ID}`欄位](../api/getting-started.md#know-your-tenant_id)，您組織下建立的所有XDM欄位都必須與之命名。

### 資料類型 {#data-types}

對於畫布中顯示的每個欄位，其對應的資料類型會顯示在其名稱旁，一覽表示該欄位預期擷取的資料類型。

![](../images/ui/explore/data-types.png)

附加方括弧(`[]`)的任何資料類型都表示該特定資料類型的陣列。 例如，**[!UICONTROL String]\[]**&#x200B;的資料類型表示欄位需要字串值的陣列。 **[!UICONTROL 付款項]\[]**&#x200B;的資料類型指示符合[!UICONTROL 付款項]資料類型的對象陣列。

如果陣列欄位基於對象類型，則可以在畫布中選擇其表徵圖以顯示每個陣列項的預期屬性。

![](../images/ui/explore/array-type.png)

### [!UICONTROL 欄位屬性] {#field-properties}

當您選取畫布中任何欄位的名稱時，右側欄位會更新，以顯示&#x200B;**[!UICONTROL 欄位屬性]**&#x200B;下方該欄位的詳細資訊。 這可包含欄位預期使用案例、預設值、模式、格式的說明，以及欄位是否必要等等。

![](../images/ui/explore/field-properties.png)

如果您正在檢查的欄位是列舉欄位，右側欄位也會顯示欄位預期接收的可接受值。

![](../images/ui/explore/enum-field.png)

### 身份欄位{#identity}

在檢查包含標識欄位的方案時，這些欄位將列在提供給方案的類或混合的左側導軌中。 選取左側欄中的識別欄位名稱，以顯示畫布中的欄位，不論欄位的巢狀有多深。

在畫布中，標識欄位會以指紋圖示（![指紋圖示影像](../images/ui/explore/identity-symbol.png)）反白顯示。 如果選擇標識欄位的名稱，則可以查看其他資訊，如[ identity namespace](../../identity-service/namespaces.md)，以及該欄位是否是架構的主標識。

![](../images/ui/explore/identity-field.png)

>[!NOTE]
>
>有關身份欄位及其與下游平台服務的關係的詳細資訊，請參閱[定義身份欄位](./fields/identity.md)上的指南。

### 關係欄位{#relationship}

如果您正在檢查包含關係欄位的方案，則該欄位將列在&#x200B;**[!UICONTROL Relations]**&#x200B;下的左側導軌中。 選取左側邊欄中的關係欄位名稱，以顯示畫布中的欄位，不論其巢狀的深度為何。

關係欄位也會在畫布中唯一反白標示，顯示欄位所參照之目標架構的名稱。 如果選擇關係欄位的名稱，則可以在右側欄中查看目標方案的主要標識的身份名稱空間。

![](../images/ui/explore/relationship-field.png)

>[!NOTE]
>
>有關在XDM結構描述中使用關係的詳細資訊，請參閱[在UI](../tutorials/create-schema-ui.md)中建立關係的教程。

## 後續步驟

本檔案說明如何在Experience Platform UI中探索現有的XDM資源。 有關[!UICONTROL 方案]工作區和[!DNL Schema Editor]的不同功能的詳細資訊，請參閱[[!UICONTROL 方案]工作區概述](./overview.md)。