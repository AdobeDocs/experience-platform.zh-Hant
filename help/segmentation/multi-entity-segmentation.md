---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;segment service;segments;Segments;multi-entity;multi-entity segmentation;multi-entity segments;
solution: Experience Platform
title: 多實體分段
topic: overview
description: 多實體分段是指能夠根據產品、商店或其他非描述檔類別，以額外資料擴充描述檔資料。 連線後，其他類別的資料就會變成描述檔架構的原生資料。
translation-type: tm+mt
source-git-commit: 8568c55003127a295acff9cfbbc3bbf6005e7a51
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 0%

---


# 多實體分段

多實體細分是Adobe Experience Platform的進階功能 [!DNL Segmentation Service]。 此功能可讓您以貴組織 [!DNL Real-time Customer Profile] 可能定義的額外「非人員」資料（也稱為「維度實體」）來擴充資料，例如與產品或商店相關的資料。 多實體細分可根據與您獨特業務需求相關的資料來定義受眾細分，而且無需具備查詢資料庫的專業知識即可執行。 透過多實體分段，您可以將關鍵資料新增至區段，而不需對資料串流進行昂貴的變更，或等待後端資料合併。

## 快速入門

多實體細分需要對細分中涉及的各種Adobe Experience Platform服務有良好的瞭解。 繼續使用本指南之前，請先閱讀下列檔案：

* [[!DNL即時客戶基本資料]](../profile/home.md):根據來自多個來源的匯總資料，即時提供統一的消費者個人檔案。
   * [描述檔護欄](../profile/guardrails.md):建立受支援資料模型的最佳實務 [!DNL Profile]。
* [[!DNL Adobe Experience Platform分段服務]](./home.md):可讓您從資料建立 [!DNL Real-time Customer Profile] 區段。
* [[!DNL體驗資料模型(XDM)]](../xdm/home.md):Experience Platform組織客戶體驗資料的標準化架構。
   * [架構構成基礎](../xdm/schema/composition.md#union):瞭解在Experience Platform中用於構成結構描述的最佳範例。

## 使用個案

為了說明多實體細分的價值，請考慮三個標準行銷使用案例，以說明大部分行銷應用程式面臨的挑戰：

### 結合線上和線下購買資料

建立電子郵件促銷活動的行銷人員可能會嘗試在過去三個月內使用最近的客戶商店購買來建立目標對象的區段。 理想情況下，此區段同時需要進行購買之商店的項目名稱和名稱。 以前，挑戰在於從購買事件中擷取商店識別碼，並將它指派給個別客戶個人檔案。

### 針對購物車放棄的電子郵件重新定位

建立使用者並將其限定為以放棄購物車為目標的群體通常很複雜。 瞭解個人化重新定位促銷活動中要包含哪些產品，需要有關個別放棄哪些產品的資料。 此資料與商務事件有關，而商務事件過去在監控及擷取資料方面十分困難。

## 建立多實體區段

建立多實體區段首先需要先定義結構之間的關係，然後才能使用 [!DNL Segmentation] API或區段產生器UI來建立區段定義。

### 定義關係

在體驗資料模型(XDM)架構的結構中定義關係是建立多實體區段的不可或缺部分。 此過程可以使用方案註冊表API或方案編輯器完成。 如需說明如何定義兩個結構之間的關係的詳細步驟，請從下列教學課程中選擇：

* [使用API定義兩個結構之間的關係](../xdm/tutorials/relationship-api.md)
* [使用架構編輯器UI定義兩個架構之間的關係](../xdm/tutorials/relationship-ui.md)

### 建立多實體區段

定義了必要的XDM關係後，就可以開始構建多實體段。 此程式可使用區段API或區段產生器UI來完成。 如需詳細資訊，請從下列指南中選擇：

* [使用區段API建立區段](./tutorials/create-a-segment.md)
* [使用區段產生器UI建立區段](./ui/overview.md)

## 評估並存取多實體區段

建立區段後，您可使用區段API來評估和存取區段結果。 評估多實體區段與評估標準區段非常類似。 此程式只能使用區段API來完成。 如需詳細指南，說明如何使用API評估和存取區段，請閱讀評估和存 [取區段教學課程](./tutorials/evaluate-a-segment.md) 。
