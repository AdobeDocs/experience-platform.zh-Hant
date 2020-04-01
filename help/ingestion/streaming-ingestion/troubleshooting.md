---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 串流擷取疑難排解
topic: troubleshooting
translation-type: tm+mt
source-git-commit: 4817162fe2b7cbf4ae4c1ed325db2af31da5b5d3

---


# 串流擷取疑難排解指南

本檔案針對Adobe Experience Platform上串流擷取的常見問題提供解答。 如需其他平台服務的相關問題和疑難排解，包括所有平台API所遇到的問題，請參閱「 [Experience Platform疑難排解指南」](../../landing/troubleshooting.md)。

Adobe Experience Platform Data Ingestion提供REST風格的API，您可用來將資料收錄至Experience Platform。 所擷取的資料可用來即時更新個別客戶個人檔案，讓您跨多個通道提供個人化、相關的體驗。 請閱讀資料 [擷取概觀](../home.md) ，以取得有關服務和不同擷取方法的詳細資訊。 如需如何使用串流擷取API的步驟，請閱讀串流 [擷取概觀](../streaming-ingestion/overview.md)。

## 常見問題集

以下是串流擷取常見問題的解答清單。

### 我要如何得知我傳送的裝載已正確格式化？

資料擷取運用體驗資料模型(XDM)架構來驗證傳入資料的格式。 發送不符合預定義XDM模式結構的資料將導致接收失敗。 如需XDM及其在Experience Platform中使用的詳細資訊，請參閱 [XDM系統概觀](../../xdm/home.md)。

串流擷取支援兩種驗證模式：同步與非同步。 每個驗證方法處理失敗資料的方式都不同。

**在您的開發流程中** ，應使用同步驗證。 失敗驗證的記錄會被丟棄，並傳回錯誤訊息，說明其失敗的原因(例如：&quot;無效的XDM消息格式&quot;)。

**在生產中** ，應使用非同步驗證。 任何未通過驗證的格式錯誤資料都會以失敗的批次檔案傳送至資料湖，稍後可在此擷取以進一步分析。

如需同步和非同步驗證的詳細資訊，請參閱串 [流驗證概觀](../quality/streaming-validation.md)。 有關如何查看失敗驗證的批的步驟，請參閱有關檢索失敗 [批的指南](../quality/retrieve-failed-batches.md)。

### 我是否可先驗證請求裝載，再將它傳送至平台？

請求負載只能在傳送至平台後評估。 執行同步驗證時，有效負載會傳回已填入的JSON物件，而無效負載則會傳回錯誤訊息。 在非同步驗證期間，服務會偵測並傳送任何格式錯誤的資料至資料湖，以供日後擷取以進行分析。 如需詳細 [資訊，請參閱串流驗證](../quality/streaming-validation.md) 概觀。

### 當在不支援同步驗證的邊緣上要求同步驗證時，會發生什麼情況？

當請求的位置不支援同步驗證時，會傳回501錯誤回應。 如需同步驗證 [的詳細資訊](../quality/streaming-validation.md) ，請參閱串流驗證總覽。

### 如何驗證傳送的資料？

Experience Platform支援安全的資料收集。 啟用驗證資料收集後，用戶端必須傳送JSON Web Token(JWT)及其IMS組織ID作為請求標題。 如需如何傳送驗證資料至平台的詳細資訊，請參閱驗證資料收 [集指南](../tutorials/create-authenticated-streaming-connection.md)。

### 將資料串流至即時客戶個人檔案的延遲為何？

串流事件通常在60秒內反映在即時客戶個人檔案中。 實際延遲可能因資料量、消息大小和頻寬限制而有所不同。

### 我是否可在相同的API要求中包含多個訊息？

您可以在單一請求裝載內將多個訊息分組，並將其串流至平台。 正確使用時，在單一要求中分組多個訊息是最佳化資料作業的絕佳方式。 請閱讀教學課程，瞭解 [如何在請求中傳送多則訊息](../tutorials/streaming-multiple-messages.md) ，以取得詳細資訊。

### 我要如何得知我傳送的資料是否收到？

所有傳送至平台的資料（無論是否成功）都會先儲存為批次檔案，再保存在資料集中。 批次的處理狀態會顯示在傳送至的資料集中。

您可以使用 [Experience Platform使用者介面檢查資料集活動，以確認資料是否已成功](https://platform.adobe.com)擷取。 按一 **下左側導覽** 中的「資料集」，以顯示資料集清單。 從顯示的清單中選擇要流式處理的資料集，以開啟其「 *Dataset* 」活動頁，顯示在選定時段內發送的所有批。 如需使用Experience Platform監控資料串流的詳細資訊，請參閱監控串流資 [料流的指南](../quality/monitor-data-flows.md)。

如果您的資料未能收錄，而您想要從平台中復原，則可以透過將失敗的批次ID傳送至資料存取API來 [擷取這些批次][Data Access Service API]。 有關詳細資訊，請 [參閱檢索失敗批](../quality/retrieve-failed-batches.md) 的指南。

### 為什麼我的串流資料無法在Data Lake中使用？

批次擷取可能無法到達資料湖的原因有多種，例如無效的格式、遺失資料或系統錯誤。 要確定批處理失敗的原因，必須使用Data Ingestion Service API檢索批 [處理][Data Ingestion Service] ，並查看其詳細資訊。 有關檢索失敗批的詳細步驟，請參見有關檢索失敗 [批的指南](../quality/retrieve-failed-batches.md)。

### 如何剖析API要求傳回的回應？

您可以先檢查伺服器回應程式碼，以判斷您的要求是否被接受，從而解析回應。 如果返回成功的響應代碼，則可以查看 `responses` 陣列對象以確定接收任務的狀態。

成功的單一訊息API要求會傳回狀態碼200。 成功（或部分成功）批次訊息API請求會傳回狀態代碼207。

下列JSON是含有兩則訊息之API要求的範例回應物件：一個成功，一個失敗。 成功串流的訊息會傳回 `xactionId` 屬性。 無法串流的訊息會傳回屬 `statusCode` 性和回應，並 `message` 包含更多資訊。

```JSON
{
    "inletId": "9b0cb233972f3b0092992284c7353f5eead496218e8441a79b25e9421ea127f5",
    "batchId": "1565638336649:1750:244",
    "receivedTimeMs": 1565638336705,
    "responses": [
        {
            "xactionId": "1565650704337:2124:92:3"
        },
        {
            "statusCode": 400,
            "message": "inletId: [9b0cb233972f3b0092992284c7353f5eead496218e8441a
                79b25e9421ea127f5] 
                imsOrgId: [{IMS_ORG}] 
                Message has unknown xdm format"
        }
    ]
}
```

### 為什麼即時客戶個人檔案未收到我的傳送訊息？

如果即時客戶個人檔案拒絕訊息，很可能是因為身分資訊不正確。 這可能是為身份提供無效值或命名空間的結果。

身份名稱空間有兩種類型：預設值和自訂值。 使用自訂名稱空間時，請確定名稱空間已在Identity Service中註冊。 如需使用預 [設和自訂名稱空間的詳細資訊](../../identity-service/namespaces.md) ，請參閱身分名稱空間概觀。

您可以使用 [Experience Platform UI](https://platform.adobe.com) ，查看訊息擷取失敗原因的詳細資訊。 按一 **下左側導覽中的** 「監控」，然後檢視「串流端對端 __ 」標籤，以查看在選取時段內串流的訊息批次。