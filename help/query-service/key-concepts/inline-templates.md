---
title: 內嵌範本
description: 瞭解如何使用內嵌範本在多個查詢中重複使用多個條件。
exl-id: 78959070-f9e5-4736-b72a-a8ef518bfa4f
source-git-commit: ef4c7f20710f56ca0de7c0dfdb99751ff2fe8ebe
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 1%

---

# 內聯範本

內嵌範本可讓您在多個查詢中重複使用多個條件。 您可以將條件儲存在範本中，然後在多個查詢中重複使用。 可重複使用的SQL範本可減少開發工作，也會減少在查詢之間複製長陳述式時產生的錯誤風險。 使用內嵌範本，您可以在一個位置進行變更，並使這些變更反映在參考此範本的任何查詢中。

本文介紹查詢編輯器中內嵌範本的使用和限制。

## 先決條件

UI和查詢服務API都支援內嵌範本。 在繼續本指南之前，請先閱讀有關如何透過API[&#128279;](../api/query-templates.md#create-a-query-template)或使用[查詢編輯器](../ui/user-guide.md#query-authoring)來建立查詢範本的檔案。

## 內嵌範本語法 {#syntax}

查詢儲存後，即稱為範本。 當範本參考陳述式中的其他範本時，即稱為內嵌範本。 內嵌範本在SQL中，會使用雜湊符號(#)加上範本名稱來表示。 此語法的範例為`#YOUR_TEMPLATE_NAME`。

## 使用實例 {#use-case}

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

您可以使用範本來儲存一或多個條件。 它們本身不需要是完整的查詢。 如果您的範本包含有效的查詢，只要呼叫前面有雜湊符號的範本名稱，即可執行查詢。 例如，如果您將`SELECT * FROM JUNE_2023_LOYALTY_MEMBERS;`儲存為名為`JUNE_2023_LOYALTY_MEMBERS`的範本，則命令`#JUNE_2023_LOYALTY_MEMBERS;`會執行範本中包含的有效查詢。

>[!NOTE]
>
>在Adobe Experience Platform UI中，僅在父層級支援引數化查詢形式的內嵌範本。 這表示引數化查詢只會在原始範本中使用時運作。 子範本必須是靜態範本，而且不能有動態引數。 請參閱[引數化查詢檔案](../ui/parameterized-queries.md)以深入瞭解。

## 後續步驟

閱讀本檔案後，您現在知道如何在查詢編輯器或透過查詢服務API參照SQL中的其他範本。

此外，您應該閱讀[匿名區塊指南](./anonymous-block.md)，其中說明如何透過鏈結一或多個依序執行的SQL敘述句，將開發間接成本降至最低。
