---
keywords: Experience Platform；首頁；熱門主題；串流；串流擷取；疑難排解；串流擷取疑難排解；串流擷取常見問題集；faq；
solution: Experience Platform
title: 串流擷取疑難排解指南
description: 本檔案提供在Adobe Experience Platform上串流擷取相關常見問題的解答。
exl-id: 5d5deccf-25b8-44c9-ae27-9a4713ced274
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1026'
ht-degree: 0%

---

# 串流擷取疑難排解指南

本檔案提供在Adobe Experience Platform上串流擷取相關常見問題的解答。 有關其他[!DNL Platform]服務（包括所有[!DNL Platform] API中遇到的服務）的問題和疑難排解，請參閱[Experience Platform疑難排解指南](../../landing/troubleshooting.md)。

Adobe Experience Platform [!DNL Data Ingestion]提供您可用來將資料擷取到[!DNL Experience Platform]的RESTful API。 內嵌的資料會用於近乎即時更新個別客戶設定檔，讓您跨多個管道提供個人化的相關體驗。 請閱讀[資料擷取概觀](../home.md)，以取得有關服務和不同擷取方法的詳細資訊。 如需如何使用串流擷取API的步驟，請閱讀[串流擷取總覽](../streaming-ingestion/overview.md)。

## 常見問題集

以下是有關串流擷取的常見問題解答清單。

### 我如何知道我正在傳送的裝載格式正確？

[!DNL Data Ingestion]利用[!DNL Experience Data Model] (XDM)結構描述來驗證傳入資料的格式。 傳送不符合預先定義XDM結構描述的資料將會導致擷取失敗。 如需XDM及其在[!DNL Experience Platform]中的使用的詳細資訊，請參閱[XDM系統總覽](../../xdm/home.md)。

串流擷取支援兩種驗證模式：同步和非同步。 每個驗證方法處理失敗資料的方式都不同。

**在您的開發過程中應該使用同步驗證**。 未通過驗證的記錄會被捨棄，並傳回失敗原因的錯誤訊息（例如：「無效的XDM訊息格式」）。

**非同步驗證**&#x200B;應該用於生產環境。 任何未通過驗證的格式錯誤資料都會當作失敗的批次檔案傳送到[!DNL Data Lake]，以便稍後擷取進一步分析。

如需同步和非同步驗證的詳細資訊，請參閱[串流驗證概觀](../quality/streaming-validation.md)。 如需如何檢視驗證失敗的批次的步驟，請參閱[擷取失敗的批次](../quality/retrieve-failed-batches.md)的指南。

### 我可以先驗證要求裝載再傳送至[!DNL Platform]嗎？

要求裝載只有在傳送至[!DNL Platform]後，才能進行評估。 執行同步驗證時，有效裝載會傳回填入的JSON物件，而無效裝載會傳回錯誤訊息。 在非同步驗證期間，服務會偵測任何格式錯誤的資料，並將其傳送至[!DNL Data Lake]，以便稍後擷取該資料進行分析。 如需詳細資訊，請參閱[串流驗證概觀](../quality/streaming-validation.md)。

### 在不支援同步驗證的邊緣上請求同步驗證時，會發生什麼情況？

當要求的位置不支援同步驗證時，會傳回501錯誤回應。 如需同步驗證的詳細資訊，請參閱[串流驗證概觀](../quality/streaming-validation.md)。

### 如何確保僅從受信任的來源收集資料？

[!DNL Experience Platform]支援安全資料收集。 啟用已驗證的資料收集時，使用者端必須傳送JSON Web權杖(JWT)及其組織ID作為要求標題。 如需有關如何將已驗證的資料傳送至[!DNL Platform]的詳細資訊，請參閱[已驗證的資料彙集](../tutorials/create-authenticated-streaming-connection.md)的指南。

### 將資料串流至[!DNL Real-Time Customer Profile]的延遲為何？

串流事件通常會在60秒內反映在[!DNL Real-Time Customer Profile]中。 實際延遲可能會因資料量、訊息大小和頻寬限制而異。

### 我可以在同一API請求中包含多則訊息嗎？

您可以在單一要求裝載中將多個訊息分組，並將它們串流至[!DNL Platform]。 若正確使用，在單一請求中將多個訊息分組，是最佳化資料作業的絕佳方式。 如需詳細資訊，請閱讀有關[在要求中傳送多封郵件](../tutorials/streaming-multiple-messages.md)的教學課程。

### 如何知道是否收到我傳送的資料？

傳送到[!DNL Platform]的所有資料（無論成功與否）都會先儲存為批次檔案，再保留在資料集中。 批次的處理狀態會顯示在它們被傳送到的資料集中。

您可以使用[Experience Platform使用者介面](https://platform.adobe.com)檢查資料集活動，以確認是否已成功擷取資料。 按一下左側導覽中的&#x200B;**[!UICONTROL 資料集]**&#x200B;以顯示資料集清單。 從顯示的清單中選取您要串流至的資料集，以開啟其&#x200B;**[!UICONTROL 資料集活動]**&#x200B;頁面，其中顯示所選時段內傳送的所有批次。 如需有關使用[!DNL Experience Platform]監視資料串流的詳細資訊，請參閱[監視串流資料流](../quality/monitor-data-ingestion.md)的指南。

如果您的資料擷取失敗，而您想要從[!DNL Platform]復原該資料，您可以將失敗批次的ID傳送至[!DNL Data Access API]以擷取它們。 如需詳細資訊，請參閱[擷取失敗的批次](../quality/retrieve-failed-batches.md)的指南。

### 為什麼我的串流資料無法在資料湖中使用？

批次擷取可能無法達到[!DNL Data Lake]的原因有很多，例如格式無效、資料遺失或系統錯誤。 若要判斷批次失敗的原因，您必須使用[!DNL Data Ingestion Service API]擷取批次並檢視其詳細資料。 如需擷取失敗批次的詳細步驟，請參閱[擷取失敗批次](../quality/retrieve-failed-batches.md)的指南。

### 如何剖析針對API請求傳回的回應？

您可以先檢查伺服器回應代碼，判斷是否已接受您的要求，以剖析回應。 如果傳回成功的回應代碼，您可以檢閱`responses`陣列物件以判斷擷取任務的狀態。

成功的單一訊息API要求會傳回狀態碼200。 成功（或部分成功）的批次訊息API請求傳回狀態碼207。

以下JSON是API要求的回應物件範例，其中含有兩條訊息：一條成功一條失敗。 成功串流的訊息傳回`xactionId`屬性。 無法串流的訊息傳回`statusCode`屬性以及包含更多資訊的回應`message`。

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

### 為什麼[!DNL Real-Time Customer Profile]未接收我的已傳送訊息？

如果[!DNL Real-Time Customer Profile]拒絕訊息，很可能是因為不正確的身分資訊。 這可能是由於為身分提供無效值或名稱空間所導致。

有兩種型別的身分識別名稱空間：預設和自訂。 使用自訂名稱空間時，請確定名稱空間已在[!DNL Identity Service]內註冊。 如需使用預設和自訂名稱空間的詳細資訊，請參閱[身分名稱空間概觀](../../identity-service/features/namespaces.md)。

您可以使用[[!DNL Experience Platform UI]](https://platform.adobe.com)檢視訊息擷取失敗原因的詳細資訊。 按一下左側導覽中的&#x200B;**[!UICONTROL 監視]**，然後檢視&#x200B;**[!UICONTROL 串流端對端]**&#x200B;標籤，以檢視在選取的時段內串流處理的訊息批次。
