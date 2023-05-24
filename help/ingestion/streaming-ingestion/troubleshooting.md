---
keywords: Experience Platform；主題；熱門主題；流；流；流；故障排除；流處理；故障排除；流處理；常見問題；faq;
solution: Experience Platform
title: 流式接收故障排除指南
description: 本文檔提供有關Adobe Experience Platform流式攝入的常見問題解答。
exl-id: 5d5deccf-25b8-44c9-ae27-9a4713ced274
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '1024'
ht-degree: 0%

---

# 流攝入故障排除指南

本文檔提供有關Adobe Experience Platform流式攝入的常見問題解答。 有關與其他相關的問題和故障排除 [!DNL Platform] 服務，包括在所有 [!DNL Platform] API，請參閱 [Experience Platform故障排除指南](../../landing/troubleshooting.md)。

Adobe Experience Platform [!DNL Data Ingestion] 提供了REST風格的API，您可以使用這些API將資料插入 [!DNL Experience Platform]。 所攝取的資料用於近即時更新單個客戶配置檔案，使您能夠跨多個渠道提供個性化的相關體驗。 請閱讀 [資料接收概述](../home.md) 的子菜單。 有關如何使用流式接收API的步驟，請閱讀 [流式處理概述](../streaming-ingestion/overview.md)。

## 常見問題集

以下是有關流式接收的常見問題的答案清單。

### 我如何知道發送的負載格式正確？

[!DNL Data Ingestion] 利用 [!DNL Experience Data Model] (XDM)架構，用於驗證傳入資料的格式。 發送不符合預定義XDM架構結構的資料將導致接收失敗。 有關XDM及其在 [!DNL Experience Platform]，請參見 [XDM系統概述](../../xdm/home.md)。

流式接收支援兩種驗證模式：同步和非同步。 每個驗證方法處理失敗資料的方式不同。

**同步驗證** 在開發過程中應使用。 驗證失敗的記錄會被刪除，並返回一條錯誤消息，說明失敗的原因(例如：&quot;XDM消息格式無效&quot;)。

**非同步驗證** 應用於生產。 未通過驗證的任何格式錯誤的資料都會發送到 [!DNL Data Lake] 作為失敗的批處理檔案，稍後可在其中檢索該檔案以供進一步分析。

有關同步和非同步驗證的詳細資訊，請參見 [流驗證概述](../quality/streaming-validation.md)。 有關如何查看驗證失敗的批的步驟，請參閱上的指南 [檢索失敗批](../quality/retrieve-failed-batches.md)。

### 能否在將請求負載發送到之前驗證它 [!DNL Platform]?

請求有效負載只有在發送到 [!DNL Platform]。 執行同步驗證時，有效負載返回填充的JSON對象，無效負載返回錯誤消息。 在非同步驗證期間，服務將檢測併發送任何格式錯誤的資料到 [!DNL Data Lake] 以後可以檢索到它以進行分析。 查看 [流驗證概述](../quality/streaming-validation.md) 的子菜單。

### 當在不支援同步驗證的邊緣上請求同步驗證時會發生什麼情況？

如果請求的位置不支援同步驗證，則返回501錯誤響應。 請參閱 [流驗證概述](../quality/streaming-validation.md) 的子菜單。

### 如何確保僅從受信任的源收集資料？

[!DNL Experience Platform] 支援安全的資料收集。 啟用經過身份驗證的資料收集後，客戶端必須將JSON Web令牌(JWT)及其組織ID作為請求標頭髮送。 有關如何將經過身份驗證的資料發送到的詳細資訊 [!DNL Platform]，請參閱上的指南 [經過驗證的資料收集](../tutorials/create-authenticated-streaming-connection.md)。

### 流資料到的延遲是什麼 [!DNL Real-Time Customer Profile]?

流式事件通常反映在 [!DNL Real-Time Customer Profile] 不到60秒。 實際延遲可能因資料量、消息大小和頻寬限制而有所不同。

### 我是否可以在同一API請求中包含多個消息？

您可以在單個請求負載內對多個消息進行分組，並將它們流式傳輸到 [!DNL Platform]。 正確使用時，在單個請求中對多個消息進行分組是優化資料操作的極好方法。 請閱讀有關 [在請求中發送多個消息](../tutorials/streaming-multiple-messages.md) 的子菜單。

### 我如何知道我發送的資料是否正在收到？

發送到的所有資料 [!DNL Platform] （成功或否）在保存到資料集之前，將作為批處理檔案儲存。 批處理的處理狀態顯示在發送到的資料集中。

通過使用 [Experience Platform用戶介面](https://platform.adobe.com)。 按一下 **[!UICONTROL 資料集]** 的子菜單。 從顯示清單中選擇要流式處理的資料集以開啟其 **[!UICONTROL 資料集活動]** 頁，顯示在選定時間段內發送的所有批。 有關使用的詳細資訊 [!DNL Experience Platform] 要監視資料流，請參見上的指南 [監視流資料流](../quality/monitor-data-ingestion.md)。

如果資料未能接收，並且您希望從 [!DNL Platform]，您可以通過將失敗的批發送到 [!DNL Data Access API]。 請參閱上的指南 [檢索失敗批](../quality/retrieve-failed-batches.md) 的子菜單。

### 為什麼我的流資料在資料湖中不可用？

批量攝取可能無法達到以下目的的原因有很多 [!DNL Data Lake]，例如格式無效、缺少資料或系統錯誤。 要確定批失敗的原因，必須使用 [!DNL Data Ingestion Service API] 並查看其詳細資訊。 有關檢索失敗批的詳細步驟，請參閱上的指南 [檢索失敗批](../quality/retrieve-failed-batches.md)。

### 如何分析為API請求返回的響應？

您可以通過首先檢查伺服器響應代碼來確定是否接受您的請求來解析響應。 如果返回成功的響應代碼，則可以查看 `responses` array對象以確定接收任務的狀態。

成功的單消息API請求返回狀態代碼200。 成功（或部分成功）批處理消息API請求返回狀態代碼207。

以下JSON是包含兩條消息的API請求的示例響應對象：一個成功，一個失敗。 成功流式傳輸的消息返回 `xactionId` 屬性。 無法流式傳輸的消息返回 `statusCode` 屬性和響應 `message` 的雙曲余弦值。

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

### 為什麼我的發送郵件未被 [!DNL Real-Time Customer Profile]?

如果 [!DNL Real-Time Customer Profile] 拒絕消息，很可能是由於身份資訊不正確所致。 這可能是為標識提供無效值或命名空間的結果。

有兩種類型的標識命名空間：預設和自定義。 使用自定義命名空間時，請確保已在中註冊了該命名空間 [!DNL Identity Service]。 查看 [標識命名空間概述](../../identity-service/namespaces.md) 的子菜單。

您可以使用 [[!DNL Experience Platform UI]](https://platform.adobe.com) 查看有關消息接收失敗原因的詳細資訊。 按一下 **[!UICONTROL 監視]** 在左導航中，然後查看 **[!UICONTROL 流式端到端]** 頁籤，查看在選定時間段內流式處理的郵件批。
