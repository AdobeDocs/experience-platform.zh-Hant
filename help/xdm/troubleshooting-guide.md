---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Experience Data Model(XDM)系統疑難排解指南
topic: troubleshooting
translation-type: tm+mt
source-git-commit: 14cd3d17c7d9ba602d02925abddec9e0b246a8c8

---


# Experience Data Model(XDM)系統疑難排解指南

本檔案提供有關Experience Data Model(XDM)System的常見問題解答，以及常見錯誤的疑難排解指南。 如需Adobe Experience Platform中其他服務的相關問題和疑難排解，請參閱 [Experience Platform疑難排解指南](../landing/troubleshooting.md)。

**Experience Data Model(XDM)** 是一種開放原始碼規格，可定義客戶體驗管理的標準化架構。 建立Experience Platform的方法- **XDM System**，可操作Experience Data Model架構，供Platform服務使用。 The **Schema Registry** provides a user interface and a RESTful API to access the **Schema Library within Experience Platform** . 如需詳細 [資訊，請參閱XDM](home.md) 檔案。

## 常見問題集

以下是有關XDM系統及架構註冊表API使用的常見問題解答清單。

### 如何將欄位新增至架構？

您可以使用mixin，將欄位添加到架構中。 每個混音都與一個或多個類相容，允許混音用於實現這些相容類之一的任何模式。 雖然Adobe Experience Platform提供數種業界混音及其預先定義的欄位，但您可以使用API或使用者介面建立新混音，將自己的欄位新增至架構。

如需在API中建立新混音的詳細資訊，請參閱 [Schema Registry API開發人員指南中的](api/create-mixin.md) 「建立混音檔案」。 如果您使用UI，請參閱架構編 [輯器教學課程](./tutorials/create-schema-ui.md)。

### 混音與資料類型的最佳用途為何？

[Mixins](./schema/composition.md#mixin) 是定義架構中一或多個欄位的元件。 Mixins可強制其欄位在架構階層中的顯示方式，因此在每個架構中都會顯示與其所包含的相同結構。 Mixin只與特定類別相容，由其屬性 `meta:intendedToExtend` 識別。

[資料類型](./schema/composition.md#data-type) ，也可以為方案提供一個或多個欄位。 但是，與mixin不同，資料類型不限於特定類別。 這使得資料類型成為更有彈性的選項，以說明可在具有潛在不同類別的多個結構中重複使用的常用資料結構。

### 架構的唯一ID是什麼？

所有方案註冊表資源（方案、混合、資料類型、類）都有一個URI，它充當唯一ID，用於引用和查找。 在API中檢視結構時，可在頂層和屬性中找 `$id` 到 `meta:altId` 。

如需詳細資訊，請參 [閱「方案註冊](api/getting-started.md#schema-identification) API開發人員指南」中的「方案識別」一節。

### 架構何時開始防止中斷更改？

只要架構從未用於建立資料集或啟用用於即時客戶描述檔，就可以對 [其進行中斷變更](../profile/home.md)。 一旦在資料集建立中使用架構或啟用與即時客戶描述檔搭配使用，系統就會嚴格執行 [Schema Evolution](schema/composition.md#evolution) （架構演化）規則。

### 長欄位類型的最大大小是多少？

長欄位類型是一個最大大小為53(+1)位的整數，其電位範圍介於-9007199254740992和9007199254740992之間。 這是由於JSON的JavaScript實作如何表示長整數的限制。

如需欄位類型的詳細資訊，請參 [閱「架構註冊表API開發人員指南」中的](api/appendix.md#field-types) 「定義XDM欄位類型」一節。

### 如何定義我的架構的身分？

在Experience Platform中，身分識別用於識別主體（通常為個人），不論所解讀的資料來源為何。 它們是在結構中定義的，方法是將鍵欄位標籤為「標識」。 常用的身分識別欄位包括電子郵件地址、電話號碼、 [Experience Cloud ID(ECID)](https://docs.adobe.com/content/help/zh-Hant/id-service/using/home.html)、CRM ID和其他唯一ID欄位。

欄位可使用API或使用者介面標示為身分。

#### 在API中定義身份

在API中，通過建立身份描述符來建立身份。 身份描述符信號表示模式的特定屬性是唯一標識符。

身份描述符由POST請求建立到／描述符端點。 如果成功，您將會收到HTTP狀態201（已建立）和包含新描述符詳細資訊的響應對象。

有關在API中建立身份描述符的詳細資訊，請參閱「方案註冊 [表](api/descriptors.md) 」開發人員指南中的「描述符」部分。

#### 在UI中定義身份

在模式編輯器中開啟模式時，按一下要標籤為身份的編輯器的「結構 **** 」部分中的欄位。 在右 **側的「欄位屬性** 」下，按一下「識別」核取 **方塊** 。

有關在UI中管理身份的詳細資訊，請參閱「架構編輯器」教程中 [的「定義身份欄位](./tutorials/create-schema-ui.md#identity-field) 」一節。

### 我的架構需要主要身分識別嗎？

主要身份是可選的，因為結構可能有0或1個。 但是，方案必須具有主要標識，才能在即時客戶配置檔案中啟用方案。 如需詳細 [資訊，請參閱](./tutorials/create-schema-ui.md#identity-field) 「架構編輯器」教學課程的識別區段。

### 如何啟用結構以用於即時客戶描述檔？

結構可以通過在 [結構的屬性中添加&quot;union&quot;標籤，在即時客戶](../profile/home.md)`meta:immutableTags` 配置檔案中使用。 可使用API或使用者介面來啟用與描述檔搭配使用的架構。

#### 使用API啟用現有的描述檔結構

發出PATCH請求以更新模式並將屬 `meta:immutableTags` 性添加為包含值&quot;union&quot;的陣列。 如果更新成功，回應將顯示現在包含union標籤的更新架構。

有關使用API啟用架構以用於即時客戶描述檔的詳細資訊，請參閱 [Schema Registry Developer Guide的](./api/unions.md) unions document。

#### 使用UI啟用現有的描述檔架構

在Experience Platform中，按一下左側導覽中的 **Schemas** ，然後從架構清單中選取您要啟用的架構名稱。 然後，在編輯器的右側，按一下「架構屬性」( **Schema Properties**)下的「 **Profile** 」（配置檔案）將其開啟。


如需詳細資訊，請參閱「架構編 [輯器」教學課程中「即時客戶描述檔](./tutorials/create-schema-ui.md#profile) 」中的使用章節。

### 我可以直接編輯聯合架構嗎？

聯合模式是只讀的，由系統自動生成。 無法直接編輯。 將&quot;union&quot;標籤添加到實現該類的模式時，將為特定類建立聯合模式。

有關XDM中工會的詳細資訊，請參 [閱](./api/unions.md) Schema Registry API開發人員指南中的Unions一節。

### 如何格式化資料檔案以將資料嵌入到模式？

Experience Platform可接受Parke或JSON格式的資料檔案。 這些檔案的內容必須符合資料集參考的架構。 有關資料檔案提取的最佳做法的詳細資訊，請參 [閱批處理概述](../ingestion/home.md)。

## 錯誤和疑難排解

以下是使用方案註冊表API時可能遇到的錯誤消息清單。

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

如需在API中建構查閱路徑的詳細資訊，請參閱「方案註冊 [表」開發](./api/getting-started.md#container) 人 [員指南中的容](api/getting-started.md#schema-identification) 器和方案識別區段。

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

當您嘗試使用另一個資源已使用的標題建立資源時，將顯示此錯誤消息。 標題在所有資源類型中必須是唯一的。 例如，如果您嘗試建立包含已由架構使用之標題的混音，您會收到此錯誤。

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

當您嘗試建立新混音時，會顯示此錯誤訊息，其中的欄位名稱不正確。 由IMS組織定義的Mixin必須使用命名空間命名其欄位，以 `TENANT_ID` 避免與其他產業和廠商資源發生衝突。 如需混合的適當資料結構的詳細範例，請參閱「架構註冊API開發 [人員指南」中有關建立混合](api/create-mixin.md) in區段的檔案。


### 即時客戶個人檔案錯誤

以下錯誤消息與啟用即時客戶概要檔案的結構涉及的操作相關聯。 如需詳細 [資訊](./api/unions.md) ，請參閱Schema Registry API開發人員指南中的Unions一節。

#### 要啟用配置檔案資料集，架構應有效

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "To enable profile datasets the schema should be valid"
}
```

當您嘗試為尚未啟用即時客戶描述檔的方案啟用描述檔資料集時，會顯示此錯誤訊息。 在啟用資料集之前，請確定架構包含union標籤。

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

當您嘗試為配置式啟用方案時，將顯示此錯誤消息，其中一個屬性包含沒有引用標識描述符的關係描述符。 將參考身份描述符添加到相關的模式欄位以解決此錯誤。

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

為了在配置檔案中啟用包含關係描述符的方案，源欄位的命名空間和目標欄位的主命名空間必須相同。 當您嘗試啟用包含引用標識描述符的不匹配命名空間的架構時，將顯示此錯誤消息。 確保目標方 `xdm:namespace` 案的標識欄位的值與源欄位的 `xdm:identityNamespace` 引用標識描述符中屬性的值匹配，以解決此問題。

如需支援的身分名稱空間代碼清單，請參閱身分名稱空 [間概觀中](../identity-service/namespaces.md) ，關於標準名稱空間的章節。

### 接受標題錯誤

架構註冊表API中的大多數GET請求都需要「接受」標題，以便系統決定如何格式化回應。 以下是與「接受」標題相關的常見錯誤清單。 有關不同API請求的相容「接受」標題清單，請參閱「架構註冊表」開發人員指南中 [的相應章節](api/getting-started.md)。

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

查找描述符時，如果「接受」標題提供不正確，將顯示此錯誤消息。 請確定您已正確輸入了描述符的 [一個支援的接受標頭](./api/descriptors.md) ，然後再重試。

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

如需支援的「接受」標題清單，請參閱「方 [案註冊表](api/getting-started.md#accept) 」開發人員指南中的「接受」標題區段。

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

如果您在列出(GET)資源時嘗試在「接受」標題中包含版本，您會收到此錯誤。 只有在單一資源上嘗試查閱請求時，才需要版本。 從「接受」標題移除版本以解決錯誤。