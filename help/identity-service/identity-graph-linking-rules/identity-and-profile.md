---
title: Identity Service和即時客戶個人檔案
description: 瞭解Identity Service和即時客戶個人檔案之間的關係
hide: true
hidefromtoc: true
source-git-commit: 026f0dee203dd9d7f23d3343025665313692efbe
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 1%

---

# 瞭解Identity Service與即時客戶個人檔案之間的關係

>[!IMPORTANT]
>
>此頁面假設合併原則正在使用身分圖表。 如需即時客戶個人檔案中合併原則的詳細資訊，請參閱以下檔案： [合併原則與身分拼接](../../profile/merge-policies/overview.md#identity-stitching).

雖然您可以同時使用Identity Service和即時客戶個人檔案，但Adobe Experience Platform的這兩項功能本身並不相同。

* 您可以使用Identity Service來產生及維護身分圖表，將個別客戶的不同身分整合在一起。
* 您可以使用即時客戶個人檔案，將不同的個人檔案片段放在一起，並建立合併的個人檔案。 此程式需要使用身分圖表。

本檔案概述Identity Service與即時客戶個人檔案之間的相似性、差異和關係。

## Identity Service與即時客戶個人檔案的比較

Identity Service和即時客戶設定檔之間的主要差異如下：

| | 身分識別服務 | 即時客戶設定檔 |
| --- | --- |--- |
| **用途** | <ul><li>您可以使用Identity Service來建立和管理身分圖表。</li></ul> | 您可以使用即時客戶個人檔案： <ul><li>建立客戶設定檔的360度檢視。</li><li>檢視和管理設定檔</li><li>區隔設定檔以建立對象。</li></ul> |
| **輸入** | <ul><li>若要使用Identity Service，您必須擷取至少有兩個標示為身分的欄位的記錄資料或時間序列事件。 接著，您標籤為身分的欄位會擷取至Identity Service。</li></ul> | **若要合併設定檔，您必須提供**： <ul><li>設定檔片段：代表指定資料集中該ID的唯一主要身分和對應的記錄或事件資料。</li><li>身分圖：設定檔會參照指定客戶設定檔的身分圖，以識別具有相同主要身分的所有設定檔片段。</li></ul> **如需區段資格，您必須提供**： <ul><li>合併的設定檔：合併的設定檔是客戶的單一檢視，其中不同的設定檔片段和身分會收集到一個完整的檢視中。</li></ul> |
| **程序** | <ul><li>一旦您擷取到至少兩個身分，Identity Service就會將這些身分連結在一起。</li></ul> | <ul><li>即時客戶設定檔會合併設定檔片段，同時參考其對應的身分圖表。</li><li>根據細分條件限定設定檔的區段</li></ul> |
| **Output** | <ul><li>結果會產生身分圖表，這是與個人相關的一組身分。</li></ul> | <ul><li>結果是合併的設定檔，這是特定客戶的單一全面檢視。</li><li>已定義具有區段會籍的設定檔</li></ul> |

{style="table-layout:auto"}

>[!BEGINSHADEBOX]

## 如何建立合併的設定檔？

請閱讀下列步驟，以更加瞭解建立合併設定檔的過程：

* 首先，即時客戶設定檔會參考身分圖表並擷取所有身分。
* 接著，設定檔會擷取與每個身分識別相關的所有設定檔片段。
* 成功後，設定檔合併所有現有事件和屬性。
   * 如有需要，可套用優先順序規則以決定要使用的屬性或事件

![詳述Identity Service和設定檔合併運作方式的流程圖。](../images/identity-settings/identity-and-profile.png)

>[!ENDSHADEBOX]

### 將欄位標示為身分是什麼意思？

若要將某個欄位標示或指定為身分，會指示Experience Platform將該特定欄位擷取至Identity Service。 然後，這種指定允許在即時客戶個人檔案中合併個人檔案片段。 如果沒有與身分相關聯的設定檔片段，則請勿將其指定為身分。

#### 瞭解主要和次要身分

將欄位標示為身分後，即可將其定義為主要或次要身分。 主要和次要身分是即時客戶個人檔案中的概念。

* 主要身分（有時稱為「主要金鑰」）是設定檔片段儲存所在的身分。
* 如果指定資料列中只有一個身分，則該單一身分會指定為主要身分。
* 如果有兩個或多個身分，則將其中一個指定為主要身分，其餘的則指定為次要身分。

Identity Service只會擷取指定為身分的欄位。 Identity Service不會儲存有關身分是主要身分還是次要身分的資訊。

## 後續步驟

如需身分圖表連結規則的詳細資訊，請參閱下列檔案：

* [身分圖表連結規則概觀](./overview.md)
* [設定身分圖表連結規則的範例案例](./example-scenarios.md)
* [身分連結邏輯](./identity-linking-logic.md)