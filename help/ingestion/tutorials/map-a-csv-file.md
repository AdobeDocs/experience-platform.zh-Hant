---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 將CSV檔案對應至XDM架構
topic: tutorial
translation-type: tm+mt
source-git-commit: 33282b1c8ab1129344bd4d7054e86fed75e7b899

---


# 將CSV檔案對應至XDM架構

若要將CSV資料內嵌至Adobe Experience Platform，資料必須對應至Experience Data Model(XDM)架構。 本教學課程涵蓋如何使用Experience Platform使用者介面，將CSV檔案對應至XDM架構。

此外，本教學課程的附錄還提供有關使用映射功能的進 [一步資訊](#mapping-functions)。

## 快速入門

本教學課程需要對Adobe Experience Platform的下列元件有正確的認識：

- [體驗資料模型（XDM系統）](../../xdm/home.md):Experience Platform組織客戶體驗資料的標準化架構。
- [批次擷取](../batch-ingestion/overview.md):平台從用戶提供的資料檔案中接收資料的方法。

本教學課程也要求您已建立資料集，以將CSV資料收錄至。 如需在UI中建立資料集的步驟，請參閱資料 [收錄教學課程](./ingest-batch-data.md)。

## 新增資料

在Experience Platform UI中，按一下左側導 **覽中的** 「工作流程」，然後按一 **下「將CSV對應至XDM架構」**。 在出現的右側導軌中，按一下「啟 **動」**。

![](../images/tutorials/map-a-csv-file/workflow-tab.png)

將 _CSV對應至XDM架構_ ，從新增資料步驟 _開始_ 。

![](../images/tutorials/map-a-csv-file/add-data.png)

將CSV檔案拖放至提供的空間，或按一下「瀏 **覽** 」直接選取檔案。 上 _傳檔案後_ ，會顯示「範例資料」區段，顯示前10列資料。 確認資料已如預期上傳後，按一下「下一 **步**」。

![](../images/tutorials/map-a-csv-file/csv-added.png)

## 選擇目標

出現 _「Destination_ （目標）」步驟。 從提供的清單中，選取CSV資料將收錄到的資料集，然後按一下「下 **一步**」。

![](../images/tutorials/map-a-csv-file/select-destination.png)

## 將CSV欄位對應至XDM結構欄位

此時將 _顯示_ 「映射」步驟。 CSV檔案的欄位列在「來源欄位」 _下_，其對應的XDM架構欄位列在「目標欄位」 _下_。 未選取的目標欄位以紅色勾勒。

要將CSV列映射到XDM欄位，請按一下該列相應目標欄位旁的架構表徵圖。

![](../images/tutorials/map-a-csv-file/target-field-mapping.png)

將出 _現「選擇方案_ 」欄位窗口。 您可以在這裡導覽XDM架構的結構，並找出您要將CSV欄對應至的欄位。 按一下XDM欄位以選取它，然後按一下「選 **取**」。

![](../images/tutorials/map-a-csv-file/xdm-field-selection.png)

「映 _射_ 」畫面會重新出現，選取的XDM欄位現在會顯示在「目標 _欄位」下_。

![](../images/tutorials/map-a-csv-file/xdm-field-mapped.png)

如果您不想映射特定CSV欄，可以按一下目標欄位旁的「移 **除** 」圖示來移除映射。 如果要添加新映射，請按一下列 **表底部的** 「添加新映射」。

![](../images/tutorials/map-a-csv-file/remove-or-add-mapping.png)

在映射欄位時，您還可以包括函式，以便根據輸入源欄位計算值。 如需詳 [細資訊](#mapping-functions) ，請參閱附錄中的對應函式一節。

重複上述步驟，繼續將CSV欄對應至XDM欄位。 完成後，按一下「下 **一步**」。

![](../images/tutorials/map-a-csv-file/mapping-finish.png)

## 收錄資料

此時 _會顯示_ 「收錄」步驟，讓您檢視來源檔案和目標資料集的詳細資料。 按一 **下「收錄** 」以開始收錄CSV資料。 視CSV檔案的大小而定，此程式可能需要幾分鐘的時間。 擷取完成後，畫面會更新，指出成功或失敗。 Click **Finish** to complete the workflow.

![](../images/tutorials/map-a-csv-file/ingest-data.png)

## 後續步驟

在本教學課程中，您已成功將平面CSV檔案對應至XDM架構，並將其內嵌至平台。 現在，下游平台服務（例如即時客戶個人檔案）可以使用此資料。 如需詳 [細資訊，請參閱即時客戶個人檔案](../../profile/home.md) 。

## 附錄

下節提供將CSV欄對應至XDM欄位的其他資訊。

### 映射函式

某些映射函式可用於根據在源欄位中輸入的內容計算和計算值。 若要使用函式，請在「來源欄位」下方輸入 _函式_ ，並輸入適當的語法和輸入。

例如，若要串連 **城市****CSV和國家／地區** CSV欄位，並將它們指派至 **城市** XDM欄位，請將來源欄位設為 `concat(city, ", ", county)`。

![](../images/tutorials/map-a-csv-file/mapping-function.png)

下表列出所有支援的映射函式，包括範例運算式及其產生的輸出。

| 函數 | 說明 | 範例運算式 | 範例輸出 |
| -------- | ----------- | ----------------- | ------------- |
| concat | 串連指定的字串。 | concat(&quot;Hi, &quot;, &quot;there&quot;, &quot;!&quot;) | `"Hi, there!"` |
| 爆炸 | 根據規則運算式分割字串，並傳回部件陣列。 | explode(&quot;Hi, there!&quot;, &quot;) | `["Hi,", "there"]` |
| instr | 傳回子字串的位置／索引。 | instr(&quot;adobe<span>.com&quot;, &quot;com&quot;) | 6 |
| replacestr | 如果原始字串中有搜尋字串，請取代該搜尋字串。 | replacestr(&quot;This is a string re test&quot;, &quot;re&quot;, &quot;replace&quot;) | &quot;這是字串替換測試&quot; |
| substr | 傳回指定長度的子字串。 | substr(&quot;This is a substring test&quot;, 7, 8) | &quot; a subst&quot; |
| lower /<br>lcase | 將字串轉換為小寫。 | lower(&quot;HeLLo&quot;)<br>lcase(&quot;HeLLo&quot;) | &quot;hello&quot; |
| upper /<br>ucase | 將字串轉換為大寫。 | upper(&quot;HeLLo&quot;)<br>ucase(&quot;HeLLo&quot;) | &quot;HELLO&quot; |
| split | 在分隔符上拆分輸入字串。 | split(&quot;Hello world&quot;, &quot; &quot;) | `["Hello", "world"]` |
| 加入 | 使用分隔符連接對象清單。 | `join(" ", ["Hello", "world"]`) | &quot;Hello world&quot; |
| 聚結 | 傳回指定清單中的第一個非空值物件。 | coalesce(null, null, null, &quot;first&quot;, null, &quot;second&quot;) | &quot;first&quot; |
| 解碼 | 給定一個鍵和一個作為陣列平面化的鍵值對清單，如果找到鍵，該函式將返回該值，如果在陣列中存在，則返回預設值。 | decode(&quot;k2&quot;, &quot;k1&quot;, &quot;v1&quot;, &quot;k2&quot;, &quot;v2&quot;, &quot;default&quot;) | &quot;v2&quot; |
| if | 評估給定的布爾表達式，並根據結果返回指定的值。 | if(&quot;s&quot;。equalsIgnoreCase(&quot;S&quot;), &quot;True&quot;, &quot;False&quot;) | &quot;True&quot; |
| min | 返回給定參數的最小值。 使用自然排序。 | min(3, 1, 4) | 1 |
| max | 返回給定參數的最大值。 使用自然排序。 | max(3, 1, 4) | 4 |
| first | 檢索第一個給定參數。 | first(&quot;1&quot;, &quot;2&quot;, &quot;3&quot;) | &quot;1&quot; |
| last | 檢索最後一個給定參數。 | last(&quot;1&quot;, &quot;2&quot;, &quot;3&quot;) | &quot;3&quot; |
| uuid /<br>guid | 產生偽隨機ID。 | uuid()<br>guid() | {UNIQUE_ID} |
| now | 檢索當前時間。 | now() | `2019-10-23T10:10:24.556-07:00[America/Los_Angeles]` |
| timestamp | 檢索當前Unix時間。 | timestamp() | 1571850624571 |
| 格式 | 根據指定的格式格式化輸入日期。 | format({DATE}, &quot;yyyy-MM-dd HH:mm:ss&quot;) | &quot;2019-10-23 11:24:35&quot; |
| dformat | 根據指定的格式將時間戳轉換為日期字串。 | dformat(1571829875, &quot;dd-MMM-yyyy hh:mm&quot;) | 「2019年10月23日11:24」 |
| 日期 | 將日期字串轉換為ZonedDateTime物件（ISO 8601格式）。 | date（&quot;2019年10月23日11:24&quot;） | &quot;2019-10-23T11:24:00+00:00&quot; |
| date_part | 擷取日期的部分。 支援下列元件值： <br><br>&quot;<br>year&quot;<br>&quot;yy&quot;<br><br>&quot;yy&quot;<br>&quot;yy&quot;周&quot;<br>&quot;<br><br>.<br>&quot;yy&quot;周&quot;<br>&quot;<br><br>d&quot;<br>d&quot;<br>d&quot;d&quot;&quot;<br><br>d&quot;d&quot;&quot;<br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>d&quot;y&quot;y&quot;y&quot;y&quot;y&quot;y&quot;y&quot;y&quot;y&quot;y&quot;yy&quot;y&quot;y&quot;y&quot;yyy&quot;y&quot;y&quot;y&quot;y&quot;y&quot;y4「&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;>>>>>>>>&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt; | date_part(date(&quot;2019-10-17 11:55:12&quot;), &quot;MM&quot;) | 10 |
| set_date_part | 在指定日期中替換元件。 接受下列元件：yyyy <br><br>&quot;year&quot;<br>&quot;yyy<br>&quot;月&quot;<br><br>&quot;yymm&quot;<br>&quot;mm&quot;日&quot;dd&quot;小時&quot;&quot;<br>yyy&quot;yyy&quot;yyy&quot;<br><br>&quot;yyy&quot;月&quot;yyy&quot;yy&quot;<br><br><br><br><br><br><br><br><br><br><br><br><br>&quot;yyy&quot;yyy&quot;yyyy&quot;yyy&quot;日&quot;d&quot;小時&quot; | set_date_part(&quot;m&quot;, 4, date(&quot;2016-11-09T11:44:44.797&quot;) | &quot;2016-04-09T11:44:44.797&quot; |
| make_date_time /<br>make_timestamp | 從零件建立日期。 | make_date_time(2019、10、17、11、55、12、999、「America/Los_Angeles」) | `2019-10-17T11:55:12.0&#x200B;00000999-07:00[America/Los_Angeles]` |
| current_timestamp | 傳回目前的時間戳記。 | current_timestamp() | 1571850624571 |
| current_date | 傳回不含時間元件的目前日期。 | current_date() | 《2019年11月18日》 |