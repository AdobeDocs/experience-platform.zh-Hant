---
solution: Experience Platform
title: People對象
description: 瞭解如何使用People受眾鎖定目標。
source-git-commit: d73f8c47f9eedff05446688f0c798c322e51aa5d
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 1%

---

# People對象指南

在Adobe Experience Platform中，以人物為基礎的對象可讓您針對行銷活動鎖定特定的人物群組。

People受眾會使用客戶個人檔案資料來鎖定特定市場，讓您更能鎖定您要廣告宣傳的特定人口統計。

## 術語 {#terminology}

開始使用人員對象之前，請先檢閱不同對象型別之間的差異：

- **帳戶對象**：帳戶對象是使用&#x200B;**帳戶**&#x200B;設定檔資料建立的對象。 帳戶設定檔資料可用來建立受眾，將下游帳戶內的人員設為目標。 如需帳戶對象的詳細資訊，請參閱[帳戶對象總覽](./account-audiences.md)。
- **People對象**： People對象是使用&#x200B;**客戶**&#x200B;設定檔資料建立的對象。 客戶設定檔資料可用來建立以您企業的客戶為目標之對象。
- **潛在客戶對象**：潛在客戶對象是使用&#x200B;**潛在客戶**&#x200B;設定檔資料建立的對象。 潛在客戶設定檔資料可用來從未經驗證的使用者建立對象。 如需潛在客戶對象的詳細資訊，請閱讀[潛在客戶對象概觀](./prospect-audiences.md)。

## 存取 {#access}

若要存取People對象，請在&#x200B;**[!UICONTROL 客戶]**&#x200B;區段中選取&#x200B;**[!UICONTROL 對象]**。

![「客戶」區段中的「對象」標籤會醒目提示。](../images/types/people/select-audiences.png)

隨即顯示「對象入口網站」，顯示組織內所有人員對象的清單。

![已顯示People受眾的對象入口網站。](../images/types/people/people-audiences.png)

此檢視會列出對象的相關資訊，包括名稱、設定檔計數、來源、生命週期狀態、建立日期和上次更新日期。

您也可以使用搜尋和篩選功能，快速搜尋及排序特定帳戶對象。 如需有關此功能的詳細資訊，請參閱[對象入口網站概觀](../ui/audience-portal.md#manage-audiences)。

## 客群詳細資料 {#details}

若要檢視特定人物對象的詳細資訊，請在Audience Portal上選取對象。

![在對象入口網站中反白顯示指定的對象。](../images/types/people/select-audience.png)

將會顯示對象詳細資訊頁面。 包括說明、來源和生命週期狀態在內的資訊將會顯示。

![會顯示對象詳細資訊頁面，顯示有關人員對象的資訊。](../images/types/people/audience-details.png)

如需對象詳細資訊頁面的詳細資訊，請參閱對象入口網站概觀[&#128279;](../ui/audience-portal.md#audience-details)的對象詳細資訊區段。

## 建立客群 {#create}

您可以使用對象撰寫器或區段產生器來建立人物對象。 若要開始建立人物對象，請選取對象入口網站上的「建立對象」 。

![[建立對象]按鈕已反白顯示。](../images/types/people/select-create-audience.png)

此時畫面會顯示彈出視窗，讓您在構成對象或建立規則之間做出選擇。

![會顯示一個彈出視窗，其中顯示構成和對象與建置規則之間的選擇。](../images/types/people/create-audience-popover.png)

如需建立對象的詳細資訊，請參閱[對象入口網站概觀](../ui/audience-portal.md#create-audience)。

## 啟用客群 {#activate}

建立您的人員對象後，您可以對其他下游服務啟用此對象。

選取您要啟用的對象，然後選取&#x200B;**[!UICONTROL 啟用到目的地]**。

![快速動作功能表下會醒目顯示[啟用至目的地]按鈕。](../images/types/people/activate-to-destination.png)

[!UICONTROL 啟用目的地]頁面隨即顯示，並根據對象的更新頻率，列出可用的目的地。 如需啟用程式的詳細資訊，請閱讀[啟用概觀](../../destinations/ui/activation-overview.md)。

## 後續步驟

閱讀本指南後，您就會知道如何在Adobe Experience Platform中建立和管理您的人員對象。 若要瞭解不同型別的對象，請閱讀[對象型別概觀](./overview.md)。
