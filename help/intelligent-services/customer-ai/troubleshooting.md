---
keywords: Experience Platform；入門；客戶ai；熱門主題；客戶ai輸入；客戶ai輸出；客戶ai疑難排解；客戶ai錯誤
solution: Experience Platform, Intelligent Services, Real-time Customer Data Platform
title: 客戶人工智慧錯誤疑難排解
topic-legacy: Getting started
description: 在客戶人工智慧中尋找常見錯誤的解答。
type: Documentation
source-git-commit: ceb203899cda83aa79b994d45798d6147c3ff3b8
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 0%

---


# 客戶人工智慧錯誤疑難排解

當模型訓練、計分和配置失敗時，客戶人工智慧會顯示錯誤。 在&#x200B;**[!UICONTROL 服務實例]**&#x200B;部分中，**[!UICONTROL LAST RUN STATUS]**&#x200B;的列顯示以下消息之一：**[!UICONTROL Success]**、**[!UICONTROL 訓練課程]**&#x200B;和&#x200B;**[!UICONTROL Failed]**。

![上次運行狀態](./images/errors/last-run-status.png)

如果顯示&#x200B;**[!UICONTROL Failed]**&#x200B;或&#x200B;**[!UICONTROL Training issue]**，您可以選取執行狀態以開啟側面板。 側面板包含&#x200B;**[!UICONTROL 上次運行狀態]**&#x200B;和&#x200B;**[!UICONTROL 上次運行詳細資訊]**。 **[!UICONTROL 上次執行詳]** 細資訊包含執行失敗原因的資訊。如果客戶AI無法提供您錯誤的詳細資訊，請連絡支援部門，並提供錯誤碼。

<img src="./images/errors/last-run-details.png" width="300" /><br />

## 模型質量差

如果收到錯誤&quot;[!UICONTROL 「型號質量較差」。 我們建議使用已修改的設定]&quot;建立新應用程式。 請遵循下列建議步驟，協助疑難排解。

<img src="./images/errors/model-quality.png" width="300" /><br />

### 建議的修正

「模型質量差」意指模型精度不在可接受範圍內。 客戶AI在培訓後無法建立可靠的型號和AUC（ROC曲線下的區域）&lt; 0.65。 若要修正錯誤，建議您變更其中一個設定參數，然後重新執行訓練。

首先檢查資料的正確性。 您的資料必須包含預測結果所需的必要欄位。

- 檢查您的資料集是否有最新日期。 客戶人工智慧一律假設觸發模型時資料是最新的。
- 檢查您定義的預測和資格視窗中是否遺失資料。 您的資料必須完整無缺。 另請確定您的資料集符合[客戶AI歷史資料需求](./input-output.md#data-requirements)。
- 在您的架構欄位屬性中，檢查商務、應用程式、網頁和搜尋中是否遺失資料。

如果您的資料似乎不是問題所在，請嘗試變更資格人口狀況，將模型限制為特定描述檔（例如，`_experience.analytics.customDimensions.eVars.eVar142`存在於最近56天）。 這會限制訓練視窗中使用之資料的數量和大小。

如果限制資格人口無法運作或無法運作，請變更您的預測視窗。

- 嘗試將預測視窗變更為7天，並查看錯誤是否持續發生。 如果錯誤不再發生，這表示您可能沒有足夠的資料用於您定義的預測視窗。

