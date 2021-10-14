---
keywords: Experience Platform；快速入門；customer ai；熱門主題；customer ai輸入；customer ai輸出；customer ai疑難排解；customer ai錯誤
solution: Experience Platform, Intelligent Services, Real-time Customer Data Platform
feature: Customer AI
title: Customer AI錯誤疑難排解
topic-legacy: Getting started
description: 尋找Customer AI中常見錯誤的解答。
type: Documentation
exl-id: 37ff4e85-da92-41ca-afd4-b7f3555ebd43
source-git-commit: c3320f040383980448135371ad9fae583cfca344
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 0%

---

# Customer AI錯誤疑難排解

模型訓練、計分和設定失敗時，Customer AI會顯示錯誤。 在&#x200B;**[!UICONTROL Service instances]**&#x200B;區段中，**[!UICONTROL LAST RUN STATUS]**&#x200B;的列顯示以下消息之一：**[!UICONTROL Success]**、**[!UICONTROL 訓練問題]**&#x200B;和&#x200B;**[!UICONTROL Failed]**。

![上次運行狀態](./images/errors/last-run-status.png)

在顯示&#x200B;**[!UICONTROL Failed]**&#x200B;或&#x200B;**[!UICONTROL 培訓問題]**&#x200B;時，您可以選擇運行狀態以開啟側面板。 側面板包含您的&#x200B;**[!UICONTROL 上次運行狀態]**&#x200B;和&#x200B;**[!UICONTROL 上次運行詳細資訊]**。 **[!UICONTROL 上次運行詳]** 細資訊包含運行失敗原因的資訊。如果Customer AI無法提供您錯誤的詳細資訊，請聯絡支援人員，並提供錯誤代碼。

<img src="./images/errors/last-run-details.png" width="300" /><br />

## 模型質量差

如果您收到錯誤「[!UICONTROL 模型質量較差。 建議您使用已修改的設定]建立新應用程式。 請依照下列建議步驟協助疑難排解。

<img src="./images/errors/model-quality.png" width="300" /><br />

### 建議的修正

「模型質量差」表示模型精度不在可接受的範圍內。 培訓後，Customer AI無法建立可靠的模型，且AUC（ROC曲線下的區域）&lt; 0.65。 若要修正錯誤，建議您變更其中一個設定參數並重新執行訓練。

首先，檢查資料的準確性。 您的資料必須包含預測結果所需的必要欄位。

- 檢查您的資料集是否有最新日期。 Customer AI一律假設資料是觸發模型時的最新狀態。
- 檢查您定義的預測和資格窗口中是否缺少資料。 您的資料必須完整無缺。 另外，請確定您的資料集符合[ Customer AI歷史資料需求](./input-output.md#data-requirements)。
- 在您的架構欄位屬性中，檢查商務、應用程式、Web和搜尋中是否遺失資料。

如果您的資料似乎不是問題所在，請嘗試變更資格母體條件，將模型限制為特定設定檔（例如，`_experience.analytics.customDimensions.eVars.eVar142`存在於過去56天中）。 這會限制訓練視窗中所使用資料的母體和大小。

如果限制適用性母體無法運作或無法運作，請變更預測視窗。

- 嘗試將預測窗口更改為7天，查看錯誤是否繼續發生。 如果錯誤不再發生，表示您可能沒有足夠的資料用於定義的預測視窗。
