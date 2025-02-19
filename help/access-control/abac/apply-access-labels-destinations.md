---
title: 使用存取權標籤來管理使用者對目的地資料流程的存取權
description: 瞭解如何使用存取標籤來管理使用者對目的地資料流程的存取，以便只有組織中使用者的子集才能存取特定目的地資料流程。
role: Developer, Admin, User
exl-id: 85944720-8551-491c-8991-dd9668beb0ca
source-git-commit: e1b8ca463146d300b48257304778a82aa745df73
workflow-type: tm+mt
source-wordcount: '995'
ht-degree: 1%

---

# 使用存取權標籤來管理使用者對目的地資料流程的存取權

作為Real-Time CDP中[[!UICONTROL 屬性型存取控制]](overview.md)功能的一部分，您現在可以將存取標籤套用至[目的地資料流](../../dataflows/ui/monitor-destinations.md)。 這樣的話，您可以確保組織中只有一部分使用者才能存取特定目的地資料流。

將存取標籤新增至特定目的地時，只有可存取已指派該標籤之角色的使用者，才能檢視及編輯該目的地資料流。 如果目的地資料流未標籤任何標籤，則屬於您組織的所有使用者皆可看到該資料流。

請參閱本頁面以瞭解範例使用案例、使用此功能時將存取標籤套用至目的地資料流程的先決條件，以及其他重要圖說文字。

## 先決條件 {#prerequisites}

開始使用此功能前，請注意下列要完成的先決條件。 若要熟悉[!UICONTROL 屬性型存取控制]，Adobe也建議您閱讀下列文章：

* [屬性式存取控制概觀](/help/access-control/abac/overview.md)
* [以屬性為基礎的存取控制端對端指南](/help/access-control/abac/end-to-end-guide.md)

### 存取許可權UI {#access-permissions-ui}

[!UICONTROL 許可權]是Experience Cloud的區域，管理員可在此定義使用者角色和原則，以管理產品應用程式內功能和物件的許可權。 閱讀[許可權區段](/help/access-control/abac/end-to-end-guide.md#permissions)以開始。

### 建立角色、標籤並指派使用者 {#create-roles-labels-assign-users}

存取[!UICONTROL 許可權] UI後，您或您的團隊成員必須設定角色，並將必要的標籤新增至這些角色。 最後，必須將應該存取已使用特定標籤標示之資源的使用者新增至角色。 請參閱下列檔案區段：

* [建立新角色](/help/access-control/abac/ui/roles.md)
* [將標籤新增至角色](/help/access-control/abac/end-to-end-guide.md#label-roles)
* [將使用者新增至角色](/help/access-control/ui/users.md)

### 建立目的地資料流 {#create-dataflow}

您必須先連線到所需的目的地並建立資料流以匯出資料，才能對資料流套用存取標籤。

閱讀[連線至目的地](/help/destinations/ui/connect-destination.md)和[啟用資料至目的地](/help/destinations/ui/activation-overview.md)的指南。 然後，從可用聯結器的[目錄](/help/destinations/catalog/overview.md)中選取所要的目的地。

## 已可使用：將存取權標籤套用至其他Experience Platform資源 {#apply-labels-other-resources}

雖然此版本可讓您授與使用者物件層級存取特定目的地資料流程的許可權，但其他Experience Platform資源（例如[對象](/help/access-control/abac/end-to-end-guide.md#apply-labels-to-segments)）已普遍可以使用授與物件層級存取控制的功能。

## 使用案例範例 {#use-case-example}

透過目的地的物件層級存取控制，可限制行銷人員的特定團隊只能存取其特定目的地。 例如，如果貴組織在數個地理位置（例如美國和英國）擁有客戶資料，您可以限制行銷團隊只能檢視和編輯美國位置的資料流，限制其他行銷團隊只能檢視和編輯英國位置的資料流。

## 將存取權標籤套用至目的地資料流 {#apply-labels-to-destination-dataflow}

若要將存取權標籤套用至特定資料流：

1. 導覽至&#x200B;**[!UICONTROL 目的地]** > **[!UICONTROL 瀏覽]**，並找出您要限制使用者存取的目的地資料流。
1. 選取[!UICONTROL 名稱]資料行中的省略符號(`...`)，並使用![編輯詳細資料控制項](/help/images/icons/key.png) **[!UICONTROL 套用存取標籤]**控制項來新增標籤並管理資料流的現有標籤。
   ![在目的地工作區的瀏覽檢視中選取[套用存取標籤]。](/help/access-control/images/olac/apply-access-labels.png)
1. 選取您要新增至目的地資料流的標籤，並選取&#x200B;**[!UICONTROL 儲存]**。
   ![選取中應套用至目的地資料流的存取權標籤。](/help/access-control/images/olac/view-access-labels.png)
1. 請注意資料流現在如何在UI中顯示存取標籤。
   ![含有所選資料流的數個目的地資料流檢視如何顯示存取標籤。](/help/access-control/images/olac/dataflow-with-access-label.png)

如果目的地資料流未標籤任何標籤，所有使用者都可以看到該資料流。 如果資料流標示有一或多個存取標籤，則只有屬於具有相同標籤或標籤組合之角色的使用者才能看到該資料流。

您可以將標準和自訂標籤新增到目的地資料流。 將標籤新增至目的地資料流後：

* 指派給角色且具有相同標籤存取權的使用者可以在UI中檢視具有新標籤的資料流。 他們可以在使用者介面中或透過API檢視及編輯目的地資料流。

* *未*&#x200B;指派給具有相同標籤存取權之角色的使用者，無權存取目的地資料流，以在使用者介面或透過API中檢視或編輯資料流。

## 要瞭解的重要圖說文字和專案 {#important-callouts}

目前，存取標籤只能套用至現有的資料流。 這表示在套用存取權標籤之前，您必須先建立指向目的地的資料流。

如果您沒有存取權標籤，就無法將存取權標籤套用至目的地資料流。

將多個標籤新增至目的地資料流時，應該能夠檢視和編輯資料流的使用者必須新增至至少具有相同標籤組合的角色。 例如，如果您將標籤C1、I2和另一個自訂標籤套用至目的地資料流，則只有新增至角色且具有這三個標籤組合存取權的使用者才能檢視和編輯此特定目的地資料流。

>[!NOTE]
>
> 使用Experience Platform使用者介面頂端的搜尋方塊搜尋目的地資料流時，結果可能包括您的使用者存取標籤限制您檢視的目的地資料流。 此行為將在未來更新中更正。

![文氏圖表顯示只有特定使用者才能存取已套用多個標籤的目的地。](/help/access-control/images/olac/multiple-labels-venn.png)

## 後續步驟 {#next-steps}

依照本檔案中的步驟，您現在瞭解如何將存取權標籤套用至目的地資料流，以便只有組織中使用者的子集才能存取特定目的地資料流。

接著，您可以深入瞭解[!UICONTROL 以屬性為基礎的存取控制]在啟用資料至目的地時支援的其他功能。 例如，您可以限制使用者對[只檢視和啟用特定欄位](/help/access-control/abac/overview.md#destinations)的存取權。
