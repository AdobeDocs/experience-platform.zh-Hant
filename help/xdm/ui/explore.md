---
keywords: Experience Platform；首頁；熱門主題；ui；UI；XDM；XDM系統；體驗資料模型；體驗資料模型；資料模型；資料模型；探索；類別；欄位群組；資料型別；結構描述；
solution: Experience Platform
title: 探索UI中的結構描述資源
description: 瞭解如何在Experience Platform使用者介面中探索現有結構描述、類別、結構描述欄位群組和資料型別。
type: Tutorial
exl-id: b527b2a0-e688-4cfe-a176-282182f252f2
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1360'
ht-degree: 0%

---

# 探索UI中的結構描述資源

在Adobe Experience Platform中，所有Experience Data Model (XDM)結構描述資源都儲存在[!DNL Schema Library]中，包括Adobe提供的標準資源以及您組織定義的自訂資源。 在Experience Platform UI中，您可以檢視[!DNL Schema Library]中任何現有結構描述、類別、欄位群組或資料型別的結構和欄位。 這在計畫和準備資料擷取時特別有用，因為UI會提供關於這些XDM資源提供的每個欄位的預期資料型別和使用案例的資訊。

本教學課程涵蓋在Experience Platform UI中探索現有結構描述、類別、欄位群組和資料型別的步驟。

## 查詢結構描述資源 {#lookup}

在Experience Platform UI中，選取左側導覽中的&#x200B;**[!UICONTROL 結構描述]**。 [!UICONTROL 結構描述]工作區提供&#x200B;**[!UICONTROL 瀏覽]**&#x200B;索引標籤以探索您組織中的所有結構描述，以及其他專用索引標籤以分別探索&#x200B;**[!UICONTROL 類別]**、**[!UICONTROL 欄位群組]**、**[!UICONTROL 資料型別]**&#x200B;和&#x200B;**[!UICONTROL 關係]**。

![包含數個反白索引標籤的結構描述工作區。](../images/ui/explore/tabs.png)

篩選圖示（![篩選圖示影像](/help/images/icons/filter.png)）在左側邊欄中顯示控制項，以縮小列出的結果。 資源篩選器可分別用於&#x200B;**[!UICONTROL 瀏覽]**&#x200B;和&#x200B;**[!UICONTROL 關係]**&#x200B;標籤上的結構描述和關係。

在[!UICONTROL 結構描述]工作區的[!UICONTROL 瀏覽]索引標籤上，您可以篩選結構描述詳細目錄。 使用&#x200B;**[!UICONTROL 包含在設定檔]**&#x200B;切換功能，只顯示已啟用在[即時客戶設定檔](../../profile/home.md)中使用的結構描述。 使用&#x200B;**[!UICONTROL 顯示臨機操作結構描述]**&#x200B;切換功能，篩選使用名稱空間為僅供單一資料集使用的欄位所建立的結構描述清單。

![反白顯示篩選面板的[!UICONTROL 結構描述]工作區[!UICONTROL 瀏覽]索引標籤。](../images/ui/explore/filters.png)

在[!UICONTROL 結構描述]工作區的[!UICONTROL Relationship]標籤上，您可以根據四個條件篩選關係清單。 篩選器包含[!UICONTROL Source結構描述]、[!UICONTROL 目的地結構描述]、[!UICONTROL Source類別]和[!UICONTROL 目的地類別]。 下表提供篩選的說明。

| 篩選器 | 說明 |
|-----------------------------------|------------|
| [!UICONTROL Source結構描述] | 若要檢視所選結構描述是起點或「來源」的所有關係，請從[!UICONTROL Source結構描述]下拉式選單中選取結構描述。 |
| [!UICONTROL 目的地結構描述] | 若要檢視所選結構描述為目標或「目的地」的所有關係，請從[!UICONTROL 目的地結構描述]下拉式選單中選取結構描述。 |
| [!UICONTROL Source類別] | 若要根據起始結構描述的類別篩選關係，請從[!UICONTROL Source class]下拉式選單中選取類別。 |
| [!UICONTROL 目的地類別] | 若要顯示以特定類別的結構描述結尾的關係，請從[!UICONTROL 目的地類別]下拉式選單中選取類別。 |

{style="table-layout:auto"}

![反白顯示篩選區段的[關係]索引標籤。](../images/ui/explore/relationships-filter.png)

您也可以使用搜尋列進一步縮小結果的範圍。

![搜尋欄位反白顯示的[結構描述]工作區的[瀏覽]索引標籤。](../images/ui/explore/search.png)

搜尋結果中顯示的資源會先依標題比對排序，然後依說明比對排序。 反過來，符合這些類別的單字越多，資源在清單中顯示的位置就越高。

找到要探索的資源後，從清單中選取其名稱，以在畫布中檢視其結構。

## 在畫布中探索XDM資源 {#explore}

選取資源後，其結構會在畫布中開啟。

![顯示Commerce資料型別的資料型別工作區畫布。](../images/ui/explore/canvas.png)

所有包含子屬性的物件型別欄位首次出現在畫布中時，預設會收合。 若要顯示任何欄位的子屬性，請選取其名稱旁的圖示。

![資料型別工作區畫布具有展開的欄位和強調的子屬性。](../images/ui/explore/field-expand.png)

### 標準類別和欄位群組指標 {#standard-class-and-field-group-indicator}

在結構描述編輯器中，標準(Adobe產生的)類別和欄位群組會以掛鎖圖示(![掛鎖圖示表示。](/help/images/icons/lock-closed.png)。掛鎖會顯示在類別或欄位群組名稱旁的左側邊欄中，也會顯示在架構圖表中，屬於系統產生資源之一部分的任何欄位旁邊。

![結構描述編輯器反白顯示掛鎖圖示](../images/ui/explore/schema-editor-padlock-icon.png)

請參閱[將自訂欄位新增到標準欄位群組](./resources/schemas.md)檔案以取得指引。 您無法編輯標準類別。

### 系統產生的欄位 {#system-fields}

某些欄位名稱的前置字元為底線，例如`_repo`和`_id`。 這些代表系統將在擷取資料時自動產生並指派之欄位的預留位置。

因此，大部分這些欄位在擷取至Experience Platform時應該從資料結構中排除。 此規則的主要例外是[`_{TENANT_ID}`欄位](../api/getting-started.md#know-your-tenant_id)，在您組織下建立的所有XDM欄位都必須位於該欄位之下。

### 資料類型 {#data-types}

對於畫布中顯示的每個欄位，其對應的資料型別會顯示在名稱旁邊，以指出該欄位預期擷取的資料型別。

![畫布上顯示的郵寄地址資料型別及其相關聯的資料型別已反白顯示。](../images/ui/explore/data-types.png)

任何附加了方括弧(`[]`)的資料型別都代表該特定資料型別的陣列。 例如，**[!UICONTROL String]\[]**&#x200B;的資料型別表示欄位需要字串值的陣列。 **[!UICONTROL 付款專案]\[]**&#x200B;的資料型別表示符合[!UICONTROL 付款專案]資料型別的物件陣列。

如果陣列欄位是以物件型別為基礎，您可以在畫布中選取其圖示，以顯示每個陣列專案的預期屬性。

![畫布中的物件反白顯示陣列欄位，並顯示每個陣列專案的預期屬性。](../images/ui/explore/array-type.png)

### [!UICONTROL 欄位屬性] {#field-properties}

當您選取畫布中任何欄位的名稱時，右邊欄會更新，以在&#x200B;**[!UICONTROL 欄位屬性]**&#x200B;下顯示該欄位的詳細資訊。 其中包括欄位預期使用案例、預設值、模式、格式、欄位是否為必填等內容的說明。

![從Commerce資料型別中選取的欄位，其欄位屬性已反白顯示。](../images/ui/explore/field-properties.png)

如果您要檢查的欄位是列舉欄位，右側邊欄也會顯示欄位預期會收到的可接受值。

![結構描述編輯器已選取欄位，且欄位屬性邊欄中反白顯示的列舉值和顯示名稱。](../images/ui/explore/enum-field.png)

### 身分識別欄位 {#identity}

檢查包含身分欄位的結構描述時，這些欄位會列在左側邊欄中，位於類別或欄位群組（提供這些欄位給結構描述）下方。 在左側邊欄中選取身分欄位名稱，以顯示畫布中的欄位，無論其巢狀深度為何。

畫布中的身分欄位會以指紋圖示（![指紋圖示影像](/help/images/icons/identity-service.png)）強調顯示。 如果您選取身分欄位名稱，則可以檢視其他資訊，例如[身分名稱空間](../../identity-service/features/namespaces.md)，以及該欄位是否為結構描述的主要身分。

![結構描述編輯器在左側邊欄中反白顯示結構描述身分、在結構描述圖表中反白顯示的欄位，以及在欄位屬性中反白顯示的身分名稱空間。](../images/ui/explore/identity-field.png)

>[!NOTE]
>
>請參閱[定義身分欄位](./fields/identity.md)的指南，以取得身分欄位及其與下游Experience Platform服務關係的詳細資訊。

### 關係欄位 {#relationship}

如果您正在檢查包含關聯性欄位的結構描述，該欄位將會列在左側邊欄的&#x200B;**[!UICONTROL 關聯性]**&#x200B;下。 在左側邊欄中選取關係欄位名稱，以顯示畫布中的欄位，無論其巢狀深度為何。 關聯性欄位在畫布中也以唯一方式反白顯示，顯示該欄位連結到的參考結構描述名稱。 對於具有B2B功能的組織，在這些情況下，可以寫入自訂關係名稱並將顯示在畫布上。

![結構描述編輯器，其關聯欄位和編輯關聯性已反白顯示。](../images/ui/explore/relationship-field.png)

若要檢視參考結構描述主要身分的身分名稱空間，請選取關聯性欄位，然後在[!UICONTROL 欄位屬性]側邊欄中選取&#x200B;**[!UICONTROL 編輯關聯性]**。 關聯性的引數會顯示在顯示的[!UICONTROL 編輯關聯性]對話方塊中。

![顯示關聯性引數的[編輯關聯性]對話方塊。](../images/ui/explore/edit-relationship-dialog.png)

請參閱有關[在UI](../tutorials/relationship-ui.md)中建立關聯性的教學課程，以瞭解在XDM結構描述中使用關聯性的詳細資訊。

## 後續步驟

本檔案說明如何在Experience Platform UI中探索現有的XDM資源。 如需[!UICONTROL 結構描述]工作區和[!DNL Schema Editor]不同功能的詳細資訊，請參閱[[!UICONTROL 結構描述]工作區概觀](./overview.md)。
