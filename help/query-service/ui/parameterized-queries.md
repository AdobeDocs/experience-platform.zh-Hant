---
title: 引數化查詢
description: 瞭解如何在Adobe Experience Platform UI中使用引數化查詢。
exl-id: 5c5ac691-5e29-4262-ba53-84dcc56e744f
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '691'
ht-degree: 11%

---

# 參數化查詢 {#parameterized-queries}

>[!CONTEXTUALHELP]
>id="platform_queryService_queryEditor_parameterizedQueries"
>title="參數化查詢"
>abstract="使用參數化查詢，可在執行時新增參數值。這樣做可讓您處理動態資料，並為不同的使用案例重新使用查詢。使用 `'$'` 前置詞，在文本編輯器中將查詢參數輸入到查詢中。接下來，在編輯器下方的查詢參數部分中新增機碼的值。"

查詢服務支援在查詢編輯器中使用引數化查詢。 透過引數化查詢，您現在可以使用引數的預留位置，並在執行時新增引數值。 預留位置可讓您使用動態資料，但您不知道在執行陳述式前將會有哪些值。 您也可以提前準備查詢，並重複使用它們以達到類似的目的。 重複使用查詢可節省大量時間，因為您可以避免為每個使用案例建立不同的SQL查詢。

## 先決條件

繼續本指南之前，請先閱讀[查詢編輯器UI指南](./user-guide.md)。 查詢編輯器指南提供關於如何在Experience Platform使用者介面中撰寫、驗證和執行客戶體驗資料查詢的詳細資訊。

>[!NOTE]
>
>在Adobe Experience Platform UI中，僅在內嵌範本的父層級支援引數化查詢。 這表示引數化查詢只會在原始範本中使用時運作。 子範本必須是靜態範本，而且不能有動態引數。 請參閱[內嵌範本檔案](../key-concepts/inline-templates.md)以瞭解更多資訊。

## 引數化查詢語法 {#syntax}

引數化的查詢使用格式`'$YOUR_PARAMETER_NAME'`，而且可以使用點標籤法串連。 使用引數化查詢的範例SQL陳述式如下所示。

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

若要在UI中建立引數化查詢，請導覽至「查詢編輯器」。 如需更多指示，請參閱[存取查詢編輯器](./user-guide.md#accessing-query-editor)一節。

使用 `'$'` 前置詞，在文本編輯器中將查詢參數輸入到查詢中。接著，選取[!UICONTROL 主控台]旁的&#x200B;**[!UICONTROL 查詢引數]**&#x200B;索引標籤，為索引鍵新增缺少的值。 如果您忽略將值新增到任何必要的索引鍵，則無法執行查詢。 警示圖示(![警示圖示。](/help/images/icons/alert.png))出現在任何空白[!UICONTROL 值]輸入欄位旁的查詢引數區段。

>[!NOTE]
>
>如果查詢未採用引數，您仍可在「查詢編輯器」中輸入不必要的引數。 查詢編輯器會忽略所有不必要的索引鍵值配對，而這些配對對查詢的執行或結果沒有影響。

![具有引數化查詢的查詢編輯器以及反白的查詢引數區段。](../images/ui/parameterized-queries/parameterized-query.png)

>[!TIP]
>
>將索引標籤從[!UICONTROL 查詢引數]變更為[!UICONTROL 主控台]，以檢視查詢的主控台輸出。

## 使用查詢記錄檔詳細資料檢查引數值 {#check-parameter-values}

您無法儲存範本中的引數，因為所使用的值不是永久性的。 不過，您可以檢查[!UICONTROL 查詢記錄詳細資料]頁面，以尋找查詢執行中使用的引數值。 在此情況下，記錄檔不會指出查詢是引數化查詢。 請參閱[查詢記錄檔案](./query-logs.md)，以取得如何尋找使用值的指示。

![查詢記錄檔檢視，在詳細資訊區段中反白引數化查詢的SQL。](../images/ui/parameterized-queries/parameterized-query-logs.png)

<!-- improve screenshot above ^ I am waiting for a scheduled run to complete -->

## 排程引數化查詢 {#schedule}

當您排定引數化查詢時，會儲存引數值。 若要排程引數化查詢，請依照指南中所述的典型程式來建立排程的查詢，以[建立查詢排程](./query-schedules.md#create-schedule)，然後輸入要用於查詢執行的引數值。 此UI區段只會針對引數化查詢顯示。 如需特定指示，請參閱[中有關為排程引數化查詢](./query-schedules.md#set-parameters)設定引數的章節。

>[!TIP]
>
>查詢服務透過使用引數化查詢支援準備的陳述式。 如需有關SQL語法的詳細資訊，請參閱[準備陳述式語法指南](../sql/prepared-statements.md)。

## 後續步驟

閱讀本檔案後，您已瞭解如何在Adobe Experience Platform UI中引數化查詢，並在排程的查詢執行中使用它們。 本檔案也重點說明如何檢查日誌中用於查詢執行的引數值。

接下來，建議您閱讀[監視排程的查詢](./monitor-queries.md)指南，以透過Experience Platform UI進一步瞭解所有查詢工作的狀態。
