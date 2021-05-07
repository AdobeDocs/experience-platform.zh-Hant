---
keywords: Experience Platform；主題；熱門主題；XDM;XDM系統；XDM個人資料；XDM ExperienceEvent;XDM ExperienceEvent;experienceEvent;XDM ExperienceEvent;XDM ExperienceEvent；體驗資料模型；體驗資料模型；資料模型；方案；疑難排解；常見問題；常見問題；聯合方案；聯合概要檔案；聯合概要檔案
solution: Experience Platform
title: XDM系統故障排除指南
description: 本檔案提供有關Adobe Experience PlatformExperience Data Model(XDM)和XDM System的常見問題解答，以及常見錯誤的疑難排解指南。
topic-legacy: troubleshooting
exl-id: a0c7c661-bee8-4f66-ad5c-f669c52c9de3
translation-type: tm+mt
source-git-commit: 3985ba8f46a62e8d9ea8b1f084198b245318a24f
workflow-type: tm+mt
source-wordcount: '1888'
ht-degree: 0%

---

# XDM系統故障排除指南

本檔案提供有關Adobe Experience Platform[!DNL Experience Data Model](XDM)和XDM系統的常見問題解答，以及常見錯誤的疑難排解指南。 有關其他平台服務的問題和故障排除，請參閱[Experience Platform故障排除指南](../landing/troubleshooting.md)。

**[!DNL Experience Data Model](XDM)是開** 放原始碼規格，可定義客戶體驗管理的標準架構。構建[!DNL Experience Platform]的方法&#x200B;**XDM系統**&#x200B;操作[!DNL Experience Data Model]方案，以便由[!DNL Platform]服務使用。 **[!DNL Schema Registry]**&#x200B;提供用戶介面和REST風格的API以訪問[!DNL Experience Platform]中的&#x200B;**[!DNL Schema Library]**。 如需詳細資訊，請參閱[XDM檔案](home.md)。

## 常見問題集

以下是有關XDM系統及[!DNL Schema Registry] API使用的常見問題解答清單。

### 如何將欄位新增至架構？

可以使用架構欄位組將欄位添加到架構中。 每個欄位組都與一個或多個類相容，允許在實現其中一個相容類的任何方案中使用欄位組。 雖然Adobe Experience Platform提供數個產業欄位群組，其中包含其預先定義的欄位，但您可以使用API或使用者介面建立新欄位群組，將自己的欄位新增至架構。

有關在[!DNL Schema Registry] API中建立新欄位組的詳細資訊，請參閱[欄位組端點指南](api/field-groups.md#create)。 如果您使用UI，請參閱[架構編輯器教程](./tutorials/create-schema-ui.md)。

### 欄位群組與資料類型的最佳用途為何？

[欄位](./schema/composition.md#field-group) 組是定義方案中一個或多個欄位的元件。欄位群組強制其欄位在架構階層中的顯示方式，因此在每個架構中都會顯示與其所包含的相同結構。 欄位組僅與特定類相容，由其`meta:intendedToExtend`屬性標識。

[資料](./schema/composition.md#data-type) 類型還可以為模式提供一個或多個欄位。但是，與欄位組不同，資料類型不限於特定類。 這使得資料類型成為更有彈性的選項，以說明可在具有潛在不同類別的多個結構中重複使用的常用資料結構。

### 架構的唯一ID是什麼？

所有[!DNL Schema Registry]資源（結構、欄位群組、資料類型、類別）都有URI，可當成參考和查閱用途的唯一ID。 在API中查看架構時，可在頂級`$id`和`meta:altId`屬性中找到。

如需詳細資訊，請參閱[!DNL Schema Registry] API開發人員指南中的[資源識別](api/getting-started.md#resource-identification)一節。

### 架構何時開始防止中斷更改？

只要在建立資料集時從未使用過或在[[!DNL Real-time Customer Profile]](../profile/home.md)中啟用過，就可以對模式進行中斷更改。 一旦在資料集建立中使用模式或啟用與[!DNL Real-time Customer Profile]一起使用，系統將嚴格執行[模式演化](schema/composition.md#evolution)規則。

### 長欄位類型的最大大小是多少？

長欄位類型是一個最大大小為53(+1)位的整數，其電位範圍介於-9007199254740992和9007199254740992之間。 這是由於JSON的JavaScript實作如何表示長整數的限制。

有關欄位類型的詳細資訊，請參閱[XDM欄位類型約束](./schema/field-constraints.md)上的文檔。

### 如何定義我的架構的身分？

在[!DNL Experience Platform]中，身分用於識別對象（通常是個人），而不管所解釋的資料源為何。 它們是在結構中定義的，方法是將鍵欄位標籤為「標識」。 常用的身分識別欄位包括電子郵件地址、電話號碼、[[!DNL Experience Cloud ID (ECID)]](https://experienceleague.adobe.com/docs/id-service/using/home.html)、CRM ID和其他唯一ID欄位。

欄位可使用API或使用者介面標示為身分。

#### 在API中定義身份

在API中，通過建立身份描述符來建立身份。 身份描述符信號表示模式的特定屬性是唯一標識符。

身份描述符由POST請求建立到／描述符端點。 如果成功，您將會收到HTTP狀態201（已建立）和包含新描述符詳細資訊的響應對象。

有關在API中建立身份描述符的詳細資訊，請參閱[!DNL Schema Registry]開發人員指南中[描述符](api/descriptors.md)部分的文檔。

#### 在UI中定義身份

在模式編輯器中開啟模式時，在編輯器的&#x200B;**[!UICONTROL Structure]**&#x200B;部分中選擇要標籤為身份的欄位。 在右側的&#x200B;**[!UICONTROL Field Properties]**&#x200B;下，選中&#x200B;**[!UICONTROL Identity]**&#x200B;複選框。

有關在UI中管理身份的詳細資訊，請參閱方案編輯器教程中[定義身份欄位](./tutorials/create-schema-ui.md#identity-field)部分一節。

### 我的架構需要主要身分識別嗎？

主要身份是可選的，因為結構可能有0或1個。 但是，方案必須具有主標識，才能在[!DNL Real-time Customer Profile]中啟用方案。 如需詳細資訊，請參閱架構編輯器教學課程的[identity](./tutorials/create-schema-ui.md#identity-field)一節。

### 如何啟用模式以用於[!DNL Real-time Customer Profile]?

通過在架構的`meta:immutableTags`屬性中添加&quot;union&quot;標籤，可在[[!DNL Real-time Customer Profile]](../profile/home.md)中使用架構。 可以使用API或用戶介面來啟用與[!DNL Profile]一起使用的模式。

#### 使用API為[!DNL Profile]啟用現有模式

發出PATCH請求以更新模式，並將`meta:immutableTags`屬性添加為包含值&quot;union&quot;的陣列。 如果更新成功，回應將顯示現在包含union標籤的更新架構。

有關使用API啟用架構以用於[!DNL Real-time Customer Profile]的詳細資訊，請參閱[!DNL Schema Registry]開發人員指南的[unions](./api/unions.md)檔案。

#### 使用UI為[!DNL Profile]啟用現有模式

在[!DNL Experience Platform]中，在左側導航中選擇&#x200B;**[!UICONTROL Schemas]**，然後從方案清單中選擇要啟用的方案名稱。 然後，在編輯器的右側&#x200B;**[!UICONTROL Schema Properties]**&#x200B;下，選擇&#x200B;**[!UICONTROL Profile]**&#x200B;以將其開啟。


如需詳細資訊，請參閱[!UICONTROL Schema Editor]教學課程中「即時客戶個人檔案](./tutorials/create-schema-ui.md#profile)使用」一節。[

### 我可以直接編輯聯合架構嗎？

聯合模式是只讀的，由系統自動生成。 無法直接編輯。 將&quot;union&quot;標籤添加到實現該類的模式時，將為特定類建立聯合模式。

有關XDM中工會的詳細資訊，請參閱[!DNL Schema Registry] API開發人員指南中的[unions](./api/unions.md)一節。

### 如何格式化資料檔案以將資料嵌入到模式？

[!DNL Experience Platform] 接受或JSON格式 [!DNL Parquet] 的資料檔案。這些檔案的內容必須符合資料集參考的架構。 有關資料檔案提取的最佳做法的詳細資訊，請參見[批次提取概述](../ingestion/home.md)。

## 錯誤和疑難排解

以下是使用[!DNL Schema Registry] API時可能遇到的錯誤訊息清單。

### 找不到對象

```json
{
    "type": "/placeholder/type/uri",
    "status": 404,
    "title": "NotFoundError",
    "detail": "Object https://ns.adobe.com/incorrectTenantId/schemas/ee067e31b08514d21e2b82577813409d 
      with version 1 not found"
}
```

當系統找不到特定資源時，將顯示此錯誤。 資源可能已刪除，或API呼叫中的路徑無效。 請確定您已輸入API呼叫的有效路徑，然後再次嘗試。 您可能想要檢查是否已為資源輸入正確的ID，以及路徑是否與適當的容器（全域或租用戶）正確命名。

如需在API中建構查閱路徑的詳細資訊，請參閱[!DNL Schema Registry]開發人員指南中的[container](./api/getting-started.md#container)和[資源識別](api/getting-started.md#resource-identification)章節。

### 標題必須是唯一的

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "Title must be unique. An object 
      https://ns.adobe.com/{TENANT_ID}/schemas/26f6833e55db1dd8308aa07a64f2042d 
      already exists with the same title."
}
```

當您嘗試使用另一個資源已使用的標題建立資源時，將顯示此錯誤消息。 標題在所有資源類型中必須是唯一的。 例如，如果您嘗試建立標題已由架構使用的欄位群組，您會收到此錯誤。

### 自訂欄位必須使用頂層欄位

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "For custom fields, you must use a top level field named _{TENANT_ID}
       and all the other fields must be defined under it"
}
```

當您嘗試建立新的欄位群組時，會顯示此錯誤訊息。 您的IMS組織所定義的欄位群組必須使用`TENANT_ID`命名其欄位，以避免與其他產業和廠商資源產生衝突。 有關欄位組的正確資料結構的詳細示例，請參見[欄位組端點指南](./api/field-groups.md#create)。


### [!DNL Real-time Customer Profile] 錯誤

以下錯誤消息與啟用[!DNL Real-time Customer Profile]方案時涉及的操作相關聯。 如需詳細資訊，請參閱[!DNL Schema Registry] API開發人員指南中的[unions](./api/unions.md)一節。

#### 要啟用配置檔案資料集，架構應有效

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "To enable profile datasets the schema should be valid"
}
```

當您嘗試為尚未為[!DNL Real-time Customer Profile]啟用的架構啟用配置式資料集時，將顯示此錯誤消息。 在啟用資料集之前，請確定架構包含union標籤。

#### 必須有引用標識描述符

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "For a schema to be able to participate in union, if any of its 
      property is associated with a xdm:descriptorOneToOne descriptor, there must 
      be a xdm:descriptorReferenceIdentity descriptor for that property"
}
```

當您嘗試為[!DNL Profile]啟用模式時，將顯示此錯誤消息，其中一個屬性包含沒有引用標識描述符的關係描述符。 將參考身份描述符添加到相關的模式欄位以解決此錯誤。

#### 引用標識描述符欄位和目標模式的名稱空間必須匹配

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "If both schemas from an already defined xdm:descriptorOneToOne 
      descriptor are promoted to union, and if there is a primary identity on one of 
      the schemas from the xdm:descriptorOneToOne descriptor, the 
      xdm:identityNamespace of the sourceSchema's descriptorReferenceIdentity and the 
      xdm:namespace field of the xdm:descriptorIdentity for the destinationSchema must 
      match"
}
```

為了啟用包含關係描述符的方案以便用於[!DNL Profile]，源欄位的命名空間和目標欄位的主命名空間必須相同。 當您嘗試啟用包含引用標識描述符的不匹配命名空間的架構時，將顯示此錯誤消息。 確保目標方案的標識欄位的`xdm:namespace`值與源欄位的引用標識描述符中`xdm:identityNamespace`屬性的值匹配，以解決此問題。

如需支援的身分名稱空間代碼清單，請參閱識別名稱空間概觀中有關[標準名稱空間](../identity-service/namespaces.md)的章節。

### 接受標題錯誤

[!DNL Schema Registry] API中的大多數GET請求都需要「接受」標題，以便系統決定如何格式化回應。 以下是與「接受」標題相關的常見錯誤清單。 有關不同API請求的相容「接受」標題清單，請參閱[方案註冊表開發人員指南](api/getting-started.md)中的相應章節。

#### 必須接受標題參數

```json
{
    "type": "/placeholder/type/uri",
    "status": 406,
    "title": "NotAcceptableError",
    "detail": "Accept header parameter is required"
}
```

當API請求中遺失「接受」標題時，會顯示此錯誤訊息。 在再次嘗試之前，請確定已包含「接受」標題。

#### 未知接受提供的介質

```json
{
    "type": "/placeholder/type/uri",
    "status": 406,
    "title": "NotAcceptableError",
    "detail": "Unknown Accept media supplied: xed+json"
}
```

當「接受」標題無效時，會顯示此錯誤訊息。 請確定您已正確輸入與您嘗試進行之API要求相容的「接受」標題，然後再再試一次。

#### 可用的未知接受格式

```json
{
    "type": "/placeholder/type/uri",
    "status": 406,
    "title": "NotAcceptableError",
    "detail": "Unknown Accept format available "
}
```

查找描述符時，如果「接受」標題提供不正確，則會顯示此錯誤消息。 在重試之前，請確保已正確輸入[支援的描述符](./api/descriptors.md)的接受標頭之一。

#### 必須在「接受」標題中提供版本

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "version must be supplied in the accept header. Example: 
      application/vnd.adobe.xed-full-notext+json; version=1"
}
```

當「接受」標題中未包含版本號碼時，會顯示此錯誤訊息。 某些元素（如結構）在查找單個實例時需要指定版本。 包含版本號碼的「接受」標題看起來類似下列：

```plaintext
application/vnd.adobe.xed+json; version=1
```

如需支援的「接受」標題清單，請參閱[!DNL Schema Registry]開發人員指南中的[接受標題](api/getting-started.md#accept)一節。

#### 「接受」標題中不能提供版本

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "version must not be supplied in the accept header. Example: 
      application/vnd.adobe.xed-full+json"
}
```

如果您在列出(GET)資源時嘗試在「接受」標題中加入版本，將會收到此錯誤。 只有在單一資源上嘗試查閱請求時，才需要版本。 從「接受」標題移除版本以解決錯誤。
