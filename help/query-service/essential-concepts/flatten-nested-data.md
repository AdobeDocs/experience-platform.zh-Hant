---
keywords: Experience Platform；查詢服務；查詢服務；巢狀資料結構；巢狀資料；平面化；平面化巢狀資料；
title: 平面化巢狀資料結構以便與BI工具搭配使用
description: 本檔案說明搭配Query Service使用協力廠商BI工具時，如何在工作階段期間平面化所有表格和檢視的XDM結構。
exl-id: 7e534c0a-db6c-463e-85da-88d7b2534ece
source-git-commit: 1c590350c9d519dba60375b92de7bbbbd77961dc
workflow-type: tm+mt
source-wordcount: '857'
ht-degree: 0%

---

# 平面化巢狀資料結構以搭配第三方BI工具使用

Adobe Experience Platform Query Service支援 `FLATTEN` 透過協力廠商BI工具連線至資料庫時進行設定。 此功能會拼合協力廠商BI工具中的巢狀資料結構，以改善其可用性，並減少擷取、分析、轉換和報表資料所需的工作量。

許多BI工具，例如 [!DNL Tableau] 和 [!DNL Power BI] 本機不支援巢狀資料結構。 此 `FLATTEN` 設定可消除在資料上建立SQL視圖以提供平面版本或使用查詢服務的需要 `CTAS` 或 `INSERT INTO` 使用臨機結構時，將資料集複製到一般版本的工作。

此 `FLATTEN` 設定會將每個葉欄位的結構提取至表格的根中，並將欄位命名為原始命名空間之後的欄位。 這可讓您使用點記號來比對欄位與其體驗資料模型(XDM)路徑，同時保留欄位的內容。

## 先決條件

使用 `FLATTEN` 若要設定，您必須妥善了解下列Adobe Experience Platform元件：

* [XDM系統](../../xdm/home.md):XDM及其實作的概觀Experience Platform。

   * [建立隨選結構](../../xdm/tutorials/ad-hoc.md):XDM結構中的欄位命名僅供單一資料集使用，稱為臨機結構。 臨機結構用於各種資料擷取工作流程中，以用於Experience Platform和建立特定類型的來源連線。

* [沙箱](../../sandboxes/home.md):Experience Platform提供可將單一Platform執行個體分割成個別虛擬環境的虛擬沙箱，以協助開發及改進數位體驗應用程式。

* [巢狀資料結構](./nested-data-structures.md):本檔案提供如何建立、處理或轉換資料集的範例，其中包含複雜的資料類型，包括巢狀資料結構。

## 使用FLATTEN設定連接到資料庫 {#connect-with-flatten}

此 `FLATTEN` 設定會將巢狀資料結構拼合成單獨的列，其中屬性名稱將成為保存行值的列名。 在不支援巢狀資料結構的BI工具中處理資料時，此設定可改善隨選結構的可用性，並減少必要的工作量。

與您選擇的第三方用戶端連線至Query Service時，請附加 `FLATTEN` 設定為資料庫名稱。 如需連線特定BI工具的相關資訊，請參閱 [將客戶端連接到查詢服務概述](../clients/overview.md). 連線字串應包含：

* 沙箱名稱。
* 冒號，後面跟 `all` 或特定資料集ID、檢視ID或資料庫名稱。
* 問號(?) 後面 `FLATTEN` 關鍵字。

輸入應採用下列格式：

```terminal
{sandbox_name}:{all/ID/database_name}?FLATTEN
```

連線字串的範例如下所示：

```terminal
prod:all?FLATTEN
```

## 範例 {#example}

本指南中使用的範例結構採用標準欄位群組 [!UICONTROL 商務詳細資訊]，會利用 `commerce` 物件結構和 `productListItems` 陣列。 請參閱XDM檔案，以了解 [有關 [!UICONTROL 商務詳細資訊] 欄位群組](../../xdm/field-groups/event/commerce-details.md). 架構結構的表示可在下圖中看到。

![「商務詳細資訊」欄位組的架構圖，包括 `commerce` 和 `productListItems` 結構。](../images/essential-concepts/commerce-details.png)

如果BI工具不支援巢狀資料結構，如果巢狀欄位包含序列化值(例如 `commerce` 和 `productListItems` 在範例結構中)。 這些值可能會顯示為單一編碼的一部分 `commerce` 字串欄位且實際上無法使用。

下列值代表 `commerce.order.priceTotal` (3018.0), `commerce.order.purchaseID` (c9b5aff9-25de-450b-98f4-4484a2170180)，以及 `commerce.purchases.value`(1.0)。

```terminal
("(3018.0,c9b5aff9-25de-450b-98f4-4484a2170180)","(1.0)")
```

使用 `FLATTEN` 設定後，您可以使用點記號及其原始路徑名來存取架構內或巢狀資料結構的整個區段中的個別欄位。 此格式的範例，使用 `commerce` 欄位群組如下。

```terminal
commerce.order.priceTotal
commerce.order.purchaseID
commerce.purchases.value
```

此 `FLATTEN` 設定在處理其他資料結構時有某些限制。 如需完整詳細資料，請參閱 [限制部分](#limitations).

### 在查詢中對欄位使用引號 {#quotation-marks}

平面化的根欄位現在使用點記號來比對其XDM路徑。 在查詢中使用時，欄位需要用引號(&quot; &quot;)括住。

下面的SQL示例顯示嵌套查詢的原始狀態：

```sql
SELECT YEAR(timestamp) AS year,
       SUM(commerce.order.priceTotal) AS revenue
FROM purchase_events_dataset
WHERE commerce.purchases.value > 0
GROUP BY 1;
```

使用平面化資料欄位時，查詢會使用點記號撰寫，並以引號括住，如下所示：

```sql
SELECT YEAR(timestamp) AS year,
       SUM("commerce.order.priceTotal") AS revenue
FROM purchase_events_dataset
WHERE "commerce.purchases.value" > 0
GROUP BY 1;
```

## 限制 {#limitations}

此 `FLATTEN` 設定目前不會平面化下列資料結構：

| 資料結構 | 限制 |
|---|---|
| 陣列 | 使用顯式陣列索引或 `EXPLODE` 函式來存取陣列。 |
| 地圖 | 使用字串鍵存取地圖下的值以存取地圖。 |

要解決映射和陣列限制，您需要使用BI工具原始SQL編輯，如Power BI中的高級選項 — > SQL陳述式。

要解決映射和陣列限制，需要BI工具（如原始SQL編輯）。 請參閱如何 [使用Power BI高級選項輸入自定義SQL查詢](../clients/power-bi.md#import-tables-using-custom-sql) 在SQL陳述式部分。

## 後續步驟

本檔案說明如何平面化巢狀資料結構，以便與協力廠商BI工具搭配使用。 如果尚未連接客戶端，請參閱 [客戶端連接概述](../clients/overview.md) 以取得支援的協力廠商用戶端清單。
