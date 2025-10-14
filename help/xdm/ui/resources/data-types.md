---
keywords: Experience Platform；首頁；熱門主題；ui；XDM；XDM系統；體驗資料模型；體驗資料模型；資料模型；資料模型；結構描述登入；結構描述登入；結構描述；結構描述；結構描述；建立；資料型別；
solution: Experience Platform
title: 使用UI建立及編輯資料型別
type: Tutorial
description: 瞭解如何在Experience Platform使用者介面中建立和編輯資料型別。
exl-id: 2c917154-c425-463c-b8c8-04ba37d9247b
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1387'
ht-degree: 6%

---

# 使用 UI 建立和編輯資料類型 {#ui-create-and-edit}

>[!CONTEXTUALHELP]
>id="platform_schemas_datatype_filter"
>title="標準或自訂資料類型篩選器"
>abstract="可用資料類型清單已根據其建立方式預先進行篩選。選取選項按鈕，在「標準」和「自訂」選項之間進行選擇。標準選項顯示由 Adobe 建立的實體，而自訂選項顯示在您的組織內建立的實體。請參閱文件以了解更多有關建立和編輯資料類型的資訊。"

在體驗資料模型(XDM)中，資料型別是包含多個子欄位的可重複使用欄位。 雖然資料型別與結構描述欄位群組類似，因為其允許一致地使用多欄位結構，但資料型別更靈活，因為它們可以包含在結構描述結構中的任意位置，而欄位群組只能新增到根層級。

Adobe Experience Platform提供許多標準資料型別，可用於涵蓋各種常見的體驗管理使用案例。 不過，您也可以定義自己的自訂資料型別，以滿足獨特的業務需求。

>[!NOTE]
>
>如果欄位定義為特定資料型別，則無法在另一個結構描述中以不同的資料型別建立相同的欄位。 此限制適用於您組織的租使用者。

本教學課程涵蓋在Experience Platform使用者介面中建立和編輯自訂資料型別的步驟。

## 先決條件 {#prerequisites}

本指南需要實際瞭解XDM系統。 請參閱[XDM總覽](../../home.md)，瞭解XDM在Experience Platform生態系統中的角色簡介，以及[結構描述組合基本概念](../../schema/composition.md)，瞭解資料型別對XDM結構描述的貢獻。

雖然本指南並非必要專案，但建議您也按照有關[在UI](../../tutorials/create-schema-ui.md)中構成結構描述的教學課程，熟悉[!DNL Schema Editor]的各種功能。

## 開啟資料型別的[!DNL Schema Editor] {#data-type}

在Experience Platform UI中，選取左側導覽中的&#x200B;**[!UICONTROL 結構描述]**&#x200B;以開啟[!UICONTROL 結構描述]工作區，然後選取&#x200B;**[!UICONTROL 資料型別]**&#x200B;索引標籤。 畫面隨即顯示可用資料型別清單。 系統會根據資料型別的建立方式自動篩選資料型別清單。 預設設定會顯示Adobe定義的資料型別。 您還可以篩選清單以顯示您的組織建立的清單。

![左側導覽中有[!UICONTROL 個結構描述]且[!UICONTROL 資料型別]反白顯示的[!UICONTROL 結構描述]工作區。](../../images/ui/resources/data-types/data-types-tab.png)

從這裡，您有以下選項：

- [建立新的資料型別](#create)
- [篩選資料型別](#filter)
- [選取要編輯的現有資料型別](#edit)

### 建立新的資料型別 {#create}

從&#x200B;**[!UICONTROL 資料型別]**&#x200B;索引標籤中，選取&#x200B;**[!UICONTROL 建立資料型別]**。

![&#x200B; [!UICONTROL 結構描述]工作區[!UICONTROL 資料型別]索引標籤，其中[!UICONTROL 建立資料型別]已反白顯示。](../../images/ui/resources/data-types/create.png)

[!DNL Schema Editor]隨即顯示，顯示畫布中新資料型別的目前結構。 在編輯器的右側，您可以為資料型別提供顯示名稱和可選說明。 請確定您為您的資料型別提供唯一且簡潔的名稱，因為這是將資料型別新增至結構描述時識別資料型別的方式。

本教學課程會建立描述餐廳屬性的資料型別，因此該資料型別的顯示名稱為「餐廳」。

![](../../images/ui/resources/data-types/data-type-properties.png)

從這裡，您可以跳到[下一節](#add-fields)，開始將欄位新增到新資料型別。

### 篩選資料型別 {#filter}

可用資料類型清單已根據其建立方式預先進行篩選。選取選項按鈕以在[!UICONTROL 標準]與[!UICONTROL 自訂]選項之間選擇。 [!UICONTROL 標準]選項會顯示Adobe建立的實體，而[!UICONTROL 自訂]選項則會顯示貴組織內建立的實體。

![&#x200B; [!UICONTROL 結構描述]工作區的[!UICONTROL 資料型別]索引標籤中反白顯示[!UICONTROL 標準]和[!UICONTROL 自訂]。](../../images/ui/resources/data-types/standard-and-custom-data-types.png)

### 編輯現有的資料型別 {#edit}

>[!NOTE]
>
>在已啟用用於即時客戶個人檔案的結構描述中使用現有資料型別後，此後只能對該資料型別進行非破壞性變更。 如需詳細資訊，請參閱結構描述演化[&#128279;](../../schema/composition.md#evolution)的規則。

只能編輯您的組織定義的自訂資料型別。 選取&#x200B;**[!UICONTROL 自訂]**&#x200B;以僅顯示貴組織擁有的自訂資料型別。

從清單中選取您要編輯的資料型別，以開啟右側邊欄，顯示資料型別的詳細資訊。 您還可以從詳細資料面板下載範例檔案、複製JSON結構或將資料型別新增到套件中。

在右側邊欄中選取資料型別的名稱，以在[!DNL Schema Editor]中開啟其結構。

![&#x200B; [!UICONTROL 結構描述]工作區的[!UICONTROL 資料型別]索引標籤，資料型別為[!UICONTROL 自訂]且資料型別為[!UICONTROL 名稱]，已強調顯示。](../../images/ui/resources/data-types/edit.png)

## 新增欄位至資料型別 {#add-fields}

若要開始將欄位新增至資料型別，請在畫布的根層級欄位旁選取&#x200B;**加號(+)**&#x200B;圖示。 下方會顯示新欄位，而右側邊欄會更新，以顯示新欄位的控制項。

![](../../images/ui/resources/data-types/new-field.png)

使用右側邊欄中的控制項來設定新欄位的詳細資訊。 請參閱[在UI](../fields/overview.md#define)中定義欄位的指南，以瞭解如何設定欄位並將其新增至資料型別的具體步驟。

餐廳資料型別需要字串欄位來代表餐廳名稱。 因此，[!UICONTROL 欄位名稱]設為&quot;name&quot;，[!UICONTROL 型別]設為&quot;[!UICONTROL String]&quot;。 選取&#x200B;**[!UICONTROL 套用]**&#x200B;以套用變更至欄位。

![](../../images/ui/resources/data-types/name-field.png)

視需要繼續新增更多欄位至資料型別。 範例Restaurant資料型別現在有品牌、座位容量和樓層空間的額外欄位。

![](../../images/ui/resources/data-types/more-fields.png)

除了基本欄位之外，您也可以在自訂資料型別中巢狀內嵌其他資料型別。 例如，「餐廳」資料型別需要欄位來代表屬性的實體位址。 在此案例中，您可以新增指派為標準資料型別&quot;[!UICONTROL 郵寄地址]&quot;的「地址」欄位。

![](../../images/ui/resources/data-types/address-field.png)

這說明了資料型別在描述您的資料方面可以有多大的彈性：資料型別可以使用欄位，這些欄位也是資料型別，其本身可以包含進一步的資料型別等等。 這可讓您在XDM結構描述中抽象化並重複使用通用資料模式，更輕鬆地表示複雜的資料結構。

完成新增欄位至資料型別後，請選取&#x200B;**[!UICONTROL 儲存]**&#x200B;以儲存變更並將資料型別新增至[!DNL Schema Library]。

## 將資料型別新增到結構描述 {#add-data-type}

建立資料型別後，您就可以開始在結構描述中使用它。 由於XDM結構描述是由類別和零個或多個欄位群組所組成，因此資料型別提供的欄位無法直接新增到結構描述。 反之，它們必須包含在類別或欄位群組中。

首先，請依照[將欄位新增至類別](./classes.md#add-fields)或[將欄位新增至欄位群組](./field-groups.md#add-fields)的相關步驟進行。 或者，您可以開始[將欄位直接新增到結構描述](./schemas.md#add-individual-fields)，並從那裡選擇父類別或欄位群組。 當您為新欄位選擇&#x200B;**[!UICONTROL 型別]**&#x200B;時，請從下拉式選單中選取您的資料型別名稱。

## 將多欄位物件轉換為資料型別 {#convert}

當您在[!DNL Schema Editor]中建立具有多個子欄位的物件型別欄位時，可以將該欄位轉換為資料型別，以便在不同的類別或欄位群組中使用該相同的欄位結構。

若要將物件型別欄位轉換為資料型別，請選取畫布中的欄位。 在轉換欄位之前，請確定&#x200B;**[!UICONTROL 顯示名稱]**&#x200B;描述物件將包含的資料，因為這會成為資料型別的名稱。 當您準備好要轉換欄位時，請在右側邊欄中選取&#x200B;**[!UICONTROL 轉換成新資料型別]**。

![](../../images/ui/resources/data-types/convert-object.png)

畫布會將欄位的資料型別從&quot;[!UICONTROL 物件]&quot;更新為新資料型別。 定義新欄位時，可以從&#x200B;**[!UICONTROL Type]**&#x200B;下拉式清單中選取此資料型別，以在其他類別和欄位群組中重複使用此結構。

![](../../images/ui/resources/data-types/converted.png)

## 後續步驟 {#next-steps}

本指南說明如何使用Experience Platform UI建立和編輯資料型別。 如需[!UICONTROL 結構描述]工作區功能的詳細資訊，請參閱[[!UICONTROL 結構描述]工作區概觀](../overview.md)。

若要瞭解如何使用[!DNL Schema Registry] API管理資料型別，請參閱[資料型別端點指南](../../api/data-types.md)。
