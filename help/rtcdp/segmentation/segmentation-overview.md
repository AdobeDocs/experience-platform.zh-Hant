---
keywords: 細分；細分rtcdp；即時客戶資料平台細分
title: Real-time Customer Data Platform中的分段服務
description: Adobe即時客戶資料平台是以Adobe Experience Platform為建置基礎，並運用許多Experience Platform服務和功能。 使用「細分服務」，您可以將客戶劃分為具有類似特徵的較小群組，借此提供量身打造的行銷。
exl-id: 140667c0-e288-40c4-8c45-c275e348b84a
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 4%

---

# [!DNL Segmentation Service]在 [!DNL Real-Time Customer Data Platform]

[!DNL Adobe Real-Time Customer Data Platform] (Real-Time CDP)可讓您從多個來源帶入資料，為客戶提供協調一致的體驗。 您可以使用 [!DNL Segmentation Service]，屬於Adobe Experience Platform。

Real-Time CDP建置在Adobe Experience Platform上，並運用許多 [!DNL Experience Platform] 服務和功能。 使用 [!DNL Segmentation Service]，您可以將客戶劃分為具有類似特徵的較小群組，借此提供量身打造的行銷。

## 區段

區段是定義設定檔存放區中一組設定檔子集所共用的特定屬性或行為的程式，以區分可行銷的一組人員和您的客戶群。 例如，在名為「您忘記購買運動鞋嗎？」的電子郵件行銷活動中，您可能想要有過去30天內搜尋跑鞋，但未完成購買的所有使用者的對象。 使用不同的區段，您可以專注於不同的受眾，提供更自訂的行銷體驗。

## [!DNL Segment Builder]

[!DNL Platform] 可讓您輕鬆建立和存取區段，並使用不同的建置區塊來進一步描述區段的特徵。 如需如何使用區段產生器的詳細資訊，請參閱 [區段產生器指南](./segment-builder-guide.md).

## Customer AI

Customer AI隨附於Real-time Customer Data Platform，可讓您在個別層級產生客戶預測並提供說明。

在影響因子的協助下，Customer AI 可告知您客戶可能會有什麼行為以及原因何在。 此外，您還可以受益於Customer AI預測和深入分析，提供最適當的選件和訊息，以個人化客戶體驗。 Customer AI可協助：

* 提供高準確度的客戶傾向模型，以便更強大的細分和鎖定目標。
* 了解特定客戶行為背後的影響因素和可能性。
* 為您公司獨特的使用案例和資料提供可自訂的選項。
* 利用客戶傾向分數（例如流失率和轉換）增強「即時客戶個人檔案」。
* 利用傾向分數的影響因素來增強客戶設定檔。
* 根據影響因素和傾向分數建立客戶區段。

Customer AI位於 **[!UICONTROL 服務]** 標籤 **[!UICONTROL Adobe服務]**.

![Customer AI位置](../assets/overview/rtcdp-customer-ai.png)

### Customer AI快速入門

若要開始使用Customer AI，您必須遵循 [資料準備教學課程](../../intelligent-services/data-preparation.md) 並根據您的使用案例設定輸入結構。 接下來，您需要 [設定Customer AI例項](../../intelligent-services/customer-ai/user-guide/configure.md). 設定例項後，會產生模型，您可在其中 [檢視您的分析和分數](../../intelligent-services/customer-ai/user-guide/discover-insights.md). 使用從模型產生的資料，您可以建立區段以進行資料導向啟動。

若要深入了解Customer AI，請先造訪 [Customer AI概觀](../../intelligent-services/customer-ai/overview.md). 此外，下列影片顯示客戶AI如何運用AI傾向豐富客戶個人檔案，以及執行客戶細分和目標定位工作。

>[!VIDEO](https://video.tv.adobe.com/v/40374/?quality=12&learn=on)


## 後續步驟

閱讀此概觀後，您現在應了解Real-Time CDP如何運用 [!DNL Segmentation Service] 以增強行銷活動的自訂和個人化。 如需 [!DNL Segmentation Service]，請閱讀 [區段檔案](../../segmentation/home.md).
