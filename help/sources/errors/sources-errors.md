---
title: 來源錯誤訊息
description: 瞭解在針對來源使用流量服務時可能會遇到的錯誤訊息。
exl-id: cfba9780-4ab9-447b-8c60-c9f813107d11
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '3192'
ht-degree: 8%

---

# 來源錯誤訊息

本檔案提供錯誤訊息的目錄、說明，以及來源的建議解決方案。

## 一般錯誤

| 錯誤代碼 | 標題 | 詳細訊息 |
| --- | --- | --- |
| `1000-400` | 錯誤請求 | 請求無效。 請檢查請求，然後再試一次。 |
| `1001-401` | 未獲授權 | 使用者未獲授權。 請聯絡您的管理員以取得資源的存取權。 |
| `1002-403` | 已禁止 | 請求的操作被禁止。 請檢查要求的操作，然後再試一次。 |
| `1003-404` | 找不到資源 | 找不到請求的資源。 請檢查提供的請求，然後再試一次。 |
| `1004-415` | 不支援的媒體型別 | 提供的裝載格式不受支援。 請檢查您提供的請求，然後再試一次。 |
| `1005-500` | 內部錯誤 | 發生內部錯誤。 請再試一次，如果問題仍然存在，請聯絡客戶支援。 |
| `1006-408` | 請求逾時 | 處理請求時發生錯誤。 要求已逾時。 請再試一次，如果問題仍然存在，請聯絡客戶支援。 |
| `1007-400` | 無效的標頭引數 | 收到無效的標頭引數：{headerName}。 請檢查標頭引數，然後再試一次。 |
| `1008-401` |  | 無效的授權權杖 | 授權權杖沒有此組織的存取權，或組織不存在。 請確定組織存在，或聯絡您的管理員以取得存取權。 |
| `1009-403` | IMS組織ID遺失或空白 | 組織ID請求標頭遺失或空白。 請更新標頭值並重試。 |
| `1010-500` | 無效的詳細訊息 | 詳細訊息中的引數未正確提供。 請檢查詳細訊息中的引數，然後再試一次。 |
| `1011-503` | 服務無法使用 | 服務暫時無法使用。 請再試一次，如果問題仍然存在，請聯絡客戶支援。 |
| `1012-504` | 閘道逾時 | 發生閘道逾時。 請再試一次，如果問題仍然存在，請聯絡客戶支援。 |
| `1013-412` | 先決條件失敗 | 不符合If-Unmodified-Since或If-None-Match標頭定義的條件。 請檢查並再試一次。 |
| `1014-400` | 錯誤請求非法引數 | 無法處理要求。 {detailedMessage} |

## 框架錯誤

| 錯誤代碼 | 標題 | 詳細訊息 |
| --- | --- | --- |
| `1100-400` | Bad Request | 無法處理要求。 {detailedMessage} |
| `1101-500` | 內部錯誤 | 發生內部錯誤。 請再試一次，如果問題仍然存在，請聯絡客戶支援。 |
| `1102-404` | 找不到資源 | 找不到請求的資源。 {detailedMessage} |
| `1103-503` | 服務無法使用 | 服務暫時無法使用。 請再試一次，如果問題仍然存在，請聯絡客戶支援。 |
| `1104-504` | 閘道逾時 | 發生閘道逾時。 請再試一次，如果問題仍然存在，請聯絡客戶支援。 |
| `1105-401` | 未獲授權 | 使用者未獲授權。 {detailedMessage} |
| `1106-403` | 已禁止 | 請求的操作被禁止。 {detailedMessage} |
| `1107-412` | 先決條件失敗 | 不符合If-Unmodified-Since或If-None-Match標頭定義的條件。 {detailedMessage} |

## 加密錯誤

| 錯誤代碼 | 標題 | 詳細訊息 |
| --- | --- | --- |
| `1200-500` | 內部錯誤 | 發生內部錯誤。 請再試一次，如果問題仍然存在，請聯絡客戶支援。 |
| `1201-400` | Bad Request | flowId不可為Null或空白。 請在請求中提供有效的flowId，然後再試一次。 |
| `1202-400` | Bad Request | 流程的transformations={transformations}中缺少publicKeyId。 請在請求中提供publicKeyId，然後再試一次。 |
| `1203-400` | Bad Request | 在流程的轉換={transformations}中，keyID={keyID}不存在加密金鑰。 請檢查您提供的keyID，然後重試。 |
| `1204-400` | Bad Request | 提供的加密演演算法無效。 請提供有效的加密演演算法，然後重試。 |
| `1205-400` | Bad Request | 提供的請求中的params區段中缺少密碼短語。 請在引數中提供passPhrase，然後再試一次。 |

## REST API錯誤

| 錯誤代碼 | 標題 | 詳細訊息 |
| --- | --- | --- |
| `1300-400` | Bad Request | {connectorType}聯結器不支援修補程式連線要求。 請檢查提供的請求，然後再試一次。 |
| `1301-400` | Bad Request | 不支援提供的authSpecType引數：{authSpecType}。 請提供有效的驗證規格型別，然後再試一次。 |
| `1302-400` | Bad Request | 提供的驗證型別= {authType}不支援聯結器={connectorType}。 請提供指定聯結器的有效驗證型別。 |
| `1303-400` | Bad Request | 無法使用指定的驗證引數來編碼URL，因為{value}不支援URL編碼。 請檢查您的驗證引數，然後再試一次。 |
| `1304-400` | Bad Request | 未提供必要欄位{field}。 請提供{field}，然後再試一次。 |
| `1305-400` | Bad Request | 此作業不支援提供的聯結器型別= {connectorType}。 |
| `1306-400` | Bad Request | 驗證目標連線規格ID時，目標連線不可為Null。 請檢查提供的請求，然後再試一次。 |
| `1307-400` | Bad Request | 目標連線規格ID無效={targetConnectionSpecId}。 允許值為： `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |
| `1308-400` | Bad Request | 無法處理要求。 錯誤訊息：{msftErrorMessage} |
| `1309-400` | Bad Request | 提供的加密轉換無效，因為引數中缺少{requiredParam}。 請提供{requiredParam}，然後再試一次。 |
| `1310-400` | Bad Request | 引數中提供的publicKeyId已過期。 請提供有效的publicKeyId，然後再試一次。 |
| `1311-400` | Bad Request | 引數中提供的publicKeyId無效。 請提供有效的publicKeyId，然後再試一次。 |
| 1312-400 | Bad Request | 提供的引數值{paramValue}不是property={requestParam}的有效輸入。 請提供有效的引數值，然後再試一次。 |
| `1313-400` | Bad Request | 路徑屬性{attribute}不存在。 請確定屬性存在，然後再試一次。 |
| `1314-400` | Bad Request | 已提供複雜路徑，但不允許。 請確定未提供複雜路徑，然後再試一次。 |
| `1315-400` | Bad Request | 提供的路徑{path}應指向記錄陣列。 請確定提供的路徑指向記錄陣列，然後再試一次。 |
| `1316-400` | Bad Request | 提供的分頁引數不應為空白。 請提供有效的分頁引數，然後再試一次。 |
| `1317-400` | Bad Request | 提供的排程引數為空白，但不應為空白。 請提供有效的排程引數，然後再試一次。 |
| `1318-400` | Bad Request | {combinedMessage}。 請檢查提供的請求，然後再試一次。 |
| `1319-400` | Bad Request | {param}應是父集合的一部分。 請在父集合中提供{param}，然後再試一次。 |
| `1320-400` | Bad Request | {idType}不可為Null或空白。 請提供有效的{idType}，然後再試一次。 |
| `1321-400` | Bad Request | {idType}的長度應為1，提供的大小為{size}。 請提供有效的大小，然後再試一次。 |
| `1322-400` | Bad Request | 建立結構描述參考時，來源連線不可為Null。 請提供有效的來源連線，然後重試。 |
| `1323-400` | Bad Request | 來源連線{sourceConnection}中的{entity}不能為null或空白。 請提供有效的{entity}，然後再試一次。 |
| `1324-400` | Bad Request | 擷取資料集ID時，目標連線不能為Null。 請提供有效的目標連線，然後重試。 |
| `1325-400` | Bad Request | 目標連線{TargetConnection}中的dataSetId引數不能為Null或空白。 請提供有效的dataSetId引數並重試。 |
| `1326-400` | Bad Request | 擷取來源格式時，來源連線不可為Null。 請提供有效的來源連線，然後重試。 |
| `1327-400` | Bad Request | 不支援SourceConnection中提供的來源資料格式={sourceFormat}。 允許的值為：{values}。 請提供允許的值，然後再試一次。 |
| `1328-400` | Bad Request | 擷取{param}時，對應轉換不能為Null。 請提供有效的對應轉換，然後再試一次。 |
| `1329-400` | Bad Request | 引數{param}在提供的請求中不能為null或空白。 請提供有效的{param}，然後再試一次。 |
| `1330-400` | Bad Request | 找不到資料表{tableName}的資料行。 請提供有效的資料表名稱，然後再試一次。 |
| `1331-400` | Bad Request | 欄分隔符號在SourceConnection {sourceConnection}中不能超過一個字元。 請提供有效的欄分隔符號，然後再試一次。 |
| `1332-400` | Bad Request | connectionSpecId為{connectionSpecId}的來源連線要求不能有baseConnectionId。 請移除baseConnectionId，然後再試一次。 |
| `1333-400` | 錯誤請求 | 規格ID={specId}的來源不支援flowRunAction={flowRunAction}。 請提供有效的流程執行動作，然後再試一次。 |
| `1334-400` | Bad Request | 查詢引數{param}不得為空白。 請提供有效的{param}，然後再試一次。 |
| `1335-400` | Bad Request | 序列化用於探索的篩選引數時發生錯誤。 請檢查您的篩選引數請求，然後再試一次。 |
| `1336-400` | Bad Request | 探索連線不支援連線規格ID：{connectionSpecId}。 請提供支援的連線規格ID，然後再試一次。 |
| `1337-400` | Bad Request | objectType={objectType}的{QueryParam}不得為空白。 請提供有效的{QueryParam}，然後再試一次。 |
| `1338-400` | Bad Request | 在flowRequest中，{connectionType}連線ID不可為Null。 請在flowRequest中提供有效的{connectionType}連線ID。 |
| `1339-400` | Bad Request | 請求中提供的organization={imsOrg}格式無效。 請提供有效的組織ID，然後重試。 |
| `1340-400` | Bad Request | 剖析{time}時發生錯誤。 請檢查請求中提供的時間格式，然後再試一次。 |
| `1341-400` | Bad Request | 提供的ODI Json是空的。 請提供有效的ODI Json，然後再試一次。 |
| `1342-400` | Bad Request | 「odi.json」中的「dls：folder」區段缺少定義。 請在&#39;odi.json&#39;中提供適當的定義，然後再試一次。 |
| `1343-400` | Bad Request | 「odi.json」中的「dls：entityReferences」和「dls：partitionSpec」區段都缺少定義。 請在&#39;odi.json&#39;中提供適當的定義，然後再試一次。 |
| `1344-400` | Bad Request | &#39;odi.json&#39;中&#39;dls：partitionSpec&#39;的定義無效，因為找到多個partitionSpec。 請在&#39;odi.json&#39;中提供適當的定義，然後再試一次。 |
| `1345-400` | Bad Request | 路徑中1或多個區段遺漏定義：`odi.json`中的`dls：partitionSpec/dls：fileFormat`、`dls：partitionSpec/dls：partitionTemplate`、`dls：partitionSpec/dls：fileFormat/@type`、`dls：partitionSpec/dls：fileFormat/dls：csvDelimiters`。 請在&#39;odi.json&#39;中提供適當的定義，然後再試一次。 |
| `1346-400` | Bad Request | 在&#39;odi.json&#39;的&#39;dls：fileFormat&#39;中提供的&#39;@type&#39;定義無效。 請在&#39;odi.json&#39;中提供適當的定義，然後再試一次。 |
| `1347-400` | Bad Request | 不支援「odi.json」中的dls：csvDelimiters」定義。 支援的csvDelimiters包括： [&#39;，&#39;]. 請在&#39;odi.json&#39;中提供適當的定義，然後再試一次。 |
| `1348-400` | Bad Request | 將「dls：entityReferences」還原序列化時發生錯誤。 請檢查資料格式是否有效，然後再試一次。 |
| `1349-400` | Bad Request | 提供的篩選引數無效。 請提供有效的篩選引數，然後再試一次。 |
| `1350-400` | Bad Request | 來源中沒有提供用於篩選的運運算元。 請提供具有適當運運算元的有效篩選條件請求，然後再試一次。 |
| `1351-400` | Bad Request | 提供的運運算元{operator}不支援此聯結器的來源篩選條件。 請提供有效的運運算元，然後重試。 |
| `1352-400` | Bad Request | 提供的運運算元{operator}無法對應到{ql}支援的任何原生運運算元。 請提供有效的運運算元，然後重試。 |
| `1353-400` | Bad Request | {connectorType}聯結器尚不支援來源處的篩選器。 請檢視檔案中支援的聯結器： https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/filter.html。 |
| `1354-400` | Bad Request | 來源處的篩選器尚不支援查詢語言{ql}。 請提供有效的查詢語言，然後再試一次。 |
| `1355-400` | Bad Request | 提供的篩選型別無效。 支援的篩選型別是： PQL。 請提供有效的篩選器型別，然後再試一次。 |
| `1356-400` | Bad Request | 提供的篩選格式無效。 支援的篩選器格式為： pql/json。 請提供有效的篩選格式，然後再試一次。 |
| `1357-400` | Bad Request | 提供的篩選器無效。 該值必須隨附詳細篩選器。 請提供有效的篩選器，然後再試一次。 |
| `1358-400` | Bad Request | 提供的引數&#39;objectType&#39;無效。 請提供有效的objectType，然後再試一次。 |
| `1359-400` | Bad Request | 請求中缺少引數{param}。 請提供有效的{param}，然後再試一次。 |
| `1360-400` | Bad Request | 開始時間不能設定在過去。 請提供有效的開始時間，然後重試。 |
| `1361-400` | Bad Request | 不允許間隔一次內嵌。 請移除間隔或變更頻率，然後重試。 |
| `1362-400` | Bad Request | 間隔不能小於{minInterval}。 請提供有效的間隔值，然後再試一次。 |
| `1363-400` | Bad Request | 間隔{interval}不允許使用頻率：{frequency}。 請提供有效的間隔值，然後再試一次。 |
| `1364-400` | Bad Request | 當頻率設為1時，不允許使用回填旗標。 當頻率設定為一次時，請移除回填旗標，然後再試一次。 |
| `1365-400` | Bad Request | ops中提供的路徑{path}無效。 請提供有效的路徑{path}，然後再試一次。 |
| `1366-400` | Bad Request | 開始時間已過，不再允許更新操作。 |
| `1367-400` | Bad Request | 建立CRM聯結器時，複製轉換需要差異欄。 請提供差異欄，然後再試一次。 |
| `1368-400` | Bad Request | 流程請求中不允許模式。 請檢查您的請求，然後再試一次。 |
| `1369-400` | Bad Request | 頻率設定為一次時，複製轉換中不允許差異欄。 請移除差異欄，然後再試一次。 |
| `1370-400` | Bad Request | 無法擷取來源資料行以供擷取，因為缺少對應轉換。 請新增對應轉換，然後重試。 |
| `1371-400` | Bad Request | {connectorType}聯結器不支援檔案屬性偵測。 請手動提供檔案屬性。 |
| `1372-400` | Bad Request | 不允許目前操作。 連線規格ID={connectionSpecId}不允許透過連線規格探索。 |
| `1373-400` | Bad Request | 請求中缺少flowSpecType。 請提供有效的flowSpecType，然後再試一次。 |
| `1374-400` | Bad Request | 提供的查詢引數無效。 同一請求中不能有determineProperties旗標和使用者定義的屬性。 請修正您的請求，然後再試一次。 |
| `1375-400` | Bad Request | 檔案屬性偵測失敗。 請手動輸入屬性。 |
| `1376-400` | Bad Request | 連線規格id={connectionSpecId}不支援檔案屬性偵測。 請手動提供檔案屬性。 |
| `1377-400` | Bad Request | 提供的值引數為null，無法與運運算元{operator}比較。 請提供有效的值引數，然後再試一次。 |
| `1378-400` | Bad Request | 驗證來源篩選器的輸入資料行{column}時發生錯誤。 資料行名稱應為表格中的有效資料行。 請提供有效的欄名稱，然後再試一次。 |
| `1379-400` | Bad Request | 驗證來源篩選器的輸入{value}時發生錯誤。 來源處的資料行DataType是{columnDataType}且值為DataType [字串] 不符合。 請提供有效的{value}，然後再試一次。 |
| `1380-400` | Bad Request | 無法建立資料流執行。 錯誤訊息：{message} |
| `1381-400` | Bad Request | WindowEndTime={endTime}不能早於Window StartTime={startTime}。 請提供有效的結束時間，然後重試。 |
| `1382-400` | Bad Request | 差異欄應該和流程的「複製轉換」中存在的值相符。 請提供有效的差異欄並重試。 |
| `1383-400` | Bad Request | 在建立資料流執行時收到的引數中缺少差異資料行。 請在引數中提供差異欄，然後再試一次。 |
| `1384-400` | Bad Request | 為建立資料流執行而提供的params={params}無效或空白。 請提供有效的引數，然後再試一次。 |
| `1385-400` | Bad Request | 提供的connectorType={connectorType}不支援建立流程執行。 請提供有效的connectorType，然後再試一次。 |
| `1386-400` | Bad Request | 不支援使用scheduleParams frequency={frequency}的flowId={flowId}建立流量執行。 請提供有效的頻率，然後再試一次。 |
| `1387-400` | Bad Request | flowRunId={flowRunId}處於無效狀態={state}，無法重新觸發。 請稍後再試，如果問題仍然存在，請聯絡客戶支援。 |
| `1388-400` | Bad Request | 流程={flow}處於state={state}狀態，無法重新觸發。 流程必須處於啟用狀態才能重新觸發。 |
| `1389-400` | Bad Request | 剖析提供的base64編碼字串時發生錯誤。 請提供有效的編碼篩選字串，然後再試一次。 |
| `1390-400` | Bad Request | &#39;not&#39;運運算元只能有一個比較。 請提供有效的比較次數，然後再試一次。 |
| `1391-400` | Bad Request | 無法剖析Id={sourceConnectionId}的sourceConnection中的SchemaMetaData。 請檢查請求中的schemaMetaData，然後再試一次。 |
| `1392-400` | Bad Request | 無法剖析flowId={flowId}的流程請求中的轉換。 請檢查請求中的轉換，然後再試一次。 |
| `1393-400` | Bad Request | 提供的引數{parameter}為Null或空白。 請提供有效的{parameter}，然後再試一次。 |
| `1394-400` | Bad Request | 引數{parameter}的最小值是1。 請提供有效的{parameter}，然後再試一次。 |
| `1395-400` | Bad Request | 在流程中找到的來源連線為Null或空白。 請在流程中提供有效的來源連線，然後重試。 |
| `1396-400` | Bad Request | 找不到符合的格式。 請提供相符的格式，然後再試一次。 |
| `1397-400` | Bad Request | 提供的頻率：{frequency}無效。 請提供有效的頻率，然後再試一次。 |
| `1398-400` | Bad Request | 不支援提供的操作：{action}。 請檢查所提供的操作，然後再試一次。 |
| `1399-400` | Bad Request | 找不到有效的requestFileType。 請提供有效的requestFileType，然後再試一次。 |
| `1400-400` | Bad Request | 提供的引數「templateType」無效。 請提供有效的範本型別，然後重試。 |
| `1401-400` | Bad Request | 不支援提供的資料流執行action={flowRunAction}。 請提供有效的資料流執行動作，然後再試一次。 |
| `1402-500` | 內部錯誤 | 發生內部錯誤。 請再試一次，如果問題仍然存在，請聯絡客戶支援。 |
| `1403-400` | Bad Request | 開始時間已過，您無法再將頻率變更為一次。 |
| `1404-400` | Bad Request | 開始時間已過，您無法再更新回填。 |

## 流程服務例外(1600-1699)

| 錯誤代碼 | 標題 | 詳細訊息 |
| --- | --- | --- |
| `1600-400` | Bad Request | 無法處理要求。 {detailedMessage} |
| `1601-500` | 內部錯誤 | 發生內部錯誤。 請再試一次，如果問題仍然存在，請聯絡客戶支援。 |
| `1602-404` | 找不到資源 | 找不到請求的資源。 {detailedMessage} |
| `1603-503` | 服務無法使用 | 服務暫時無法使用。 請重試。如果問題仍然存在，請聯絡客戶支援。 |
| `1604-504` | 閘道逾時 | 發生閘道逾時。 請重試。如果問題仍然存在，請聯絡客戶支援。 |
| `1605-401` | 未獲授權 | 使用者未獲授權。 {detailedMessage} |
| `1606-403` | 已禁止 | 請求的操作被禁止。 {detailedMessage} |
| `1607-412` | 先決條件失敗 | 不符合If-Unmodified-Since或If-None-Match標頭定義的條件。 {detailedMessage} |

## 資料登陸區域錯誤

| 錯誤代碼 | 標題 | 詳細訊息 |
| --- | --- | --- |
| `1700-500` | 內部錯誤 | 發生內部錯誤。 請再試一次，如果問題仍然存在，請聯絡客戶支援。 |
| `1701-400` | Bad Request | 提供的登陸區域為非作用中。 請啟動登陸區域，然後再試一次。 |
| `1702-400` | Bad Request | 不允許為登陸區域提供的SAS Type={sasType}。 請提供有效的SAS，然後再試一次。 |
| `1703-400` | Bad Request | 不允許重新整理認證。 |
| `1704-400` | Bad Request | 針對subscriptionId={subscriptionId}和resourceGroupName={resourceGroupName}中的storageAccountName={accountName}傳回的金鑰格式錯誤。 請檢查您的請求，然後再試一次。 如果問題仍然存在，請聯絡支援人員。 |
| `1705-400` | Bad Request | 不支援提供的資料登陸區域動作。 請提供有效的動作，然後再試一次。 |
| `1706-400` | Bad Request | 登陸區域={landingZoneType}的允許啟用設定未正確設定。 請再試一次，如果問題仍然存在，請聯絡客戶支援。 |
| `1707-400` | Bad Request | 服務無法啟動，因為登入區域設定不能為Null或空白。 請確定登陸區域設定不是Null，然後再試一次。 |
| `1708-400` | Bad Request | 容器設定在landingZoneType={landingZoneType}中不能為Null。 請確定容器設定不是Null，然後再試一次。 |
| `1709-400` | Bad Request | 在landingZoneType={landingZoneType}中，{tokenConfig}的SAS詳細資料不可為Null。 請在設定中提供有效的SAS，然後再試一次。 |
| `1710-400` | Bad Request | 不支援提供的型別{landingZoneUseCase}的登陸區域。 請提供有效的登陸區域型別，然後再試一次。 |
| `1711-400` | Bad Request | 找不到所提供型別為{landingZoneUseCase}的資料登陸區域的SAS詳細資料。 請檢查是否針對提供的登陸區域型別提供了SAS詳細資料。 |
| `1712-400` | Bad Request | 不允許提供的登陸區域動作：{actionType}。 請提供有效的資料登陸區域動作，然後重試。 |
| `1713-400` | Bad Request | 提供的{tokenType}不允許使用{OperationType}。 請檢查您的請求，然後再試一次。 |
| `1714-400` | Bad Request | 不允許clientId={clientId}執行此作業。 請檢查您的許可權請求，然後再試一次。 |
