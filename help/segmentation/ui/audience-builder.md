---
keywords: Experience Platform；主題；熱門主題；分段服務；分段服務；使用手冊；使用手冊；使用手冊；用戶使用手冊；受眾使用手冊；受眾生成器；受眾；受眾；受眾；用戶使用手冊；
solution: Experience Platform
title: 觀眾UI指南
description: Adobe Experience PlatformUI中的「受眾構建器」提供了一個豐富的工作區，允許您與配置檔案資料元素交互。 工作區提供直觀的控制項，用於為您的組織建立和編輯受眾。
hide: true
hidefromtoc: true
exl-id: 0dda0cb1-49e0-478b-8004-84572b6cf625
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '1321'
ht-degree: 1%

---

# 「受眾生成器UI」指南

>[!IMPORTANT]
>
>「受眾構建器」當前處於測試版中，並且不適用於所有用戶。 文件和功能可能會有所變更。

「受眾構建器」提供一個工作區，用於使用用於表示不同操作的塊來構建和編輯受眾。

![受眾生成器UI。](../images/ui/audience-builder/audience-builder.png)

觀眾合成畫布由五種不同的塊組成： **[[!UICONTROL 觀眾]](#audience-block)**。 **[[!UICONTROL 排除]](#exclude-block)**。 **[[!UICONTROL 加入]](#join-block)**。 **[[!UICONTROL 排名]](#rank-block)**, **[[!UICONTROL 拆分]](#split-block)**。

## [!UICONTROL 對象] {#audience-block}

的 **[!UICONTROL 觀眾]** 塊類型允許您添加要構成新的較大受眾的子受眾。 預設情況下， **[!UICONTROL 觀眾]** 塊包含在合成畫布的頂部。

選擇 **[!UICONTROL 觀眾]** 框，右滑軌顯示用於標籤和向框添加觀眾的控制項。

![將顯示「受眾」塊詳細資訊。](../images/ui/audience-builder/select-audience.png)

選擇後 **[!UICONTROL 添加受眾]**，將顯示觀眾清單。 選擇要包括的受眾，然後 **[!UICONTROL 添加]** 將它們追加到觀眾區。

![將顯示受眾清單。 您可以從此對話框中選擇要添加的受眾。](../images/ui/audience-builder/select-audience.png)

您選定的觀眾現在出現在右欄中 **[!UICONTROL 觀眾]** 框。 從此處，可以更改組合受眾的合併類型。

![將突出顯示受眾的可能合併類型。](../images/ui/audience-builder/merge-types.png)

| 合併類型 | 說明 |
| ---------- | ----------- |
| [!UICONTROL Union] | 觀眾被合為一個觀眾。 這相當於OR操作。 |
| [!UICONTROL 交集] | 將觀眾與僅共用的觀眾合併 **全部** 被加進去。 這相當於AND操作。 |
| [!UICONTROL 排除重疊] | 將觀眾與僅共用的觀眾合併 **一個，但不是全部** 被加進去。 這相當於XOR操作。 |

## [!UICONTROL 排除] {#exclude-block}

的 **[!UICONTROL 排除]** 塊類型允許您從新的較大受眾中排除指定的子受眾或屬性。

添加 **[!UICONTROL 排除]** 框，選擇 **+** 表徵圖，後跟 **[!UICONTROL 排除]**。

![「排除」(Exclude)選項被選中。](../images/ui/audience-builder/add-exclude-block.png)

的 **[!UICONTROL 排除]** 框。 選中此塊後，有關排除的詳細資訊將出現在右欄中。 這包括塊的標籤和排除類型。 可以排除 [按受眾](#exclude-audience) 或 [按屬性](#exclude-attribute)。

![「排除」(Exclude)塊，突出顯示兩個可用的不同排除類型。](../images/ui/audience-builder/exclude.png)

### 按受眾排除 {#exclude-audience}

如果按受眾排除，則可以通過選擇 **[!UICONTROL 添加受眾]**。

![「添加受眾」按鈕被選中，您可以選擇要排除的受眾。](../images/ui/audience-builder/add-excluded-audience.png)

將顯示受眾清單。 選擇 **[!UICONTROL 添加]** 將要排除的受眾添加到排除塊。

![將顯示受眾清單。 您可以從此對話框中選擇要添加的受眾。](../images/ui/audience-builder/select-audience.png)

### 按屬性排除 {#exclude-attribute}

如果按屬性排除，則可以通過選擇 ![濾波器](../images/ui/audience-builder/filter-attribute.png) 表徵圖 **[!UICONTROL 排除規則]** 的子菜單。

![屬性部分將突出顯示，顯示要選擇排除的屬性的位置。](../images/ui/audience-builder/exclude-attribute.png)

此時將顯示配置檔案屬性清單。 選擇要排除的屬性類型，然後 **[!UICONTROL 選擇]** 將其添加到排除塊。

![將顯示屬性清單。](../images/ui/audience-builder/select-attribute.png)

## [!UICONTROL 加入] {#join-block}

的 **[!UICONTROL 加入]** 塊類型允許您從尚未由Adobe Experience Platform處理的資料集添加外部訪問群集。

添加 **[!UICONTROL 加入]** 框，選擇 **+** 表徵圖，後跟 **[!UICONTROL 加入]**。

![「聯接」(Join)選項被選中。](../images/ui/audience-builder/add-join-block.png)

選擇塊時，有關連接的詳細資訊將顯示在右欄中，包括塊的標籤和向濃縮資料集添加受眾的選項。

![加亮連接塊，包括有關連接塊的詳細資訊。](../images/ui/audience-builder/join.png)

選擇後 **[!UICONTROL 添加受眾]**，將顯示觀眾清單。 選擇要包括的受眾，然後 **[!UICONTROL 添加]** 將其添加到您的加入塊。

![將顯示受眾清單。 您可以從此對話框中選擇要添加的受眾。](../images/ui/audience-builder/select-audience.png)

您選定的觀眾現在出現在右欄中 **[!UICONTROL 加入]** 框。

![將顯示作為「連接」一部分添加的受眾。](../images/ui/audience-builder/selected-audiences.png)

## [!UICONTROL 排名] {#rank-block}

的 **[!UICONTROL 排名]** 塊類型允許您在發佈新受眾之前對受眾進行排序。

添加 **[!UICONTROL 排名]** 框，選擇 **+** 表徵圖，後跟 **[!UICONTROL 排名]**。

![「排名」(Rank)選項被選中。](../images/ui/audience-builder/add-rank-block.png)

當您選擇塊時，有關排名的詳細資訊將顯示在右欄中，包括塊的標籤、要排名的屬性、排名順序以及用於限制要排名的配置檔案數的切換。

![將突出顯示秩塊以及秩塊的詳細資訊。](../images/ui/audience-builder/rank.png)

要選擇要對受眾進行排名的屬性，請選擇 ![濾波器](../images/ui/audience-builder/filter-attribute.png) 表徵圖

![過濾器表徵圖會突出顯示，顯示要選擇什麼來訪問配置檔案屬性選擇螢幕。](../images/ui/audience-builder/select-rank-attribute.png)

此時將顯示配置檔案屬性清單。 在此跨距上，您可以選擇要按受眾排名的屬性類型。 選擇 **[!UICONTROL 選擇]** 將其添加到排名塊。 請注意，所選屬性可 **僅** 類型 `int`。

![將顯示屬性清單。](../images/ui/audience-builder/select-attribute.png)

選擇屬性後，可以選擇排序順序。 按升序（從最低到最高）或降序（從最高到最低）排序。

此外，您可以通過啟用 **[!UICONTROL 添加配置檔案限制]** 切換。 啟用此切換後，可設定在 **[!UICONTROL 包括的配置檔案]** 的子菜單。

![「添加配置檔案限制」切換將突出顯示，這允許您限制返回的受眾數。](../images/ui/audience-builder/add-profile-limit.png)

## [!UICONTROL Split] {#split-block}

的 **[!UICONTROL 拆分]** 塊類型允許您將新觀眾分成不同的子觀眾。 您可以根據百分比或屬性拆分此受眾。

添加 **[!UICONTROL 拆分]** 框，選擇 **+** 表徵圖，後跟 **[!UICONTROL 拆分]**。

![「拆分」(Split)選項被選中。](../images/ui/audience-builder/add-split-block.png)

### 按百分比拆分 {#split-percentage}

按百分比拆分時，將根據提供的路徑數和百分比隨機拆分受眾。

例如，您可以有三條路徑，每條路徑的配置檔案百分比不同。

![顯示已保存受眾數和百分比的細分。](../images/ui/audience-builder/percentages.png)

此外，您可以將一個拆分的受眾標籤為控制組。

![控制組切換已啟用。 這允許您將一個拆分的受眾標籤為控制組。](../images/ui/audience-builder/control-group.png)

### 按屬性拆分 {#split-attribute}

當按屬性拆分時，將根據提供的屬性拆分受眾。 要選擇要拆分的屬性，請選擇 **[!UICONTROL 拆分]** 塊，後跟 ![濾波器](../images/ui/audience-builder/filter-attribute.png) 表徵圖

![將選擇篩選器按鈕，顯示如何按屬性進行篩選。](../images/ui/audience-builder/select-attribute-split.png)

此時將顯示配置檔案屬性清單。 選擇屬性類型，然後 **[!UICONTROL 選擇]** 將其添加到分割塊中。

![將顯示屬性清單。](../images/ui/audience-builder/select-attribute.png)

選擇屬性後，您可以通過在 **[!UICONTROL 值]** 的子菜單。

![將添加要拆分屬性的值。](../images/ui/audience-builder/attribute-split-values.png)

此外，您還可以 **[!UICONTROL 其他配置檔案]** 切換以建立包含所有未選配置檔案的子訪問群體。

![「其它」(Other)配置檔案切換被加亮。](../images/ui/audience-builder/attribute-split-other-profiles.png)

## 發佈您的受眾

撰寫受眾後，您可以通過選擇 **[!UICONTROL 發佈]**。

![「發佈」(Publish)按鈕會突出顯示，顯示如何保存和發佈您的受眾。](../images/ui/audience-builder/publish-audience.png)

如果建立訪問群體時出現任何錯誤，則會顯示警報，讓您知道如何解決問題。

![「發佈」(Publish)按鈕會突出顯示，顯示如何保存和發佈您的受眾。](../images/ui/audience-builder/audience-alert.png)

## 後續步驟

「受眾構建器」提供了豐富的工作流，允許您從不同的塊類型建立受眾。 要瞭解有關分段服務UI的其他部分的詳細資訊，請閱讀 [分段服務使用手冊](./overview.md)。
