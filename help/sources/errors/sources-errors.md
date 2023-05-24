---
title: 源錯誤消息
description: 瞭解在對源使用流服務時可能遇到的錯誤消息。
exl-id: cfba9780-4ab9-447b-8c60-c9f813107d11
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '3192'
ht-degree: 8%

---

# 源錯誤消息

此文檔提供錯誤消息、說明和源建議解決方案的目錄。

## 一般錯誤

| 錯誤代碼 | 標題 | 詳細消息 |
| --- | --- | --- |
| `1000-400` | 錯誤請求 | 請求無效。 請檢查請求，然後重試。 |
| `1001-401` | 未授權 | 用戶未授權。 請與管理員聯繫以獲得對資源的訪問權限。 |
| `1002-403` | 禁止 | 禁止請求的操作。 請檢查請求的操作，然後重試。 |
| `1003-404` | 找不到資源 | 找不到請求的資源。 請檢查提供的請求，然後重試。 |
| `1004-415` | 不支援的媒體類型 | 不支援提供的負載格式。 請檢查您提供的請求，然後重試。 |
| `1005-500` | 內部錯誤 | 發生內部錯誤。 如果問題仍然存在，請重試並聯繫客戶支援。 |
| `1006-408` | 請求超時 | 處理請求時出錯。 請求已超時。 如果問題仍然存在，請重試並聯繫客戶支援。 |
| `1007-400` | 標頭參數無效 | 無效的標頭參數：已收到{headerName}。 請檢查標題參數，然後重試。 |
| `1008-401` |  | 授權令牌無效 | 授權令牌無權訪問此組織或該組織不存在。 請確保組織存在或與管理員聯繫以獲取訪問權限。 |
| `1009-403` | IMS組織ID缺失或為空 | 組織ID請求標頭缺失或為空。 請更新標頭值，然後重試。 |
| `1010-500` | 無效的詳細消息 | 未正確提供detailed-message中的參數。 請檢查詳細消息中的參數，然後重試。 |
| `1011-503` | 服務不可用 | 服務暫時不可用。 如果問題仍然存在，請重試並聯繫客戶支援。 |
| `1012-504` | 網關超時 | 網關超時。 如果問題仍然存在，請重試並聯繫客戶支援。 |
| `1013-412` | 先決條件失敗 | 未滿足If-Unomodifed-Sine或If-None-Match標頭定義的條件。 請檢查並重試。 |
| `1014-400` | 錯誤請求非法參數 | 無法處理該請求。 {detailedMessage} |

## 框架錯誤

| 錯誤代碼 | 標題 | 詳細消息 |
| --- | --- | --- |
| `1100-400` | Bad Request | 無法處理該請求。 {detailedMessage} |
| `1101-500` | 內部錯誤 | 發生內部錯誤。 如果問題仍然存在，請重試並聯繫客戶支援。 |
| `1102-404` | 找不到資源 | 找不到請求的資源。 {detailedMessage} |
| `1103-503` | 服務不可用 | 服務暫時不可用。 如果問題仍然存在，請重試並聯繫客戶支援。 |
| `1104-504` | 網關超時 | 網關超時。 如果問題仍然存在，請重試並聯繫客戶支援。 |
| `1105-401` | 未授權 | 用戶未授權。 {detailedMessage} |
| `1106-403` | 禁止 | 禁止請求的操作。 {detailedMessage} |
| `1107-412` | 先決條件失敗 | 未滿足If-Unomodifed-Sine或If-None-Match標頭定義的條件。 {detailedMessage} |

## 加密錯誤

| 錯誤代碼 | 標題 | 詳細消息 |
| --- | --- | --- |
| `1200-500` | 內部錯誤 | 發生內部錯誤。 如果問題仍然存在，請重試並聯繫客戶支援。 |
| `1201-400` | Bad Request | flowId不能為null或為空。 請在請求中提供有效的flowId，然後重試。 |
| `1202-400` | Bad Request | 流的轉換={transformations}中缺少publicKeyId。 請在請求中提供publicKeyId，然後重試。 |
| `1203-400` | Bad Request | 在流的轉換={transformations}中，對於keyID={keyID}不存在加密密鑰。 請檢查您提供的keyID，然後重試。 |
| `1204-400` | Bad Request | 提供的加密算法無效。 請提供有效的加密算法，然後重試。 |
| `1205-400` | Bad Request | 在提供的請求的params部分中缺少密碼。 請在參數中提供passPhrase，然後重試。 |

## REST API錯誤

| 錯誤代碼 | 標題 | 詳細消息 |
| --- | --- | --- |
| `1300-400` | Bad Request | {connectorType}連接器不支援修補程式連接請求。 請檢查提供的請求，然後重試。 |
| `1301-400` | Bad Request | 提供的authSpecType參數：不支援{authSpecType}。 請提供有效的身份驗證規範類型，然後重試。 |
| `1302-400` | Bad Request | 連接器={connectorType}不支援提供的身份驗證類型= {authType}。 請為給定連接器提供有效的身份驗證類型。 |
| `1303-400` | Bad Request | 無法使用給定的身份驗證參數對URL進行編碼，因為{value}不支援URL編碼。 請檢查您的身份驗證參數，然後重試。 |
| `1304-400` | Bad Request | 未提供必填欄位{field}。 請提供{field}，然後重試。 |
| `1305-400` | Bad Request | 此操作不支援提供的連接器類型= {connectorType}。 |
| `1306-400` | Bad Request | 驗證目標連接規範ID時，目標連接不能為Null。 請檢查提供的請求，然後重試。 |
| `1307-400` | Bad Request | 目標連接規範ID無效={targetConnectionSpecId}。 允許的值為： `c604ff05-7f1a-43c0-8e18-33bf874cb11c`。 |
| `1308-400` | Bad Request | 無法處理該請求。 錯誤消息：{msftErrorMessage} |
| `1309-400` | Bad Request | 提供的加密轉換無效，因為參數中缺少{requiredParam}。 請提供{requiredParam}並重試。 |
| `1310-400` | Bad Request | 參數中提供的publicKeyId已過期。 請提供有效的publicKeyId，然後重試。 |
| `1311-400` | Bad Request | params中提供的publicKeyId無效。 請提供有效的publicKeyId，然後重試。 |
| 1312-400 | Bad Request | 提供的參數值{paramValue}不是屬性={requestParam}的有效輸入。 請提供有效的參數值，然後重試。 |
| `1313-400` | Bad Request | 路徑屬性{attribute}不存在。 請確保該屬性存在，然後重試。 |
| `1314-400` | Bad Request | 已提供複雜路徑，但不允許。 請確保未提供複雜路徑，然後重試。 |
| `1315-400` | Bad Request | 提供的路徑{path}應指向記錄陣列。 請確保提供的路徑指向記錄陣列，然後重試。 |
| `1316-400` | Bad Request | 提供的分頁參數不應為空。 請提供有效的分頁參數，然後重試。 |
| `1317-400` | Bad Request | 提供的計畫參數為空，但不應為空。 請提供有效的計畫參數，然後重試。 |
| `1318-400` | Bad Request | {combinedMessage}。 請檢查提供的請求，然後重試。 |
| `1319-400` | Bad Request | {param}應是父集合的一部分。 請在父集合中提供{param}，然後重試。 |
| `1320-400` | Bad Request | {idType}不能為null或為空。 請提供有效的{idType}，然後重試。 |
| `1321-400` | Bad Request | {idType}的長度應為1，提供的大小為{size}。 請提供有效大小並重試。 |
| `1322-400` | Bad Request | 源連接不能為空，無法生成架構引用。 請提供有效的源連接，然後重試。 |
| `1323-400` | Bad Request | 源連接中的{entity}不能為null或為空：{sourceConnection}。 請提供有效的{entity}，然後重試。 |
| `1324-400` | Bad Request | 提取資料集ID時，目標連接不能為null。 請提供有效的目標連接，然後重試。 |
| `1325-400` | Bad Request | 目標連接中的dataSetId參數不能為null或為空：{TargetConnection}。 請提供有效的dataSetId參數，然後重試。 |
| `1326-400` | Bad Request | 獲取源格式時，源連接不能為null。 請提供有效的源連接，然後重試。 |
| `1327-400` | Bad Request | 不支援SourceConnection中提供的源資料格式={sourceFormat}。 允許的值包括：{values}。 請提供允許的值，然後重試。 |
| `1328-400` | Bad Request | 提取{param}時，映射轉換不能為Null。 請提供有效的映射轉換，然後重試。 |
| `1329-400` | Bad Request | 參數：{param}在提供的請求中不能為null或為空。 請提供有效的{param}，然後重試。 |
| `1330-400` | Bad Request | 找不到表{tableName}的列。 請提供有效的表名，然後重試。 |
| `1331-400` | Bad Request | SourceConnection中的列分隔符不能多於一個字元：{sourceConnection}。 請提供有效的列分隔符，然後重試。 |
| `1332-400` | Bad Request | 具有connectionSpecId的源連接請求：{connectionSpecId}不能有baseConnectionId。 請刪除baseConnectionId，然後重試。 |
| `1333-400` | 錯誤請求 | 規範id={specId}的源不支援flowRunAction={flowRunAction}。 請提供有效的流運行操作，然後重試。 |
| `1334-400` | Bad Request | 查詢參數：{param}不能為空。 請提供有效的{param}，然後重試。 |
| `1335-400` | Bad Request | 序列化篩選參數以進行瀏覽時出錯。 請檢查篩選參數請求，然後重試。 |
| `1336-400` | Bad Request | 連接規範ID不支援瀏覽連接：{connectionSpecId}。 請提供支援的連接規範id，然後重試。 |
| `1337-400` | Bad Request | 對於objectType={objectType},{QueryParam}不能為空。 請提供有效的{QueryParam}，然後重試。 |
| `1338-400` | Bad Request | flowRequest中{connectionType}連接ID不能為null。 請在flowRequest中提供有效的{connectionType}連接ID。 |
| `1339-400` | Bad Request | 請求中提供的組織={imsOrg}的格式無效。 請提供有效的組織ID，然後重試。 |
| `1340-400` | Bad Request | 分析{time}時出錯。 請檢查請求中提供的時間格式，然後重試。 |
| `1341-400` | Bad Request | 提供的ODI Json為空。 請提供有效的ODI Json，然後重試。 |
| `1342-400` | Bad Request | 「odi.json」中的「dls:folder」段缺少定義。 請在「odi.json」中提供相應的定義，然後重試。 |
| `1343-400` | Bad Request | 「odi.json」中的「dls:entityReferences」和「dls:partitionSpec」段都缺少定義。 請在「odi.json」中提供相應的定義，然後重試。 |
| `1344-400` | Bad Request | 「odi.json」中「dls:partitionSpec」的定義無效，因為找到多個partitionSpec。 請在「odi.json」中提供相應的定義，然後重試。 |
| `1345-400` | Bad Request | 路徑中1個或多個段中缺少定義：「dls:partitionSpec/dls:fileFormat」、「dls:partitionSpec/dls:partitionTemplate」、「dls:partitionSpec/dls:fileFormat/@type」、「odi.json」中的「dls:partitionSpec/dls:fileFormat/dls:csvDelimiters」。 請在「odi.json」中提供相應的定義，然後重試。 |
| `1346-400` | Bad Request | 「odi.json」中「dls:fileFormat」中提供的「@type」定義無效。 請在「odi.json」中提供相應的定義，然後重試。 |
| `1347-400` | Bad Request | 不支援「odi.json」中的dls:csvDelimiters定義。 支援的csvDelimiters包括： [&#39;,&#39;]。 請在「odi.json」中提供相應的定義，然後重試。 |
| `1348-400` | Bad Request | 反序列化「dls:entityReferences」時出錯。 請檢查資料的格式是否有效，然後重試。 |
| `1349-400` | Bad Request | 提供的篩選器參數無效。 請提供有效的篩選器參數，然後重試。 |
| `1350-400` | Bad Request | 未為源處的篩選器提供運算子。 請為有效的篩選器請求提供相應的運算子，然後重試。 |
| `1351-400` | Bad Request | 此連接器的源篩選器不支援提供的運算子{operator}。 請提供有效的運算子，然後重試。 |
| `1352-400` | Bad Request | 無法將提供的運算子{operator}映射到{ql}的任何受支援的本機運算子。 請提供有效的運算子，然後重試。 |
| `1353-400` | Bad Request | {connectorType}連接器尚不支援源上的篩選器。 請檢查文檔中支援的連接器：https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/filter.html。 |
| `1354-400` | Bad Request | 源中的篩選器尚不支援查詢語言{ql}。 請提供有效的查詢語言，然後重試。 |
| `1355-400` | Bad Request | 提供的篩選器類型無效。 支援的篩選器類型為：PQL。 請提供有效的篩選器類型，然後重試。 |
| `1356-400` | Bad Request | 提供的篩選器格式無效。 支援的篩選器格式為：pql/json。 請提供有效的篩選器格式，然後重試。 |
| `1357-400` | Bad Request | 提供的篩選器無效。 值必須提供詳細的篩選器。 請提供有效的篩選器，然後重試。 |
| `1358-400` | Bad Request | 提供的參數「objectType」無效。 請提供有效的objectType並重試。 |
| `1359-400` | Bad Request | 請求中缺少參數{param}。 請提供有效的{param}，然後重試。 |
| `1360-400` | Bad Request | 不能在過去設定開始時間。 請提供有效的開始時間，然後重試。 |
| `1361-400` | Bad Request | 不允許使用一次性攝取。 請刪除間隔或更改頻率，然後重試。 |
| `1362-400` | Bad Request | 間隔不能小於{minInterval}。 請提供有效的間隔值，然後重試。 |
| `1363-400` | Bad Request | 不允許間隔{interval}，頻率：{frequency}。 請提供有效的間隔值，然後重試。 |
| `1364-400` | Bad Request | 頻率設定為1時不允許回填標誌。 請在頻率設定為一次後刪除回填標誌，然後重試。 |
| `1365-400` | Bad Request | ops中提供的路徑{path}無效。 請提供有效路徑{path}，然後重試。 |
| `1366-400` | Bad Request | 開始時間已過，不再允許更新操作。 |
| `1367-400` | Bad Request | 建立CRM連接器時，複製轉換中需要增量列。 請提供增量列，然後重試。 |
| `1368-400` | Bad Request | 流請求中不允許使用模式。 請檢查您的請求，然後重試。 |
| `1369-400` | Bad Request | 將頻率設定為一次時，不允許複製轉換中的增量列。 請刪除增量列，然後重試。 |
| `1370-400` | Bad Request | 由於缺少映射轉換，因此無法提取源列以進行接收。 請添加映射轉換並重試。 |
| `1371-400` | Bad Request | {connectorType}連接器不支援檔案屬性檢測。 請手動提供檔案屬性。 |
| `1372-400` | Bad Request | 不允許當前操作。 連接規範ID={connectionSpecId}不允許通過連接規範進行瀏覽。 |
| `1373-400` | Bad Request | 請求中缺少flowSpecType。 請提供有效的flowSpecType並重試。 |
| `1374-400` | Bad Request | 提供的查詢參數無效。 不能在同一請求中具有determineProperties標誌和用戶定義的屬性。 請更正您的請求，然後重試。 |
| `1375-400` | Bad Request | 檔案屬性檢測失敗。 請手動輸入屬性。 |
| `1376-400` | Bad Request | 連接規範id={connectionSpecId}不支援檔案屬性檢測。 請手動提供檔案屬性。 |
| `1377-400` | Bad Request | 提供的值參數為null，無法與運算子{operator}進行比較。 請提供有效值參數，然後重試。 |
| `1378-400` | Bad Request | 驗證源處的篩選器的輸入列{column}時出錯。 列名應為表中的有效列。 請提供有效的列名，然後重試。 |
| `1379-400` | Bad Request | 驗證源處的篩選器的輸入{value}時出錯。 源處的列DataType為{columnDataType}，值為DataType [字串] 不匹配。 請提供有效的{value}，然後重試。 |
| `1380-400` | Bad Request | 無法建立流運行。 錯誤消息：{message} |
| `1381-400` | Bad Request | WindowsEndTime={endTime}不能早於Windows StartTime={startTime}。 請提供有效的結束時間，然後重試。 |
| `1382-400` | Bad Request | 增量列應與流的「複製」轉換中存在的值匹配。 請提供有效的增量列，然後重試。 |
| `1383-400` | Bad Request | 為建立流運行而接收的參數中缺少增量列。 請在參數中提供增量列，然後重試。 |
| `1384-400` | Bad Request | 為建立流運行提供的params={params}無效或為空。 請提供有效的參數並重試。 |
| `1385-400` | Bad Request | 建立流運行時不支援提供的connectorType={connectorType}。 請提供有效的connectorType，然後重試。 |
| `1386-400` | Bad Request | 建立流運行時不支援scheduleParams frequency={frequency}的flowId={flowId}。 請提供有效頻率，然後重試。 |
| `1387-400` | Bad Request | flowRunId={flowRunId}處於無效狀態={state}，無法重新觸發。 請稍後重試，如果問題仍然存在，請與客戶支援聯繫。 |
| `1388-400` | Bad Request | 流={flow}處於狀態={state}，無法重新觸發。 流必須處於啟用狀態才能重新觸發。 |
| `1389-400` | Bad Request | 分析提供的base64編碼字串時出錯。 請提供有效的編碼篩選器字串，然後重試。 |
| `1390-400` | Bad Request | 「not」運算子不能有多個比較。 請提供有效的比較數，然後重試。 |
| `1391-400` | Bad Request | 無法在sourceConnection中分析ID={sourceConnectionId}的SchemaMetaData。 請檢查請求中的schemaMetaData，然後重試。 |
| `1392-400` | Bad Request | 無法分析flowId={flowId}的流請求中的轉換。 請檢查請求中的轉換，然後重試。 |
| `1393-400` | Bad Request | 提供的參數{parameter}為null或為空。 請提供有效的{parameter}，然後重試。 |
| `1394-400` | Bad Request | 參數{parameter}的最小值為1。 請提供有效的{parameter}，然後重試。 |
| `1395-400` | Bad Request | 在流中找到的源連接為Null或空。 請在流中提供有效的源連接，然後重試。 |
| `1396-400` | Bad Request | 找不到匹配格式。 請提供匹配的格式，然後重試。 |
| `1397-400` | Bad Request | 提供的頻率：{frequency}無效。 請提供有效頻率，然後重試。 |
| `1398-400` | Bad Request | 提供的操作：不支援{action}。 請檢查提供的操作，然後重試。 |
| `1399-400` | Bad Request | 找不到有效的requestFileType。 請提供有效的requestFileType，然後重試。 |
| `1400-400` | Bad Request | 提供的參數「templateType」無效。 請提供有效的模板類型，然後重試。 |
| `1401-400` | Bad Request | 不支援提供的流運行操作={flowRunAction}。 請提供有效的流運行操作，然後重試。 |
| `1402-500` | 內部錯誤 | 發生內部錯誤。 如果問題仍然存在，請重試並聯繫客戶支援。 |
| `1403-400` | Bad Request | 開始時間已過，您不能再將頻率更改為一次。 |
| `1404-400` | Bad Request | 開始時間已過，您無法再更新回填。 |

## 流式服務例外(1600-1699)

| 錯誤代碼 | 標題 | 詳細消息 |
| --- | --- | --- |
| `1600-400` | Bad Request | 無法處理該請求。 {detailedMessage} |
| `1601-500` | 內部錯誤 | 發生內部錯誤。 如果問題仍然存在，請重試並聯繫客戶支援。 |
| `1602-404` | 找不到資源 | 找不到請求的資源。 {detailedMessage} |
| `1603-503` | 服務不可用 | 服務暫時不可用。 請重試。如果問題仍然存在，請與客戶支援聯繫。 |
| `1604-504` | 網關超時 | 網關超時。 請重試。如果問題仍然存在，請與客戶支援聯繫。 |
| `1605-401` | 未授權 | 用戶未授權。 {detailedMessage} |
| `1606-403` | 禁止 | 禁止請求的操作。 {detailedMessage} |
| `1607-412` | 先決條件失敗 | 未滿足If-Unomodifed-Sine或If-None-Match標頭定義的條件。 {detailedMessage} |

## 資料登錄區錯誤

| 錯誤代碼 | 標題 | 詳細消息 |
| --- | --- | --- |
| `1700-500` | 內部錯誤 | 發生內部錯誤。 如果問題仍然存在，請重試並聯繫客戶支援。 |
| `1701-400` | Bad Request | 所提供的著陸區是非活動的。 請激活登錄區域，然後重試。 |
| `1702-400` | Bad Request | 不允許為登錄區域提供的SAS類型={sasType}。 請提供有效的SAS並重試。 |
| `1703-400` | Bad Request | 不允許刷新憑據。 |
| `1704-400` | Bad Request | subscriptionId={subscriptionId}和resourceGroupName={resourceGroupName}中為storageAccountName={accountName}返回的密鑰格式不正確。 請檢查您的請求，然後重試。 如果問題仍然存在，請與支援人員聯繫。 |
| `1705-400` | Bad Request | 不支援提供的資料登錄區域操作。 請提供有效操作，然後重試。 |
| `1706-400` | Bad Request | 未正確為登錄區域={landingZoneType}配置允許的激活配置。 如果問題仍然存在，請重試並聯繫客戶支援。 |
| `1707-400` | Bad Request | 服務無法啟動，因為登錄區域配置不能為null或為空。 請確保登錄區域配置不為空，然後重試。 |
| `1708-400` | Bad Request | 在landingZoneType={landingZoneType}中，容器配置不能為空。 請確保容器配置不為空，然後重試。 |
| `1709-400` | Bad Request | landingZoneType={landingZoneType}中的{tokenConfig}的SAS詳細資訊不能為空。 請在配置中提供有效的SAS，然後重試。 |
| `1710-400` | Bad Request | 提供的著陸區類型：不支援{landingZoneUseCase}。 請提供有效的登錄區域類型，然後重試。 |
| `1711-400` | Bad Request | 未找到所提供的資料登錄區域類型的SAS詳細資訊：{landingZoneUseCase}。 請檢查是否為提供的登錄區域類型提供了SAS詳細資訊。 |
| `1712-400` | Bad Request | 所提供的著陸區動作：不允許{actionType}。 請提供有效的資料登錄區域操作，然後重試。 |
| `1713-400` | Bad Request | 提供的{tokenType}不允許{OperationType}。 請檢查您的請求，然後重試。 |
| `1714-400` | Bad Request | 不允許ClientId={clientId}執行此操作。 請使用權限檢查您的請求，然後重試。 |
