---
keywords: Experience Platform；首頁；熱門主題；統一編記；標記；
title: 統一標記概觀 (Beta)
description: 本文件會提供有關如何在 Adob​​e Experience Platform 中管理統一標記的資訊
exl-id: a19e37c3-697a-4000-9cb8-d67478b47dc6
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: ht
source-wordcount: '607'
ht-degree: 100%

---

# 統一標記概觀 (Beta)

>[!IMPORTANT]
>
>統一標記目前為 Beta 版。 如果您想留下回饋意見，請選取標記管理頁面頂端的按鈕即可進行。

標記是 Adob&#x200B;&#x200B;e Experience Platform 的一項功能，讓管理員能夠管理中繼資料分類法，以便將商業物件進行分類，使得探索和分類更輕鬆。標記是可視為關鍵字的中繼資料，可將其附加到區段、資料集、歷程或其他物件上，讓搜尋能找到該物件和相關物件。標記分成兩種類型：已分類和未分類。

為了提供更多內容並定義標記的用途，類別將標記整理成了有用的集合。管理員會定義哪些分類標記可供使用者新增到物件上。在套用標記的工作流程中，也能以內聯方式建立不包含類別的新標記。這些標記會顯示在標記詳細目錄的未分類區段中。無論建立者是誰，管理員和使用者都可以套用標記。在指派給物件、搜尋或篩選時，所有類型的標記都可供選取。

## 標記術語 

標記包含下列元件：

| 術語 | 定義 |
| --- | --- |
| 已封存 | 保持和物件目前的關聯性但限制將標記套用於其他物件的標記狀態。已封存的標記會在標記選擇器上隱藏。 |
| 物件 | 已套用標記的 Experience Cloud 項目。範例：區段、歷程、資料集。 |
| 標記 | 標記為中繼資料並可將其視為關鍵字，可將其附加到區段、資料集、歷程或其他物件上，讓搜尋能找到該物件和相關物件。 |
| 標記類別 | 標記類別會將標記分組成有意義的集合，以提供更多內容或說明標記的用途。管理員會管理標記類別和類別內的標記。 |
| 未分類的標記 | 在套用標記的位置以內聯方式建立新標記。這些標記可以由任何使用者建立和套用，但不綁定至某個類別。管理員可以將這些標記移至某個類別，以和其他類似標記保持一致。 |

## 標記詳細目錄

Experience Platform 和 Journey Optimizer 導覽中會提供使用標記詳細目錄的標記類別和標記管理。在詳細目錄中對標記進行的變更會反映在所有支援標記的物件中。所有使用者都能存取和瀏覽標記詳細目錄，但標記管理則僅限於系統和產品管理員。

標記詳細目錄具有三個等級的階層，讓使用者能夠管理標記類別、類別內部的標記以及個別標記。管理個別標記時，使用者可檢視並瀏覽至目前已套用該標記的任何物件。

### 標記類別

類別會將標記分組成有意義的集合，以提供更多內容或說明標記的用途。在任何具有類別的標記上，後面接著冒號的類別名稱會在標記名稱前面。

使用標記類別時可進行下列動作：

* [建立標記類別](./ui/tags-categories.md#create-tag-category)
* [編輯標記類別](./ui/tags-categories.md#edit-tag-category-edit-tag-category)
* [刪除標記類別](./ui/tags-categories.md#delete-tag-category-delete-tag-category)

### 管理類別內部的標記

>[!NOTE]
>
>您必須是貴組織的 Adob&#x200B;&#x200B;e Experience Platform 的系統管理員或產品管理員，才能管理 Experience Cloud 的標記，貴組織必須訂閱了 Experience Cloud。

您可以在類別 (或預設的「未分類」群組) 內部建立和管理標記。管理標記時可進行下列動作：

* [建立標記](./ui/managing-tags.md#create-a-tag-create-tag)
* [編輯標記](./ui/managing-tags.md#edit-a-tag-edit-tag)
* [在類別之間移動標記](./ui/managing-tags.md#move-a-tag-between-categories-move-tag)
* [封存一個標記](./ui/managing-tags.md#archive-a-tag-archive-tag)
* [還原已封存的標記](./ui/managing-tags.md#restore-an-archived-tag-restore-archived-tag)
* [刪除標記](./ui/managing-tags.md#delete-a-tag-delete-tag)
* [檢視已標記的物件](./ui/managing-tags.md#viewing-tagged-objects-view-tagged)
