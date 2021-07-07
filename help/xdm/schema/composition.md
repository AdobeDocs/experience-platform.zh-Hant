---
keywords: Experience Platform；首頁；熱門主題；方案；方案；枚舉；混合；欄位組；混合；資料類型；資料類型；資料類型；主要身份；主要身份； XDM個人配置檔案； XDM欄位；枚舉資料類型；體驗事件； XDM體驗事件； XDM體驗事件； XDM ExperienceEvent; XDM ExperienceEvent; XDM ExperienceEvent；方案；設計；類別；類別；類別；資料類型；資料類型；地圖；資料類型；IdentityMap架構設計；地圖；地圖；聯合架構；聯合
solution: Experience Platform
title: Basics of Schema Composition
topic-legacy: overview
description: 本檔案介紹Experience Data Model(XDM)結構，以及合成結構以用於Adobe Experience Platform的結構的建置組塊、原則和最佳實務。
exl-id: d449eb01-bc60-4f5e-8d6f-ab4617878f7e
source-git-commit: afe748d443aad7b6da5b348cd569c9e806e4419b
workflow-type: tm+mt
source-wordcount: '3726'
ht-degree: 0%

---

# Basics of schema composition

本檔案介紹[!DNL Experience Data Model](XDM)結構，以及合成要在Adobe Experience Platform中使用的結構的組成模組、原則和最佳實務。 For general information on XDM and how it is used within [!DNL Platform], see the [XDM System overview](../home.md).

## Understanding schemas

結構是一組規則，可代表及驗證資料的結構和格式。 At a high level, schemas provide an abstract definition of a real-world object (such as a person) and outline what data should be included in each instance of that object (such as first name, last name, birthday, and so on).

In addition to describing the structure of data, schemas apply constraints and expectations to data so it can be validated as it moves between systems. 這些標準定義允許一致地解釋資料（無論來源為何），並消除跨應用程式翻譯的需要。

[!DNL Experience Platform] 使用結構來維護此語義標準化。Schemas are the standard way of describing data in [!DNL Experience Platform], allowing all data that conforms to schemas to be reused across an organization without conflicts, or even shared between multiple organizations.

XDM結構非常適合以獨立格式儲存大量複雜資料。 請參閱本檔案附錄中[內嵌物件](#embedded)和[big data](#big-data)的相關章節，以了解XDM如何完成此作業的詳細資訊。

### [!DNL Experience Platform]中的架構型工作流程

標準化是[!DNL Experience Platform]背後的一個關鍵概念。 XDM受Adobe推動，致力於標準化客戶體驗資料，並定義客戶體驗管理的標準結構。

The infrastructure on which [!DNL Experience Platform] is built, known as [!DNL XDM System], facilitates schema-based workflows and includes the [!DNL Schema Registry], [!DNL Schema Editor], schema metadata, and service consumption patterns. See the [XDM System overview](../home.md) for more information.

善用[!DNL Experience Platform]中的結構有幾個主要優點。 首先，結構可改善資料控管和資料最小化，這對隱私權法規尤其重要。 其次，使用Adobe的標準元件建立結構，可立即獲得深入分析，並使用AI/ML服務，且自訂項目最少。 最後，結構為資料共用見解和高效協調提供了基礎架構。

## 規劃您的結構

The first step in building a schema is to determine the concept, or real-world object, that you are trying to capture within the schema. 識別您嘗試描述的概念後，您就可以開始規劃您的架構，思考資料類型、潛在身分欄位，以及架構在未來可能會如何演變等問題。

### [!DNL Experience Platform]中的資料行為

用於[!DNL Experience Platform]的資料分為兩種行為類型：

* **Record data**: Provides information about the attributes of a subject. A subject could be an organization or an individual.
* **Time series data**: Provides a snapshot of the system at the time an action was taken either directly or indirectly by a record subject.

All XDM schemas describe data that can be categorized as record or time series. 架構的資料行為由架構的類定義，該類在首次建立時分配給架構。 XDM classes are described in further detail later in this document.

記錄和時間序列結構都包含身分圖(`xdm:identityMap`)。 This field contains the identity representation of a subject, drawn from fields marked as &quot;Identity&quot; as described in the next section.

### [!UICONTROL 身分] {#identity}

結構用於將資料內嵌至[!DNL Experience Platform]。 This data can be used across multiple services to create a single, unified view of an individual entity. 因此，思考結構時請務必考量客戶身分，以及可使用哪些欄位來識別主題（無論資料來自何處）。

若要協助進行此程式，您結構中的關鍵欄位可標示為身分。 資料內嵌時，這些欄位中的資料會插入該個人的「[!UICONTROL 身分圖表]」中。 The graph data can then be accessed by [[!DNL Real-time Customer Profile]](../../profile/home.md) and other [!DNL Experience Platform] services to provide a stitched-together view of each individual customer.

通常標示為「[!UICONTROL Identity]」的欄位包括：電子郵件地址、電話號碼、[[!DNL Experience Cloud ID (ECID)]](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=zh-Hant)、CRM ID或其他唯一ID欄位。 您也應考慮組織專屬的任何唯一識別碼，因為這些識別碼可能也是正確的「[!UICONTROL Identity]」欄位。

It is important to think about customer identities during the schema planning phase in order to help ensure that data is being brought together to build the most robust profile possible. 請參閱[Adobe Experience Platform Identity Service](../../identity-service/home.md)的概觀，深入了解身分資訊如何協助您為客戶提供數位體驗。

There are two ways to send identity data to Platform:

1. Adding identity descriptors to individual fields, either through the [Schema Editor UI](../ui/fields/identity.md) or using the [Schema Registry API](../api/descriptors.md#create)
1. Using an [`identityMap` field](#identityMap)

#### `identityMap` {#identityMap}

`identityMap` 是地圖類型欄位，可說明個人的各種身分值及其相關聯的命名空間。此欄位可用來提供結構的身分資訊，而非在結構本身的結構內定義身分值。

使用`identityMap`的主要缺點是身分會嵌入資料中，因此變得不太可見。 If you are ingesting raw data, you should be defining individual identity fields within the actual schema structure instead. Schemas that use `identityMap` also cannot participate in relationships.

However, identity maps can be particularly useful if you are bringing in data from sources that store identities together (such as [!DNL Airship] or Adobe Audience Manager), or when there are a variable number of identities for a schema. 此外，如果您使用[Adobe Experience Platform Mobile SDK](https://aep-sdks.gitbook.io/docs/)，則需要身分對應。

簡單身分對應的範例如下所示：

```json
"identityMap": {
  "email": [
    {
      "id": "jsmith@example.com",
      "primary": false
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
  "loyaltyId": [
    {
      "id": "2e33192000007456-0365c00000000000",
      "primary": true
    }
  ]
}
```

如上例所示，`identityMap`物件中的每個索引鍵代表身分命名空間。 每個索引鍵的值是物件的陣列，代表個別命名空間的身分值(`id`)。 請參閱[!DNL Identity Service]檔案，以取得Adobe應用程式所識別之標準身分命名空間](../../identity-service/troubleshooting-guide.md#standard-namespaces)清單。[

>[!NOTE]
>
>也可以為每個身分值提供一個布林值，用於判斷值是否為主要身份(`primary`)。 Primary identities only need to be set for schemas intended to be used in [!DNL Real-time Customer Profile]. See the section on [union schemas](#union) for more information.

### Schema evolution principles {#evolution}

As the nature of digital experiences continues to evolve, so must the schemas used to represent them. 因此，設計良好的架構能夠視需要調整和演變，而不會對舊版架構造成破壞性變更。

由於維護向後相容性對於架構演化至關重要，[!DNL Experience Platform]強制執行純加性版本設定原則。 This principle ensures that any revisions to the schema only result in non-destructive updates and changes. 換句話說，不支援&#x200B;**中斷變更。**

>[!NOTE]
>
>If a schema has not yet been used to ingest data into [!DNL Experience Platform] and hasn&#39;t been enabled for use in Real-time Customer Profile, you may introduce a breaking change to that schema. 但是，一旦[!DNL Platform]中使用了架構，它必須遵守附加版本設定策略。

下表劃分了編輯結構、欄位群組和資料類型時支援哪些變更：

| Supported changes | Breaking changes (Not supported) |
| --- | --- |
| <ul><li>Adding new fields to the resource</li><li>將必填欄位設為選填</li><li>Changing the resource&#39;s display name and description</li><li>啟用結構以參與設定檔</li></ul> | <ul><li>移除先前定義的欄位</li><li>引入新的必填欄位</li><li>更名或重定義現有欄位</li><li>Removing or restricting previously supported field values</li><li>將現有欄位移動到樹中的不同位置</li><li>刪除架構</li><li>停用架構參與設定檔</li></ul> |

### 結構和資料擷取

In order to ingest data into [!DNL Experience Platform], a dataset must first be created. Datasets are the building blocks for data transformation and tracking for [[!DNL Catalog Service]](../../catalog/home.md), and generally represent tables or files that contain ingested data. 所有資料集皆以現有XDM結構為基礎，所擷取資料應包含的內容及其建構方式受到限制。 如需詳細資訊，請參閱[Adobe Experience Platform資料擷取](../../ingestion/home.md)的概觀。

## 架構的建置區塊

[!DNL Experience Platform] 使用組合方法，結合標準建置區塊以建立結構。此方法促進現有元件的可重用性，並推動整個行業的標準化，以支援[!DNL Platform]中的供應商架構和元件。

結構是使用下列公式組成：

**類+方案欄位組(&amp;A);= XDM結構**

&amp;ast;A schema is composed of a class and zero or more schema field groups. This means that you could compose a dataset schema without using field groups at all.

### 類別 {#class}

Composing a schema begins by assigning a class. 類別會定義結構將包含的資料的行為方面（記錄或時間序列）。 除此之外，類還描述了基於該類的所有結構都需要包含的最小公共屬性數，並為合併多個相容資料集提供了一種方法。

A schema&#39;s class determines which field groups will be eligible for use in that schema. 這在[下一節](#field-group)中有更詳細的討論。

Adobe provides several standard (&quot;core&quot;) XDM classes. 幾乎所有下游Platform程式都需要其中兩個類[!DNL XDM Individual Profile]和[!DNL XDM ExperienceEvent]。 In addition these core classes, you can also create your own custom classes to describe more specific use cases for your organization. 當沒有Adobe定義的核心類可用於描述唯一的使用案例時，自定義類由組織定義。

以下螢幕擷圖示範如何在Platform UI中呈現類別。 Since the example schema shown does not contain any field groups, all of the displayed fields are provided by the schema&#39;s class ([!UICONTROL XDM Individual Profile]).

![](../images/schema-composition/class.png)

For the most up-to-date list of available standard XDM classes, refer to the [official XDM repository](https://github.com/adobe/xdm/tree/master/components/classes). Alternatively, you can refer to the guide on [exploring XDM components](../ui/explore.md) if you prefer to view resources in the UI.

### 欄位組 {#field-group}

欄位群組是可重複使用的元件，定義可實作特定功能（例如個人詳細資訊、酒店偏好設定或地址）的一或多個欄位。 Field groups are intended to be included as part of a schema that implements a compatible class.

欄位群組會根據所代表資料的行為（記錄或時間序列），定義相容的類別。 這表示並非所有欄位組都可用於所有類別。

[!DNL Experience Platform] includes many standard Adobe field groups while also allowing vendors to define field groups for their users, and individual users to define field groups for their own specific concepts.

例如，要為「[!UICONTROL 忠誠會員]」架構捕獲諸如「[!UICONTROL 名字]」和「[!UICONTROL 家庭地址]」等詳細資訊，您可以使用定義這些常見概念的標準欄位組。 However, concepts that are specific to less-common use cases (such as &quot;[!UICONTROL Loyalty Program Level]&quot;) often do not have a pre-defined field group. 在這種情況下，您必須定義自己的欄位群組以擷取此資訊。

請記住，結構由「零個或更多」欄位群組組成，因此這表示您無需使用任何欄位群組即可組成有效的結構。

下列螢幕擷取示範在Platform UI中呈現欄位群組的方式。 在本示例中，將單個欄位組（[!UICONTROL 人口統計詳細資訊]）添加到架構，該架構為架構的結構提供欄位分組。

![](../images/schema-composition/field-group.png)

如需可用標準XDM欄位群組的最新清單，請參閱[官方XDM存放庫](https://github.com/adobe/xdm/tree/master/components/fieldgroups)。 Alternatively, you can refer to the guide on [exploring XDM components](../ui/explore.md) if you prefer to view resources in the UI.

### 資料類型 {#data-type}

資料類型與基本常值欄位的使用方式相同，可作為類別或結構中的參考欄位類型。 主要差異在於資料類型可以定義多個子欄位。 Similar to a field group, a data type allows for the consistent use of a multi-field structure, but has more flexibility than a field group because a data type can be included anywhere in a schema by adding it as the &quot;data type&quot; of a field.

[!DNL Experience Platform] 在中提供了一些常用資料類型，以支 [!DNL Schema Registry] 援使用標準模式來描述常用資料結構。This is explained in more detail in the [!DNL Schema Registry] tutorials, where it will become clearer as you walk through the steps to define data types.

下列螢幕擷圖示範在Platform UI中呈現資料類型的方式。 [!UICONTROL 人口統計詳細資料]欄位組提供的其中一個欄位使用「[!UICONTROL 人員名稱]」資料類型，如欄位名稱旁垂直號字元(`|`)後面的文字所示。 此特定資料類型提供與個人姓名相關的多個子欄位，此結構可重複用於其他需要擷取個人姓名的欄位。

![](../images/schema-composition/data-type.png)

如需可用標準XDM資料類型的最新清單，請參閱[官方XDM存放庫](https://github.com/adobe/xdm/tree/master/components/datatypes)。 Alternatively, you can refer to the guide on [exploring XDM components](../ui/explore.md) if you prefer to view resources in the UI.

### 欄位

欄位是架構最基本的建置區塊。 欄位會定義特定資料類型，以提供與可包含的資料類型相關的限制。 這些基本資料類型定義單一欄位，而先前提到的[資料類型](#data-type)可讓您定義多個子欄位，並在各種結構中重複使用相同的多欄位結構。 So, in addition to defining a field&#39;s &quot;data type&quot; as one of the data types defined in the registry, [!DNL Experience Platform] supports basic scalar types such as:

* 字串
* 整數
* 雙倍
* 布林值
* 陣列
* 物件

>[!TIP]
>
>有關在對象類型欄位上使用自由格式欄位的優缺點，請參閱[附錄](#objects-v-freeform)。

這些標量類型的有效範圍可以進一步限制為特定模式、格式、最小值/最大值或預定值。 Using these constraints, a wide range of more specific field types can be represented, including:

* 列舉
* 長
* 簡短
* 位元組
* Date
* 日期時間
* 地圖

>[!NOTE]
>
>「對應」欄位類型可用於索引鍵/值組資料，包括單一索引鍵的多個值。 地圖只能在系統級別定義，這意味著您可能會遇到行業或供應商定義的結構中的地圖，但它不可用於您定義的欄位。 [Schema Registry API開發者指南](../api/getting-started.md)包含有關定義欄位類型的詳細資訊。

Some data operations used by downstream services and applications enforce constraints on specific field types. 受影響的服務包括但不限於：

* [[!DNL Real-time Customer Profile]](../../profile/home.md)
* [[!DNL Identity Service]](../../identity-service/home.md)
* [[!DNL Segmentation]](../../segmentation/home.md)
* [[!DNL Query Service]](../../query-service/home.md)
* [[!DNL Data Science Workspace]](../../data-science-workspace/home.md)

在建立綱要以用於下游服務之前，請查閱這些服務的相應文檔，以便更好地了解該綱要所用資料操作的欄位要求和限制。

### XDM欄位

除了基本欄位和定義您自己資料類型的功能外，XDM還提供一組標準欄位和資料類型，這些欄位和資料類型隱含地被[!DNL Experience Platform]服務理解，並且在跨[!DNL Platform]元件使用時提供更高的一致性。

這些欄位（例如「名字」和「電子郵件地址」）包含除基本標量欄位類型之外的附加含義，它告訴[!DNL Platform]任何共用相同XDM資料類型的欄位都將以相同方式行事。 This behavior can be trusted to be consistent regardless of where the data is coming from, or in which [!DNL Platform] service the data is being used.

如需可用XDM欄位的完整清單，請參閱[XDM欄位字典](field-dictionary.md)。 建議您盡可能使用XDM欄位和資料類型，以支援[!DNL Experience Platform]之間的一致性和標準化。

## 合成示例

結構代表將擷取至[!DNL Platform]，並使用合成模型建置的資料格式和結構。 As previously mentioned, these schemas are composed of a class and zero or more field groups that are compatible with that class.

例如，描述在零售商店進行的購買的架構可稱為「[!UICONTROL 商店交易]」。 架構實現與標準[!UICONTROL Commerce]欄位組和用戶定義的[!UICONTROL 產品資訊]欄位組組合的[!DNL XDM ExperienceEvent]類。

追蹤網站流量的其他結構可稱為「[!UICONTROL 網站造訪]」。 它也會實作[!DNL XDM ExperienceEvent]類別，但這次會結合標準[!UICONTROL Web]欄位群組。

下圖顯示這些結構以及每個欄位群組貢獻的欄位。 它也包含以[!DNL XDM Individual Profile]類別為基礎的兩個結構，包括本指南中先前提及的「[!UICONTROL 忠誠會員]」結構。

![](../images/schema-composition/composition.png)

### Union {#union}

While [!DNL Experience Platform] allows you to compose schemas for particular use cases, it also allows you to see a &quot;union&quot; of schemas for a specific class type. 上圖顯示以XDM ExperienceEvent類別為基礎的兩個結構，以及以[!DNL XDM Individual Profile]類別為基礎的兩個結構。 The union, shown below, aggregates the fields of all schemas that share the same class ([!DNL XDM ExperienceEvent] and [!DNL XDM Individual Profile], respectively).

![](../images/schema-composition/union.png)

通過啟用架構以與[!DNL Real-time Customer Profile]一起使用，該類型將包含在聯合中。 [!DNL Profile] 提供強大且集中的客戶屬性設定檔，以及客戶在任何與整合的系統中發生之每個事件的時間戳記帳 [!DNL Platform]戶。[!DNL Profile] uses the union view to represent this data and provide a holistic view of each individual customer.

有關使用[!DNL Profile]的詳細資訊，請參閱[即時客戶設定檔概述](../../profile/home.md)。

## Mapping datafiles to XDM schemas

All datafiles that are ingested into [!DNL Experience Platform] must conform to the structure of an XDM schema. For more information on how to format datafiles to comply with XDM hierarchies (including sample files), see the document on [sample ETL transformations](../../etl/transformations.md). 有關將資料檔案內嵌到[!DNL Experience Platform]的一般資訊，請參閱[批次內嵌概述](../../ingestion/batch-ingestion/overview.md)。

## 外部區段的結構

如果要將外部系統的區段帶入Platform，您必須使用下列元件來擷取其結構描述：

* [[!UICONTROL 區段] 定義類別](../classes/segment-definition.md):使用此標準類可捕獲外部段定義的關鍵屬性。
* [[!UICONTROL 區段成員資] 格詳細資料群組](../field-groups/profile/segmentation.md):將此欄位群組新增至您的 [!UICONTROL XDM個別設] 定檔架構，以便將客戶設定檔與特定區段建立關聯。

## 後續步驟

現在您已了解結構構成的基本知識，可以開始使用[!DNL Schema Registry]探索和建立結構。

若要檢閱兩個核心XDM類別及其常用的相容欄位群組的結構，請參閱下列參考檔案：

* [[!DNL XDM Individual Profile]](../classes/individual-profile.md)
* [[!DNL XDM ExperienceEvent]](../classes/experienceevent.md)

The [!DNL Schema Registry] is used to access the [!DNL Schema Library] within Adobe Experience Platform, and provides a user interface and RESTful API from which all available library resources are accessible. The [!DNL Schema Library] contains Industry resources defined by Adobe, Vendor resources defined by [!DNL Experience Platform] partners, and classes, field groups, data types, and schemas that have been composed by members of your organization.

若要開始使用UI合成架構，請遵循[架構編輯器教學課程](../tutorials/create-schema-ui.md)來建置本檔案提及的「忠誠會員」架構。

若要開始使用[!DNL Schema Registry] API，請先閱讀[Schema Registry API開發人員指南](../api/getting-started.md)。 閱讀開發人員指南後，請依照教學課程中概述的步驟，使用Schema Registry API](../tutorials/create-schema-api.md)建立架構。[

## 附錄

以下各節載有關於方案組成原則的補充資訊。

### 關係表與嵌入式對象 {#embedded}

使用關係資料庫時，最佳實務包括標準化資料，或將實體分割為離散片段，然後顯示在多個表格中。 為了整體讀取資料或更新實體，必須使用JOIN對許多單個表執行讀和寫操作。

XDM結構通過嵌入對象的使用，可以直接表示複雜的資料，並將其儲存在具有層次結構的獨立文檔中。 此結構的主要優點之一是，它允許您查詢資料，而無需通過昂貴的連接到多個非正常表來重構實體。 There are no hard restrictions to how many levels your schema hierarchy can be.

### 結構與巨量資料 {#big-data}

現代數位系統會產生大量的行為訊號（交易資料、網頁記錄、物聯網、顯示等）。 This big data offers extraordinary opportunities to optimize experiences, but is challenging to use due to the scale and variety of the data. 為了從資料中獲得價值，其結構、格式和定義必須標準化，以便能夠一致且有效地處理它。

結構允許從多個源整合資料、通過通用結構和定義進行標準化，並跨解決方案共用，從而解決了此問題。 這允許後續的流程和服務回答任何類型的資料問題，從傳統的資料建模方法轉向資料建模方法，即預先知道將要詢問資料的所有問題，並且資料建模以符合這些期望。

### 對象與自由格式欄位 {#objects-v-freeform}

There are some key factors to consider when choosing objects over free-form fields when designing your schemas:

| 物件 | Free-form fields |
| --- | --- |
| 增加嵌套 | 少或無嵌套 |
| 建立邏輯欄位分組 | 欄位會放置在隨選位置 |

{style=&quot;table-layout:auto&quot;}

#### 物件

在自由格式欄位上使用對象的優點和缺點如下。

**優點**:

* 要建立特定欄位的邏輯分組時，最好使用對象。
* 對象以更結構化的方式組織架構。
* Objects indirectly help in creating a good menu structure in the Segment Builder UI. 結構中的分組欄位會直接反映在「區段產生器」UI中提供的資料夾結構中。

**缺點**:

* 欄位會變得更巢狀化。
* 使用[Adobe Experience Platform查詢服務](../../query-service/home.md)時，必須為對象中嵌套的查詢欄位提供較長的參考字串。

#### 自由格式欄位

在物件上使用自由格式欄位的優點和缺點列於下方。

**優點**:

* 自由表單欄位直接建立在架構的根物件(`_tenantId`)下，提高可見性。
* 使用查詢服務時，自由表單欄位的參考字串往往較短。

**缺點**:

* 架構中自由表單欄位的位置是隨選的，這表示這些欄位在架構編輯器中會以字母順序顯示。 這可能會使結構變得不那麼結構化，而類似的自由格式欄位最終可能會根據其名稱而遠隔開來。
