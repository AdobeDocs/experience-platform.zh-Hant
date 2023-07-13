---
solution: Experience Platform
title: Audiences UI指南
description: Adobe Experience Platform UI中的對象構成提供豐富的工作區，可讓您與設定檔資料元素互動。 工作區提供直覺式控制項，可讓您為組織建立及編輯對象。
exl-id: 0dda0cb1-49e0-478b-8004-84572b6cf625
source-git-commit: 13492b90552d16334030792323956ea18ca928dc
workflow-type: tm+mt
source-wordcount: '1289'
ht-degree: 0%

---

# 對象組合UI指南

對象構成會使用用來代表不同動作的區塊，提供工作區來建立和編輯對象。

![對象構成UI。](../images/ui/audience-composition/audience-composition.png)

若要變更構成詳細資訊，包括標題和說明，請選取 ![滑桿](../images/ui/audience-composition/sliders.png) 按鈕。

此 **[!UICONTROL 組合屬性]** 彈出視窗隨即顯示。 您可以在此處插入組合的詳細資訊，包括標題和說明。

![「構成」屬性彈出視窗隨即顯示。](../images/ui/audience-composition/composition-properties.png)

>[!NOTE]
>
>如果您有 **not** 為您的構成提供一個標題，依預設，其標題為「構成」，後面接著建立日期和時間。

更新撰寫的詳細資訊後，選取 **[!UICONTROL 儲存]** 以確認這些更新。 對象構成畫布會重新出現。

對象構成畫布由四種不同型別的區塊組成： **[[!UICONTROL 對象]](#audience-block)**， **[[!UICONTROL 排除]](#exclude-block)**， **[[!UICONTROL 排名]](#rank-block)**、和 **[[!UICONTROL Split]](#split-block)**.

## [!UICONTROL 對象] {#audience-block}

此 **[!UICONTROL 對象]** 區塊型別可讓您新增要組成新較大受眾的子受眾。 依預設， **[!UICONTROL 對象]** 區塊會包含在構成畫布的頂端。

當您選取 **[!UICONTROL 對象]** 區塊，右側欄會顯示用來標示對象、將對象新增至區塊，以及建置對象區塊的自訂規則的控制項。

>[!NOTE]
>
>您可以新增對象 **或** 建立自訂規則。 這兩項功能 **無法** 搭配使用。

![將會顯示對象區塊詳細資料。](../images/ui/audience-composition/audience-block.png)

### [!UICONTROL 新增對象] {#add-audience}

將對象新增至「對象」區塊。 選取 **[!UICONTROL 新增對象]**.

![「新增對象」按鈕會反白顯示。](../images/ui/audience-composition/add-audience.png)

對象清單隨即顯示。 選取您要包含的對象，然後按一下「 」 **[!UICONTROL 新增]** 以將其附加至您的對象區塊。

![對象清單隨即顯示。 您可以在此對話方塊中選取要新增的對象。](../images/ui/audience-composition/select-audience.png)

現在，當您選取的對象出現在右側邊欄內時， **[!UICONTROL 對象]** 區塊已選取。 您可以從這裡變更合併對象的合併型別。

![對象可能的合併型別會反白顯示。](../images/ui/audience-composition/merge-types.png)

| 合併型別 | 說明 |
| ---------- | ----------- |
| [!UICONTROL Union] | 這些對象會合併為一個對象。 這相當於OR操作。 |
| [!UICONTROL 交集] | 對象會結合，而只有共用的對象 **全部** 新增的URL數目。 這相當於AND操作。 |
| [!UICONTROL 排除重疊] | 對象會結合，而只有共用的對象 **一個，但不是全部** 新增的URL數目。 這相當於XOR操作。 |

### [!UICONTROL 建置規則] {#build-rule}

若要將自訂規則新增至對象區塊，請選取 **[!UICONTROL 建置規則]**.

![「建置規則」按鈕會反白顯示。](../images/ui/audience-composition/build-rule.png)

「區段產生器」隨即出現。 您可以使用區段產生器建立自訂規則，供對象遵循。 如需使用「區段產生器」的詳細資訊，請參閱 [區段產生器指南](./segment-builder.md).

![隨即顯示區段產生器UI。](../images/ui/audience-composition/segment-builder.png)

新增自訂規則後，選取 **[!UICONTROL 儲存]** 以將規則新增至您的對象。

![](../images/ui/audience-composition/custom-rule.png)

## [!UICONTROL 排除] {#exclude-block}

此 **[!UICONTROL 排除]** 區塊型別可讓您從新的較大對象中排除指定的子對象或屬性。

若要新增 **[!UICONTROL 排除]** 區塊，選取 **+** 圖示，後面接著 **[!UICONTROL 排除]**.

![已選取排除選項。](../images/ui/audience-composition/add-exclude-block.png)

此 **[!UICONTROL 排除]** 區塊。 選取此區塊時，右側欄中會顯示排除專案的詳細資訊。 這包括區塊的標籤和排除型別。 您可以排除 [依對象](#exclude-audience) 或 [依屬性](#exclude-attribute).

![「排除」區塊，會反白顯示可用的兩種不同的排除型別。](../images/ui/audience-composition/exclude.png)

### 依對象排除 {#exclude-audience}

如果您依對象排除，您可以選取「 」，以選取您要排除的對象 **[!UICONTROL 新增對象]**.

![此 [!UICONTROL 新增對象] 按鈕已選取，可讓您選擇要排除的對象。](../images/ui/audience-composition/add-excluded-audience.png)

對象清單隨即顯示。 選取 **[!UICONTROL 新增]** 以將您想要排除的對象新增至排除區塊。

![對象清單隨即顯示。 您可以在此對話方塊中選取要新增的對象。](../images/ui/audience-composition/select-audience.png)

### 依屬性排除 {#exclude-attribute}

如果您依屬性排除，可以選取 ![篩選](../images/ui/audience-composition/filter-attribute.png) 圖示位於 **[!UICONTROL 排除規則]** 區段。

![屬性區段會反白顯示，顯示從何處選取要排除的屬性。](../images/ui/audience-composition/exclude-attribute.png)

設定檔屬性清單隨即顯示。 選取要排除的屬性型別，然後按一下 **[!UICONTROL 選取]** 以將其新增至排除區塊。

![隨即顯示屬性清單。](../images/ui/audience-composition/select-attribute-exclude.png)

<!-- ## [!UICONTROL Join] {#join-block}

The **[!UICONTROL Join]** block type allows you to add in external audiences from datasets that have not yet been processed by Adobe Experience Platform.

To add a **[!UICONTROL Join]** block, select the **+** icon, followed by **[!UICONTROL Join]**.

![The Join option is selected.](../images/ui/audience-composition/add-join-block.png)

When you select the block, details about the join are shown in the right rail, including the block's label and the option to add audiences to the enrichment dataset.

![The join block is highlighted, including details about the join block.](../images/ui/audience-composition/join.png)

After selecting **[!UICONTROL Add Audience]**, a list of audiences appears. Select the audiences you want to include, followed by **[!UICONTROL Add]** to add them to your join block.

![A list of audiences appears. You can select which audience you want to add from this dialog.](../images/ui/audience-composition/select-audience.png)

Your selected audiences now appear within the right rail when the **[!UICONTROL Join]** block is selected. 

![The audiences that were added as part of the Join are shown.](../images/ui/audience-composition/selected-audiences.png) -->

## [!UICONTROL 排名] {#rank-block}

此 **[!UICONTROL 排名]** 區塊型別可讓您根據指定屬性來排名和排序設定檔，並將這些排名設定檔納入您的構成。

若要新增 **[!UICONTROL 排名]** 區塊，選取 **+** 圖示，後面接著 **[!UICONTROL 排名]**.

![已選取「排名」選項。](../images/ui/audience-composition/add-rank-block.png)

當您選取區塊時，排名的詳細資訊會顯示在右側邊欄中，包括區塊的標籤、排名依據的屬性、排名順序，以及用於限制排名之設定檔數目的切換按鈕。

![會醒目顯示排名區塊，以及排名區塊的詳細資料。](../images/ui/audience-composition/rank.png)

若要選取依哪個屬性來排名對象，請選取 ![篩選](../images/ui/audience-composition/filter-attribute.png) 圖示。

![篩選圖示會反白顯示，顯示存取設定檔屬性選取畫面所需的選取專案。](../images/ui/audience-composition/select-rank-attribute.png)

設定檔屬性清單隨即顯示。 在此彈出視窗中，您可以選取要依其排名對象的屬性型別。 選取 **[!UICONTROL 選取]** 以將其新增至排名區塊。 請注意，選取的屬性可以 **僅限** 是數字。

![隨即顯示屬性清單。](../images/ui/audience-composition/select-attribute-rank.png)

選取屬性後，您可以選取排序依據。 這是以遞增（從最低到最高）或遞減（從最高到最低）順序排列。

此外，您可以透過啟用 **[!UICONTROL 新增設定檔限制]** 切換。 啟用此切換時，您可以設定在「 」中傳回的最大對象數 **[!UICONTROL 包含的設定檔]** 欄位。

![「新增設定檔限制」切換會反白顯示，可讓您限制傳回的對象數量。](../images/ui/audience-composition/add-profile-limit.png)

## [!UICONTROL Split] {#split-block}

此 **[!UICONTROL Split]** 區塊型別可讓您將新對象分割成各種子對象。 您可以根據百分比或屬性分割此對象。

若要新增 **[!UICONTROL Split]** 區塊，選取 **+** 圖示，後面接著 **[!UICONTROL Split]**.

![已選取「分割」選項。](../images/ui/audience-composition/add-split-block.png)

### 依百分比分割 {#split-percentage}

依百分比分割時，會根據提供的路徑數和百分比，隨機分割對象。

例如，您可能有三個路徑，每個路徑都具有設定檔的不同百分比。

![系統會顯示已儲存對象數量和百分比的劃分。](../images/ui/audience-composition/percentages.png)

### 依屬性分割 {#split-attribute}

依屬性分割時，會根據提供的屬性分割對象。 若要選取分割依據的屬性，請選取 **[!UICONTROL Split]** 區塊，後面接著 ![篩選](../images/ui/audience-composition/filter-attribute.png) 圖示。

![篩選按鈕已選取，顯示如何依屬性篩選。](../images/ui/audience-composition/select-split-attribute.png)

設定檔屬性清單隨即顯示。 選取屬性型別，然後選取 **[!UICONTROL 選取]** 以將其新增至分割區塊。

![隨即顯示屬性清單。](../images/ui/audience-composition/select-attribute-exclude.png)

選取屬性後，您可以在中新增值，選擇哪些設定檔將屬於哪個子對象。 **[!UICONTROL 值]** 欄位。

![您想要分割屬性的值會被新增。](../images/ui/audience-composition/attribute-split-values.png)

此外，您可以啟用 **[!UICONTROL 其他設定檔]** 切換即可建立包含所有未選取之設定檔的子對象。

![其他設定檔切換會反白顯示。](../images/ui/audience-composition/split-other-profiles.png)

## 發佈您的對象

構成對象後，您可以選取「 」，儲存並發佈對象 **[!UICONTROL 發佈]**.

![「發佈」按鈕會反白顯示，顯示如何儲存和發佈您的對象。](../images/ui/audience-composition/publish.png)

如果在建立對象時發生錯誤，會出現警報，讓您知道如何解決問題。

![「發佈」按鈕會反白顯示，顯示如何儲存和發佈您的對象。](../images/ui/audience-composition/audience-alert.png)

## 後續步驟

對象構成提供豐富的工作流程，可讓您從不同的區塊型別建立對象。 若要進一步瞭解Segmentation Service UI的其他部分，請閱讀 [Segmentation Service使用手冊](./overview.md).
