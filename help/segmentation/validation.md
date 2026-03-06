---
title: 對象驗證
description: 瞭解Experience Platform如何驗證您的對象，以確保它們在下游的表現良好。
exl-id: 55877ad5-757f-4928-853c-3b211ece0a45
source-git-commit: 2d7ba15f918c314fe219212df82aec6d7ac1fc77
workflow-type: tm+mt
source-wordcount: '1630'
ht-degree: 13%

---

# 對象驗證

當您在Adobe Experience Platform中編寫對象定義時，對象驗證會提供內建的驗證和護欄，以確保您的對象不僅準確，而且穩定且可擴充。

透過遵循對象定義最佳實務，您可以確保對象可更快地評估，確保您的邏輯即使對象人數增加仍有效率，並降低高流量期間評估失敗的風險。 最佳化的對象也可提高目的地的啟用速度、減少即時個人化延遲，並維持整體沙箱穩定性。

當您在「區段產生器」中建立對象時，Experience Platform會即時執行這些驗證。 新增超過驗證臨界值的事件或屬性時，您會在「區段產生器」介面中立即收到回饋。

## 驗證型別 {#validation-types}

當對象驗證在您的對象上執行時，可能會違反兩種不同型別的建構：重要驗證建構和效能最佳化建構。

如果違反了關鍵驗證結構，系統將阻止您儲存對象以保護沙箱的穩定性。 如果違反了效能最佳化建構，您就可以儲存您的對象，但&#x200B;*強烈建議您更新對象定義以避免效能問題*。

## 驗證檢查 {#validation-checks}

目前支援下列驗證：

| 驗證檢查 | 類型 | 臨界值 |
| ---------------- | ---- | --------- |
| 邏輯複雜性 | 關鍵驗證 | 對象定義包含太多查詢，導致不必要的邏輯複雜性。 |
| 循序事件 | 關鍵驗證 | 對象定義中有6個以上的循序事件。 |
| 彙總計數 | 效能最佳化 | 對象定義中有超過3個彙總函式。 |
| 巢狀資料 | 效能最佳化 | 對象定義中有超過2個層級的巢狀資料（陣列或地圖資料型別）深度。 |
| 對象規模 | 效能最佳化 | 對象資格大小超過沙箱中設定檔總數的30%。 |

### [!BADGE 關鍵驗證]{type=Negative}邏輯複雜性 {#logical-complexity}

>[!CONTEXTUALHELP]
>id="platform_segmentation_segmentbuilder_rewritescheck"
>title="查詢效率警報"
>abstract="您的客群包含太多查詢，導致不必要的邏輯複雜性。請先簡化您的客群定義，然後再繼續。"

>[!CONTEXTUALHELP]
>id="platform_segmentation_segmentbuilder_cnfcomplexitycheck"
>title="邏輯複雜性"
>abstract="您的客群包含太多查詢，導致不必要的邏輯複雜性。請先簡化您的客群定義，然後再繼續。"

邏輯複雜度驗證會分析對象定義中邏輯陳述式(AND、OR、NOT)的結構。 具體來說，它會尋找會強制系統為每個設定檔執行過多比較的受眾定義。

如果您的對象定義在每個設定檔中有過多比較次數，這種增加複雜性會導致每個設定檔的評估變慢。 因此，這增加了對象評估的整體所用時間。

若要避免觸發此驗證，請簡化您的對象定義。 如果您無法瞭解自己的對象定義，則會過於複雜，而Experience Platform可能需要更長的時間來評估對象。

**範例**

假設您想要尋找生活在特定狀態的客戶。 您&#x200B;_可能會_&#x200B;藉由檢查設定檔是否有符合清單45個值之一之狀態的值，而造成寫入效率低下，如下所示：

+++ 對象定義效率低下

```
State.equals("AL", "AK", "AZ", "AR", "CA", "CO", "CT", "DE", "FL", "GA","HI", "ID", "IL", "IN", "IA", "KS", "KY", "LA", "ME", "MD", "MA", "MI", "MN", "MS", "MO", "MT", "NE", "NV", "NH", "NJ", "NM", "NY", "NC", "ND", "OH", "OK", "OR", "PA", "RI", "SC", "SD", "TN", "TX", "UT")
```

+++

不過，若使用not check ，您只需要檢查設定檔是否沒有列出的5個值之一，即可產生更有效率的查詢。

+++ 有效的受眾定義

```
not(State.equals("VT", "VA", "WA", "WV", "WI", "WY" ))
```

+++

或者，假設您想要尋找在您的試用計畫中屬於加拿大人的客戶。 較不有效率的方法是手動逐一排除所有其他計畫，並檢查設定檔是否不在任何計畫中，以在您的試用計畫中尋找加拿大人。

+++ 對象定義效率低下

```
NOT(
    plan.equals("basic") OR
    plan.equals("standard") OR
    plan.equals("premium") OR
    plan.equals("enterprise")
) AND NOT (
    region.equals("us-east") OR
    region.equals("us-west") OR
    region.equals("eu-central") OR
    region.equals("apac")
)
```

+++

相反地，您應該採取直接的態度，並鎖定您要納入的特定計畫。

+++ 有效的受眾定義

```
plan.equals("trial") AND region.equals("canada")
```

+++

### [!BADGE 關鍵驗證]{type=Negative}序列事件複雜性 {#sequential-event-complexity}

>[!CONTEXTUALHELP]
>id="platform_segmentation_segmentbuilder_chaincountcheck"
>title="事件序列限制"
>abstract="您的客群包含太多序列事件。客群定義中最多只能有 6 個序列事件。請先從客群定義中移除一些序列事件，然後再繼續。"

循序事件複雜性驗證將序列中的循序事件數量限製為6個事件。

循序細分是Experience Platform中運算最複雜的作業之一，因為系統需掃描客戶的體驗事件完整歷史記錄、依時間戳記排序，以及驗證指定的順序是否符合您的查詢。 因此，當鏈增長時，系統需要計算的排列數會大幅增加。

若要避免觸發此驗證，請透過定義歷程的開頭、中間和結尾，專注於循序鏈的基本知識。 立即步驟通常隱含在最終轉換中。

**範例**

假設您想要鎖定檢視過產品、將產品新增至購物車並購買產品的使用者。 效率較低的方法會檢查使用者路徑的每個個別狀態。 例如，下列查詢會經過以下事件順序：登入網站 — >搜尋產品 — >檢視產品頁面 — >新增至購物車 — >導覽至結帳 — >購買事件

+++ 對象定義效率低下

```
chain(xEvent, timestamp, [ A: WHAT(eventType = "login"), B: WHAT(eventType = "search"), C: WHAT(eventType = "productView"), D: WHAT(eventType = "addToCart"), E: WHAT(eventType = "checkout"), F: WHAT(eventType = "purchase") ])
```

+++

但是，將序列減少到其開頭、中間和結尾，您只需要擁有3個事件長度的事件序列，即可產生更有效率的查詢。 例如，以下查詢會經過此事件序列：檢視產品頁面 — >新增到購物車 — >購買事件

+++ 有效的受眾定義

```
chain(xEvent, timestamp, [ A: WHAT(eventType = "productView"), B: WHAT(eventType = "addToCart"), C: WHAT(eventType = "purchase") ])
```

+++

### [!BADGE 效能最佳化]{type=Caution}彙總計數 {#aggregated-count}

>[!CONTEXTUALHELP]
>id="platform_segmentation_segmentbuilder_countaggregationcheck"
>title="計數篩選器警告"
>abstract="您的客群具備太多彙總事件。客群中最多僅應使用 3 個彙總事件。為避免效能問題，您應該從客群定義中移除一些彙總事件。"

彙總計數檢查將對象內使用的彙總事件數限製為3個條件。

標準事件只需要尋找單一相符事件，即可讓使用者符合資格。 但是，彙總事件必須先讀取和分析使用者的&#x200B;**整個事件歷史記錄**，才能做出決定，導致處理時間變慢，而使用更多彙總事件。

為避免觸發此驗證，僅在對象定義完全必要時使用特定計數。 例如，如果您只需要知道使用者是否參與一次，您可以使用標準「存在」邏輯，而不使用「計數> 0」事件。

### [!BADGE 效能最佳化]{type=Caution}巢狀資料複雜性 {#nested-data-complexity}

>[!CONTEXTUALHELP]
>id="platform_segmentation_segmentbuilder_arraydepthcheck"
>title="巢狀資料警告"
>abstract="您的客群具備太多巢狀資料層。客群中最多僅應使用 2 層資料。為避免效能問題，您應該將客群定義平面化。"

巢狀資料複雜性驗證會將對象定義中的巢狀資料數量限製為2層。

雖然Experience Platform支援使用陣列和對應物件來儲存複雜的資料型別，但解壓縮巢狀結構以尋找值需要更複雜的周遊邏輯。 巢狀資料越深入於陣列中，擷取以進行驗證所需的時間就越長。

如果您經常對深層巢狀屬性執行分段，您可能需要聯絡資料工程團隊，將屬性複製到設定檔結構描述中的更高層級，以方便存取。

### [!BADGE 效能最佳化]{type=Caution}客群規模 {#audience-size}

>[!CONTEXTUALHELP]
>id="platform_segmentation_segmentbuilder_profilestorecheck"
>title="客群規模警告"
>abstract="您的客群寫得過於寬泛。客群定義應該避免符合對象達到沙箱中輪廓總數 30% 以上。為避免效能問題，您應該將客群定義限縮。"

對象人數驗證會檢查您的對象定義是否廣泛，以致於您的沙箱中超過30%的總設定檔符合對象的資格。

雖然Experience Platform可以處理大量受眾，但太模糊的受眾定義（例如所有活躍客戶）可能會增加評估時間和啟用延遲。

如果您需要建立符合設定檔存放區中30%以上資格的受眾，請確保使用彈性的受眾評估來完成受眾的首次評估。 透過隨選評估來評估對象，可以降低大量對象對日常細分工作的整體影響。

## 後續步驟

閱讀本指南後，您就能更瞭解Experience Platform如何執行自動驗證，以改進評估、穩定性和擴充性。 如需使用UI建立對象的詳細資訊，請參閱[區段產生器檔案](./ui/segment-builder.md)。

## 附錄

下列附錄列出有關Experience Platform中對象驗證的常見問題。

### 常見問題 {#faq}

**如果忽略警告並儲存對象，會發生什麼事？**

+++ 回答

針對效能最佳化警告，將會儲存對象且系統會嘗試評估對象。 不過，處理時間可能會顯著變慢。 在極端情況下，如果資料量夠高，細分工作可能會失敗或逾時，並強制您重新設計對象。

發生嚴重驗證錯誤時，您將無法儲存閱聽眾。

+++

**我可以要求增加至「循序事件」上限嗎？**

+++ 回答

不行。 這是硬護欄，專為保護整個Experience Platform環境的穩定性而設計。 如果您的序列需要超過6個步驟，這是將此邏輯簡化或分成兩個不同對象（例如「參與」對象和「轉換」對象）的有力指標。

+++

**這些新驗證會破壞我現有的對象嗎？**

+++ 回答

這些驗證會在&#x200B;**編寫**&#x200B;時執行。 因此，您現有的對象將會繼續依原樣執行。 不過，如果您嘗試編輯違反這些規則的現有對象，則必須先最佳化對象，才能儲存變更。

+++

**我有複雜的資料需求。 如何避免「巢狀資料」警告？**

+++ 回答

避免「巢狀資料」警告的最佳方式是在資料模型層解決。 部分秘訣包括與您的資料工程團隊合作，以平面化XDM結構描述，並將關鍵屬性（例如`subscriptionStatus`和`loyaltyTier`）帶至設定檔的最上層。

+++

**這些檢查是否同時適用於草稿和已發佈的對象？**

+++ 回答

是，這些檢查適用於Experience Platform中評估的&#x200B;*所有*&#x200B;對象。

+++
