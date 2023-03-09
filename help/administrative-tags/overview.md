---
keywords: Experience Platform；首頁；熱門主題；管理標籤；標籤；
title: 管理標籤概述
description: 本檔案提供Adobe Experience Platform中管理標籤的相關資訊
source-git-commit: f184e94350a79936cbbd9072791650af99fa945f
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 2%

---

# 標記總覽

標籤是Adobe Experience Platform的一項功能，使管理員能夠管理元資料分類，以便對業務對象進行分類，以便更輕鬆地發現和分類。 標籤是中繼資料，可視為可附加至區段、資料集、歷程或其他物件的關鍵字，以便搜尋以尋找該物件和相關物件。 標籤分為兩種類型：分類和取消分類。

為了提供更多上下文並定義標籤的用途，類別會將標籤組織成有用的集。 管理員定義哪些分類標籤可供使用者新增至物件。 不包含類別的新標籤也可以在套用標籤的工作流程中串列建立。 這些標籤會顯示在標籤詳細目錄的未分類區段中。 無論標籤的建立者為何，管理員和使用者都可以套用標籤。 指派給物件、搜尋或篩選時，所有類型的標籤皆可供選取。

## 標籤術語

標籤涉及下列元件：

| 術語 | 定義 |
| --- | --- |
| 已封存 | 標籤的狀態，該狀態保持當前與對象的關聯，但限制將標籤應用於其他對象。  封存的標籤會從標籤選擇器中隱藏。 |
| 物件 | 可套用標籤的Experience Cloud項目。  範例：區段、歷程、資料集。 |
| 標記 | 標籤是中繼資料，可視為可附加至區段、資料集、歷程或其他物件的關鍵字，以便搜尋以尋找該物件和相關物件。 |
| 標籤類別 | 「標籤類別」會將標籤分組成有意義的集合，以提供更豐富的內容或說明標籤的用途。  管理員可管理類別中的標籤和標籤。 |
| 未分類的標籤 | 套用標籤的串列建立的新標籤。 這些標籤可由任何使用者建立和套用，但不會系結至類別。  管理員可將這些標籤移至類別，以與其他類似標籤一致。 |

## 標籤清單

Experience Platform和Journey Optimizer導覽中提供標籤類別和使用標籤詳細目錄的標籤管理。 清單中標籤的變更會反映在支援標籤的所有物件中。 所有使用者都能存取及瀏覽標籤詳細目錄，但標籤管理僅限於系統和產品管理員。

標籤清單有三個層級的階層，可讓使用者管理標籤類別、類別中的標籤和個別標籤。 管理個別標籤時，使用者可以檢視並導覽至目前套用該標籤的任何物件。

### 標籤類別

類別將標籤分組為有意義的集合，以提供更豐富的內容或說明標籤的用途。 在任何具有類別的標籤上，標籤名稱前面會加上類別名稱，後面會加上冒號。

使用標籤類別時，可執行下列動作：

* [建立標籤類別](./ui/tags-categories.md#create-tag-category)
* [編輯標籤類別](./ui/tags-categories.md#edit-tag-category-edit-tag-category)
* [刪除標籤類別](./ui/tags-categories.md#delete-tag-category-delete-tag-category)

### 管理類別中的標籤

>[!NOTE]
>
>若要管理Experience Cloud的標籤，您必須是貴組織的Adobe Experience Platform系統管理員或產品管理員，且該組織有Experience Cloud的訂閱。

在類別（或預設的「未分類」群組）中，您可以建立和管理標籤。 管理標籤時，可執行下列動作：

* [建立標籤](./ui/managing-tags.md#create-a-tag-create-tag)
* [編輯標籤](./ui/managing-tags.md#edit-a-tag-edit-tag)
* [在類別之間移動標籤](./ui/managing-tags.md#move-a-tag-between-categories-move-tag)
* [封存標籤](./ui/managing-tags.md#archive-a-tag-archive-tag)
* [還原已封存的標籤](./ui/managing-tags.md#restore-an-archived-tag-restore-archived-tag)
* [刪除標籤](./ui/managing-tags.md#delete-a-tag-delete-tag)
* [查看標籤的對象](./ui/managing-tags.md#viewing-tagged-objects-view-tagged)
