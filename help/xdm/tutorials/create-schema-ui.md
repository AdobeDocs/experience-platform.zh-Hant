---
keywords: Experience Platform;home;popular topics;ui;UI;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema editor;Schema Editor;schema;Schema;schemas;Schemas;create
solution: Experience Platform
title: 使用結構編輯器建立架構
topic: tutorials
description: 本教學課程涵蓋使用Experience Platform中的架構編輯器建立架構的步驟。
translation-type: tm+mt
source-git-commit: ed1f2fdac0f9c977d11c867327c084353c1bcd0f
workflow-type: tm+mt
source-wordcount: '3528'
ht-degree: 0%

---


# 使用 [!DNL Schema Editor]

Adobe Experience Platform使用者介面可讓您在稱為的互動式 [!DNL Experience Data Model] 視覺畫布中建立和管理(XDM)結構 [!DNL Schema Editor]。 本教學課程介紹如何使用建立模式 [!DNL Schema Editor]。

>[!NOTE]
>
>為了進行示範，本教學課程中的步驟包括建立描述客戶忠誠度方案成員的範例架構。 雖然您可以使用這些步驟來建立不同的架構，但建議您先遵循建立範例架構的步驟，以瞭解其功能 [!DNL Schema Editor]。

如果您偏好使用 [!DNL Schema Registry] API來編寫架構，請先閱讀開發人員指南 [[!DNL Schema Registry] ，再嘗試使用API](../api/getting-started.md) 建立架構的教學課程 [](create-schema-api.md)。

## 快速入門

本教學課程需要對架構建立中涉及的Adobe Experience Platform各個方面有深入的瞭解。 在開始本教學課程之前，請先閱讀說明檔案，瞭解下列概念：

* [[!DNL體驗資料模型(XDM)]](../home.md):組織客戶體驗資料 [!DNL Platform] 的標準化架構。
   * [架構構成基礎](../schema/composition.md):概述XDM結構描述及其構建塊，包括類、混合、資料類型和欄位。
* [[!DNL即時客戶基本資料]](../../profile/home.md):根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。

## 瀏覽結構工作區中的現 [!UICONTROL 有結構] {#browse}

UI中 [!UICONTROL 的] 「結構描述」工作區 [!DNL Platform] 提供了結構的可視化效果 [!DNL Schema Library]，允許您查看管理組織可用的結構描述。 工作區也包含畫 [!DNL Schema Editor]布，您可在此教學課程中，在畫布上編寫架構。

登入後， [!DNL Experience Platform]在左側導 **[!UICONTROL 覽中選取「方]** 案」 **** 。 「瀏 **[!UICONTROL 覽]** 」頁籤顯示可查看和自定義的方案清單( [!DNL Schema Library]表示方案)。 該清單包括方案所基於的名稱、類型、類和行為（記錄或時間序列），以及上次修改方案的日期和時間。

選取搜尋列旁的篩選圖示，以針對註冊表中的所有資源（包括類別、混合和資料類型）使用篩選功能。 您也可以根據資源是否歸Adobe或您的組織所有，以及是否已啟用供使用，來進行篩選 [!DNL Real-time Customer Profile]。

![](../images/tutorials/create-schema/schemas_filter.png)

## 建立架構並命名架構 {#create}

要開始合成方案，請選 **[!UICONTROL 擇]** 「方案」工作區右上角的「創 **[!UICONTROL 建方案]** 」。 此時會出現下拉式選單，提供您選擇核心類別 [!UICONTROL XDM Individual Profile] 和 [!UICONTROL XDM ExperienceEvent]，或瀏覽其他可用類別的選項。 在本教學課程中，請選擇「 **[!UICONTROL XDM個別描述檔」]**。

![](../images/tutorials/create-schema/create_schema_button.png)

將出 [!DNL Schema Editor] 現。 這是您將在其中構成架構的畫布。 到達編輯器後，系統會自動在畫布的 **[!UICONTROL Structure]** （結構）區段中建立未命名的架構，並根據 [!UICONTROL XDM Individual Profile] （XDM單個配置檔案）類別在所有架構中包含的標準欄位。 方案的已分配類列在「合成」部 **[!UICONTROL 分的]** 「類 **[!UICONTROL 」下]** 。

![](../images/tutorials/create-schema/schema_editor.png)

>[!NOTE]
>
>在保 [存架構之前，您可以在初始合成過程中的任意點更改架構類](#change-class) ，但應該非常小心。 Mixins僅與特定類別相容，因此變更類別會重設畫布和您新增的任何欄位。

使用編輯器右側的欄位，提供架構的顯示名稱和選用說明。 輸入名稱后，畫布會更新以反映架構的新名稱。

![](../images/tutorials/create-schema/name_schema.png)

在決定架構的名稱時，需要考慮幾個重要事項：

* 架構名稱應簡短且具說明性，以便稍後可輕鬆找到架構。
* 架構名稱必須是唯一的，這表示它也應足夠具體，以免日後重複使用。 例如，如果您的組織針對不同品牌有不同的忠誠度方案，最好將方案命名為「品牌A忠誠度成員」，以便輕鬆區分您稍後可能定義的其他忠誠度相關方案。
* 您也可以使用結構描述來提供與結構描述相關的任何其他上下文資訊。

本教程將構建一個方案，以便接收與忠誠度方案成員相關的資料，因此，該方案名為「忠誠度成員」。

## 新增混音 {#mixin}

您現在可以新增mix，開始將欄位新增至您的架構。 混音是一組一個或多個欄位，通常一起用於描述特定概念。 本教學課程使用mixin來描述忠誠度計畫的成員，並擷取關鍵資訊，例如姓名、生日、電話號碼、地址等。

若要新增混音，請在 **[!UICONTROL Mixins子區段中]** ，選 **[!UICONTROL 取]** 「新增」。

![](../images/tutorials/create-schema/add_mixin_button.png)

隨即出現新對話方塊，顯示可用混音清單。 每個混音都僅用於特定類，因此對話框僅列出與您選擇的類（在本例中為類）相容的混 [!DNL XDM Individual Profile] 音。

從清單中選取混音，會使混音出現在右側邊欄中。 此外，在選取混音的右側會出現圖示，可讓您預覽其提供欄位的結構。 選擇「 **[!UICONTROL Profile Person Details]** 」混合，然後選擇「 **[!UICONTROL Add Mixin」]**。

![](../images/tutorials/create-schema/add_mixin_person_details.png)

結構畫布會重新出現。 Mixins **[!UICONTROL 區段現在會列]** 出「Profile Person Details[!UICONTROL 」（設定檔人員詳細資訊），而]Structure **** 區段則包含mixin貢獻的欄位。 您可以在「 **[!UICONTROL Mixins]** 」區段下選取mixin的名稱，以反白顯示它在畫布中提供的特定欄位。

![](../images/tutorials/create-schema/person_details_structure.png)

此混音在頂層名稱&quot;[!UICONTROL person]&quot;與資料類型&quot;[!UICONTROL Person]&quot;下提供數個欄位。 此欄位群組說明個人的相關資訊，包括姓名、出生日期和性別。

>[!NOTE]
>
>請記住，欄位可能使用在中定義的標量類型（例如字串、整數、陣列或日期），以及任何資料類型（表示共同概念的欄位群組） [!DNL Schema Registry]。

請注意，「[!UICONTROL name]」欄位的資料類型為「[!UICONTROL Full name]」，這表示它也說明一個通用概念，並包含與名稱相關的子欄位，例如名字、姓氏、字首和字尾。

在畫布中選取不同的欄位，以檢視它們對架構結構所貢獻的其他欄位。

## 新增另一個混音 {#mixin-2}

您現在可以重複相同的步驟來新增另一個混音。 當您這次檢視「 **[!UICONTROL Add Mixin]** 」(新增Mixin[!UICONTROL )對話方塊時，請注意，「]Profile Person Details」（個人資料）混音已變灰，且旁邊的選項按鈕無法選取。 這可防止意外複製您已包含在目前架構中的混音。

您現在可以從對話方塊[!DNL Profile Personal Details" mixin] 中新增「」。

![](../images/tutorials/create-schema/add_mixin_personal_details.png)

新增後，畫布會重新顯示。 「[!UICONTROL Profile Personal Details]」現在會列在「Composition **[!UICONTROL 」（合成）區段的「]** Mixins **[!UICONTROL 」（設定檔個人詳細資訊）下，而「]****** StructureSchure」（結構）下則新增了首頁位址、行動電話等欄位。

與「名稱」欄位類似，您剛新增的欄位代表多欄位概念。 例如，&quot;[!UICONTROL homeAddress]&quot;的資料類型為&quot;[!UICONTROL Address]&quot;,&quot;[!UICONTROL MobilePhone]&quot;的資料類型為&quot;Phone NumberAddress&quot;。 您可以選取每個欄位以展開這些欄位，並查看資料類型中包含的其他欄位。

![](../images/tutorials/create-schema/personal_details_structure.png)

## 定義新混音 {#define-mixin}

「忠誠[!UICONTROL 會員]」架構旨在擷取與忠誠度方案成員相關的資料，因此需要某些特定的忠誠度相關欄位。 沒有可用的標準混音包含必要的欄位，因此您需要定義新的混音。

此時，當您開啟「新增 *[!UICONTROL Mixin」對話方塊]* ，請選 **[!UICONTROL 取「建立新Mixin」]**。 接著會要求您提供混 **[!UICONTROL 音的顯示名]****[!UICONTROL 稱和說]** 明。

![](../images/tutorials/create-schema/mixin_create_new.png)

和類名一樣，混音名應簡短，說明混音對架構的貢獻。 這些名稱也是唯一的，因此您將無法重複使用名稱，因此必須確保它足夠具體。

在本教學課程中，請將新混音命名為「[!UICONTROL 忠誠度詳細資]」。

選 **[!UICONTROL 取「新增Mixin]** 」以返回 [!DNL Schema Editor]。 「[!UICONTROL Loyalty Details]」（忠誠度詳細資訊）現在應會顯示在畫布左側的 **[!UICONTROL Mixins下方，但是目前尚無相關欄位，因此「結構」下方不會顯示新]** 欄位 ****。

## 新增欄位至混音 {#mixin-fields}

現在您已建立「[!UICONTROL Loyalty Details]」混音，是時候定義混音將對結構貢獻的欄位了。

首先，在「混音」區段中選取混音 **[!UICONTROL 名稱]** 。 執行此操作後，mixin的屬性會顯示在編輯器的右側，而「結構」( **[!UICONTROL Structure]** )下的架構名稱旁會出現「添加欄位 **[!UICONTROL 」按鈕]**。

![](../images/tutorials/create-schema/loyalty_details_structure.png)

選 **[!UICONTROL 擇「]** 」旁的「添加欄位[!DNL Loyalty Members]」，在結構中建立新節點。 此節點（在此範例中稱為&quot;_tenantId&quot;）代表您IMS組織的租用戶ID，前面加上底線。 租用戶ID的存在表示您新增的欄位包含在您組織的命名空間中。

換言之，您新增的欄位對您的組織而言是獨一無二的，而且會儲存在您 [!DNL Schema Registry] 組織只能存取的特定區域。 您定義的欄位必須一律新增至您的租用戶名稱空間，以避免與其他標準類別、混合、資料類型和欄位的名稱產生衝突。

該命名空間節點內部有一個「[!UICONTROL 新欄位]」。 這是「忠誠度詳細資[!UICONTROL 訊]」混合的開始。

![](../images/tutorials/create-schema/new_field_loyalty.png)

使用編輯器右側的控制項，首先建立「[!DNL loyalty]」欄位，其類型為「[!UICONTROL Object]」，用於保留您的忠誠度相關欄位。 完成後，選擇「應 **[!UICONTROL 用」]**。

![](../images/tutorials/create-schema/loyalty_object.png)

會套用變更，並顯示新建立的「[!DNL loyalty]」物件。 選 **[!UICONTROL 取物件旁的「新增欄位]** 」，以新增其他與忠誠度相關的欄位。 「新[!UICONTROL 欄位]」出現，畫布右側 **[!UICONTROL 會顯示「欄位屬性]** 」區段。

![](../images/tutorials/create-schema/new_field_in_loyalty_object.png)

每個欄位都需要下列資訊：

* **[!UICONTROL 欄位名稱]:** 欄位的名稱，用駝峰寫的。 範例：loyaltyLevel
* **[!UICONTROL 顯示名稱]:** 欄位名稱，以標題大寫寫。 範例：忠誠度等級
* **[!UICONTROL 類型]:** 欄位的資料類型。 這包括基本標量類型和中定義的任何資料類型 [!DNL Schema Registry]。 範例： [!UICONTROL 字串]、整數、 [!UICONTROL Person][!UICONTROL 、Address]Address [!UICONTROL 、Phone Number、Boolean]等。
* **[!UICONTROL 說明]:** 該欄位的可選說明應包括在句子中，最多200個字元。

物件的第一個欄 [!DNL Loyalty] 位是名為&quot;[!DNL loyaltyId]&quot;的字串。 將新欄位的類型設定為「[!UICONTROL String]」時，「 **[!UICONTROL Field Properties]** 」部分會填入幾個用於應用約束的選項，包括 **[!UICONTROL Default Value]**、 ******** Format Germat Length和Jognamiz Length。

![](../images/tutorials/create-schema/string_constraints.png)

根據所選資料類型，可使用不同的約束選項。 由於「[!DNL loyaltyId]」將是電子郵件地址，所以從「格式」下拉式選單[!UICONTROL 中選取「]email **** 」。 選擇 **[!UICONTROL 應用]** ，以應用更改。

![](../images/tutorials/create-schema/loyaltyId_field.png)

## 新增更多欄位至混音 {#mixin-fields-2}

現在您已新增「[!DNL loyaltyId]」欄位，您可以新增其他欄位來擷取與忠誠度相關的資訊，例如：

* 點（整數）
* 會員登記（日期）

每個欄位都會新增，方 **[!UICONTROL 法是在忠誠度物件上選取「新增欄位]** 」並填入必要的資訊。

完成後，「忠誠度」物件將包含忠誠度ID、點數和成員間隔的欄位。

![](../images/tutorials/create-schema/loyalty_object_fields.png)

## 新增列舉欄位至混音 {#enum}

在中定義欄位時 [!DNL Schema Editor]，有一些附加選項可以應用於基本欄位類型，以便對欄位可以包含的資料提供進一步的約束。 下表說明了這些約束的使用案例：

| 約束 | 說明 |
| --- | --- |
| [!UICONTROL 必填] | 指出資料擷取需要此欄位。 任何根據此架構上傳至資料集且不包含此欄位的資料，在擷取時都會失敗。 |
| [!UICONTROL 陣列] | 指出欄位包含一組值，每個值都指定了資料類型。 例如，在資料類型為&quot;[!UICONTROL String]&quot;的欄位上使用此限制會指定欄位將包含字串陣列。 |
| [!UICONTROL Enum] | 指出此欄位必須包含可能值列舉清單中的其中一個值。 |
| [!UICONTROL 身份] | 指出此欄位是身分欄位。 有關身分欄位的詳細資訊，請 [參閱本教學課程](#identity-field)。 |
| [!UICONTROL 關係] | 雖然方案關係可以通過使用union方案和來推斷 [!DNL Real-time Customer Profile]，但這僅適用於共用相同類的方案。 關係 [!UICONTROL 約束表示] ，此欄位引用基於不同類的方案的主標識，這表示兩個方案之間的關係。 如需詳細資訊，請 [參閱定義關係](./relationship-ui.md) 的教學課程。 |

在本教學課程中， [!DNL "loyalty"] 架構中的物件需要新的列舉欄位，以說明客戶的「忠誠度等級」，其中值只能是四個可能選項之一。 要將此欄位添加到方案中，請選擇「 **[!UICONTROL 」對象旁邊的「添加欄位]** 」 ，並填寫欄位名和顯[!DNL loyalty]示名稱的必 **[!UICONTROL 要欄位]******。 對於 **[!UICONTROL 類型]**，選擇「[!UICONTROL 字串]」。

![](../images/tutorials/create-schema/loyalty-level-type.png)

選取欄位類型後，會顯示其他核取方塊，包括 **[!UICONTROL Array]**、 **[!UICONTROL Enum]**&#x200B;和 **[!UICONTROL Identity的核取方塊]**。

選擇 **[!UICONTROL Enum]** 複選框以開啟 **[!UICONTROL Enum值部分]** 。 您可以在此輸入每個可 **[!UICONTROL 接受的忠誠度等級的Value]** （camelCase中）和 **[!UICONTROL Label]** （Title Case中的可選Reader友好名稱）。

完成所有欄位屬性後，選擇 **[!UICONTROL 應用]** ，將「[!DNL loyaltyLevel]」欄位添加到「[!DNL loyalty]」對象。

![](../images/tutorials/create-schema/loyalty_level_enum.png)

## 將多欄位物件轉換為資料類型 {#datatype}

「[!DNL loyalty]」物件現在包含數個忠誠度特定欄位，並代表通用資料結構，可用於其他結構。 可 [!DNL Schema Editor] 讓您將這些物件的結構轉換為資料類型，以輕鬆套用可重複使用的多欄位物件。

資料類型允許一致地使用多欄位結構，並提供比混音更大的靈活性，因為它們可以在架構中的任意位置使用。 若要這麼做，請將欄位的「類 **[!UICONTROL 型]** 」值設為中定義之任何資料類型的值 [!DNL Schema Registry]。

要將「[!DNL loyalty]」對象轉換為資料類型，請在「結構」下選擇「[!DNL loyalty]」欄位 **[!UICONTROL ，然後在「欄位屬性」下選擇編輯器右側的「轉換為新資料類型」]**********。 出現綠色快顯，確認物件已成功轉換。

![](../images/tutorials/create-schema/convert-data-type.png)

現在，當您查看「結構」下方時，您會看到「 **[!UICONTROL 」欄位的資料類型為「]**[!DNL loyalty][!DNL Loyalty]」，欄位旁邊有小型鎖定圖示，表示它們不再是個別欄位，而是多欄位資料類型的一部分。

![](../images/tutorials/create-schema/loyalty_data_type.png)

在未來的架構中，您現在可以指派 **[!UICONTROL Type]** &quot;[!DNL Loyalty]&quot;欄位，並自動包含ID、忠誠度等級、成員自由和點數的欄位。

## 將架構欄位設定為身份欄位 {#identity-field}

架構所提供的標準資料結構可用於跨多個來源識別屬於同一個人的資料，允許各種下游使用案例，例如分段、報告、資料科學分析等。 為了根據個別身分來接合資料，索引鍵欄位必須標示為適用結構中的「[!UICONTROL Identity]」欄位。

[!DNL Experience Platform] 使您可以透過使用中的「身分」核取方塊，輕鬆地 **[!UICONTROL 標示身分]** 欄位 [!DNL Schema Editor]。 不過，您必鬚根據資料的性質，判斷哪個欄位最適合做為身分識別。

例如，可能有數千個忠誠度方案會員屬於相同的「忠誠度等級」，但忠誠度方案的每個會員都有唯一的「[!DNL loyaltyId]」（在此例中為個別會員的電子郵件地址）。 「[!DNL loyaltyId]」是每個成員的唯一識別碼，這讓它成為身分識別欄位的最佳候選者，而「忠誠度」則否。

>[!IMPORTANT]
>
>下面介紹的步驟介紹如何將身份描述符添加到現有模式欄位。 除了在架構本身的結構中定義身份欄位外，您還可以使用一個欄位來 `identityMap` 改為包含身份資訊。
>
>如果您打算使 `identityMap`用，請記住，它將覆蓋您直接添加到架構的任何主要標識。 有關詳細資訊， `identityMap` 請參 [閱架構構成指南的](../schema/composition.md#identityMap) 「基礎」部分。

在編輯器 **[!UICONTROL 的]** 「結構」區段中，選擇「[!DNL loyaltyId]」欄位，並在「欄位屬性」下顯示 **[!UICONTROL 「身份]** 」複選 **[!UICONTROL 框]**。 選中該框並顯示將其設定為「主身份」 **[!UICONTROL 的選項]** 。 也選擇此框。

接著，您必須從下拉式清 **[!UICONTROL 單中預先定義的名稱空間清單中提供「識別名稱空間]** 」。 由於「[!DNL loyaltyId]」是客戶的電子郵件地址，因此請從下拉式清單中選[!UICONTROL 取「電子郵件]」。 選擇 **[!UICONTROL 應用]** ，確認對「[!DNL loyaltyId]」欄位的更新。

![](../images/tutorials/create-schema/loyaltyId_primary_identity.png)

>[!NOTE]
>
>如需標準名稱空間及其定義的清單，請參閱 [Identity Service檔案](../../identity-service/troubleshooting-guide.md#standard-namespaces)。

現在，所有包含在「[!DNL loyaltyId]」欄位中的資料都將用來協助識別該個人，並將該客戶的單一視圖拼湊在一起。

>[!NOTE]
>
>一旦將架構欄位設定為主標識，如果您稍後嘗試將架構中的另一個欄位設定為主標識，將會收到錯誤消息。 每個架構只能包含一個主標識欄位。

若要進一步瞭解在中使用身 [!DNL Experience Platform]份，請檢閱 [[!DNL Identity Service]檔案](../../identity-service/home.md) 。

## 啟用模式以用於 [!DNL Real-time Customer Profile] {#profile}

[[!DNL即時客戶個人檔案]](../../profile/home.md) 利用身分資料， [!DNL Experience Platform] 提供每位客戶的全貌。 此服務可建立強穩、360°的客戶屬性描述檔，以及客戶在與之整合的任何系統上，所有互動的時間戳記帳戶 [!DNL Experience Platform]。

要啟用與一起使用的模式， [!DNL Real-time Customer Profile]它必須定義主標識。 如果您嘗試啟用方案而未先定義主要身分，則會收到錯誤訊息。

<img src="../images/tutorials/create-schema/missing_primary_identity.png" width="600" /><br>

要啟用「忠誠成員」結構以用於 [!DNL Profile]，請首先在編輯器的「結[!DNL Loyalty Members]構 **[!UICONTROL 」部分中選擇「]** 」。

在編輯器的右側，會顯示有關架構的資訊，包括其顯示名稱、說明和類型。 除了此資訊外，還有「描述檔 **[!UICONTROL 切換]** 」按鈕。

![](../images/tutorials/create-schema/profile-toggle.png)

選擇 **[!UICONTROL 描述檔]** ，然後出現一個快顯視窗，要求您確認您要為其啟用架構 [!DNL Profile]。

![](../images/tutorials/create-schema/enable-profile.png)

>[!WARNING]
>
>在模式啟用並保存後， [!DNL Real-time Customer Profile] 便無法禁用它。

選取「 **[!UICONTROL 啟用]** 」以確認您的選擇。 如果您願意，可以再次選擇 **[!UICONTROL Profile]** toggle以禁用該架構，但一旦在啟用時保存了該 [!DNL Profile] 架構，就不能再禁用它。

## 後續步驟和其他資源

現在您已完成「忠誠成員」結構的構建，您就可以在畫布中看到完整的結構。 選擇 **[!UICONTROL 保存]** ，並將模式保存到中 [!DNL Schema Library]，使模式可由訪問 [!DNL Schema Registry]。

您的新架構現在可用來將資料內嵌至 [!DNL Platform]。 請記住，一旦使用架構來收錄資料，則只能進行加性變更。 有關方案 [版本化的詳細資訊](../schema/composition.md) ，請參閱方案構成的基本資訊。

您現在可以遵循在UI中定 [義結構關係的教學課程](./relationship-ui.md) ，在「忠誠度成員」結構中新增關係欄位。

「忠誠度成員」結構也可供使用 [!DNL Schema Registry] API檢視和管理。 若要開始使用API，請先閱讀開發人員 [[!DNL Schema Registry API] 指南](../api/getting-started.md)。

### 視訊資源

>[!WARNING]
>
>以 [!DNL Platform] 下影片中顯示的UI已過時。 請參閱上述檔案以取得最新的UI螢幕擷取和功能。

以下視訊說明如何在UI中建立簡單的 [!DNL Platform] 架構。

>[!VIDEO](https://video.tv.adobe.com/v/27012?quality=12&learn=on)

以下影片旨在強化您對使用混合與類別的瞭解。

>[!VIDEO](https://video.tv.adobe.com/v/27013?quality=12&learn=on)

## 附錄

以下各節提供有關使用的附加資訊 [!DNL Schema Editor]。

### Create a new class {#create-new-class}

[!DNL Experience Platform] 提供了根據組織唯一的類定義方案的靈活性。

在「方 **[!UICONTROL 案]** 」工作區中，選 **[!UICONTROL 擇「建立方案]**」，然後從下拉式 **[!UICONTROL 清單中選擇「瀏覽]** 」。

![](../images/tutorials/create-schema/browse-classes.png)

此時將出現一個對話框，允許您從可用類清單中進行選擇。 在對話框頂部，選擇「創 **[!UICONTROL 建新類」]**。 然後，您可以為新類指定 **[!UICONTROL Display Name]** （類的簡短、描述性、唯一且用戶友好的名稱）、 **[!UICONTROL Description]**、和 **[!UICONTROL Behavior]** (「TimeSeries Record」或「Oracle Series」)，用於方案將定義的資料。

![](../images/tutorials/create-schema/create_new_class.png)

>[!IMPORTANT]
>
>當建立實作組織定義之類的架構時，請記住混合僅可用於相容類。 由於您定義的類是新的，因此「添加混音」對話框中沒有列 *出相容混音* 。 您需要選取「建立新 **[!UICONTROL Mixin」]** ，並定義混音以用於該類別。 下次構建實施新類的模式時，將列出您定義的混合併可供使用。

### 更改方案的類 {#change-class}

可以在保存模式之前，在初始合成過程中的任意點更改模式的類。

>[!WARNING]
>
>重新指派架構的類別時應格外小心。 Mixins僅與特定類別相容，因此變更類別會重設畫布和您新增的任何欄位。

若要重新指派類別，請 **[!UICONTROL 在畫布的左側]** ，選取「指派」。

![](../images/tutorials/create-schema/assign_class_button.png)

此時會出現一個對話框，其中顯示所有可用類的清單，包括您的組織定義的任何類(所有者是「[!UICONTROL Customer]」)以及Adobe定義的標準類。

從清單中選擇一個類，在對話框的右側顯示其說明。 您也可以選取「預 **[!UICONTROL 覽類別結構]** 」，以查看與類別相關聯的欄位和中繼資料。 選擇 **[!UICONTROL 分配類]** ，繼續。

![](../images/tutorials/create-schema/assign_class.png)

隨即開啟新對話方塊，要求您確認您要指派新類別。 選擇 **[!UICONTROL 指派]** ，以確認。

![](../images/tutorials/create-schema/assign-confirm.png)

在確認類別變更後，畫布將重設，而所有的構圖進度都將遺失。