---
title: 引數化查詢
description: 瞭解如何在Adobe Experience Platform UI中使用引數化查詢。
source-git-commit: a0f826a2e5fcdfc2f9e08221f30ba01470c9b3be
workflow-type: tm+mt
source-wordcount: '638'
ht-degree: 0%

---

# 引數化查詢

>[!IMPORTANT]
>
>引數化的查詢UI功能可在 **限量發行** 而且並非所有客戶都可使用。

查詢服務支援在查詢編輯器中使用引數化查詢。 透過引數化查詢，您現在可以使用引數的預留位置，並在執行時新增引數值。 預留位置可讓您使用動態資料，但您不知道在執行陳述式前值為何。 您也可以提前準備查詢，並重複使用它們以達到類似的目的。 重複使用查詢可節省大量工作，因為您可以避免為每個使用案例建立不同的SQL查詢。

## 先決條件

在繼續本指南之前，請先閱讀 [查詢編輯器UI指南](./user-guide.md). 查詢編輯器指南提供有關如何在Experience Platform使用者介面中編寫、驗證和執行客戶體驗資料查詢的詳細資訊。

>
>
>在其直接父級以外的內嵌範本內不支援引數化查詢。 引數化查詢只有在原始範本或直接子內嵌範本中使用時才有效。

## 引數化查詢語法 {#syntax}

引數化查詢使用格式 `'$YOUR_PARAMETER_NAME'` 可使用點標籤法串連和。 使用引數化查詢的SQL陳述式範例，如下所示。

```sql
INSERT INTO
   $Database_Name.Schema_Name.adwh_lkup_process_delta_log
   (process_name, merge_policy_id, process_status, process_date, create_ts, change_ts)
SELECT
   '$Table_Process_Name' process_name,
   hash('$Merge_PolicyID') merge_policy_id,
   '$process_status' process_status,
   to_date('$date_key') process_date,
   CURRENT_TIMESTAMP create_ts,
   CURRENT_TIMESTAMP change_ts;
```

## 建立引數化查詢 {#create}

若要在UI中建立引數化查詢，請導覽至「查詢編輯器」。 請參閱以下小節： [存取查詢編輯器](./user-guide.md#accessing-query-editor) 以取得更多指示。

使用 `'$'` 在文字編輯器中將查詢引數輸入到查詢中的前言。 接下來，將索引鍵的缺少值新增至 [!UICONTROL 查詢引數] 區段。 如果您忽略將值新增到任何必要的索引鍵，則無法執行查詢。 警示圖示(![警示圖示。](../images/ui/parameterized-queries/alert-icon.png))會顯示在「查詢引數」區段中，任何空白區域旁邊 [!UICONTROL 值] 輸入欄位。

![具有引數化查詢的「查詢編輯器」和「查詢引數」區段會反白顯示。](../images/ui/parameterized-queries/parameterized-query.png)

>[!TIP]
>
>變更索引標籤 [!UICONTROL 查詢引數] 至 [!UICONTROL 主控台] 以檢視查詢的主控台輸出。

如果您移除引數，並在查詢執行後再次嘗試執行查詢，則會在 [!UICONTROL 查詢引數] 區段來警示您。

![查詢編輯器的空白值欄位和查詢引數錯誤會反白顯示。](../images/ui/parameterized-queries/query-parameter-error.png)

## 使用查詢記錄檔詳細資料檢查引數值 {#check-parameter-values}

您無法儲存範本中的引數，因為所使用的值不是永久性的。 不過，您可以檢查 [!UICONTROL 查詢記錄檔詳細資料] 頁面，以尋找查詢執行中使用的引數值。 在此情況下，記錄檔不會指出查詢是引數化查詢。 請參閱 [查詢記錄檔案](./query-logs.md) 以取得有關如何尋找使用值的指示。

![查詢記錄檢視，並在詳細資訊區段中反白引數化查詢的SQL。](../images/ui/parameterized-queries/parameterized-query-logs.png)

<!-- improve screenshot above ^ I am waiting for a scheduled run to complete -->

## 排程引數化查詢 {#schedule}

引數值會在您排程引數化查詢時儲存。 若要排程引數化查詢，請依照指南中所述的典型程式建立排程查詢，以 [建立查詢排程](./query-schedules.md#create-schedule)，然後輸入要在查詢執行中使用的引數值。 此UI區段只會針對引數化查詢顯示。 請參閱以下小節： [為排程的引數化查詢設定引數](./query-schedules.md#set-parameters) 以取得特定指示。

>[!TIP]
>
>Query Service透過使用引數化查詢支援準備陳述式。 請參閱 [prepared陳述式語法指南](../sql/prepared-statements.md) 以取得有關SQL語法的詳細資訊。

## 後續步驟

閱讀本檔案後，您已瞭解如何在Adobe Experience Platform UI中將查詢引數化，並在排程的查詢執行中使用它們。 該檔案還突出顯示如何檢查日誌中用於查詢執行的引數值。

如果您尚未閱讀指南，建議您閱讀 [監視排定的查詢](./monitor-queries.md) 以透過Platform UI更能瞭解所有查詢工作的狀態。
