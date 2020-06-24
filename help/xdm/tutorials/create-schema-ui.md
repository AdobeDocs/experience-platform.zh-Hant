---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 使用結構編輯器建立架構
topic: tutorials
translation-type: tm+mt
source-git-commit: b3fa5a17c3a5c2406d368d165da63f2f8c01154d
workflow-type: tm+mt
source-wordcount: '3409'
ht-degree: 0%

---


# 使用結構編輯器建立架構

架構註冊表提供使用者介面和REST風格的API，您可從中檢視和管理Adobe Experience Platform架構庫中的所有資源。 方案庫包含由Adobe、Experience Platform合作夥伴和您所使用之應用程式的廠商提供給您的資源，以及您定義並儲存至方案註冊表的資源。

本教學課程涵蓋使用Experience Platform中的架構編輯器建立架構的步驟。 如果您希望使用方案註冊表API合成方案，請先閱讀 [Schema Registry Developer Guide](../api/getting-started.md) ，再嘗試使用API [建立方案](create-schema-api.md)。

本教學課程也包含定 [義新類別的步驟](#create-new-class) ，然後您可使用此類別來編寫架構。

## 快速入門

本教學課程需要對使用架構編輯器時涉及的Adobe Experience Platform各個方面有深入的瞭解。 在開始本教學課程之前，請先閱讀說明檔案，瞭解下列概念：

* [體驗資料模型(XDM)](../home.md): 平台組織客戶體驗資料的標準化架構。
* [架構構成基礎](../schema/composition.md): 概述XDM結構描述及其構建塊，包括類、混合、資料類型和欄位。
* [即時客戶個人檔案](../../profile/home.md): 根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。

本教學課程要求您必須擁有Experience Platform的存取權。 如果您無法存取Experience Platform中的IMS組織，請在繼續前先與系統管理員聯絡。

## 瀏覽「方案」工作區中的現有方案 {#browse}

「體驗平台」中的「結構描述」工作區提供結構描述庫的視覺化效果，可讓您檢視和管理所有可用的結構描述，以及構成新的結構描述。 工作區還包括「架構編輯器」，您將在本教程中構建架構的畫布。

登入Experience Platform後，按一下左側導 **覽中的** 「結構描述」，您就會被帶到「結構描述」工作區。 您將看到一個方案清單（方案庫的表示法），您可以在其中查看、管理和自定義所有可用的方案。 該清單包括方案所基於的名稱、類型、類和行為（記錄或時間序列），以及上次修改方案的日期和時間。

按一下搜尋列旁的篩選圖示，以針對註冊表中的所有資源（包括類別、混合和資料類型）使用篩選功能。

![查看方案庫](../images/tutorials/create-schema/schemas_filter.png)

## 建立架構並命名架構 {#create}

要開始合成方案，請單 **擊「方案** 」工作區右上角的「建立方案」。

![「建立結構」按鈕](../images/tutorials/create-schema/create_schema_button.png)

此時 *將顯示架構編* 輯器。 這是您將在其中構成架構的畫布。 當您到達編輯器時，畫布的「結構」區段中會自動建立「未命名的架構」，供您開始自訂。 **

![架構編輯器](../images/tutorials/create-schema/schema_editor.png)

在編輯器的右側是「方案屬 *性* 」，您可在其中提供方案的名稱(使用「顯 **** 示名稱」欄位)。 輸入名稱后，畫布會更新以反映架構的新名稱。

![架構畫布](../images/tutorials/create-schema/name_schema.png)

在決定架構的名稱時，需要考慮幾個重要事項：

* 架構名稱應簡短且具說明性，以便稍後在程式庫中輕鬆找到架構。
* 架構名稱必須是唯一的，這表示它也應足夠具體，以免日後重複使用。 例如，如果您的組織針對不同品牌有不同的忠誠度方案，最好將方案命名為「品牌A忠誠度成員」，以便輕鬆區分您稍後可能定義的其他忠誠度相關方案。
* 或者，您可以使用「說明」欄位提供有關方案的其 **他資訊** 。

本教程將構建一個方案，以便提取與忠誠度方案成員相關的資料，因此該方案命名為「忠誠度成員」。

## 指派類別 {#class}

編輯器的左側是「合成」 *部分* 。 它目前包含兩個子區域： *架構* 和 *類*。

既然架構具有名稱，現在就應該指派將實施的類。 按一 **下** 「類別」旁 *的「指派」*。

![](../images/tutorials/create-schema/assign_class_button.png)

此時將 *顯示「指定類* 」對話框。 此窗口顯示所有可用類的清單，包括您的組織定義的任何類（所有者是「客戶」）以及Adobe定義的標準類。

按一下類名以顯示類的說明。 您也可以選擇「預 **覽類別結構」** ，以查看與類別相關聯的欄位和中繼資料。

本教程使用XDM Individual Profile類。 按一下類別旁的選項按鈕以選取它，然後按一下「指 **派類別」**。

![「分配類」對話框](../images/tutorials/create-schema/assign_class.png)

畫布會重新出現。 「類 *」部分現在包含您選擇的類(XDM Individual Profile)，而「XDM Individual Profile」類貢獻的欄位現在可在「結構」部分*** 中顯示。

![已分配XDM單個配置檔案類](../images/tutorials/create-schema/class_assigned_structure.png)

欄位以「fieldName」格式顯示 |資料類型」。 本教學課程稍後提供在UI中定義架構欄位的步驟。

>[!NOTE] 在保 [存架構之前，您可以在初始合成過程中的任意點更改架構類](#change-class) ，但應該非常小心。 Mixins僅與特定類別相容，因此變更類別會重設畫布和您新增的任何欄位。

## 新增混音 {#mixin}

現在已指派類別，「構 *成* 」區段包含第三個子區段： *米辛*。

您現在可以新增mix，開始將欄位新增至您的架構。 混音是描述特定概念的一或多個欄位的組。 本教學課程使用mixin來描述忠誠度計畫的成員，並擷取關鍵資訊，例如姓名、生日、電話號碼、地址等。

若要新增混音，請按 **一下***Mixins子區* 段中的「新增」。

![](../images/tutorials/create-schema/add_mixin_button.png)

此時將 *顯示「添加混音* 」對話框。 Mixin僅用於特定類，因此，mixin清單僅顯示與所選類（在本例中為XDM Individual Profile類）相容的類。

選擇混合旁的單選按鈕將提供「預覽混合結構」( **Preview Mixin Structure**)選項。 選擇「個人資料人員詳細資料」混合，然後按一下「新 **增混合」**。

![](../images/tutorials/create-schema/add_mixin_person_details.png)

結構畫布會重新出現。 Mixins *區段現在會列出* &quot;Profile Person Details&quot;混音，而 *Structure* 區段則包含混音所貢獻的欄位。

![](../images/tutorials/create-schema/person_details_structure.png)

此混音在頂層名稱&quot;person&quot;下提供數個欄位，資料類型為&quot;Person&quot;。 此欄位群組說明個人的相關資訊，包括姓名、出生日期和性別。

>[!NOTE] 請記住，欄位可能使用標量類型（如字串、整數、陣列或日期）作為其資料類型，以及模式註冊表中的任何「資料類型」（表示通用概念的一組欄位）。

請注意，「名稱」欄位的資料類型為「人員姓名」，這表示該欄位也說明一般概念，並包含與名稱相關的子欄位，例如名字、姓氏和全名。

按一下畫布中的不同欄位，以檢視它們對架構結構所貢獻的其他欄位。

## 新增另一個混音 {#mixin-2}

您現在可以重複相同的步驟來新增另一個混音。 當您這次檢視「 *Add Mixin* 」對話方塊時，請注意「Profile Person Details」混音已變灰，且旁邊的選項按鈕無法選取。 這可防止意外複製您已包含在目前架構中的混音。

您現在可以從「新增Mixin」對話方塊新增「個人資 *料詳細資訊* 」混合。

![](../images/tutorials/create-schema/add_mixin_personal_details.png)

新增後，畫布會重新顯示。 「個人資料」現在會列在「構圖」區段的 *Mixins* 下，而「結構」下則會新增家庭位址、行動電話等 *欄位***。

與「名稱」欄位類似，您剛新增的欄位代表多欄位概念。 例如，「homeAddress」的資料類型為「Address」，而「mobilePhone」的資料類型為「Phone Number」。 您可以按一下這些欄位以展開，並查看資料類型中包含的其他欄位。

![](../images/tutorials/create-schema/personal_details_structure.png)

## 定義新混音 {#define-mixin}

「忠誠會員」結構是用來擷取與忠誠度方案成員相關的資料，因此需要某些特定的忠誠度相關欄位。 沒有可用的標準混音包含必要的欄位，因此您需要定義新的混音。

此時，當您開啟「新增 *Mixin」對話方塊* ，請選 **取「建立新Mixin」**。 接著會要求您提供混 **音的顯示名****稱和說** 明。

![](../images/tutorials/create-schema/mixin_create_new.png)

和類名一樣，混音名應簡短，說明混音對架構的貢獻。 這些名稱也是唯一的，因此您將無法重複使用名稱，因此必須確保它足夠具體。

在本教學課程中，請將新混音命名為「忠誠度詳細資訊」。

按一 **下「新增Mixin** 」以返回架構編輯器。 「忠誠度詳細資料」現在應會顯示在畫布左側的 *Mixins* 下，但是尚未有與其關聯的欄位，因此「結構」下不會出現新的欄位 **。

## 新增欄位至混音 {#mixin-fields}

現在您已建立「忠誠度詳細資料」混音，是時候定義混音將對結構貢獻的欄位了。

若要開始，請按一下「混音」區段中的 *混音* 。 執行此操作後， *Mixin Properties* ( **Mixin屬性)將顯示在編輯器的右側，而「結構」(Structure)下的架構名稱旁邊將顯示「添加欄位** 」(Add Field *)按鈕*。

![](../images/tutorials/create-schema/loyalty_details_structure.png)

按一 **下** 「忠誠會員」旁的「新增欄位」，在結構中建立新節點。 此節點（在此範例中稱為&quot;_tenantId&quot;）代表您IMS組織的租用戶ID，前面加上底線。 租用戶ID的存在表示您新增的欄位包含在您組織的命名空間中。

換言之，您新增的欄位對您的組織而言是獨一無二的，而且將儲存在「方案註冊表」中，位於您IMS組織僅能存取的特定區域。 您定義的欄位必須一律新增至您的命名空間，以避免與其他標準類別、混合、資料類型和欄位的名稱產生衝突。

該命名空間節點內部有一個「新欄位」。 這是「忠誠度詳細資訊」混搭的開始。

![](../images/tutorials/create-schema/new_field_loyalty.png)

使用 *編輯器右側的「欄位屬性* 」，首先建立「忠誠度」欄位，其類型為「物件」，用來保存您的忠誠度相關欄位。 完成後，按一下「 **套用**」。

![](../images/tutorials/create-schema/loyalty_object.png)

系統會套用變更，並顯示新建立的「忠誠度」物件。 按一 **下物件旁的「新增欄位** 」，新增其他與忠誠度相關的欄位。 此時會顯示「新欄位」，畫 *布右側會顯示「欄位屬性* 」區段。

![](../images/tutorials/create-schema/new_field_in_loyalty_object.png)

每個欄位都需要下列資訊：

* **欄位名稱：** 欄位的名稱，用駝峰寫的。 範例： loyaltyLevel
* **顯示名稱：** 欄位名稱，以標題大寫寫。 範例： 忠誠度等級
* **類型：** 欄位的資料類型。 這包括基本標量類型和模式註冊表中定義的任何資料類型。 範例： 字串、整數、布林值、人員、地址、電話號碼等。
* **說明：** 該欄位的可選說明應包括在句子中。 （最多200個字元）

「忠誠度」物件的第一個欄位將是名為「loyaltyId」的字串。 將新欄位的類型設定為&quot;String&quot;時，「 *Field Properties* 」（欄位屬性）窗口會填入幾個用於應用約束的選項，包括 **Default Value**、 **Format**&#x200B;和 **** Maximum Length Enghtings。

![](../images/tutorials/create-schema/string_constraints.png)

根據所選資料類型，可使用不同的約束選項。 由於「loyaltyId」將是電子郵件地址，因此從「格式」下拉式選單中選 **取「** email」。 選擇 **應用** ，以應用更改。

![](../images/tutorials/create-schema/loyaltyId_field.png)

## 新增更多欄位以混合 {#mixin-fields-2}

現在您已新增「loyaltyId」欄位，您可以新增其他欄位來擷取與忠誠度相關的資訊，例如：

* 點（整數）
* 成員自（日期）

每個欄位都是透過按一 **下忠誠度物件上的「新增欄位** 」並填入所需資訊來新增。

完成時，「忠誠度」物件將包含下列欄位： 忠誠度ID、點數和會員。

![](../images/tutorials/create-schema/loyalty_object_fields.png)

## 新增&#39;enum&#39;欄位至mixin {#enum}

在方案編輯器中定義欄位時，有一些附加選項可以應用於基本欄位類型，以便對欄位可包含的資料提供進一步的約束。

例如，「忠誠度等級」欄位，其值只能是四種可能選項之一。 若要將此欄位新增至結構，請按一 **下「忠誠度」物件旁的「新增欄位** 」，並填入欄位屬性下的必 *要欄位*。

對於 **類型**，選擇「字串」，您會看到Array **、** Enum **和****** Identity的其他複選框。

選擇 **Enum** 複選框以開啟 *下面的Enum Values* 部分。 您可以在此輸入每個可 **接受的忠誠度等級的Value** （camelCase中）和 **Label** （Title Case中的可選Reader友好名稱）。

當您完成所有欄位屬性後，按一 **下「套用** 」,「loyaltyLevel」欄位就會新增至「loyalty」物件。

![](../images/tutorials/create-schema/loyalty_level_enum.png)

有關可用附加約束的詳細資訊：

* **必要：** 指出資料擷取需要此欄位。 任何根據此架構上傳至資料集且不包含此欄位的資料，在擷取時都會失敗。
* **陣列：** 指出欄位包含一組值，每個值都指定了資料類型。 例如，選取「字串」的資料類型並勾選「陣列」核取方塊表示欄位將包含字串陣列。
* **列舉：** 指出此欄位必須包含可能值列舉清單中的其中一個值。
* **身份：** 指出此欄位是身分欄位。 有關身分欄位的詳細資訊，請 [參閱本教學課程](#identity-field)。

## 將多欄位物件轉換為資料類型 {#datatype}

新增數個忠誠度特定欄位後，「忠誠度」物件現在包含可在其他結構中有用的通用資料結構。

當您覺得多欄位結構可以重複使用，而且想要在其他地方使用相同的資料結構時，架構編輯器可將該結構轉換為資料類型。

資料類型允許一致地使用多欄位結構，並提供比混音更大的靈活性，因為它們可以在架構中的任意位置使用。 這是通過將混合中 **的欄位類型** 設定為註冊表中定義的任何資料類型來完成的。

若要將「忠誠度」物件轉換為資料類型，請按一下「結構」下的「忠誠度」欄位，然後選取「欄位屬性」下編輯器右側的「轉換為新資料類型 ********」。 出現一個小的綠色彈出式選單，確認「對象已轉換為資料類型」。

現在，當您查看「結構 **」下方時，您會看到「忠誠度」欄位的資料類型為「忠誠度」，欄位旁邊有小型鎖定圖示，表示它們不再是個別欄位，而是多欄位結構的一部分。

在未來的方案中，您現在可以指派「 **Type** of Loyalty」（忠誠度）欄位，並自動包含「Loyalty Level」（忠誠度等級）、「Points」（點數）、「Member Since」（成員開始）和「Loyalty ID」（忠誠度ID）欄位)。

![](../images/tutorials/create-schema/loyalty_data_type.png)

## 將架構欄位設定為身份欄位 {#identity-field}

結構描述用於將資料擷取至Experience Platform，而資料最終用於識別個人，並將來自多個來源的資訊結合在一起。 為協助處理此程式，關鍵欄位可標示為「身分」欄位。

Experience Platform可讓您透過使用架構編輯器中的「身分」核取方塊，輕鬆地 **標示身分欄位** 。

例如，忠誠度方案中可能有數千個成員屬於相同的「等級」，但忠誠度方案的每個成員都有唯一的「loyantyId」（在此例中為個別成員的電子郵件地址）。 「loyaltyId」是每個成員的唯一識別碼，這讓它成為身分欄位的最佳候選者，而「level」則否。

在編輯器 *的* 「結構」區段中，按一下您建立的「loyaltyId」欄位，您會看到「欄位屬性」下方的「身分 **」核取方** 塊出現 **。 選中該框，您將可以選擇將其設定為主 **身份**。 也勾選該方塊。

接下來，您必須提供身 **分名稱空間**。 有數個預先定義的名稱空間，但由於&quot;loyaltyId&quot;是成員的電子郵件地址，所以請從下拉式清單中選取&quot;Email&quot;。 您現在可以按一 **下「套用** 」，確認「loyaltyId」欄位的更新。

現在，所有包含在「loyaltyId」欄位中的資料都將用來協助識別該個人，並將該客戶的單一檢視結合在一起。

![](../images/tutorials/create-schema/loyaltyId_primary_identity.png)

>[!NOTE] 一旦將架構欄位設定為主標識，如果您稍後嘗試將架構中的另一個欄位設定為主標識，將會收到錯誤消息。 每個架構只能包含一個主標識欄位。

若要進一步瞭解如何使用身分識別，請參閱 [Identity Service](../../identity-service/home.md) 檔案。

<!-- ## Relationship

Schemas define a static view of a concept, but do not provide specific details on how data based on these schemas (datasets, etc) may relate to one another. Adobe Experience Platform allows you to describe these relationships through the **Relationship** checkbox in the schema editor. 

In order to define a relationship, click on the field and check the **Relationship** checkbox on the right-side of the canvas. 

![](../images/tutorials/create-schema/relationship.png)

More information about relationships and other schema metadata can be found in the [Schema Registry API Developer Guide](../schema_registry_developer_guide.md). -->

## 啟用結構以用於即時客戶配置檔案 {#profile}

結構編輯器提供啟用結構以便與即時客戶描述 [檔一起使用的功能](../../profile/home.md)。 設定檔可全面瞭解每位客戶，建立健全的360°客戶屬性設定檔，以及客戶在與Experience Platform整合的任何系統上進行的每次互動的時間戳記帳戶。

要使結構能夠與即時客戶配置檔案一起使用，它必須定義主要標識。 如果您嘗試啟用方案而未先定義主要識別，則會收到「缺少主要識別」錯誤訊息。

![](../images/tutorials/create-schema/missing_primary_identity.png)

若要啟用「忠誠成員」結構以用於描述檔，請先按一下編輯器「結構」區段中的「忠誠 *成員* 」。

在編輯器的右側，在「方案屬性」 *下方*，會顯示有關方案的資訊，包括其顯示名稱、說明和類型。 除了此資訊外，還有一個名為「描述檔」的切換 **按鈕**。

![](../images/tutorials/create-schema/unified_profile_toggle.png)

按一 **下「描述檔** 」，隨即出現快顯視窗，要求您確認您要啟用描述檔的架構。

![](../images/tutorials/create-schema/enable_unified_profile.png)

>[!NOTE] 一旦對即時客戶描述檔啟用並儲存結構後，便無法停用它。

## 後續步驟

現在您已完成「忠誠成員」架構的構成，您可以在編輯器的「結構」區 *段中* ，看到完整架構。 按一下 **保存** ，架構將保存到架構庫，使架構註冊表可以訪問該架構庫。

您的新架構現在可用來將資料內嵌至平台。 請記住，一旦使用架構來收錄資料，則只能進行加性變更。 有關方案 [版本化的詳細資訊](../schema/composition.md) ，請參閱方案構成的基本資訊。

「Loyalty Members」結構也可供使用「結構註冊表API」來檢視和管理。 若要開始使用API，請先閱讀 [Schema Registry API開發人員指南](../api/getting-started.md)。

## 附錄

以下資訊是方案編輯器教程的補充資訊。

### Create a new class {#create-new-class}

Experience Platform提供根據組織專屬類別定義架構的彈性。

在方案編 *輯器的「類* 」部分中按一下「分配 **」，開啟「分配類**** 」對話框。 在對話框中，選擇「創 **建新類」**。

然後，您可以為新類提供 **Display Name** （類的簡短、描述性、唯一且用戶友好的名稱）、 **Description**，以及 **Behavior** （「Record」或「Time Series」），作為方案將定義的資料。

![新類詳細資訊](../images/tutorials/create-schema/create_new_class.png)

>[!NOTE] 當建立實作組織定義之類的架構時，請記住混合僅可用於相容類。 由於您定義的類是新的，因此「添加混音」對話框中沒有列 *出相容混音* 。 您需要選取「建立新 **Mixin」** ，並定義混音以用於該類別。 下次構建實施新類的模式時，將列出您定義的混合併可供使用。

### 更改方案的類 {#change-class}

在初始模式合成過程中，在保存模式之前，您可以隨時更改模式所基於的類。

>[!WARNING] 在更改課程之前，請務必小心。 Mixins僅與特定類別相容，因此變更類別會重設畫布，並移除您已新增至該點的任何欄位。

要更改類，請按一下編 **輯器** 「合成 *」部分中* 「類」旁邊的「指定 ** 」。

當「指 *定類* 」對話框開啟時，可以從可用清單中選擇新類。 按一 **下「指派類別** 」，隨即開啟新對話方塊，要求您確認您要指派新類別。

![變更類別](../images/tutorials/create-schema/assign_new_class_warning.png)

如果您確認類別變更，畫布將會重設，而所有構圖進度都將遺失。