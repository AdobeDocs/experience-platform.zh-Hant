---
keywords: Experience Platform；熱門主題；XDM;XDM系統；XDM個人概況；XDM體驗事件；XDM體驗事件；體驗事件；XDM體驗事件；XDM體驗事件；體驗資料模型；體驗資料模型；資料模型；模式；故障排除；FAQ;faq;Union schema;UNION PROFILE;union profile;http://ns.adobe.com/aep/errors/XDM-1010-404;http://ns.adobe.com/aep/errors/XDM-1011-404;http://ns.adobe.com/aep/errors/XDM-1012-404;http://ns.adobe.com/aep/errors/XDM-1013-404;http://ns.adobe.com/aep/errors/XDM-1014-404;http://ns.adobe.com/aep/errors/XDM-1015-404;http://ns.adobe.com/aep/errors/XDM-1016-404;http://ns.adobe.com/aep/errors/XDM-1017-404;http://ns.adobe.com/aep/errors/XDM-1521-400;http://ns.adobe.com/aep/errors/XDM-1020-400;http://ns.adobe.com/aep/errors/XDM-1021-400;http://ns.adobe.com/aep/errors/XDM-1022-400;http://ns.adobe.com/aep/errors/XDM-1023-400;http://ns.adobe.com/aep/errors/XDM-1024-400;http://ns.adobe.com/aep/errors/XDM-1006-400;http://ns.adobe.com/aep/errors/XDM-1007-400;http://ns.adobe.com/aep/errors/XDM-1008-400;http://ns.adobe.com/aep/errors/XDM-1009-400;http://ns.adobe.com/aep/errors/XDM-1526-400;http://ns.adobe.com/aep/errors/XDM-1527-400;http://ns.adobe.com/aep/errors/XDM-1528-400;XDM-1010-404;XDM-1011-404;XDM-1012-404;XDM-1013-404;XDM-1014-404;XDM-1015-404;XDM-1016-404;XDM-1017-404;XDM-1521-400;XDM-1020-400;XDM-1021-400;XDM-1022-400;XDM-1023-400;XDM-1024-400;XDM-1006-400;XDM-1007-400;XDM-1008-400;XDM-1009-400;XDM-1413-400;XDM-1526-400;XDM-1527-400;XDM-1528-400;
solution: Experience Platform
title: 《 XDM系統故障排除指南》
description: 查找有關體驗資料模型(XDM)的常見問題的答案，包括解決常見API錯誤的步驟。
exl-id: a0c7c661-bee8-4f66-ad5c-f669c52c9de3
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '2073'
ht-degree: 0%

---

# XDM系統故障排除指南

本文檔提供有關 [!DNL Experience Data Model] (XDM)和Adobe Experience Platform的XDM系統，包括常見錯誤的故障排除指南。 有關其他平台服務的問題和故障排除，請參閱 [Experience Platform故障排除指南](../landing/troubleshooting.md)。

**[!DNL Experience Data Model](XDM)** 是一種開源規範，它定義了客戶體驗管理的標準化架構。 方法 [!DNL Experience Platform] 是建的， **XDM系統**，操作 [!DNL Experience Data Model] 方案使用者 [!DNL Platform] 服務。 的 **[!DNL Schema Registry]** 提供用戶介面和REST風格的API以訪問 **[!DNL Schema Library]** 內 [!DNL Experience Platform]。 查看 [XDM文檔](home.md) 的子菜單。

## 常見問題集

以下是有關XDM系統和使用的常見問題的答案清單 [!DNL Schema Registry] API。

### 如何將欄位添加到架構？

可以使用架構欄位組將欄位添加到架構。 每個欄位組都與一個或多個類相容，允許在實現這些相容類之一的任何架構中使用欄位組。 雖然Adobe Experience Platform提供了多個行業欄位組及其自己的預定義欄位，但您可以通過使用API或用戶介面建立自定義欄位組將自己的欄位添加到架構中。

有關在中建立欄位組的詳細資訊 [!DNL Schema Registry] API，請參見 [欄位組終結點指南](api/field-groups.md#create)。 如果使用UI，請參閱 [架構編輯器教程](./tutorials/create-schema-ui.md)。

### 欄位組與資料類型的最佳用途是什麼？

[欄位組](./schema/composition.md#field-group) 是在架構中定義一個或多個欄位的元件。 欄位組強制實施其欄位在架構層次結構中的顯示方式，因此在每個架構中都顯示了與其包含的相同結構。 欄位組僅與由其標識的特定類相容 `meta:intendedToExtend` 屬性。

[資料類型](./schema/composition.md#data-type) 也可以為架構提供一個或多個欄位。 但是，與欄位組不同，資料類型不受特定類的限制。 這使得資料類型成為描述可跨具有潛在不同類的多個架構重複使用的通用資料結構的更靈活選項。

### 架構的唯一ID是什麼？

全部 [!DNL Schema Registry] 資源（方案、欄位組、資料類型、類）的URI充當唯一ID，用於參考和查找。 在API中查看架構時，可以在頂級 `$id` 和 `meta:altId` 屬性。

有關詳細資訊，請參見 [資源標識](api/getting-started.md#resource-identification) 的 [!DNL Schema Registry] API指南。

### 架構何時開始阻止中斷更改？

只要在建立資料集時從未使用過或在中啟用過，就可以對架構進行中斷更改 [[!DNL Real-Time Customer Profile]](../profile/home.md)。 在資料集建立中使用或啟用模式後 [!DNL Real-Time Customer Profile]的 [架構演化](schema/composition.md#evolution) 被制度嚴格執行。

### 長欄位類型的最大大小是多少？

長欄位類型是一個最大大小為53(+1)位的整數，其勢範圍為–9007199254740992到9007199254740992。 這是由於JSON的JavaScript實現如何表示長整數的限制。

有關欄位類型的詳細資訊，請參閱上的文檔 [XDM欄位類型約束](./schema/field-constraints.md)。

### 如何為架構定義標識？

在 [!DNL Experience Platform]，身份用於標識對象（通常是個人），而不管所解釋的資料源如何。 通過將關鍵字欄位標籤為「標識」，在架構中定義了這些關鍵字。 常用的標識欄位包括電子郵件地址、電話號碼、 [[!DNL Experience Cloud ID (ECID)]](https://experienceleague.adobe.com/docs/id-service/using/home.html)、CRM ID和其他唯一ID欄位。

欄位可以使用API或用戶介面標籤為標識。

#### 在API中定義標識

在API中，通過建立標識描述符來建立標識。 標識描述符表示模式的特定屬性是唯一標識符。

標識描述符由POST請求建立到/descriptors終結點。 如果成功，您將收到HTTP狀態201（已建立）和包含新描述符詳細資訊的響應對象。

有關在API中建立標識描述符的詳細資訊，請參閱上的文檔 [描述符](api/descriptors.md) 的 [!DNL Schema Registry] 的子菜單。

#### 在UI中定義標識

在架構編輯器中開啟架構時，選擇 **[!UICONTROL 結構]** 的子菜單。 下 **[!UICONTROL 欄位屬性]** 在右側，選擇 **[!UICONTROL 身份]** 複選框。

有關在UI中管理標識的詳細資訊，請參閱 [定義標識欄位](./tutorials/create-schema-ui.md#identity-field) 的子目錄。

### 我的架構是否需要主標識？

主標識是可選的，因為方案可能具有零個或其中一個。 但是，架構必須具有主標識才能在中啟用該架構 [!DNL Real-Time Customer Profile]。 查看 [身份](./tutorials/create-schema-ui.md#identity-field) 。

### 如何啟用架構以用於 [!DNL Real-Time Customer Profile]?

已啟用方案供使用 [[!DNL Real-Time Customer Profile]](../profile/home.md) 通過在Conter的 `meta:immutableTags` 架構的屬性。 啟用用於的架構 [!DNL Profile] 可以使用API或用戶介面完成。

#### 啟用現有架構 [!DNL Profile] 使用API

發出PATCH請求以更新架構並添加 `meta:immutableTags` 屬性作為包含值「union」的陣列。 如果更新成功，響應將顯示現在包含聯合標籤的更新架構。

有關使用API啟用模式以供使用的詳細資訊 [!DNL Real-Time Customer Profile]，請參見 [工會](./api/unions.md) 的 [!DNL Schema Registry] 的子菜單。

#### 啟用現有架構 [!DNL Profile] 使用UI

在 [!DNL Experience Platform]選中 **[!UICONTROL 架構]** 在左導航中，然後從架構清單中選擇要啟用的架構的名稱。 然後，在編輯的右側 **[!UICONTROL 架構屬性]**&#x200B;選中 **[!UICONTROL 配置檔案]** 開啟。


有關詳細資訊，請參閱 [在即時客戶配置檔案中使用](./tutorials/create-schema-ui.md#profile) 的 [!UICONTROL 架構編輯器] 教程。

### 是否可以直接編輯聯合架構？

聯合架構是只讀的，並由系統自動生成。 不能直接編輯。 將「union」標籤添加到實現該類的架構時，將為特定類建立聯合架構。

有關XDM中工會的詳細資訊，請參見 [工會](./api/unions.md) 的 [!DNL Schema Registry] API指南。

### 如何格式化資料檔案以將資料導入到架構中？

[!DNL Experience Platform] 接受任一資料檔案 [!DNL Parquet] 或JSON格式。 這些檔案的內容必須符合資料集引用的架構。 有關資料檔案接收的最佳做法的詳細資訊，請參見 [批處理接收概述](../ingestion/home.md)。

## 錯誤和故障排除

以下是使用時可能遇到的錯誤消息清單 [!DNL Schema Registry] API。

### 找不到資源

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

當系統找不到特定資源時，將顯示此錯誤。 資源可能已被刪除，或API調用中的路徑無效。 請確保在重試之前已輸入API調用的有效路徑。 您可能需要檢查是否已為資源輸入了正確的ID，以及路徑是否與相應的容器（全局或租戶）正確命名。

>[!NOTE]
>
>根據正在檢索的資源類型，此錯誤可以使用以下任一項 `type` URI:
>
>* `http://ns.adobe.com/aep/errors/XDM-1010-404`
>* `http://ns.adobe.com/aep/errors/XDM-1011-404`
>* `http://ns.adobe.com/aep/errors/XDM-1012-404`
>* `http://ns.adobe.com/aep/errors/XDM-1013-404`
>* `http://ns.adobe.com/aep/errors/XDM-1014-404`
>* `http://ns.adobe.com/aep/errors/XDM-1015-404`
>* `http://ns.adobe.com/aep/errors/XDM-1016-404`
>* `http://ns.adobe.com/aep/errors/XDM-1017-404`


有關在API中構建查找路徑的詳細資訊，請參見 [容器](./api/getting-started.md#container) 和 [資源標識](api/getting-started.md#resource-identification) 的 [!DNL Schema Registry] 的子菜單。

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

當您嘗試建立具有已被其他資源使用的標題的資源時，將顯示此錯誤消息。 標題在所有資源類型中必須是唯一的。 例如，如果您嘗試建立一個欄位組，其標題已被架構使用，則將收到此錯誤。

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

當您嘗試建立具有不正確命名空間欄位的資源或將不正確命名空間欄位添加到現有資源時，將顯示此錯誤消息。

由您的組織定義的資源必須將其欄位命名為租戶ID下的欄位，以避免與其他行業和供應商資源發生衝突。 使用標準欄位組構建架構時，在這些欄位組結構中添加的任何自定義欄位也必須在租戶ID下命名。

>[!NOTE]
>
>根據命名空間錯誤的特定性質，此錯誤可以使用下列任何一項 `type` URI以及不同的消息詳細資訊：
>
>* `http://ns.adobe.com/aep/errors/XDM-1020-400`
>* `http://ns.adobe.com/aep/errors/XDM-1021-400`
>* `http://ns.adobe.com/aep/errors/XDM-1022-400`
>* `http://ns.adobe.com/aep/errors/XDM-1023-400`
>* `http://ns.adobe.com/aep/errors/XDM-1024-400`


有關XDM資源的正確資料結構的詳細示例，請參閱《架構註冊API指南》：

* [建立自定義類](./api/classes.md#create)
* [建立自定義欄位組](./api/field-groups.md#create)
* [建立自定義資料類型](./api/data-types.md#create)

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

GET請求 [!DNL Schema Registry] API需要 `Accept` 頭以便系統確定如何格式化響應。 當需要 `Accept` 標頭無效或缺失。

根據您使用的端點， `detailed-message` 屬性指示有效 `Accept` 標頭應類似於成功響應。 確保已正確輸入 `Accept` 與您嘗試建立的API請求相容的標頭，然後再重試。

>[!NOTE]
>
>根據所使用的端點，此錯誤可以使用下列任何一項 `type` URI:
>
>* `http://ns.adobe.com/aep/errors/XDM-1006-400`
>* `http://ns.adobe.com/aep/errors/XDM-1007-400`
>* `http://ns.adobe.com/aep/errors/XDM-1008-400`
>* `http://ns.adobe.com/aep/errors/XDM-1009-400`


有關不同API請求的相容接受標頭的清單，請參閱 [架構註冊表開發人員指南](./api/overview.md)。

### [!DNL Real-Time Customer Profile] 錯誤

以下錯誤消息與啟用架構時涉及的操作關聯 [!DNL Real-Time Customer Profile]。 查看 [工會](./api/unions.md) 的 [!DNL Schema Registry] API指南，瞭解詳細資訊。

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

當您嘗試為 [!DNL Profile] 其屬性之一包含沒有引用標識描述符的關係描述符。 將引用標識描述符添加到有關的架構欄位以解決此錯誤。

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
>對於此錯誤，「目標架構」是指關係中的引用架構。

為了啟用包含關係描述符的架構，以便在 [!DNL Profile]，源欄位的命名空間和引用欄位的主命名空間必須相同。 當您嘗試啟用包含引用標識描述符的不匹配命名空間的架構時，將顯示此錯誤消息。

確保 `xdm:namespace` 引用架構的標識欄位的值與 `xdm:identityNamespace` 源欄位的引用標識描述符中的屬性，以解決此問題。

有關標準標識名稱空間代碼的清單，請參見上的部分 [標準命名空間](../identity-service/namespaces.md) 標識名稱空間概述中。

#### 架構必須包括identityMap或主標識

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

在為配置檔案啟用架構之前，必須先 [建立主標識描述符](./api/descriptors.md#create) 為架構，或者包括一個標識映射欄位以代替主標識。

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

屬於同一類的所有啟用配置檔案的架構都必須能夠合併在一起，以便為該類構建聯合架構。 當您嘗試將欄位添加到其路徑由另一個啟用了配置檔案的架構共用且資料類型與原始模式不同的架構時，會出現此錯誤。 由於架構都啟用了Profile並且包含相同的欄位路徑，因此在構建聯合架構時，Profile將嘗試將這兩個欄位合併為一個。 由於不同資料類型不能合併在一起，因此這將被視為合併衝突，不允許。

要解決此問題，請為該欄位選擇其他名稱，或將其嵌套在具有唯一名稱進度的對象下，以避免與具有相似欄位的同一類下的其他啟用了配置檔案的方案合併衝突。
