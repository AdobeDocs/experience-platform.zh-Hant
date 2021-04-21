---
keywords: Experience Platform；機器學習模型；資料科學工作區；即時客戶概要檔案；熱門主題；機器學習見解
solution: Experience Platform
title: 運用機器學習見解豐富即時客戶個人檔案
topic-legacy: tutorial
type: Tutorial
description: 本檔案提供如何運用機器學習見解豐富即時客戶個人檔案的指南。
exl-id: 397023c9-383d-4a21-b58a-0f920631ac56
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 0%

---

# 運用機器學習見解豐富[!DNL Real-time Customer Profile]內容

Adobe Experience Platform[!DNL Data Science Workspace]提供工具和資源來建立、評估和運用機器學習模型，以產生資料預測和洞見。 當機器學習見解被收錄到啟用[!DNL Profile]的資料集時，相同的資料也會被收錄為[!DNL Profile]記錄，然後可使用[!DNL Adobe Experience Platform Segmentation Service]加以分段。 當擷取描述檔和時間系列資料時，即時客戶描述檔會自動決定透過稱為串流分段的持續程式，將該資料加入或排除區段中，然後將其與現有資料合併並更新聯合檢視。 因此，您可以即時執行計算並做出決策，以便客戶在與品牌互動時提供增強的個人化體驗。

本檔案提供教學課程的連結，讓您運用機器學習的見解豐富[!DNL Real-time Customer Profile]內容。

## 快速入門

為完成下列教學課程，您必須對擷取[!DNL Profile]資料和建立區段有良好的認識。 在開始本教學課程之前，請先閱讀下列服務的檔案：

- [[!DNL Real-time Customer Profile]](../../profile/home.md):根據來自多個來源的匯整資料，為每位客戶提供完整、統一的呈現。
- [[!DNL Identity Service]](../../identity-service/home.md):借由 [!DNL Real-time Customer Profile] 將不同資料來源的身分橋接至平台，實現此目的。
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):平台組織客戶體驗資料的標準化架構。

除了上述文檔，強烈建議您還查看以下方案指南和方案編輯器：

- [架構構成基礎](../../xdm/schema/composition.md):介紹XDM架構、構建塊、原則和最佳做法，以合成要用於的架構 [!DNL Experience Platform]。
- [架構編輯器教程](../../xdm/tutorials/create-schema-ui.md):提供使用中的方案編輯器建立方案的詳細說明 [!DNL Experience Platform]。

## 建立和配置輸出模式和資料集{#create-an-output-schema-and-dataset}

透過計分見解豐富[!DNL Real-time Customer Profile]的第一步是瞭解您的資料所定義的真實對象（例如個人）。 瞭解資料後，您便能描述和設計可增加意義的結構，就像設計關係資料庫。

構成模式的開始方法是分配類。 類定義模式將包含的資料的行為方面（記錄或時間序列）。 要開始建立自己的方案，請按照[教程中的步驟使用方案編輯器](../../xdm/tutorials/create-schema-ui.md)建立方案。 請注意，在為[!DNL Profile]啟用資料集之前，您需要將資料集的模式配置為具有主標識欄位，然後為[!DNL Profile]啟用模式。 當資料被收錄至啟用[!DNL Profile]的資料集時，相同的資料也會被收錄為[!DNL Profile]記錄。

如果您偏好使用[!DNL Schema Registry] API來編寫架構，請先閱讀[[!DNL Schema Registry] 開發人員指南](../../xdm/api/getting-started.md)，再嘗試使用API](../../xdm/tutorials/create-schema-api.md)建立架構的教學課程。[

在您的架構和資料集準備完成後，您可以使用適當的模型執行計分執行，以產生計分資料並將計分資料收錄至資料集。

## 使用[!DNL Segment Builder] {#create-segments-using-the-segment-builder}建立區段

在您產生並將計分資料見解擷取至啟用[!DNL Profile]的資料集後，您可以使用[!DNL Segment Builder]建立動態區段。

[!DNL Segment Builder]提供豐富的工作區，可讓您與[!DNL Profile]資料元素互動。 工作區提供建立和編輯規則的直覺式控制項，例如用來表示資料屬性的拖放圖格。 請依照[[!DNL Segment Builder] 使用指南](../../segmentation/ui/segment-builder.md)瞭解：

- 使用屬性、事件和現有對象的組合來建立區段定義，做為建立區塊。
- 使用規則產生器畫布和容器來控制區段規則的執行順序。
- 檢視您潛在讀者的估計值，讓您視需要調整區段定義。
- 為排程的區段啟用所有區段定義。
- 為串流區段啟用指定的區段定義。

## 下一步 {#next-steps}

若要進一步瞭解區段和[!DNL Segment Builder]，請閱讀[區段服務概觀](../../segmentation/home.md)。

若要進一步瞭解[!DNL Real-time Customer Profile]，請閱讀[即時客戶資料概觀](../../profile/home.md)
