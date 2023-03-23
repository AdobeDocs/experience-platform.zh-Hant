---
keywords: Experience Platform；首頁；熱門主題；API; API; XDM; XDM系統；體驗資料模型；資料模型；ui；工作區；列舉；欄位；
solution: Experience Platform
title: 在UI中定義列舉欄位和建議的值
description: 了解如何為Experience Platform使用者介面中的字串欄位定義列舉和建議值。
exl-id: 67ec5382-31de-4f8d-9618-e8919bb5a472
source-git-commit: a3140d5216857ef41c885bbad8c69d91493b619d
workflow-type: tm+mt
source-wordcount: '1257'
ht-degree: 8%

---

# 在UI中定義列舉和建議的值 {#enums-and-suggested-values}

>[!CONTEXTUALHELP]
>id="platform_xdm_enum_suggestedvalue"
>title="列舉和建議值"
>abstract="**列舉**&#x200B;會將字串欄位限制為只能擷取和一組預先定義的值相符的資料。可對每個列舉限制式指派一個&#x200B;**顯示名稱**，這會在分段 UI 中填入屬性下拉式清單。欄位的&#x200B;**建議值**&#x200B;不會限制擷取，只會判斷分段中顯示的顯示名稱。如果您有多個方案共用一個屬於通用類別或欄位群組的欄位，並且您對每個方案之間的該欄位定義了不同的列舉或建議值，則這些值將合併並附加到聯合方案中。"

在Experience Data Model(XDM)中，可為字串欄位指定一組預先定義的接受或建議值，以更妥善地控制要擷取到該欄位的值，或其在細分中的行為。

**[!UICONTROL 列舉]** 將字串欄位可擷取的值限制為預先定義的集。 如果您嘗試將資料內嵌至列舉欄位，而值不符合其設定中定義的任何欄位，則擷取將會遭到拒絕。

與列舉不同， **[!UICONTROL 建議的值]** option可為字串欄位指出一組建議的值，而不會限制其可內嵌的值。 反之，建議的值會影響 [區段UI](../../../segmentation/ui/overview.md) 將字串欄位納入為屬性時。

當 [定義新欄位](./overview.md#define) 在Adobe Experience Platform使用者介面中，並將類型設為 [!UICONTROL 字串]，您會獲得定義 [列舉](#enum) 或 [建議值](#suggested-values) 那塊地。

![在UI中為字串欄位啟用「列舉與建議值」選項的影像](../../images/ui/fields/enum/enum-options-selected.png)

本檔案說明如何定義 [!UICONTROL 結構] UI工作區。 如需列舉和建議值的快速概覽，包括如何在UI中設定列舉及其下游效果，請觀看下列影片：

>[!VIDEO](https://video.tv.adobe.com/v/3409501/?quality=12&learn=on)

## 定義列舉 {#enum}

選擇 **[!UICONTROL 列舉和建議值]**，然後選取 **[!UICONTROL 列舉]**. 會出現其他控制項，可讓您指定列舉的值限制。 要添加約束，請選擇 **[!UICONTROL 新增列]**.

![顯示UI中選取之列數選項的影像](../../images/ui/fields/enum/enum-add-row.png)

在 **[!UICONTROL 值]** 欄，您必須提供要將欄位限制為的確切值。 您可以選擇提供人性化 **[!UICONTROL 顯示名稱]** 限制，這會影響值在分段中的表示方式。

繼續使用 **[!UICONTROL 新增列]** 若要將所需的限制和選用標籤新增至列舉，或選取刪除圖示(![刪除圖示的影像](../../images/ui/fields/enum/remove-icon.png))，以將其移除。 完成後，請選取 **[!UICONTROL 套用]** 將更改應用到架構。

![顯示UI中字串欄位所填入的列舉值和顯示名稱的影像](../../images/ui/fields/enum/enum-confirm.png)

畫布會更新以反映變更。 日後探索此架構時，您可以在右側邊欄中檢視及編輯列舉欄位的限制。

## 定義建議的值 {#suggested-values}

選擇 **[!UICONTROL 列舉和建議值]**，然後選取 **[!UICONTROL 建議的值]** 以顯示其他控制項。 從此處，選擇 **[!UICONTROL 新增列]** 開始添加建議值。

![顯示UI中選取之「建議值」選項的影像](../../images/ui/fields/enum/suggested-add-row.png)

在 **[!UICONTROL 顯示名稱]** 欄，提供您要值顯示在「細分」UI中的好記名稱。 若要新增更多建議值，請選取 **[!UICONTROL 新增列]** 再次，並視需要重複此程式。 若要移除先前新增的列，請選取 ![「刪除」圖示](../../images/ui/fields/enum/remove-icon.png) 旁邊。

完成後，請選取 **[!UICONTROL 套用]** 將更改應用到架構。

![顯示UI中字串欄位所填入的列舉值和顯示名稱的影像](../../images/ui/fields/enum/suggested-confirm.png)

>[!NOTE]
>
>欄位的更新建議值會延遲約五分鐘，以反映在分段UI中。

### 管理標準欄位的建議值

標準XDM元件中的某些欄位會包含自己的建議值，例如 `eventType` 從 [[!UICONTROL XDM ExperienceEvent] 類](../../classes/experienceevent.md). 雖然您可以為標準欄位建立其他建議值，但您無法修改或移除組織未定義的任何建議值。 在UI中檢視標準欄位時，其建議的值會顯示，但是是唯讀的。

![顯示UI中字串欄位所填入的列舉值和顯示名稱的影像](../../images/ui/fields/enum/suggested-standard.png)

若要為標準欄位新增建議的值，請選取 **[!UICONTROL 新增列]**. 若要移除組織先前新增的建議值，請選取 ![「刪除」圖示](../../images/ui/fields/enum/remove-icon.png) 旁邊。

![顯示UI中字串欄位所填入的列舉值和顯示名稱的影像](../../images/ui/fields/enum/suggested-standard-add.png)

<!-- ### Removing suggested values for standard fields

Only suggested values that you define can be removed from a standard field. Existing suggested values can be disabled so that they no longer appear in the segmentation dropdown, but they cannot be removed outright.

For example, consider a profile schema where the a suggested value for the standard `person.gender` field is disabled:

![Image showing the enum values and display names filled out for the string field in the UI](../../images/ui/fields/enum/standard-enum-disabled.png)

In this example, the display name "[!UICONTROL Non-specific]" is now disabled from being shown in the segmentation dropdown list. However, the value `non_specific` is still part of the list of enumerated fields and is therefore still allowed on ingestion. In other words, you cannot disable the actual enum value for the standard field as it would go against the principle of only allowing changes that make a field less restrictive.

See the [section below](#evolution) for more information on the rules for updating enums and suggested values for existing schema fields. -->

## 列舉和建議值的演化規則 {#evolution}

使用具有列舉欄位的架構將資料內嵌至Platform後，對架構定義所做的任何進一步變更都必須符合系統中已有的資料。 一般而言，對現有欄位所做的變更只能建立該欄位 **less** 限制性。 欄位的限制性不能比現在更強。

關於列舉和建議的值，下列規則會套用擷取後：

* 您 **可** 為標準和自訂欄位新增建議值，並加入現有建議值。
* 您 **可** 使用現有的建議值，從自訂欄位中移除建議值。
* 您 **可** 為現有的自訂列舉欄位新增列舉值。
* 您 **可** 僅將自訂欄位的列舉值切換為建議值，或將其轉換為沒有列舉或建議值的字串。 **此開關一經套用便無法復原。**
* 您 **無法** 從標準欄位中移除列號或建議的值。
* 您 **無法** 將列舉值新增至沒有現有列舉的欄位。
* 您 **無法** 移除自訂欄位的現有列舉值以下。
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

若要了解如何在 [!DNL Schema Editor]，請參閱 [定義UI中的欄位](./overview.md#special).
