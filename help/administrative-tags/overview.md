---
keywords: Experience Platform；首頁；熱門主題；統一標籤；標籤；
title: 統一標籤概述(beta)
description: 本文檔提供有關Adobe Experience Platform統一標籤的資訊
exl-id: a19e37c3-697a-4000-9cb8-d67478b47dc6
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 1%

---

# 統一標籤概述(Beta)

>[!IMPORTANT]
>
>統一標籤在Beta中。 如果要保留反饋，請通過選擇「標籤管理」頁頂部的按鈕來完成。

標籤是Adobe Experience Platform的一種功能，它使管理員能夠管理元資料分類以便對業務對象進行分類，以便更輕鬆地發現和分類。 標籤是可以視為關鍵字的元資料，可以附加到段、資料集、行程或其他對象，以使搜索能夠查找該對象和相關對象。 標籤分為兩類：分類和未分類。

為了提供更多上下文並定義標籤的用途，類別將標籤組織成有用的集。 管理員定義哪些分類標籤可供用戶添加到對象。 在應用標籤的工作流中，也可以串聯建立不包含類別的新標籤。 這些標籤將顯示在標籤清單的未分類部分中。 管理員和用戶都可以應用標籤，而不管是誰建立的標籤。 所有類型的標籤在分配給對象、搜索或篩選時都可供選擇。

## 標籤術語

標籤涉及以下元件：

| 術語 | 定義 |
| --- | --- |
| 存檔 | 保持當前與對象關聯但限制將標籤應用於其他對象的標籤的狀態。  已存檔的標籤隱藏在標籤選取器中。 |
| 物件 | 可應用標籤的Experience Cloud項。  示例：段、旅程、資料集。 |
| 標記 | 標籤是元資料，可以將其視為關鍵字，可以附加到段、資料集、行程或其他對象，以使搜索能夠查找該對象和相關對象。 |
| 標籤類別 | 標籤類別將標籤組合為有意義的集，以提供更大的上下文或描述標籤的用途。  管理員管理類別中的標籤類別和標籤。 |
| 未分類標籤 | 在應用標籤的行中建立的新標籤。 這些標籤可由任何用戶建立和應用，但不綁定到類別。  管理員可以將這些標籤移到一個類別，以與其他類似的標籤對齊。 |

## 貨簽清單

Experience Platform和Journey Optimizer導航中提供使用標籤清單的標籤類別和標籤管理。 清單中對標籤的更改反映在支援標籤的所有對象中。 所有用戶都可以訪問和瀏覽標籤清單，但標籤管理僅限於系統和產品管理員。

標籤清單有三個層次，允許用戶管理標籤類別、類別中的標籤和單個標籤。 管理單個標籤時，用戶可以查看並導航到當前應用該標籤的任何對象。

### 標籤類別

類別將標籤組合為有意義的集，以提供更大的上下文或描述標籤的用途。 在任何具有類別的標籤上，該類別名稱后跟冒號後面的標籤名稱。

使用標籤類別時，可執行以下操作：

* [建立標籤類別](./ui/tags-categories.md#create-tag-category)
* [編輯標籤類別](./ui/tags-categories.md#edit-tag-category-edit-tag-category)
* [刪除標籤類別](./ui/tags-categories.md#delete-tag-category-delete-tag-category)

### 管理類別中的標籤

>[!NOTE]
>
>為了管理Experience Cloud的標籤，您必須是Adobe Experience Platform的系統管理員或產品管理員，您所在的組織具有Experience Cloud的訂閱。

在類別（或預設的「未分類」組）中，可以建立和管理標籤。 管理標籤時，可執行以下操作：

* [建立標籤](./ui/managing-tags.md#create-a-tag-create-tag)
* [編輯標籤](./ui/managing-tags.md#edit-a-tag-edit-tag)
* [在類別之間移動標籤](./ui/managing-tags.md#move-a-tag-between-categories-move-tag)
* [存檔標籤](./ui/managing-tags.md#archive-a-tag-archive-tag)
* [還原存檔的標籤](./ui/managing-tags.md#restore-an-archived-tag-restore-archived-tag)
* [刪除標籤](./ui/managing-tags.md#delete-a-tag-delete-tag)
* [查看標籤對象](./ui/managing-tags.md#viewing-tagged-objects-view-tagged)
