---
keywords: Experience Platform；首頁；熱門主題；API；API；XDM；XDM系統；體驗資料模型；資料模型；ui；工作區；列舉；欄位；
solution: Experience Platform
title: 在UI中定義列舉欄位和建議值
description: 瞭解如何在Experience Platform使用者介面中定義字串欄位的列舉和建議值。
exl-id: 67ec5382-31de-4f8d-9618-e8919bb5a472
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '1256'
ht-degree: 8%

---

# 在 UI 中定義列舉和建議值 {#enums-and-suggested-values}

>[!CONTEXTUALHELP]
>id="platform_xdm_enum_suggestedvalue"
>title="列舉和建議值"
>abstract="**列舉**&#x200B;會將字串欄位限制為只能擷取和一組預先定義的值相符的資料。可對每個列舉限制式指派一個&#x200B;**顯示名稱**，這會在分段 UI 中填入屬性下拉選單。欄位的&#x200B;**建議值**&#x200B;不會限制擷取，只會判斷分段中顯示的顯示名稱。如果您有多個方案共用一個屬於通用類別或欄位群組的欄位，並且您對每個方案之間的該欄位定義了不同的列舉或建議值，則這些值將合併並附加到聯合方案中。"

在Experience Data Model (XDM)中，字串欄位可以獲得一組預先定義的接受或建議值，以便更好地控制哪些值會擷取到該欄位中，或其在分段中會如何表現。

**[!UICONTROL 列舉]**&#x200B;將字串欄位可擷取的值限製為預先定義的集合。 如果您嘗試將資料內嵌至列舉欄位，但值不符合其設定中定義的任何值，則會拒絕內嵌。

與列舉相反，**[!UICONTROL 建議值]**&#x200B;選項允許為字串欄位表示一組建議值，這些建議值不會限制它可以擷取的值。 建議值反而會影響將字串欄位加入為屬性時，[分段UI](../../../segmentation/ui/overview.md)中可用的預先定義值。

在Adobe Experience Platform使用者介面中定義[新欄位](./overview.md#define)並將型別設定為[!UICONTROL 字串]時，您可以選擇為該欄位定義[列舉](#enum)或[建議值](#suggested-values)。

![影像顯示UI中字串欄位已啟用列舉與建議值選項](../../images/ui/fields/enum/enum-options-selected.png)

本文介紹如何在[!UICONTROL 結構描述] UI工作區中定義列舉和建議值。 如需列舉和建議值的快速概覽（包括如何在UI中設定它們及其下游效果），請觀看以下影片：

>[!VIDEO](https://video.tv.adobe.com/v/3409501/?quality=12&learn=on)

## 定義列舉 {#enum}

選取&#x200B;**[!UICONTROL 列舉和建議值]**，然後選取&#x200B;**[!UICONTROL 列舉]**。 會出現其他控制項，可讓您指定列舉的值限制。 若要新增限制，請選取&#x200B;**[!UICONTROL 新增列]**。

![顯示UI中選取之列舉選項的影像](../../images/ui/fields/enum/enum-add-row.png)

在&#x200B;**[!UICONTROL Value]**&#x200B;欄下，您必須提供您想要強制欄位使用的確切值。 您也可以選擇為限制提供人性化的&#x200B;**[!UICONTROL 顯示名稱]**，這會影響分段中值的呈現方式。

繼續使用&#x200B;**[!UICONTROL 新增列]**&#x200B;將所需的限制和選擇性標籤新增至列舉，或選取先前新增列旁的刪除圖示（![刪除圖示的影像](../../images/ui/fields/enum/remove-icon.png)）以移除它。 完成後，選取&#x200B;**[!UICONTROL 套用]**&#x200B;將變更套用至結構描述。

![此影像顯示UI中字串欄位填寫的列舉值和顯示名稱](../../images/ui/fields/enum/enum-confirm.png)

畫布會更新以反映變更。 當您日後探索此結構時，可以檢視並編輯右側邊欄中列舉欄位的限制。

## 定義建議值 {#suggested-values}

選取&#x200B;**[!UICONTROL 列舉和建議值]**，然後選取&#x200B;**[!UICONTROL 建議值]**，以顯示其他控制項。 從這裡，選取&#x200B;**[!UICONTROL 新增列]**&#x200B;以開始新增建議值。

![顯示UI中選取之[建議值]選項的影像](../../images/ui/fields/enum/suggested-add-row.png)

在&#x200B;**[!UICONTROL 顯示名稱]**&#x200B;欄下，為值提供您想在分段UI中顯示的好記名稱。 若要新增更多建議值，請再次選取&#x200B;**[!UICONTROL 新增列]**，然後視需要重複此程式。 若要移除先前新增的列，請選取相關列旁的![刪除圖示](../../images/ui/fields/enum/remove-icon.png)。

完成後，選取&#x200B;**[!UICONTROL 套用]**&#x200B;將變更套用至結構描述。

![此影像顯示UI中字串欄位填寫的列舉值和顯示名稱](../../images/ui/fields/enum/suggested-confirm.png)

>[!NOTE]
>
>欄位更新的建議值大約會延遲五分鐘，才會反映在分段UI中。

### 管理標準欄位的建議值

標準XDM元件中的某些欄位包含其自己的建議值，例如[[!UICONTROL XDM ExperienceEvent]類別](../../classes/experienceevent.md)中的`eventType`。 雖然您可以為標準欄位建立其他建議值，但無法修改或移除組織未定義的任何建議值。 在UI中檢視標準欄位時，其建議值會顯示，但為唯讀。

![此影像顯示UI中字串欄位填寫的列舉值和顯示名稱](../../images/ui/fields/enum/suggested-standard.png)

若要為標準欄位新增建議值，請選取&#x200B;**[!UICONTROL 新增列]**。 若要移除貴組織先前新增的建議值，請選取相關列旁的![刪除圖示](../../images/ui/fields/enum/remove-icon.png)。

![此影像顯示UI中字串欄位填寫的列舉值和顯示名稱](../../images/ui/fields/enum/suggested-standard-add.png)

<!-- ### Removing suggested values for standard fields

Only suggested values that you define can be removed from a standard field. Existing suggested values can be disabled so that they no longer appear in the segmentation dropdown, but they cannot be removed outright.

For example, consider a profile schema where the a suggested value for the standard `person.gender` field is disabled:

![Image showing the enum values and display names filled out for the string field in the UI](../../images/ui/fields/enum/standard-enum-disabled.png)

In this example, the display name "[!UICONTROL Non-specific]" is now disabled from being shown in the segmentation dropdown list. However, the value `non_specific` is still part of the list of enumerated fields and is therefore still allowed on ingestion. In other words, you cannot disable the actual enum value for the standard field as it would go against the principle of only allowing changes that make a field less restrictive.

See the [section below](#evolution) for more information on the rules for updating enums and suggested values for existing schema fields. -->

## 列舉和建議值的演化規則 {#evolution}

使用具有列舉欄位的結構描述將資料擷取到Platform後，對結構描述定義所做的任何進一步變更都必須符合系統中已存在的資料。 一般而言，對現有欄位進行的變更只能使該欄位&#x200B;**減少**&#x200B;的限制。 欄位不可設定得比原來更嚴格。

有關列舉和建議值，下列規則適用於擷取之後：

* 您&#x200B;**可以**&#x200B;為具有現有建議值的標準和自訂欄位新增建議值。
* 您&#x200B;**可以**&#x200B;從具有現有建議值的自訂欄位中移除建議值。
* 您&#x200B;**可以**&#x200B;為現有的自訂列舉欄位新增列舉值。
* 您&#x200B;**可以**&#x200B;只將自訂欄位的列舉值切換為建議值，或將其轉換為沒有列舉或建議值的字串。 **一旦套用，就無法復原此引數。**
* 您&#x200B;**無法**&#x200B;從標準欄位移除列舉值或建議值。
* 您&#x200B;**無法**&#x200B;將列舉值新增至沒有現有列舉的欄位。
* 您&#x200B;**無法**&#x200B;移除自訂欄位少於所有現有的列舉值。
* 您&#x200B;**無法**&#x200B;從建議值切換為列舉。

## 合併列舉和建議值的規則 {#merging}

如果多個結構描述使用具有不同設定的相同列舉欄位，而這些結構描述包含在聯合中，則某些規則會套用在如何協調列舉差異上。 確切的規則取決於結構描述參考的是相同的標準欄位（例如`eventType`），還是參考的是不同欄位群組中的相同自訂欄位路徑。

如果參照相同的標準欄位：

* 任何其他建議值皆為聯合中的&#x200B;**APPENDED**。
* 相同列舉索引鍵的建議值更新為聯合中的&#x200B;**UPDATED**。

如果參照不同欄位群組中的相同自訂欄位路徑：

* 任何其他建議值皆為聯合中的&#x200B;**APPENDED**。
* 如果在多個結構描述中定義了相同的其他建議值，則這些值在聯合中為&#x200B;**MERGED**。 換句話說，相同的建議值在合併後不會顯示兩次。

## 驗證限制

由於目前系統的限制，在兩種情況下，系統會在擷取期間未驗證列舉：

1. 列舉定義於[陣列欄位](./array.md)。
1. 列舉在結構描述階層中定義了一個以上的層級。

## 後續步驟

本指南說明如何在UI中定義字串欄位的列舉和建議值。 有關如何使用結構描述登入API管理列舉和建議值的資訊，請參閱下列[教學課程](../../tutorials/suggested-values.md)。

若要瞭解如何在[!DNL Schema Editor]中定義其他XDM欄位型別，請參閱[在UI](./overview.md#special)中定義欄位的概觀。
