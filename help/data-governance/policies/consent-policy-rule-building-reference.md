---
title: 同意原則規則建置參考
description: 瞭解如何使用XDM資料型別、支援的運運算元和進階邏輯，在Adobe Experience Platform UI中建立精細的同意原則規則。
source-git-commit: 678220b14cefd4dd31ef7a12355d796575a77a50
workflow-type: tm+mt
source-wordcount: '1576'
ht-degree: 0%

---

# 同意原則規則建置參考

在進階規則邏輯上使用此參考，在Adobe Experience Platform中同意原則產生器的&#x200B;**[!UICONTROL Then]**&#x200B;子句中設定精確、合法有效的規則。

![強調使用者定義規則條件的[!UICONTROL Then]子句區段的同意原則產生器介面。](../images/policies/multiple-rules.png)

瞭解原則規則如何套用至您的同意資料結構和型別，以準確強制客戶同意偏好設定。

請閱讀本檔案，瞭解如何透過導覽至XDM結構描述中的容器欄位並選取基本欄位，根據同意篩選設定檔。 然後使用適當的運運算元來定義設定檔必須符合的確切值。

## 先決條件

使用此參考資料之前，請確定您的同意原則設定已完成，且您瞭解Adobe Experience Platform資料架構和治理架構的基本概念。

請確定您符合下列先決條件：

* **原則設定完成**：您已在Adobe Experience Platform UI中建立或開始建立同意原則。 如需詳細步驟，請參閱[資料使用原則使用手冊](user-guide.md#consent-policy)。

* **熟悉資料結構**：此參考需要下列核心概念的實用知識：
   * **XDM和聯合結構描述**：瞭解Experience資料模型結構如何定義資料關係，以及聯合結構描述如何代表統一的客戶設定檔。 如需瞭解詳細資訊，請參閱[XDM系統總覽](../../xdm/home.md)。
   * **資料控管架構**：瞭解Adobe Experience Platform如何強制資料使用原則與控管規則。 如需詳細資訊，請參閱[資料控管概觀](../home.md)。
   * **客戶同意處理**：瞭解如何在客戶體驗工作流程中收集、儲存及套用同意資料。 請參閱[同意處理概述](../../landing/governance-privacy-security/consent/adobe/overview.md)。

## 核心概念：基本和容器欄位

請閱讀本小節，瞭解同意原則規則如何在XDM結構描述中使用不同的欄位型別。 瞭解容器和原始欄位之間的區別，有助於您在定義原則條件時選取正確的欄位和運運算元。

### 支援的欄位型別和規則邏輯

同意原則支援多種欄位型別，每種型別都有用於建立規則條件的特定運運算元。 欄位型別會分組為兩個類別： **容器型別**&#x200B;和&#x200B;**基本型別**。

### 容器型別（結構描述導覽）

容器型別會組織同意資料，但無法直接在原則條件中使用。 它們用作導覽路徑，以到達儲存實際值的原始欄位。

| 容器型別 | 說明 |
|----------------|-------------|
| **物件** | 具有固定結構描述的容器，可容納多種不同型別的欄位。 |
| **陣列** | 容納相同型別之多個值的容器。 |
| **地圖** | 具有動態鍵的容器，可容納物件或其他欄位型別。 |

>[!IMPORTANT]
>
>無法在同意原則條件中直接選取容器欄位。 您必須瀏覽至容器，以選取&#x200B;**基本欄位** （例如字串、數字或布林值）來建立規則。 容器運運算元僅用於結構描述導覽，不用於設定原則條件。

### 標準型別（規則條件）

基本欄位會保留實際的同意資料值（例如，`true`或`"weekly"`），而且是唯一可用來定義原則條件的欄位型別。

下表說明每個支援的基本型別和可用的運運算元。

| 標準型別 | 支援的運運算元 | 說明 |
|----------------|---------------------|-------------|
| **字串** | `is equal to`、`is not equal to`、`exists`、`does not exist` | 文字型同意屬性。 |
| **數字** | `is equal to`、`is not equal to`、`is greater than`、`is less than`、`exists`、`does not exist` | 數值同意屬性。 |
| **布林值** | `is equal to`、`is not equal to` | 真或假同意值。 |
| **日期** | `is equal to`、`is not equal to`、`exists`、`does not exist` | 以日期為基礎的同意屬性。 |


## 使用複雜的資料結構

請參閱本節，瞭解如何導覽同意結構描述中的巢狀容器，以存取原始欄位。 它會簡介常見的結構模式，並說明更深層的結構如何啟用更精細的同意邏輯。

### 處理巢狀和複雜的結構描述結構

複雜的同意結構通常包括巢狀容器結構，可支援靈活且可擴充的資料管理。 由於原則規則只能參考基本欄位，因此您必須瀏覽容器階層，以存取可在同意原則條件中使用的欄位。 更深入的巢狀結構可讓您更精細、更明確的規則目標定位。

常見的巢狀容器模式包括：

* **對應** — 包含其他對映的動態索引鍵。
* **物件的對應** — 包含具有固定結構描述之物件的動態金鑰。
* **對應陣列** — 包含具有動態索引鍵之對應的陣列。
* **物件陣列** — 包含具有固定結構描述的物件的陣列。
* **具有對應或陣列屬性的物件** — 包含對應或陣列欄位的物件。

### 欄位結構範例

下列結構可作為本指南中規則範例的視覺參考。

```
consent.marketing (Object)
├── email (Boolean)
├── sms (Boolean)
├── preferences (Map with dynamic keys)
│   ├── "email_preferences" (Object)
│   │   ├── frequency (String)
│   │   └── channels (Array of Strings)
│   ├── "sms_preferences" (Object)
│   │   ├── frequency (String)
│   │   └── opt_in_time (Date)
│   └── "push_preferences" (Object)
│       ├── frequency (String)
│       └── categories (Array of Strings)
└── lastUpdated (Date)
```

## 依欄位型別建立進階規則

請閱讀本節，瞭解根據欄位型別建立同意原則規則的詳細指引。 您將瞭解如何設定布林值、地圖、物件和陣列的規則邏輯，以擷取精確的同意條件。

### 規則建置元件和步驟

建立有效的同意原則規則需要瞭解如何導覽您的結構描述結構，並為每個欄位型別套用正確的運運算元。 每個規則都遵循相同的基本方法：導覽至基本欄位，選取適當的運運算元，並定義必須符合的條件。

請依照下列步驟建立規則：

1. **選取欄位** — 瀏覽容器欄位以存取基本欄位。
2. **選擇運運算元** — 選取欄位型別支援的運運算元。
   ![階層式結構描述導覽面板，顯示使用者將容器展開到基本欄位。](../images/policies/consent-policy-map-field.png)
3. **設定值** — 定義要符合的值或條件。
4. **比對對應金鑰** — 選擇是否鎖定特定金鑰，或比對對應中的所有金鑰。
5. **新增條件** — 視需要使用AND或OR邏輯來結合多個規則。

### 使用布林值欄位（隱含同意邏輯）

布林欄位會儲存true或false同意值，並代表最常見的同意屬性。 `is not equal to`運運算元可讓您包含未明確選擇退出的設定檔，支援隱含同意情況。

**布林運運算元與結果**

| 運算子 | 價值 | 結果 |
|----------|-------|--------|
| `is equal to` | `true` | 包含明確同意的設定檔(`true`)。 |
| `is equal to` | `false` | 包含具有明確選擇退出(`false`)的設定檔。 |
| `is not equal to` | `true` | 包含未經明確同意的設定檔（`false`或遺失）。 |
| `is not equal to` | `false` | 包含未明確選擇退出（`true`或遺失）的設定檔。 |

**範例：隱含的電子郵件同意**

```
Field: consent.marketing.email (boolean)
Operator: is not equal to
Value: false
Result: Includes profiles who have not explicitly opted out of email marketing (includes both true and missing/null values).
```

### 使用地圖欄位（動態偏好設定）

對應欄位會使用動態索引鍵儲存索引鍵值配對，不同於具有固定結構描述的物件。 地圖通常用於偏好設定中心，無需結構描述更新即可新增類別。 您可以鎖定特定金鑰或使用萬用字元比對所有金鑰。

**符合的特定金鑰**

使用此方法以特定偏好設定類別為目標。

```
Field: consent.preferences["email_preferences"].frequency (string) - navigated to from the map container
Operator: is equal to
Value: "weekly"
Result: Includes profiles who set the email frequency to weekly (for the "email_preferences" key)
```

**任何符合**&#x200B;的金鑰

使用&quot;**[!UICONTROL find any matching item]**&quot;核取方塊選項可比對對應中所有動態索引鍵。

![原則規則產生器顯示[對應]欄位的[尋找任何符合的專案]核取方塊，用來比對所有動態索引鍵的值。](../images/policies/find-any-matching-item.png)

```
Field: consent.preferences.*.frequency (string)
Operator: is equal to
Value: "weekly"
Result: Includes profiles who set frequency to weekly in ANY preference category (for example, email_preferences, sms_preferences, or push_preferences)
```

### 使用物件欄位（固定導覽）

物件欄位可作為包含固定結構描述的容器。 它們僅用於導覽，無法在原則條件中直接參照。

**導覽範例**

```
consent.marketing (object) → consent.marketing.email (boolean)
```

**範例使用案例：**

```
Field: consent.marketing.email (Boolean) - navigated to from the object
Operator: is equal to
Value: true
Result: Include profiles who have explicitly consented to marketing emails
```


### 使用陣列欄位（多個值）

陣列欄位包含相同型別的多個值，並且需要不同的處理，具體取決於它們是儲存原始值還是物件。 導覽和運運算元選項會因陣列型別而異。

**基本專案陣列範例**

使用`contains`運運算元，根據陣列中的特定值識別設定檔。

```
Field: consent.communication_channels (array of strings)
Operator: contains
Value: "email"
Result: Include profiles who have consented to email communication
```

**物件陣列範例**

瀏覽至陣列，以存取巢狀物件中的基本欄位。

```
Field: consent.preferences["email_preferences"].categories[].type - navigated to from the array
Operator: is equal to
Value: "promotional"
Result: Include profiles where any email category is "promotional"
```

## 結合規則與複雜邏輯

本節說明如何使用AND或OR邏輯來結合多個規則條件。 您將瞭解邏輯運運算元如何共同運作以定義進階、多條件同意原則。

### 結合多個條件（AND或OR邏輯）

您可以使用AND或OR邏輯來結合多個規則條件，以建立更複雜的同意政策，將目標鎖定在特定設定檔區段。\
**AND邏輯**&#x200B;要求所有條件都必須為true，才能產生較窄的相符對象。\
**OR邏輯**&#x200B;允許任何條件為true，擴大對象範圍。

在同意原則介面中，使用規則條件之間顯示的邏輯選取器，在AND和OR邏輯之間切換。

### 一般複雜規則範例

下列範例結合基本同意狀態與偏好設定頻率，以建立目標區段。

```
Field: consent.marketing.email
Operator: is equal to true
AND
Field: consent.preferences.frequency
Operator: is not equal to "daily"
Result: Include profiles who consent to email marketing but not to a daily frequency
```

### 物件陣列的進階邏輯

在物件陣列中組合條件時，行為取決於您在條件之間使用AND或OR邏輯。

**範例：具有AND條件的物件陣列**

當所有條件都必須套用至&#x200B;*相同*&#x200B;陣列元素時，請使用AND邏輯。

```
Field: consent.preferences["email_preferences"].categories[].enabled (boolean)
Operator: is equal to
Value: true
AND
Field: consent.preferences["email_preferences"].categories[].type (string)
Operator: is equal to
Value: "promotional"
Result: Includes profiles where the same category entry has both enabled=true and type="promotional".
Note: AND conditions apply to the same array entry. Using OR logic would include profiles if any array entry matches any of the conditions.
```

>[!TIP]
>
>**AND邏輯的最佳實務**
>
>在建置AND型陣列條件時，請謹記下列重要行為：
>
>* 當所有條件都必須套用至&#x200B;**相同的陣列專案**&#x200B;時，請使用AND邏輯。
>* 請記住，AND會建立限制性目標定位（相符的設定檔較少）。
>* 在多個陣列專案間請勿要求AND邏輯相符；此邏輯適用於每個專案。
>* 當您需要跨專案彈性比對時，請避免使用AND邏輯。

>[!IMPORTANT]
>
>使用AND邏輯時，每個陣列專案必須同時滿足所有指定的條件。 當您需要比對合併屬性時（例如已啟用和促銷的類別），這是最理想的作法。

>[!NOTE]
>
>AND邏輯僅適用於物件陣列，套用至相同的陣列專案&#x200B;**。**\
>若是基本陣列，會在整個陣列的欄位層級評估AND邏輯。

**範例：具有OR條件的物件陣列**

使用OR邏輯，允許陣列專案間的任何條件都為true，以建立內含對象符合。

```
Field: consent.preferences["email_preferences"].categories[].enabled (boolean)
Operator: is equal to
Value: true
OR
Field: consent.preferences["email_preferences"].categories[].type (string)
Operator: is equal to
Value: "newsletter"
Result: Includes profiles where any category entry has enabled=true or any entry has type="newsletter".
Note: OR logic allows matching across different array entries. One entry can meet the first condition while another meets the second.
```

### 後續步驟

在建立並修訂同意原則規則後，請使用下列資源完成設定、驗證原則執行並檢閱基礎資料模型。

* **原則建立工作流程**：使用[同意原則UI指南](user-guide.md#consent-policy.md)實作您在原則產生器UI中定義的規則
* **同意原則評估與執行**：確認啟用的原則如何影響對象啟用與設定檔資料使用。 如需詳細資訊，請參閱[自動原則執行指南](../enforcement/auto-enforcement.md)
* **XDM同意資料型別**：參考原則規則中使用的同意屬性的特定結構描述結構和欄位定義。 請參閱[XDM同意和偏好設定資料型別](../../xdm/data-types/consents.md)指南。
