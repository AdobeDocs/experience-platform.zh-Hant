---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 多實體分段
topic: overview
translation-type: tm+mt
source-git-commit: bfbf2074a9dcadd809de043d62f7d2ddaa7c7b31
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 0%

---


# 多實體分段

多實體分段是指能夠根據產 [!DNL Profile] 品、商店或其他非描述檔類別，以額外資料擴充資料。 連線後，其他類別的資料就會變成架構的原生 [!DNL Profile] 資料。

若要進一步瞭解多實體細分，請繼續閱讀檔案，並透過觀看以下影片或探索細分概觀，來補充您 [的學習](./home.md)。]

>[!VIDEO](https://video.tv.adobe.com/v/28947?quality=12&learn=on)

## 快速入門

本教學課程需要對使用區段時涉及的各種Adobe Experience Platform服務有深入的瞭解。 在開始本教學課程之前，請先閱讀下列服務的檔案：

- [!DNL Real-time Customer Profile](../profile/home.md): 根據來自多個來源的匯總資料，即時提供統一的消費者個人檔案。
- [Adobe Experience Platform細分服務](./home.md): 可讓您從即時客戶個人檔案建立細分。
- [!DNL Experience Data Model (XDM)](../xdm/home.md): 組織客戶體驗資料 [!DNL Platform] 的標準化架構。

## 如何定義XDM關係

定義與(XDM)結構的關 [!DNL Experience Data Model] 系是區段建立的重要且不可或缺的一環。

此程式可使用 [!DNL Schema Registry] API或 [!DNL Schema Editor]。 有關使用API定義兩個方案之間關係的詳細說明，請閱 [讀有關使用API定義兩個方案之間關係的教程](../xdm/tutorials/relationship-api.md)。 有關使用定義兩個方案之 [!DNL Schema Editor] 間關係的詳細指南，請閱讀 [有關使用方案編輯器定義兩個方案之間關係的教程](../xdm/tutorials/relationship-ui.md)。

## 如何建立使用XDM關係的區段

定義XDM關係後，您就可以使用 [!DNL Segmentation Service] API來建立區段。

此程式可使用 [!DNL Segmentation] API或使用者介 [!DNL Segment Builder] 面完成。 如需使用API建立區段的詳細指南，請閱 [讀使用區段API建立區段的教學課程](./tutorials/create-a-segment.md)。 如需使用區段產生器建立區段的詳細指南，請閱 [讀區段產生器使用指南](./ui/overview.md)。

## 如何評估和存取多實體區段的區段

建立區段後，您可以使用 [!DNL Segmentation Service] API評估及存取區段結果。 評估多實體區段與評估一般區段非常類似。

此程式只能使用 [!DNL Segmentation Service] API完成。 如需使用API評估和存取區段的詳細指南，請閱讀評估和存取區段 [的教學課程](./tutorials/evaluate-a-segment.md)。