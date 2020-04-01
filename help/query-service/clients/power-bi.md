---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 連接Power BI
topic: connect
translation-type: tm+mt
source-git-commit: 7d5d98d8e32607abf399fdc523d2b3bc99555507

---


# 連接Power BI(PC)

PC用戶可以從https://powerbi.microsoft.com/en-us/desktop/安裝Power BI [](https://powerbi.microsoft.com/en-us/desktop/)。

## 設定Power Bi

安裝Power BI後，需要設定必要的元件以支援PostgreSQL連接器。 請遵循下列步驟：

- 查找並安 `npgsql`裝PowerBI的。NET驅動程式包，這是PostgreSQL的正式連接方式。

- 選取v4.0.10（較新版本目前會導致錯誤）。

- 在「自定義設定」螢幕的「Npgsql GAC安裝」下，選擇「 **將安裝在本地硬碟上」**。 未安裝GAC將導致Power BI以後失敗。

- 重新啟動Windows。

- 尋找PowerBI Desktop評估版。

## 將Power BI連接到查詢服務

執行這些準備步驟後，您可以將Power BI連接到查詢服務：

- 開啟Power BI。

- 按一 **下頂端功能表功能區** 中的「取得資料」。

- 選擇 **PostgreSQL資料庫**，然後按一下 **連接**。

- 輸入伺服器和資料庫的值。 **Server** is the Host found under the connection details. 在生產中，將端 `:80` 口添加到主機字串的末尾。 **資料庫** 可以是「全部」或資料集表名。 （請試用其中一個CTAS衍生的資料集。）

- 按一 **下「進階選項**」，然後取消勾 **選「包含關係欄」**。 請勿勾選使 **用完整階層導覽**。

- *（可選，但在為資料庫聲明「全部」時建議）* 輸入SQL陳述式。

>[!NOTE] 如果未提供SQL陳述式，則Power BI將預覽資料庫中的所有表。 對於分層資料，應使用自定義SQL陳述式。 如果表模式是平面的，則它將使用或不使用自定義SQL陳述式。 Power BI尚未支援複合類型——要從複合類型中獲得基本類型，您需要編寫SQL陳述式來導出它們。

```sql
SELECT web.webPageDetails.name AS Page_Name, 
SUM(web.webPageDetails.pageviews.value) AS Page_Views 
FROM _TABLE_ 
WHERE _ACP_YEAR=2018 AND _ACP_MONTH=11 AND _ACP_DAY=20 
GROUP BY web.webPageDetails.name 
ORDER BY SUM(web.webPageDetails.pageviews.value) DESC 
LIMIT 10
```

- 選擇 **DirectQuery** 或 **Import模式** 。 在「 **導入** 」模式下，資料將以power BI導入。 在 **DirectQuery模式中** ，所有查詢都將發送到查詢服務以執行。

- 按一下&#x200B;**「確定」**。現在，Power BI會連線至查詢服務，並在沒有錯誤時產生預覽。 「預覽」轉換數值欄有已知問題。 繼續下一步。

- 按一 **下「載入** 」，將資料集匯入Power BI。
