---
keywords: Experience Platform；首頁；熱門主題；分段；分段；區段服務；區段；區段；多實體；多實體分段；多實體區段；
solution: Experience Platform
title: 多實體區段概觀
description: 多實體分段是指根據產品、商店或其他非設定檔類別，以其他資料擴充設定檔資料的功能。 連線後，其他類別的資料就可供使用，就像它們是設定檔架構的原生資料。
exl-id: 01a37fdc-2abe-4a84-b7da-fcbd141ff51f
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '699'
ht-degree: 0%

---

# 多實體區段概觀

多實體分段是Adobe Experience Platform中提供的進階功能 [!DNL Segmentation Service]. 此功能可讓您擴充 [!DNL Real-Time Customer Profile] 含有貴組織可定義之其他「非人員」資料（也稱為「維度實體」）的資料，例如與產品或商店相關的資料。 多實體細分可根據與您的獨特業務需求相關的資料來定義受眾區段時，提供彈性，而且無需在查詢資料庫方面具備專業知識即可執行。 透過多實體細分，您可以將關鍵資料新增至區段，而無須對資料流進行成本高昂的變更，或等待後端資料合併。

## 快速入門

多實體細分需要各方切實了解細分中涉及的各種Adobe Experience Platform服務。 繼續閱讀本指南之前，請先檢閱下列檔案：

* [[!DNL Real-Time Customer Profile]](../profile/home.md):根據來自多個來源的匯總資料，即時提供統一的消費者設定檔。
   * [設定檔護欄](../profile/guardrails.md):建立資料模型的最佳實務，支援 [!DNL Profile].
* [[!DNL Adobe Experience Platform Segmentation Service]](./home.md):可讓您從 [!DNL Real-Time Customer Profile] 資料。
* [[!DNL Experience Data Model (XDM)]](../xdm/home.md):Experience Platform組織客戶體驗資料的標準化架構。
   * [結構構成基本概念](../xdm/schema/composition.md#union):了解合成結構以用於Experience Platform的最佳實務。 為了最能善用區段，請確定您的資料已根據 [資料模型最佳實務](../xdm/schema/best-practices.md).

## 使用案例

為了說明多實體細分的價值，請考慮三個標準行銷使用案例，說明大多數行銷應用程式中存在的挑戰：

### 結合線上和離線購買資料

建立電子郵件行銷活動的行銷人員可能已嘗試透過在過去三個月內使用最近的客戶商店購買項目來建立目標對象的區段。 理想情況下，此區段需要進行購買之商店的項目名稱和名稱。 以前，難題是從購買事件中擷取商店識別碼，並將其指派給個別客戶設定檔。

### 針對購物車放棄率的電子郵件重新鎖定

建立使用者並讓使用者進入以購物車放棄為目標的區段通常很複雜。 若要知道要在個人化重新定位促銷活動中包含哪些產品，需要有關個人已放棄哪些產品的資料。 此資料與商務事件相關，而之前這些事件在監控及擷取資料方面有挑戰。

## 建立多實體區段

建立多實體區段首先需要先定義結構之間的關係，再使用 [!DNL Segmentation] API或區段產生器UI來建立區段定義。

### 定義關係

在體驗資料模型(XDM)結構內定義關係是多實體區段建立的必要部分。 對於關係，目標中的欄位必須標示為該架構的主要身分。 身分只能在字串上標籤，不能在陣列上標籤。 此外，由於您可以將設定檔和體驗事件連結至多個目的地，因此關係不一定需要一對一。

可使用方案註冊表API或方案編輯器來定義關係。 如需如何定義兩個結構之間關係的詳細步驟，請從下列教學課程中選擇：

* [使用API定義兩個結構之間的關係](../xdm/tutorials/relationship-api.md)
* [使用結構編輯器UI定義兩個結構之間的關係](../xdm/tutorials/relationship-ui.md)

### 建立多實體區段

定義好必要的XDM關係後，您就可以開始建立多實體區段。 您可以使用「區段API」或「區段產生器UI」來完成此操作。 欲知更多資訊，請從以下指南中選擇：

* [使用區段API建立區段](./tutorials/create-a-segment.md)
* [使用區段產生器UI建立區段](./ui/overview.md)

## 評估及存取多實體區段

建立區段後，您可以使用區段API評估及存取區段結果。 評估多實體區段與評估標準區段非常類似。 此程式只能使用分段API來完成。 如需詳細指南，說明如何使用API評估及存取區段，請參閱 [評估和存取區段](./tutorials/evaluate-a-segment.md) 教學課程。
