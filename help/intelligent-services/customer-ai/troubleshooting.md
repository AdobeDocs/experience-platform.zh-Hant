---
keywords: Experience Platform；入門；客戶ai；熱門主題；客戶ai輸入；客戶ai輸出；客戶ai故障排除；客戶ai錯誤
solution: Experience Platform, Real-time Customer Data Platform
feature: Customer AI
title: 客戶AI錯誤疑難解答
description: 查找客戶AI中常見錯誤的答案。
type: Documentation
exl-id: 37ff4e85-da92-41ca-afd4-b7f3555ebd43
source-git-commit: 3bc750b5e1cf47cbca6b037d099936c80c926cf8
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 0%

---

# 客戶AI錯誤疑難解答

當模型培訓、評分和配置失敗時，客戶AI顯示錯誤。 在 **[!UICONTROL 服務實例]** 節，列 **[!UICONTROL 上次運行狀態]** 顯示以下消息之一： **[!UICONTROL 成功]**。 **[!UICONTROL 培訓問題]**, **[!UICONTROL 失敗]**。

![上次運行狀態](./images/errors/last-run-status.png)

如果 **[!UICONTROL 失敗]** 或 **[!UICONTROL 培訓問題]** 的子菜單。 側面板包含 **[!UICONTROL 上次運行狀態]** 和 **[!UICONTROL 上次運行詳細資訊]**。 **[!UICONTROL 上次運行詳細資訊]** 包含運行失敗原因的資訊。 如果客戶AI無法提供有關您的錯誤的詳細資訊，請與支援人員聯繫，並提供錯誤代碼。

<img src="./images/errors/last-run-details.png" width="300" /><br />

## 無法在Chrome Incognito中訪問客戶AI

由於GoogleChrome的隱藏模式安全設定中的更新，出現了在GoogleChrome的隱藏模式中載入錯誤。 該問題正在與Chrome一起積極研究，以使experience.adobe.com成為可信域。

<img src="./images/errors/error.PNG" width="500" /><br />

### 建議的修復

要解決此問題，您需要將experience.adobe.com添加為始終可以使用cookie的站點。 從導航開始 **chrome://settings/cookies**。 下一步，向下滾動到 **自定義行為** 部分，然後選擇 **添加** 按鈕「始終可以使用cookie的站點」。 在出現的跨距中，複製和貼上 `[*.]experience.adobe.com` 選擇 **包括第三方Cookie** 複選框。 完成後，選擇 **添加** 以隱藏方式重新載入客戶AI。

![建議修復](./images/errors/cookies2.gif)

## 模型質量差

如果收到錯誤&#39;&#39;[!UICONTROL 模型質量較差。 我們建議使用已修改的配置建立新應用]。 按照以下建議步驟幫助排除故障。

<img src="./images/errors/model-quality.png" width="300" /><br />

### 建議的修復

&quot;模型質量差&quot;是指模型精度不在可接受範圍內。 培訓後，客戶AI無法構建可靠的模型，AUC（ROC曲線下的區域）&lt; 0.65。 要修復錯誤，建議您更改其中一個配置參數並重新運行培訓。

首先檢查資料的準確性。 您的資料必須包含預測結果所需的必要欄位。

- 檢查您的資料集是否具有最新日期。 客戶AI始終假設觸發模型時資料是最新的。
- 檢查您定義的預測和資格窗口中是否缺少資料。 您的資料需要完成，而且不需要間隙。 同時確保您的資料集滿足 [客戶AI歷史資料要求](./data-requirements.md#data-requirements)。
- 檢查架構欄位屬性中商業、應用程式、Web和搜索中的缺失資料。

如果資料似乎不是問題所在，請嘗試更改資格填充條件以將模型限制為特定配置檔案(例如， `_experience.analytics.customDimensions.eVars.eVar142` 存在)。 這限制了在培訓窗口中使用的資料的數量和大小。

如果限制資格填充無效或不可能，請更改預測窗口。

- 嘗試將預測窗口更改為7天，並查看錯誤是否繼續發生。 如果錯誤不再發生，則表明您可能沒有足夠的資料用於定義的預測窗口。
