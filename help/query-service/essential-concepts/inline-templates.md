---
title: 內嵌範本
description: 瞭解如何使用內嵌範本在多個查詢中重複使用多個條件。
source-git-commit: f8ec94b4c93e3b36667bdb179ce12c10d20fa30f
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 1%

---

# 內嵌範本

內嵌範本可讓您在多個查詢中重複使用多個條件。 您可以將條件儲存在範本中，然後在多個查詢中重複使用。 可重複使用的SQL範本可減少開發工作量，也減少在查詢之間複製長陳述式的錯誤風險。 使用內嵌範本，您可以在一個位置進行變更，並讓這些變更反映在參考此範本的任何查詢中。

本文介紹查詢編輯器中內嵌範本的使用和限制。

## 先決條件

UI和查詢服務API都支援內嵌範本。 在繼續使用本指南之前，請先閱讀如何操作的檔案 [透過API建立查詢範本](../api/query-templates.md#create-a-query-template) 或使用 [查詢編輯器](../ui/user-guide.md#query-authoring).

## 內嵌範本語法 {#syntax}

查詢儲存後，即稱為範本。 當範本參照陳述式中的另一個範本時，即稱為內嵌範本。 在您的SQL中，會使用雜湊符號(#)加上範本名稱來指示內嵌範本。 此語法的範例為 `#YOUR_TEMPLATE_NAME`.

## 使用案例 {#use-case}

下列SQL範本示範內嵌範本的效用，並舉例說明在2023年6月前消費超過「最大收入」且訂購的來自任何地區的美國客戶數量。 內嵌範本的優點是您可以輕鬆編輯子範本（在此為最大收入和訂單日期），而不需要變更父範本。

**範例**

```sql
#parent_template : SELECT count(*) FROM customer WHERE region=NA AND country=US AND revenue > #revenue_max
#revenue_max: SELECT max(revenue) FROM revenue_table WHERE order_date > '01-06-2023'
```

執行查詢時，查詢服務會以具名範本的SQL敘述句取代從雜湊符號開始的範本名稱。

>[!NOTE]
>
>查詢範本可呼叫任意數量的其他內嵌範本。 您可以從單一查詢叫用的內嵌範本數量沒有限制。 範本也可以巢狀內嵌在其他內嵌範本中。

您可以使用範本來儲存一或多個條件。 它們本身不需要是完整的查詢。 如果您的範本包含有效的查詢，只要呼叫前面有雜湊符號的範本名稱即可執行查詢。 例如，如果您將 `SELECT * FROM JUNE_2023_LOYALTY_MEMBERS;` 作為範本，命名為 `JUNE_2023_LOYALTY_MEMBERS`，命令  `#JUNE_2023_LOYALTY_MEMBERS;` 會執行範本中包含的有效查詢。

>
>
>在Adobe Experience Platform UI中，僅在父層級支援引數化查詢形式的內嵌範本。 這表示引數化查詢只有在用於原始範本時才有效。 子範本必須是靜態範本，且不能有動態引數。

## 後續步驟

閱讀本檔案後，您現在知道如何在「查詢編輯器」中或透過「查詢服務API」參照SQL中的其他範本。

此外，您應閱讀 [匿名封鎖指南](./anonymous-block.md)，說明如何透過鏈結一或多個依序執行的SQL敘述句，將開發間接成本降至最低。
