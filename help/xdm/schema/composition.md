---
keywords: Experience Platform；首頁；熱門主題；架構；架構；列舉；mixin；欄位群組；欄位群組；mixin；資料型別；資料型別；資料型別；主要身分；XDM個人設定檔；XDM欄位；列舉資料型別；體驗事件；XDM體驗事件；XDM ExperienceEvent；experienceevent；XDM Experienceevent；架構設計；類別；類別；類別；類別；資料型別；資料型別；架構；架構架構；identityMap；身份對映；身份對映；架構設計；對映；合併架構；合併
solution: Experience Platform
title: 結構描述組合基本概念
description: 瞭解Experience Data Model (XDM)結構描述，以及在Adobe Experience Platform中構成結構描述的建置組塊、原則和最佳實務。
exl-id: d449eb01-bc60-4f5e-8d6f-ab4617878f7e
source-git-commit: 595d9bd6a0aa0c9f1059e485c54e89ce02b7ec68
workflow-type: tm+mt
source-wordcount: '4365'
ht-degree: 8%

---

# 結構描述構成的基礎知識

瞭解Experience Data Model (XDM)結構描述，以及在Adobe Experience Platform中構成結構描述的建置組塊、原則和最佳實務。 如需XDM的一般資訊以及在[!DNL Platform]中的使用方式，請參閱[XDM系統概覽](../home.md)。

## 了解結構描述 {#understanding-schemas}

結構是一組規則，可代表及驗證資料的結構和格式。 從高層面來說，結構提供了真實對象 (如人) 的抽象定義，並概述應包含在該對象的每個執行個體中的資料 (如名字、姓氏、生日等)。

除了說明資料結構外，結構描述還會對資料套用限制和期望，以便在系統之間移動時進行驗證。 這些標準定義可讓資料以一致方式解譯，無論其來源為何，並移除跨應用程式翻譯的需求。

Experience Platform會使用結構來維護此語意標準化。 結構描述是 Experience Platform 描述資料的標準方式，允許所有符合結構描述的資料在整個組織重複使用而不會產生衝突，甚至可在多個組織之間共用。

XDM結構描述適合用來以獨立格式儲存大量複雜的資料。 請參閱本檔案附錄中[內嵌物件](#embedded)和[巨量資料](#big-data)的章節，以取得有關XDM如何完成此作業的詳細資訊。

### Experience Platform中的結構描述型工作流程 {#schema-based-workflows}

標準化是Experience Platform背後的關鍵概念。 XDM以Adobe為驅動，致力於標準化客戶體驗資料並定義客戶體驗管理的標準結構描述。

建置Experience Platform的基礎結構（稱為[!DNL XDM System]）有助於以結構描述為基礎的工作流程，並包含[!DNL Schema Registry]、[!DNL Schema Editor]、結構描述中繼資料和服務使用模式。 如需詳細資訊，請參閱[XDM系統總覽](../home.md)。

在Experience Platform中使用結構描述有幾個主要優點。 首先，結構描述可提供更好的資料控管和資料最小化，這對隱私權法規尤其重要。 第二，使用Adobe的標準元件建置結構描述可允許現成的深入分析和以最少的自訂使用AI/ML服務。 最後，結構描述可提供資料共用見解和高效協調的基礎架構。

## 規劃您的結構描述 {#planning}

建立結構描述的第一步是決定您嘗試在結構描述中擷取的概念，或真實世界的物件。 一旦您識別出您要描述的概念後，請思考資料型別、潛在身分欄位以及結構描述未來可能如何演化，以開始規劃結構描述。

### Experience Platform中的資料行為 {#data-behaviors}

打算用於Experience Platform的資料分為兩種行為型別：

* **記錄資料**：提供有關主旨屬性的資訊。 主旨可以是組織或個人。
* **時間序列資料**：提供記錄主體直接或間接執行動作時的系統快照。

所有XDM結構描述都說明可歸類為記錄或時間序列的資料。 結構描述的資料行為由結構描述的類別定義，該類別在首次建立時指派給結構描述。 本檔案稍後將詳細說明XDM類別。

記錄和時間序列結構描述都包含身分地圖(`xdm:identityMap`)。 此欄位包含主旨的身分表示，從標示為「身分」的欄位中擷取，如下節所述。

### [!UICONTROL 身分識別] {#identity}

>[!CONTEXTUALHELP]
>id="platform_schemas_identities"
>title="結構描述中的身分識別"
>abstract="身分識別是結構描述中的重要欄位，可用於身分識別主題，例如電子郵件地址或行銷 ID。這些欄位用於為每個人建構身分識別圖並建立客戶輪廓。如需進一步了解結構描述中的身分識別，請查看此文件。"

結構用於擷取資料到Experience Platform中。 此資料可用於多項服務，以建立個別實體的單一、統一檢視。 因此，在為客戶身分設計結構時，重要的是考慮哪些欄位可用於識別主旨，無論資料來自何處。

為了協助進行此程式，結構描述中的關鍵欄位可以標示為身分。 資料擷取後，這些欄位中的資料會插入該個人的&quot;[!UICONTROL 身分圖表]&quot;。 然後[[!DNL Real-Time Customer Profile]](../../profile/home.md)和其他Experience Platform服務可以存取圖表資料，以提供每個個別客戶的拼接檢視。

通常標示為「[!UICONTROL 身分]」的欄位包括：電子郵件地址、電話號碼、[[!DNL Experience Cloud ID (ECID)]](https://experienceleague.adobe.com/docs/id-service/using/home.html)、CRM ID或其他唯一ID欄位。 請考量您組織特定的任何唯一識別碼，因為這些識別碼可能是好的&quot;[!UICONTROL 身分]&quot;欄位。

在結構描述規劃階段思考客戶身分非常重要，以協助確保資料彙集在一起，以儘可能建置最強大的設定檔。 若要進一步瞭解身分資訊如何協助您為客戶傳遞數位體驗，請參閱[身分識別服務概覽](../../identity-service/home.md)。 請參閱資料模型最佳實務檔案，以取得[建立結構描述](./best-practices.md#data-validation-fields)時使用身分的相關提示。

有兩種方式可將身分資料傳送至Platform：

1. 透過[結構描述編輯器UI](../ui/fields/identity.md)或使用[結構描述登入API](../api/descriptors.md#create)，將身分描述項新增至個別欄位
1. 使用[`identityMap`欄位](#identityMap)

#### `identityMap` {#identityMap}

`identityMap`是對應型別欄位，說明個人的各種身分值及其關聯的名稱空間。 此欄位可用於提供結構描述的身分資訊，而非在結構描述本身的結構中定義身分值。

使用`identityMap`的主要缺點是，身分會內嵌在資料中，因此變得較不顯眼。 如果您要擷取原始資料，則應在實際結構描述結構中定義個別身分欄位。

>[!NOTE]
>
>使用`identityMap`的結構描述可以做為關聯性中的來源結構描述，但不能做為參考結構描述。 這是因為所有參考結構描述都必須具備可見的身分識別，且可以在來源結構描述內的參考欄位中進行對應。 請參閱[關係](../tutorials/relationship-ui.md)的UI指南，以取得來源和參考結構描述需求的詳細資訊。

不過，如果結構描述的身分識別數目不同，或是您從一起儲存身分識別的來源(例如[!DNL Airship]或Adobe Audience Manager)匯入資料，身分對應就相當實用。 此外，如果您使用[Adobe Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/home/)，則需要身分對應。

簡單身分對應的範例看起來像這樣：

```json
"identityMap": {
  "email": [
    {
      "id": "jsmith@example.com",
      "primary": true
    }
  ],
  "ECID": [
    {
      "id": "87098882279810196101440938110216748923",
      "primary": false
    },
    {
      "id": "55019962992006103186215643814973128178",
      "primary": false
    }
  ],
  "CRMID": [
    {
      "id": "2e33192000007456-0365c00000000000",
      "primary": false
    }
  ]
}
```

如上述範例所示，`identityMap`物件中的每個索引鍵都代表一個身分名稱空間。 每個索引鍵的值是一個物件陣列，代表個別名稱空間的識別值(`id`)。 請參閱[!DNL Identity Service]檔案以取得Adobe應用程式可辨識的標準識別名稱空間](../../identity-service/troubleshooting-guide.md#standard-namespaces)的[清單。

>[!NOTE]
>
>也可以為每個身分值提供布林值，表示值是否為主要身分(`primary`)。 您只需要設定要在[!DNL Real-Time Customer Profile]中使用的結構描述的主要身分。 如需詳細資訊，請參閱[聯合結構描述](#union)的相關章節。

### 結構描述演化原則 {#evolution}

由於數位體驗的性質持續演化，因此用來代表體驗的結構描述也必須持續演化。 因此，設計良好的結構描述能夠視需要調整和演變，而不會對結構描述的先前版本造成破壞性變更。

由於維持回溯相容性對架構演化至關重要，因此Experience Platform會強制實施純粹加性的版本設定原則。 此原則可確保對結構描述的任何修訂只會產生非破壞性的更新和變更。 換言之，不支援&#x200B;**中斷變更。**

>[!NOTE]
>
>您只能在結構描述中引入重大變更，如果尚未使用它來將資料擷取到Experience Platform，並且尚未啟用用於即時客戶個人檔案。 不過，一旦結構描述已在[!DNL Platform]中使用，它就必須遵守加法版本設定原則。

下表劃分在編輯方案、欄位群組和資料型別時支援的變更：

| 支援的變更 | 重大變更（不支援） |
| --- | --- |
| <ul><li>將新欄位新增至資源</li><li>將必填欄位設為選用</li><li>引入新的必填欄位*</li><li>變更資源的顯示名稱和說明</li><li>啟用結構描述以參與設定檔</li></ul> | <ul><li>移除先前定義的欄位</li><li>重新命名或重新定義現有欄位</li><li>移除或限制先前支援的欄位值</li><li>將現有欄位移至樹狀結構中的其他位置</li><li>刪除結構描述</li><li>停用參與設定檔的結構描述</li></ul> |

\**請參考下節以取得有關[設定新必要欄位](#post-ingestion-required-fields).*&#x200B;的重要考量

### 必填欄位

個別結構描述欄位可以[標籤為必要](../ui/fields/required.md)，這表示任何擷取的記錄都必須包含這些欄位中的資料才能通過驗證。 例如，將結構描述的主要身分欄位設定為必要有助於確保所有擷取的記錄都將參與即時客戶個人檔案。 同樣地，視需要設定時間戳記欄位可確保所有時間序列事件都按時間順序保留。

>[!IMPORTANT]
>
>無論結構描述欄位是否為必要欄位，Platform不接受任何內嵌欄位的`null`或空值。 如果記錄或事件中沒有特定欄位的值，則應該從擷取裝載中排除該欄位的索引鍵。

#### 在內嵌後視需要設定欄位 {#post-ingestion-required-fields}

如果欄位曾用於擷取資料，且最初未設定為必要，則該欄位對於某些記錄可能會有null值。 如果您將此欄位設為必要的擷取後，即使歷史記錄可能為Null，所有未來記錄都必須包含此欄位的值。

將先前可選欄位設為必要欄位時，請記住下列事項：

1. 如果您查詢歷史資料並將結果寫入新資料集，某些列會失敗，因為它們包含必要欄位的null值。
1. 如果欄位參與了[即時客戶設定檔](../../profile/home.md)，而您在視需要設定它之前匯出資料，則某些設定檔可能會為空值。
1. 您可以使用Schema Registry API來檢視Platform中所有XDM資源的時間戳記變更記錄，包括新的必要欄位。 如需詳細資訊，請參閱[稽核記錄端點](../api/audit-log.md)的指南。

### 結構描述和資料擷取

若要將資料擷取至Experience Platform，必須先建立資料集。 資料集是[[!DNL Catalog Service]](../../catalog/home.md)的資料轉換和追蹤的建置組塊，通常代表包含擷取資料的資料表或檔案。 所有資料集都以現有的XDM結構描述為基礎，這些結構描述會針對所擷取的資料應該包含的內容以及應該如何建構提供限制。 如需詳細資訊，請參閱[Adobe Experience Platform資料擷取](../../ingestion/home.md)的概觀。

## 結構描述的建置區塊 {#schema-building-blocks}

Experience Platform使用組合方法，其中結合標準建置區塊以建立方案。 此方法可促進現有元件的重複使用性，並推動業界標準化，以支援[!DNL Platform]中的廠商結構描述和元件。

使用下列公式來構成結構描述：

**類別+結構描述欄位群組&amp;amp；ast； = XDM結構描述**

&amp;amp；ast；結構描述是由類別和零個或多個結構描述欄位群組所組成。 這表示您完全可以使用欄位群組來撰寫資料集結構。

### 類別 {#class}

>[!CONTEXTUALHELP]
>id="platform_schemas_class"
>title="類別"
>abstract="每個結構描述都以單一類別為基礎。類別定義了結構描述的行為，以及做為所有結構描述的基礎且類別必須包含的通用屬性。如需深入了解類別如何參與結構描述的構成，請查看此文件。"

>[!CONTEXTUALHELP]
>id="platform_schemas_class_industries"
>title="行業類型"
>abstract="如果選擇與您業務相關的行業，機器學習模式可以更準確地將來源欄位對應到符合行業標準的標準欄位群組，以提供更好的資料組織。這可確保系統根據您的行業特定需求，量身打造資料整合結果，以產生更精確和相關的資料深入解析。"

構成結構描述從指派類別開始。 類別會定義結構描述將包含之資料（記錄或時間序列）的行為方面。 除此之外，類別會說明基於該類別的所有結構描述所需包含的最小通用屬性數量，並提供合併多個相容資料集的方法。

結構描述的類別會決定哪些欄位群組適合在該結構描述中使用。 將在[下一節](#field-group)中更詳細地討論這個問題。

Adobe提供幾個標準（「核心」） XDM類別。 這些類別中的兩個[!DNL XDM Individual Profile]和[!DNL XDM ExperienceEvent]是幾乎所有下游平台處理序的必要專案。 除了這些核心類別以外，您也可以建立自己的自訂類別，以說明貴組織更具體的使用案例。 當沒有Adobe定義的核心類別可用於描述獨特的使用案例時，自訂類別由組織定義。

下列熒幕擷圖示範類別在Platform UI中的呈現方式。 由於顯示的範例結構描述不包含任何欄位群組，因此所有顯示的欄位都由結構描述的類別（[!UICONTROL XDM個別設定檔]）提供。

![結構描述編輯器中的[!UICONTROL XDM個別設定檔]。](../images/schema-composition/class.png)

如需可用標準XDM類別的最新清單，請參閱[官方XDM存放庫](https://github.com/adobe/xdm/tree/master/components/classes)。 或者，如果您偏好在UI中檢視資源，您可以參閱[探索XDM元件](../ui/explore.md)的指南。

### 欄位群組 {#field-group}

>[!CONTEXTUALHELP]
>id="platform_schemas_fieldgroup"
>title="欄位群組"
>abstract="欄位群組是可重複使用的元件，可讓您使用額外屬性擴充結構描述。大部分欄位群組僅與部分類別相容。您可以使用 Adobe 定義的標準欄位群組，或是手動定義您自己的自訂欄位群組。如需深入了解欄位群組如何參與結構描述的構成，請查看此文件。"

>[!CONTEXTUALHELP]
>id="platform_schemas_fieldgroup_requiredFieldgroup"
>title="必要欄位群組"
>abstract="您正在使用的來源需要此欄位群組。因此，您無法將其從結構描述中刪除。"

欄位群組是可重複使用的元件，可定義一或多個實作特定功能的欄位，例如個人詳細資料、飯店偏好設定或地址。 欄位群組是要包含在實作相容類別的結構描述中。

欄位群組會根據其代表的資料行為（記錄或時間序列），定義與其相容的類別或類別。 這表示並非所有欄位群組都可用於所有類別。

Experience Platform包含許多標準Adobe欄位群組，同時也允許廠商為其使用者定義欄位群組，以及允許個別使用者為自己的特定概念定義欄位群組。

例如，若要擷取「[!UICONTROL 忠誠會員]」結構描述的「[!UICONTROL 名字]」和「[!UICONTROL 住家地址]」等詳細資料，您可以使用定義這些一般概念的標準欄位群組。 不過，標準欄位群組可能未涵蓋的組織專用概念（例如自訂忠誠度方案詳細資訊或產品屬性）。 在這種情況下，您必須定義自己的欄位群組來擷取此資訊。

>[!NOTE]
>
>強烈建議您在結構描述中儘可能使用標準欄位群組，因為Experience Platform服務會隱含瞭解這些欄位，並且在跨[!DNL Platform]元件使用時可提供較一致的一致性。
>
>標準元件（例如「名字」和「電子郵件地址」）提供的欄位包含基本純量欄位型別以外的新增內涵。 它們會告訴[!DNL Platform]，共用相同資料型別的任何欄位將會以相同的方式運作。 無論資料來自何處，或資料正由哪個[!DNL Platform]服務使用，此行為皆可信賴為一致。

請記住，結構描述是由「零個或多個」欄位群組組成，因此這表示您可以撰寫有效的結構描述而不需使用任何欄位群組。

下列熒幕擷圖示範欄位群組在Platform UI中的呈現方式。 在此範例中，單一欄位群組（[!UICONTROL 人口統計詳細資料]）已新增至結構描述，該結構描述提供結構描述結構的一組欄位。

![結構描述編輯器在範例結構描述中反白顯示[!UICONTROL 人口統計詳細資料]欄位群組。](../images/schema-composition/field-group.png)

如需可用標準XDM欄位群組的最新清單，請參閱[官方XDM存放庫](https://github.com/adobe/xdm/tree/master/components/fieldgroups)。 或者，如果您偏好在UI中檢視資源，您可以參閱[探索XDM元件](../ui/explore.md)的指南。

>[!NOTE]
>
> 標準XDM欄位群組一律在發展，而且某些欄位群組已被取代。 如需最新更新的已棄用欄位群組清單，請參閱官方XDM存放庫中的[已棄用欄位群組區段](https://github.com/adobe/xdm/tree/master/components/fieldgroups/deprecated)。

### 資料類型 {#data-type}

資料型別在類別或結構描述中作為參考欄位型別使用，其使用方式與基本常值欄位相同。 主要差異在於，資料型別可與欄位群組相同的方式定義多個子欄位。 兩者之間的主要差異在於，資料型別可以新增為欄位的「資料型別」，包含於結構描述中的任何位置。 雖然欄位群組僅與某些類別相容，但資料型別可包含在任何父類別或欄位群組中。

>[!NOTE]
>
>如果欄位定義為特定資料型別，則無法在另一個結構描述中以不同的資料型別建立相同的欄位。 此限制適用於您組織的租使用者。

Experience Platform提供一些通用資料型別作為[!DNL Schema Registry]的一部分，以支援使用標準模式來說明通用資料結構。 在[結構描述登入教學課程](../tutorials/create-schema-api.md)中對此有更詳細的說明，當您逐步完成定義資料型別的步驟時，將會變得更清晰。

下列熒幕擷圖示範資料型別在Platform UI中的呈現方式。 [!UICONTROL 人口統計詳細資料]欄位群組所提供的其中一個欄位使用&quot;[!UICONTROL Object]&quot;資料型別，如欄位名稱旁的垂直號字元(`|`)後面的文字所指示。 此特定資料型別提供與個人名稱相關的幾個子欄位，此建構可重複用於需要擷取個人名稱的其他欄位。

![結構描述編輯器中個人全名物件和屬性反白顯示圖。](../images/schema-composition/data-type.png)

如需可用標準XDM資料型別的最新清單，請參閱[官方XDM存放庫](https://github.com/adobe/xdm/tree/master/components/datatypes)。 或者，如果您偏好在UI中檢視資源，您可以參閱[探索XDM元件](../ui/explore.md)的指南。

>[!NOTE]
>
> 標準XDM資料型別一律在發展，部分資料型別已被取代。 如需最新更新的已棄用資料型別清單，請參閱官方XDM存放庫中的[已棄用資料型別區段](https://github.com/adobe/xdm/tree/master/components/datatypes/deprecated)。

### 欄位 {#field}

欄位是結構描述中最基本的建置區塊。 欄位透過定義特定資料型別，提供其可包含之資料型別的相關限制。 這些基本資料型別會定義單一欄位，而先前提到的[資料型別](#data-type)可讓您定義多個子欄位，並在各種結構描述中重複使用相同的多欄位結構。 因此，除了將欄位的「資料型別」定義為登入中定義的其中一種資料型別外，Experience Platform還支援基本純量型別，例如：

* 字串
* 整數
* 雙精度
* 布林值
* 陣列
* 物件

>[!TIP]
>
>如需在物件型別欄位上使用任意格式欄位的優缺點相關資訊，請參閱[附錄](#objects-v-freeform)。

這些純量型別的有效範圍可以進一步限製為特定圖樣、格式、最小值/最大值或預先定義的值。 使用這些限制，可以表示各種更具體的欄位型別，包括：

* 列舉
* 長整數
* 短整數
* 位元組
* 日期
* 日期時間
* 地圖

>[!NOTE]
>
>「對應」欄位型別允許索引鍵值配對資料，包括單一索引鍵的多個值。 您可以在標準XDM類別和欄位群組中找到對應，但您也可以定義自訂對應。 如需詳細資訊，請參閱[定義自訂對應欄位](../tutorials/custom-fields-api.md#custom-maps)上的API教學課程，或[在UI](../ui/fields/map.md)中定義對應欄位的指南。

## 組合範例 {#composition-example}

結構描述是使用組合模型建置，並代表要擷取到[!DNL Platform]中的資料格式和結構。 如前所述，這些結構描述由一個類別和零個或多個與該類別相容的欄位群組組成。

例如，描述在零售商店進行的購買的結構描述可能稱為「[!UICONTROL 商店交易]」。 結構描述實作結合標準[!UICONTROL Commerce]欄位群組和使用者定義的[!UICONTROL 產品資訊]欄位群組的[!DNL XDM ExperienceEvent]類別。

追蹤網站流量的另一個結構描述可能稱為「[!UICONTROL 網站造訪]」。 它也實作[!DNL XDM ExperienceEvent]類別，但這次結合標準[!UICONTROL Web]欄位群組。

下圖顯示這些結構以及每個欄位群組貢獻的欄位。 其中也包含兩個以[!DNL XDM Individual Profile]類別為基礎的結構描述，包括本指南中先前提及的&quot;[!UICONTROL 忠誠會員]&quot;結構描述。

![四個結構描述和貢獻它們的欄位群組的流程圖。](../images/schema-composition/composition.png)

### 聯合 {#union}

雖然Experience Platform可讓您針對特定使用案例來撰寫結構描述，但也允許您檢視特定類別型別的結構描述「聯合」。 上圖顯示兩個以XDM ExperienceEvent類別為基礎的結構描述，以及兩個以[!DNL XDM Individual Profile]類別為基礎的結構描述。 如下所示的等位會彙總共用相同類別的所有結構描述（分別為[!DNL XDM ExperienceEvent]和[!DNL XDM Individual Profile]）的欄位。

![聯合結構描述流程圖，其中描繪構成這些欄位的欄位。](../images/schema-composition/union.png)

透過啟用結構描述以搭配[!DNL Real-Time Customer Profile]使用，它就包含在該類別型別的聯合中。 [!DNL Profile]針對客戶在與[!DNL Platform]整合的任何系統中發生的每個事件，提供健全且集中的客戶屬性設定檔和時間戳記帳戶。 [!DNL Profile]使用聯合檢視來表示此資料，並提供每個個別客戶的整體檢視。

如需使用[!DNL Profile]的詳細資訊，請參閱[即時客戶個人檔案總覽](../../profile/home.md)。

## 將資料檔對應至XDM結構描述 {#mapping-datafiles}

所有內嵌至Experience Platform的資料檔都必須符合XDM結構描述的結構。 如需有關如何格式化資料檔以符合XDM階層（包括範例檔案）的詳細資訊，請參閱[範例ETL轉換](../../etl/transformations.md)的檔案。 如需將資料檔擷取到Experience Platform的一般資訊，請參閱[批次擷取總覽](../../ingestion/batch-ingestion/overview.md)。

## 外部對象的結構

如果您要將受眾從外部系統引進Platform，您必須使用以下元件在您的結構中擷取它們：

* [[!UICONTROL 區段定義]類別](../classes/segment-definition.md)：使用此標準類別來擷取外部區段定義的索引鍵屬性。
* [[!UICONTROL 區段會籍詳細資料]欄位群組](../field-groups/profile/segmentation.md)：將此欄位群組新增至您的[!UICONTROL XDM個人設定檔]結構描述，以將客戶設定檔與特定對象建立關聯。

## 後續步驟

現在您已瞭解結構描述組合的基本知識，您已準備好開始使用[!DNL Schema Registry]探索和建置結構描述。

若要檢閱兩個核心XDM類別的結構及其常用的相容欄位群組，請參閱下列參考檔案：

* [[!DNL XDM Individual Profile]](../classes/individual-profile.md)
* [[!DNL XDM ExperienceEvent]](../classes/experienceevent.md)

[!DNL Schema Registry]是用來存取Adobe Experience Platform中的[!DNL Schema Library]，並提供使用者介面和RESTful API，以便存取所有可用的程式庫資源。 [!DNL Schema Library]包含由Adobe定義的產業資源、由Experience Platform合作夥伴定義的廠商資源，以及由您組織的成員組成的類別、欄位群組、資料型別和結構描述。

若要使用UI開始撰寫結構描述，請連同[結構描述編輯器教學課程](../tutorials/create-schema-ui.md)一起建立本檔案中提及的「忠誠會員」結構描述。

若要開始使用[!DNL Schema Registry] API，請先閱讀[Schema Registry API開發人員指南](../api/getting-started.md)。 閱讀開發人員指南後，請依照教學課程中概述的步驟，使用Schema Registry API建立結構描述[](../tutorials/create-schema-api.md)。

## 附錄

以下小節包含有關結構描述組合原則的其他資訊。

### 關聯式表格與內嵌物件 {#embedded}

使用關聯式資料庫時，最佳實務包括標準化資料，或是將實體分割為多個分散的片段，然後顯示在多個表格中。 若要整體讀取資料或更新實體，必須使用JOIN對許多個別表格進行讀取和寫入作業。

透過使用內嵌物件，XDM結構描述可以直接表示複雜的資料，並將其儲存在具有階層結構的獨立檔案中。 此結構的主要優點之一，是它可讓您查詢資料，而不需透過昂貴的連線來重新建構實體，以連線多個非正規化表格。 對於您的結構描述階層可以包含多少層級，沒有嚴格限制。

### 結構描述和巨量資料 {#big-data}

現代數位系統會產生大量行為訊號（交易資料、網站記錄檔、物聯網、顯示等）。 這種巨量資料提供絕佳機會來最佳化體驗，但由於資料的規模和多樣性而難以使用。 若要從資料中獲得價值，其結構、格式和定義必須標準化，以便能一致且有效地處理。

結構描述可解決此問題，其方式是允許從多個來源整合資料、透過通用結構和定義進行標準化，並在解決方案之間共用。 如此一來，後續程式和服務就能解答任何型別的資料問題。 它告別傳統的資料模型化方法，即將詢問資料的所有問題都已預先知道，且資料模型化符合這些期望。

### 物件與自由表單欄位 {#objects-v-freeform}

在設計結構時，透過自由格式欄位選擇物件時要考慮一些關鍵因素：

| 物件 | 自由格式欄位 |
| --- | --- |
| 增加巢狀 | 較少或沒有巢狀 |
| 建立邏輯欄位群組 | 欄位會放置在臨機位置 |

{style="table-layout:auto"}

#### 物件

以下列出在自由格式欄位上使用物件的優缺點。

**優點**：

* 當您想要建立特定欄位的邏輯群組時，最好使用物件。
* 物件會以更具結構化的方式組織結構描述。
* 物件間接有助於在區段產生器UI中建立良好的功能表結構。 結構描述中的分組欄位會直接反映在區段產生器UI中提供的資料夾結構中。

**缺點**：

* 欄位會變得更巢狀。
* 使用[Adobe Experience Platform查詢服務](../../query-service/home.md)時，必須為巢狀物件中的查詢欄位提供較長的參考字串。

#### 自由格式欄位

以下列出在物件上使用自由格式欄位的優點和缺點。

**優點**：

* 自由格式欄位會直接建立於結構描述(`_tenantId`)的根物件下，以增加可見度。
* 使用查詢服務時，自由格式欄位的參考字串往往較短。

**缺點**：

* 結構描述中自由格式欄位的位置是臨機操作的，這表示它們會依字母順序出現在結構描述編輯器中。 這會使結構描述較少結構化，而類似的自由格式欄位可能會根據其名稱出現大幅分隔。
