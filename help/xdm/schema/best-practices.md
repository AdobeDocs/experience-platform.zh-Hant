---
keywords: Experience Platform；首頁；熱門主題；結構；結構；列舉；主要身分；主要身分；XDM個人設定檔；體驗事件；XDM體驗事件；XDM ExperienceEvent；experienceevent；XDM Experienceevent；結構描述設計；最佳實務
solution: Experience Platform
title: 資料模型化的最佳實務
description: 本檔案介紹Experience Data Model (XDM)結構描述，以及構成要在Adobe Experience Platform中使用的結構描述的建置組塊、原則和最佳實務。
exl-id: 2455a04e-d589-49b2-a3cb-abb5c0b4e42f
source-git-commit: 7521273c0ea4383b7141e9d7a82953257ff18c34
workflow-type: tm+mt
source-wordcount: '3236'
ht-degree: 1%

---

# 資料建模的最佳做法

[!DNL Experience Data Model] (XDM)是核心架構，藉由提供用於下游Adobe Experience Platform服務的通用結構和定義，可標準化客戶體驗資料。 只要遵守XDM標準，所有客戶體驗資料都可整合至共同呈現方式，並用來從客戶動作中獲得有價值的深入分析、定義客戶對象，以及針對個人化目的表達客戶屬性。

由於XDM極為通用而且可依設計方式自訂，因此在設計結構描述時，請務必遵循資料模型化的最佳實務。 本檔案說明將客戶體驗資料對應至XDM時，必須做出的重要決定和考量事項。

## 快速入門

閱讀本指南之前，請檢閱[XDM系統總覽](../home.md)，以瞭解XDM及其在Experience Platform中的角色的高層級簡介。

由於本指南僅著重於有關結構描述設計的主要考量，因此強烈建議您閱讀結構描述組合的[基本知識](./composition.md)，以取得本指南中提及的個別結構描述元素的詳細解釋。

## 最佳實務摘要 {#summary}

設計資料模型以用於Experience Platform的建議方法可概述如下：

1. 瞭解您資料的業務使用案例。
1. 確定應帶入Experience Platform的主要資料來源，以解決這些使用案例。
1. 識別可能也會感興趣的任何次要資料來源。 例如，如果貴組織中目前只有一個業務單位有興趣將其資料移轉到Experience Platform，則類似的業務單位將來可能也會有興趣移轉類似的資料。 考慮這些次要來源，有助於將整個組織的資料模型標準化。
1. 為已識別的資料來源建立高階實體關係圖(ERD)。
1. 將高階的ERD轉換為以Experience Platform為中心的ERD （包括設定檔、體驗事件和查詢實體）。

與識別執行業務使用案例所需的適用資料來源相關的步驟因組織而異。 雖然本檔案的其餘章節專注於在識別資料來源後組織和建立ERD的後幾個步驟，但圖表各種元件的說明可能會告知您決定要將哪些資料來源移轉至Experience Platform。

## 建立高階ERD {#create-an-erd}

在您決定好要帶入Experience Platform的資料來源後，請建立高層級ERD以協助引導將資料對應至XDM結構的程式。

以下範例代表想要將資料帶入Experience Platform之公司的簡化ERD。 圖表會強調應分類為XDM類別的基本實體，包括客戶帳戶、飯店和幾個常見的電子商務事件。

![實體關聯圖表，強調應排序為XDM類別以進行資料擷取的必要實體。](../images/best-practices/erd.png)

## 將實體排序為設定檔、查詢及事件類別 {#sort-entities}

建立ERD以識別要帶入Experience Platform的基本實體後，這些實體必須分類為設定檔、查詢和事件類別：

| 類別 | 說明 |
| --- | --- |
| 設定檔圖元 | 設定檔實體代表與個人（通常是客戶）相關的屬性。 屬於此類別的實體應該由基於&#x200B;**[!DNL XDM Individual Profile]類別**&#x200B;的結構描述來表示。 |
| 查詢實體 | 查詢實體代表可能與個人相關的概念，但無法直接用於識別個人。 屬於此類別的實體應該由基於&#x200B;**自訂類別**&#x200B;的結構描述表示，並透過[結構描述關係](../tutorials/relationship-ui.md)連結到設定檔和事件。 |
| 事件實體 | 事件實體代表與客戶可採取的動作、系統事件或您可能想要隨時間追蹤變更的任何其他概念相關的概念。 屬於此類別的實體應該由基於&#x200B;**[!DNL XDM ExperienceEvent]類別**&#x200B;的結構描述來表示。 |

{style="table-layout:auto"}

### 實體排序的考量事項 {#considerations}

以下各節提供如何將實體排序為上述類別的進一步指引。

#### 可變和不可變資料 {#mutable-and-immutable-data}

實體類別之間排序的主要方式是擷取的資料是否可變。

屬於設定檔或查詢實體的屬性通常可變。 例如，客戶的偏好設定可能會隨著時間而改變，而訂閱計畫的引數可根據市場趨勢進行更新。

相較之下，事件資料通常不可變動。 由於事件會附加至特定時間戳記，因此事件提供的「系統快照」不會變更。 例如，事件可在客戶結帳購物車時擷取其偏好設定，即使客戶的偏好設定日後有所變更，也不會變更。 事件資料在記錄後即無法變更。

總而言之，設定檔和查詢實體包含可變屬性，並代表其擷取之主題的最新資訊，而事件則是系統特定時間不可變的記錄。

#### 客戶屬性 {#customer-attributes}

如果實體包含與個別客戶相關的任何屬性，則很可能為設定檔實體。 客戶屬性的範例包括：

* 姓名、出生日期、性別和帳戶ID等個人詳細資訊。
* 位置資訊，例如，地址和GPS資訊。
* 聯絡資訊，例如，電話號碼和電子郵件地址。

#### 追蹤一段時間內的資料 {#track-data}

如果您想要分析實體內的某些屬性如何隨著時間改變，則很可能是事件實體。 例如，在Experience Platform中，將產品專案新增至購物車可以當作購物車新增事件進行追蹤：

| 客戶ID | 類型 | 產品 ID | 數量 | 時間戳記 |
| --- | --- | --- | --- | --- |
| 1234567 | 新增 | 275098 | 2 | 10月1日，上午10:32 |
| 1234567 | 移除 | 275098 | 1 | 10月1日上午10:33 |
| 1234567 | 新增 | 486502 | 1 | 10月1日上午10:41 |
| 1234567 | 新增 | 910482 | 5 | 10月3日，下午2:15 |

{style="table-layout:auto"}

#### 區段使用案例 {#segmentation-use-cases}

將實體分類時，請務必考量您想要建立的對象，以解決您的特定業務使用案例。

例如，某公司想要瞭解忠誠計畫中的所有「黃金」或「白金」會員，去年他們購買了超過五次。 根據此分段邏輯，可以得出有關相關實體應如何呈現的以下結論：

* 「金級」和「白金級」代表適用於個別客戶的忠誠度狀態。 由於區段邏輯僅與客戶目前的忠誠度狀態有關，因此此資料可模組化為設定檔方案的一部分。 如果您想要追蹤忠誠度狀態在一段時間內的變更，也可以針對忠誠度狀態變更建立其他事件結構。
* 購買是指發生於特定時間的事件，而分段邏輯則與指定時間範圍內的購買事件有關。 因此，此資料應該模型化為事件結構描述。

#### 啟用使用案例 {#activation-use-cases}

除了有關區段使用案例的考量事項外，您也應該檢閱這些對象的啟用使用案例，以識別其他相關屬性。

例如，某公司已根據`country = US`的規則建立對象。 然後，當將該對象啟用至某些下游目標時，公司想要根據首頁狀態篩選所有匯出的設定檔。 因此，也應在適用的設定檔實體中擷取`state`屬性。

#### 彙總值 {#aggregated-values}

根據使用案例和資料的粒度，您應決定是否需要預先彙總某些值，才能將其納入設定檔或事件實體中。

例如，一家公司想要根據購物車購買次數來建立受眾。 您可以選擇以最低的詳細程度合併此資料，方法是將每個時間戳記購買事件納入為本身的實體。 但是，這有時可能會以指數方式增加記錄的事件數。 若要減少擷取的事件數，您可以選擇建立一週或一個月長期間的彙總值`numberOfPurchases`。 其他彙總函式(如MIN和MAX)也可套用至這些情況。

>[!CAUTION]
>
>Experience Platform目前不會執行自動值彙總，不過此動作預計會在未來發行中執行。 如果您選擇使用彙總值，則必須先從外部執行計算，再將資料傳送至Experience Platform。

#### 基數 {#cardinality}

在ERD中建立的基數也可提供一些有關如何將實體分類的線索。 如果兩個實體之間有一對多關係，則代表「許多」的實體可能是事件實體。 但是，在某些情況下，「許多」是指一組查詢實體，這些實體在設定檔實體中以陣列形式提供。

>[!NOTE]
>
>由於沒有適用於所有使用案例的通用方法，因此根據基數分類實體時，務必要考慮每種情況的利弊。 如需詳細資訊，請參閱[下一節](#pros-and-cons)。

下表概述一些常見的實體關係，以及可從這些關係衍生的類別：

| 關係 | 基數 | 實體類別 |
| --- | --- | --- |
| 客戶和購物車結帳 | 一對多 | 單一客戶可能會有許多購物車結帳，這些是可隨著時間追蹤的事件。 因此，客戶將成為設定檔實體，而購物車結帳將成為事件實體。 |
| 客戶與忠誠度帳戶 | 一對一 | 單一客戶只能有一個熟客帳戶，且熟客帳戶只能屬於一個客戶。 由於關係是一對一，客戶和忠誠帳戶都會代表設定檔實體。 |
| 客戶與訂閱 | 一對多 | 單一客戶可能有許多訂閱。 由於公司僅關注客戶的目前訂閱，因此客戶是設定檔實體，而訂閱是查詢實體。 |

{style="table-layout:auto"}

### 不同實體類別的優劣 {#pros-and-cons}

雖然上一節提供了決定如何將實體分類的一些一般准則，但請務必瞭解，選擇一個實體類別通常有利有弊。 以下案例研究旨在說明您如何在這些情況下考慮您的選項。

公司會追蹤其客戶的作用中訂閱，其中一位客戶可以有許多訂閱。 該公司也想要納入細分使用案例的訂閱，例如尋找具有有效訂閱的所有使用者。

在此案例中，公司有兩個潛在選項，可用於在其資料模型中表示客戶的訂閱：

1. [使用設定檔屬性](#profile-approach)
1. [使用事件實體](#event-approach)

#### 方法1：使用設定檔屬性 {#profile-approach}

第一種方式是在客戶的設定檔實體中加入`subscriptionID`陣列。

![結構描述編輯器中的客戶結構描述，其類別和結構強調顯示](../images/best-practices/profile-schema.png)

**優點**

* 分段適用於預期的使用案例。
* 結構描述只會為客戶保留最新的訂閱記錄。

**缺點**

* 每當陣列中任何欄位發生變更時，都必須重述整個陣列。
* 如果不同的資料來源或業務單位正在將資料饋送至陣列，則要在所有通道上保持最新更新的陣列同步會是一項挑戰。

#### 方法2：使用事件實體 {#event-approach}

第二種方式是使用事件結構描述來代表訂閱事件。 其中包括訂閱ID以及客戶ID，還有訂閱事件發生的時間戳記。

![醒目提示XDM體驗事件類別和訂閱結構的訂閱事件結構描述圖表。](../images/best-practices/event-schema.png)

**優點**

* 區段規則可更具彈性（例如找出過去30天內變更過訂閱的所有客戶）。
* 客戶的訂閱狀態變更時，您不必再更新客戶設定檔屬性中冗長且可能複雜的陣列。 如果同時變更客戶的訂閱清單來自多個來源，這會特別有用。

**缺點**

* 對於原始預期使用案例（識別客戶最近訂閱的狀態），細分會變得更加複雜。 對象現在需要其他邏輯來標幟客戶的最後一個訂閱事件，以檢查其狀態。
* 事件會自動過期並從設定檔存放區中清除的風險較高。 如需詳細資訊，請參閱[體驗活動有效期](../../profile/event-expirations.md)的指南。

## 根據已分類的實體建立方案 {#schemas-for-categorized-entities}

將實體排序為設定檔、查閱和事件類別後，您就可以開始將資料模型轉換為XDM結構描述。 為了示範，先前顯示的範例資料模型已排序為下圖中的適當類別：

![包含於設定檔、查閱和事件實體中的結構描述圖表](../images/best-practices/erd-sorted.png)

實體已排序的類別應該會決定您為其結構描述所根據的XDM類別。 再次重申：

* 設定檔實體應使用[!DNL XDM Individual Profile]類別。
* 事件實體應使用[!DNL XDM ExperienceEvent]類別。
* 查詢實體應使用貴組織定義的自訂XDM類別。 然後，設定檔和事件實體可以透過結構描述關係參照這些查詢實體。

>[!NOTE]
>
>雖然事件實體幾乎總是由不同的結構描述表示，但設定檔或查詢類別中的實體可能會根據其基數在一個XDM結構描述中組合在一起。
>
>例如，由於客戶實體與LoyaltyAccount實體具有一對一的關係，因此客戶實體的結構描述也可包含`LoyaltyAccount`物件，以包含每個客戶的適當忠誠度欄位。 但是，如果關係是一對多，則代表「多」的實體可能會由單獨的結構描述或設定檔屬性陣列表示，具體取決於其複雜性。

以下各節提供根據您的ERD建構方案的一般指引。

### 採用反複的模型方法 {#iterative-modeling}

結構描述演化[&#128279;](./composition.md#evolution)的規則規定，在結構描述實作後，只能對結構描述進行非破壞性變更。 換言之，一旦您將欄位新增到結構描述並且已根據該欄位擷取資料，就無法再移除該欄位。 因此，當您首次建立結構描述時，一定要採用反複的模型方法，從隨著時間推移逐漸增加複雜性的簡化實作開始。

如果您不確定某個特定欄位是否必須包含在結構描述中，最佳作法是將其排除在外。 如果之後確定該欄位是必要的，可隨時將其新增到結構的下一個疊代中。

### 身分識別欄位 {#identity-fields}

在Experience Platform中，標示為身分的XDM欄位可用來拼接來自多個資料來源的個別客戶相關資訊。 雖然結構描述可以有多個欄位標示為身分，但必須定義單一主要身分，才能讓結構描述在[!DNL Real-Time Customer Profile]中使用。 如需這些欄位使用案例的詳細資訊，請參閱結構描述組合基本知識中[身分欄位](./composition.md#identity)的相關章節。

在設計方案時，關聯式資料庫表格中的任何主索引鍵都可能是主要身分的候選專案。 適用身分欄位的其他範例是客戶電子郵件地址、電話號碼、帳戶ID和[ECID](../../identity-service/features/ecid.md)。

### Adobe應用程式結構欄位群組 {#adobe-application-schema-field-groups}

Experience Platform提供幾個現成的XDM結構描述欄位群組，用於擷取與下列Adobe應用程式相關的資料：

* Adobe Analytics
* Adobe Audience Manager
* Adobe Campaign
* Adobe Target

例如，您可以使用[[!UICONTROL Adobe Analytics ExperienceEvent範本]欄位群組](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/analytics/experienceevent-all.schema.json)，將[!DNL Analytics]特定欄位對應到您的XDM結構描述。 根據您使用的Adobe應用程式，您應在結構中使用這些Adobe提供的欄位群組。

![ [!UICONTROL Adobe Analytics ExperienceEvent範本]的結構描述圖表。](../images/best-practices/analytics-field-group.png)

Adobe應用程式欄位群組會透過使用`identityMap`欄位自動指派預設主要身分，該欄位是系統產生的唯讀物件，可對應個別客戶的標準身分值。

對於Adobe Analytics，ECID是預設的主要身分。 如果客戶未提供ECID值，則主要身分會預設為AAID。

>[!IMPORTANT]
>
>使用Adobe應用程式欄位群組時，其他任何欄位都不應標示為主要身分。 如果有其他屬性需要標籤為身分，這些欄位必須指派為次要身分。

## 資料驗證欄位 {#data-validation-fields}

當您將資料內嵌至Data Lake時，只會針對受限欄位強制執行資料驗證。 若要在批次擷取期間驗證特定欄位，您必須在XDM結構描述中將欄位標籤為受限。 為了防止將不良資料擷取到Experience Platform，建議您在建立結構描述時，定義欄位層級驗證的條件。

>[!IMPORTANT]
>
>驗證不適用於巢狀欄。 如果欄位格式位於陣列欄中，將不會驗證資料。

若要在特定欄位上設定限制，請從結構描述編輯器中選取欄位，以開啟&#x200B;**[!UICONTROL 欄位屬性]**&#x200B;側欄。 如需可用欄位的確切說明，請參閱[特定型別欄位屬性](../ui/fields/overview.md#type-specific-properties)的相關檔案。

![結構描述編輯器，在[!UICONTROL 欄位屬性]側邊欄中反白顯示限制欄位。](../images/best-practices/data-validation-fields.png)

### 維持資料完整性的秘訣 {#data-integrity-tips}

以下是在您建立結構描述時用來維護資料完整性的建議集合。

* **以主要身分為例**：對於網頁SDK、行動SDK、Adobe Analytics和Adobe Journey Optimizer等Adobe產品，`identityMap`欄位通常可作為主要身分。 避免將其他欄位指定為該結構描述的主要身分。
* **確定`_id`未作為身分使用**：體驗事件結構描述中的`_id`欄位無法作為身分使用，因為它適用於記錄唯一性。
* **設定長度限制**：最佳實務是在標示為身分的欄位上設定最小和最大長度。 如果您嘗試將自訂名稱空間指派給身分欄位，但不符合最小和最大長度限制，則會觸發警告。 這些限制有助於維持一致性和資料品質。
* **套用一致值的模式**：如果您的身分值遵循特定模式，您應該使用&#x200B;**[!UICONTROL 模式]**&#x200B;設定來強制此限制。 此設定可包含僅數字、大寫或小寫或特定字元組合等規則。 使用規則運算式來比對字串中的模式。
* **在Analytics結構描述中限制eVar**：通常，Analytics結構描述應該只將一個eVar指定為身分。 如果您打算使用多個eVar作為身分，應仔細檢查資料結構是否可以最佳化。
* **確定所選欄位的唯一性**：與結構描述中的主要身分相比，您選擇的欄位應該是唯一的。 如果不是，請勿標籤為身分。 例如，如果多位客戶可以提供相同的電子郵件地址，則該名稱空間不是合適的身分。 此原則也適用於其他身分識別名稱空間，例如電話號碼。 將非唯一欄位標示為身分可能會導致不需要的設定檔摺疊。
* **驗證字串長度下限**：所有字串欄位的長度至少要有一個字元，因為字串值絕不能空白。 不過，可接受非必要欄位的Null值。 新字串欄位預設會有一個最小長度。

## 後續步驟

本檔案說明為Experience Platform設計資料模型的一般准則和最佳作法。 總結：

* 在建構方案之前，使用由上而下的方法，將資料表格排序為設定檔、查詢和事件類別。
* 在設計針對不同目的的結構時，通常有多種方法和選項。
* 您的資料模型應該支援您的業務使用案例，例如細分或客戶歷程分析。
* 儘可能簡化您的結構描述，只在絕對必要時新增欄位。

準備就緒後，請參閱有關[在UI](../tutorials/create-schema-ui.md)中建立結構描述的教學課程，以取得如何建立結構描述、為實體指派適當類別，以及新增欄位以對應資料的逐步指示。
