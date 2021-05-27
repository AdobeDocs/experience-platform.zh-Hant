---
keywords: Experience Platform；首頁；熱門主題；UI;UI; XDM; XDM系統；體驗資料模型；體驗資料模型；資料模型；結構編輯器；結構編輯器；結構；結構；結構；結構；結構；建立
solution: Experience Platform
title: 使用結構編輯器建立結構
topic-legacy: tutorial
type: Tutorial
description: 本教學課程涵蓋以 Experience Platform 結構編輯器建立結構的相關步驟。
exl-id: 3edeb879-3ce4-4adb-a0bd-8d7ad2ec6102
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '3754'
ht-degree: 0%

---

# 使用[!DNL Schema Editor]建立架構

Adobe Experience Platform使用者介面可讓您在名為[!DNL Schema Editor]的互動式視覺畫布中建立和管理[!DNL Experience Data Model](XDM)結構。 本教學課程涵蓋如何使用[!DNL Schema Editor]建立架構。

>[!NOTE]
>
>為了示範，本教學課程中的步驟涉及建立描述客戶忠誠度計畫成員的範例結構。 雖然您可以使用這些步驟建立不同的架構以供自己使用，但建議您先按照建立範例架構的步驟來了解[!DNL Schema Editor]的功能。

如果您偏好使用[!DNL Schema Registry] API來撰寫架構，請先閱讀[[!DNL Schema Registry] 開發人員指南](../api/getting-started.md)，再嘗試使用API](create-schema-api.md)建立架構的[教學課程。

## 快速入門

本教學課程需要妥善了解Adobe Experience Platform在架構建立中涉及的各個層面。 開始本教學課程之前，請先檢閱本檔案中的下列概念：

* [[!DNL Experience Data Model (XDM)]](../home.md):組織客戶體驗資 [!DNL Platform] 料的標準化架構。
   * [結構構成基本概念](../schema/composition.md):概述XDM結構及其建置區塊，包括類別、結構欄位群組、資料類型和個別欄位。
* [[!DNL Real-time Customer Profile]](../../profile/home.md):根據來自多個來源的匯總資料，提供統一的即時消費者設定檔。

## 開啟[!UICONTROL 結構]工作區 {#browse}

[!DNL Platform] UI中的[!UICONTROL 結構]工作區提供[!DNL Schema Library]的視覺效果，讓您檢視管理組織可用的結構。 工作區也包含[!DNL Schema Editor]，您可在此教學課程中撰寫架構的畫布。

登入[!DNL Experience Platform]後，在左側導覽中選取&#x200B;**[!UICONTROL 結構]**&#x200B;以開啟&#x200B;**[!UICONTROL 結構]**&#x200B;工作區。 **[!UICONTROL Browse]**&#x200B;標籤顯示可查看和自定義的架構清單（[!DNL Schema Library]的表示）。 該清單包括架構所基於的名稱、類型、類和行為（記錄或時間序列），以及上次修改架構的日期和時間。

如需詳細資訊，請參閱[探索UI](../ui/explore.md)中現有XDM資源的指南。

## 建立架構並命名 {#create}

要開始合成架構，請選擇&#x200B;**[!UICONTROL Schemas]**&#x200B;工作區右上角的&#x200B;**[!UICONTROL Create schema]**。 此時會顯示下拉式功能表，供您選擇核心類別[!UICONTROL XDM個別設定檔]和[!UICONTROL XDM ExperienceEvent]。 如果這些類不符合您的目的，您也可以選擇&#x200B;**[!UICONTROL Browse]**&#x200B;以從其他可用類中選擇，或選擇[建立新類](#create-new-class)。

在本教學課程中，請選取&#x200B;**[!UICONTROL XDM個別設定檔]**。

![](../images/tutorials/create-schema/create_schema_button.png)

由於您選擇了標準XDM類以作為架構的基礎，因此會出現「**[!UICONTROL 添加欄位組]**」對話框，允許您立即開始向架構添加欄位。 目前，請選擇&#x200B;**[!UICONTROL 取消]**&#x200B;退出對話框。

![](../images/tutorials/create-schema/cancel-field-group.png)

出現[!DNL Schema Editor]。 這是您要在其中組成架構的畫布。 當您到達編輯器時，會自動在畫布的&#x200B;**[!UICONTROL Structure]**&#x200B;區段中建立未命名的架構，以及該類別所有架構中包含的標準欄位。 該架構的分配類也列在&#x200B;**[!UICONTROL Composition]**&#x200B;部分的&#x200B;**[!UICONTROL Class]**&#x200B;下。

![](../images/tutorials/create-schema/schema_editor.png)

>[!NOTE]
>
>您可以在儲存架構之前的初始合成程式期間的任何時間點[變更架構](#change-class)的類別，但應格外小心。 欄位組僅與某些類相容，因此更改類將重置畫布和您添加的任何欄位。

使用編輯器右側的欄位來提供結構的顯示名稱和可選說明。 輸入名稱后，畫布會更新，以反映架構的新名稱。

![](../images/tutorials/create-schema/name_schema.png)

決定結構名稱時，需考量幾項重要事項：

* 架構名稱應簡短且具描述性，以便日後輕鬆找到架構。
* 架構名稱必須是唯一的，這表示其特定性也應足夠，以免日後重複使用。 例如，如果貴組織針對不同品牌有不同的忠誠計畫，最好將您的結構命名為「品牌忠誠會員」，以便輕鬆區分與其他與忠誠度相關的結構，您稍後可能會定義。
* 您也可以使用結構描述來提供與結構相關的任何其他內容資訊。

本教學課程會組成結構來內嵌與忠誠計畫成員相關的資料，因此結構命名為「忠誠會員」。

## 添加欄位組{#field-group}

您現在可以透過新增欄位群組，開始將欄位新增至您的架構。 欄位群組是一或多個欄位的群組，通常搭配使用以描述特定概念。 本教學課程使用欄位群組來說明忠誠計畫的成員，並擷取關鍵資訊，例如名稱、生日、電話號碼、地址等。

要添加欄位組，請在&#x200B;**[!UICONTROL 欄位組]**&#x200B;子節中選擇&#x200B;**[!UICONTROL 添加]**。

![](../images/tutorials/create-schema/add-field-group-button.png)

隨即出現新對話方塊，顯示可用欄位群組的清單。 每個欄位組僅用於特定類，因此對話框僅列出與您選擇的類相容的欄位組（在此例中為[!DNL XDM Individual Profile]類）。 如果您使用標準XDM類別，欄位群組清單將會根據使用頻率聰明地排序。

![](../images/tutorials/create-schema/field-group-popularity.png)

從清單中選取欄位群組，會使其顯示在右側邊欄中。 您可以視需要選取多個欄位群組，在確認前將每個欄位新增至右側邊欄的清單。 此外，當前所選欄位組的右側將顯示一個表徵圖，允許您預覽它提供的欄位的結構。

![](../images/tutorials/create-schema/preview-field-group-button.png)

預覽欄位群組時，右側邊欄會提供欄位群組架構的詳細說明。 您也可以瀏覽所提供畫布中欄位群組的欄位。 當您選取不同欄位時，右側邊欄會更新，顯示有關欄位的詳細資訊。 完成預覽後，選擇&#x200B;**[!UICONTROL Back]**&#x200B;以返回欄位組選擇對話框。

![](../images/tutorials/create-schema/preview-field-group.png)

在本教程中，選擇&#x200B;**[!UICONTROL 人口統計詳細資料]**&#x200B;欄位組，然後選擇&#x200B;**[!UICONTROL 添加欄位組]**。

![](../images/tutorials/create-schema/demographic-details.png)

架構畫布會重新顯示。 **[!UICONTROL 欄位群組]**&#x200B;區段現在會列出「[!UICONTROL 人口統計詳細資料]」，而&#x200B;**[!UICONTROL 結構]**&#x200B;區段則包含欄位群組貢獻的欄位。 您可以在&#x200B;**[!UICONTROL 欄位群組]**&#x200B;區段下選取欄位群組的名稱，以反白顯示畫布內提供的特定欄位。

![](../images/tutorials/create-schema/demographic-details-structure.png)

此欄位組在頂層名稱`person`下按資料類型「[!UICONTROL Person]」貢獻多個欄位。 此欄位群組說明個人的相關資訊，包括姓名、出生日期和性別。

>[!NOTE]
>
>請記住，欄位可能使用標量類型（如字串、整數、陣列或日期），以及[!DNL Schema Registry]中定義的任何資料類型（表示通用概念的一組欄位）。

請注意，`name`欄位的資料類型為「[!UICONTROL 人員名稱]」，這表示它也描述了通用概念，並包含與名稱相關的子欄位，如名字、姓氏、字首和尾碼。

選取畫布中的不同欄位，以顯示它們對架構結構貢獻的任何其他欄位。

## 添加另一個欄位組{#field-group-2}

您現在可以重複相同步驟來新增其他欄位群組。 這次查看&#x200B;**[!UICONTROL 添加欄位組]**&#x200B;對話框時，請注意「[!UICONTROL 人口統計詳細資訊]」欄位組已呈灰色顯示，並且無法選中該欄位組旁邊的複選框。 這可防止您意外重複目前架構中已包含的欄位群組。

在本教程中，從對話框中選擇「[!DNL Personal Contact Details]」欄位組，然後選擇&#x200B;**[!UICONTROL 添加欄位組]**&#x200B;將其添加到架構中。

![](../images/tutorials/create-schema/personal-contact-details.png)

新增後，畫布會重新顯示。 「[!UICONTROL 個人聯繫人詳細資訊]」現在列在&#x200B;**[!UICONTROL Composition]**&#x200B;部分的&#x200B;**[!UICONTROL 欄位組]**&#x200B;下，**[!UICONTROL Structure]**&#x200B;下新增了家庭地址、行動電話等欄位。

與`name`欄位類似，您剛新增的欄位代表多欄位概念。 例如，`homeAddress`的資料類型為「[!UICONTROL 郵遞區號]」，而`mobilePhone`的資料類型為「[!UICONTROL 電話號碼]」。 您可以選取這些欄位，以展開它們，並查看資料類型中包含的其他欄位。

![](../images/tutorials/create-schema/personal-contact-details-structure.png)

## 定義自訂欄位群組{#define-field-group}

「[!UICONTROL 忠誠會員]」結構旨在擷取與忠誠計畫成員相關的資料，因此需要一些特定的忠誠相關欄位。

您可以將標準[!UICONTROL 忠誠度詳細資料]欄位群組新增至結構，以擷取與忠誠度計畫相關的常見欄位。 雖然強烈建議您使用標準欄位群組來呈現結構擷取的概念，但標準忠誠度欄位群組的結構可能無法擷取特定忠誠計畫的所有相關資料。 在此案例中，您可以選擇定義新的自訂欄位群組，以擷取這些欄位。

再次開啟「**[!UICONTROL 添加欄位組]**」對話框，但此次在頂部附近選擇「建立新欄位組&#x200B;]**」。**[!UICONTROL &#x200B;系統會要求您提供欄位群組的顯示名稱和說明。

![](../images/tutorials/create-schema/create-new-field-group.png)

與類名一樣，欄位組名應簡短，說明欄位組將對架構作何貢獻。 這些名稱也是唯一的，因此您將無法重複使用名稱，因此必須確保名稱足夠具體。

在本教學課程中，將新欄位群組命名為「忠誠度詳細資料」。

選擇&#x200B;**[!UICONTROL 添加欄位組]**&#x200B;以返回[!DNL Schema Editor]。 &quot;[!UICONTROL 忠誠度詳細資料]&quot;現在應顯示在畫布左側的&#x200B;**[!UICONTROL 欄位群組]**&#x200B;下，但沒有與其相關聯的欄位，因此在&#x200B;**[!UICONTROL Structure]**&#x200B;下面不會顯示新欄位。

## 將欄位添加到欄位組{#field-group-fields}

現在您已建立「忠誠度詳細資料」欄位群組，可以定義欄位群組將貢獻至結構的欄位。

若要開始，請在&#x200B;**[!UICONTROL 欄位群組]**&#x200B;區段中選取欄位群組名稱。 執行此操作後，欄位組的屬性會顯示在編輯器的右側，而&#x200B;**+(+)**&#x200B;圖示會出現在&#x200B;**[!UICONTROL Structure]**&#x200B;下架構名稱旁。

![](../images/tutorials/create-schema/loyalty_details_structure.png)

選取「[!DNL Loyalty Members]」旁的&#x200B;**加號(+)**&#x200B;圖示，在結構中建立新節點。 此節點（在此範例中稱為`_tenantId`）代表您的IMS組織的租用戶ID，前面加上底線。 租用戶ID的存在表示您新增的欄位包含在組織的命名空間中。

換言之，您新增的欄位對您的組織來說是唯一的，且會儲存在[!DNL Schema Registry]中您的組織僅能存取的特定區域。 您定義的欄位必須一律新增至租用戶命名空間，以避免與其他標準類別、欄位群組、資料類型和欄位的名稱衝突。

命名節點內是&quot;[!UICONTROL New Field]&quot;。 這是「[!UICONTROL 忠誠度詳細資料]」欄位群組的開頭。

![](../images/tutorials/create-schema/new_field_loyalty.png)

使用編輯器右側的控制項，首先建立一個`loyalty`欄位，其類型為「[!UICONTROL Object]」，將用於保留與忠誠度相關的欄位。 完成後，選擇&#x200B;**[!UICONTROL Apply]**。

![](../images/tutorials/create-schema/loyalty_object.png)

將應用更改，並顯示新建立的`loyalty`對象。 選取物件旁的&#x200B;**加號(+)**&#x200B;圖示，以新增其他與忠誠度相關的欄位。 畫布的右側會顯示「[!UICONTROL 新欄位]」，且「**[!UICONTROL 欄位屬性]**」區段。

![](../images/tutorials/create-schema/new_field_in_loyalty_object.png)

每個欄位都需要下列資訊：

* **[!UICONTROL 欄位名稱]:** 以駝峰式大小寫撰寫的欄位名稱。範例：loalytyLevel
* **[!UICONTROL 顯示名稱]:** 以標題寫入的欄位名稱。範例：忠誠度等級
* **[!UICONTROL 類型]:** 欄位的資料類型。這包括基本標量類型和[!DNL Schema Registry]中定義的任何資料類型。 範例：[!UICONTROL 字串]、[!UICONTROL 整數]、[!UICONTROL 布林]、[!UICONTROL 人員]、[!UICONTROL 地址]、[!UICONTROL 電話號碼]等。
* **[!UICONTROL 說明]:** 應包含欄位的選用說明，以句子寫入，最多200個字元。

`Loyalty`物件的第一個欄位將是名為`loyaltyId`的字串。 將新欄位的類型設定為&quot;[!UICONTROL String]&quot;時，**[!UICONTROL Field properties]**&#x200B;部分將填充幾個應用約束的選項，包括預設值、格式和最大長度。

![](../images/tutorials/create-schema/string_constraints.png)

根據所選資料類型，可使用不同的約束選項。 由於`loyaltyId`將是電子郵件地址，請從&#x200B;**[!UICONTROL Format]**&#x200B;下拉式選單中選擇「[!UICONTROL email]」。 選擇&#x200B;**[!UICONTROL Apply]**&#x200B;以應用更改。

![](../images/tutorials/create-schema/loyaltyId_field.png)

## 將更多欄位添加到欄位組{#field-group-fields-2}

現在您已新增`loyaltyId`欄位，可以新增其他欄位來擷取與忠誠度相關的資訊，例如：

* 點（整數）
* 會員自（日期）

若要將每個欄位新增至架構，請選取`loyalty`物件旁的&#x200B;**加號(+)**&#x200B;圖示，並填入所需資訊。

完成後，「忠誠度」物件將包含忠誠度ID、點數和成員加入後的欄位。

![](../images/tutorials/create-schema/loyalty_object_fields.png)

## 將列舉欄位新增至欄位群組 {#enum}

在[!DNL Schema Editor]中定義欄位時，有些其他選項可以套用至基本欄位類型，以便對欄位可包含的資料提供進一步的限制。 下表說明了這些限制的使用案例：

| 限制 | 說明 |
| --- | --- |
| [!UICONTROL 必填] | 指出資料擷取需要此欄位。 任何根據此結構上傳至資料集但不含此欄位的資料，在擷取時都會失敗。 |
| [!UICONTROL 陣列] | 指出欄位包含值的陣列，每個值都指定了資料類型。 例如，對資料類型為&quot;[!UICONTROL String]&quot;的欄位使用此限制會指定該欄位將包含字串的陣列。 |
| [!UICONTROL 列舉] | 指示此欄位必須包含可能值枚舉清單中的值之一。 |
| [!UICONTROL 身分] | 指出此欄位是身分欄位。 有關身分欄位的詳細資訊，請參閱本教學課程](#identity-field)的稍後內容。[ |
| [!UICONTROL 關係] | 雖然可透過使用聯合架構和[!DNL Real-time Customer Profile]來推斷架構關係，但這隻適用於共用相同類別的架構。 [!UICONTROL Relationship]約束指明此欄位引用基於不同類的架構的主標識，這表示兩個架構之間的關係。 如需詳細資訊，請參閱[定義關係](./relationship-ui.md)的教學課程。 |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>任何必要、身分或關係欄位都會顯示在左側邊欄中，讓您無論結構的複雜性為何，都能輕鬆找到這些欄位。
>
>![](../images/tutorials/create-schema/left-rail-special.png)

在本教學課程中，結構中的[!DNL "loyalty"]物件需要新的列舉欄位，該欄位描述客戶的「忠誠度」，其值只能是四個可能選項之一。 若要將此欄位新增至架構，請選取`loyalty`物件旁的&#x200B;**加號(+)**&#x200B;圖示，並填寫&#x200B;**[!UICONTROL 欄位名稱]**&#x200B;和&#x200B;**[!UICONTROL 顯示名稱]**&#x200B;的必填欄位。 對於&#x200B;**[!UICONTROL 類型]**，選擇&quot;[!UICONTROL 字串]&quot;。

![](../images/tutorials/create-schema/loyalty-level-type.png)

選取欄位類型後，欄位會出現其他核取方塊，包括&#x200B;**[!UICONTROL Array]**、**[!UICONTROL Enum]**&#x200B;和&#x200B;**[!UICONTROL Identity]**&#x200B;的核取方塊。

選取&#x200B;**[!UICONTROL Enum]**&#x200B;核取方塊以開啟下方的&#x200B;**[!UICONTROL Enum values]**&#x200B;區段。 您可以在此輸入每個可接受的忠誠度等級的&#x200B;**[!UICONTROL 值]**（在camelCase中）和&#x200B;**[!UICONTROL 標籤]**（標題案例中為選用且方便閱讀的名稱）。

完成所有欄位屬性後，選擇&#x200B;**[!UICONTROL Apply]**&#x200B;以將「[!DNL loyaltyLevel]」欄位添加到`loyalty`對象。

![](../images/tutorials/create-schema/loyalty_level_enum.png)

## 將多欄位物件轉換為資料類型 {#datatype}

`loyalty`物件現在包含數個忠誠度專屬欄位，並代表可用於其他結構的通用資料結構。 [!DNL Schema Editor]允許您通過將這些對象的結構轉換為資料類型來輕鬆應用可重複使用的多欄位對象。

資料類型允許一致地使用多欄位結構，並提供比欄位組更大的靈活性，因為它們可以在架構內的任何位置使用。 要執行此操作，請將欄位的&#x200B;**[!UICONTROL Type]**&#x200B;值設定為[!DNL Schema Registry]中定義的任何資料類型的值。

要將`loyalty`對象轉換為資料類型，請選擇&#x200B;**[!UICONTROL Structure]**&#x200B;下的`loyalty`欄位，然後選擇編輯器右側的&#x200B;**[!UICONTROL Field properties]**&#x200B;下的&#x200B;**[!UICONTROL Convert to new data type]**。 畫面會顯示綠色彈出視窗，確認物件已成功轉換。

![](../images/tutorials/create-schema/convert-data-type.png)

現在，查看&#x200B;**[!UICONTROL Structure]**&#x200B;下方時，您會看到`loyalty`欄位的資料類型為「[!DNL Loyalty]」，且欄位旁邊有小型鎖定圖示，表示它們不再是個別欄位，而是多欄位資料類型的一部分。

![](../images/tutorials/create-schema/loyalty_data_type.png)

在未來的架構中，您現在可以將欄位指派為「[!DNL Loyalty]」類型，並自動包含ID、忠誠度、成員起始時間和點的欄位。

>[!NOTE]
>
>您也可以建立和編輯自訂資料類型，而不需編輯結構。 如需詳細資訊，請參閱[建立和編輯資料類型](../ui/resources/data-types.md)的指南。

## 搜尋及篩選結構欄位

除了基礎類提供的欄位之外，您的架構現在還包含多個欄位群組。 使用較大的結構時，您可以在左側邊欄中選取欄位群組名稱旁的核取方塊，將顯示的欄位篩選為僅限您感興趣的欄位群組所提供的欄位。

![](../images/tutorials/create-schema/filter-by-field-group.png)

如果您在結構中尋找特定欄位，也可以使用搜尋列來依名稱篩選顯示的欄位，無論欄位底下提供的欄位群組為何。

![](../images/tutorials/create-schema/search.png)

>[!IMPORTANT]
>
>顯示相符欄位時，搜尋函式會考慮任何選取的欄位群組篩選器。 如果搜索查詢未顯示您期望的結果，則可能需要再次檢查您是否未篩選出任何相關欄位組。

## 將架構欄位設為身分欄位{#identity-field}

結構提供的標準資料結構可運用於跨多個來源識別屬於相同個人的資料，以支援不同的下游使用案例，例如細分、報告、資料科學分析等。 若要根據個別身分匯整資料，索引鍵欄位必須在適用結構中標示為[!UICONTROL Identity]欄位。

[!DNL Experience Platform] 借由中的「識別」核取方塊，輕鬆指 **** 出身分欄 [!DNL Schema Editor]位。不過，您必鬚根據資料的性質，決定要將哪個欄位當作身分的最佳候選欄位。

例如，可能有數千個忠誠計畫成員屬於相同的「忠誠級別」，但忠誠計畫的每個成員都有唯一的`loyaltyId`（在此例中是個別成員的電子郵件地址）。 `loyaltyId`是每個成員的唯一標識符，這使它成為身份欄位的良好候選符，而`loyaltyLevel`則否。

>[!IMPORTANT]
>
>以下概述的步驟說明如何將身份描述符添加到現有架構欄位。 除了在架構本身的結構內定義身分欄位外，您也可以使用`identityMap`欄位來改用包含身分資訊。
>
>如果您打算使用`identityMap`，請記住，它將覆蓋您直接添加到架構的任何主要標識。 有關詳細資訊，請參閱[架構組合指南](../schema/composition.md#identityMap)基礎中`identityMap`一節。

在編輯器的&#x200B;**[!UICONTROL Structure]**&#x200B;區段中，選取`loyaltyId`欄位，並在&#x200B;**[!UICONTROL Field properties]**&#x200B;下顯示&#x200B;**[!UICONTROL Identity]**&#x200B;核取方塊。 核取方塊，並選取選項以將此設定為出現&#x200B;**[!UICONTROL 主要身分]**。 也選擇此框。

>[!NOTE]
>
>每個架構只能包含一個主要身分欄位。 將架構欄位設定為主要身分後，如果您稍後嘗試將架構中的另一個身分欄位設定為主要身分，將會收到錯誤訊息。

接下來，您必須從下拉式清單中預先定義的命名空間清單中提供&#x200B;**[!UICONTROL 身分命名空間]**。 由於`loyaltyId`是客戶的電子郵件地址，請從下拉式清單中選取「[!UICONTROL 電子郵件]」。 選擇&#x200B;**[!UICONTROL 應用]**&#x200B;以確認`loyaltyId`欄位的更新。

![](../images/tutorials/create-schema/loyaltyId_primary_identity.png)

>[!NOTE]
>
>如需標準命名空間及其定義的清單，請參閱[[!DNL Identity Service] 檔案](../../identity-service/troubleshooting-guide.md#standard-namespaces)。

應用更改後，`loyaltyId`的表徵圖顯示指紋符號，表示它現在是標識欄位。

![](../images/tutorials/create-schema/identity-applied.png)

現在，擷取至`loyaltyId`欄位的所有資料都將用來協助識別該個人，並匯整該客戶的單一檢視。 若要進一步了解如何在[!DNL Experience Platform]中使用身分，請檢閱[[!DNL Identity Service]](../../identity-service/home.md)檔案。

## 啟用架構以用於[!DNL Real-time Customer Profile] {#profile}

[[!DNL Real-time Customer Profile]](../../profile/home.md) 利用中的身 [!DNL Experience Platform] 分資料，提供每個客戶的整體檢視。該服務可構建強大的360°客戶屬性配置檔案，以及客戶在與[!DNL Experience Platform]整合的任何系統中擁有的每個交互的時間戳帳戶。

若要啟用架構以便與[!DNL Real-time Customer Profile]搭配使用，必須定義主要身分。 如果您未先定義主標識而嘗試啟用架構，則會收到錯誤消息。

<img src="../images/tutorials/create-schema/missing_primary_identity.png" width="600" /><br>

若要啟用「忠誠會員」架構以用於[!DNL Profile]，請從編輯器的&#x200B;**[!UICONTROL Structure]**&#x200B;區段中選取「[!DNL Loyalty Members]」開始。

在編輯器的右側，會顯示結構的相關資訊，包括其顯示名稱、說明和類型。 除了此資訊外，還有&#x200B;**[!UICONTROL Profile]**&#x200B;切換按鈕。

![](../images/tutorials/create-schema/profile-toggle.png)

選擇&#x200B;**[!UICONTROL Profile]**&#x200B;並出現彈出窗口，要求您確認要為[!DNL Profile]啟用架構。

<img src="../images/tutorials/create-schema/enable-profile.png" width="700" /><br>

>[!WARNING]
>
>為[!DNL Real-time Customer Profile]啟用並儲存架構後，便無法停用該架構。

選擇&#x200B;**[!UICONTROL 啟用]**&#x200B;以確認您的選擇。 您可以再次選擇&#x200B;**[!UICONTROL Profile]**&#x200B;切換以禁用架構（如果希望），但一旦[!DNL Profile]啟用時已保存架構，則無法再禁用該架構。

## 後續步驟和其他資源

現在您完成架構撰寫後，就可以在畫布中看到完整的架構。 選擇&#x200B;**[!UICONTROL Save]**，架構將保存到[!DNL Schema Library]，使[!DNL Schema Registry]可訪問。

您的新架構現在可用於將資料內嵌至[!DNL Platform]。 請記住，一旦使用結構來內嵌資料，則只能進行加法變更。 有關架構版本設定的詳細資訊，請參閱架構組合的[基本介紹](../schema/composition.md)。

您現在可以按照[的教學課程，在UI](./relationship-ui.md)中定義架構關係，將新的關係欄位新增至「忠誠會員」架構。

也可使用[!DNL Schema Registry] API來檢視和管理「忠誠會員」結構。 若要開始使用API，請先閱讀[[!DNL Schema Registry API] 開發人員指南](../api/getting-started.md)。

### 視訊資源

>[!WARNING]
>
>下列影片中顯示的[!DNL Platform] UI已過期。 請參閱上述檔案，了解最新的UI螢幕擷取畫面和功能。

以下影片說明如何在[!DNL Platform] UI中建立簡單結構。

>[!VIDEO](https://video.tv.adobe.com/v/27012?quality=12&learn=on)

以下影片旨在加強您對使用欄位群組和類別的了解。

>[!VIDEO](https://video.tv.adobe.com/v/27013?quality=12&learn=on)

## 附錄

以下各節提供了有關[!DNL Schema Editor]使用的附加資訊。

### 建立新類{#create-new-class}

[!DNL Experience Platform] 提供根據貴組織專屬的類別定義結構的彈性。若要了解如何建立新類，請參閱UI](../ui/resources/classes.md#create)中[建立和編輯類的指南。

### 更改架構{#change-class}的類

您可以在儲存架構之前的初始合成程式期間的任何時間點變更架構的類別。

>[!WARNING]
>
>為架構重新指派類別時應格外小心。 欄位組僅與某些類相容，因此更改類將重置畫布和您添加的任何欄位。

若要了解如何變更結構的類別，請參閱UI](../ui/resources/schemas.md)中[管理結構的指南。
