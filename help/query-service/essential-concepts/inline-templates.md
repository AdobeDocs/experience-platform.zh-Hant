---
title: 內嵌範本
description: 瞭解如何使用內嵌範本在多個查詢中重複使用多個條件。
exl-id: 78959070-f9e5-4736-b72a-a8ef518bfa4f
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 1%

---

# 內聯範本

內嵌範本可讓您在多個查詢中重複使用多個條件。 您可以將條件儲存在範本中，然後在多個查詢中重複使用。 可重複使用的SQL範本可減少開發工作，也會減少在查詢之間複製長陳述式時產生的錯誤風險。 使用內嵌範本，您可以在一個位置進行變更，並使這些變更反映在參考此範本的任何查詢中。

本文介紹查詢編輯器中內嵌範本的使用和限制。

## 先決條件

UI和查詢服務API都支援內嵌範本。 在繼續本指南之前，請先閱讀以下說明檔案： [透過API建立查詢範本](../api/query-templates.md#create-a-query-template) 或使用 [查詢編輯器](../ui/user-guide.md#query-authoring).

## 內嵌範本語法 {#syntax}

查詢儲存後，即稱為範本。 當範本參考陳述式中的其他範本時，即稱為內嵌範本。 內嵌範本在SQL中，會使用雜湊符號(#)加上範本名稱來表示。 此語法的範例為 `#YOUR_TEMPLATE_NAME`.

## 使用案例 {#use-case}

下列SQL範本展示內嵌範本的效用，並舉例說明在2023年6月前消費超過「最大收入」且訂購的來自任何地區的美國客戶數量。 內嵌範本的優點在於，您可以輕鬆編輯子範本（在此為最大收入和訂單日期），且不必變更父範本。

**範例**

```sql
#parent_template : SELECT count(*) FROM customer WHERE region=NA AND country=US AND revenue > #revenue_max
#revenue_max: SELECT max(revenue) FROM revenue_table WHERE order_date > '01-06-2023'
```

執行查詢時，Query Service會以具名範本的SQL敘述句取代從雜湊符號開始的範本名稱。

>[!NOTE]
>
>查詢範本可呼叫任意數量的其他內嵌範本。 您可以從單一查詢叫用的內嵌範本數量沒有限制。 範本也可以巢狀內嵌在其他內嵌範本中。

您可以使用範本來儲存一或多個條件。 它們本身不需要是完整的查詢。 如果您的範本包含有效的查詢，只要呼叫前面有雜湊符號的範本名稱，即可執行查詢。 例如，如果您將 `SELECT * FROM JUNE_2023_LOYALTY_MEMBERS;` 作為範本，命名為 `JUNE_2023_LOYALTY_MEMBERS`，命令  `#JUNE_2023_LOYALTY_MEMBERS;` 會執行包含在範本中的有效查詢。

>
>
>在Adobe Experience Platform UI中，僅在父層級支援引數化查詢形式的內嵌範本。 這表示引數化查詢只會在原始範本中使用時運作。 子範本必須是靜態範本，而且不能有動態引數。 請參閱 [引數化查詢檔案](../ui/parameterized-queries.md) 以進一步瞭解。

## 後續步驟

閱讀本檔案後，您現在知道如何在查詢編輯器或透過查詢服務API參照SQL中的其他範本。

此外，您應閱讀 [匿名區塊指南](./anonymous-block.md)，說明如何透過鏈結一或多個依序執行的SQL敘述句，將開發間接成本降至最低。
