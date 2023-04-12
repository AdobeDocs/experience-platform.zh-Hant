---
keywords: Experience Platform；首頁；熱門主題；串流；串流獲取；疑難排解；串流獲取疑難排解；串流獲取常見問題集；faq;
solution: Experience Platform
title: 串流擷取疑難排解指南
description: 本檔案提供Adobe Experience Platform上串流獲取的常見問題解答。
exl-id: 5d5deccf-25b8-44c9-ae27-9a4713ced274
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '1024'
ht-degree: 0%

---

# 串流內嵌疑難排解指南

本檔案提供Adobe Experience Platform上串流獲取的常見問題解答。 以了解與其他 [!DNL Platform] 服務，包括所有 [!DNL Platform] API請參閱 [Experience Platform疑難排解指南](../../landing/troubleshooting.md).

Adobe Experience Platform [!DNL Data Ingestion] 提供RESTful API，供您用來將資料內嵌至 [!DNL Experience Platform]. 擷取的資料可用來近乎即時更新個別客戶設定檔，讓您能夠跨多個管道提供個人化的相關體驗。 請閱讀 [資料擷取概觀](../home.md) 以取得服務和不同擷取方法的詳細資訊。 如需如何使用串流獲取API的步驟，請參閱 [串流獲取概觀](../streaming-ingestion/overview.md).

## 常見問題集

以下為串流獲取常見問題的解答清單。

### 如何知道我傳送的裝載格式正確？

[!DNL Data Ingestion] 利用 [!DNL Experience Data Model] (XDM)結構，以驗證傳入資料的格式。 傳送不符合預先定義XDM架構結構的資料會導致擷取失敗。 如需XDM及其在 [!DNL Experience Platform]，請參閱 [XDM系統概觀](../../xdm/home.md).

串流內嵌支援兩種驗證模式：同步與非同步。 每個驗證方法處理失敗資料的方式都不同。

**同步驗證** 應在開發程式中使用。 會捨棄驗證失敗的記錄，並傳回錯誤訊息，說明失敗的原因(例如：「XDM訊息格式無效」)。

**非同步驗證** 應用於生產。 任何未通過驗證的格式錯誤的資料都會傳送至 [!DNL Data Lake] 作為失敗的批處理檔案，稍後可在其中檢索該檔案以進行進一步分析。

如需同步與非同步驗證的詳細資訊，請參閱 [串流驗證概觀](../quality/streaming-validation.md). 有關如何查看未通過驗證的批的步驟，請參閱 [檢索失敗的批](../quality/retrieve-failed-batches.md).

### 我可以在將請求裝載傳送至 [!DNL Platform]?

要求裝載只有在傳送至 [!DNL Platform]. 執行同步驗證時，有效負載會傳回填入的JSON物件，而無效負載會傳回錯誤訊息。 在非同步驗證期間，服務會偵測並傳送任何格式錯誤的資料至 [!DNL Data Lake] 供稍後擷取以進行分析之用。 請參閱 [串流驗證概觀](../quality/streaming-validation.md) 以取得更多資訊。

### 如果在不支援同步驗證的邊緣上請求同步驗證，會發生什麼情況？

當請求的位置不支援同步驗證時，會傳回501錯誤回應。 請參閱 [串流驗證概觀](../quality/streaming-validation.md) 有關同步驗證的詳細資訊。

### 如何確保僅從受信任的來源收集資料？

[!DNL Experience Platform] 支援安全資料收集。 啟用已驗證的資料收集時，用戶端必須傳送JSON網頁代號(JWT)及其組織ID作為要求標題。 如需如何將已驗證資料傳送至的詳細資訊 [!DNL Platform]，請參閱 [驗證的資料收集](../tutorials/create-authenticated-streaming-connection.md).

### 將資料串流至的延遲為何 [!DNL Real-Time Customer Profile]?

流式事件通常反映在 [!DNL Real-Time Customer Profile] 在60秒內。 實際延遲可能會因資料量、消息大小和頻寬限制而改變。

### 我可以在相同API請求中包含多則訊息嗎？

您可以在單一請求裝載中將多個訊息分組，並將其串流至 [!DNL Platform]. 正確使用時，在單一請求中分組多個訊息是最佳化資料作業的絕佳方式。 請閱讀以下教學課程： [在請求中傳送多則訊息](../tutorials/streaming-multiple-messages.md) 以取得更多資訊。

### 如何知道我傳送的資料是否收到？

所有傳送至的資料 [!DNL Platform] （成功或以其他方式）會先儲存為批次檔案，再保存在資料集中。 批次處理狀態會顯示在傳送給的資料集中。

您可以使用檢查資料集活動，以確認資料是否已成功內嵌 [Experience Platform使用者介面](https://platform.adobe.com). 按一下 **[!UICONTROL 資料集]** 在左側導覽中，顯示資料集清單。 從顯示的清單中選取要串流至的資料集，以開啟其 **[!UICONTROL 資料集活動]** 頁，顯示選定時段內發送的所有批。 如需使用的詳細資訊 [!DNL Experience Platform] 若要監控資料流，請參閱 [監控串流資料流](../quality/monitor-data-ingestion.md).

如果您的資料未能內嵌，而您想要從中復原 [!DNL Platform]，您可以將失敗的批次ID傳送至 [!DNL Data Access API]. 請參閱 [檢索失敗的批](../quality/retrieve-failed-batches.md) 以取得更多資訊。

### 為何資料湖無法使用我的串流資料？

批次內嵌可能無法達到以下目的的原因有許多 [!DNL Data Lake]，例如無效的格式、遺失資料或系統錯誤。 要確定批處理失敗的原因，必須使用 [!DNL Data Ingestion Service API] 並查看其詳細資訊。 有關檢索失敗批處理的詳細步驟，請參閱 [檢索失敗的批](../quality/retrieve-failed-batches.md).

### 如何剖析API要求傳回的回應？

您可以先檢查伺服器回應代碼，以判斷是否接受您的要求，借此剖析回應。 如果傳回成功的回應代碼，您就可以檢閱 `responses` 陣列物件，以判斷擷取任務的狀態。

成功的單一訊息API要求會傳回狀態代碼200。 成功（或部分成功）的批次訊息API請求會傳回狀態代碼207。

下列JSON是含有兩則訊息之API要求的範例回應物件：一個成功，一個失敗。 成功串流的訊息會傳回 `xactionId` 屬性。 無法串流傳回的訊息 `statusCode` 屬性和回應 `message` 以取得更多資訊。

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
                imsOrgId: [{ORG_ID}] 
                Message has unknown xdm format"
        }
    ]
}
```

### 為什麼我的已發送郵件未被接收 [!DNL Real-Time Customer Profile]?

若 [!DNL Real-Time Customer Profile] 拒絕訊息，很可能是因為身分資訊不正確。 這可能是為身分提供無效值或命名空間的結果。

身分識別命名空間有兩種類型：預設和自訂。 使用自訂命名空間時，請確定命名空間已在中註冊 [!DNL Identity Service]. 請參閱 [身分命名空間概述](../../identity-service/namespaces.md) 如需使用預設和自訂命名空間的詳細資訊。

您可以使用 [[!DNL Experience Platform UI]](https://platform.adobe.com) ，了解訊息擷取失敗的原因的詳細資訊。 按一下 **[!UICONTROL 監控]** 在左側導覽中，然後檢視 **[!UICONTROL 端對端串流]** 頁簽，查看選定時段內流化的消息批。
