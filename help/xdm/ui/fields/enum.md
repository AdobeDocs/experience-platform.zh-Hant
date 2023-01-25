---
keywords: Experience Platform；首頁；熱門主題；API; API; XDM; XDM系統；體驗資料模型；資料模型；ui；工作區；列舉；欄位；
solution: Experience Platform
title: 在UI中定義列舉欄位和建議的值
description: 了解如何為Experience Platform使用者介面中的字串欄位定義列舉和建議值。
exl-id: 67ec5382-31de-4f8d-9618-e8919bb5a472
source-git-commit: f770ba8668c5154b2cf5a57ba61d771ca34ab2d8
workflow-type: tm+mt
source-wordcount: '1358'
ht-degree: 0%

---

# 在UI中定義列舉和建議的值 {#enums-and-suggested-values}

>[!CONTEXTUALHELP]
>id="platform_xdm_enum_suggestedvalue"
>title="列舉與建議值"
>abstract="安 **列舉** 限制字串欄位，以僅允許內嵌符合一組預先定義值的資料。 可為每個枚舉約束分配 **顯示名稱** 填入「區段」UI中的屬性下拉式清單。 **建議的值** 的欄位不會限制擷取，而只會決定「細分」中顯示的顯示名稱。 如果您有多個架構共用屬於公用類或欄位組的欄位，並且在每個架構之間為該欄位定義不同的列號或建議值，則這些值會合併並附加至聯合架構中。"

在Experience Data Model(XDM)中，可為字串欄位指定一組預先定義的接受或建議值，以更妥善地控制要擷取到該欄位的值，或其在細分中的行為。

**[!UICONTROL 列舉]** 將字串欄位可擷取的值限制為預先定義的集。 如果您嘗試將資料內嵌至列舉欄位，而值不符合其設定中定義的任何欄位，則擷取將會遭到拒絕。

與列舉不同， **[!UICONTROL 建議的值]** option可為字串欄位指出一組建議的值，而不會限制其可內嵌的值。 反之，建議的值會影響 [區段UI](../../../segmentation/ui/overview.md) 將字串欄位納入為屬性時。

當 [定義新欄位](./overview.md#define) 在Adobe Experience Platform使用者介面中，並將類型設為 [!UICONTROL 字串]，您會獲得定義 [列舉](#enum) 或 [建議值](#suggested-values) 那塊地。

![為UI中的字串欄位啟用「列舉與建議的值」選項。](../../images/ui/fields/enum/enum-options-selected.png)

本檔案說明如何定義 [!UICONTROL 結構] UI工作區。 如需列舉和建議值的快速概覽，包括如何在UI中設定列舉及其下游效果，請觀看下列影片：

>[!VIDEO](https://video.tv.adobe.com/v/3409501/?quality=12&learn=on)

## 定義列舉 {#enum}

選擇 **[!UICONTROL 列舉和建議值]**，然後選取 **[!UICONTROL 列舉]**. 會出現其他控制項，可讓您指定列舉的值限制。 要添加約束，請選擇 **[!UICONTROL 新增列]**.

![在UI中選取的列舉選項。](../../images/ui/fields/enum/enum-add-row.png)

在 **[!UICONTROL 值]** 欄，您必須提供要將欄位限制為的確切值。 您可以選擇提供人性化 **[!UICONTROL 顯示名稱]** 限制，這會影響值在分段中的表示方式。

繼續使用 **[!UICONTROL 新增列]** 若要將所需的限制和選用標籤新增至列舉，或選取刪除圖示(![刪除圖示的影像](../../images/ui/fields/enum/remove-icon.png))，以將其移除。 完成後，請選取 **[!UICONTROL 套用]** 將更改應用到架構。

![為UI中的字串欄位填入的列舉值和顯示名稱。](../../images/ui/fields/enum/enum-confirm.png)

畫布會更新以反映變更。 日後探索此架構時，您可以在右側邊欄中檢視及編輯列舉欄位的限制。

## 定義建議的值 {#suggested-values}

選擇 **[!UICONTROL 列舉和建議值]**，然後選取 **[!UICONTROL 建議的值]** 以顯示其他控制項。 從此處，選擇 **[!UICONTROL 新增列]** 開始添加建議值。

![在UI中選取的「建議值」選項。](../../images/ui/fields/enum/suggested-add-row.png)

在 **[!UICONTROL 顯示名稱]** 欄，提供您要值顯示在「細分」UI中的好記名稱。 若要新增更多建議值，請選取 **[!UICONTROL 新增列]** 再次，並視需要重複此程式。 若要移除先前新增的列，請選取 ![「刪除」圖示](../../images/ui/fields/enum/remove-icon.png) 旁邊。

完成後，請選取 **[!UICONTROL 套用]** 將更改應用到架構。

![為UI中的字串欄位填入的列舉值和顯示名稱。](../../images/ui/fields/enum/suggested-confirm.png)

>[!NOTE]
>
>欄位的更新建議值會延遲約五分鐘，以反映在分段UI中。

### 管理標準欄位的建議值 {#standard-fields}

標準XDM元件中的某些欄位會包含自己的建議值，例如 `eventType` 從 [[!UICONTROL XDM ExperienceEvent] 類](../../classes/experienceevent.md) 您也可以以自訂欄位相同的方式，為這些標準欄位建立其他建議值。 您也可以停用任何不符合您使用案例的標準建議值，但無法從欄位定義中直接移除這些值。

>[!IMPORTANT]
>
>您只能針對沒有對應列舉限制的標準欄位停用建議的值。 換句話說，如果 **[!UICONTROL 列舉]** 選項，而非啟用 **[!UICONTROL 建議的值]**，則欄位會限制為列舉，且這些限制無法停用。
>
>請參閱 [下文](#evolution) 以取得更新現有架構欄位的列舉和建議值之規則的詳細資訊。

若要停用標準建議值，請選取相關值旁的切換按鈕。 您可以停用建議值的任何組合，包括所有值。

![部分標準建議值 [!UICONTROL 事件類型] 欄位在UI中已停用。](../../images/ui/fields/enum/suggested-standard.png)

若要為標準欄位新增建議的值，請選取 **[!UICONTROL 新增列]**. 若要移除組織先前新增的建議值，請選取 ![「刪除」圖示](../../images/ui/fields/enum/remove-icon.png) 旁邊。

![新增至UI中標準字串欄位的自訂建議值。](../../images/ui/fields/enum/suggested-standard-add.png)

## 列舉和建議值的演化規則 {#evolution}

使用具有列舉欄位的架構將資料內嵌至Platform後，對架構定義所做的任何進一步變更都必須符合系統中已有的資料。 一般而言，對現有欄位所做的變更只能建立該欄位 **less** 限制性。 欄位的限制性不能比現在更強。

關於列舉和建議的值，下列規則會套用擷取後：

* 您 **可** 將建議值新增至任何具有現有建議值的欄位。
* 您 **可** 從具有現有建議值的欄位中移除自訂建議值。
* 您 **可** 在欄位中停用僅包含建議值且沒有列舉限制的標準建議值。
* 您 **可** 為現有的自訂列舉欄位新增列舉值。
* 您 **可** 僅將自訂欄位的列舉值切換為建議值，或將其轉換為沒有列舉或建議值的字串。 **此開關一經套用便無法復原。**
* 您 **無法** 從標準欄位新增或移除列舉限制。
* 您 **無法** 從標準欄位中移除建議的值（僅限停用）。
* 您 **無法** 將列舉限制新增至沒有現有列舉的欄位。
* 您 **無法** 移除自訂欄位的「少於所有現有列舉」限制。
* 您 **無法** 從建議值切換為列舉。

## 合併列舉和建議值的規則 {#merging}

如果多個結構使用具有不同設定的相同列舉欄位，且這些結構包含在聯合中，則當有關列舉差異的調解方式，會套用某些規則。 確切的規則取決於參考相同標準欄位的結構(例如 `eventType`)，或是他們參考不同欄位群組中相同的自訂欄位路徑。

如果參考相同的標準欄位：

* 任何其他建議的值 **已附加** 在工會里。
* 對相同列舉索引鍵的建議值進行更新為 **已更新** 在工會里。

如果在不同的欄位群組中參考相同的自訂欄位路徑：

* 任何其他建議的值 **已附加** 在工會里。
* 如果在多個架構中定義了相同的其他建議值，則這些值為 **已合併** 在工會里。 換句話說，合併後相同的建議值不會顯示兩次。

## 驗證限制

由於目前的系統限制，在擷取期間，有兩種情況下系統未驗證列舉：

1. 列舉是在 [陣列欄位](./array.md).
1. 枚舉在架構層次結構中定義了多個深層。

## 後續步驟

本指南說明如何在UI中定義字串欄位的列舉和建議值。 有關如何使用Schema Registry API管理列舉和建議值的資訊，請參閱以下內容 [教學課程](../../tutorials/suggested-values.md).

若要了解如何在 [!DNL Schema Editor]，請參閱 [定義UI中的欄位。](./overview.md#special).
