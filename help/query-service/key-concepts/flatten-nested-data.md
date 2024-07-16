---
keywords: Experience Platform；查詢服務；查詢服務；巢狀資料結構；巢狀資料；平面化；平面化巢狀資料；
title: 平面化巢狀資料結構以用於BI工具
description: 本檔案說明如何將工作階段期間的所有表格和檢視的XDM結構描述平面化為搭配查詢服務使用協力廠商BI工具。
exl-id: 7e534c0a-db6c-463e-85da-88d7b2534ece
source-git-commit: 99cd69234006e6424be604556829b77236e92ad7
workflow-type: tm+mt
source-wordcount: '857'
ht-degree: 0%

---

# 平面化巢狀資料結構以用於協力廠商BI工具

透過協力廠商BI工具連線至資料庫時，Adobe Experience Platform查詢服務支援`FLATTEN`設定。 此功能可平面化協力廠商BI工具中的巢狀資料結構，以提高其可用性並減少擷取、分析、轉換和報表資料所需的工作量。

許多BI工具（如[!DNL Tableau]和[!DNL Power BI]）本身並不支援巢狀資料結構。 `FLATTEN`設定會移除在資料上建立SQL檢視以提供平面版本的需求，或是使用查詢服務`CTAS`或`INSERT INTO`工作將您的資料集複製到平面版本的需求。

`FLATTEN`設定會將每個分葉欄位的結構提取到表格的根中，並將欄位命名在原始名稱空間之後。 這可讓您使用點標籤法來比對欄位與其體驗資料模型(XDM)路徑，同時保留欄位的內容。

## 先決條件

使用`FLATTEN`設定需要您實際瞭解下列Adobe Experience Platform元件：

* [XDM系統](../../xdm/home.md)： XDM及其在Experience Platform中實作的高層級概觀。

   * [建立臨機操作結構描述](../../xdm/tutorials/ad-hoc.md)： XDM結構描述具有僅供單一資料集使用的名稱空間的欄位，稱為臨機操作結構描述。 臨時結構用於各種資料擷取工作流程中，以進行Experience Platform和建立特定型別的來源連線。

* [沙箱](../../sandboxes/home.md)：Experience Platform提供的虛擬沙箱可將單一Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

* [巢狀資料結構](./nested-data-structures.md)：本檔案提供如何建立、處理或轉換包含複雜資料型別（包括巢狀資料結構）的資料集範例。

## 使用FLATTEN設定連線到資料庫 {#connect-with-flatten}

`FLATTEN`設定會將巢狀資料結構平面化為個別的資料行，其中屬性名稱會成為保留資料列值的資料行名稱。 在不支援巢狀資料結構的BI工具中使用資料時，此設定可改善臨時結構描述的可用性並減少必要的工作負載。

使用您選擇的協力廠商使用者端連線到查詢服務時，將`FLATTEN`設定附加至資料庫名稱。 如需如何連線特定BI工具的詳細資訊，請參閱[將使用者端連線至查詢服務總覽](../clients/overview.md)中的個別檔案。 連線字串應包含：

* 沙箱名稱。
* 冒號後面接著`all`或特定的資料集ID、檢視表ID或資料庫名稱。
* 問號(？) 後面接著`FLATTEN`關鍵字。

輸入內容應採用以下格式：

```terminal
{sandbox_name}:{all/ID/database_name}?FLATTEN
```

連線字串範例可能如下所示：

```terminal
prod:all?FLATTEN
```

## 範例 {#example}

本指南中使用的範例結構描述採用標準欄位群組[!UICONTROL Commerce詳細資料]，它使用`commerce`物件結構和`productListItems`陣列。 請參閱XDM檔案以取得[有關[!UICONTROL Commerce詳細資料]欄位群組](../../xdm/field-groups/event/commerce-details.md)的詳細資訊。 結構描述結構的代表可以在下圖中看到。

![包含`commerce`和`productListItems`結構的Commerce詳細資料欄位群組的結構描述圖表。](../images/essential-concepts/commerce-details.png)

如果您的BI工具不支援巢狀資料結構，則當巢狀欄位包含序列化值（例如範例結構描述中的`commerce`和`productListItems`）時，可能很難參考巢狀欄位。 這些值可能會顯示為單一編碼`commerce`字串欄位的一部分，而且實際上並非無法使用。

下列值在格式不正確的巢狀欄位中代表`commerce.order.priceTotal` (3018.0)、`commerce.order.purchaseID` (c9b5aff9-25de-450b-98f4-4484a2170180)和`commerce.purchases.value` (1.0)。

```terminal
("(3018.0,c9b5aff9-25de-450b-98f4-4484a2170180)","(1.0)")
```

透過`FLATTEN`設定，您可以使用點標籤法及其原始路徑名稱，存取結構描述中的個別欄位或巢狀資料結構的整個區段。 以下是使用`commerce`欄位群組的格式範例。

```terminal
commerce.order.priceTotal
commerce.order.purchaseID
commerce.purchases.value
```

處理其他資料結構時，`FLATTEN`設定有某些限制。 在[限制區段](#limitations)中提供完整詳細資料。

### 在查詢中的欄位使用引號 {#quotation-marks}

平面化的根欄位現在會使用點標籤法來比對其XDM路徑。 在查詢中使用時，欄位必須括在引號(&quot; &quot;)中。

下列SQL範例顯示巢狀查詢的原始狀態：

```sql
SELECT YEAR(timestamp) AS year,
       SUM(commerce.order.priceTotal) AS revenue
FROM purchase_events_dataset
WHERE commerce.purchases.value > 0
GROUP BY 1;
```

使用平面化資料欄位時，會使用點標籤法寫入查詢，並以下列方式括在引號中：

```sql
SELECT YEAR(timestamp) AS year,
       SUM("commerce.order.priceTotal") AS revenue
FROM purchase_events_dataset
WHERE "commerce.purchases.value" > 0
GROUP BY 1;
```

## 限制 {#limitations}

`FLATTEN`設定目前不會平面化下列資料結構：

| 資料結構 | 限制 |
|---|---|
| 陣列 | 使用明確的陣列索引或`EXPLODE`函式來存取陣列。 |
| 地圖 | 使用字串索引鍵來存取對應下的值，以存取對應。 |

若要解決Map和Array限制，您需要使用BI工具原始SQL編輯，例如Power BI中的「進階選項 — > SQL陳述式」。

需要原始的SQL編輯等BI工具才能解決對應和陣列限制。 請參閱指南以瞭解如何[使用Power BI進階選項在SQL陳述式區段中輸入自訂SQL查詢](../clients/power-bi.md#import-tables-using-custom-sql)。

## 後續步驟

本檔案說明如何平面化巢狀資料結構以搭配協力廠商BI工具使用。 如果您尚未連線使用者端，請參閱[使用者端連線概觀](../clients/overview.md)，以取得支援的協力廠商使用者端清單。
