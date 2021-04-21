---
keywords: Experience Platform；首頁；熱門主題；串流；串流擷取；疑難排解；串流擷取疑難排解；串流擷取常見問答；常見問答；
solution: Experience Platform
title: 串流擷取疑難排解指南
topic-legacy: troubleshooting
description: 本檔案針對有關Adobe Experience Platform串流擷取的常問問題提供解答。
exl-id: 5d5deccf-25b8-44c9-ae27-9a4713ced274
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1019'
ht-degree: 0%

---

# 串流擷取疑難排解指南

本檔案針對有關Adobe Experience Platform串流擷取的常問問題提供解答。 有關其他[!DNL Platform]服務的問題和疑難排解，包括所有[!DNL Platform] API中遇到的問題，請參閱[Experience Platform故障排解指南](../../landing/troubleshooting.md)。

Adobe Experience Platform[!DNL Data Ingestion]提供REST風格的API，您可用來將資料內嵌至[!DNL Experience Platform]。 所擷取的資料可用來即時更新個別客戶個人檔案，讓您跨多個通道提供個人化、相關的體驗。 請閱讀[資料擷取概觀](../home.md)，以取得有關服務和不同擷取方法的詳細資訊。 有關如何使用串流擷取API的步驟，請閱讀[串流擷取概觀](../streaming-ingestion/overview.md)。

## 常見問題集

以下是串流擷取常見問題的解答清單。

### 我要如何得知我傳送的裝載已正確格式化？

[!DNL Data Ingestion] 利 [!DNL Experience Data Model] 用(XDM)模式來驗證傳入資料的格式。發送不符合預定義XDM模式結構的資料將導致接收失敗。 有關XDM及其在[!DNL Experience Platform]中的使用的詳細資訊，請參閱[ XDM系統概述](../../xdm/home.md)。

串流擷取支援兩種驗證模式：同步與非同步。 每個驗證方法處理失敗資料的方式都不同。

**在開** 發程式期間，應使用同步驗證。失敗驗證的記錄會被丟棄，並傳回錯誤訊息，說明其失敗的原因(例如：&quot;無效的XDM消息格式&quot;)。

**生產** 中應使用非同步驗證。任何未通過驗證的格式錯誤的資料都作為失敗的批處理檔案發送到[!DNL Data Lake]，以便稍後在此處檢索以進行進一步分析。

如需同步與非同步驗證的詳細資訊，請參閱[串流驗證概觀](../quality/streaming-validation.md)。 有關如何查看驗證失敗批次的步驟，請參閱[檢索失敗批次](../quality/retrieve-failed-batches.md)上的指南。

### 我是否可先驗證請求裝載，再將其傳送至[!DNL Platform]?

請求負載只能在發送到[!DNL Platform]後評估。 執行同步驗證時，有效負載會傳回已填入的JSON物件，而無效負載則會傳回錯誤訊息。 在非同步驗證期間，服務會偵測並傳送任何格式錯誤的資料至[!DNL Data Lake]，以便稍後擷取該資料以進行分析。 如需詳細資訊，請參閱[串流驗證概觀](../quality/streaming-validation.md)。

### 當在不支援同步驗證的邊緣上要求同步驗證時，會發生什麼情況？

當請求的位置不支援同步驗證時，會傳回501錯誤回應。 如需同步驗證的詳細資訊，請參閱[串流驗證概觀](../quality/streaming-validation.md)。

### 如何確保僅從受信任來源收集資料？

[!DNL Experience Platform] 支援安全的資料收集。啟用驗證資料收集後，用戶端必須傳送JSON Web Token(JWT)及其IMS組織ID作為請求標題。 有關如何將已驗證資料發送到[!DNL Platform]的詳細資訊，請參閱[已驗證資料收集](../tutorials/create-authenticated-streaming-connection.md)上的指南。

### 串流資料至[!DNL Real-time Customer Profile]的延遲為何？

串流事件通常在60秒內反映在[!DNL Real-time Customer Profile]中。 實際延遲可能因資料量、消息大小和頻寬限制而有所不同。

### 我是否可在相同的API要求中包含多個訊息？

您可以在單一請求裝載內將多個訊息分組，並將其串流至[!DNL Platform]。 正確使用時，在單一要求中分組多個訊息是最佳化資料作業的絕佳方式。 請閱讀有關[在請求中發送多條消息的教程](../tutorials/streaming-multiple-messages.md)，以瞭解更多資訊。

### 我要如何得知我傳送的資料是否收到？

所有傳送至[!DNL Platform]（成功或否）的資料都會儲存為批次檔案，然後再保存在資料集中。 批次的處理狀態會顯示在傳送至的資料集中。

您可以使用[Experience Platform使用者介面](https://platform.adobe.com)檢查資料集活動，以確認資料是否已成功擷取。 按一下左側導覽中的&#x200B;**[!UICONTROL Datasets]**&#x200B;以顯示資料集清單。 從顯示的清單中選擇要流式處理的資料集以開啟其&#x200B;**[!UICONTROL Dataset activity]**&#x200B;頁，顯示選定時段內發送的所有批。 有關使用[!DNL Experience Platform]監控資料流的詳細資訊，請參閱[監控流資料流](../quality/monitor-data-ingestion.md)的指南。

如果您的資料未能收錄，而您想從[!DNL Platform]中恢復，則可以通過將失敗的批次的ID發送到[!DNL Data Access API]來檢索失敗的批次。 有關詳細資訊，請參閱[檢索失敗批](../quality/retrieve-failed-batches.md)指南。

### 為什麼我的串流資料無法在Data Lake中使用？

批次擷取可能無法到達[!DNL Data Lake]的原因有很多，例如無效的格式、遺失資料或系統錯誤。 要確定批失敗的原因，您必須使用[!DNL Data Ingestion Service API]檢索批並查看其詳細資訊。 有關檢索失敗批的詳細步驟，請參見[檢索失敗批](../quality/retrieve-failed-batches.md)的指南。

### 如何剖析API要求傳回的回應？

您可以先檢查伺服器回應程式碼，以判斷您的要求是否被接受，從而解析回應。 如果返回成功的響應代碼，則可以查看`responses`陣列對象以確定接收任務的狀態。

成功的單一訊息API要求會傳回狀態碼200。 成功（或部分成功）批次訊息API請求會傳回狀態代碼207。

下列JSON是含有兩則訊息之API要求的範例回應物件：一個成功，一個失敗。 成功串流的訊息會傳回`xactionId`屬性。 無法串流的訊息會傳回`statusCode`屬性和回應`message`，並包含更多資訊。

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

### 為什麼[!DNL Real-time Customer Profile]未收到我的已發送消息？

如果[!DNL Real-time Customer Profile]拒絕訊息，則很可能是由於身分資訊不正確所致。 這可能是為身份提供無效值或命名空間的結果。

身份名稱空間有兩種類型：預設值和自訂值。 使用自訂名稱空間時，請確定名稱空間已在[!DNL Identity Service]中註冊。 如需使用預設和自訂名稱空間的詳細資訊，請參閱[identity namespace綜覽](../../identity-service/namespaces.md)。

您可以使用[[!DNL Experience Platform UI]](https://platform.adobe.com)來查看郵件擷取失敗原因的詳細資訊。 在左側導覽中按一下&#x200B;**[!UICONTROL Monitoring]**，然後檢視&#x200B;**[!UICONTROL Streaming end-to-end]**&#x200B;標籤，以檢視在選取時段內串流的訊息批次。
