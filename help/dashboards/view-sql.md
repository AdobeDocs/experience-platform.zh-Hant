---
title: 檢視分析SQL
description: 檢視您的設定檔、對象、目的地和自訂深入分析背後的SQL，並透過查詢編輯器依需求執行查詢。
source-git-commit: be90cf38970a54431f48799bf506fb0a20ec0166
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 0%

---

# 檢視分析SQL

使用 [!UICONTROL 檢視SQL] 功能，可檢視您的設定檔、對象、目的地和自訂深入分析背後的SQL，並透過查詢編輯器依需求執行查詢。 從SQL中汲取超過40種現有的見解靈感，以建立新的查詢，這些查詢會根據您的業務需求從Platform資料中獲得獨特的見解。

## 導覽至控制面板概觀 {#navigate-to-overview}

若要開啟您選擇的儀表板，請選取 **[!UICONTROL 設定檔]**， **[!UICONTROL 受眾]**，或 **[!UICONTROL 目的地]** 從左側導覽。 下次選取 **[!UICONTROL 概觀]** 如果工作區未自動顯示，則從「索引標籤」選項啟動。

或者，選取 **[!UICONTROL 儀表板]** 從左側導覽，後面接著自訂儀表板的名稱。 使用者定義控制面板的概觀隨即顯示。

![Experience Platform UI搭配 [!UICONTROL 設定檔]， [!UICONTROL 受眾]， [!UICONTROL 目的地]、和 [!UICONTROL 儀表板] 反白顯示。](./images/view-sql/dashboard-navigation.png)

## 檢視SQL切換 {#toggle}

您可從設定檔、對象、目的地和使用者定義控制面板的概觀切換以啟用或停用功能。

>[!NOTE]
>
>如果您啟用 [!UICONTROL 檢視SQL] 在切換功能之前，您無法變更全域和Widget層級篩選器。

![此 [!UICONTROL 檢視SQL] 切換反白顯示。](./images/view-sql/view-sql-toggle.png)

啟用切換即可顯示 [!UICONTROL 檢視SQL] 個別分析上的文字。

![深入分析，使用 [!UICONTROL 檢視SQL] 反白顯示。](./images/view-sql/insight-view-sql.png)

選取 **[!UICONTROL 檢視SQL]** 以開啟包含介面工具之SQL的對話方塊。

## SQL對話方塊 {#sql-dialog}

會出現一個對話方塊，其中包含分析標題以及產生分析的SQL。

>[!TIP]
>
>您可以選取復製圖示(![復製圖示。](./images/view-sql/copy-icon.png))。

![反白顯示SQL敘述句的深入分析對話方塊。](./images/view-sql/sql-dialog.png)

選取 **[!UICONTROL 執行SQL]** 以開啟查詢編輯器，並預先填入查詢。

![與的深入分析對話方塊 [!UICONTROL 執行SQL] 反白顯示。](./images/view-sql/run-sql.png)

## 編輯現有的SQL {#edit-sql}

「查詢編輯器」即會出現。 您現在可以編輯陳述式，並以更符合報告需求的方式查詢平台資料。 以適當的名稱儲存您的新查詢範本。

![已預先填入所選分析SQL的查詢編輯器。](./images/view-sql/edit-sql.png)

## 後續步驟

閱讀本檔案後，您現在瞭解如何在標準儀表板或使用者定義儀表板中存取SQL以取得任何深入分析。 如果您尚未閱讀本文章，建議您閱讀 [Real-time Customer Data Platform Insights資料模型檔案](./cdp-insights-data-model.md). 該檔案包含針對您的行銷和KPI需求量身打造的Real-Time CDP報表自訂SQL範本的相關見解。
