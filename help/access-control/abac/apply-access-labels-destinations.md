---
title: 使用存取權標籤來管理使用者對目的地資料流程的存取權
description: 瞭解如何使用存取標籤來管理使用者對目的地資料流程的存取，以便只有組織中使用者的子集才能存取特定目的地資料流程。
badgePrivateBeta: label="私人測試版" type="Informative"
hide: true
hidefromtoc: true
role: Developer, Admin, User
source-git-commit: 5e5dc2f755be0f396dec1d3f19c166bae3bc9575
workflow-type: tm+mt
source-wordcount: '955'
ht-degree: 1%

---


# 使用存取權標籤來管理使用者對目的地資料流程的存取權

作為 [!UICONTROL 以屬性為基礎的存取控制] Real-Time CDP功能，您現在可以將存取權標籤套用至目的地資料流。 因此，您可以確保組織中只有一部分使用者有權存取特定目的地資料流。

將存取權標籤新增至特定目的地時，只有可存取已指派該標籤之角色的使用者，才能檢視及編輯該目的地資料流。 如果目的地資料流未標籤任何標籤，則屬於您組織的所有使用者皆可看到該資料流。

請參閱本頁面以瞭解範例使用案例、使用此功能時將存取標籤套用至目的地資料流程的先決條件，以及其他重要圖說文字。

## 先決條件 {#prerequisites}

開始使用此功能前，請注意下列要完成的先決條件。 熟悉 [!UICONTROL 以屬性為基礎的存取控制] 功能性，Adobe也建議您閱讀下列文章：

* [屬性式存取控制概觀](/help/access-control/abac/overview.md)
* [以屬性為基礎的存取控制端對端指南](/help/access-control/abac/end-to-end-guide.md)

### 存取許可權UI {#access-permissions-ui}

[!UICONTROL 許可權] 是Experience Cloud區域，管理員可在此定義使用者角色和原則，以管理產品應用程式內功能和物件的許可權。 閱讀 [許可權區段](/help/access-control/abac/end-to-end-guide.md#permissions) 以開始使用。

### 建立角色、標籤並指派使用者 {#create-roles-labels-assign-users}

存取後 [!UICONTROL 許可權] UI，您或您團隊的成員必須設定角色，並將必要的標籤新增到這些角色。 最後，必須將應該存取已使用特定標籤標示之資源的使用者新增至角色。 請參閱下列檔案區段：

* [建立新角色](/help/access-control/abac/ui/roles.md)
* [將標籤新增至角色](/help/access-control/abac/end-to-end-guide.md#label-roles)
* [將使用者新增至角色](/help/access-control/ui/users.md)

### 建立目的地資料流 {#create-dataflow}

您必須先連線到所需的目的地並建立資料流以匯出資料，才能對資料流套用存取標籤。

閱讀指南 [連線到目的地](/help/destinations/ui/connect-destination.md) 和 [將資料啟用至目的地](/help/destinations/ui/activation-overview.md). 然後，從中選擇所需的目的地 [可用聯結器的目錄](/help/destinations/catalog/overview.md).

## 已經可用：將存取權標籤套用至其他Experience Platform資源 {#apply-labels-other-resources}

雖然此版本可讓您授與使用者物件層級存取特定目的地資料流程的許可權，但授與物件層級存取控制的功能通常已可供其他Experience Platform資源使用，例如 [對象](/help/access-control/abac/end-to-end-guide.md#apply-labels-to-segments).

## 使用案例範例 {#use-case-example}

透過目的地的物件層級存取控制，可限制行銷人員的特定團隊只能存取其特定目的地。 例如，如果貴組織在數個地理位置（例如美國和英國）擁有客戶資料，您可以限制行銷團隊只能檢視和編輯美國位置的資料流，限制其他行銷團隊只能檢視和編輯英國位置的資料流。

## 將存取權標籤套用至目的地資料流 {#apply-labels-to-destination-dataflow}

若要將存取權標籤套用至特定資料流：

1. 瀏覽至 **[!UICONTROL 目的地]** > **[!UICONTROL 瀏覽]** 並找出您要限制使用者存取的目的地資料流。
1. 選取省略符號(`...`)中 [!UICONTROL 名稱] 欄並使用 ![編輯詳細資訊控制項](/help/access-control/images/olac/key-icon.svg) **[!UICONTROL 套用存取權標籤]** 控制以新增標籤並管理資料流的現有標籤。
   ![在瀏覽目的地工作區檢視中，選取套用存取權標籤。](/help/access-control/images/olac/apply-access-labels.png)
1. 選取您要新增至目的地資料流的標籤，然後選取「 」 **[!UICONTROL 儲存]**.
   ![選取中應套用至目的地資料流的存取權標籤。](/help/access-control/images/olac/view-access-labels.png)
1. 請注意資料流現在如何在UI中顯示存取標籤。
   ![含有所選資料流的數個目的地資料流檢視如何顯示存取標籤。](/help/access-control/images/olac/dataflow-with-access-label.png)

如果目的地資料流未標籤任何標籤，則會為所有使用者顯示。 如果資料流標示有一或多個存取標籤，則它只會針對屬於具有相同標籤或標籤組合之角色的使用者顯示。

您可以將標準和自訂標籤新增到目的地資料流。 將標籤新增至目的地資料流後：

* 指派給角色且具有相同標籤存取權的使用者可以在UI中檢視具有新標籤的資料流。 他們可以在使用者介面中或透過API檢視及編輯目的地資料流。

* 使用者： *非* 指派給可存取相同標籤的角色無權存取目的地資料流，無法在使用者介面中或透過API檢視或編輯資料流。

## 要瞭解的重要圖說文字和專案 {#important-callouts}

目前，存取標籤只能套用至現有的資料流。 這表示某人必須先建立連至目的地的資料流，才能套用存取標籤。

如果您沒有存取權標籤，就無法將存取權標籤套用至目的地資料流。

將多個標籤新增至目的地資料流時，應該能夠檢視和編輯資料流的使用者必須新增至至少具有相同標籤組合的角色。 例如，如果您將標籤C1、I2和另一個自訂標籤套用至目的地資料流，則只有新增至角色且具有這三個標籤組合存取權的使用者才能檢視和編輯此特定目的地資料流。

![文氏圖表顯示只有特定使用者才能存取已套用多個標籤的目的地的情形。](/help/access-control/images/olac/multiple-labels-venn.png)

## 後續步驟 {#next-steps}

依照本檔案中的步驟，您現在瞭解如何將存取權標籤套用至目的地資料流，以便只有組織中使用者的子集才能存取特定目的地資料流。

接下來，您可以閱讀更多有關支援的其他功能 [!UICONTROL 以屬性為基礎的存取控制] 啟用目的地的資料時。 例如，您可以將使用者的存取許可權製為 [僅檢視及啟用特定欄位](/help/access-control/abac/overview.md#destinations).