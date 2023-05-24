---
keywords: Experience Platform；主題；熱門主題；分段；分段；段；段；多實體；多實體分段；多實體分段；
solution: Experience Platform
title: 多實體分段概述
description: 多實體分段是指能夠根據產品、儲存或其他非配置檔案類使用附加資料擴展配置檔案資料。 連接後，來自其他類的資料將變為可用，就好像它們是配置檔案架構的本機資料。
exl-id: 01a37fdc-2abe-4a84-b7da-fcbd141ff51f
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '699'
ht-degree: 0%

---

# 多實體分割概述

多實體分割是Adobe Experience Platform的一個高級特徵 [!DNL Segmentation Service]。 此功能可擴展 [!DNL Real-Time Customer Profile] 包含您的組織可能定義的其他「非人員」資料（也稱為「維實體」）的資料，例如與產品或儲存相關的資料。 當基於與您獨特業務需要相關的資料定義受眾段時，多實體分段提供了靈活性，並且無需在查詢資料庫方面的專業知識即可執行。 使用多實體分段，您可以將關鍵資料添加到段中，而無需對資料流進行成本高昂的更改或等待後端資料合併。

## 快速入門

多實體分割需要對分割中涉及的Adobe Experience Platform各種服務進行工作理解。 在繼續閱讀本指南之前，請查看以下文檔：

* [[!DNL Real-Time Customer Profile]](../profile/home.md):根據來自多個源的聚合資料即時提供統一的用戶配置檔案。
   * [輪廓護欄](../profile/guardrails.md):建立受支援的資料模型的最佳做法 [!DNL Profile]。
* [[!DNL Adobe Experience Platform Segmentation Service]](./home.md):允許您從 [!DNL Real-Time Customer Profile] 資料。
* [[!DNL Experience Data Model (XDM)]](../xdm/home.md):Experience Platform組織客戶體驗資料的標準化框架。
   * [架構組合的基礎](../xdm/schema/composition.md#union):瞭解合成架構以用於Experience Platform的最佳做法。 為最好地利用分段，請確保根據 [資料建模的最佳做法](../xdm/schema/best-practices.md)。

## 使用案例

為了說明多實體細分的價值，請考慮三個標準市場營銷使用案例，這些案例說明了大多數市場營銷應用程式中存在的挑戰：

### 組合線上和離線採購資料

構建電子郵件市場活動的營銷人員可能試圖通過在過去三個月內使用最近的客戶商店採購為目標受眾構建市場細分。 理想情況下，此段要求同時提供採購所在商店的物料名稱和名稱。 以前，難題是從購買事件中捕獲儲存標識符並將其分配給單個客戶配置檔案。

### 電子郵件重新定位以放棄購物車

建立用戶並將用戶限定在針對購物車放棄的細分市場通常非常複雜。 瞭解哪些產品要納入個性化重新定位活動需要有關每個人放棄哪些產品的資料。 這些資料與以前難以監控和提取資料的商業事件有關。

## 建立多實體段

建立多實體段首先需要在使用 [!DNL Segmentation] API或段生成器UI，用於生成段定義。

### 定義關係

在「體驗資料模型」(XDM)架構的結構中定義關係是多實體段建立的一個組成部分。 對於關係，目標中的欄位需要標籤為該架構的主標識。 只能在字串上標籤標識，不能在陣列上標籤標識。 此外，由於您可以將配置檔案和體驗事件連接到多個目標，因此關係不一定需要一對一。

可以使用架構註冊表API或架構編輯器來定義關係。 有關如何定義兩個方案之間關係的詳細步驟，請從以下教程中選擇：

* [使用API定義兩個架構之間的關係](../xdm/tutorials/relationship-api.md)
* [使用架構編輯器UI定義兩個架構之間的關係](../xdm/tutorials/relationship-ui.md)

### 構建多實體段

一旦定義了必要的XDM關係，就可以開始構建多實體段。 可以使用分段API或段生成器UI來完成此操作。 有關詳細資訊，請從以下指南中選擇：

* [使用分段API建立段](./tutorials/create-a-segment.md)
* [使用段生成器UI建立段](./ui/overview.md)

## 評估和訪問多實體段

建立段後，可使用「分段API」評估和訪問段結果。 評估多實體段與評估標準段非常相似。 此過程只能使用分段API完成。 有關如何使用API評估和訪問段的詳細指南，請閱讀 [評估和訪問段](./tutorials/evaluate-a-segment.md) 教程。
