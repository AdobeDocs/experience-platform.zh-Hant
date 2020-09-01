---
keywords: Experience Platform;home;popular topics;streaming
solution: Experience Platform
title: 串流擷取疑難排解
topic: troubleshooting
translation-type: tm+mt
source-git-commit: 1bb896f7629d7b71b94dd107eeda87701df99208
workflow-type: tm+mt
source-wordcount: '997'
ht-degree: 0%

---


# 串流擷取疑難排解指南

本檔案針對Adobe Experience Platform上串流擷取的常見問題提供解答。 如需其他服務的相關問題和疑難排 [!DNL Platform] 解，包括所有API中遇到的 [!DNL Platform] 問題，請參閱 [Experience Platform疑難排解指南](../../landing/troubleshooting.md)。

Adobe Experience Platform提 [!DNL Data Ingestion] 供REST風格的API，您可用來將資料收錄到 [!DNL Experience Platform]中。 所擷取的資料可用來即時更新個別客戶個人檔案，讓您跨多個通道提供個人化、相關的體驗。 請閱讀資料 [擷取概觀](../home.md) ，以取得有關服務和不同擷取方法的詳細資訊。 如需如何使用串流擷取API的步驟，請閱讀串流 [擷取概觀](../streaming-ingestion/overview.md)。

## 常見問題集

以下是串流擷取常見問題的解答清單。

### 我要如何得知我傳送的裝載已正確格式化？

[!DNL Data Ingestion] 利用 [!DNL Experience Data Model] (XDM)模式來驗證傳入資料的格式。 發送不符合預定義XDM模式結構的資料將導致接收失敗。 有關XDM及其在中使用的詳細信 [!DNL Experience Platform]息，請參閱 [XDM系統概述](../../xdm/home.md)。

串流擷取支援兩種驗證模式：同步與非同步。 每個驗證方法處理失敗資料的方式都不同。

**在您的開發流程中** ，應使用同步驗證。 失敗驗證的記錄會被丟棄，並傳回錯誤訊息，說明其失敗的原因(例如：&quot;無效的XDM消息格式&quot;)。

**在生產中** ，應使用非同步驗證。 任何未通過驗證的格式錯誤的資料都會作為失敗的 [!DNL Data Lake] 批處理檔案發送到該檔案，以便稍後檢索該檔案以進一步分析。

如需同步和非同步驗證的詳細資訊，請參閱串 [流驗證概觀](../quality/streaming-validation.md)。 有關如何查看失敗驗證的批的步驟，請參閱有關檢索失敗 [批的指南](../quality/retrieve-failed-batches.md)。

### 我是否可先驗證請求裝載，再將它傳送至 [!DNL Platform]?

請求負載只能在傳送至之後評估 [!DNL Platform]。 執行同步驗證時，有效負載會傳回已填入的JSON物件，而無效負載則會傳回錯誤訊息。 在非同步驗證期間，服務會偵測並傳送任何格式錯誤的資 [!DNL Data Lake] 料至稍後可擷取的資料以供分析。 如需詳細 [資訊，請參閱串流驗證](../quality/streaming-validation.md) 概觀。

### 當在不支援同步驗證的邊緣上要求同步驗證時，會發生什麼情況？

當請求的位置不支援同步驗證時，會傳回501錯誤回應。 如需同步驗證 [的詳細資訊](../quality/streaming-validation.md) ，請參閱串流驗證總覽。

### 如何確保僅從受信任的來源收集資料？

[!DNL Experience Platform] 支援安全的資料收集。 啟用驗證資料收集後，用戶端必須傳送JSON Web Token(JWT)及其IMS組織ID作為請求標題。 如需如何傳送已驗證資料給的詳細資訊， [!DNL Platform]請參閱已驗證資料收 [集指南](../tutorials/create-authenticated-streaming-connection.md)。

### 串流資料的延遲為何 [!DNL Real-time Customer Profile]?

串流事件一般在60秒 [!DNL Real-time Customer Profile] 內就能反映。 實際延遲可能因資料量、消息大小和頻寬限制而有所不同。

### 我是否可在相同的API要求中包含多個訊息？

您可以在單一請求裝載內將多個訊息分組，並將其串流至 [!DNL Platform]。 正確使用時，在單一要求中分組多個訊息是最佳化資料作業的絕佳方式。 請閱讀教學課程，瞭解 [如何在請求中傳送多則訊息](../tutorials/streaming-multiple-messages.md) ，以取得詳細資訊。

### 我要如何得知我傳送的資料是否收到？

所有傳送至(成功或以其他方 [!DNL Platform] 式)的資料都會先儲存為批次檔案，再保存在資料集中。 批次的處理狀態會顯示在傳送至的資料集中。

您可以使用 [Experience Platform使用者介面檢查資料集活動，以確認資料是否已成功](https://platform.adobe.com)擷取。 按一 **[!UICONTROL 下左側導覽]** 中的「資料集」，以顯示資料集清單。 從顯示的清單中選擇要流式處理的資料集，以開啟其「 **[!UICONTROL Dataset]** 」活動頁，顯示在選定時段內發送的所有批。 如需使用監控資料 [!DNL Experience Platform] 串流的詳細資訊，請參閱監 [控串流資料流指南](../quality/monitor-data-flows.md)。

如果您的資料未能收錄，而您希望從中恢復 [!DNL Platform]，則可以通過將失敗的批次的ID發送到 [!DNL Data Access API]。 有關詳細資訊，請 [參閱檢索失敗批](../quality/retrieve-failed-batches.md) 的指南。

### 為什麼我的串流資料無法在Data Lake中使用？

批次擷取可能無法到達的原因有多種， [!DNL Data Lake]例如格式無效、遺失資料或系統錯誤。 要確定批失敗的原因，您必須使用檢索批並查看其 [!DNL Data Ingestion Service API] 詳細資訊。 有關檢索失敗批的詳細步驟，請參見有關檢索失敗 [批的指南](../quality/retrieve-failed-batches.md)。

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

### 為什麼我的已傳送訊息未收到 [!DNL Real-time Customer Profile]?

如果 [!DNL Real-time Customer Profile] 拒絕訊息，很可能是因為身分資訊不正確。 這可能是為身份提供無效值或命名空間的結果。

身份名稱空間有兩種類型：預設值和自訂值。 使用自訂名稱空間時，請確定名稱空間已在中註冊 [!DNL Identity Service]。 如需使用預 [設和自訂名稱空間的詳細資訊](../../identity-service/namespaces.md) ，請參閱身分名稱空間概觀。

您可以使用 [[!DNL Experience Platform UI]](https://platform.adobe.com) ，查看訊息擷取失敗原因的詳細資訊。 按一 **[!UICONTROL 下左側導覽中的]** 「監控」，然後檢視「串流端對端 **** 」標籤，以查看在選取時段內串流的訊息批次。
