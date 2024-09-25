---
title: 建立日期篩選
description: 瞭解如何依日期篩選您的自訂深入分析。
exl-id: fa05d651-ea43-41f0-9b7d-f19c4a9ac256
source-git-commit: 77cedd351b5628d15c279fceabde735f4f93f392
workflow-type: tm+mt
source-wordcount: '922'
ht-degree: 1%

---

# 建立日期篩選 {#create-date-filter}

若要依日期篩選您的深入分析，您必須將引數新增至可以接受日期限制的SQL查詢。 這是作為查詢專家模式見解建立工作流程的一部分完成的。 請參閱[query pro mode檔案](#query-pro-mode)，瞭解如何輸入SQL作為您的深入分析。

查詢引數可讓您使用動態資料，因為它們會作為您在執行時新增值的預留位置。 這些預留位置值可以透過UI更新，並讓技術較差的使用者根據日期範圍更新深入分析。

如果您不熟悉查詢引數，請參閱有關如何實作引數化查詢](../../../../query-service/ui/parameterized-queries.md)的[指南檔案。

## 將日期篩選器套用至您的儀表板 {#apply-date-filter}

若要套用日期篩選，請從您的儀表板檢視的下拉式功能表中選取&#x200B;**[!UICONTROL 新增篩選]**，然後選取&#x200B;**[!UICONTROL 日期篩選]**。

![自訂儀表板，其新增篩選器及其下拉式功能表已反白顯示。](../../../images/query-pro-mode/add-filter.png)

畫面會顯示下列日期篩選選項。

| 篩選器 | 說明 |
| --- | --- |
| 無自訂日期 | 從多個預設值中選取一或多個自訂日期。 |
| 自訂日期範圍 | 從多個預設值中選取一個或多個自訂日期，或指定自訂日期範圍。 |
| 自訂日期 | 從預設值中選取，或指定儀表板的開始日期。 |

![反白顯示三個自訂日期選擇器選項的建立日期篩選對話方塊。](../../../images/query-pro-mode/create-date-filter.png)

### 建立無自訂日期篩選

若要套用預先定義的日期篩選，請選取&#x200B;**[!UICONTROL 無自訂日期]**，然後選取您要包含的預先定義日期選項。 最後，使用下拉式清單選取預設日期範圍，然後選取&#x200B;**[!UICONTROL 儲存]**。

![建立日期篩選對話方塊沒有自訂日期篩選並反白顯示。](../../../images/query-pro-mode/no-custom-date-filter.png)

您會回到儀表板，其中顯示您先前選取的預設日期範圍。 使用下拉式選單來選取另一個預設日期範圍。

![自訂儀表板，顯示預設日期範圍，並反白顯示下拉式清單。](../../../images/query-pro-mode/no-custom-date-filter-results.png)

### 建立自訂日期範圍篩選器

若要套用自訂日期範圍篩選，請選取&#x200B;**[!UICONTROL 自訂日期範圍]**，然後選取您要包含的預先定義日期選項。 最後，選取&#x200B;**[!UICONTROL 自訂]**&#x200B;以設定預設日期範圍。 使用行事曆指定日期範圍，然後選取&#x200B;**[!UICONTROL 儲存]**。

>[!NOTE]
>
>不需要選取預先定義的日期選項。

![使用自訂日期範圍篩選器、自訂及醒目提示儲存的建立日期篩選器對話方塊。](../../../images/query-pro-mode/custom-date-range-filter.png)

您會回到控制面板，顯示您先前指定的自訂資料範圍。 使用下拉式選單來選取另一個預設日期範圍。

![顯示預設日期範圍的自訂儀表板，其中反白顯示自訂日期。](../../../images/query-pro-mode/custom-date-range-filter-results.png)

### 建立自訂日期篩選

若要套用自訂日期篩選，請選取&#x200B;**[!UICONTROL 自訂日期]**，然後選取您要包含的預先定義日期選項。 最後，選取&#x200B;**[!UICONTROL 自訂]**，然後使用行事曆選取開始日期。 最後，選取&#x200B;**[!UICONTROL 儲存]**。

>[!NOTE]
>
>不需要選取預先定義的日期選項。

![使用自訂日期篩選器、自訂及醒目提示儲存的建立日期篩選器對話方塊。](../../../images/query-pro-mode/custom-date-filter.png)

您會回到控制面板，顯示您先前指定的自訂資料。 使用下拉式選單來選取其他日期。

![顯示預設日期範圍的自訂儀表板，其中反白顯示自訂日期。](../../../images/query-pro-mode/custom-date-filter-results.png)

## 刪除日期篩選 {#delete-date-filter}

若要移除您的日期篩選，請選取刪除篩選圖示（![刪除篩選圖示。](/help/images/icons/filter-delete.png)）。

![反白顯示篩選刪除圖示的自訂儀表板。](../../../images/query-pro-mode/delete-date-filter.png)

## 編輯您的SQL以包含日期查詢引數 {#include-date-parameters}

接下來，請確定您的SQL包含查詢引數，以允許日期範圍。 如果您尚未在SQL中合併查詢引數，請編輯您的深入分析以包含這些引數。 請參閱檔案以瞭解如何[編輯分析](../overview.md#edit)的說明。

>[!TIP]
>
>建議您在要啟用日期篩選的每個圖表中，將`$START_DATE`和`$END_DATE`引數新增至SQL陳述式。

>[!NOTE]
>
>日期篩選器不支援時間限制。 此篩選條件僅適用於日期範圍。 這表示如果您在24小時內擁有多個報表，則無法區分同一天內的不同小時。 因此，建議您將時間元件轉換為日期。

如果您正在分析的資料模型或表格有時間元件，您可以依日期將資料分組，然後套用這些日期篩選器。

以下範例SQL陳述式示範如何整合`$START_DATE`和`$END_DATE`引數，並使用`cast`將時間元件框定為日期。

```sql
SELECT Sum(personalization_consent_count) AS Personalization,
       Sum(datacollection_consent_count)  AS Datacollection,
       Sum(datasharing_consent_count)     AS Datasharing
FROM   fact_daily_consent_aggregates f
       INNER JOIN dim_consent_valued
               ON f.consent_value_id = d.consent_value_id
WHERE  f.date BETWEEN Upper(Coalesce(Cast('$START_DATE' AS date), '')) AND Upper
                      (
                             Coalesce(Cast('$END_DATE' AS date), ''))
       AND ( ( Upper(Coalesce($consent_value_filter, '')) IN ( '', 'NULL' ) )
              OR ( f.consent_value_id IN ( $consent_value_filter ) ) )
LIMIT  0; 
```

下面的熒幕擷圖會強調納入SQL陳述式及查詢引數索引鍵值配對中的日期限制。

>[!NOTE]
>
>在query pro模式中構成陳述式時，您必須提供每個引數的範例值，才能執行SQL陳述式並建置圖表。 構成陳述式時提供的範例值，會由您在執行階段為日期（或全域）篩選器選取的實際值取代。

![含有SQL中反白之日期引數的[!UICONTROL 輸入SQL]對話方塊。](../../../images/sql-insights/sql-date-parameters.png)

## 在每個深入分析中啟用日期引數 {#enable-date-parameters}

將適當的引數併入您的深入分析SQL後，`Start_date`和`End_date`變數現在可在Widget Composer中作為切換使用。 如需如何編輯深入分析的資訊，請參閱[查詢專業模式Widget母體部分](#populate-widget)。

在Widget撰寫器中，選取切換以啟用`Start_date`和`End_date`引數。

![具有Start_date和End_date的Widget撰寫器會切換反白顯示。](../../../images/sql-insights/widget-composer-date-filter-toggles.png)

接著，從下拉式選單中選取適當的查詢引數。

![醒目提示Start_date下拉式功能表的Widget Composer。](../../../images/sql-insights/widget-composer-date-filter-dropdown.png)

最後，選取&#x200B;**[!UICONTROL 儲存並關閉]**&#x200B;以返回您的儀表板。 現在已針對所有具有開始和結束日期引數的深入分析啟用日期篩選器。
