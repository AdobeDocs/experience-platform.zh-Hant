---
keywords: Experience Platform；首頁；熱門主題；UI;UI;XDM;XDM系統；體驗資料模型；體驗資料模型；資料模型；結構編輯器；結構編輯器；結構；結構；結構；結構；結構；建立
solution: Experience Platform
title: 使用結構編輯器建立結構
topic-legacy: tutorial
type: Tutorial
description: 本教學課程涵蓋以 Experience 平台結構編輯器建立結構的相關步驟。
exl-id: 3edeb879-3ce4-4adb-a0bd-8d7ad2ec6102
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '3754'
ht-degree: 0%

---

# 使用 [!DNL Schema Editor]

Adobe Experience Platform使用者介面可讓您建立和管理 [!DNL Experience Data Model] (XDM)互動式視覺畫布中的結構，稱為 [!DNL Schema Editor]. 本教學課程涵蓋如何使用 [!DNL Schema Editor].

>[!NOTE]
>
>為了示範，本教學課程中的步驟涉及建立描述客戶忠誠度計畫成員的範例結構。 雖然您可以使用這些步驟來建立不同的架構以供自己使用，但建議您先依照建立範例架構的操作，以了解 [!DNL Schema Editor].

如果您偏好使用 [!DNL Schema Registry] 請改為從閱讀 [[!DNL Schema Registry] 開發人員指南](../api/getting-started.md) 在嘗試上的教學課程之前 [使用API建立結構](create-schema-api.md).

## 快速入門

本教學課程需要妥善了解Adobe Experience Platform在架構建立中涉及的各個層面。 開始本教學課程之前，請先檢閱本檔案中的下列概念：

* [[!DNL Experience Data Model (XDM)]](../home.md):標準化框架 [!DNL Platform] 組織客戶體驗資料。
   * [結構構成基本概念](../schema/composition.md):概述XDM結構及其建置區塊，包括類別、結構欄位群組、資料類型和個別欄位。
* [[!DNL Real-Time Customer Profile]](../../profile/home.md):根據來自多個來源的匯總資料，提供統一的即時消費者設定檔。

## 開啟 [!UICONTROL 結構] 工作區 {#browse}

此 [!UICONTROL 結構] 工作區中 [!DNL Platform] UI提供 [!DNL Schema Library]，可讓您檢視管理組織可用的結構。 工作區也包含 [!DNL Schema Editor]，您可在本教學課程中撰寫架構的畫布。

登入後 [!DNL Experience Platform]，選取 **[!UICONTROL 結構]** 在左側導覽中，開啟 **[!UICONTROL 結構]** 工作區。 此 **[!UICONTROL 瀏覽]** 索引標籤會顯示結構清單(表示 [!DNL Schema Library])，您可以檢視和自訂。 該清單包括架構所基於的名稱、類型、類和行為（記錄或時間序列），以及上次修改架構的日期和時間。

請參閱 [在UI中探索現有的XDM資源](../ui/explore.md) 以取得更多資訊。

## 建立架構並命名 {#create}

要開始合成架構，請選擇 **[!UICONTROL 建立結構]** 在 **[!UICONTROL 結構]** 工作區。 畫面會顯示下拉式功能表，供您選擇核心類別 [!UICONTROL XDM個別設定檔] 和 [!UICONTROL XDM ExperienceEvent]. 如果這些類不符合您的目的，您也可以選擇 **[!UICONTROL 瀏覽]** 從其他可用類中選擇 [建立新類](#create-new-class).

在本教學課程中，請選取 **[!UICONTROL XDM個別設定檔]**.

![](../images/tutorials/create-schema/create_schema_button.png)

由於您選擇標準XDM類別來建立結構，因此 **[!UICONTROL 新增欄位群組]** 對話框，允許您立即開始向架構添加欄位。 目前，請選取 **[!UICONTROL 取消]** ，退出對話框。

![](../images/tutorials/create-schema/cancel-field-group.png)

此 [!DNL Schema Editor] 框。 這是您要在其中組成架構的畫布。 系統會自動在 **[!UICONTROL 結構]** 編輯器時顯示畫布的區段，以及根據該類別包含在所有結構中的標準欄位。 架構的指派類也列在 **[!UICONTROL 類別]** in **[!UICONTROL 組合物]** 區段。

![](../images/tutorials/create-schema/schema_editor.png)

>[!NOTE]
>
>您可以 [更改架構的類](#change-class) 在架構儲存之前的初始合成程式期間的任何時間點，都應格外小心。 欄位組僅與某些類相容，因此更改類將重置畫布和您添加的任何欄位。

使用編輯器右側的欄位來提供結構的顯示名稱和可選說明。 輸入名稱后，畫布會更新，以反映架構的新名稱。

![](../images/tutorials/create-schema/name_schema.png)

決定結構名稱時，需考量幾項重要事項：

* 架構名稱應簡短且具描述性，以便日後輕鬆找到架構。
* 架構名稱必須是唯一的，這表示其特定性也應足夠，以免日後重複使用。 例如，如果貴組織針對不同品牌有不同的忠誠計畫，最好將您的結構命名為「品牌忠誠會員」，以便輕鬆區分與其他與忠誠度相關的結構，您稍後可能會定義。
* 您也可以使用結構描述來提供與結構相關的任何其他內容資訊。

本教學課程會組成結構來內嵌與忠誠計畫成員相關的資料，因此結構命名為「忠誠會員」。

## 新增欄位群組 {#field-group}

您現在可以透過新增欄位群組，開始將欄位新增至您的架構。 欄位群組是一或多個欄位的群組，通常搭配使用以描述特定概念。 本教學課程使用欄位群組來說明忠誠計畫的成員，並擷取關鍵資訊，例如名稱、生日、電話號碼、地址等。

若要新增欄位群組，請選取 **[!UICONTROL 新增]** 在 **[!UICONTROL 欄位群組]** 小節。

![](../images/tutorials/create-schema/add-field-group-button.png)

隨即出現新對話方塊，顯示可用欄位群組的清單。 每個欄位組僅用於特定類，因此對話框僅列出與所選類相容的欄位組(在本例中，為 [!DNL XDM Individual Profile] 類別)。 如果您使用標準XDM類別，欄位群組清單將會根據使用頻率聰明地排序。

![](../images/tutorials/create-schema/field-group-popularity.png)

從清單中選取欄位群組，會使其顯示在右側邊欄中。 您可以視需要選取多個欄位群組，在確認前將每個欄位新增至右側邊欄的清單。 此外，當前所選欄位組的右側將顯示一個表徵圖，允許您預覽它提供的欄位的結構。

![](../images/tutorials/create-schema/preview-field-group-button.png)

預覽欄位群組時，右側邊欄會提供欄位群組架構的詳細說明。 您也可以瀏覽所提供畫布中欄位群組的欄位。 當您選取不同欄位時，右側邊欄會更新，顯示有關欄位的詳細資訊。 選擇 **[!UICONTROL 返回]** 完成預覽以返回到欄位組選擇對話框時。

![](../images/tutorials/create-schema/preview-field-group.png)

在本教學課程中，請選取 **[!UICONTROL 人口統計詳細資料]** 欄位群組，然後選取 **[!UICONTROL 新增欄位群組]**.

![](../images/tutorials/create-schema/demographic-details.png)

架構畫布會重新顯示。 此 **[!UICONTROL 欄位群組]** 部分現在列出「[!UICONTROL 人口統計詳細資料]」和 **[!UICONTROL 結構]** 小節包括欄位組貢獻的欄位。 您可以在 **[!UICONTROL 欄位群組]** 區段來反白顯示其在畫布內提供的特定欄位。

![](../images/tutorials/create-schema/demographic-details-structure.png)

此欄位群組會在頂層名稱下貢獻多個欄位 `person` 資料類型為「[!UICONTROL 人員]」。 此欄位群組說明個人的相關資訊，包括姓名、出生日期和性別。

>[!NOTE]
>
>請記住，欄位可能使用標量類型（如字串、整數、陣列或日期），以及在 [!DNL Schema Registry].

請注意， `name` 欄位的資料類型為「[!UICONTROL 人員名稱]「，這表示它也描述了一個通用概念，並包含與名稱相關的子欄位，如名字、姓氏、字首和尾碼。

選取畫布中的不同欄位，以顯示它們對架構結構貢獻的任何其他欄位。

## 新增其他欄位群組 {#field-group-2}

您現在可以重複相同步驟來新增其他欄位群組。 當您檢視 **[!UICONTROL 新增欄位群組]** 對話方塊，請注意「[!UICONTROL 人口統計詳細資料]「 」欄位組已呈現灰色狀態，無法選中該欄位組旁邊的複選框。 這可防止您意外重複目前架構中已包含的欄位群組。

在本教學課程中，請選取「[!DNL Personal Contact Details]「 」欄位組，然後選擇 **[!UICONTROL 新增欄位群組]** 將其新增至結構。

![](../images/tutorials/create-schema/personal-contact-details.png)

新增後，畫布會重新顯示。 &quot;[!UICONTROL 個人聯繫人詳細資訊]「 」現在列於 **[!UICONTROL 欄位群組]** 在 **[!UICONTROL 組合物]** 區段，以及首頁位址、行動電話等欄位，已新增至 **[!UICONTROL 結構]**.

類似於 `name` 欄位中，您剛新增的欄位代表多欄位概念。 例如， `homeAddress` 資料類型為「[!UICONTROL 郵遞區號]&quot;和 `mobilePhone` 資料類型為「[!UICONTROL 電話號碼]」。 您可以選取這些欄位，以展開它們，並查看資料類型中包含的其他欄位。

![](../images/tutorials/create-schema/personal-contact-details-structure.png)

## 定義自訂欄位群組 {#define-field-group}

「[!UICONTROL 忠誠會員]「結構」是用來擷取與忠誠計畫成員相關的資料，因此需要一些特定的忠誠相關欄位。

有標準 [!UICONTROL 忠誠度詳細資料] 欄位群組，您可將其新增至結構以擷取與忠誠計畫相關的常見欄位。 雖然強烈建議您使用標準欄位群組來呈現結構擷取的概念，但標準忠誠度欄位群組的結構可能無法擷取特定忠誠計畫的所有相關資料。 在此案例中，您可以選擇定義新的自訂欄位群組，以擷取這些欄位。

開啟 **[!UICONTROL 添加欄位組]** 再次對話，但這次請選取 **[!UICONTROL 建立新欄位組]** 靠近頂端。 系統會要求您提供欄位群組的顯示名稱和說明。

![](../images/tutorials/create-schema/create-new-field-group.png)

與類名一樣，欄位組名應簡短，說明欄位組將對架構作何貢獻。 這些名稱也是唯一的，因此您將無法重複使用名稱，因此必須確保名稱足夠具體。

在本教學課程中，將新欄位群組命名為「忠誠度詳細資料」。

選擇 **[!UICONTROL 新增欄位群組]** 返回 [!DNL Schema Editor]. &quot;[!UICONTROL 忠誠度詳細資料]「 」現在應顯示在 **[!UICONTROL 欄位群組]** 在畫布的左側，但沒有與其關聯的欄位，因此在下方不會顯示新欄位 **[!UICONTROL 結構]**.

## 新增欄位至欄位群組 {#field-group-fields}

現在您已建立「忠誠度詳細資料」欄位群組，可以定義欄位群組將貢獻至結構的欄位。

若要開始，請在 **[!UICONTROL 欄位群組]** 區段。 執行此操作後，欄位群組的屬性會顯示在編輯器的右側，而 **加號(+)** 表徵圖將出現在 **[!UICONTROL 結構]**.

![](../images/tutorials/create-schema/loyalty_details_structure.png)

選取 **加號(+)** 表徵圖[!DNL Loyalty Members]&quot;在結構中建立新節點。 此節點(稱為 `_tenantId` 在此範例中)代表您的IMS組織的租用戶ID，前面加上底線。 租用戶ID的存在表示您新增的欄位包含在組織的命名空間中。

換言之，您新增的欄位對您的組織來說是唯一的，且會儲存在 [!DNL Schema Registry] 特定區域（僅限貴組織存取）。 您定義的欄位必須一律新增至租用戶命名空間，以避免與其他標準類別、欄位群組、資料類型和欄位的名稱衝突。

在命名節點內，[!UICONTROL 新欄位]」。 這是「[!UICONTROL 忠誠度詳細資料]&quot;欄位組。

![](../images/tutorials/create-schema/new_field_loyalty.png)

使用編輯器右側的控制項，首先建立 `loyalty` 類型為&quot;的欄位[!UICONTROL 物件]「 」，此欄位將用於保留您的忠誠度相關欄位。 完成後，請選取 **[!UICONTROL 套用]**.

![](../images/tutorials/create-schema/loyalty_object.png)

會套用變更，並新建立 `loyalty` 對象。 選取 **加號(+)** 圖示以新增其他與忠誠度相關的欄位。 A &quot;[!UICONTROL 新欄位]」， **[!UICONTROL 欄位屬性]** 區段會顯示在畫布的右側。

![](../images/tutorials/create-schema/new_field_in_loyalty_object.png)

每個欄位都需要下列資訊：

* **[!UICONTROL 欄位名稱]:** 欄位的名稱，用駝峰寫。 範例：loalytyLevel
* **[!UICONTROL 顯示名稱]:** 以標題寫入的欄位名稱。 範例：忠誠度等級
* **[!UICONTROL 類型]:** 欄位的資料類型。 這包括基本標量類型和 [!DNL Schema Registry]. 範例： [!UICONTROL 字串], [!UICONTROL 整數], [!UICONTROL 布林值], [!UICONTROL 人員], [!UICONTROL 地址], [!UICONTROL 電話號碼]、等
* **[!UICONTROL 說明]:** 應包含欄位的選用說明，以句子寫入，最多200個字元。

的第一個欄位 `Loyalty` 物件將是名為的字串 `loyaltyId`. 將新欄位的類型設定為「[!UICONTROL 字串]」、 **[!UICONTROL 欄位屬性]** 區段會填入多個套用限制的選項，包括預設值、格式和最大長度。

![](../images/tutorials/create-schema/string_constraints.png)

根據所選資料類型，可使用不同的約束選項。 自 `loyaltyId` 將是電子郵件地址，請選擇「[!UICONTROL 電子郵件]」 **[!UICONTROL 格式]** 下拉式功能表。 選擇 **[!UICONTROL 套用]** 來套用變更。

![](../images/tutorials/create-schema/loyaltyId_field.png)

## 新增更多欄位至欄位群組 {#field-group-fields-2}

現在您已新增 `loyaltyId` 欄位，您可以新增其他欄位來擷取忠誠度相關資訊，例如：

* 點（整數）
* 會員自（日期）

若要將每個欄位新增至架構，請選取 **加號(+)** 表徵圖 `loyalty` 物件，並填入所需資訊。

完成後，「忠誠度」物件將包含忠誠度ID、點數和成員加入後的欄位。

![](../images/tutorials/create-schema/loyalty_object_fields.png)

## 將列舉欄位新增至欄位群組 {#enum}

定義 [!DNL Schema Editor]，您可以套用至基本欄位類型的一些其他選項，以對欄位可包含的資料提供進一步限制。 下表說明了這些限制的使用案例：

| 限制 | 說明 |
| --- | --- |
| [!UICONTROL 必填] | 指出資料擷取需要此欄位。 任何根據此結構上傳至資料集但不含此欄位的資料，在擷取時都會失敗。 |
| [!UICONTROL 陣列] | 指出欄位包含值的陣列，每個值都指定了資料類型。 例如，對資料類型為「」的欄位使用此限制[!UICONTROL 字串]&quot;指定欄位將包含字串的陣列。 |
| [!UICONTROL 列舉] | 指示此欄位必須包含可能值枚舉清單中的值之一。 |
| [!UICONTROL 身分] | 指出此欄位是身分欄位。 提供有關身分欄位的更多資訊 [本教學課程的稍後部分](#identity-field). |
| [!UICONTROL 關係] | 而架構關係則可透過使用聯合架構和 [!DNL Real-Time Customer Profile]，此欄位僅適用於共用相同類別的結構。 此 [!UICONTROL 關係] 約束指明此欄位引用基於不同類的架構的主標識，這表示兩個架構之間的關係。 請參閱 [定義關係](./relationship-ui.md) 以取得更多資訊。 |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>任何必要、身分或關係欄位都會顯示在左側邊欄中，讓您無論結構的複雜性為何，都能輕鬆找到這些欄位。
>
>![](../images/tutorials/create-schema/left-rail-special.png)

在本教學課程中， [!DNL "loyalty"] 結構中的物件需要新的列舉欄位，該欄位描述客戶的「忠誠度」，其值只能是四個可能選項的其中一個。 若要將此欄位新增至架構，請選取 **加號(+)** 表徵圖 `loyalty` 物件，並填寫 **[!UICONTROL 欄位名稱]** 和 **[!UICONTROL 顯示名稱]**. 針對 **[!UICONTROL 類型]**，請選取「[!UICONTROL 字串]」。

![](../images/tutorials/create-schema/loyalty-level-type.png)

選取欄位類型後，欄位會出現其他核取方塊，包括的核取方塊 **[!UICONTROL 陣列]**, **[!UICONTROL 列舉]**，和 **[!UICONTROL 身分]**.

選取 **[!UICONTROL 列舉]** 開啟核取方塊 **[!UICONTROL 列舉值]** 一節。 您可以在此輸入 **[!UICONTROL 值]** （在camelCase中）和 **[!UICONTROL 標籤]** （標題案例中為選用、方便閱讀的名稱），以取得每個可接受的忠誠度等級。

完成所有欄位屬性後，請選擇 **[!UICONTROL 套用]** 若要新增「[!DNL loyaltyLevel]」欄位 `loyalty` 物件。

![](../images/tutorials/create-schema/loyalty_level_enum.png)

## 將多欄位物件轉換為資料類型 {#datatype}

此 `loyalty` 物件現在包含數個忠誠度專屬欄位，並代表可用於其他結構的通用資料結構。 此 [!DNL Schema Editor] 可讓您將這些物件的結構轉換為資料類型，輕鬆套用可重複使用的多欄位物件。

資料類型允許一致地使用多欄位結構，並提供比欄位組更大的靈活性，因為它們可以在架構內的任何位置使用。 若要這麼做，請設定欄位的 **[!UICONTROL 類型]** 的值轉換為 [!DNL Schema Registry].

若要轉換 `loyalty` 對象，請選擇 `loyalty` 欄位 **[!UICONTROL 結構]**，然後選取 **[!UICONTROL 轉換為新資料類型]** 編輯的右側 **[!UICONTROL 欄位屬性]**. 畫面會顯示綠色彈出視窗，確認物件已成功轉換。

![](../images/tutorials/create-schema/convert-data-type.png)

現在，當你看下面 **[!UICONTROL 結構]**，您可以看到 `loyalty` 欄位的資料類型為「[!DNL Loyalty]「欄位旁邊有小的鎖定表徵圖，表明它們不再是單個欄位，而是多欄位資料類型的一部分。

![](../images/tutorials/create-schema/loyalty_data_type.png)

在未來的架構中，您現在可以將欄位指派為「[!DNL Loyalty]「類型」，會自動包含ID、忠誠度、成員開始時間和點數的欄位。

>[!NOTE]
>
>您也可以建立和編輯自訂資料類型，而不需編輯結構。 請參閱 [建立和編輯資料類型](../ui/resources/data-types.md) 以取得更多資訊。

## 搜尋及篩選結構欄位

除了基礎類提供的欄位之外，您的架構現在還包含多個欄位群組。 使用較大的結構時，您可以在左側邊欄中選取欄位群組名稱旁的核取方塊，將顯示的欄位篩選為僅限您感興趣的欄位群組所提供的欄位。

![](../images/tutorials/create-schema/filter-by-field-group.png)

如果您在結構中尋找特定欄位，也可以使用搜尋列來依名稱篩選顯示的欄位，無論欄位底下提供的欄位群組為何。

![](../images/tutorials/create-schema/search.png)

>[!IMPORTANT]
>
>顯示相符欄位時，搜尋函式會考慮任何選取的欄位群組篩選器。 如果搜索查詢未顯示您期望的結果，則可能需要再次檢查您是否未篩選出任何相關欄位組。

## 將架構欄位設為身分欄位 {#identity-field}

結構提供的標準資料結構可運用於跨多個來源識別屬於相同個人的資料，以支援不同的下游使用案例，例如細分、報告、資料科學分析等。 若要根據個別身分匯整資料，索引鍵欄位必須標示為 [!UICONTROL 身分] 欄位。

[!DNL Experience Platform] 可透過 **[!UICONTROL 身分]** 核取方塊 [!DNL Schema Editor]. 不過，您必鬚根據資料的性質，決定要將哪個欄位當作身分的最佳候選欄位。

例如，可能有數千個忠誠計畫成員屬於相同的「忠誠度」，但忠誠計畫的每個成員都有獨特的 `loyaltyId` （在本例中是個別成員的電子郵件地址）。 事實上 `loyaltyId` 是每個成員的唯一標識符，因此它是標識欄位的理想候選符，但 `loyaltyLevel` 不是。

>[!IMPORTANT]
>
>以下概述的步驟說明如何將身份描述符添加到現有架構欄位。 除了在結構本身的結構內定義身分欄位外，您也可以使用 `identityMap` 欄位來改用包含身分資訊。
>
>如果您打算使用 `identityMap`，請記住，它會覆寫您直接新增至結構的任何主要身分。 請參閱 `identityMap` 在 [綱要構成指南](../schema/composition.md#identityMap) 以取得更多資訊。

在 **[!UICONTROL 結構]** 在編輯器的區段中，選取 `loyaltyId` 欄位和 **[!UICONTROL 身分]** 「 」下顯示的複選框 **[!UICONTROL 欄位屬性]**. 核取方塊和選項，將此項目設為 **[!UICONTROL 主要身分]** 框。 也選擇此框。

>[!NOTE]
>
>每個架構只能包含一個主要身分欄位。 將架構欄位設定為主要身分後，如果您稍後嘗試將架構中的另一個身分欄位設定為主要身分，將會收到錯誤訊息。

接下來，您必須提供 **[!UICONTROL 身分命名空間]** 從下拉式清單中預先定義的命名空間清單。 自 `loyaltyId` 是客戶的電子郵件地址，請選擇「[!UICONTROL 電子郵件]」。 選擇 **[!UICONTROL 套用]** 確認 `loyaltyId` 欄位。

![](../images/tutorials/create-schema/loyaltyId_primary_identity.png)

>[!NOTE]
>
>如需標準命名空間及其定義的清單，請參閱 [[!DNL Identity Service] 檔案](../../identity-service/troubleshooting-guide.md#standard-namespaces).

套用變更後， `loyaltyId` 顯示指紋符號，表示它現在是標識欄位。

![](../images/tutorials/create-schema/identity-applied.png)

現在所有擷取至 `loyaltyId` 欄位將用來協助識別該個人，並匯整該客戶的單一檢視。 若要進一步了解如何使用身分，請前往 [!DNL Experience Platform]，請檢閱 [[!DNL Identity Service]](../../identity-service/home.md) 檔案。

## 啟用架構以用於 [!DNL Real-Time Customer Profile] {#profile}

[[!DNL Real-Time Customer Profile]](../../profile/home.md) 在 [!DNL Experience Platform] 提供每個客戶的整體檢視。 此服務可建立強大的360°客戶屬性設定檔，以及客戶在與 [!DNL Experience Platform].

為了讓結構能與 [!DNL Real-Time Customer Profile]，則必須定義主要身分。 如果您未先定義主標識而嘗試啟用架構，則會收到錯誤消息。

<img src="../images/tutorials/create-schema/missing_primary_identity.png" width="600" /><br>

啟用「忠誠會員」結構以用於 [!DNL Profile]，請選取「[!DNL Loyalty Members]」 **[!UICONTROL 結構]** 的子母體。

在編輯器的右側，會顯示結構的相關資訊，包括其顯示名稱、說明和類型。 除了此資訊外， **[!UICONTROL 設定檔]** 切換按鈕。

![](../images/tutorials/create-schema/profile-toggle.png)

選擇 **[!UICONTROL 設定檔]** 畫面隨即顯示彈出視窗，要求您確認要為 [!DNL Profile].

<img src="../images/tutorials/create-schema/enable-profile.png" width="700" /><br>

>[!WARNING]
>
>架構啟用後 [!DNL Real-Time Customer Profile] 和儲存時，無法加以停用。

選擇 **[!UICONTROL 啟用]** 確認您的選擇。 您可以選取 **[!UICONTROL 設定檔]** 再次切換為禁用模式（如果需要），但一旦模式在保存時 [!DNL Profile] 已啟用，則無法再停用。

## 後續步驟和其他資源

現在您完成架構撰寫後，就可以在畫布中看到完整的架構。 選擇 **[!UICONTROL 儲存]** 架構會儲存至 [!DNL Schema Library]，讓使用者方便存取 [!DNL Schema Registry].

您的新結構現在可用來將資料內嵌至 [!DNL Platform]. 請記住，一旦使用結構來內嵌資料，則只能進行加法變更。 請參閱 [綱要構成基本知識](../schema/composition.md) 以了解架構版本設定的詳細資訊。

您現在可以依照 [在UI中定義架構關係](./relationship-ui.md) 新增關係欄位至「忠誠會員」結構。

您也可以使用 [!DNL Schema Registry] API。 若要開始使用API，請先閱讀 [[!DNL Schema Registry API] 開發人員指南](../api/getting-started.md).

### 視訊資源

>[!WARNING]
>
>此 [!DNL Platform] 下列影片中顯示的UI已過期。 請參閱上述檔案，了解最新的UI螢幕擷取畫面和功能。

以下影片說明如何在 [!DNL Platform] UI。

>[!VIDEO](https://video.tv.adobe.com/v/27012?quality=12&learn=on)

以下影片旨在加強您對使用欄位群組和類別的了解。

>[!VIDEO](https://video.tv.adobe.com/v/27013?quality=12&learn=on)

## 附錄

以下各節提供有關使用 [!DNL Schema Editor].

### 建立新類 {#create-new-class}

[!DNL Experience Platform] 提供根據貴組織專屬的類別定義結構的彈性。 若要了解如何建立新類別，請參閱 [在UI中建立和編輯類](../ui/resources/classes.md#create).

### 更改架構的類 {#change-class}

您可以在儲存架構之前的初始合成程式期間的任何時間點變更架構的類別。

>[!WARNING]
>
>為架構重新指派類別時應格外小心。 欄位組僅與某些類相容，因此更改類將重置畫布和您添加的任何欄位。

若要了解如何變更結構的類別，請參閱 [在UI中管理結構](../ui/resources/schemas.md).
