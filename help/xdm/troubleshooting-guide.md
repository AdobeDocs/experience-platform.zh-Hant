---
keywords: Experience Platform；熱門主題；XDM;XDM系統；XDM個別設定檔；XDM ExperienceEvent;XDM體驗事件；experienceEvent;XDM體驗事件；XDM ExperienceEvent；體驗資料模型；體驗資料模型；資料模型；結構；疑難排解；FAQ;Union架構；UNION設定檔；聯合設定檔；http://ns.adobe.com/aep/errors/XDM-1010-404;http://ns.adobe.com/aep/errors/XDM-1011-404;http://ns.adobe.com/aep/errors/XDM-1012-404;http://ns.adobe.com/aep/errors/XDM-1013-404;http://ns.adobe.com/aep/errors/XDM-1014-404;http://ns.adobe.com/aep/errors/XDM-1015-404;http://ns.adobe.com/aep/errors/XDM-1016-404;http://ns.adobe.com/aep/errors/XDM-1017-404;http://ns.adobe.com/aep/errors/XDM-1521-400;http://ns.adobe.com/aep/errors/XDM-1020-400;http://ns.adobe.com/aep/errors/XDM-1021-400;http://ns.adobe.com/aep/errors/XDM-1022-400;http://ns.adobe.com/aep/errors/XDM-1023-400;http://ns.adobe.com/aep/errors/XDM-1024-400;http://ns.adobe.com/aep/errors/XDM-1006-400;http://ns.adobe.com/aep/errors/XDM-1007-400;http://ns.adobe.com/aep/errors/XDM-1008-400;http://ns.adobe.com/aep/errors/XDM-1009-400;http://ns.adobe.com/aep/errors/XDM-1526-400;http://ns.adobe.com/aep/errors/XDM-1527-400;http://ns.adobe.com/aep/errors/XDM-1528-400;XDM-1010-404;XDM-1011-404;XDM-1012-404;XDM-1013-404;XDM-1014-404;XDM-1015-404;XDM-1016-404;XDM-1017-404;XDM-1521-400;XDM-1020-400;XDM-1021-400;XDM-1022-400;XDM-1023-400;XDM-1024-400;XDM-1006-400;XDM-1007-400;XDM-1008-400;XDM-1009-400;XDM-1413-400;XDM-1526-400;XDM-1527-400;XDM-1528-400
solution: Experience Platform
title: XDM系統疑難排解指南
description: 尋找Experience Data Model(XDM)常見問題的解答，包括解決常見API錯誤的步驟。
exl-id: a0c7c661-bee8-4f66-ad5c-f669c52c9de3
source-git-commit: 7021725e011a1e1d95195c6c7318ecb5afe05ac6
workflow-type: tm+mt
source-wordcount: '2074'
ht-degree: 0%

---

# XDM系統疑難排解指南

本檔案提供關於 [!DNL Experience Data Model] (XDM)和Adobe Experience Platform中的XDM系統，包括常見錯誤的疑難排解指南。 如需其他Platform服務的相關問題和疑難排解，請參閱 [Experience Platform疑難排解指南](../landing/troubleshooting.md).

**[!DNL Experience Data Model](XDM)** 是開放原始碼規格，定義客戶體驗管理的標準化結構。 方法 [!DNL Experience Platform] 是建的， **XDM系統**，操作 [!DNL Experience Data Model] 供使用的結構 [!DNL Platform] 服務。 此 **[!DNL Schema Registry]** 提供使用者介面和RESTful API，以存取 **[!DNL Schema Library]** with [!DNL Experience Platform]. 請參閱 [XDM檔案](home.md) 以取得更多資訊。

## 常見問題集

以下是XDM系統與使用的常見問題解答清單 [!DNL Schema Registry] API。

### 如何將欄位新增至結構？

您可以使用架構欄位群組，將欄位新增至架構。 每個欄位組都與一個或多個類相容，允許在實現其中一個相容類的任何架構中使用該欄位組。 雖然Adobe Experience Platform提供數個產業欄位群組及其預先定義的欄位，但您可以使用API或使用者介面建立自訂欄位群組，將您自己的欄位新增至結構。

如需在 [!DNL Schema Registry] API，請參閱 [欄位群組端點指南](api/field-groups.md#create). 如果您使用UI，請參閱 [結構編輯器教學課程](./tutorials/create-schema-ui.md).

### 欄位群組與資料類型的最佳用途為何？

[欄位群組](./schema/composition.md#field-group) 是定義架構中一或多個欄位的元件。 欄位群組強制其欄位在架構階層中的顯示方式，因此在每個架構中呈現的結構都與其所包含的相同。 欄位組僅與特定類相容，由其標識 `meta:intendedToExtend` 屬性。

[資料類型](./schema/composition.md#data-type) 也可以為架構提供一或多個欄位。 不過，與欄位群組不同，資料類型不會限制在特定類別。 這樣，資料類型就可更靈活地描述可跨具有潛在不同類別的多個架構重複使用的通用資料結構。

### 結構的唯一ID為何？

全部 [!DNL Schema Registry] 資源（結構、欄位群組、資料類型、類別）的URI可作為唯一ID，以供參考和查詢之用。 在API中檢視結構時，可在頂層 `$id` 和 `meta:altId` 屬性。

如需詳細資訊，請參閱 [資源識別](api/getting-started.md#resource-identification) 區段 [!DNL Schema Registry] API指南。

### 架構何時開始防止中斷變更？

只要您從未在建立資料集時使用或啟用於，您就可以對結構進行中斷變更 [[!DNL Real-Time Customer Profile]](../profile/home.md). 在建立資料集時使用結構或啟用搭配使用後 [!DNL Real-Time Customer Profile]，規則 [綱要演變](schema/composition.md#evolution) 被制度嚴格執行。

### 長欄位類型的最大大小是多少？

長欄位類型是一個最大大小為53(+1)位的整數，給它一個介於 — 9007199254740992和9007199254740992之間的位範圍。 這是由於JSON的JavaScript實作如何呈現長整數受到限制。

有關欄位類型的詳細資訊，請參閱 [XDM欄位類型限制](./schema/field-constraints.md).

### 如何定義結構的身分？

在 [!DNL Experience Platform]，身分識別可用來識別主體（通常是個別人員），無論解讀的資料來源為何。 在結構中，會將索引鍵欄位標示為「身分」，以定義這些欄位。 身分的常用欄位包括電子郵件地址、電話號碼、 [[!DNL Experience Cloud ID (ECID)]](https://experienceleague.adobe.com/docs/id-service/using/home.html)、CRM ID和其他唯一ID欄位。

欄位可使用API或使用者介面標示為身分。

#### 在API中定義身分

在API中，身分識別是透過建立身分描述元來建立。 身份描述符發出信號，表示模式的特定屬性是唯一標識符。

身份描述符由POST請求建立到/descriptors端點。 如果成功，您將收到HTTP狀態201（已建立）和包含新描述符詳細資訊的響應對象。

如需在API中建立身分描述元的詳細資訊，請參閱 [描述符](api/descriptors.md) 區段 [!DNL Schema Registry] 開發人員指南。

#### 在UI中定義身分

在架構編輯器中開啟架構後，選取 **[!UICONTROL 結構]** 標籤為標識的編輯器部分。 在 **[!UICONTROL 欄位屬性]** 在右側，選取 **[!UICONTROL 身分]** 核取方塊。

如需在UI中管理身分的詳細資訊，請參閱 [定義身分欄位](./tutorials/create-schema-ui.md#identity-field) 一節。

### 我的架構是否需要主要身分識別？

主要身分為選用，因為結構可能為零或其中一個。 但是，架構必須具有主要身分，才能在中啟用該架構 [!DNL Real-Time Customer Profile]. 請參閱 [身分](./tutorials/create-schema-ui.md#identity-field) 一節，以取得詳細資訊。

### 如何啟用結構以用於 [!DNL Real-Time Customer Profile]?

結構可在 [[!DNL Real-Time Customer Profile]](../profile/home.md) 在 `meta:immutableTags` 結構的屬性。 啟用結構以便與 [!DNL Profile] 可使用API或使用者介面完成。

#### 為啟用現有架構 [!DNL Profile] 使用API

發出PATCH請求以更新結構並新增 `meta:immutableTags` 屬性，作為包含「union」值的陣列。 如果更新成功，回應會顯示更新的架構，其現在包含union標籤。

如需使用API來啟用結構以供使用的詳細資訊，請參閱 [!DNL Real-Time Customer Profile]，請參閱 [工會](./api/unions.md) 檔案 [!DNL Schema Registry] 開發人員指南。

#### 為啟用現有架構 [!DNL Profile] 使用UI

在 [!DNL Experience Platform]，選取 **[!UICONTROL 結構]** 在左側導覽中，從架構清單中選取要啟用的架構名稱。 然後，在編輯的右側， **[!UICONTROL 架構屬性]**，選取 **[!UICONTROL 設定檔]** 開啟。


如需詳細資訊，請參閱 [在即時客戶個人檔案中使用](./tutorials/create-schema-ui.md#profile) 在 [!UICONTROL 結構編輯器] 教學課程。

### 我可以直接編輯聯合結構嗎？

聯合結構是唯讀的，由系統自動產生。 無法直接編輯。 當實作該類的架構中新增「union」標籤時，會為特定類別建立union結構。

如需XDM中聯合的詳細資訊，請參閱 [工會](./api/unions.md) 區段 [!DNL Schema Registry] API指南。

### 如何將資料檔案格式化以將資料內嵌到架構中？

[!DNL Experience Platform] 接受其中一個 [!DNL Parquet] 或JSON格式。 這些檔案的內容必須符合資料集參考的結構。 如需資料檔案內嵌最佳實務的詳細資訊，請參閱 [批次匯入概觀](../ingestion/home.md).

## 錯誤和疑難排解

以下是使用時可能會遇到的錯誤訊息清單 [!DNL Schema Registry] API。

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
>根據要檢索的資源類型，此錯誤可使用下列任一項 `type` URI:
>
>* `http://ns.adobe.com/aep/errors/XDM-1010-404`
>* `http://ns.adobe.com/aep/errors/XDM-1011-404`
>* `http://ns.adobe.com/aep/errors/XDM-1012-404`
>* `http://ns.adobe.com/aep/errors/XDM-1013-404`
>* `http://ns.adobe.com/aep/errors/XDM-1014-404`
>* `http://ns.adobe.com/aep/errors/XDM-1015-404`
>* `http://ns.adobe.com/aep/errors/XDM-1016-404`
>* `http://ns.adobe.com/aep/errors/XDM-1017-404`


如需在API中建構查詢路徑的詳細資訊，請參閱 [容器](./api/getting-started.md#container) 和 [資源識別](api/getting-started.md#resource-identification) 區段 [!DNL Schema Registry] 開發人員指南。

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
>根據命名空間錯誤的特定性質，此錯誤可能會使用下列任一項 `type` URI以及不同的消息詳細資訊：
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

GET請求 [!DNL Schema Registry] API需要 `Accept` 標題，以便系統判斷如何格式化回應。 當需要 `Accept` 標題無效或遺失。

視您使用的端點而定， `detailed-message` 屬性表示有效 `Accept` 標題看起來應該是成功回應。 請確定您已正確輸入 `Accept` 與您嘗試進行之API請求相容的標題，然後再次嘗試。

>[!NOTE]
>
>根據使用的端點，此錯誤可使用下列任一項 `type` URI:
>
>* `http://ns.adobe.com/aep/errors/XDM-1006-400`
>* `http://ns.adobe.com/aep/errors/XDM-1007-400`
>* `http://ns.adobe.com/aep/errors/XDM-1008-400`
>* `http://ns.adobe.com/aep/errors/XDM-1009-400`


如需不同API請求的相容接受標題清單，請參閱 [Schema Registry開發人員指南](./api/overview.md).

### [!DNL Real-Time Customer Profile] 錯誤

下列錯誤訊息與啟用結構中涉及的操作相關聯 [!DNL Real-Time Customer Profile]. 請參閱 [工會](./api/unions.md) 區段 [!DNL Schema Registry] API指南，以了解詳細資訊。

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

當您嘗試為啟用架構時，會顯示此錯誤訊息 [!DNL Profile] 並且其一個屬性包含沒有引用標識描述符的關係描述符。 將參考標識描述符添加到相關架構欄位以解決此錯誤。

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

>[!NOTE]
>
>對於此錯誤，「目標架構」是指關係中的參考架構。

為了啟用包含關係描述符的架構以用於 [!DNL Profile]，來源欄位的命名空間和參考欄位的主要命名空間必須相同。 當您嘗試啟用包含引用標識描述符的不匹配命名空間的架構時，將顯示此錯誤消息。

確保 `xdm:namespace` 引用架構的標識欄位的值與 `xdm:identityNamespace` 屬性（位於源欄位的引用標識描述符中），以解決此問題。

如需標準身分命名空間代碼的清單，請參閱 [標準命名空間](../identity-service/namespaces.md) 在「身分命名空間」概述中。

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

為設定檔啟用結構之前，您必須先 [建立主身份描述符](./api/descriptors.md#create) ，或納入「身分對應」欄位以改用主要身分。

#### 無法合併不相容的資料類型

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1413-400",
    "title": "Merge Schema Error",
    "status": 400,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "Cannot merge incompatible data types. The path /person/name has already been defined in schema (id=0238be93d3e7a06aec5e0655955901ec) using a different data type. Types: string, object",
        "sub-errors": []
    },
    "detail": "Cannot merge incompatible data types. The path /person/name has already been defined in schema (id=0238be93d3e7a06aec5e0655955901ec) using a different data type. Types: string, object"
}
```

屬於相同類的所有啟用配置檔案的結構必須能夠合併在一起，才能構建該類的聯合結構。 當您嘗試將欄位新增至某個架構，而該架構的路徑已由另一個啟用設定檔的架構共用，且該資料類型與原始資料不同時，就會出現此錯誤。 由於結構已啟用設定檔且包含相同的欄位路徑，因此在建構聯合結構時，設定檔會嘗試將這兩個欄位合併為一個欄位。 由於不同的資料類型無法合併在一起，因此這會被視為合併衝突，且不允許。

要解決此問題，請為欄位選擇不同名稱，或在命名空間唯一的對象下嵌套該欄位，以避免與具有相同欄位的同類中啟用配置檔案的其他架構合併衝突。
