---
keywords: Experience Platform；首頁；熱門主題；api;API;XDM;XDM系統；經驗資料模型；資料模型；ui;workspace;enum;field;
solution: Experience Platform
title: 在UI中定義枚舉欄位和建議值
description: 瞭解如何在Experience Platform用戶介面中定義字串欄位的枚舉和建議值。
exl-id: 67ec5382-31de-4f8d-9618-e8919bb5a472
source-git-commit: a3140d5216857ef41c885bbad8c69d91493b619d
workflow-type: tm+mt
source-wordcount: '1257'
ht-degree: 8%

---

# 在UI中定義枚舉和建議值 {#enums-and-suggested-values}

>[!CONTEXTUALHELP]
>id="platform_xdm_enum_suggestedvalue"
>title="列舉和建議值"
>abstract="**列舉**&#x200B;會將字串欄位限制為只能擷取和一組預先定義的值相符的資料。可對每個列舉限制式指派一個&#x200B;**顯示名稱**，這會在分段 UI 中填入屬性下拉式清單。欄位的&#x200B;**建議值**&#x200B;不會限制擷取，只會判斷分段中顯示的顯示名稱。如果您有多個方案共用一個屬於通用類別或欄位群組的欄位，並且您對每個方案之間的該欄位定義了不同的列舉或建議值，則這些值將合併並附加到聯合方案中。"

在經驗資料模型(XDM)中，可以為字串欄位提供一組預定義的接受值或建議值，以更好地控制將哪些值輸入到該欄位或它在分段中的行為。

**[!UICONTROL 埃努姆]** 將可為字串欄位攝取的值限制為預定義集。 如果嘗試將資料輸入到枚舉欄位，並且該值與其配置中定義的任何資料都不匹配，則將拒絕接收。

與枚舉相比， **[!UICONTROL 建議值]** option允許為字串欄位指示一組建議的值，這些值不限制它可以攝取的值。 相反，建議的值會影響在 [分段UI](../../../segmentation/ui/overview.md) 將字串欄位作為屬性包含時。

當 [定義新欄位](./overview.md#define) 在Adobe Experience Platform用戶介面中，並將類型設定為 [!UICONTROL 字串]，您可以選擇定義 [枚舉](#enum) 或 [建議值](#suggested-values) 那塊地。

![顯示為UI中的字串欄位啟用的「枚舉和建議值」選項的影像](../../images/ui/fields/enum/enum-options-selected.png)

本文檔介紹如何在 [!UICONTROL 架構] UI工作區。 有關枚舉和建議值（包括如何在UI中配置它們及其下游效果）的快速概述，請觀看以下視頻：

>[!VIDEO](https://video.tv.adobe.com/v/3409501/?quality=12&learn=on)

## 定義枚舉 {#enum}

選擇 **[!UICONTROL 枚舉和建議值]**，然後選擇 **[!UICONTROL 埃努姆]**。 將顯示附加控制項，允許您指定枚舉的值約束。 要添加約束，請選擇 **[!UICONTROL 添加行]**。

![顯示在UI中選擇的「枚舉」選項的影像](../../images/ui/fields/enum/enum-add-row.png)

在 **[!UICONTROL 值]** 列中，必須提供要將欄位限制為的準確值。 您可以選擇提供人性化 **[!UICONTROL 顯示名稱]** 這影響了分割中值的表示方式。

繼續使用 **[!UICONTROL 添加行]** 將所需約束和可選標籤添加到枚舉，或選擇刪除表徵圖(![刪除表徵圖的影像](../../images/ui/fields/enum/remove-icon.png))，以將其刪除。 完成後，選擇 **[!UICONTROL 應用]** 將更改應用到架構。

![顯示UI中字串欄位的枚舉值和顯示名稱的影像](../../images/ui/fields/enum/enum-confirm.png)

畫布將更新以反映更改。 將來當您瀏覽此架構時，可以查看和編輯右欄中枚舉欄位的約束。

## 定義建議值 {#suggested-values}

選擇 **[!UICONTROL 枚舉和建議值]**，然後選擇 **[!UICONTROL 建議值]** 來修改標籤元素的屬性。 從此處，選擇 **[!UICONTROL 添加行]** 開始添加建議的值。

![顯示在UI中選擇的「建議值」選項的影像](../../images/ui/fields/enum/suggested-add-row.png)

在 **[!UICONTROL 顯示名稱]** 列中，提供希望值在分割UI中顯示時的人性化名稱。 要添加更多建議值，請選擇 **[!UICONTROL 添加行]** 重複並根據需要重複該過程。 要刪除先前添加的行，請選擇 ![「刪除」表徵圖](../../images/ui/fields/enum/remove-icon.png) 排旁邊。

完成後，選擇 **[!UICONTROL 應用]** 將更改應用到架構。

![顯示UI中字串欄位的枚舉值和顯示名稱的影像](../../images/ui/fields/enum/suggested-confirm.png)

>[!NOTE]
>
>欄位的更新建議值在分段UI中反映大約有五分鐘的延遲。

### 管理標準欄位的建議值

標準XDM元件中的某些欄位包含它們自己的建議值，如 `eventType` 從 [[!UICONTROL XDM體驗事件] 類](../../classes/experienceevent.md)。 雖然您可以為標準欄位建立附加建議值，但您不能修改或刪除組織未定義的任何建議值。 在UI中查看標準欄位時，其建議值將顯示，但是是只讀的。

![顯示UI中字串欄位的枚舉值和顯示名稱的影像](../../images/ui/fields/enum/suggested-standard.png)

要為標準欄位添加新的建議值，請選擇 **[!UICONTROL 添加行]**。 要刪除組織先前添加的建議值，請選擇 ![「刪除」表徵圖](../../images/ui/fields/enum/remove-icon.png) 排旁邊。

![顯示UI中字串欄位的枚舉值和顯示名稱的影像](../../images/ui/fields/enum/suggested-standard-add.png)

<!-- ### Removing suggested values for standard fields

Only suggested values that you define can be removed from a standard field. Existing suggested values can be disabled so that they no longer appear in the segmentation dropdown, but they cannot be removed outright.

For example, consider a profile schema where the a suggested value for the standard `person.gender` field is disabled:

![Image showing the enum values and display names filled out for the string field in the UI](../../images/ui/fields/enum/standard-enum-disabled.png)

In this example, the display name "[!UICONTROL Non-specific]" is now disabled from being shown in the segmentation dropdown list. However, the value `non_specific` is still part of the list of enumerated fields and is therefore still allowed on ingestion. In other words, you cannot disable the actual enum value for the standard field as it would go against the principle of only allowing changes that make a field less restrictive.

See the [section below](#evolution) for more information on the rules for updating enums and suggested values for existing schema fields. -->

## 枚舉和建議值的演化規則 {#evolution}

使用具有枚舉欄位的架構將資料導入到平台後，對架構定義所做的任何進一步更改都必須符合系統中已有的資料。 通常，對現有欄位所做的更改只能使該欄位 **少** 限制性。 不能使欄位比現有欄位限制更多。

對於枚舉和建議值，以下規則適用後接收：

* 你 **可** 為具有現有建議值的標準欄位和自定義欄位添加建議值。
* 你 **可** 從具有現有建議值的自定義欄位中刪除建議值。
* 你 **可** 為現有自定義枚舉欄位添加新枚舉值。
* 你 **可** 將自定義欄位的枚舉值切換為僅建議值，或將其轉換為沒有枚舉或建議值的字串。 **應用此開關後無法撤消。**
* 你 **無法** 從標準欄位中刪除枚舉或建議值。
* 你 **無法** 將枚舉值添加到沒有現有枚舉的欄位。
* 你 **無法** 刪除自定義欄位的少於所有現有枚舉值。
* 你 **無法** 從建議值切換到枚舉。

## 合併枚舉和建議值的規則 {#merging}

如果多個方案使用具有不同配置的同一枚舉欄位，並且這些方案包含在聯合中，則當涉及如何協調枚舉差異時，將應用某些規則。 確切的規則取決於引用相同標準欄位的架構(如 `eventType`)，或者是否在不同欄位組中引用相同的自定義欄位路徑。

如果引用相同的標準欄位：

* 任何其他建議值 **附加** 在工會。
* 對相同枚舉鍵的建議值進行的更新是 **已更新** 在工會。

如果引用不同欄位組中的相同自定義欄位路徑：

* 任何其他建議值 **附加** 在工會。
* 如果在多個方案中定義了相同的附加建議值，則這些值 **合併** 在工會。 換句話說，合併後，相同的建議值不會出現兩次。

## 驗證限制

由於當前系統限制，在接收期間系統未驗證枚舉的兩種情況：

1. 枚舉是在 [陣列場](./array.md)。
1. 枚舉在架構層次結構中定義了多個級別。

## 後續步驟

本指南介紹了如何在UI中定義字串欄位的枚舉和建議值。 有關如何使用架構註冊表API管理枚舉和建議值的資訊，請參閱以下內容 [教程](../../tutorials/suggested-values.md)。

瞭解如何在中定義其他XDM欄位類型 [!DNL Schema Editor]，請參閱 [定義UI中的欄位](./overview.md#special)。
