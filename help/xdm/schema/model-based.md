---
keywords: Experience Platform；首頁；熱門主題；模型架構；關聯式架構；關聯式架構；架構；架構；xdm；體驗資料模型；
solution: Experience Platform
title: 以模型為基礎的結構描述
description: 瞭解Adobe Experience Platform中以模型為基礎的結構描述（也稱為關聯式結構描述），包括功能、必填欄位、關係和限制。
badge: 有限可用性
exl-id: 397e5937-b892-4fd3-b90e-29ed9229dc69
source-git-commit: 4586a820556919aeb6cebd94d961c3f726637f16
workflow-type: tm+mt
source-wordcount: '1306'
ht-degree: 0%

---

# 以模型為基礎的結構描述

>[!AVAILABILITY]
>
>Adobe Journey Optimizer **協調的行銷活動**&#x200B;授權持有人可使用Data Mirror和模型型結構描述。 視您的授權和功能啟用而定，它們也可作為Customer Journey Analytics使用者的&#x200B;**有限版本**&#x200B;提供。 請聯絡您的Adobe代表以取得存取權。

以模型為基礎的結構描述提供靈活、受控制的模型模式，用於表示Adobe Experience Platform Data Lake中的結構化資料。 它們支援強制的主索引鍵、綱要層級關係，以及對記錄的精細控制，而完全不依賴聯合綱要或完整的關聯式資料庫系統。

>[!IMPORTANT]
>
>資料刪除考量事項適用於所有以模型為基礎的結構描述實作。 使用這些結構描述的應用程式必須瞭解刪除如何影響相關資料集、法規遵循需求和下游流程。 規劃刪除案例，並在實作前檢閱[資料衛生指南](../../hygiene/ui/record-delete.md#model-based-record-delete)。

>[!NOTE]
>
>在請求關聯式資料模型化使用案例的結構描述建立時，應用程式可能會將基於模型的結構描述稱為「關聯式結構描述」。

使用以模型為基礎的結構描述可以：

* 使用強制的單欄位或複合主索引鍵確保資料完整性。
* 使用版本設定來啟用插入、更新和刪除的精確變更追蹤。
* 定義可重複使用的結構描述層級關係來模擬真實世界的實體連線。
* 藉由支援多個資料模型，避免跨應用程式複製結構描述結構。
* 略過聯合結構描述限制以簡化上線、減少結構描述膨脹，並避免不需要的結構描述變更。

## 以模型為基礎的結構描述與標準XDM結構描述有何不同

Experience Platform中的標準XDM結構描述會遵循下列三種資料行為之一：記錄、時間序列或臨機。 如需定義和詳細資訊，請參閱[XDM資料行為](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home#data-behaviors)。

在傳統模型中，記錄和時間序列結構描述參與[聯合結構描述](../api/unions.md) （另請參閱[聯合結構描述UI指南](../../profile/ui/union-schema.md)）。 這些結構描述會隨著共用[欄位群組](./composition.md#field-group)的更新而自動演化，且自訂欄位必須巢狀置於租使用者名稱空間下。 此模型雖然功能強大，但可能會拖慢上線速度、產生包含未使用欄位且過於複雜的結構描述，並需要額外的資料對應或轉換。 這些因素會增加學習曲線以及持續的維護工作。

基於模型的結構描述移除聯合結構描述相依性，這會從共用欄位群組中消除自動更新，並允許直接欄位定義而沒有租使用者名稱空間限制。 您可以明確控制主索引鍵、關係和初始方案設計，更輕鬆地根據建立時的需求對資料建模。

## 模型架構的功能

使用下列功能來模型化Data Lake中的結構化資料，同時維護治理、完整性和互用性。

* **結構描述行為支援**：設定為：
   * **記錄行為**：擷取實體（例如客戶、帳戶或促銷活動）的目前狀態。
   * **時間序列行為**：擷取事件及其發生時間，用於追蹤序列或隨時間發生的變更。
* **主要金鑰強制執行**：定義主要金鑰以唯一識別每個記錄，並防止擷取期間出現重複專案。
* **版本控制**：使用&#x200B;**版本識別碼** （描述項），確保更新以正確順序套用，即使記錄未按順序送達。
* **關聯對應**：在基於模型的結構描述之間或基於模型的結構描述與標準結構描述之間，建立一對一或多對一的關係。 關係定義會儲存為描述元，以啟用有效率的結合。
* **簡化的演化**：以模型為基礎的結構描述不會參與聯合檢視，而且在共用欄位群組變更時也不會更新，以防止意外的下游變更。
* **彈性欄位定義**：直接新增沒有租使用者ID名稱空間的欄位。 以模型為基礎的結構描述不支援XDM欄位群組。
* **聯合結構描述沒有相依性**：改善查詢效能，並減少管理全域結構描述檢視的作業額外負荷。
* **事件時間順序**：對於時間序列結構描述，請使用&#x200B;**時間戳記識別碼**&#x200B;來依發生時間而非擷取時間排序事件。

## 必填欄位

以模型為基礎的結構描述需要某些描述元，也就是結構描述定義中控制關鍵行為和限制的中繼資料。 在結構描述定義中新增下列描述項。

### 主索引鍵描述項

使用主索引鍵描述項來確保每個記錄都是唯一可識別的。 支援的設定包括：

* **單一欄位主索引鍵**：針對每個記錄使用一個具有唯一值的欄位。
* **複合主索引鍵**：使用多個欄位來形成唯一識別碼。 對於時間序列結構描述，複合金鑰必須包含由時間戳記描述項識別的時間戳記欄位。

>[!NOTE]
>
>在UI結構描述編輯器中，版本描述項和時間戳記描述項分別顯示為&quot;[!UICONTROL 版本識別項]&quot;和&quot;[!UICONTROL 時間戳記識別項]&quot;。

**範例（單一欄位）：**

```json
{
  "xdm:descriptor": "xdm:descriptorPrimaryKey",
  "xdm:sourceProperty": "customerId"
}
```

**範例（時間序列複合）**

```json
{
  "xdm:descriptor": "xdm:descriptorPrimaryKey",
  "xdm:sourceProperty": ["customerId", "eventTimestamp"]
}
```

### 版本描述項（識別碼）

定義版本描述項（識別碼）以維持正確的記錄狀態並確保套用最新的更新。 當多個記錄共用相同的主索引鍵時，具有最高版本值的記錄會被視為最新記錄。

**範例：**

```json
{
  "xdm:descriptor": "xdm:descriptorVersion",
  "xdm:sourceProperty": "lastModified"
}
```

### 時間戳記描述項（識別碼）

對於時間序列結構描述，請定義時間戳記描述項（識別碼）來設定事件時間以便排序。

**範例：**

```json
{
  "xdm:descriptor": "xdm:descriptorTimestamp",
  "xdm:sourceProperty": "eventTimestamp"
}
```

>[!NOTE]
>
>描述項是結構描述定義中繼資料的一部分，不會儲存在資料列中。

如需在結構描述編輯器中建立描述項的指示，請參閱[在結構描述編輯器中建立描述項](../tutorials/relationship-ui.md)。 如需以API為基礎的建立，請參閱[使用API建立描述元](../tutorials/relationship-api.md)。

## 關係支援 {#relationship-support}

關聯式資料模型化是以模型為基礎的結構描述的主要用途。 應用程式使用案例甚至可能將這些方案稱為「關聯式方案」。 關係描述項透過連結跨結構描述的資料集來啟用這些連線，而不需在資料列中嵌入外部索引鍵。 它們可改善參考完整性、啟用可重複使用的模型模式，並支援跨應用程式的連線查詢。

在結構描述層級建立關係描述項，以在查詢時動態解析。 基數值（1:1，多對一）會提供指引，但不會在擷取期間強制執行限制，支援跨連線資料集的彈性資料模型。

在新增關係描述項之前，請先決定適當的型別和目標：

* **一對一** — 來源結構描述中的每個記錄最多只對應到目的地結構描述中的一個記錄。
* **多對一** — 來源結構描述中的多個記錄可能會參考目的地結構描述中的相同記錄。

>[!NOTE]
>
>您可以定義兩個以模型為基礎的結構描述之間的關係，或是以模型為基礎的結構描述和標準結構描述之間的關係。 不支援與臨時結構描述的關係。

<!-- Q) 
Madeline commented: "model-based schema to standard might only be offered for b2b customers; that's how it will be on the UI" - is that still accurate? -->

**範例：一對一關係**

```json
{
  "xdm:descriptor": "xdm:descriptorRelationship",
  "xdm:sourceProperty": "accountId",
  "xdm:destinationSchema": "https://ns.adobe.com/xdm/context/account",
  "xdm:destinationProperty": "accountId"
}
```

<!-- Q) 
Should these be `@type: "xdm:descriptorRelationship",` This could be a copy-pasting error? -->

**範例：多對一關係**

```json
{
  "xdm:descriptor": "xdm:descriptorRelationship",
  "xdm:sourceProperty": "customerId",
  "xdm:destinationSchema": "https://ns.adobe.com/xdm/context/customer",
  "xdm:destinationProperty": "customerId"
}
```

如需關聯性描述項型別和語法的清單，請參閱[描述項API參考](../api/descriptors.md)。若要瞭解如何在實踐中套用這些概念，請遵循教學課程以[在API中定義關聯性](../tutorials/relationship-api.md)或[在UI中建立關聯性](../tutorials/relationship-ui.md)。

>[!NOTE]
>
>由於關係是在結構描述層級定義，請務必明確聯結查詢中的相關資料集。 使用Data Distiller之類的工具，在查詢期間解決這些關係。

>[!IMPORTANT]
>
>關係基數是資訊性質，在擷取期間不會強制執行。 它僅在查詢或分析期間解析關係時套用。 在內嵌期間，請勿依賴基數設定來驗證資料。 自行檢查並清除資料，並確認您定義的關係規則符合您要查詢或分析資料的方式。

>[!NOTE]
>
> 以模型為基礎的結構描述可以連結到標準結構描述，但無法連結到臨時結構描述。

## 資料刪除和衛生考量事項 {#data-hygiene-support}

以模型為基礎的結構描述可精確刪除記錄層級，這些刪除對所有應用程式和使用案例具有普遍影響。 主要金鑰、版本和時間戳記描述項為刪除作業期間準確識別記錄奠定了基礎。

### 通用刪除影響

所有使用模型架構的應用程式都必須考慮：

* **參考完整性**：刪除可能會影響跨連線資料集的相關記錄
* **法規遵循需求**：某些產業需要特定的刪除行為和稽核軌跡
* **應用程式行為**：下游系統可能需要適當地處理刪除事件
* **資料一致性**：刪除作業期間相關資料集必須維持一致性
* **刪除計畫**：說明設計階段所有連線資料集和應用程式的下游影響

如需實作指南，請參閱[從模型資料集刪除記錄](../../hygiene/ui/record-delete.md#model-based-record-delete)。

## 限制和考量事項 {#limitations}

在使用模型架構之前，請先檢閱下列限制：

* 以模型為基礎的結構描述不參與聯合結構描述。
* 結構描述演化是手動的；它們不會在欄位群組變更時自動更新。

>[!IMPORTANT]
>
>使用結構描述初始化資料集後，結構描述演化會受到限制。 請事先謹慎規劃欄位名稱和型別，因為一旦擷取資料，就無法刪除或修改欄位。

* 關係限於一對一和多對一。
* 可用性取決於您的授權或功能啟用。
* 時間序列結構需要複合主索引鍵。
