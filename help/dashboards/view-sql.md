---
title: 檢視分析SQL
description: 檢視您的設定檔、對象、目的地和自訂深入分析背後的SQL，並透過查詢編輯器依需求執行查詢。
exl-id: fd728926-c113-4593-92b1-916a02d09d41
source-git-commit: e0af1f0110ceb514a5b249c42a05bf780ea834c6
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 0%

---

# 檢視分析SQL

使用[!UICONTROL 檢視SQL]功能來檢視您的設定檔、對象、目的地和自訂深入分析背後的SQL，並透過「查詢編輯器」依需求執行查詢。 從SQL中汲取超過40種現有的見解靈感，以建立新的查詢，這些查詢會根據您的業務需求從Platform資料中獲得獨特的見解。

## 導覽至控制面板概觀 {#navigate-to-overview}

若要開啟您選擇的儀表板，請從左側導覽中選取&#x200B;**[!UICONTROL 設定檔]**、**[!UICONTROL 對象]**&#x200B;或&#x200B;**[!UICONTROL 目的地]**。 接著，如果工作區未自動顯示，請從索引標籤選項中選取&#x200B;**[!UICONTROL 概觀]**。

或者，從左側導覽選取&#x200B;**[!UICONTROL 儀表板]**，然後選取自訂儀表板的名稱。 使用者定義控制面板的概觀隨即顯示。

![具有[!UICONTROL 設定檔]、[!UICONTROL 對象]、[!UICONTROL 目的地]和[!UICONTROL 儀表板]的Experience PlatformUI已強調顯示。](./images/view-sql/dashboard-navigation.png)

## 檢視SQL切換 {#toggle}

您可從設定檔、對象、目的地和使用者定義控制面板的概觀切換以啟用或停用功能。

>[!NOTE]
>
>如果您啟用[!UICONTROL 檢視SQL]切換，則在您停用此功能之前，您無法變更全域和Widget層級篩選器。

![反白顯示[!UICONTROL 檢視SQL]切換。](./images/view-sql/view-sql-toggle.png)

啟用切換功能以在每個個別分析上顯示[!UICONTROL 檢視SQL]文字。

![強調顯示[!UICONTROL 檢視SQL]的深入分析。](./images/view-sql/insight-view-sql.png)

選取&#x200B;**[!UICONTROL 檢視SQL]**&#x200B;以開啟包含Widget SQL的對話方塊。

## SQL對話方塊 {#sql-dialog}

會出現一個對話方塊，其中包含分析標題以及產生分析的SQL。

>[!TIP]
>
>您可以選取復製圖示（![復製圖示），將整個SQL陳述式複製到剪貼簿。](./images/view-sql/copy-icon.png))。

![反白顯示SQL陳述式的深入分析對話方塊。](./images/view-sql/sql-dialog.png)

選取&#x200B;**[!UICONTROL 執行SQL]**&#x200B;以開啟已預先填入查詢的查詢編輯器。

![與[!UICONTROL 執行SQL]的深入分析對話方塊已反白顯示。](./images/view-sql/run-sql.png)

## 編輯現有的SQL {#edit-sql}

「查詢編輯器」即會出現。 您現在可以編輯陳述式，並以更符合報告需求的方式查詢平台資料。 以適當的名稱儲存您的新查詢範本。

![已預先填入您選擇的分析SQL的查詢編輯器。](./images/view-sql/edit-sql.png)

## 後續步驟

閱讀本檔案後，您現在瞭解如何在標準儀表板或使用者定義儀表板中存取SQL以取得任何深入分析。 如果您尚未閱讀[Real-time Customer Data Platform Insights資料模型檔案](./data-models/cdp-insights-data-model-b2c.md)，建議您先閱讀。 該檔案包含針對您的行銷和KPI需求量身打造的Real-Time CDP報表自訂SQL範本的相關見解。
