---
keywords: Experience Platform；查詢服務；查詢服務；嵌套資料結構；嵌套資料；拼合；拼合嵌套資料；
title: 拼合用於BI工具的嵌套資料結構
description: 本文檔介紹在將第三方BI工具與查詢服務一起使用時，如何在會話期間展平所有表和視圖的XDM架構。
exl-id: 7e534c0a-db6c-463e-85da-88d7b2534ece
source-git-commit: 1c590350c9d519dba60375b92de7bbbbd77961dc
workflow-type: tm+mt
source-wordcount: '857'
ht-degree: 0%

---

# 拼合用於第三方BI工具的嵌套資料結構

Adobe Experience Platform查詢服務支援 `FLATTEN` 通過第三方BI工具連接到資料庫時進行設定。 此功能將第三方BI工具中的嵌套資料結構拼合，以提高其可用性，並減少檢索、分析、轉換和報告資料所需的工作量。

許多BI工具，如 [!DNL Tableau] 和 [!DNL Power BI] 不本機支援嵌套的資料結構。 的 `FLATTEN` 設定將消除在資料之上建立SQL視圖以提供平面版本或使用查詢服務的需要 `CTAS` 或 `INSERT INTO` 作業，以在使用臨時架構時將資料集複製到平面版本。

的 `FLATTEN` 設定將每個葉欄位的結構拉入表的根中，並將欄位命名為原始命名空間之後的欄位。 這允許您使用點表示法將欄位與其「體驗資料模型」(XDM)路徑匹配，同時保留該欄位的上下文。

## 先決條件

使用 `FLATTEN` 設定要求對Adobe Experience Platform的下列組成部分有正確的理解：

* [XDM系統](../../xdm/home.md):對XDM及其在Experience Platform中的實施情況進行高級別概述。

   * [建立即席架構](../../xdm/tutorials/ad-hoc.md):XDM模式（具有僅由單個資料集使用而命名的欄位）稱為ad hoc模式。 Ad hoc模式用於各種資料接收工作流以Experience Platform和建立特定類型的源連接。

* [沙箱](../../sandboxes/home.md):Experience Platform提供虛擬沙箱，將單個平台實例分區為獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

* [嵌套資料結構](./nested-data-structures.md):本文檔提供了如何建立、處理或轉換具有複雜資料類型（包括嵌套資料結構）的資料集的示例。

## 使用FLATTEN設定連接到資料庫 {#connect-with-flatten}

的 `FLATTEN` 設定會將嵌套的資料結構拼合到單獨的列中，其中屬性名稱將成為保存行值的列名。 當在不支援嵌套資料結構的BI工具中處理資料時，此設定可提高即席模式的可用性，並減少必要的工作量。

在與所選第三方客戶端連接到查詢服務時，追加 `FLATTEN` 設定為資料庫名。 有關如何連接特定BI工具的資訊，請參閱 [將客戶端連接到Query Service概述](../clients/overview.md)。 連接字串應包含：

* 沙盒名稱。
* 冒號後跟 `all` 或特定資料集ID、視圖ID或資料庫名。
* 問號(?) 後跟 `FLATTEN` 的雙曲餘切值。

輸入應採用以下格式：

```terminal
{sandbox_name}:{all/ID/database_name}?FLATTEN
```

連接字串示例如下所示：

```terminal
prod:all?FLATTEN
```

## 範例 {#example}

本指南中使用的示例架構採用標準欄位組 [!UICONTROL 商業詳細資訊]它利用 `commerce` 對象結構和 `productListItems` 陣列。 有關 [更多資訊 [!UICONTROL 商業詳細資訊] 欄位組](../../xdm/field-groups/event/commerce-details.md)。 在下圖中可看到模式結構的表示。

![Commerce Details欄位組的架構圖，包括 `commerce` 和 `productListItems` 結構。](../images/essential-concepts/commerce-details.png)

如果BI工具不支援嵌套資料結構，則如果嵌套欄位包含序列化值(如 `commerce` 和 `productListItems` )。 這些值可能作為單個編碼的部分出現 `commerce` 字串欄位，不現實地不可用。

以下值表示 `commerce.order.priceTotal` (3018.0), `commerce.order.purchaseID` (c9b5aff9-25de-450b-98f4-4484a2170180), `commerce.purchases.value`(1.0)格式錯誤的嵌套欄位。

```terminal
("(3018.0,c9b5aff9-25de-450b-98f4-4484a2170180)","(1.0)")
```

使用 `FLATTEN` 設定時，可以使用點符號及其原始路徑名訪問架構或嵌套資料結構整個部分中的單獨欄位。 此格式的示例 `commerce` 欄位組如下。

```terminal
commerce.order.priceTotal
commerce.order.purchaseID
commerce.purchases.value
```

的 `FLATTEN` 設定在處理其他資料結構時具有某些限制。 全部詳細資訊請參閱 [限制部分](#limitations)。

### 對查詢中的欄位使用引號 {#quotation-marks}

展平的根欄位現在使用點表示法來匹配其XDM路徑。 在查詢中使用時，欄位需要用引號(&quot; &quot;)括起來。

下面的SQL示例顯示嵌套查詢的原始狀態：

```sql
SELECT YEAR(timestamp) AS year,
       SUM(commerce.order.priceTotal) AS revenue
FROM purchase_events_dataset
WHERE commerce.purchases.value > 0
GROUP BY 1;
```

使用拼合資料欄位時，查詢使用點標籤並括在引號中，如下所示：

```sql
SELECT YEAR(timestamp) AS year,
       SUM("commerce.order.priceTotal") AS revenue
FROM purchase_events_dataset
WHERE "commerce.purchases.value" > 0
GROUP BY 1;
```

## 限制 {#limitations}

的 `FLATTEN` 設定當前不會展平以下資料結構：

| 資料結構 | 限制 |
|---|---|
| 陣列 | 使用顯式陣列索引或 `EXPLODE` 函式以訪問陣列。 |
| 地圖 | 使用字串鍵訪問映射下的值以訪問映射。 |

要解決映射和陣列限制，您需要使用BI工具原始SQL編輯，如Power BI中的高級選項 — > SQL陳述式。

BI工具（如原始SQL編輯）是解決映射和陣列限制所必需的。 請參閱有關如何 [使用Power BI高級選項輸入自定義SQL查詢](../clients/power-bi.md#import-tables-using-custom-sql) 在SQL陳述式節中。

## 後續步驟

本文檔介紹了如何拼合嵌套資料結構，以便與第三方BI工具一起使用。 如果尚未連接客戶端，請參閱 [客戶端連接概述](../clients/overview.md) 的子目錄。
