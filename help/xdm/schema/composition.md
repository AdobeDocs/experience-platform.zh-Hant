---
keywords: Experience Platform；主題；熱門主題；架構；模式；枚舉；混合；欄位組；欄位組；混合；資料類型；資料類型；資料類型；資料類型；資料類型；主標識；主標識；XDM個人配置檔案；XDM欄位；枚舉；資料類型；體驗事件；XDM體驗事件；XDM體驗事件；體驗事件；體驗事件；體驗事件；XDMdm ExperienceEvenet；架構設計；類；類；類；類；資料類型；資料類型；資料類型；資料類型；架構；架構；標識映射；標識映射；標識映射；架構設計；映射；聯合架構；聯合架構
solution: Experience Platform
title: 架構組合基礎
description: 本文檔介紹了經驗資料模型(XDM)架構，以及用於組合要在Adobe Experience Platform使用的架構的構成模組、原則和最佳做法。
exl-id: d449eb01-bc60-4f5e-8d6f-ab4617878f7e
source-git-commit: a3f38a18693e0ef4bc93765c090eafd56dcd15d3
workflow-type: tm+mt
source-wordcount: '4140'
ht-degree: 6%

---

# 架構組合的基礎

本文檔介紹 [!DNL Experience Data Model] (XDM)架構以及構成要在Adobe Experience Platform使用的架構的構成模組、原則和最佳做法。 有關XDM及其在中的使用方式的一般資訊 [!DNL Platform]，請參見 [XDM系統概述](../home.md)。

## 瞭解架構

結構是一組規則，可代表及驗證資料的結構和格式。 從高層面來說，結構提供了真實對象 (如人) 的抽象定義，並概述應包含在該對象的每個執行個體中的資料 (如名字、姓氏、生日等)。  

除了描述資料的結構外，模式還對資料應用約束和期望值，以便在系統之間移動時對其進行驗證。 這些標準定義允許對資料進行一致的解釋，而不管其來源如何，並消除跨應用程式進行翻譯的需要。

[!DNL Experience Platform] 使用模式維護此語義規範化。 模式是描述資料的標準方法 [!DNL Experience Platform]，允許符合架構的所有資料在組織中重複使用，而不會發生衝突，甚至在多個組織之間共用。

XDM模式是以自包含格式儲存大量複雜資料的理想選擇。 請參閱 [嵌入對象](#embedded) 和 [大資料](#big-data) 的子文檔。

### 基於架構的工作流 [!DNL Experience Platform]

標準化是其背後的一個關鍵概念 [!DNL Experience Platform]。 XDM由Adobe驅動，旨在標準化客戶體驗資料並定義客戶體驗管理的標準架構。

其基礎架構 [!DNL Experience Platform] 是構建的，稱為 [!DNL XDM System]，方便基於模式的工作流並包括 [!DNL Schema Registry]。 [!DNL Schema Editor]、架構元資料和服務消耗模式。 查看 [XDM系統概述](../home.md) 的子菜單。

利用中的架構有幾個關鍵好處 [!DNL Experience Platform]。 首先，模式允許更好的資料治理和資料最小化，這在隱私法規中尤為重要。 其次，使用Adobe的標準元件構建架構允許開箱即用的洞察力和使用AI/ML服務，而且定制最少。 最後，架構為資料共用提供了深入洞察和高效協調的基礎結構。

## 計畫架構

構建架構的第一步是確定您試圖在架構中捕獲的概念或現實世界對象。 一旦確定了您嘗試描述的概念，您就可以開始規劃您的架構，方法是考慮資料類型、潛在標識欄位以及架構在將來可能如何發展。

### 資料行為 [!DNL Experience Platform]

用於 [!DNL Experience Platform] 分為兩種行為類型：

* **記錄資料**:提供有關主題屬性的資訊。 主題可以是組織或個人。
* **時間序列資料**:提供記錄主題直接或間接執行操作時系統的快照。

所有XDM架構都描述可以分類為記錄或時間序列的資料。 架構的資料行為由架構的類定義，該類在首次建立架構時分配給該架構。 XDM類在本文檔的後面有更詳細的介紹。

記錄和時間序列架構都包含標識映射(`xdm:identityMap`)。 此欄位包含主題的標識表示，它取自標為「標識」的欄位，如下一節所述。

### [!UICONTROL 身分] {#identity}

>[!CONTEXTUALHELP]
>id="platform_schemas_identities"
>title="方案中的身分"
>abstract="身分是方案中的重要欄位，可用於識別主題，例如電子郵件地址或行銷 ID。這些欄位用於為每個人建構身分識別圖並建立客戶設定檔。如需進一步了解方案中的身分，請查看此文件。"

架構用於將資料插入 [!DNL Experience Platform]。 此資料可以跨多個服務使用，以建立單個實體的單個統一視圖。 因此，在考慮架構時，必須考慮客戶身份以及哪些欄位可用於標識主題，而不管資料可能來自何處。

要幫助處理此過程，可以將架構中的關鍵欄位標籤為標識。 在資料接收時，這些欄位中的資料將插入到「 」[!UICONTROL 標識圖]為那個人。 然後，可以通過 [[!DNL Real-Time Customer Profile]](../../profile/home.md) 其他 [!DNL Experience Platform] 提供每個客戶的縫合視圖。

通常標籤為「」的欄位[!UICONTROL 身份]「包括：電子郵件地址，電話號碼， [[!DNL Experience Cloud ID (ECID)]](https://experienceleague.adobe.com/docs/id-service/using/home.html)、CRM ID或其他唯一ID欄位。 您還應考慮組織特有的任何唯一標識符，因為它們可能是好的&quot;[!UICONTROL 身份]」對話框。

在架構規劃階段考慮客戶身份非常重要，以幫助確保將資料匯集到一起，以構建盡可能最強健的配置檔案。 請參閱 [Adobe Experience Platform身份服務](../../identity-service/home.md) 瞭解有關身份資訊如何幫助您向客戶提供數字型驗的更多資訊。

將身份資料發送到平台有兩種方法：

1. 通過 [架構編輯器UI](../ui/fields/identity.md) 或使用 [架構註冊表API](../api/descriptors.md#create)
1. 使用 [`identityMap` 場](#identityMap)

#### `identityMap` {#identityMap}

`identityMap` 是映射類型欄位，它描述單個標識值及其關聯的命名空間。 此欄位可用於提供方案的標識資訊，而不是在方案本身的結構中定義標識值。

使用的主要缺點 `identityMap` 身份會被嵌入資料中，因此變得不那麼可見。 如果正在接收原始資料，則應改為在實際架構結構中定義單個標識欄位。

>[!NOTE]
>
>使用 `identityMap` 可以用作關係中的源架構，但不能用作引用架構。 這是因為所有引用架構都必須具有可在源架構的引用欄位中映射的可見標識。 請參閱上的UI指南 [關係](../tutorials/relationship-ui.md) 的子菜單。

但是，如果您將儲存身份的源中的資料(如 [!DNL Airship] 或Adobe Audience Manager)，或當架構的標識數可變時。 此外，如果使用 [Adobe Experience Platform移動SDK](https://aep-sdks.gitbook.io/docs/)。

簡單標識映射的示例如下所示：

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

如上例所示， `identityMap` 對象表示標識命名空間。 每個鍵的值是對象陣列，表示標識值(`id`)。 請參閱 [!DNL Identity Service] 文檔 [標準標識命名空間清單](../../identity-service/troubleshooting-guide.md#standard-namespaces) 由Adobe應用程式識別。

>[!NOTE]
>
>用於該值是否是主標識(`primary`)也可為每個標識值提供。 只需為要用於的架構設定主標識 [!DNL Real-Time Customer Profile]。 請參閱 [聯合模式](#union) 的子菜單。

### 圖式演化原則 {#evolution}

隨著數字型驗的性質不斷演變，用來表示數字型驗的模式也必須不斷演變。 因此，設計良好的架構能夠根據需要調整和演化，而不會對架構的早期版本造成破壞性更改。

由於保持向後相容性對架構演化至關重要， [!DNL Experience Platform] 強制實施純附加版本化原則。 此原則確保對架構的任何修訂只會導致非破壞性更新和更改。 換句話說， **不支援斷開更改。**

>[!NOTE]
>
>如果尚未使用架構將資料插入 [!DNL Experience Platform] 並且尚未啟用在即時客戶配置檔案中使用，您可能會對該架構引入突破性的更改。 但是，一旦將架構用於 [!DNL Platform]，它必須遵守附加版本化策略。

下表分析了編輯方案、欄位組和資料類型時支援哪些更改：

| 支援的更改 | 斷開更改（不支援） |
| --- | --- |
| <ul><li>向資源添加新欄位</li><li>使必填欄位為可選欄位</li><li>介紹新的必填欄位*</li><li>更改資源的顯示名稱和說明</li><li>啟用架構參與配置檔案</li></ul> | <ul><li>刪除以前定義的欄位</li><li>更名或重定義現有欄位</li><li>刪除或限制以前支援的欄位值</li><li>將現有欄位移動到樹中的其他位置</li><li>刪除架構</li><li>禁用架構以阻止其參與配置檔案</li></ul> |

\**請參閱下節，瞭解有關 [設定新必填欄位](#post-ingestion-required-fields)。*

### 必填欄位

單個架構欄位可以是 [標籤為必需](../ui/fields/required.md)，這意味著任何所攝取的記錄都必須包含這些欄位中的資料，才能通過驗證。 例如，根據需要設定架構的主要標識欄位有助於確保所有攝取的記錄都將參與即時客戶配置檔案，同時根據需要設定時間戳欄位可確保按時間順序保留所有時間序列事件。

>[!IMPORTANT]
>
>無論是否需要架構欄位，平台都不接受 `null` 或任何已接收欄位的空值。 如果記錄或事件中沒有特定欄位的值，則應將該欄位的鍵從接收負載中排除。

#### 設定接收後所需的欄位 {#post-ingestion-required-fields}

如果某個欄位已用於接收資料且最初未根據需要設定，則該欄位可能對某些記錄具有空值。 如果將此欄位設定為必需的接收後記錄，則所有將來記錄都必須包含此欄位的值，即使歷史記錄可能為空。

在根據需要設定以前可選的欄位時，請牢記以下事項：

1. 如果查詢歷史資料並將結果寫入新資料集，則某些行將失敗，因為它們包含所需欄位的空值。
1. 如果欄位參與 [即時客戶配置檔案](../../profile/home.md) 並且在根據需要設定資料之前導出資料，對於某些配置檔案，它可能為空。
1. 可以使用架構註冊表API查看平台中所有XDM資源的時間戳更改日誌，包括新的必需欄位。 請參閱 [審計日誌終結點](../api/audit-log.md) 的子菜單。

### 架構和資料接收

為了將資料 [!DNL Experience Platform]，必須先建立資料集。 資料集是資料轉換和跟蹤的構建基塊 [[!DNL Catalog Service]](../../catalog/home.md)，並通常表示包含所接收資料的表或檔案。 所有資料集都基於現有的XDM架構，這些架構為所攝取的資料應包含的內容以及資料的結構提供約束。 請參閱 [Adobe Experience Platform資料接收](../../ingestion/home.md) 的子菜單。

## 架構的構建塊

[!DNL Experience Platform] 使用組合方法，其中組合標準構建塊以建立模式。 此方法促進現有元件的可重用性，並推動整個行業的標準化，以支援供應商模式和元件 [!DNL Platform]。

方案使用以下公式組成：

**類+架構欄位組(&amp;A);= XDM架構**

&amp;ast；架構由類和零個或多個架構欄位組組成。 這意味著您無需使用欄位組即可合成資料集架構。

### 類別 {#class}

>[!CONTEXTUALHELP]
>id="platform_schemas_class"
>title="類別"
>abstract="每個方案都以單一類別為基礎。類別定義了方案的行為，以及做為所有方案的基礎且類別必須包含的通用屬性。如需深入了解類別如何參與方案的組成，請查看此文件。"

合成架構的開始是分配類。 類定義模式將包含的資料的行為方面（記錄或時間序列）。 此外，類還描述了基於該類的所有方案需要包括的最小數量的公共屬性，並為合併多個相容資料集提供了一種方法。

架構的類確定哪些欄位組有資格在該架構中使用。 在 [下一部分](#field-group)。

Adobe提供多個標準（「核心」）XDM類。 其中兩門課， [!DNL XDM Individual Profile] 和 [!DNL XDM ExperienceEvent]，是幾乎所有下游平台進程所必需的。 除了這些核心類之外，您還可以建立自己的自定義類，以說明組織的更具體的使用案例。 當沒有Adobe定義的核心類可用於描述唯一的使用情形時，自定義類由組織定義。

以下螢幕快照演示了如何在平台UI中表示類。 由於所示示例架構不包含任何欄位組，所以所有顯示的欄位都由架構的類([!UICONTROL XDM個人配置檔案])。

![](../images/schema-composition/class.png)

有關可用標準XDM類的最新清單，請參閱 [正式XDM儲存庫](https://github.com/adobe/xdm/tree/master/components/classes)。 或者，可參閱上的指南 [探索XDM元件](../ui/explore.md) 的子菜單。

### 欄位群組 {#field-group}

>[!CONTEXTUALHELP]
>id="platform_schemas_fieldgroup"
>title="欄位群組"
>abstract="欄位群組是可重複使用的元件，可讓您使用額外屬性擴充方案。大部分欄位群組僅與部分類別相容。您可以使用 Adobe 定義的標準欄位群組，或是手動定義您自己的自訂欄位群組。如需深入了解欄位群組如何參與方案的組成，請查看此文件。"

>[!CONTEXTUALHELP]
>id="platform_schemas_fieldgroup_requiredFieldgroup"
>title="必要欄位群組"
>abstract="您所使用的來源需要此欄位群組。因此，您無法將其從方案中刪除。"

欄位組是可重用的元件，它定義了一個或多個欄位，這些欄位實現了某些功能，如個人詳細資訊、酒店首選項或地址。 欄位組將作為實現相容類的架構的一部分被包括。

欄位組根據它們所代表的資料的行為（記錄或時間序列）定義它們與哪些類相容。 這意味著並非所有欄位組都可用於所有類。

[!DNL Experience Platform] 包括許多標準Adobe欄位組，同時允許供應商為其用戶定義欄位組，並允許單個用戶為其特定概念定義欄位組。

例如，要捕獲詳細資訊，如「」[!UICONTROL 名字]&quot;和&quot;[!UICONTROL 家庭地址]&quot;[!UICONTROL 會員]&quot;架構，您可以使用定義這些通用概念的標準欄位組。 但是，標準欄位組可能未涵蓋的更特定於您的組織的概念（如自定義會員計畫詳細資訊或產品屬性）。 在這種情況下，必須定義自己的欄位組才能捕獲此資訊。

>[!NOTE]
>
>強烈建議在方案中盡可能使用標準欄位組，因為這些欄位由 [!DNL Experience Platform] 提供更高的一致性 [!DNL Platform] 元件。
>
>標準元件（如「名字」和「電子郵件地址」）提供的欄位包含除基本標量欄位類型之外的附加含義，說明 [!DNL Platform] 共用相同資料類型的任何欄位將以相同方式運行。 無論資料來自何處，或資料來自何處，都可以信任此行為保持一致 [!DNL Platform] 為正在使用的資料提供服務。

請記住，架構由「零個或更多」欄位組組成，因此這意味著您無需使用任何欄位組即可組成有效架構。

以下螢幕快照演示了如何在平台UI中表示欄位組。 單個欄位組([!UICONTROL 人口結構詳細資訊])添加到此示例中的架構中，該架構為架構的結構提供欄位分組。

![](../images/schema-composition/field-group.png)

有關可用標準XDM欄位組的最新清單，請參閱 [正式XDM儲存庫](https://github.com/adobe/xdm/tree/master/components/fieldgroups)。 或者，可參閱上的指南 [探索XDM元件](../ui/explore.md) 的子菜單。

### 資料類型 {#data-type}

資料類型與基本文本欄位的使用方式相同，在類或方案中用作引用欄位類型。 關鍵區別在於資料類型可以定義多個子欄位。 它們可以以與欄位組相同的方式定義多個子欄位，但關鍵區別在於，通過將資料類型添加為欄位的「資料類型」，可以將資料類型包括在架構中的任何位置。 雖然欄位組僅與某些類相容，但資料類型可以包括在任何父類或欄位組中。

[!DNL Experience Platform] 提供了許多常用資料類型作為 [!DNL Schema Registry] 支援使用標準模式來描述常用資料結構。 在 [!DNL Schema Registry] 教程，在定義資料類型的步驟中將會更清晰。

以下螢幕快照演示了在平台UI中如何表示資料類型。 提供的欄位之一 [!UICONTROL 人口結構詳細資訊] 欄位組使用&quot;[!UICONTROL 對象]&quot;資料類型，如管道字元後面的文本所示(`|`)。 此特定資料類型提供了幾個與個人姓名相關的子欄位，此構造可重新用於需要捕獲個人姓名的其他欄位。

![](../images/schema-composition/data-type.png)

有關可用標準XDM資料類型的最新清單，請參閱 [正式XDM儲存庫](https://github.com/adobe/xdm/tree/master/components/datatypes)。 或者，可參閱上的指南 [探索XDM元件](../ui/explore.md) 的子菜單。

### 欄位

欄位是架構的最基本構建塊。 欄位提供了通過定義特定資料類型可以包含的資料類型的約束。 這些基本資料類型定義一個欄位，而 [資料類型](#data-type) 前面提到的允許您定義多個子欄位，並在各種架構中重新使用相同的多欄位結構。 因此，除了將欄位的「資料類型」定義為註冊表中定義的資料類型之一外， [!DNL Experience Platform] 支援基本標量類型，如：

* 字串
* 整數
* 雙倍
* 布林值
* 陣列
* 物件

>[!TIP]
>
>查看 [附錄](#objects-v-freeform) 有關在對象類型欄位上使用自由格式欄位的利弊的資訊。

這些標量類型的有效範圍可以進一步限制為某些模式、格式、最小值/最大值或預定義值。 使用這些約束，可以表示範圍更廣的更具體的欄位類型，包括：

* 枚舉
* 龍
* 短
* 位元組
* 日期
* 日期時間
* 地圖

>[!NOTE]
>
>「map」欄位類型允許鍵值對資料，包括單個鍵的多個值。 在標準XDM類和欄位組中可以找到映射，但您也可以使用架構註冊表API定義自定義映射。 請參閱上的教程 [定義自定義欄位](../tutorials/custom-fields-api.md#custom-maps) 的子菜單。

## 合成示例

架構表示將要接收到的資料的格式和結構 [!DNL Platform]，並使用合成模型構建。 如前所述，這些架構由類和與該類相容的零個或多個欄位組組成。

例如，描述在零售商店進行的採購的架構可能稱為「」[!UICONTROL 儲存事務]。 架構實現 [!DNL XDM ExperienceEvent] 類與標準組合 [!UICONTROL 商業] 欄位組和用戶定義的 [!UICONTROL 產品資訊] 欄位組。

另一個跟蹤網站通信的架構可能稱為「」[!UICONTROL Web訪問]。 它還實現 [!DNL XDM ExperienceEvent] 但這次將標準 [!UICONTROL Web] 欄位組。

下圖顯示了這些方案以及每個欄位組貢獻的欄位。 它還包含兩個基於 [!DNL XDM Individual Profile] 類，包括&quot;[!UICONTROL 會員]&quot;本指南中前面提到的架構。

![](../images/schema-composition/composition.png)

### Union {#union}

同時 [!DNL Experience Platform] 允許您為特定使用案例編寫架構，還允許您查看特定類類型的架構的「聯合」。 上圖顯示了基於XDM ExperienceEvent類的兩個模式和基於 [!DNL XDM Individual Profile] 類。 如下所示，聯合聚合共用同一類的所有架構的欄位([!DNL XDM ExperienceEvent] 和 [!DNL XDM Individual Profile])。

![](../images/schema-composition/union.png)

通過啟用模式以與 [!DNL Real-Time Customer Profile]，它將包含在該類型的聯合中。 [!DNL Profile] 提供了客戶屬性的強健、集中的配置檔案以及客戶在與整合的任何系統中發生的每個事件的時間戳記錄 [!DNL Platform]。 [!DNL Profile] 使用聯合視圖來表示此資料並提供每個客戶的整體視圖。

有關使用的詳細資訊 [!DNL Profile]，請參見 [即時客戶概要資訊概述](../../profile/home.md)。

## 將資料檔案映射到XDM架構

所有正被攝取到的資料檔案 [!DNL Experience Platform] 必須符合XDM架構的結構。 有關如何格式化資料檔案以符合XDM層次結構（包括示例檔案）的詳細資訊，請參閱上的文檔 [示例ETL轉換](../../etl/transformations.md)。 有關將資料檔案插入的一般資訊 [!DNL Experience Platform]，請參見 [批處理接收概述](../../ingestion/batch-ingestion/overview.md)。

## 外部段的架構

如果要將外部系統的段引入平台，則必須使用以下元件在架構中捕獲它們：

* [[!UICONTROL 段定義] 類](../classes/segment-definition.md):使用此標準類可捕獲外部段定義的關鍵屬性。
* [[!UICONTROL 段成員身份詳細資訊] 欄位組](../field-groups/profile/segmentation.md):將此欄位組添加到 [!UICONTROL XDM個人配置檔案] 模式，以將客戶配置檔案與特定段關聯。

## 後續步驟

現在，您已經瞭解了架構組合的基礎知識，可以開始使用 [!DNL Schema Registry]。

要查看兩個核心XDM類及其常用相容欄位組的結構，請參閱以下參考文檔：

* [[!DNL XDM Individual Profile]](../classes/individual-profile.md)
* [[!DNL XDM ExperienceEvent]](../classes/experienceevent.md)

的 [!DNL Schema Registry] 用於訪問 [!DNL Schema Library] 提供用戶介面和REST風格的API，可從中訪問所有可用的庫資源。 的 [!DNL Schema Library] 包含由Adobe定義的行業資源，由 [!DNL Experience Platform] 合作夥伴、類、欄位組、資料類型和由組織成員組成的架構。

要開始使用UI合成架構，請與 [架構編輯器教程](../tutorials/create-schema-ui.md) 構建本文檔中提到的「會員」架構。

開始使用 [!DNL Schema Registry] API，從讀取 [架構註冊API開發人員指南](../api/getting-started.md)。 閱讀開發人員指南後，請按照上面的教程中介紹的步驟操作 [使用架構註冊表API建立架構](../tutorials/create-schema-api.md)。

## 附錄

以下各節包含有關架構組成原則的其他資訊。

### 關係表與嵌入式對象 {#embedded}

在使用關係資料庫時，最佳做法涉及標準化資料，或將實體分割成離散的部分，然後在多個表中顯示。 為了將資料作為一個整體讀取或更新實體，必須使用JOIN在多個單獨的表中進行讀和寫操作。

XDM模式通過嵌入對象的使用，可以直接表示複雜資料並儲存在具有層次結構的自包含文檔中。 此結構的一個主要優點是，它允許您查詢資料，而不必通過與多個非正常表的昂貴連接來重建實體。 您的架構層次結構可以包含多少個級別沒有硬性限制。

### 架構和大資料 {#big-data}

現代數字系統產生大量的行為信號（交易資料、網路日誌、物聯網、顯示等）。 這些大資料為優化體驗提供了非凡的機會，但由於資料的規模和多樣性，使用這些大資料具有挑戰性。 為了從資料中獲取價值，必須對其結構、格式和定義進行標準化，以便能夠一致和高效地對其進行處理。

方案通過允許從多個源整合資料、通過通用結構和定義標準化資料並跨解決方案共用資料來解決此問題。 這允許後續過程和服務回答任何類型的資料問題，而不再採用傳統的資料建模方法，即預先知道所有資料問題，並對資料建模以符合這些期望。

### 對象與自由格式欄位 {#objects-v-freeform}

在設計方案時，在自由格式欄位上選擇對象時，需要考慮一些關鍵因素：

| 物件 | 自由格式欄位 |
| --- | --- |
| 增加嵌套 | 少或無嵌套 |
| 建立邏輯欄位分組 | 欄位放置在即席位置 |

{style="table-layout:auto"}

#### 物件

下面列出了在自由格式欄位上使用對象的利弊。

**優點**:

* 當要建立特定欄位的邏輯分組時，最好使用對象。
* 對象以更結構化的方式組織架構。
* 對象間接有助於在段生成器UI中建立良好的菜單結構。 架構中的分組欄位直接反映在段生成器UI中提供的資料夾結構中。

**缺點**:

* 欄位變得更嵌套。
* 使用時 [Adobe Experience Platform查詢服務](../../query-service/home.md)，必須為查詢嵌套在對象中的欄位提供較長的引用字串。

#### 自由格式欄位

下面列出了在對象上使用自由格式欄位的利弊。

**優點**:

* 自由格式欄位直接在架構的根對象(`_tenantId`)，提高可見度。
* 使用查詢服務時，自由表單域的引用字串往往較短。

**缺點**:

* 架構中自由格式欄位的位置是即席的，這意味著它們按字母順序顯示在架構編輯器中。 這會使架構的結構化程度降低，並且類似的自由格式欄位最終可能會根據名稱被分開很遠。
