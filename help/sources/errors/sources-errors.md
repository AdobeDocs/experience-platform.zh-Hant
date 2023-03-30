---
title: 源錯誤消息
description: 了解將流程服務用於來源時可能會遇到的錯誤訊息。
source-git-commit: 10edb5dfd9ce99b69cf5bb014f4903942c9bff3e
workflow-type: tm+mt
source-wordcount: '3192'
ht-degree: 8%

---

# 源錯誤消息

本文檔提供錯誤消息、說明和源建議的解決方案的目錄。

## 一般錯誤

| 錯誤代碼 | 標題 | 詳細訊息 |
| --- | --- | --- |
| `1000-400` | 錯誤請求 | 請求無效。 請檢查請求，然後重試。 |
| `1001-401` | 未授權 | 用戶未授權。 請連絡您的管理員以取得資源的存取權。 |
| `1002-403` | 禁止 | 禁止請求的操作。 請檢查請求的操作，然後重試。 |
| `1003-404` | 未找到資源 | 未找到請求的資源。 請檢查提供的請求，然後重試。 |
| `1004-415` | 不支援的媒體類型 | 不支援提供的裝載格式。 請檢查您提供的請求，然後重試。 |
| `1005-500` | 內部錯誤 | 發生內部錯誤。 如果問題仍然存在，請重試並聯繫客戶支援。 |
| `1006-408` | 請求逾時 | 處理請求時出錯。 請求已超時。 如果問題仍然存在，請重試並聯繫客戶支援。 |
| `1007-400` | 標題參數無效 | 標題參數無效：已接收{headerName}。 請檢查標題參數，然後重試。 |
| `1008-401` |  | 授權令牌無效 | 授權Token沒有此組織的存取權，或組織不存在。 請確保組織存在，或與管理員聯繫以獲得訪問權限。 |
| `1009-403` | IMS組織ID遺失或空白 | 組織ID請求標題遺失或空白。 請更新標題值，然後重試。 |
| `1010-500` | 無效的詳細消息 | 未正確提供詳細訊息中的參數。 請檢查詳細資訊中的參數，然後重試。 |
| `1011-503` | 服務不可用 | 服務暫時不可用。 如果問題仍然存在，請重試並聯繫客戶支援。 |
| `1012-504` | 網關超時 | 已發生網關超時。 如果問題仍然存在，請重試並聯繫客戶支援。 |
| `1013-412` | 先決條件失敗 | 由If-Undificed-Sine或If-None-Match標題定義的條件未達成。 請檢查並重試。 |
| `1014-400` | Bad Request Illigal引數 | 無法處理請求。 {detailedMessage} |

## 框架錯誤

| 錯誤代碼 | 標題 | 詳細訊息 |
| --- | --- | --- |
| `1100-400` | Bad Request | 無法處理請求。 {detailedMessage} |
| `1101-500` | 內部錯誤 | 發生內部錯誤。 如果問題仍然存在，請重試並聯繫客戶支援。 |
| `1102-404` | 未找到資源 | 未找到請求的資源。 {detailedMessage} |
| `1103-503` | 服務不可用 | 服務暫時不可用。 如果問題仍然存在，請重試並聯繫客戶支援。 |
| `1104-504` | 網關超時 | 已發生網關超時。 如果問題仍然存在，請重試並聯繫客戶支援。 |
| `1105-401` | 未授權 | 用戶未授權。 {detailedMessage} |
| `1106-403` | 禁止 | 禁止請求的操作。 {detailedMessage} |
| `1107-412` | 先決條件失敗 | 由If-Undificed-Sine或If-None-Match標題定義的條件未達成。 {detailedMessage} |

## 加密錯誤

| 錯誤代碼 | 標題 | 詳細訊息 |
| --- | --- | --- |
| `1200-500` | 內部錯誤 | 發生內部錯誤。 如果問題仍然存在，請重試並聯繫客戶支援。 |
| `1201-400` | Bad Request | flowId不能為null或為空。 請在請求中提供有效的flowId，然後重試。 |
| `1202-400` | Bad Request | 流的轉換={transformations}中缺少publicKeyId。 請在請求中提供publicKeyId，然後重試。 |
| `1203-400` | Bad Request | 在流的轉換={transformations}中，對keyID={keyID}不存在加密密鑰。 請檢查您提供的keyID，然後重試。 |
| `1204-400` | Bad Request | 提供的加密算法無效。 請提供有效的加密算法，然後重試。 |
| `1205-400` | Bad Request | 提供的請求的params區段中缺少密碼短語。 請在參數中提供passPhrase，然後重試。 |

## REST API錯誤

| 錯誤代碼 | 標題 | 詳細訊息 |
| --- | --- | --- |
| `1300-400` | Bad Request | {connectorType}連接器不支援修補程式連接請求。 請檢查提供的請求，然後重試。 |
| `1301-400` | Bad Request | 提供的authSpecType參數：不支援{authSpecType}。 請提供有效的驗證規範類型，然後重試。 |
| `1302-400` | Bad Request | 連接器={connectorType}不支援提供的驗證類型= {authType}。 請為給定連接器提供有效的驗證類型。 |
| `1303-400` | Bad Request | 無法使用指定的驗證參數對URL進行編碼，因為{value}不支援URL編碼。 請檢查驗證參數，然後重試。 |
| `1304-400` | Bad Request | 未提供必填欄位{field}。 請提供{field}，然後重試。 |
| `1305-400` | Bad Request | 此操作不支援提供的連接器類型= {connectorType}。 |
| `1306-400` | Bad Request | 驗證目標連接規範ID時，目標連接不能為Null。 請檢查提供的請求，然後重試。 |
| `1307-400` | Bad Request | 目標連接規範ID無效={targetConnectionSpecId}。 允許的值為： `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |
| `1308-400` | Bad Request | 無法處理請求。 錯誤訊息：{msftErrorMessage} |
| `1309-400` | Bad Request | 提供的加密轉換無效，因為參數中缺少{requiredParam}。 請提供{requiredParam}，然後重試。 |
| `1310-400` | Bad Request | 參數中提供的publicKeyId已過期。 請提供有效的publicKeyId，然後重試。 |
| `1311-400` | Bad Request | params中提供的publicKeyId無效。 請提供有效的publicKeyId，然後重試。 |
| 1312-400 | Bad Request | 提供的參數值{paramValue}不是屬性={requestParam}的有效輸入。 請提供有效的參數值，然後重試。 |
| `1313-400` | Bad Request | 路徑屬性{attribute}不存在。 請確保屬性存在，然後重試。 |
| `1314-400` | Bad Request | 已提供複雜路徑，但不允許。 請確保未提供複雜路徑，然後重試。 |
| `1315-400` | Bad Request | 提供的路徑{path}應指向一個記錄陣列。 請確保提供的路徑指向記錄陣列，然後重試。 |
| `1316-400` | Bad Request | 提供的分頁參數不應為空。 請提供有效的分頁參數，然後重試。 |
| `1317-400` | Bad Request | 提供的排程參數為空，但不應為空。 請提供有效的計畫參數，然後重試。 |
| `1318-400` | Bad Request | {combinedMessage}。 請檢查提供的請求，然後重試。 |
| `1319-400` | Bad Request | {param}應屬於父集合。 請在父集合中提供{param}，然後重試。 |
| `1320-400` | Bad Request | {idType}不能為Null或為空。 請提供有效的{idType}，然後重試。 |
| `1321-400` | Bad Request | {idType}的長度應為1，提供的大小為{size}。 請提供有效的大小，然後重試。 |
| `1322-400` | Bad Request | 源連接不能為空，無法用於構建架構引用。 請提供有效的源連接，然後重試。 |
| `1323-400` | Bad Request | 源連接中的{entity}不能為Null或為空：{sourceConnection}。 請提供有效的{entity}，然後重試。 |
| `1324-400` | Bad Request | 擷取資料集ID時，目標連線不能為null。 請提供有效的目標連接，然後重試。 |
| `1325-400` | Bad Request | Target連線中的dataSetId參數不能為null或空：{TargetConnection}。 請提供有效的dataSetId參數，然後重試。 |
| `1326-400` | Bad Request | 提取源格式時，源連接不能為null。 請提供有效的源連接，然後重試。 |
| `1327-400` | Bad Request | 不支援SourceConnection中提供的源資料={sourceFormat}的格式。 允許的值為：{values}。 請提供允許的值，然後重試。 |
| `1328-400` | Bad Request | 提取{param}時，映射轉換不能為null。 請提供有效的映射轉換，然後重試。 |
| `1329-400` | Bad Request | 參數：提供的請求中的{param}不能為null或空。 請提供有效的{param}，然後重試。 |
| `1330-400` | Bad Request | 未找到表{tableName}的列。 請提供有效的表名，然後重試。 |
| `1331-400` | Bad Request | SourceConnection中的列分隔符不能多於一個字元：{sourceConnection}。 請提供有效的列分隔符，然後重試。 |
| `1332-400` | Bad Request | 具有connectionSpecId的源連接請求：{connectionSpecId}不能有baseConnectionId。 請刪除baseConnectionId，然後重試。 |
| `1333-400` | 錯誤請求 | 規格id={specId}的源不支援flowRunAction={flowRunAction}。 請提供有效的流運行操作，然後重試。 |
| `1334-400` | Bad Request | 查詢參數：{param}不能為空。 請提供有效的{param}，然後重試。 |
| `1335-400` | Bad Request | 序列化篩選器參數以進行瀏覽時出錯。 請檢查您的篩選參數請求，然後重試。 |
| `1336-400` | Bad Request | 連接規範ID不支援瀏覽連接：{connectionSpecId}。 請提供支援的連接規範id，然後重試。 |
| `1337-400` | Bad Request | objectType={objectType}的{QueryParam}不能為空。 請提供有效的{QueryParam}，然後重試。 |
| `1338-400` | Bad Request | flowRequest中的{connectionType}連接ID不能為null。 請在flowRequest中提供有效的{connectionType}連接ID。 |
| `1339-400` | Bad Request | 請求中提供的組織={imsOrg}格式無效。 請提供有效的組織ID，然後重試。 |
| `1340-400` | Bad Request | 分析{time}時出錯。 請檢查請求中提供的時間格式，然後重試。 |
| `1341-400` | Bad Request | 提供的ODI Json為空。 請提供有效的ODI Json，然後重試。 |
| `1342-400` | Bad Request | 「odi.json」中的「dls:folder」區段缺少定義。 請在&#39;odi.json&#39;中提供適當的定義，然後再試一次。 |
| `1343-400` | Bad Request | 「odi.json」中的「dls:entityReferences」和「dls:partitionSpec」區段均缺少定義。 請在&#39;odi.json&#39;中提供適當的定義，然後再試一次。 |
| `1344-400` | Bad Request | 「odi.json」中「dls:partitionSpec」的定義無效，因為找到了多個partitionSpec。 請在&#39;odi.json&#39;中提供適當的定義，然後再試一次。 |
| `1345-400` | Bad Request | 路徑中1個或多個區段缺少定義：「dls:partitionSpec/dls:fileFormat」，「dls:partitionSpec/dls:partitionTemplate」，「dls:partitionSpec/dls:fileFormat/@type」，「odi.json」中的「dls:partitionSpec/dls:fileFormat/dls:fileFormat/dls:csvDelimeters」。 請在&#39;odi.json&#39;中提供適當的定義，然後再試一次。 |
| `1346-400` | Bad Request | 「odi.json」中「dls:fileFormat」中提供的「@type」定義無效。 請在&#39;odi.json&#39;中提供適當的定義，然後再試一次。 |
| `1347-400` | Bad Request | 「odi.json」不支援dls:csvDellifiters定義。 支援的csvDellimeter包括： [&#39;,&#39;]. 請在&#39;odi.json&#39;中提供適當的定義，然後再試一次。 |
| `1348-400` | Bad Request | 反序列化「dls:entityReferences」時出錯。 請檢查資料的格式是否有效，然後重試。 |
| `1349-400` | Bad Request | 提供的篩選參數無效。 請提供有效的篩選參數，然後重試。 |
| `1350-400` | Bad Request | 未為源的篩選提供任何運算子。 請提供具有適當運算子的有效篩選請求，然後重試。 |
| `1351-400` | Bad Request | 提供的運算子{operator}不支援用於此連接器的源篩選器。 請提供有效的運算子，然後重試。 |
| `1352-400` | Bad Request | 提供的運算子{operator}無法映射到{ql}的任何受支援的本機運算子。 請提供有效的運算子，然後重試。 |
| `1353-400` | Bad Request | {connectorType}連接器尚不支援源處的篩選器。 請查看文檔中支援的連接器：https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/filter.html。 |
| `1354-400` | Bad Request | 尚未支援對源進行篩選的查詢語言{ql}。 請提供有效的查詢語言，然後重試。 |
| `1355-400` | Bad Request | 提供的篩選類型無效。 支援的篩選類型為：PQL。 請提供有效的篩選類型，然後重試。 |
| `1356-400` | Bad Request | 提供的篩選格式無效。 支援的篩選格式為：pql/json。 請提供有效的篩選格式，然後重試。 |
| `1357-400` | Bad Request | 提供的篩選器無效。 值必須隨附詳細的篩選器。 請提供有效的篩選器，然後重試。 |
| `1358-400` | Bad Request | 提供的參數&#39;objectType&#39;無效。 請提供有效的objectType，然後重試。 |
| `1359-400` | Bad Request | 請求中缺少參數{param}。 請提供有效的{param}，然後重試。 |
| `1360-400` | Bad Request | 開始時間不能設定在過去。 請提供有效的開始時間，然後重試。 |
| `1361-400` | Bad Request | 一次擷取不允許使用間隔。 請刪除時間間隔或更改頻率，然後重試。 |
| `1362-400` | Bad Request | 間隔不能小於{minInterval}。 請提供有效的時間間隔值，然後重試。 |
| `1363-400` | Bad Request | 頻率不允許間隔{interval}:{frequency}。 請提供有效的時間間隔值，然後重試。 |
| `1364-400` | Bad Request | 頻率設為一時，不允許回填標幟。 頻率設為一次時，請移除回填標幟，然後重試。 |
| `1365-400` | Bad Request | 操作中提供的路徑{path}無效。 請提供有效的路徑{path}，然後重試。 |
| `1366-400` | Bad Request | 開始時間已過，不再允許更新操作。 |
| `1367-400` | Bad Request | 建立CRM連接器時，複製轉換中需要差值欄。 請提供增量列，然後重試。 |
| `1368-400` | Bad Request | 流程請求中不允許使用模式。 請檢查您的請求，然後重試。 |
| `1369-400` | Bad Request | 頻率設為一次時，不允許複製轉換中的增量列。 請刪除增量列，然後重試。 |
| `1370-400` | Bad Request | 由於缺少映射轉換，無法為獲取提取源列。 請添加映射轉換，然後重試。 |
| `1371-400` | Bad Request | {connectorType}連接器不支援檔案屬性檢測。 請手動提供檔案屬性。 |
| `1372-400` | Bad Request | 不允許當前操作。 連接規範ID={connectionSpecId}不允許通過連接規範進行瀏覽。 |
| `1373-400` | Bad Request | 請求中缺少flowSpecType。 請提供有效的flowSpecType，然後重試。 |
| `1374-400` | Bad Request | 提供的查詢參數無效。 同一請求中不能有determineProperties標幟和用戶定義的屬性。 請更正您的請求，然後重試。 |
| `1375-400` | Bad Request | 檔案屬性檢測失敗。 請手動輸入屬性。 |
| `1376-400` | Bad Request | 連接規範id={connectionSpecId}不支援檔案屬性檢測。 請手動提供檔案屬性。 |
| `1377-400` | Bad Request | 提供的值參數為Null，無法與運算子{operator}進行比較。 請提供有效的值參數，然後重試。 |
| `1378-400` | Bad Request | 驗證源的篩選器的輸入列{column}時出錯。 列名應是表中的有效列。 請提供有效的列名，然後重試。 |
| `1379-400` | Bad Request | 驗證源的篩選器的輸入{value}時出錯。 源處的列DataType為{columnDataType}，值為DataType [字串] 不符合。 請提供有效的{value}，然後重試。 |
| `1380-400` | Bad Request | 無法建立流運行。 錯誤訊息：{message} |
| `1381-400` | Bad Request | WindowEndTime={endTime}不能早於Window StartTime={startTime}。 請提供有效的結束時間，然後重試。 |
| `1382-400` | Bad Request | 增量列應與流的「複製」轉換中存在的值匹配。 請提供有效的增量列，然後重試。 |
| `1383-400` | Bad Request | 為建立流運行而接收的參數中缺少增量列。 請在參數中提供增量列，然後重試。 |
| `1384-400` | Bad Request | 為建立流運行而提供的params={params}無效或為空。 請提供有效的參數，然後重試。 |
| `1385-400` | Bad Request | 不支援提供的connectorType={connectorType}來建立流運行。 請提供有效的connectorType，然後重試。 |
| `1386-400` | Bad Request | 建立流運行時不支援具有scheduleParams frequency={frequency}的flowId={flowId}。 請提供有效的頻率，然後重試。 |
| `1387-400` | Bad Request | flowRunId={flowRunId}處於無效狀態={state}，無法重新觸發。 請稍後再試，如果問題仍然存在，請聯繫客戶支援。 |
| `1388-400` | Bad Request | 流={flow}處於狀態={state}，無法重新觸發。 流必須處於啟用狀態才能重新觸發。 |
| `1389-400` | Bad Request | 分析提供的base64編碼字串時出錯。 請提供有效的編碼篩選器字串，然後重試。 |
| `1390-400` | Bad Request | 「not」運算子只能有一個比較。 請提供有效的比較數，然後重試。 |
| `1391-400` | Bad Request | 無法分析sourceConnection中SchemaMetaData的Id={sourceConnectionId}。 請檢查請求中的schemaMetaData，然後重試。 |
| `1392-400` | Bad Request | 無法分析flowId={flowId}的流請求中的轉換。 請檢查請求中的轉換，然後重試。 |
| `1393-400` | Bad Request | 提供的參數{parameter}為Null或空。 請提供有效的{parameter}，然後重試。 |
| `1394-400` | Bad Request | 參數{parameter}的最小值為1。 請提供有效的{parameter}，然後重試。 |
| `1395-400` | Bad Request | 在流中找到的源連接為null或為空。 請在流中提供有效的源連接，然後重試。 |
| `1396-400` | Bad Request | 找不到匹配的格式。 請提供匹配的格式，然後重試。 |
| `1397-400` | Bad Request | 提供的頻率：{frequency}無效。 請提供有效的頻率，然後重試。 |
| `1398-400` | Bad Request | 提供的操作：不支援{action}。 請檢查提供的操作，然後重試。 |
| `1399-400` | Bad Request | 找不到有效的requestFileType。 請提供有效的requestFileType，然後重試。 |
| `1400-400` | Bad Request | 提供的參數&#39;templateType&#39;無效。 請提供有效的模板類型，然後重試。 |
| `1401-400` | Bad Request | 不支援提供的流運行操作={flowRunAction}。 請提供有效的流運行操作，然後重試。 |
| `1402-500` | 內部錯誤 | 發生內部錯誤。 如果問題仍然存在，請重試並聯繫客戶支援。 |
| `1403-400` | Bad Request | 開始時間已過，您無法再將頻率變更為一次。 |
| `1404-400` | Bad Request | 開始時間已過，您無法再更新回填。 |

## 流服務例外(1600-1699)

| 錯誤代碼 | 標題 | 詳細訊息 |
| --- | --- | --- |
| `1600-400` | Bad Request | 無法處理請求。 {detailedMessage} |
| `1601-500` | 內部錯誤 | 發生內部錯誤。 如果問題仍然存在，請重試並聯繫客戶支援。 |
| `1602-404` | 未找到資源 | 未找到請求的資源。 {detailedMessage} |
| `1603-503` | 服務不可用 | 服務暫時不可用。 請重試。如果問題仍然存在，請聯繫客戶支援。 |
| `1604-504` | 網關超時 | 已發生網關超時。 請重試。如果問題仍然存在，請聯繫客戶支援。 |
| `1605-401` | 未授權 | 用戶未授權。 {detailedMessage} |
| `1606-403` | 禁止 | 禁止請求的操作。 {detailedMessage} |
| `1607-412` | 先決條件失敗 | 由If-Undificed-Sine或If-None-Match標題定義的條件未達成。 {detailedMessage} |

## 資料登錄區錯誤

| 錯誤代碼 | 標題 | 詳細訊息 |
| --- | --- | --- |
| `1700-500` | 內部錯誤 | 發生內部錯誤。 如果問題仍然存在，請重試並聯繫客戶支援。 |
| `1701-400` | Bad Request | 提供的登陸區域非作用中。 請激活登錄區域，然後重試。 |
| `1702-400` | Bad Request | 不允許為登錄區域提供SAS類型={sasType}。 請提供有效的SAS，然後重試。 |
| `1703-400` | Bad Request | 不允許刷新憑據。 |
| `1704-400` | Bad Request | subscriptionId={subscriptionId}和resourceGroupName={resourceGroupName}中為storageAccountName={accountName}返回的密鑰格式不正確。 請檢查您的請求，然後重試。 如果問題仍然存在，請與支援人員聯繫。 |
| `1705-400` | Bad Request | 不支援提供的資料登錄區動作。 請提供有效的操作，然後重試。 |
| `1706-400` | Bad Request | 未為登錄區域={landingZoneType}正確配置允許的激活配置。 如果問題仍然存在，請重試並聯繫客戶支援。 |
| `1707-400` | Bad Request | 服務無法啟動，因為登錄區域配置不能為null或為空。 請確保登錄區域配置非空，然後重試。 |
| `1708-400` | Bad Request | landingZoneType={landingZoneType}中的容器配置不能為null。 請確保容器配置非空值，然後重試。 |
| `1709-400` | Bad Request | landingZoneType={landingZoneType}中{tokenConfig}的SAS詳細資訊不能為null。 請在配置中提供有效的SAS，然後重試。 |
| `1710-400` | Bad Request | 提供的著陸區類型：不支援{landingZoneUseCase}。 請提供有效的登錄區域類型，然後重試。 |
| `1711-400` | Bad Request | 找不到所提供類型資料登錄區的SAS詳細資訊：{landingZoneUseCase}。 請檢查是否提供了所提供登錄區域類型的SAS詳細資訊。 |
| `1712-400` | Bad Request | 提供的登陸區動作：不允許{actionType}。 請提供有效的資料登錄區域操作，然後重試。 |
| `1713-400` | Bad Request | 提供的{tokenType}不允許{OperationType}。 請檢查您的請求，然後重試。 |
| `1714-400` | Bad Request | 不允許clientId={clientId}執行此操作。 請使用權限檢查您的請求，然後重試。 |