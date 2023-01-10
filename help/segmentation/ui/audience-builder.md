---
keywords: Experience Platform；首頁；熱門主題；分段服務；分段服務；使用手冊；ui指南；對象ui指南；對象產生器；對象；對象ui指南；
solution: Experience Platform
title: Audiences UI指南
description: Adobe Experience Platform UI中的Audience Builder提供豐富的工作區，可讓您與設定檔資料元素互動。 工作區提供直覺式控制項，可協助您為組織建立和編輯對象。
hide: true
hidefromtoc: true
exl-id: 0dda0cb1-49e0-478b-8004-84572b6cf625
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '1321'
ht-degree: 1%

---

# Audience Builder UI指南

>[!IMPORTANT]
>
>Audience Builder目前為測試版，並非所有使用者都能使用。 文件和功能可能會有所變更。

Audience Builder提供工作區，可使用用來代表不同動作的區塊來建立和編輯對象。

![Audience Builder UI。](../images/ui/audience-builder/audience-builder.png)

對象構成畫布由五種不同的區塊組成： **[[!UICONTROL 對象]](#audience-block)**, **[[!UICONTROL 排除]](#exclude-block)**, **[[!UICONTROL 加入]](#join-block)**, **[[!UICONTROL 排名]](#rank-block)**，和 **[[!UICONTROL 分割]](#split-block)**.

## [!UICONTROL 對象] {#audience-block}

此 **[!UICONTROL 對象]** 區塊類型可讓您新增要組成新大型對象的子對象。 依預設， **[!UICONTROL 對象]** 塊包含在合成畫布的頂部。

選取 **[!UICONTROL 對象]** 區塊中，右側邊欄會顯示標籤控制項，以及將對象新增至區塊。

![對象區塊詳細資料隨即顯示。](../images/ui/audience-builder/select-audience.png)

選取後 **[!UICONTROL 新增對象]**，則會顯示對象清單。 選取您要包含的對象，之後 **[!UICONTROL 新增]** 將它們附加至您的對象區塊。

![對象清單隨即顯示。 您可以從此對話方塊選取要新增的對象。](../images/ui/audience-builder/select-audience.png)

您選取的對象現在會顯示在右側邊欄中，當 **[!UICONTROL 對象]** 已選取區塊。 從這裡，您可以變更合併對象的合併類型。

![會反白顯示對象的可能合併類型。](../images/ui/audience-builder/merge-types.png)

| 合併類型 | 說明 |
| ---------- | ----------- |
| [!UICONTROL Union] | 對象會合併為一個對象。 這等同於OR操作。 |
| [!UICONTROL 交集] | 對象會合併，僅與中共用的對象 **all** 被添加。 這等同於AND操作。 |
| [!UICONTROL 排除重疊] | 對象會合併，僅與中共用的對象 **一個，但並非全部** 被添加。 這等同於XOR操作。 |

## [!UICONTROL 排除] {#exclude-block}

此 **[!UICONTROL 排除]** 區塊類型可讓您從新的較大受眾中排除指定的子受眾或屬性。

新增 **[!UICONTROL 排除]** 塊，選擇 **+** 表徵圖，後面 **[!UICONTROL 排除]**.

![已選取排除選項。](../images/ui/audience-builder/add-exclude-block.png)

此 **[!UICONTROL 排除]** 已新增區塊。 選取此區塊時，關於排除項目的詳細資訊會顯示在右側邊欄中。 這包括區塊的標籤和排除類型。 您可以排除 [依對象](#exclude-audience) 或 [按屬性](#exclude-attribute).

![「排除」區塊，醒目提示可用的兩種不同排除類型。](../images/ui/audience-builder/exclude.png)

### 依對象排除 {#exclude-audience}

如果您依對象排除，您可以選取要排除的對象 **[!UICONTROL 新增對象]**.

![已選取「新增對象」按鈕，可讓您選擇要排除的對象。](../images/ui/audience-builder/add-excluded-audience.png)

對象清單隨即顯示。 選擇 **[!UICONTROL 新增]** 將您要排除的對象新增至排除區塊。

![對象清單隨即顯示。 您可以從此對話方塊選取要新增的對象。](../images/ui/audience-builder/select-audience.png)

### 依屬性排除 {#exclude-attribute}

如果您依屬性排除，您可以選取 ![篩選](../images/ui/audience-builder/filter-attribute.png) 圖示 **[!UICONTROL 排除規則]** 區段。

![系統會反白顯示屬性區段，指出您要選取要排除的屬性的位置。](../images/ui/audience-builder/exclude-attribute.png)

將顯示配置檔案屬性清單。 選取要排除的屬性類型，後面接著 **[!UICONTROL 選擇]** 將其新增至排除區塊。

![將顯示屬性清單。](../images/ui/audience-builder/select-attribute.png)

## [!UICONTROL 加入] {#join-block}

此 **[!UICONTROL 加入]** 區塊類型可讓您從尚未由Adobe Experience Platform處理的資料集新增外部對象。

新增 **[!UICONTROL 加入]** 塊，選擇 **+** 表徵圖，後面 **[!UICONTROL 加入]**.

![已選擇「聯接」選項。](../images/ui/audience-builder/add-join-block.png)

當您選取區塊時，右側邊欄會顯示關於連結的詳細資訊，包括區塊的標籤，以及將對象新增至擴充資料集的選項。

![加亮連接塊，包括關於連接塊的詳細資訊。](../images/ui/audience-builder/join.png)

選取後 **[!UICONTROL 新增對象]**，則會顯示對象清單。 選取您要包含的對象，之後 **[!UICONTROL 新增]** 將它們添加到加入塊。

![對象清單隨即顯示。 您可以從此對話方塊選取要新增的對象。](../images/ui/audience-builder/select-audience.png)

您選取的對象現在會顯示在右側邊欄中，當 **[!UICONTROL 加入]** 已選取區塊。

![隨即顯示加入時新增的對象。](../images/ui/audience-builder/selected-audiences.png)

## [!UICONTROL 排名] {#rank-block}

此 **[!UICONTROL 排名]** 區塊類型可讓您在發佈新對象之前對對象進行排名和排序。

新增 **[!UICONTROL 排名]** 塊，選擇 **+** 表徵圖，後面 **[!UICONTROL 排名]**.

![已選取「排名」選項。](../images/ui/audience-builder/add-rank-block.png)

當您選取區塊時，排名的相關詳細資料會顯示在右側邊欄中，包括區塊的標籤、要排名的屬性、排名順序，以及用於限制要排名的設定檔數目的切換按鈕。

![會強調顯示排名區塊以及排名區塊的詳細資料。](../images/ui/audience-builder/rank.png)

若要選取要依哪個屬性來排名對象，請選取 ![篩選](../images/ui/audience-builder/filter-attribute.png) 表徵圖。

![篩選器圖示會反白顯示，顯示要選取哪些項目來存取設定檔屬性選取畫面。](../images/ui/audience-builder/select-rank-attribute.png)

將顯示配置檔案屬性清單。 在此彈出式視窗中，您可以選取要依對象排名的屬性類型。 選擇 **[!UICONTROL 選擇]** 將其新增至排名區塊。 請注意，所選屬性可以 **僅限** 類型 `int`.

![將顯示屬性清單。](../images/ui/audience-builder/select-attribute.png)

選取屬性後，您可以選取要依其排名的順序。 這會以升序（從最低到最高）或降序（從最高到最低）排序。

此外，您也可以透過啟用 **[!UICONTROL 新增設定檔限制]** 切換。 啟用此切換時，您可以在 **[!UICONTROL 包含的設定檔]** 欄位。

![系統會反白顯示「新增設定檔限制」切換，讓您限制傳回的對象數量。](../images/ui/audience-builder/add-profile-limit.png)

## [!UICONTROL Split] {#split-block}

此 **[!UICONTROL 分割]** 區塊類型可讓您將新對象分割為多個子對象。 您可以根據百分比或屬性來分割此對象。

新增 **[!UICONTROL 分割]** 塊，選擇 **+** 表徵圖，後面 **[!UICONTROL 分割]**.

![已選擇「拆分」選項。](../images/ui/audience-builder/add-split-block.png)

### 按百分比拆分 {#split-percentage}

依百分比分割時，對象會根據提供的路徑數和百分比隨機分割。

例如，您可以有三個路徑，每個路徑的設定檔百分比不同。

![會顯示儲存的對象數量和百分比的劃分。](../images/ui/audience-builder/percentages.png)

此外，您可以將其中一個分割對象標示為控制群組。

![控制組切換為啟用。 這可讓您將其中一個分割對象標示為控制群組。](../images/ui/audience-builder/control-group.png)

### 依屬性分割 {#split-attribute}

依屬性分割時，會根據提供的屬性來分割對象。 要選擇要拆分的屬性，請選擇 **[!UICONTROL 分割]** 區塊，後面接著 ![篩選](../images/ui/audience-builder/filter-attribute.png) 表徵圖。

![已選取篩選按鈕，說明如何依屬性篩選。](../images/ui/audience-builder/select-attribute-split.png)

將顯示配置檔案屬性清單。 選取屬性類型，後跟 **[!UICONTROL 選擇]** 將其添加到拆分塊。

![將顯示屬性清單。](../images/ui/audience-builder/select-attribute.png)

選取屬性後，您可以在 **[!UICONTROL 值]** 欄位。

![會新增您要依分割屬性的值。](../images/ui/audience-builder/attribute-split-values.png)

此外，您可以啟用 **[!UICONTROL 其他設定檔]** 切換以建立包含所有未選取設定檔的子對象。

![「其他」(Other)配置檔案切換按鈕將突出顯示。](../images/ui/audience-builder/attribute-split-other-profiles.png)

## 發佈您的對象

撰寫對象後，您可以選取 **[!UICONTROL 發佈]**.

![系統會強調顯示「發佈」按鈕，告訴您如何儲存和發佈您的對象。](../images/ui/audience-builder/publish-audience.png)

如果建立對象時發生任何錯誤，則會顯示警報，讓您知道如何解決問題。

![系統會強調顯示「發佈」按鈕，告訴您如何儲存和發佈您的對象。](../images/ui/audience-builder/audience-alert.png)

## 後續步驟

「對象產生器」提供豐富的工作流程，可讓您從不同的區塊類型建立對象。 若要進一步了解Segmentation Service UI的其他部分，請參閱 [區段服務使用手冊](./overview.md).
