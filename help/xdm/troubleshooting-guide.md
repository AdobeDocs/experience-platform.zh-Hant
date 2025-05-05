---
keywords: Experience Platform；熱門主題；XDM；XDM系統；XDM個人設定檔；XDM ExperienceEvent；XDM體驗事件；experienceEvent；experienceEvent；XDM體驗事件；XDM ExperienceEvent；體驗資料模型；體驗資料模型；資料模型；資料模型；結構描述；疑難排解；FAQ；Union結構描述；UNION設定檔；聯合設定檔；http://ns.adobe.com/aep/errors/XDM-1010-404;http://ns.adobe.com/aep/errors/XDM-1011-404;http://ns.adobe.com/aep/errors/XDM-1012-404;http://ns.adobe.com/aep/errors/XDM-1013-404;http://ns.adobe.com/aep/errors/XDM-1014-404;http://ns.adobe.com/aep/errors/XDM-1015-404;http://ns.adobe.com/aep/errors/XDM-1016-404;http://ns.adobe.com/aep/errors/XDM-1017-404;http://ns.adobe.com/aep/errors/XDM-1521-400;http://ns.adobe.com/aep/errors/XDM-1020-400;http://ns.adobe.com/aep/errors/XDM-1021-400;http://ns.adobe.com/aep/errors/XDM-1022-400;http://ns.adobe.com/aep/errors/XDM-1023-400;http://ns.adobe.com/aep/errors/XDM-1024-400;http://ns.adobe.com/aep/errors/XDM-1006-400;http://ns.adobe.com/aep/errors/XDM-1007-400;http://ns.adobe.com/aep/errors/XDM-1008-400;http://ns.adobe.com/aep/errors/XDM-1009-400;http://ns.adobe.com/aep/errors/XDM-1526-400;http://ns.adobe.com/aep/errors/XDM-1527-400;http://ns.adobe.com/aep/errors/XDM-1528-400;XDM-1010-404;XDM-1011-404;XDM-1012-404;XDM-1013-404;XDM-1014-404;XDM-1015-404;XDM-1016-404;XDM-1017-404;XDM-1521-400;XDM-1020-400;XDM-1021-400;XDM-1022-400;XDM-1023-400;XDM-1024-400;XDM-1006-400;XDM-1007-400;XDM-1008-400;XDM-1009-400;XDM-1413-400;XDM-1526-400;XDM-1527-400;XDM-1528-400；
solution: Experience Platform
title: XDM系統疑難排解指南
description: 尋找有關Experience Data Model (XDM)常見問題的解答，包括解決常見API錯誤的步驟。
exl-id: a0c7c661-bee8-4f66-ad5c-f669c52c9de3
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2348'
ht-degree: 0%

---

# XDM系統疑難排解指南

本檔案提供有關Adobe Experience Platform中[!DNL Experience Data Model] (XDM)和XDM系統的常見問題解答，包括常見錯誤的疑難排解指南。 有關其他Experience Platform服務的問題和疑難排解，請參閱[Experience Platform疑難排解指南](../landing/troubleshooting.md)。

**[!DNL Experience Data Model] (XDM)**&#x200B;是開放原始碼規格，定義用於客戶體驗管理的標準化結構描述。 建置[!DNL Experience Platform]的方法&#x200B;**XDM系統**&#x200B;可將[!DNL Experience Data Model]個結構描述作業化以供[!DNL Experience Platform]服務使用。 **[!DNL Schema Registry]**&#x200B;提供使用者介面和RESTful API，以存取[!DNL Experience Platform]內的&#x200B;**[!DNL Schema Library]**。 如需詳細資訊，請參閱[XDM檔案](home.md)。

## 常見問題集

以下是有關XDM系統和[!DNL Schema Registry] API使用常見問題的解答清單。

## 結構描述基本知識

在本節中，您可以找到有關XDM系統中結構描述結構、欄位使用情況和身分識別的基本問題解答。

### 如何將欄位新增至結構描述？

您可以使用結構描述欄位群組，將欄位新增到結構描述。 每個欄位群組都與一個或多個類別相容，允許欄位群組用於實作其中一個相容類別的任何結構描述中。 雖然Adobe Experience Platform為數個產業欄位群組提供自己的預先定義欄位，但您可以使用API或使用者介面建立自訂欄位群組，將自己的欄位新增到結構描述中。

如需在[!DNL Schema Registry] API中建立欄位群組的詳細資訊，請參閱[欄位群組端點指南](api/field-groups.md#create)。 如果您使用UI，請參閱[結構描述編輯器教學課程](./tutorials/create-schema-ui.md)。

### 欄位群組與資料型別的最佳用途為何？

[欄位群組](./schema/composition.md#field-group)是定義結構描述中一或多個欄位的元件。 欄位群組會強制實施其欄位在結構描述階層中的顯示方式，因此會在其包含的每個結構描述中顯示相同的結構。 欄位群組僅與特定類別相容，由其`meta:intendedToExtend`屬性識別。

[資料型別](./schema/composition.md#data-type)也可以為結構描述提供一個或多個欄位。 但是，與欄位群組不同，資料型別不受限於特定類別。 這讓資料型別成為一個更具彈性的選項，用來描述在多個結構描述中可以重複使用，且具有可能不同類別的常見資料結構。

### 結構描述的唯一ID為何？

所有[!DNL Schema Registry]資源（結構描述、欄位群組、資料型別、類別）都有一個URI做為唯一ID，以供參考和查詢。 在API中檢視結構描述時，您可以在頂層`$id`和`meta:altId`屬性中找到它。

如需詳細資訊，請參閱[!DNL Schema Registry] API指南中的[資源識別](api/getting-started.md#resource-identification)區段。

### 長欄位型別的大小上限是多少？

長欄位型別是整數，大小上限為53(+1)位元，潛在範圍介於 — 9007199254740992到9007199254740992之間。 這是由於JavaScript實施JSON如何表示長整數的限制。

如需欄位型別的詳細資訊，請參閱有關[XDM欄位型別限制](./schema/field-constraints.md)的檔案。

### 什麼是meta：AltId？

`meta:altId`是結構描述的唯一識別碼。 `meta:altId`提供易於參考的ID以用於API呼叫。 此ID可避免在每次與JSON URI格式搭配使用時進行編碼/解碼。
<!-- (Needs clarification - How do I retrieve it INCOMPLETE) ... -->

<!-- ### How can I generate a sample payload for a schema? -->

<!-- No Answer available.  -->
<!-- INCOMPLETE ... -->

### 地圖資料型別的使用限製為何？

XDM對於此資料型別的使用有下列限制：

- 對應型別必須是型別物件。
- 對應型別不得有已定義的屬性（換言之，它們會定義「空白」物件）。
- 對應型別必須包含additionalProperties.type欄位，以說明可放置在對應中的值（字串或整數）。
- 多實體分段只能根據對應索引鍵而不是值來定義。
- 帳戶對象不支援地圖。

如需詳細資訊，請參閱對應物件[&#128279;](./ui/fields/map.md#restrictions)的使用限制。

>[!NOTE]
>
>不支援多階層地圖或地圖。

<!-- You cannot create a complex map object. However, you can define map fields in the Schema Editor. See the guide on [defining map fields in the UI](./ui/fields/map.md) for more information. -->

<!-- ### How do I create a complex map object using APIs? -->

<!-- You cannot create a complex map object. -->

<!-- ### How can I manage schema inheritance in Adobe Experience Platform? -->

<!-- No Answer available.  -->
<!-- INCOMPLETE ... -->

## 結構描述Identity Management

本節包含有關在結構描述中定義和管理身分識別的常見問題解答。

### 如何為結構描述定義身分？

在[!DNL Experience Platform]中，無論要解譯的資料來源為何，身分都會用來識別主旨（通常是個人）。 它們透過將關鍵欄位標籤為「身分」來定義在結構描述中。 身分識別常用的欄位包括電子郵件地址、電話號碼、[[!DNL Experience Cloud ID (ECID)]](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=zh-Hant)、CRM ID和其他唯一ID欄位。

可使用API或使用者介面將欄位標示為身分。

### 在API中定義身分

在API中，身分識別是透過建立身分描述項來建立。 身分描述項會指出結構描述的特定屬性是唯一識別碼。

身分描述項是由POST要求建立到/descriptors端點。 如果成功，您將會收到HTTP Status 201 （已建立）以及包含新描述項詳細資訊的回應物件。

如需在API中建立身分描述項的詳細資訊，請參閱[!DNL Schema Registry]開發人員指南中[描述項](api/descriptors.md)章節的檔案。

### 在UI中定義身分

在結構描述編輯器中開啟結構描述後，在編輯器的&#x200B;**[!UICONTROL 結構]**&#x200B;區段中選取要標示為身分的欄位。 在右側的&#x200B;**[!UICONTROL 欄位屬性]**&#x200B;下，選取&#x200B;**[!UICONTROL 身分]**&#x200B;核取方塊。

如需在UI中管理身分的詳細資訊，請參閱結構描述編輯器教學課程中[定義身分欄位](./tutorials/create-schema-ui.md#identity-field)區段的相關章節。

### 我的結構描述需要主要身分嗎？

主要身分是選用的，因為結構描述可能沒有或只有一個。 但是，結構描述必須具有主要身分，才能啟用結構描述以在[!DNL Real-Time Customer Profile]中使用。 如需詳細資訊，請參閱結構描述編輯器教學課程的[identity](./tutorials/create-schema-ui.md#identity-field)一節。

## 結構描述檔啟用

本節提供啟用綱要以用於Real-Time Customer Profile的指引。

### 如何啟用結構描述以用於[!DNL Real-Time Customer Profile]？

透過在結構描述的`meta:immutableTags`屬性中新增「union」標籤，結構描述可以用於[[!DNL Real-Time Customer Profile]](../profile/home.md)。 可以使用API或使用者介面啟用結構描述以搭配[!DNL Profile]使用。

### 使用API啟用[!DNL Profile]的現有結構描述

發出PATCH請求以更新結構描述，並將`meta:immutableTags`屬性新增為包含「union」值的陣列。 如果更新成功，回應將顯示更新的結構描述，其中現在包含聯合標籤。

如需使用API啟用結構描述以在[!DNL Real-Time Customer Profile]中使用的詳細資訊，請參閱[!DNL Schema Registry]開發人員指南的[聯合](./api/unions.md)檔案。

### 使用UI啟用[!DNL Profile]的現有結構描述

在[!DNL Experience Platform]中，選取左側導覽的&#x200B;**[!UICONTROL 結構描述]**，然後從結構描述清單中選取您要啟用的結構描述名稱。 然後，在編輯器的右側&#x200B;**[!UICONTROL 結構描述屬性]**&#x200B;下，選取&#x200B;**[!UICONTROL 設定檔]**&#x200B;以將其開啟。

如需詳細資訊，請參閱[!UICONTROL 結構描述編輯器]教學課程中[用於即時客戶個人檔案](./tutorials/create-schema-ui.md#profile)的相關章節。

### 將Adobe Analytics資料匯入為來源時，是否針對設定檔啟用自動建立的結構描述？

結構描述不會自動為即時客戶設定檔啟用。 您需要根據為設定檔啟用的結構描述，為設定檔明確啟用資料集。 請參閱檔案以瞭解啟用資料集以用於Real-Time Customer Profile[&#128279;](../catalog/datasets/user-guide.md#enable-profile)所需的步驟和要求。

### 我可以刪除已啟用設定檔的結構描述嗎？

為即時客戶設定檔啟用結構描述後，您就無法再刪除它。 為設定檔啟用結構描述後，就無法停用或刪除它，也無法從結構描述中移除欄位。 因此，在為設定檔啟用結構描述之前，請務必仔細規劃及驗證該結構描述設定。 不過，您可以刪除已啟用設定檔的資料集。 您可在此找到資訊： <https://experienceleague.adobe.com/zh-hant/docs/experience-platform/catalog/datasets/user-guide#delete-a-profile-enabled-dataset>

如果您不想再使用已啟用設定檔的結構描述，建議將結構描述重新命名為包含&#x200B;**不要使用**&#x200B;或&#x200B;**非使用中**。

## 結構描述修改和限制

本節提供架構修改規則及預防中斷變更的釐清。

### 結構描述何時開始防止重大變更？

只要結構描述從未用於建立資料集，或啟用以用於[[!DNL Real-Time Customer Profile]](../profile/home.md)，就可以對結構描述進行重大變更。 一旦結構描述已用於資料集建立或啟用以與[!DNL Real-Time Customer Profile]搭配使用，[結構描述演化](schema/composition.md#evolution)的規則就會由系統嚴格執行。

### 我可以直接編輯聯合結構描述嗎？

聯合結構是唯讀的，由系統自動產生。 無法直接編輯它們。 在實作特定類別的結構描述中新增「聯合」標籤時，會為該類別建立聯合結構描述。

如需XDM中聯合的詳細資訊，請參閱[!DNL Schema Registry] API指南中的[聯合](./api/unions.md)區段。

### 如何格式化資料檔以將資料擷取至我的結構描述？

[!DNL Experience Platform]接受[!DNL Parquet]或JSON格式的資料檔。 這些檔案的內容必須符合資料集參考的結構描述。 如需資料檔擷取最佳實務的詳細資訊，請參閱[批次擷取總覽](../ingestion/home.md)。

### 如何將結構描述轉換為唯讀結構描述？

您目前無法將結構描述轉換為唯讀。

## 錯誤與疑難排解

以下是您在使用[!DNL Schema Registry] API時可能會遇到的錯誤訊息清單。

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

當系統找不到特定資源時，便會顯示此錯誤。 資源可能已遭刪除，或API呼叫中的路徑無效。 在重試之前，請確定您已為API呼叫輸入有效的路徑。 您可能想要檢查您是否為資源輸入了正確的ID，且路徑已使用適當的容器（全域或租使用者）正確命名。

>[!NOTE]
>
>根據正在擷取的資源型別，此錯誤可以使用下列`type`個URI：
>
>- `http://ns.adobe.com/aep/errors/XDM-1010-404`
>- `http://ns.adobe.com/aep/errors/XDM-1011-404`
>- `http://ns.adobe.com/aep/errors/XDM-1012-404`
>- `http://ns.adobe.com/aep/errors/XDM-1013-404`
>- `http://ns.adobe.com/aep/errors/XDM-1014-404`
>- `http://ns.adobe.com/aep/errors/XDM-1015-404`
>- `http://ns.adobe.com/aep/errors/XDM-1016-404`
>- `http://ns.adobe.com/aep/errors/XDM-1017-404`

如需在API中建構查閱路徑的詳細資訊，請參閱[!DNL Schema Registry]開發人員指南中的[容器](./api/getting-started.md#container)和[資源識別](api/getting-started.md#resource-identification)區段。

### 標題不是唯一的

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

當您嘗試建立標題已由其他資源使用的資源時，會顯示此錯誤訊息。 標題在所有資源型別中必須是唯一的。 例如，如果您嘗試以結構描述已使用的標題建立欄位群組，您將會收到此錯誤。

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

當您嘗試使用不正確的名稱空間欄位建立資源，或將不正確的名稱空間欄位新增到現有資源時，會顯示此錯誤訊息。

貴組織定義的資源必須將租使用者ID下的欄位命名為名稱空間，以避免與其他產業和廠商資源衝突。 使用標準欄位群組建立結構描述時，您在這些欄位群組的結構中新增的任何自訂欄位也必須以租使用者ID命名。

>[!NOTE]
>
>根據名稱空間錯誤的特定性質，此錯誤可以使用下列`type`個URI以及不同的訊息詳細資料：
>
>- `http://ns.adobe.com/aep/errors/XDM-1020-400`
>- `http://ns.adobe.com/aep/errors/XDM-1021-400`
>- `http://ns.adobe.com/aep/errors/XDM-1022-400`
>- `http://ns.adobe.com/aep/errors/XDM-1023-400`
>- `http://ns.adobe.com/aep/errors/XDM-1024-400`

有關XDM資源的正確資料結構的詳細範例，請參閱結構描述登入API指南：

- [建立自訂類別](./api/classes.md#create)
- [建立自訂欄位群組](./api/field-groups.md#create)
- [建立自訂資料型別](./api/data-types.md#create)

### Accept 標頭無效

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

[!DNL Schema Registry] API中的GET請求需要`Accept`標頭，系統才能決定如何格式化回應。 當必要的`Accept`標頭無效或遺失時，會發生此錯誤。

根據您使用的端點，`detailed-message`屬性會指出有效的`Accept`標頭在成功回應中應該是什麼樣子。 在重試之前，請確定您已正確輸入與嘗試發出的API要求相容的`Accept`標頭。

>[!NOTE]
>
>根據使用的端點，此錯誤可以使用下列`type`個URI：
>
>- `http://ns.adobe.com/aep/errors/XDM-1006-400`
>- `http://ns.adobe.com/aep/errors/XDM-1007-400`
>- `http://ns.adobe.com/aep/errors/XDM-1008-400`
>- `http://ns.adobe.com/aep/errors/XDM-1009-400`

如需不同API要求的相容Accept標頭清單，請參閱[結構描述登入開發人員指南](./api/overview.md)中的對應章節。

### [!DNL Real-Time Customer Profile]個錯誤

下列錯誤訊息與啟用[!DNL Real-Time Customer Profile]的結構描述相關作業。 如需詳細資訊，請參閱[!DNL Schema Registry] API指南中的[聯合](./api/unions.md)區段。

#### 必須有參考身分描述項

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

當您嘗試啟用[!DNL Profile]的結構描述時，這個錯誤訊息就會顯示，而且其其中一個屬性包含沒有參考識別描述項的關係描述項。 將參考身分描述項新增到相關結構描述欄位以解決此錯誤。

#### 參考身分描述項欄位和目的地結構描述的名稱空間必須相符

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
>對於此錯誤，「目的地結構描述」是指關係中的參考結構描述。

為了啟用包含關係描述項的結構描述以在[!DNL Profile]中使用，來源欄位的名稱空間和參考欄位的主要名稱空間必須相同。 當您嘗試啟用包含不相符名稱空間的結構描述以做為參考身分描述項時，會顯示此錯誤訊息。

請確定參考結構描述身分欄位的`xdm:namespace`值符合來源欄位參考身分描述項中`xdm:identityNamespace`屬性的值以解決此問題。

如需標準身分名稱空間程式碼的清單，請參閱身分名稱空間概觀中有關[標準名稱空間](../identity-service/features/namespaces.md)的章節。

#### 結構描述必須包含identityMap或主要身分

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

在啟用設定檔的結構描述之前，您必須先為結構描述[建立主要身分描述項](./api/descriptors.md#create)，或加入身分對應欄位以取代主要身分。

#### 無法合併不相容的資料型別

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

屬於相同類別的所有已啟用設定檔的結構描述都必須能夠合併在一起，才能為該類別建構聯合結構描述。 當您嘗試將欄位新增到結構描述時，會出現此錯誤，此結構描述的路徑由另一個已啟用設定檔的結構描述共用，且資料型別與原始結構描述不同。 由於結構描述已啟用設定檔並包含相同的欄位路徑，在建構聯合結構描述時，設定檔會嘗試將這兩個欄位合併為一個。 由於不同的資料型別無法合併在一起，這將會被視為合併衝突，因此是不允許的。

若要解決此問題，請為欄位選擇不同的名稱，或將其巢狀內嵌在唯一的名稱空間物件下，以避免與相同類別下其他具有類似欄位的已啟用設定檔結構描述發生合併衝突。
