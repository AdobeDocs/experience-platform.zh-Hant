---
keywords: Experience Platform；首頁；熱門主題；XDM;XDM系統；XDM個別設定檔；XDM ExperienceEvent;XDM體驗事件；experienceEvent;XDM體驗事件；XDM ExperienceEvent；體驗資料模型；體驗資料模型；資料模型；結構；疑難排解；FAQ；聯合結構檔案；聯合設定檔；http://ns.adobe.com/aep/errors/XDM-1010-404;http://ns.adobe.com/aep/errors/XDM-1011-404;http://ns.adobe.com/aep/errors/XDM-1012-404;http://ns.adobe.com/aep/errors/XDM-1013-404;http://ns.adobe.com/aep/errors/XDM-1014-404;http://ns.adobe.com/aep/errors/XDM-1015-404;http://ns.adobe.com/aep/errors/XDM-1016-404;http://ns.adobe.com/aep/errors/XDM-1017-404;http://ns.adobe.com/aep/errors/XDM-1521-400;http://ns.adobe.com/aep/errors/XDM-1020-400;http://ns.adobe.com/aep/errors/XDM-1021-400;http://ns.adobe.com/aep/errors/XDM-1022-400;http://ns.adobe.com/aep/errors/XDM-1023-400;http://ns.adobe.com/aep/errors/XDM-1024-400;http://ns.adobe.com/aep/errors/XDM-1006-400;http://ns.adobe.com/aep/errors/XDM-1007-400;http://ns.adobe.com/aep/errors/XDM-1008-400;http://ns.adobe.com/aep/errors/XDM-1009-400;http://ns.adobe.com/aep/errors/XDM-1526-400;http://ns.adobe.com/aep/errors/XDM-1527-400;http://ns.adobe.com/aep/errors/XDM-1528-400
solution: Experience Platform
title: XDM系統疑難排解指南
description: 尋找Experience Data Model(XDM)常見問題的解答，包括解決常見API錯誤的步驟。
topic-legacy: troubleshooting
exl-id: a0c7c661-bee8-4f66-ad5c-f669c52c9de3
source-git-commit: 415938f6f3aeec342774b73d1ae5f2dc0e27349c
workflow-type: tm+mt
source-wordcount: '1898'
ht-degree: 0%

---

# XDM系統疑難排解指南

本檔案提供Adobe Experience Platform中[!DNL Experience Data Model](XDM)和XDM系統常見問題的解答，包括常見錯誤的疑難排解指南。 如需其他Platform服務的相關問題和疑難排解，請參閱[Experience Platform疑難排解指南](../landing/troubleshooting.md)。

**[!DNL Experience Data Model](XDM)** 是開放原始碼規格，可定義客戶體驗管理的標準化結構。建立[!DNL Experience Platform]的方法&#x200B;**XDM系統**&#x200B;操作[!DNL Experience Data Model]架構，供[!DNL Platform]服務使用。 **[!DNL Schema Registry]**&#x200B;提供用戶介面和RESTful API，用於訪問[!DNL Experience Platform]內的&#x200B;**[!DNL Schema Library]**。 如需詳細資訊，請參閱[XDM檔案](home.md)。

## 常見問題集

以下是有關XDM系統和[!DNL Schema Registry] API使用的常見問題解答清單。

### 如何將欄位新增至結構？

您可以使用架構欄位群組，將欄位新增至架構。 每個欄位組都與一個或多個類相容，允許在實現其中一個相容類的任何架構中使用該欄位組。 雖然Adobe Experience Platform提供數個產業欄位群組及其預先定義的欄位，但您可以使用API或使用者介面建立自訂欄位群組，將自己的欄位新增至結構。

有關在[!DNL Schema Registry] API中建立欄位組的詳細資訊，請參閱[欄位組終結點指南](api/field-groups.md#create)。 如果您使用UI，請參閱[結構編輯器教學課程](./tutorials/create-schema-ui.md)。

### 欄位群組與資料類型的最佳用途為何？

[欄位](./schema/composition.md#field-group) 群組是定義架構中一或多個欄位的元件。欄位群組強制其欄位在架構階層中的顯示方式，因此在每個架構中呈現的結構都與其所包含的相同。 欄位組僅與特定類相容，由其`meta:intendedToExtend`屬性標識。

[資](./schema/composition.md#data-type) 料類型也可為結構提供一或多個欄位。不過，與欄位群組不同，資料類型不會限制在特定類別。 這樣，資料類型就可更靈活地描述可跨具有潛在不同類別的多個架構重複使用的通用資料結構。

### 結構的唯一ID為何？

所有[!DNL Schema Registry]資源（結構、欄位組、資料類型、類）都有一個URI，它充當唯一ID，以供參考和查閱之用。 在API中檢視結構時，可在頂層`$id`和`meta:altId`屬性中找到。

如需詳細資訊，請參閱[!DNL Schema Registry] API指南中的[資源識別](api/getting-started.md#resource-identification)一節。

### 架構何時開始防止中斷變更？

只要尚未在建立資料集時使用或在[[!DNL Real-time Customer Profile]](../profile/home.md)中啟用，架構就可以進行中斷變更。 在資料集建立中使用架構或啟用[!DNL Real-time Customer Profile]後，系統就會嚴格執行[架構演化](schema/composition.md#evolution)的規則。

### 長欄位類型的最大大小是多少？

長欄位類型是一個最大大小為53(+1)位的整數，給它一個介於 — 9007199254740992和9007199254740992之間的位範圍。 這是由於JSON的JavaScript實作如何呈現長整數受到限制。

有關欄位類型的詳細資訊，請參閱[XDM欄位類型約束](./schema/field-constraints.md)的文檔。

### 如何定義結構的身分？

在[!DNL Experience Platform]中，無論解釋的資料來源為何，身分都用於識別主體（通常是個別人）。 在結構中，會將索引鍵欄位標示為「身分」，以定義這些欄位。 身分識別常用的欄位包括電子郵件地址、電話號碼、[[!DNL Experience Cloud ID (ECID)]](https://experienceleague.adobe.com/docs/id-service/using/home.html)、CRM ID和其他唯一ID欄位。

欄位可使用API或使用者介面標示為身分。

#### 在API中定義身分

在API中，身分識別是透過建立身分描述元來建立。 身份描述符發出信號，表示模式的特定屬性是唯一標識符。

身份描述符由POST請求建立到/descriptors端點。 如果成功，您將收到HTTP狀態201（已建立）和包含新描述符詳細資訊的響應對象。

如需在API中建立身分描述元的詳細資訊，請參閱[!DNL Schema Registry]開發人員指南中[描述元](api/descriptors.md)一節的相關檔案。

#### 在UI中定義身分

在架構編輯器中開啟架構後，在要標籤為身分的編輯器的&#x200B;**[!UICONTROL Structure]**&#x200B;區段中選取欄位。 在右側的&#x200B;**[!UICONTROL 欄位屬性]**&#x200B;下，選中&#x200B;**[!UICONTROL Identity]**&#x200B;複選框。

如需在UI中管理身分的詳細資訊，請參閱結構編輯器教學課程中[定義身分欄位](./tutorials/create-schema-ui.md#identity-field)區段的區段。

### 我的架構是否需要主要身分識別？

主要身分為選用，因為結構可能為零或其中一個。 但是，架構必須具有主標識，才能在[!DNL Real-time Customer Profile]中啟用該架構。 如需詳細資訊，請參閱結構編輯器教學課程的[identity](./tutorials/create-schema-ui.md#identity-field)區段。

### 如何在[!DNL Real-time Customer Profile]中啟用架構？

在架構的`meta:immutableTags`屬性內新增「union」標籤，以便在[[!DNL Real-time Customer Profile]](../profile/home.md)中使用架構。 可使用API或使用者介面來啟用架構以與[!DNL Profile]搭配使用。

#### 使用API為[!DNL Profile]啟用現有架構

發出PATCH請求以更新架構，並將`meta:immutableTags`屬性新增為包含「union」值的陣列。 如果更新成功，回應會顯示更新的架構，其現在包含union標籤。

有關使用API啟用架構以在[!DNL Real-time Customer Profile]中使用的詳細資訊，請參閱[!DNL Schema Registry]開發人員指南的[union](./api/unions.md)檔案。

#### 使用UI為[!DNL Profile]啟用現有架構

在[!DNL Experience Platform]中，選擇左側導航中的&#x200B;**[!UICONTROL 方案]**，然後從方案清單中選擇要啟用的方案的名稱。 然後，在編輯器的右側，在&#x200B;**[!UICONTROL Schema Properties]**&#x200B;下，選擇&#x200B;**[!UICONTROL Profile]**&#x200B;以將其開啟。


如需詳細資訊，請參閱[!UICONTROL 結構編輯器]教學課程中「即時客戶設定檔」](./tutorials/create-schema-ui.md#profile)中的[使用一節。

### 我可以直接編輯聯合結構嗎？

聯合結構是唯讀的，由系統自動產生。 無法直接編輯。 當實作該類的架構中新增「union」標籤時，會為特定類別建立union結構。

如需XDM中聯合的詳細資訊，請參閱[!DNL Schema Registry] API指南中的[聯合](./api/unions.md)一節。

### 如何將資料檔案格式化以將資料內嵌到架構中？

[!DNL Experience Platform] 接受或JSON格 [!DNL Parquet] 式的資料檔案。這些檔案的內容必須符合資料集參考的結構。 如需資料檔案內嵌最佳實務的詳細資訊，請參閱[批次內嵌概述](../ingestion/home.md)。

## 錯誤和疑難排解

以下是使用[!DNL Schema Registry] API時可能遇到的錯誤訊息清單。

### 未找到資源

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1010-404",
    "title": "Resource not found",
    "status": 404,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "The requested class resource https://ns.adobe.com/{TENANT_ID}/classes/11447bb484d4599d2cd9b0aseefff78b463cbbde1527f498 with version 1 is not found.",
        "sub-errors": []
    },
    "detail": "The requested class resource https://ns.adobe.com/{TENANT_ID}/classes/11447bb484d4599d2cd9b0aseefff78b463cbbde1527f498 with version 1 is not found."
}
```

當系統找不到特定資源時，將顯示此錯誤。 資源可能已刪除，或API呼叫中的路徑無效。 請確定您已輸入API呼叫的有效路徑，然後再次嘗試。 您可能想要檢查是否已為資源輸入正確的ID，以及路徑是否與適當的容器（全域或租用戶）以適當的命名空間命名。

>[!NOTE]
>
>根據要檢索的資源類型，此錯誤可以使用以下任何`type` URI:
>
>* `http://ns.adobe.com/aep/errors/XDM-1010-404`
>* `http://ns.adobe.com/aep/errors/XDM-1011-404`
>* `http://ns.adobe.com/aep/errors/XDM-1012-404`
>* `http://ns.adobe.com/aep/errors/XDM-1013-404`
>* `http://ns.adobe.com/aep/errors/XDM-1014-404`
>* `http://ns.adobe.com/aep/errors/XDM-1015-404`
>* `http://ns.adobe.com/aep/errors/XDM-1016-404`
>* `http://ns.adobe.com/aep/errors/XDM-1017-404`


如需在API中建構查閱路徑的詳細資訊，請參閱[!DNL Schema Registry]開發人員指南中的[container](./api/getting-started.md#container)和[資源識別](api/getting-started.md#resource-identification)區段。

### 標題不唯一

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1521-400",
    "title": "Title not unique",
    "status": 400,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "Object titles must be unique. An object https://ns.adobe.com/{TENANT_ID}/classes/11447bb484d4599d2cd9b0aseefff78b463cbbde1527f498 already exists with the same title",
        "sub-errors": []
    },
    "detail": "Object titles must be unique. An object https://ns.adobe.com/{TENANT_ID}/classes/11447bb484d4599d2cd9b0aseefff78b463cbbde1527f498 already exists with the same title"
}
```

當您嘗試建立標題已被其他資源使用的資源時，會顯示此錯誤訊息。 所有資源類型的標題必須是唯一的。 例如，如果您嘗試建立標題已由架構使用的欄位群組，則會收到此錯誤。

### 命名空間驗證錯誤

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1021-400",
    "title": "Namespace validation error",
    "status": 400,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "A custom field is defined under an invalid namespace. All custom fields must be defined under a top-level field named {TENANT_ID}.",
        "sub-errors": []
    },
    "detail": "A custom field is defined under an invalid namespace. All custom fields must be defined under a top-level field named {TENANT_ID}."
}
```

當您嘗試建立命名空間不正確的欄位的資源，或將命名空間不正確的欄位新增至現有資源時，會顯示此錯誤訊息。

由您的IMS組織定義的資源必須命名您的租用戶ID下的欄位，以避免與其他產業和廠商資源產生衝突。 使用標準欄位群組建立架構時，您在這些欄位群組結構中新增的任何自訂欄位，也必須以租用戶ID命名。

>[!NOTE]
>
>根據命名空間錯誤的特定性質，此錯誤可以使用以下任何`type` URI以及不同的消息詳細資訊：
>
>* `http://ns.adobe.com/aep/errors/XDM-1020-400`
>* `http://ns.adobe.com/aep/errors/XDM-1021-400`
>* `http://ns.adobe.com/aep/errors/XDM-1022-400`
>* `http://ns.adobe.com/aep/errors/XDM-1023-400`
>* `http://ns.adobe.com/aep/errors/XDM-1024-400`


如需XDM資源適當資料結構的詳細範例，請參閱Schema Registry API指南：

* [建立自訂類別](./api/classes.md#create)
* [建立自訂欄位群組](./api/field-groups.md#create)
* [建立自訂資料類型](./api/data-types.md#create)

### 接受標頭無效

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1006-400",
    "title": "Accept header invalid",
    "status": 400,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "The supplied Accept header is not valid: application/vnd.adobe.xed+json;version=1 - A valid Accept value should look like application/vnd.adobe.{xed|xdm}+json",
        "sub-errors": []
    },
    "detail": "The supplied Accept header is not valid: application/vnd.adobe.xed+json;version=1 - A valid Accept value should look like application/vnd.adobe.{xed|xdm}+json"
}
```

[!DNL Schema Registry] API中的GET請求需要`Accept`標題，以便系統判斷回應的格式。 當所需的`Accept`標題無效或遺失時，即會發生此錯誤。

根據您使用的端點，`detailed-message`屬性指示有效的`Accept`標題在成功回應時應該是什麼樣子。 請確定您已正確輸入與您嘗試進行之API請求相容的`Accept`標題，然後再次嘗試。

>[!NOTE]
>
>根據使用的端點，此錯誤可以使用以下任何`type` URI:
>
>* `http://ns.adobe.com/aep/errors/XDM-1006-400`
>* `http://ns.adobe.com/aep/errors/XDM-1007-400`
>* `http://ns.adobe.com/aep/errors/XDM-1008-400`
>* `http://ns.adobe.com/aep/errors/XDM-1009-400`


有關不同API請求的相容Accept標題清單，請參閱[Schema Registry開發人員指南](./api/overview.md)中的對應章節。

### [!DNL Real-time Customer Profile] 錯誤

以下錯誤消息與啟用[!DNL Real-time Customer Profile]架構時涉及的操作相關聯。 如需詳細資訊，請參閱[!DNL Schema Registry] API指南中的[unions](./api/unions.md)一節。

#### 必須有引用標識描述符

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1526-400",
    "title": "Union descriptor validation error",
    "status": 400,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "If a schema contains properties that are associated with an xdm:descriptorOneToOne descriptor, those properties must also have a xdm:descriptorReferenceIdentity descriptor for that schema to participate in a union.",
        "sub-errors": []
    },
    "detail": "If a schema contains properties that are associated with an xdm:descriptorOneToOne descriptor, those properties must also have a xdm:descriptorReferenceIdentity descriptor for that schema to participate in a union."
}
```

當您嘗試為[!DNL Profile]啟用架構時，將顯示此錯誤消息，其中一個屬性包含沒有引用標識描述符的關係描述符。 將參考標識描述符添加到有關的架構欄位以解決此錯誤。

#### 引用標識描述符欄位和目標架構的命名空間必須匹配

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1527-400",
    "title": "Union descriptor validation error",
    "status": 400,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "If both schemas from an existing xdm:descriptorOneToOne descriptor are promoted to union, and one of those schemas contains a primary identity, the xdm:identityNamespace of the source schema's descriptorReferenceIdentity field must match the xdm:namespace field of destination schema's xdm:descriptorIdentity field.",
        "sub-errors": []
    },
    "detail": "If both schemas from an existing xdm:descriptorOneToOne descriptor are promoted to union, and one of those schemas contains a primary identity, the xdm:identityNamespace of the source schema's descriptorReferenceIdentity field must match the xdm:namespace field of destination schema's xdm:descriptorIdentity field."
}
```

為了啟用包含關係描述符的架構以用於[!DNL Profile]，源欄位的命名空間和目標欄位的主要命名空間必須相同。 當您嘗試啟用包含引用標識描述符的不匹配命名空間的架構時，將顯示此錯誤消息。 確保目標架構的標識欄位的`xdm:namespace`值與源欄位的引用標識描述符中的`xdm:identityNamespace`屬性的值匹配，以解決此問題。

如需標準身分命名空間代碼的清單，請參閱身分命名空間概覽中[標準命名空間](../identity-service/namespaces.md)的區段。

#### 架構必須包含identityMap或主要身分

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1528-400",
    "title": "Union descriptor validation error",
    "status": 400,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "To participate in a union, a schema must include an identityMap fieldgroup or a primary identity descriptor.",
        "sub-errors": []
    },
    "detail": "To participate in a union, a schema must include an identityMap fieldgroup or a primary identity descriptor."
}
```

在為配置檔案啟用架構之前，您必須先為架構[建立主標識描述符](./api/descriptors.md#create)，或包括標識映射欄位以改為在主標識處操作。