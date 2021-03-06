---
title: 刪除資源
description: 了解如何刪除Adobe Experience Platform中的標籤資源。
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 75%

---

# 刪除資源

>[!NOTE]
>
>Adobe Experience Platform Launch在Adobe Experience Platform中已重新命名為一套資料收集技術。 因此，產品檔案中已推出數個術語變更。 有關術語更改的綜合參考，請參閱以下[document](../../term-updates.md)。

刪除資源是將該資源從Adobe Experience Platform中永久移除。 如果您仍希望資源顯示在資料收集UI中，但不顯示在標籤庫中，請參閱[從庫中移除資源](remove-resources-from-library.md)。

您可以刪除資料元素、規則、擴充功能、主機、環境和屬性。刪除之後，就無法復原這些資源。

新增至程式庫 (資料元素、規則和擴充功能) 的資源會在您刪除時有特殊考量。

## 準備可供刪除的資源

資源存在於不同的狀態中，而且相互依存。刪除資源之前，您必須確定資源處於可刪除的狀態。

刪除資源前的準備工作包括執行下列兩個基本步驟：

1. 解析相依性。
1. 從程式庫中移除。

### 解析相依性

規則、資料元素和擴充功能都相互依存，因此大部分時間都會刪除，有階層式效果，而您有其他需要清理的項目。

#### 規則

規則取決於其他資源 (擴充功能和資料元素)，但沒有依賴它們的資源。刪除規則就表示您無法繼續在程式庫中使用或甚至檢視該規則，但您後續不會有任何需要清理的相依性。

#### 資料元素

資料元素取決於擴充功能，但不同於規則，資料元素可以有依賴它們的規則和擴充功能。如果刪除資料元素，任何依賴此資料元素的規則或擴充功能都會受到影響。

刪除之後，資料元素就不會繼續在執行階段傳回正確的值，而是傳回空白字串，或將已刪除資料元素的名稱包裹在 %% 中傳回 (例如：`%data-element-name%`)。此行為可在 Property Settings 內設定。

您可以在刪除資料元素之前或之後解析這些相依性。

#### 擴充功能

所有其他資源 (規則、規則元件和資料元素) 均由擴充功能提供。

規則元件和資料元素視擴充功能而定，但也只會顯示在資料收集使用者介面中。 如果您在解析相依性之前刪除了擴充功能，將無法再檢視這些孤立的資源。這些孤立的資源會顯示在清單檢視中，但當您嘗試開啟詳細資料檢視時，將會出現錯誤。

因此，刪除擴充功能時應格外小心，而且您必須先解析相依性，才能刪除這些擴充功能。

### 從程式庫中移除

您必須先將資源從任何包含該資源的程式庫中移除，才能刪除資源。此程序會根據程式庫的狀態而有所不同。

#### 開發

1. 開啟程式庫。
1. 移除資源。
1. 儲存程式庫。
1. 刪除資源。

#### 已提交或已核准

1. 拒絕程式庫 (將其移回開發)。
1. 按照上述步驟從開發程式庫中移除資源。

#### 生產

1. 停用資源。
1. 將已停用的資源發佈到生產。
1. 刪除資源。

## 刪除資源

從相應的清單視圖中，選擇要刪除的資源，然後選擇&#x200B;**[!UICONTROL Delete]**。
