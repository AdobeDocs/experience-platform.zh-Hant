---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 即時客戶個人檔案教學課程
topic: tutorial
translation-type: tm+mt
source-git-commit: 5c5f6c4868e195aef76bacc0a1e5df3857647bde
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 0%

---


# 設定 [!DNL Real-time Customer Profile] 和 [!DNL Identity Service]

為了為您的組 [!DNL Real-time Customer Profile] 織進行設定，您必須完成多個不同的工作流程。 本檔案概述了相關步驟，並提供教學課程連結，以完成個別工作流程。 若要進一步了 [!DNL Real-time Customer Profile]解，請先閱讀描述 [檔概觀](../profile/home.md)。

## 為和啟用 [!DNL Profile] 模式 [!DNL Identity]

在可將資料收錄至Adobe Experience Platform並用於建立之前 [!DNL Real-time Customer Profiles]，必須先建立一個架構，以提供將要收錄之資料的結構，且該架構必須啟用，才能用於 [!DNL Profile] 和Adobe Experience Platform [!DNL Identity Service]。 有關建立同時啟用和的架構的逐步說明 [!DNL Profile][!DNL Identity Service]，請參閱使用「架構註冊表API」建立架構或使用「架構生成器UI [」](../xdm/tutorials/create-schema-api.md) 建立架構的教程 [](../xdm/tutorials/create-schema-ui.md)。

## 為和配置數 [!DNL Profile] 據集 [!DNL Identity]

若要開始將資料 [!DNL Profile]擷取至，您必須已正確設定資料集以便與和 [!DNL Real-time Customer Profile] 搭配使 [!DNL Identity Service]用。 若要開始，請依照設定 [資料集以進行描述檔和身分教學課程](../profile/tutorials/dataset-configuration.md)。

## 配置合併策略

Adobe Experience Platform可讓您從多個來源匯整資料並加以匯整，以全面瞭解每個客戶。 將這些資料整合在一起時，合併原則是用來決定 [!DNL Platform] 資料的優先順序以及將哪些資料合併以建立該統一檢視的規則。 使用REST風格的API或用戶介面，您可以建立新的合併策略、管理現有策略，並為組織設定預設的合併策略。 若要在UI中使用合併原則，請 [!DNL Platform] 造訪合併原 [則使用指南](../profile/ui/merge-policies.md)。 若要使用即時客戶設定檔API來處理合併原則，請參閱合 [並原則開發人員指南](../profile/api/merge-policies.md)。

## 設定邊緣投影

為即時跨多個通道為客戶提供協調、一致且個人化的體驗，需要隨時提供適當的資料，並在變更時持續更新。 Adobe [!DNL Experience Platform] 可透過使用所謂的邊緣來即時存取資料。 邊緣是地理位置優越的伺服器，可儲存資料，讓應用程式可輕鬆存取。 資料通過投影被路由到邊，投影目的地定義資料要發送到的邊，投影配置定義將在邊上提供的特定資訊。 如需詳細資訊以及開始使用邊緣，請參閱 [!DNL Real-time Customer Profile] API [邊緣投影子指南](../profile/api/edge-projections.md)。

## 後續步驟

在您為組織設 [!DNL Real-time Customer Profile] 定後，您就可以開始將資料新增至個別客戶個人檔案，並根據特定客戶屬性建立受眾細分。 若要開始使用，請參閱下列教學課程：

* [新增資料至即時客戶個人檔案](../profile/tutorials/add-profile-data.md)
* [建立區段](../segmentation/tutorials/create-a-segment.md)